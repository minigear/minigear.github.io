---
layout: post
title:  "오라클 코드 토비님 발표"
date:   2017-08-30 14:08:54 +0900
categories: etc
permalink: /etc/:year/:month/:day/:title/
tags: [세미나, 토비, 자바, JAVA, 스프링]
comments: true
---

#### 토비님 발표
-----
###### 1. 자바는 죽었나?
팩트체크 결과 아직 수요가 많다.   

-----
###### 2. 위기와 변화
- 1차 위기 과도한 기술 복잡해짐, EJB  
    - 대안 : 자바와 객체지향의 기본으로 돌아간다 -> POJO, J2EE Development without EJB
- 2차 위기 언어 발전의 요구와 호환성
    - 언어의 발전과 함께 코드 호환성도 지킨다. 플렛폼이 바뀌어도 빌드하지 않고 재사용할 수 있다.
- 3차 위기 간결한 코드와 관례로 무장한 언어와 기술의 습격
    - 간결한 짧은 언어
    - 설정을 최소하고 관례를 우선하는 프레임워크
    - 엔터프라이즈 개발도 루비와 레일즈로 프레임워크
    - 해결책 : 애노테이션 기반의 메타프로그래밍과 영리한 디폴트로 무장한 관례의 적극 도입
- 4차 위기 함수형 프로그래밍과 비동기 논블록킹 개발의 도전
    - 스칼라
    - 대용량 비동기 분산시스템 개발에 적함한 함수형 프로그래밍 필요성 대두
    - 해결책 : 함수형 프로그래밍 스타일의 자바와 비동기 논블록킹 지원 서블릿, 스프링 등장

----
###### 3. 새로운 변화 : 자바9와 스프링5   
- 새로운 위기 : **애노테이션과 메타프로그래밍, 관례의 범람**
  - 앤노테이션의 한계와 부작용   
    - 컴파일러에 의해 검증 가능한 타입이 아님
    - 코드의 행위를 규정하지 않음
    - 상속, 확장 규칙의 표준이 없음
    - 이해하기 어려운 코드, 오해하기 쉬운 코드 가능성
    - 테스트가 어렵거나 불가능함
    - 커스트마이징하기 어려움   

  - 리플렉션과 런타임 바이트코드 생성의 문제
    - 성능저하
    - 타입정보 제거
    - 디버깅 어려움
    - 툴이나 컴파일러에 의한 검증불가  

---

- 대안 : **업그레이드된 자바의 기본으로 돌아간다.**  
  - 함수형 프로그래밍이 도입된 자바의 기본으로 돌아가자
  - 함수형 스타일의 자바 웹 코드로 전환
    - 애노테이션과 리플랙션 제거
    - 명시적 코드로 모든 기능을 표현
    - 불변객체 사용
    - 함수의 조합을 이용
    - 리액티브
  - 스프링 5.0 - 새로운 함수형 스타일 웹 개발 지원
  - 서블릿의 의존성 제거
    - 서블릿 컨테이너를 비동기 HTTP서버로 활용가능
  - 새로운 HTTP요청과 응답의 추상화 - 불변 객체
    - ServerRequest
    - ServerResponse
  - 두 개의 함수를 이용해 개발
    - HandlerFunction
    - RouterFunction
  - Mono<T>, Flux<T> 리액티브 방식
  - 스프링 5.0- 함수형 스타일 애플리케이션
    - 독립형애플리케이션
    - 스프링 컨테이너 이용
  - 웹 핸들러(컨트롤러)가 웹 요청 처리하는 방식
    - 요청매핑
    - 요청 바인딩
    - 핸들러 실행
    - 핸들러 결과 처리(응답 생성)   
  - 함수형 웹 개발
    - 람다식-메소드 상호 호환 - 메소드 레퍼런스
    - 핸들러를 람다식 대신 메소드로 작성할 수 있음
    - 기능 종류에 따라 클래스-메소드로 구조화
    - 함수의 조합   

람다식과 같은 형식의 메소드 타입
  ``` java8
  HandlerFunction helloHandler = (ServerRequest req)-> {
    String name = req.pathVariable("name");
    return ServerResponse.ok().syncBody("Hello"+name);
  };

  public Mono<ServerResponse> helloHandler(ServerRequest) {
    String name = req.pathVariable("name");
    return ServerResponse.ok().syncBody("Hello"+name);
  }
  ```
메소드 형태로 재작성된 핸들러, 라우터함수   
``` java8
Mono<ServerResponse> helloHandler(ServerRequest req) {
  String name = req.pathVariable("name");
  return ServerResponse.ok().syncBody("Hello" + name);
}

Mono<HandlerFunction<ServerResponse>> router(ServerRequest req) {
  return RequestPredicates.path("/hello/{name}").test(req)?
    Mono.just(this::helloHandler):Mono.empty();
}

void run() throws IOException {
  HttpHandler httpHandler = RouterFunctions.toHttpHandler(this::router);
}
```
함수형 웹개발 - 함수의 조합
핸들러를 메소드로 모아 놓은 클래스
``` java8
  public class PersonHandler {
    private final PersonRepository repository;
    public PersonHandler(PersonRepository repository) { this.repository = repository; }

    public Mono<ServerResponse> getPerson(ServerRequest request) {
      int personId = integer.valueOf(request.pathVariable("id"));
      Mono<Person> personMono = this.repository.getPerson(personId);
      return personMono
        .flatMap(person->
          ServerResponse.ok().contentType(APPLICATION_JSON).body(fromObject(person))).switchIfEmpty(ServerResponse.notFound().build());
    }

    public Mono<ServerResponse> savePerson(ServerRequest request) {
      Mono<Person> person = request.bodyToMono(Person.class);
      return ServerResponse.ok().build(this.repository.savePerson(person));
    }
  }
```

Mono   
ReactiveStreams의 publisher 타입   
웹요청, 웹 응답, 핸들러, 라우터 등의 모든 함수에 적용

Mono - RouterFunction
```java8
  @FunctionalInterface
  public interface RouterFunction<T extends ServerResponse> {
    Mono<HandlerFunction<T>> route(ServerRequest request);
  }
```

##### Mono/Flux
 -  정보를 전달할 때 컨테이너 사용
  - Mono - 단일 오브젝트
  - Flux - 스트림 오브젝트
- 데이터 가공, 변환, 조합을 위한 다양한 연산 제공
- 스케쥴러를 이용해 비동기 작업 수행
- 지연 연산, 자유로운 조합
- 스프링 함수형 웹 개발의 모든 기능이 Mono/Flux 기반으로 재개발
- 리액트비 프로그래밍 기반
  - ProjectReactor
  - RxJava
- 함수형 웹 개발 외의 전 계층에 적용 가능
  - 서비스, 리포지토리, API 호출
  - 대부분의 스프링 서브 프로젝트에 적용 중
- 비동기 논블록킹 방식으로 동작하는 고성능 코드
- 함수형 스타일의 코드

##### JavaSE9 - Flow API와 ReactiveStreams
 - Flow API는 ReactiveStreams 표준과 호환
 - 스프링 Mono/Flux - Java 9의 Flow API를 함께 사용해서 개발 가능
 - 자바9의 Flow API가 많은 기술의 브릿지 역할을 담당

##### 스프링5 함수형 웹 개발은 다양한 방식으로 가능
  - 순수 함수형 독립형
  - 순수 함수형 애플리케이션 코드 + 자바설정(@)
  - 하이브리드 함수형 애플리케이션 코드(@)
