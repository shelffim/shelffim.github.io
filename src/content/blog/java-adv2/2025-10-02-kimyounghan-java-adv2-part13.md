---
title: "리플렉션"
pubDate: 2025-10-02
description: "김영한님의 자바 고급 2편 강의 part 13(리플렉션) 학습 정리"
---

> **출처**: [김영한의 자바 고급 2편 강의](https://inf.run/8ES1C) - Section 13 : 리플렉션

## 리플렉션이란?

**리플렉션(Reflection)**은 프로그램이 실행되는 런타임 중에 클래스, 메서드, 필드, 생성자 등 자신의 구조와 메타데이터를 분석하고 조작할 수 있게 해주는 기능입니다.

### 주요 특징

- **동적 메서드 호출**: 동적으로 메서드를 호출하고 기능을 묶는 방안 제공
- **유연한 설계**: 유연한 설계와 동적인 코드 생성을 가능하게 함
- **런타임 분석**: 프로그램 실행 중에 클래스, 메서드, 필드 등에 대한 정보를 얻거나 조작 가능

## Class 메타데이터 얻기

클래스의 메타데이터를 얻는 방법:

```java
// 1. 클래스명.class
Class<?> clazz = MyClass.class;

// 2. 인스턴스.getClass()
MyClass instance = new MyClass();
Class<?> clazz = instance.getClass();

// 3. Class.forName()
Class<?> clazz = Class.forName("com.example.MyClass");
```

## 메서드 정보 조회

### 메서드 목록 조회

- **`getDeclaredMethods()`**: 접근 제어자와 관계없이 해당 클래스에 선언된 모든 메서드 반환
- **`getMethods()`**: 상속된 public 메서드를 포함한 모든 public 메서드 반환

### 메서드 실행

```java
// 메서드 참조 얻기
Method method = clazz.getMethod("methodName", parameterTypes);

// 메서드 실행
Object result = method.invoke(instance, arguments);
```

## 필드 정보 조회

- **`getDeclaredFields()`**: 접근 제어자에 관계없이 해당 클래스에서 선언된 모든 필드 반환
- **`getFields()`**: 해당 클래스와 상위 클래스에서 상속된 모든 public 필드 반환

## 주의사항

### 캡슐화 위배

```java
field.setAccessible(true); // private 멤버에 접근 가능하게 함
```

**문제점**:

- 캡슐화 원칙을 위배할 수 있음
- 내부 구현 변경 시 외부 코드가 쉽게 깨짐
- 코드의 안정성을 해칠 수 있음

## 사용 사례

리플렉션은 다음과 같은 경우에 주로 사용됩니다:

- **프레임워크 개발**: Spring과 같은 프레임워크가 객체를 동적으로 생성하고 관리
- **라이브러리 개발**: 동적인 동작이 필수적인 기반 시스템 개발
- **유틸리티 개발**: 일반 비즈니스 로직보다는 동적 처리가 필요한 경우

> **주의**: 리플렉션은 성능 오버헤드가 있으므로 일반적인 비즈니스 로직에서는 사용을 지양해야 합니다.
