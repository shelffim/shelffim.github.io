---
title: "애노테이션"
pubDate: 2025-10-02
description: "김영한님의 자바 고급 2편 강의 part 14(애노테이션) 학습 정리"
---

> **출처**: [김영한의 자바 고급 2편 강의](https://inf.run/8ES1C) - Section 14 : 애노테이션

## 애노테이션이란?

**애노테이션(Annotation)**은 코드에 직접적인 영향을 주지 않고, 리플렉션을 통해 런타임에 읽을 수 있는 추가적인 메타데이터를 제공합니다.

### 주요 특징

- **메타데이터 제공**: 코드에 대한 추가적인 정보를 주석처럼 제공
- **동적 동작**: 코드를 더 유연하고 동적으로 동작할 수 있도록 함
- **리플렉션 연동**: 런타임에 리플렉션을 통해 읽을 수 있음

## 애노테이션 정의

애노테이션을 정의할 때는 `@interface` 키워드를 사용합니다:

```java
@interface MyAnnotation {
    String value() default "defaultValue";
    int number() default 0;
}
```

### 특징

- 내부에는 속성을 가질 수 있음
- 인터페이스와 비슷하게 정의
- 요소에 `default` 값을 줄 수 있음

## 메타 애노테이션

### @Retention

애노테이션의 **생존 기간**을 결정합니다:

- **`SOURCE`**: 컴파일 후 사라짐
- **`CLASS`**: 메모리 로드 시점에 사라짐
- **`RUNTIME`**: 런타임까지 유지 (리플렉션 접근 시 필수)

```java
@Retention(RetentionPolicy.RUNTIME)
@interface MyAnnotation { }
```

### @Target

애노테이션을 적용할 수 있는 **위치**를 지정합니다:

- **`TYPE`**: 클래스, 인터페이스, 열거형
- **`FIELD`**: 필드
- **`METHOD`**: 메서드

```java
@Target({ElementType.TYPE, ElementType.METHOD})
@interface MyAnnotation { }
```

### @Documented

자바 API 문서를 만들 때 해당 애노테이션이 함께 포함되는지 지정합니다.

### @Inherited

부모 클래스에 적용된 애노테이션이 **자식 클래스에도 상속**되도록 합니다:

- 클래스 간의 상속에만 해당
- 인터페이스를 구현하는 클래스에는 인터페이스의 애노테이션이 상속되지 않음

## 애노테이션 상속 제한

애노테이션은 다른 애노테이션이나 인터페이스를 **직접 상속할 수 없습니다**:

- 애노테이션 사이에는 상속이라는 개념이 존재하지 않음

## 자바 기본 애노테이션

### @Override

- 메서드 재정의가 정확하게 잘 되었는지 컴파일러가 체크

### @Deprecated

- 더 이상 사용하지 않는 메서드를 표시

### @SuppressWarnings

- 컴파일러의 경고를 무시

## 프레임워크에서의 활용

현대 자바 프레임워크는 애노테이션을 통해 메타데이터를 얻고, 이를 리플렉션 기술로 읽어 동적으로 기능을 구현합니다.

### 주요 활용 분야

- **의존성 주입**: Spring의 `@Autowired`, `@Component`
- **ORM**: JPA의 `@Entity`, `@Table`
- **AOP**: `@Aspect`, `@Around`
- **설정의 자동화**: `@Configuration`, `@Bean`
- **트랜잭션 관리**: `@Transactional`
