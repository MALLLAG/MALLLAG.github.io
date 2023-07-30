---
title: Configuration and SpringBoot
tags: Spring
comments: true
---

# 빈 라이프사이클 관리

**IoC 컨테이너가 제공하는 기능 중 생성/소멸같은 빈 라이프사이클의 특정 시점에 통지를 받을 수 있게 빈을 생성하는 기능이 있다.**

> 빈이 라이프 사이클이벤트 통지를 받을 수 있게 설정하면 해당 빈은 이벤트 발생 시점에 관련 처리를 할 수 있다. <br>
> 일반적으로 두 가지 라이프사이클 이벤트가 빈과 관련이 있는데, **초기화 이후**와 **소멸 이전** 이벤트이다.

초기화 이후 이벤트는 빈에 모든 프로퍼티 값을 설정하고 의존성 점검을 마치자마자 발생하고, <br>
소멸 이전 이벤트는 스프링이 빈 인스턴스를 소멸시키기 전에 발생한다. <br>
하지만 요청을 받을때마다 빈을 생성하는 프로토타입 빈에는 스프링이 소멸 전 이벤트를 통지하지 않는다.

<img width="816" alt="4" src="https://github.com/MALLLAG/TIL/assets/87420630/aff5ab45-fe7e-4fd2-bfed-4167d4acbef5">

<br>
<hr>

# 빈 생성 시점에 통지 받기

스프링이 의존성 검사를 할 수는 있지만, 이는 하나라도 공급되지 않으면 전체 실패로 간주하여 의존성 해석 절차에 특정 로직을 추가할 수 없다. <br>
**초기화 콜백**을 사용하면 빈이 필요로 하는 의존성을 점검할 수 있어 예외를 던지거나 기본값을 제공할 수 있다.

빈은 생성자에서 의존성 검사를 할 수 없는데, 빈 생성 시점에는 스프링이 빈에 필요한 의존성을 공급할 수 없기 때문이다. <br>
초기화 콜백은 스프링이 제공할 수 있는 의존성 제공이 완료된 이후에 호출되며 사용자가 원하는 의존성 검사를 수행한다.

## @PostConstruct 애너테이션 사용하기

@PostConstruct는 라이프사이클 애너테이션으로, 빈 생성 시 메서드를 실행할 수 있게 해준다.

<br>
<hr>

# 빈 소멸 시점에 통지 받기

DefaultListableBeanFactory 인터페이스를 래핑한 ApplicationContext 구현체를 사용할때는 <br>
ConfigurableBeanFactory.destroySingletons()를 호출해 BeanFactory가 모든 싱글톤 인스턴스를 소멸시키도록 통지할 수 있다. <br>
애플리케이션을 종료할 때 소멸 통지를 사용해 여러 빈이 사용 중인 리소스를 모두 정리한 후 안전하게 애플리케이션을 종료할 수 있다.

destroySingletons()가 호출됐다는 통지를 받는 방법에는 세 가지가 있고, 초기화 콜백을 받는 매커니즘과 비슷하다.

## @PreDestroy 애너테이션 사용하기

빈이 소멸되기 전에 호출될 메서드를 지정하는 방법 중 하나는 @PreDestroy를 사용하는 것이다.

<br>
<hr>

# FactoryBean 사용하기

스프링은 기본으로 제공되는 스프링 구문으로는 생성 및 관리할 수 없는 객체를 관리하기 위한 어댑터인 FactoryBean 인터페이스를 제공한다. <br>
new 연산자로 생성할 수 없는 객체를 생성할때는 일반적으로 FactoryBean을 사용한다. <br>
FactoryBean은 다른 빈을 생성하는 Factory 역할을 하는 빈인 것이다.

FactoryBean은 스프링에서 큰 역할을 하는데, 트랜잭션 프록시와 JNDI 컨텍스트에서 자동으로 리소스를 가져오는 역할 등을 한다.

<br>
<hr>

# 스프링 부트

스프링 부트 프로젝트는 처음 스프링을 사용해 애플리케이션을 만드는 작업을 간단하게 해준다.

## @SpringBootApplication

@SpringBootApplication은 클래스 레벨에서만 사용하도록 설계된 최상위 애너테이션이다. <br>
@SpringBootApplication은 아래의 세 애너테이션을 정의한 것과 같은 애너테이션이다.

- @Configuration: 해당 클래스가 @Bean으로 빈을 정의하는 구성 클래스임을 나타낸다.
- @EnableAutoConfiguration: 사용자가 필요로 할 빈을 추측해 구성한 뒤 스프링 ApplicationContext를 활성화한다.
- @ComponentScan: 사용할 클래스에 스테레오타입 애너테이션을 지정해 몇 가지 유형의 빈으로 선언할 수 있다.


