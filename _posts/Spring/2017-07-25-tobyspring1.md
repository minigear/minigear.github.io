---
layout: post
title:  "Toby 스프링3 1장"
date:   2017-08-25 12:36:00 +0900
categories: [Spring]
permalink: /spring/:year/:month/:day/:title/
tags: [스프링, spring]
comments: true
---

## 오브젝트와 의존관계
  - 초난감 DAO
    - Extract method
  - DAO 의 분리
    - Template method pattern
    - Factory method pattern :
        객체를 생성하기 위한 interface 를 정의 하는데, 어떤 class의 instance를 만들지 subclass에서 결정하게 만든다
    -  과심사의 분리

  - DAO 확장
      - 클래스의 분리
      - interface 도입
      - 관계설정 책임의 분리
      - 원칙과 패턴
        1. 개방 폐쇄 원칙( OCP: Open-Closed Principle)
        클래스나 모듈은 확장에는 열려 있어야하고 변경에는 닫혀 있어야한다.
        2. 객체지향 설계 원칙 ( SOLID)
        => UML for java programmer 참조
        - 높은 응집도와 낮은 결합도 (high coherence and low coupling)
        - 낮은 결합도: 하나의 변경이 발생할 때 마치 파문이 여타 모듈과 객체로 변경에한 요구가 전파되지 않는 상태이다.
        - 높은 응집도 : 변화가 발생할 때 해당 모듈에서 변하는 부분이 크다
        - Strategy pattern : 전략 패턴 자신의 기능 맥락(context)에서 필요에 따라 변경이 필요한 알고리즘을 인터페이를 통해 통째로 외부로 분리시키고, 이를 구현한 구체적인 알고리즘을 인터페이스를 통해 통째로 외부로 분리시키고, 이를 구현한 구체적인 알고리즘 클래스를 필요에 따라 바꿔서 사용하는 디자인 패턴이다. context를 사용하는 client 는 context가 사용할 전략을 context의 생성자를 통해서 제공해주는게 일반적이다.

    - 제어의 역전(IOC)
      - 오브젝트 팩토리 : 객체 생성 방법을 결정하고 그렇게 만들어진 오브젝트를 리턴 하는 오브젝트를 팩토리라고 한다. 즉 설계도 역할을 한다.
      - 제어의 역전: 제어의 역전에서는 오브젝트가 자신이 사용할 오브젝트를 스스로 선택하지 않는다. 당연히 생성하지도 않는다. 모든 제어 권한을 자신이 아닌 다른 대상에게 위임한다.

      예) java의 servlet을 만들면 사용자가 직접 객체 생성에 개입하지 않고 컨테이너가 알아서 생성하고 관리한다.

    - 스프링의 IOC
      - 오브젝트 팩토리를 이용한 스프링 IOC

        ```java
        @Configuration
        @Bean
        ApplicationContext context = new AnnotationConfigApplicationContext(DaoFactory.class);
        UserDao dao = context.getBean("userDao", UserDao.class);
        ```

      - 애플리케이션 컨텍스트의 동작방식
        - ApplicationContext
           IoC를 적용해서 관리할 모든 오브젝트에 대한 생성과 관계설정을 담당
           Dao factory와 달리 직접 오브젝트를 생성하고 관계를 맺어주는 코드가 없고, 그런 생성정보와 연관관계 정보를 별도의 설정정보를 통해 얻는다.
           때로는 외부의 오브젝트 팩토리에 그 작업을 위임하고 그 결과를 가져다가 사용하기도 한다.

        - ApplicationContext의 장점
          - 클라이언트가 구체적인 팩토리 클래스를 알 필요가 없다.
          - 애플리케이션 컨텍스트는 종합 IoC 서비스를 제공해준다.
          - 애플리케이션 컨텍스트는 Bean을 검색하는 다양한 방법을 제공한다.

        - 스프링 IoC의 용어 정리
          - 빈(Bean) : 스프링이 IoC 방식으로 관리하는 오브젝트라는 뜻 managed Object라고 부르기도 한다. 주의할 점은 스프링을 사용하는 애플리케이션에서 만들어지는 모든 오브젝트가 다 Bean은 아니라는 사실이다. 그중에서 스프링이 직접 그 생성과 제어를 담당하는 오브젝트를 Bean이라고 부른다.

          - Bean Factory : 스프링의 IoC를 담당하는 핵심 컨테이너를 가리킨다. Bean을 등록하고 , 생성하고, 조회하고 돌려주고, 그 외에 부가적인 Bean을 관리하는 기능을 담당한다. 보통은 이 bean factory를 사용하지 않고 이를 확장한 application context를 이용한다. BeanFactory라고 붙여쓰면 빈 팩토리가 구현하고 있는 가장 기본적인 인터페이스의 이름이 된다. 이 인터페이스에 getBean()과 같은 method가 정의되어 있다.
          - ApplicationContext : beanFactory를 확장한 IoC 컨테이너이다. bean을 등록하고 관리하는 기본적인 기능은 bean factory와 동일하하다. 여기에 스프링이 제공하는 각종 부가 서비스를 추가로 제공한다. Bean factory라고 부를 때는 주로 bean의 생성과 제어의 관점에서 이야기하는 것이고, application Context라고 할 때는 스프링이 제공하는 애플리케이션 지원 기능을 모두 포함해서 이야기하는 것이라고 보면 된다. ApplicationContext라고 적으면 application context가 구현해야하는 기본 인터페이스를 가리키는 것이기도 하다. ApplicationContext는 BeanFactory를 상속한다.
          - 설정정보/설정 메타정보(configuration metadata) : 스프링의 설정 정보란 애플리케이션 컨텍스트 또는 빈 팩토리가 IoC를 적용하기 위해 사용하는 메타정보를 말한다.실제로 스프링의 설정정보는 컨테이너에 어떤 기능을 세팅하거나 조정하는 경우에도 사용하지만, 그보다 IoC컨테이너에 의해 관리되는 애플리케이션 오브젝트를 생성하고 구성할때 사용된다.
          - 컨테이너(container) 또는 IoC 컨테이너
          - 스프링 프레임워크 : IoC컨테이너, 애플리케이션 컨텍스트를 포함해서 스프링이 제공하는 모든 기능을 통틀어 말할때 주로 사용한다. 그냥 스프링이라고 줄여서 말하기도 한다.

  - 싱글톤 레지스트리와 오브젝트 스코프
      전통적인 싱글톤 패턴 구현 방법
      - 클래스 밖에서 오브젝트를 생성하지 못 하도록 생성자를 private로 만든다.
      - 생성된 싱글톤 오브젝트를 저장할 수 있는 자신과 같은 타입의 스태틱 필드를 정의한다.
      - 스태틱 팩토리 메소드인 getInstance()를 만들고 이 메소드가 최초로 호츨되는 시점에서 한번만 오브젝트를 만들어지게 한다. 생성된 오브젝트는 스태틱 필드에 저장한다. 또는 스태틱 필드의 초기값으로 오브젝트를 미리 만들어 둘 수 있다.
      - 한번 오브젝트(싱글톤)가 만들어지고 난 후에는 getInstance()메소드를 통해 이미 만들어져 스태틱 필드에 저장된 오브젝트를 넘겨준다.

      전통적 싱글톤의 단점
      - private 생성자를 갖고 있기 때문에 상속할 수 없다.
      - 싱글톤은 테스트가 어렵다.
      - 서버 환경에서 싱글톤이 하나만 만들어지는 것을 보장하지 못한다.
      - 싱글톤의 사용은 전역 상태를 만들 수 있기 때문에 바람직하지 못하다.

      싱글톤 레지스트리
      - 전통적 싱글톤의 단점을 보완하기 위해 만들어짐
      - 평범한 자바 클래스를 싱글톤으로 만들어 준다.

      오브젝트의 동일성(identical)과 동등성(equivalent)

      - 싱글톤 레지스트리로서의 애플리케이션 컨텍스트
스프링은 기본적으로 별다른 설정을 하지 않으면 내부에서 생성하는 빈 오브젝트를 모두 싱글톤으로 만든다. ApplicationContext는 싱글톤을 저장하고 관리하는 싱글톤 레지스트리(singleton registry) 이다.

서버 애플리케이션과 싱글톤

싱글톤 패턴으로 구현 했을 때 의 한계점
- private 생성자를 갖고 있기 때문에 상속할 수 가 없다.
- 싱글톤은 테스트하기가 어렵다
- 서버환경에서는 싱글톤이 하나만 만들어지는 것을 보장하지 못한다.
- 싱글톤의 사용은 전역 상태를 만들 수 있기 때문에 바람직하지 못하다

Singleton registry :

오브젝트 팩토리 = 스프링의 애플리케이션 컨텍스트 = Ioc컨테이너 = 스프링 컨테이너 = bean factory
