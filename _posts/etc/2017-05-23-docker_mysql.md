---
layout: post
title:  "Docker mysql 설치"
date:   2017-05-23 13:16:54 +0900
categories: etc
permalink: /etc/:year/:month/:day/:title/
tags: [도커, Docker, mysql]
comments: true
---

## Docker

### docker machine 생성(터미널 접속)
- docker-machine
- docker-machine create —driver virtualbox 머신이름 : docker머신 생성
- docker-machine start 머신이름 : docker데몬이 연결이 안될 때 머신 이름으로 시작한다

### docker 명령어
- docker search 이미지 검색
- docker pull mysql 최신 버전의 mysql이 설치된 ubuntu리눅스 이미지 다운 받기


```
docker-machine create —driver virtualbox 머신이름

docker pull mysql

docker run --name mysql -e MYSQL_ROOT_PASSWORD=mypass -d -p 3306:3306 mysql

docker exec -it docker이름 /bin/bash

apt-get update

apt-get install net-tools

```

### docker tool를 사용했을 때 문제 발생
- 로컬에서 docker-tools를 통해 설치된 mysql에 접속을 할수 없다.
- docker 자체 ip가 아닌 docker-machine의 ip로 접속해야 한다.
- container 를 생성하면 기본적으로 외부와 통신이 불가능한 상태이다. 따라서 외부와 통신을 위해서는 container를 외부로 노출할 Port를 지정해야한다. 노출할 port를 지정하는 방법은 container 를 생성할때 -p option을 이용하면 된다. 
