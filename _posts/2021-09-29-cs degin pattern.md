---
title:  "[CS] Design Pattern"
excerpt: "study Design Pattern "

categories:
- CS

toc: True
toc_sticky: True

date: 2021-09-29
last_modified_at: 2021-09-29
---

# Design Pattern

- 과거의 소프트웨어 개발 과정에서 발견된 설계의 노하우를 축적하여 그 방법에 이름을 붙여서 이후에 재사용하기 좋은 형태로 특정 규약을 만들어서 정리한 것
- 소프트웨어 설계에 있어 공통적인 문제들에 대한 표준적인 해법과 작명법을 제안하는 효율적인 코딩을 하기위한 방법론


<details>
<summary>Singleton patterns</summary>
<div markdown="1">
<br>

-  인스턴스를 여러 개 만들게 되면 자원을 낭비하게 되거나 버그를 발생시킬 수 있으므로 오직 하나만 생성하고 그 인스턴스를 사용하도록 하는 것이 이 패턴의 목적
- ex) 계산기 클래스를 만들고 필요할 때 마다 객체로 불러서 계산 -> 계산할 때 마다, 객체를 생성할 필요 없으므로 시간 및 메모리 사용률 절약 가능

```python
# singleton 클래스 만들기
class Singleton(type):
  __instances = {} # 클래스의 인스턴스를 저장할 속성
  def __call__(cls, *args, **kwargs): # 클래스로 인스턴스를 만들 때 호출되는 메서드
    if cls not in cls.__instances: # 인스턴스를 생성하지 않았다면 인스턴스를 생성하여 해당 클래스 사전에 저장
      cls.__instances[cls] = super().__call__(*args,**kwargs)
    return cls.__instances[cls]



```

</div>
</details>

