---
title: "Stack"
pubDate: 2025-09-21
description: "김영한님의 자바 중급 2편 강의 part 10(컬렉션 프레임워크 - Map, Stack, Queue) 학습 정리"
---

> **출처**: [김영한의 자바 중급 2편 강의](https://inf.run/ir9Dw) - Section 10 : 컬렉션 프레임워크 - Map, Stack, Queue

## Stack이란?

Stack은 마지막에 추가된 데이터가 가장 먼저 제거되는 자료 구조로, **후입선출(LIFO)** 방식으로 데이터를 관리합니다.

```
    [3] ← 마지막에 추가된 데이터 (가장 먼저 제거)
    [2]
    [1] ← 처음에 추가된 데이터 (가장 나중에 제거)
```

## Stack 메서드

### push() - 데이터 추가

Stack에 값을 넣는 것을 `push()` 메서드를 사용합니다.

### pop() - 데이터 제거

값을 제거하는 것을 `pop()` 메서드를 사용합니다.

```java
Stack<String> stack = new Stack<>();
stack.push("첫번째");
stack.push("두번째");
stack.push("세번째");

String item = stack.pop();  // "세번째" 반환 (마지막에 추가된 것)
```

## 사용 권장사항

Stack 클래스는 사용하지 말고 **Deque**를 사용하는 것을 권장합니다.

```java
// 권장하지 않음
Stack<String> stack = new Stack<>();

// 권장
Deque<String> deque = new ArrayDeque<>();
deque.push("데이터");
String item = deque.pop();
```
