### 1. web.xml  
```  
<web-app xmlns="http://java.sun.com/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://java.sun.com/xml/ns/javaee
	      http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd"
         version="3.0">

    <display-name>MVC Starter</display-name>

    <context-param>
        <param-name>spring.profiles.default</param-name>
        <param-value>local</param-value>
    </context-param>

    <servlet>
        <servlet-name>spring</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>classpath:config/spring/root-config.xml</param-value>
        </init-param>
        <load-on-startup>1</load-on-startup>
    </servlet>

    <servlet-mapping>
        <servlet-name>spring</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>

</web-app>
``` 
스프링으로 tomcat과 스프링을 함계 구동했을 때 web.xml의 구조이다.  
스프링으로 만든 application을 war로 빌드 후 tomcat의 webapp 디렉토리 밑에 위치 시키고 tomcat을 기동 한다.  
tomcat은 war를 풀고 위의 web.xml을 읽는다. 

servletDistpatcher를 생성하는데 해당 해당 config xml의 위치는 /config/spring/root-config.xml로 설정 하였다. 이때 classpath로 해당 xml의 위치를 설정하였는데 그 실제 코드를 작성할 때 위치는 **src/main/resources** 아래이다.  

`\<load-on-startup>1\</load-on-startup>` 초기화 시 우선순위를 의미한다. 0보다 큰값을 가지고 있으면 서버 기동과 동시에 초기화 된다.

위에서 생성한 dispatcherServlet이 담당할 URL을 아래 \<servlet-mapping\> 에서 등록하여 **/** 이하로 들어오는 요청을 dispatcherServlet에서 하도록 했다.  

### 2. root-config.xml
관리적인 측면에서 config 파일을 아래와 같이 분리해놓았다. 이는 개발자 마다 다르게 설정할 수 있다.   

```  
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <import resource="properties-config.xml"/>
    <import resource="datasource-config.xml"/>
    <import resource="tx-config.xml"/>
    <import resource="mybatis-config.xml"/>
    <import resource="aop-config.xml"/>
    <import resource="app-config.xml"/>
    <import resource="mvc-config.xml"/>

</beans>
``` 

#### 2.1 mvc-confg.xml
   
```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xsi:schemaLocation="
            http://www.springframework.org/schema/beans
            http://www.springframework.org/schema/beans/spring-beans.xsd
            http://www.springframework.org/schema/context
            http://www.springframework.org/schema/context/spring-context.xsd
            http://www.springframework.org/schema/mvc
            http://www.springframework.org/schema/mvc/spring-mvc.xsd">

    <mvc:annotation-driven />

    <context:component-scan base-package="net.ujacha.hot.mvcstarter">
        <context:include-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
    </context:component-scan>

    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="prefix">
            <value>/WEB-INF/views/jsp/</value>
        </property>
        <property name="suffix">
            <value>.jsp</value>
        </property>
    </bean>

    <mvc:resources mapping="/resources/**" location="/resources/" />

</beans>
```

##### 2.1.1 \<mvc:annotation-driven />  
spring web mvc에서 사용되는 값들을 자동 등록해 준다.  

##### 2.1.2 \<context:component-scan base-package="net.ujacha.hot.mvcstarter">  
base-package 아래에서 filter로 적용된 controller annotation 타입만을 읽어 들여 등록 한다.  

##### 2.1.3 \<bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
DispatcherServlet은 뷰 리졸버를 이용해서 controller가 리턴한 뷰 이름에 해당하는 뷰 오브젝트를 가져온다.  
jsp 파일을 WEB-INF 아래에 둔 이유는 사용자가 url을 통해 직접 jsp파일을 실행하지 못하도록 한 것이다.  

##### 2.1.4.\<mvc:resources mapping="/resources/**" location="/resources/" />  
tomcat에서 webapp/resources를 접근하게 하기 위해서 설정   

#### 2.2 datasource-config.xml  

```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:p="http://www.springframework.org/schema/p"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="dataSource" class="org.apache.commons.dbcp2.BasicDataSource"
          destroy-method="close"
          p:driverClassName="#{jdbc['jdbc.driverClassName']}"
          p:url="#{jdbc['jdbc.url']}"
          p:username="#{jdbc['jdbc.username']}"
          p:password="#{jdbc['jdbc.password']}"
    />

    <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
        <property name="dataSource" ref="dataSource"/>
    </bean>

    <bean id="userMapper" class="org.mybatis.spring.mapper.MapperFactoryBean">
        <property name="mapperInterface" value="repository.UserMapper"/>
        <property name="sqlSessionFactory" ref="sqlSessionFactory"/>
    </bean>

</beans>
```  
datasource 빈은 dbcp2로 사용하고 객체를 생성할 설정값들은 property파일로 따로 설정하여 사용한다.  
sqlSessionFactory : sqlSession객체를 생성한다. sqlSession은 commit이나 rollback, select같은 db관련 method가 정의된 interface이다.   

#### 2.3 mybatis.config.xml

```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
        <property name="dataSource" ref="dataSource"/>
        <property name="mapperLocations" value="classpath:config/mappers.user/UserMapper.xml"/>
        <property name="typeAliasesPackage" value="repository"/>
    </bean>

    <bean id="sqlSession" class="org.mybatis.spring.SqlSessionTemplate">
        <constructor-arg index="0" ref="sqlSessionFactory"/>
    </bean>

</beans>
```  

datasource-config에서는 직접 UserMapper 객체를 생성했지만 이를 SqlSessionTemplate를 통하여 Mapper 객체를 가져오도록 변경하였다.  










 
