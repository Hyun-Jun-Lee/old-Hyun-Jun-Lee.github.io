---
title:  "Dockerfile"
excerpt: "docker"

categories:
- Docker

toc: True
toc_sticky: True

date: 2022-03-31
last_modified_at: 2022-03-31
---

# Dockerfile

Dockerfile은 dockerimage를 생성하기 위한 설정파일로, 여러가지 명령어를 토대로 작성한 후 build하면 Dockerfile은 나열된 명령문을 차례대로 수행하여 dockerimage를 생성해준다. 

- 장점
  - 이미지 생성 과정을 기록함
    - dockerfile을 보면 이미지가 어떻게 구성되었는지 파악하기 쉽다
  - 배포에 용이
    - 용량이 큰 이미지 파일 자체를 배포하기 보다, 그 이미지를 만들 수 있는 스크립트인 dockerfile만 배포하면 된다.

## 작성법

파일 이름을 'Dockerfile'로 해야한다. (확장자 따로 없음!)

```python
# docker 환경에서 사용할 python 버전
From python:3.8

# image가 올라갔을 때 수행되는 명령어들
# -y 옵션을 넣어서 무조건 설치가 가능하도록 한다.
RUN \
    apt-get update && \
    apt-get install -y django

#docker안에서 srv/docker-server 폴더 생성
RUN mkdir /srv/docker-server 
#현재 디렉토리를 통째로 srv/docker-server폴더에 복사
ADD . /srv/docker-server 

#작업 디렉토리 설정
WORKDIR /srv/docker-server 

RUN pip install --upgrade pip #pip 업그레이드
RUN pip install -r requirements.txt #필수 패키지 설치

# Dockerfile의 빌드로 생성된 이미지에서 열어줄 포트 설정(테이너 생성 시 -p 옵션의 컨테이너 포트 값)
EXPOSE 8000
# 컨테이너 생성, 실행할 때 같이 실행할 명령어
CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]
```

- 생성한 Dockerfile을 image 빌드
  - `docker build -t [이미지 이름:이미지 버전] [dockerfile 경로]`

- image로 Container 생성
  - `docker run --name [컨테이너이름] -d -p [호스트포트]:[컨테이너포트] -v []`
  - --name : 컨테이너 이름
  - -d : 백그라운드 모드로 실행
  - -p : [호스트포트]:[컨테이너포트] 포트 연결
  - -v : 로컬과 컨테이너 파일 연동