---
title: "Null Object Pattern"
pubDate: 2025-09-29
description: "김영한님의 자바 고급 2편 강의 part 10(채팅 프로그램) 학습 정리"
---

> **출처**: [김영한의 자바 고급 2편 강의](https://inf.run/8ES1C) - Section 10 : 채팅 프로그램

## Null Object Pattern

### 개념

**null 대신 특정 동작을 수행하는 객체**를 반환하여 null 검사 로직을 줄이고 코드를 간결하게 만드는 패턴

### 장점

- **코드 간결성**: null 검사 로직 제거
- **안정성 향상**: NullPointerException 방지
- **가독성 개선**: 조건문 감소

## 기본 구조

### 문제 상황

```java
// ❌ null 검사가 필요한 코드
public String getUserName(String userId) {
    Map<String, String> users = getUserMap();
    if (users.containsKey(userId)) {
        return users.get(userId);
    }
    return null;  // null 반환으로 인한 문제
}
```

### 해결책

```java
// ✅ getOrDefault 사용
public String getUserName(String userId) {
    Map<String, String> users = getUserMap();
    return users.getOrDefault(userId, "Unknown");  // null 대신 기본값 반환
}

```

### 사용 예시

```java
// 안전한 사용
String name = getUserName("123");
System.out.println("Hello, " + name);  // null 검사 불필요

```

## 활용 사례

**핵심**: null로 인한 예외 상황을 **미리 방지**하고 코드를 더 안전하게 만듦
