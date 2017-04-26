Dependency + Injection + Framework

**1. Dependency ( Dependency relationship)**

**의존 관계의 발생**
- supplier가 client의 필드
- supplier가 client의 method의 파라미터
- supplier가 client의 local 변수
- supplier로 메시지를 보냄

 의존관계가 생기면 supplier에 변경이 발생하였을 때 client에 영향받게 되므로 client의 재사용이 어려워 진다.

***재사용 가능한(reusable) 객체지향 설계/개발***
- client는 재사용이 어렵다.
- client는 component/서비스가 될수 없다
- component란 이를 만든 개발자의 영향이 미치지 않는 곳에서도 아무 변경없이 필요에 따라 확장해서 사용될 수 있는 소프트웨어 덩이다.

***재사용***
- 재사용이 가능하게 되면 생산성이 향상된다.
- 재사용 가능한 객체 지향 소프트웨어를 위한 구성이 디자인 패턴이다

**Design patten**

“ Elements of Reusable Object - Oriented software -Gof- ”

- Object pattern 은 런타임 시 바뀔 수 있는 (상속이나, 관계보다) 더 동적인 오브젝트  (의존) 관계를 다룬다.
- Design pattern의 분류 방법 중 class pattern과 object pattern으로 구분 할 수 있다.
- Design pattern에서의  dependency : 컴파일 타임이 아니라 런타임 시 결정/구성되는 오브젝트 의존관계를 말한다.
- 이를 위해서
	1. 구현 대신 인터페이스 사용
	2. 오브젝트 합성(composition) 사용
