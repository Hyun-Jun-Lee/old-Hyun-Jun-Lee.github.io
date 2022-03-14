---
title:  "[Django] Generic Display Views"
excerpt: "DetailView, ListView"

categories:
- Django

toc: True
toc_sticky: True

date: 2022-03-14
last_modified_at: 2022-03-14
---

# [Django] Generic Display Views

<a href="https://github.com/django/django">Django 소스코드</a>

## DetailView

`DetailView`는 아무 내용 없이 `SingleObjectTemplateResponseMixin`,`BaseDetailView` 두 개의 클래스를 상속 받는다.

1. BaseDetailView

```python
class BaseDetailView(SingleObjectMixin, View):
    """A base view for displaying a single object."""

    def get(self, request, *args, **kwargs):
        self.object = self.get_object()
        context = self.get_context_data(object=self.object)
        return self.render_to_response(context)
```

get 요청에 대해 DB에서 하나의 object를 가져와서 context에 담아 rendering 한다. 그리고 `SingleObjectMixin` class를 상속받는다.

- SingleObjectMixin

```python
class SingleObjectMixin(ContextMixin):
    """
    Provide the ability to retrieve a single object for further manipulation.
    """

    model = None
    queryset = None
    slug_field = "slug"
    context_object_name = None
    slug_url_kwarg = "slug"
    pk_url_kwarg = "pk"
    query_pk_and_slug = False

    def get_object(self, queryset=None):
        """
        Return the object the view is displaying.
        Require `self.queryset` and a `pk` or `slug` argument in the URLconf.
        Subclasses can override this to return any object.
        """
        # Use a custom queryset if provided; this is required for subclasses
        # like DateDetailView
        if queryset is None:
            queryset = self.get_queryset()

        # Next, try looking up by primary key.
        pk = self.kwargs.get(self.pk_url_kwarg)
        slug = self.kwargs.get(self.slug_url_kwarg)
        if pk is not None:
            queryset = queryset.filter(pk=pk)

        # Next, try looking up by slug.
        if slug is not None and (pk is None or self.query_pk_and_slug):
            slug_field = self.get_slug_field()
            queryset = queryset.filter(**{slug_field: slug})

        # If none of those are defined, it's an error.
        if pk is None and slug is None:
            raise AttributeError(
                "Generic detail view %s must be called with either an object "
                "pk or a slug in the URLconf." % self.__class__.__name__
            )

        try:
            # Get the single item from the filtered queryset
            obj = queryset.get()
        except queryset.model.DoesNotExist:
            raise Http404(
                _("No %(verbose_name)s found matching the query")
                % {"verbose_name": queryset.model._meta.verbose_name}
            )
        return obj

    def get_queryset(self):
        """
        Return the `QuerySet` that will be used to look up the object.
        This method is called by the default implementation of get_object() and
        may not be called if get_object() is overridden.
        """
        if self.queryset is None:
            if self.model:
                return self.model._default_manager.all()
            else:
                raise ImproperlyConfigured(
                    "%(cls)s is missing a QuerySet. Define "
                    "%(cls)s.model, %(cls)s.queryset, or override "
                    "%(cls)s.get_queryset()." % {"cls": self.__class__.__name__}
                )
        return self.queryset.all()

    def get_slug_field(self):
        """Get the name of a slug field to be used to look up by slug."""
        return self.slug_field

    def get_context_object_name(self, obj):
        """Get the name to use for the object."""
        if self.context_object_name:
            return self.context_object_name
        elif isinstance(obj, models.Model):
            return obj._meta.model_name
        else:
            return None

    def get_context_data(self, **kwargs):
        """Insert the single object into the context dict."""
        context = {}
        if self.object:
            context["object"] = self.object
            context_object_name = self.get_context_object_name(self.object)
            if context_object_name:
                context[context_object_name] = self.object
        context.update(kwargs)
        return super().get_context_data(**context)
```

- `pk_url_kwargs`, `slug_url_kwarg` : default 값으로 pk와 slug가 지정되있다. 이것은 urls에서 넘겨주는 인자의 이름을 뜻한다.
    ```python
    # pk를 id로 바꾸려면 아래와 같이 설정

    # urls.py
    urlpatterns = [
        path('<int:id>', views.post_detail, name="post_detail"),
    ]

    # views.py

    post_detail = DetailView.as_view(model=Post, pk_url_kwarg='id')
    ```

- `get_object` : 모델에서 object를 받아오는 메서드. 지정한 클래스 변수들에 대해서 queryset, pk, slug을 설정해서 queryset을 만들어 주고 이를 통해 모델에서 객체를 가져오고 실패할 경우 에러를 일으킨다.

- `get_queryset` : 기본 값으로 모델의 모든 객체를 반환하지만, queryset이 지정되있는 경우 그에 맞게 객체를 반환한다.

2. SingleObjectTemplateResponseMixin

`template_name`을 따로 지정해주면 그에 따른 templates를 반환해준다. default 값은 `앱이름/모델이름_detail.hrml`로 지정되있다.

## ListView

`ListView`는 1개의 모델을 list 템플릿 처리를 한다. 그리고 자동으로 페이징 처리를 지원하고 `모델이름_list`의 queryset을 templates에 전달한다. 

```html
<!-- core/post_list.html -->

<h1>list 페이지</h1>

{% for post in post_list %}
    <div>{{post.title}}</div>
    <div>{{post.content}}</div>
{% endfor %}
```

### 살펴보기

`ListView`도 아무 내용 없이 `MultipleObjectTemplateResponseMixin` 와 `BaseListView` 를 상속받는다.

- BaseListView

```python
class BaseListView(MultipleObjectMixin, View):
    """A base view for displaying a list of objects."""

    def get(self, request, *args, **kwargs):
        self.object_list = self.get_queryset()
        allow_empty = self.get_allow_empty()

        if not allow_empty:
            # When pagination is enabled and object_list is a queryset,
            # it's better to do a cheap query than to load the unpaginated
            # queryset in memory.
            if self.get_paginate_by(self.object_list) is not None and hasattr(
                self.object_list, "exists"
            ):
                is_empty = not self.object_list.exists()
            else:
                is_empty = not self.object_list
            if is_empty:
                raise Http404(
                    _("Empty list and “%(class_name)s.allow_empty” is False.")
                    % {
                        "class_name": self.__class__.__name__,
                    }
                )
        context = self.get_context_data()
        return self.render_to_response(context)
```

get요청을 받아서 queryset으로 object_list를 만들어 준다.

- MultipleObjectMixin

