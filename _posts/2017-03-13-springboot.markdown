---
layout: post
title:  "Docker start"
date:   2017-03-13 14:08:54 +0900
categories: jekyll update
---
Docker
Docker tool 설치
터미널 접속
- docker-machine
- docker-machine create —driver virtualbox default : docker머신 생성
- docker-machine ls : 현재 생성된 docker 머신 목록
- docker-machine ip
- docker-machine env docker이름
- docker images : 현재 로컬에 생성된 이미지 목록
- eval $(docker-machine env docker이름) : 기본 이미지 세팅 docker데몬에 연결이 안될때
- docker pull ubuntu
- docker image repository 검색
- docker images : 현재 로컬에 있는 이미지 목록
- docker run -name 이름 ubuntu
- docker rm run된이름 : run되고 있는 이미지 삭제
- docker run -dit -name 데몬이름 이미지이름
- docker start 데몬이름 : 데몬 시작
- docker stop 데몬이름 : 데몬 중지

- docker ps -a
- docker stop 이름
- docker exec -it 이름 /bin/bash

'RUN locale-gen ko_KR.UTF-8
ENV LANG ko_KR.UTF-8
ENV LANGUAGE ko_KR.UTF-8
ENV LC_ALL ko_KR.UTF-8

CMD /bin/bash'

docker build —tag ko\_ubuntu:latest ./
docker run -it  —name ko\_ubutu ko\_ubuntu /bin/bash
-> kor\_ubuntu 이미지로 docker  ko\_ubuntu 이름으로 docker 실행하며 bash로 쉘로 로그인 한다
docker exec -it docker실행이름

Docker 이미지 만들기
- locale
- docker start 이미지 이름

Java 설치
- ubuntu 에서 java 자동 설치 : apt-get install java
- ubuntu 에서 java 수동 설치
- wget --header "Cookie: oraclelicense=accept-securebackup-cookie" [http://download.oracle.com/otn-pub/java/jdk/8u5-b13/jdk-8u5-linux-x64.tar.gz]
- 압축풀기 : tar -xvf 파일명
- ln -s jdk1.8.0\_05/ java : 실볼릭 링크 만들기
- 쿠기 설정 후 다운로드
- 다운 로드 된 압축 파일 압축 해제
- cd \~ : home directory 로 이동
- ls -al : directory 내의모든 파일 확인
- vim 설치 : apt-get install vim
- .bash.profile 설정 : JAVA\_HOME =/usr/apps/java
- source 명령어 : 로그아웃하지 않고도 환경설정 반영됨

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
