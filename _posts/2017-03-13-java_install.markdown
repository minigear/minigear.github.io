---
layout: post
title:  "Java 설치 (ubuntu)"
date:   2017-03-13 14:08:54 +0900
categories: jekyll update
---
### Java 설치
- ubuntu 에서 java 자동 설치 : apt-get install java
- ubuntu 에서 java 수동 설치
- wget 을 설치 : apt-get install wget
- wget --header "Cookie: oraclelicense=accept-securebackup-cookie" [http://download.oracle.com/otn-pub/java/jdk/8u5-b13/jdk-8u5-linux-x64.tar.gz]
- 압축풀기 : tar -xvf 파일명
- ln -s jdk1.8.0\_05/ java : 실볼릭 링크 만들기
- 쿠기 설정 후 다운로드
- 다운 로드 된 압축 파일 압축 해제
- cd \~ : home directory 로 이동
- ls -al : directory 내의모든 파일 확인
- vim 설치 : apt-get install vim
- .bash_profile 설정 :
```
JAVA\_HOME =/usr/apps/java
PATH=$PATH:$JAVA_HOME/bin
```
- source 명령어 : 로그아웃하지 않고도 환경설정 반영됨
```
source .bash_profile
```
<!-- This loops through the paginated posts -->
{% for post in paginator.posts %}
<h1><a href="{{ post.url }}">{{ post.title }}</a></h1>
<p class="author">
  <span class="date">{{ post.date }}</span>
</p>
<div class="content">
  {{ post.content }}
</div>
{% endfor %}

<!-- Pagination links -->
<div class="pagination">
{% if paginator.previous_page %}
  <a href="{{ paginator.previous_page_path }}" class="previous">Previous</a>
{% else %}
  <span class="previous">Previous</span>
{% endif %}
<span class="page_number ">Page: {{ paginator.page }} of {{ paginator.total_pages }}</span>
{% if paginator.next_page %}
  <a href="{{ paginator.next_page_path }}" class="next">Next</a>
{% else %}
  <span class="next ">Next</span>
{% endif %}
</div>
