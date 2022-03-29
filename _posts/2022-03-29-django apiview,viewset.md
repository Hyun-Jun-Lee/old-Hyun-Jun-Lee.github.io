---
title:  "[DRF] APIView, Mixins, APIView"
excerpt: "APIView, Mixins, APIView"

categories:
- Django

toc: True
toc_sticky: True

date: 2022-03-29
last_modified_at: 2022-03-29
---

# [DRF] APIView, Mixins, APIView

```python
# serializers.py

class PostSerializer(serializers.ModelSerializer):
    class Meta:
        model = Post
        fields = '__all__'
        
# views.py

serializer = PostSerializer(data=request.POST)
if serializer.is_valid():
    serializer.save()
    return JsonResponse(serializer.data, status=201)
return JsonResponse(serializer.errors, status=400)
```

DRF의 serializer는 기존 Django Form과 유사하고 Modelserializer는 ModelForm과 유사하다. 

차이점은 `Form은 HTML`을 생성하고 `Serizlizer는 JSON 문자열`을 생성 한다는 것!
