---
layout: post
title:  "Java install (ubuntu)"
date:   2017-03-13 14:08:54 +0900
categories: jekyll update
---
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
