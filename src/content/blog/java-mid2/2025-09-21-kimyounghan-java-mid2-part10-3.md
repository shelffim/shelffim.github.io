---
title: "Queue"
pubDate: 2025-09-21
description: "김영한님의 자바 중급 2편 강의 part 10(컬렉션 프레임워크 - Map, Stack, Queue) 학습 정리"
---

> **출처**: [김영한의 자바 중급 2편 강의](https://inf.run/ir9Dw) - Section 10 : 컬렉션 프레임워크 - Map, Stack, Queue

## Queue란?

Queue는 처음에 추가된 데이터가 가장 먼저 제거되는 자료 구조로, **선입선출(FIFO)** 방식으로 데이터를 관리합니다.

```
[1] → [2] → [3] → [4]
 ↑                ↑
처음 추가        마지막 추가
(먼저 제거)      (나중에 제거)
```

## Queue 메서드

### offer() - 데이터 추가

Queue에 값을 넣는 것을 `offer()` 메서드를 사용합니다.

### poll() - 데이터 제거

값을 제거하는 것을 `poll()` 메서드를 사용합니다.

```java
Queue<String> queue = new LinkedList<>();
queue.offer("첫번째");
queue.offer("두번째");
queue.offer("세번째");

String item = queue.poll();  // "첫번째" 반환 (처음에 추가된 것)
```

## Queue 구현체

Queue 인터페이스는 Collection 인터페이스를 구현하고 있고, Queue 인터페이스를 구현한 클래스로 ArrayDeque, PriorityQueue, LinkedList 등이 있습니다.

## Deque란?

Deque는 양쪽 끝에서 요소를 추가하거나 제거할 수 있는 자료 구조로 Queue와 Stack의 기능을 모두 가지고 있습니다.

```
앞쪽 ← [1] [2] [3] [4] → 뒤쪽
```

## Deque 메서드

- `offerFirst()`: 앞에 추가
- `offerLast()`: 뒤에 추가
- `pollFirst()`: 앞에 제거
- `pollLast()`: 뒤에 제거
- `peekFirst()`: 앞에 조회
- `peekLast()`: 뒤에 조회

```java
Deque<String> deque = new ArrayDeque<>();
deque.offerFirst("앞에 추가");
deque.offerLast("뒤에 추가");
```

## Deque 구현체

Deque의 대표적인 구현체는 ArrayDeque와 LinkedList가 있습니다. **ArrayDeque가 성능이 더 좋습니다**.
