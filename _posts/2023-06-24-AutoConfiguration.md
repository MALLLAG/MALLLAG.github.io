---
title: Auto Configuration
tags: Spring
comments: true
---

# Auto Configuration 동작 원리

Spring의 Auto Configuration은 Spring Boot에서 사용되는 기능 중 하나이다. <br>
이 기능은 개발자가 명시적으로 설정하지 않아도 Spring Boot가 애플리케이션을 구성하는 데 필요한 빈(Bean)과 구성(Configuration)을 자동으로 제공한다.

Auto Configuration은 Spring Boot의 조건부 구성(Conditional Configuration) 기능을 기반으로 작동한다. <br>
이를 통해 애플리케이션의 클래스 패스를 스캔하고 필요한 빈과 구성을 자동으로 구성한다.

<br>
<hr>

## 조건부 구성(Conditional Configuration) *(@ConditionalOnX)*

Spring Boot의 Auto Configuration은 조건부 구성을 사용하여 특정 조건을 만족하는 경우에만 해당 빈이나 구성을 자동으로 생성한다. <br>
이는 `@Conditional` annotation을 통해 지정되며, 조건을 만족하는 경우에만 자동 구성이 활성화된다. <br>
예를 들어, 특정 클래스가 클래스 패스에 존재하거나, 특정 빈이 이미 정의되어 있는 경우 조건을 만족할 수 있다.

- **@ConditionalOnClass**: 지정한 클래스가 클래스 패스에 존재하는 경우에만 구성이 활성화된다. 예를 들어, @ConditionalOnClass(Database.class)는 Database 클래스가 클래스 패스에 존재하는 경우에만 구성을 활성화한다.
- **@ConditionalOnBean**: 지정한 빈이 이미 등록되어 있는 경우에만 구성이 활성화된다. 예를 들어, @ConditionalOnBean(Database.class)는 Database 빈이 이미 등록되어 있는 경우에만 구성을 활성화한다.
- **@ConditionalOnProperty**: 지정한 프로퍼티 값이 설정되어 있는 경우에만 구성이 활성화된다. 예를 들어, @ConditionalOnProperty(name = "myapp.feature.enabled", havingValue = "true")는 myapp.feature.enabled 프로퍼티가 true로 설정되어 있는 경우에만 구성을 활성화한다.

```java
@Configuration
@ConditionalOnClass(Database.class)
public class DatabaseAutoConfiguration {

    @Bean
    @ConditionalOnMissingBean
    public Database database() {
        // Database 인스턴스 생성 및 구성
        return new Database();
    }
}
```

> @ConditionalOnClass(Database.class)를 사용하여 Database 클래스의 존재 여부를 확인하는 조건을 설정했다. <br>
> Database 클래스가 클래스 패스에 존재하는 경우에만 해당 구성이 활성화된다. <br>
> 또한, @ConditionalOnMissingBean을 사용하여 이미 해당 타입의 빈이 등록되어 있지 않은 경우에만 database() 메서드가 호출되어 Database 빈이 생성된다.

<br>

### @ConditionalOnBean

```java
@Configuration
public class MyAutoConfiguration {
    
    @Bean
    @ConditionalOnBean(DataSource.class)
    public MyService myService(DataSource dataSource) {
        return new MyService(dataSource);
    }
}
```

@ConditionalOnBean 어노테이션은 특정한 빈이 존재할 때 자동 구성을 활성화하는 조건을 설정하는 데 사용된다. <br>
특정 빈이 존재하는 경우에만 자동 구성을 수행하고 그렇지 않은 경우에는 자동 구성을 건너뛴다.

위 예제에서는 DataSource 빈이 존재할때만 MyService 빈을 등록한다.

### @ConditionalOnClass

```java
@Configuration
@ConditionalOnClass(name = "com.example.MyClass")
public class MyAutoConfiguration {
    
    @Bean
    public MyService myService() {
        return new MyService();
    }
}
```

@ConditionalOnClass 어노테이션은 특정한 클래스가 classpath에 존재할 때 자동 구성을 활성화하는 조건을 설정하는 데 사용된다. <br>
특정 클래스가 존재하는 경우에만 자동 구성을 수행하고 그렇지 않은 경우에는 자동 구성을 건너뛴다.

위 예제에서는 com.example.MyClass 클래스가 classpath에 존재할 때만 MyService 빈을 등록한다.

### @ConditionalOnProperty

```java
@Configuration
@ConditionalOnProperty(name = "myapp.feature.enabled", havingValue = "true")
public class MyAutoConfiguration {
    
    @Bean
    public MyService myService() {
        return new MyService();
    }
}
```

@ConditionalOnProperty 어노테이션은 지정된 프로퍼티의 값에 따라 자동 구성을 활성화하는 조건을 설정하는 데 사용된다. <br>
특정 프로퍼티가 지정된 값과 일치하는 경우에만 자동 구성을 수행하고 그렇지 않은 경우에는 자동 구성을 건너뛴다.

위 예제에서는 myapp.feature.enabled 프로퍼티의 값이 true일 때만 MyService 빈을 등록한다.



<br>

## @EnableAutoConfiguration

Auto Configuration을 활성화하려면 `@EnableAutoConfiguration` annotation을 사용해야 한다. <br>
이 annotation은 Spring Boot 애플리케이션 컨텍스트를 구성하기 위해 필요한 빈들을 자동으로 활성화한다.

```java
@SpringBootApplication
public class MyApplication {

    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class, args);
    }
}
```

> @SpringBootApplication annotation을 이용하여 Auto Configuration을 활성화했다. <br>
> 이 annotation은 @EnableAutoConfiguration을 내부적으로 포함하고 있기 때문에, 별도로 @EnableAutoConfiguration을 사용할 필요가 없다.

<br>

## spring.factories 파일

Auto Configuration은 `META-INF/spring.factories` 파일을 통해 정의된다. <br>
이 파일은 Spring Boot의 자동 구성 클래스들을 지정하는 역할을 하고, `spring.factories` 파일에는 자동 구성 클래스들의 패키지 경로와 클래스 이름이 명시되어 있다.

```
org.springframework.boot.autoconfigure.EnableAutoConfiguration=\
com.example.MyAutoConfiguration,\
com.example.OtherAutoConfiguration
```

> spring.factories 파일을 사용함으로써 Spring Boot는 클래스 패스 상에서 Auto Configuration 클래스들을 탐색하고 필요한 빈들을 자동으로 등록하거나 구성을 활성화할 수 있다.

<br>


## 구성 우선순위

여러 개의 Auto Configuration이 동일한 빈을 생성하려고 할 때, 구성 우선순위가 사용된다. <br>
구성 우선순위는 `@AutoConfigureOrder` annotation을 통해 지정할 수 있으며, 낮은 숫자가 높은 우선순위를 의미한다. <br>
우선순위가 동일한 경우에는 `@ConditionalOnBean`, `@ConditionalOnClass` 등의 annotation을 통해 더 구체적인 조건을 검사하여 결정한다.

<br>

### @AutoConfigureOrder

```java
@Configuration
@AutoConfigureOrder(Ordered.HIGHEST_PRECEDENCE)
public class MyAutoConfiguration {
    // ...
}
```

@AutoConfigureOrder annotation은 자동 구성 클래스의 우선순위를 지정하는 데 사용된다. <br>
Spring Boot는 자동 구성 클래스를 classpath 상에서 탐색하고, 자동 구성을 수행할 때 우선순위에 따라 빈을 등록하고 구성을 활성화는데, <br>
@AutoConfigureOrder를 사용하여 이 우선순위를 조정할 수 있다.

<br>


## 자동 구성 제외하기

Spring Boot 애플리케이션에서 특정한 자동 구성을 제외하고 싶은 경우, `@SpringBootApplication` annotation에 `exclude` 속성을 사용하여 해당 자동 구성 클래스를 명시적으로 제외할 수 있다.

```java
@SpringBootApplication
@EnableAutoConfiguration(exclude = {DataSourceAutoConfiguration.class, HibernateJpaAutoConfiguration.class})
public class MyApplication {
    // ...
}
```

위의 예제에서 DataSourceAutoConfiguration과 HibernateJpaAutoConfiguration 자동 구성 클래스를 exclude 속성을 사용하여 제외했다. <br>
이는 데이터베이스 연결과 JPA 기능을 사용하지 않는다는 의미이다. <br>
이렇게 하면 해당 클래스들의 자동 구성이 비활성화되며, 빈 등록과 관련된 설정도 수행되지 않는다.

<br>


> 위의 개념과 기술을 바탕으로 Auto Configuration은 다음과 같은 순서로 동작한다.
> 1. 애플리케이션 클래스 패스를 스캔하여 `META-INF/spring.factories` 파일에 정의된 자동 구성 클래스들을 찾는다.
> 2. 각 자동 구성 클래스에 대해 조건부 구성을 검사한다. `@Conditional` 애노테이션에 지정된 조건들을 확인하여 조건을 만족하는지 여부를 판단한다.
> 3. 조건을 만족하는 자동 구성 클래스들은 빈 및 구성을 생성하고, 이를 Spring 애플리케이션 컨텍스트에 등록한다.
> 4. 구성 우선순위를 고려하여 빈들이 생성되고, 의존성 주입(Dependency Injection) 등의 처리가 이루어진다.
> 5. 최종적으로 구성된 빈들을 사용하여 Spring Boot 애플리케이션을 실행한다.

```mermaid
graph LR
A[애플리케이션 클래스 패스 스캔] --> B[자동 구성 클래스 탐색]
B --> C[조건부 구성 검사]
C -- 조건 만족 --> D[빈 및 구성 생성]
D --> E[Spring 애플리케이션 컨텍스트 등록]
C -- 조건 불만족 --> F[다음 자동 구성 클래스 탐색]
E --> G[의존성 주입 및 빈 생성]
F --> B
G --> H[애플리케이션 실행]
```

Auto Configuration은 Spring Boot의 핵심 기능 중 하나로, 개발자는 필요한 빈과 구성을 명시적으로 작성하지 않아도 애플리케이션을 간편하게 구성할 수 있다.
