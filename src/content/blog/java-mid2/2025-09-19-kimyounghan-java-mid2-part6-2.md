---
title: "컬렉션 프레임워크 - List"
pubDate: 2025-09-19
description: "김영한님의 자바 중급 2편 강의 part 6(컬렉션 프레임워크 - List) 학습 정리"
---

> **출처**: [김영한의 자바 중급 2편 강의](https://inf.run/ir9Dw) - Section 6 : 컬렉션 프레임워크 - List

## ArrayList vs LinkedList 성능 비교

이론적으로는 연결 리스트가 더 빠르지만 실제로는 배열 리스트가 더 빠릅니다.

### 사용 권장사항

- **대부분의 경우**: ArrayList 사용
- **LinkedList 사용**: 매우 큰 리스트의 맨 앞에 데이터를 빈번하게 추가, 삭제하는 경우에만

```java
// 일반적인 경우 - ArrayList 권장
List<String> list = new ArrayList<>();

// 맨 앞 삽입이 빈번한 경우 - LinkedList 고려
List<String> list = new LinkedList<>();
```

## 컬렉션 프레임워크 구조

### Collection 인터페이스

컬렉션 프레임워크의 핵심 인터페이스입니다. 하위 인터페이스로 List도 있습니다.

### List 인터페이스

순서가 있고 중복을 허용하는 컬렉션을 구현합니다. ArrayList와 LinkedList와 같은 여러 구현 클래스를 가집니다.

```
Collection (인터페이스)
    └── List (인터페이스)
        ├── ArrayList (구현체)
        └── LinkedList (구현체)
```

## ArrayList 특징

### 용량 관리

- 배열을 사용해서 데이터를 관리
- 기본 용량: 10
- 용량 초과 시: 배열을 50% 증가

```java
ArrayList<String> list = new ArrayList<>();  // 기본 용량 10
// 용량 초과 시 자동으로 15, 22, 33... 으로 증가
```

### 성능 최적화

`System.arraycopy()`를 사용해서 메모리 고속 복사 연산을 하기 때문에 한 칸씩 이동하는 방식보다 빠릅니다.

## LinkedList 특징

### 이중 연결 리스트 구조

첫번째 노드의 참조값과 마지막 노드의 참조값을 가지고 있습니다.

```
first → Node1 ↔ Node2 ↔ Node3 ↔ last
```

### 양방향 순회

다음 노드뿐만 아니라 이전 노드로도 이동할 수 있어 역방향으로 조회할 수도 있습니다.

### 마지막 추가 성능

마지막 노드에 대한 참조를 제공하기 때문에 데이터를 마지막에 추가하는 경우에도 O(1)의 성능을 제공합니다.

```java
LinkedList<String> list = new LinkedList<>();
list.addLast("새 요소");  // O(1) - 빠름
```
