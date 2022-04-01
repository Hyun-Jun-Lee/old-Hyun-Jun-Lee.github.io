---
title:  "[Django] Access Mixins"
excerpt: "Access Mixins"

categories:
- Django

toc: True
toc_sticky: True

date: 2022-04-02
last_modified_at: 2022-04-02
---

# [DRF] Access Mixins

- 소스코드 : https://github.com/django/django/blob/main/django/contrib/auth/mixins.py
- document : https://docs.djangoproject.com/en/4.0/topics/auth/default/

## AccessMixin

```python
class AccessMixin:
    """
    Abstract CBV mixin that gives access mixins the same customizable
    functionality.
    """
    # default로 get_login_url() 값을 반환한다(settings.LOGIN_URL)
    login_url = None
    permission_denied_message = ""
    # True 설정시 PermissionDenied exception 반환
    raise_exception = False
    redirect_field_name = REDIRECT_FIELD_NAME

    def get_login_url(self):
        """
        Override this method to override the login_url attribute.
        """
        login_url = self.login_url or settings.LOGIN_URL
        if not login_url:
            raise ImproperlyConfigured(
                f"{self.__class__.__name__} is missing the login_url attribute. Define "
                f"{self.__class__.__name__}.login_url, settings.LOGIN_URL, or override "
                f"{self.__class__.__name__}.get_login_url()."
            )
        return str(login_url)

    def get_permission_denied_message(self):
        """
        Override this method to override the permission_denied_message attribute.
        """
        return self.permission_denied_message

    def get_redirect_field_name(self):
        """
        Override this method to override the redirect_field_name attribute.
        """
        return self.redirect_field_name

    def handle_no_permission(self):
        if self.raise_exception or self.request.user.is_authenticated:
            raise PermissionDenied(self.get_permission_denied_message())

        path = self.request.build_absolute_uri()
        resolved_login_url = resolve_url(self.get_login_url())
        # If the login url is the same scheme and net location then use the
        # path as the "next" url.
        login_scheme, login_netloc = urlparse(resolved_login_url)[:2]
        current_scheme, current_netloc = urlparse(path)[:2]
        if (not login_scheme or login_scheme == current_scheme) and (
            not login_netloc or login_netloc == current_netloc
        ):
            path = self.request.get_full_path()
        return redirect_to_login(
            path,
            resolved_login_url,
            self.get_redirect_field_name(),
        )
```

대부분의 인증 관련 mixins에 상속되어 사용된다.

## UserPassesTextMixin

```python
class UserPassesTestMixin(AccessMixin):
    """
    text_fucn() method가 False를 리턴하면 permission error와 함께 요청을 거절한다
    """

    def test_func(self):
        raise NotImplementedError(
            "{} is missing the implementation of the test_func() method.".format(
                self.__class__.__name__
            )
        )

    def get_test_func(self):
        """
        text_func를 customize 할 때 사용
        """
        return self.test_func

    def dispatch(self, request, *args, **kwargs):
        user_test_result = self.get_test_func()()
        if not user_test_result:
            return self.handle_no_permission()
        return super().dispatch(request, *args, **kwargs)
```

- 활용 예시

```python
class LoggedOutOnlyView(UserPassesTestMixin):
    def test_func(self):
        return not self.request.user.is_authenticated

    def handle_no_permission(self):
        messages.error(self.request, "Can't go there")
        return redirect("core:home")
```

## LoginRequiredMixin

```python
# 인증되지 않은 유저의 request를 login_url로 보내거나 HTTP 403 Forbidden error를 보여준다. 
class LoggedInOnlyView(LoginRequiredMixin):

    login_url = reverse_lazy("users:login")

```