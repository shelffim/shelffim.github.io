---
title: "컬렉션 프레임워크 - LinkedList"
pubDate: 2025-09-19
description: "김영한님의 자바 중급 2편 강의 part 5(컬렉션 프레임워크 - LinkedList) 학습 정리"
---

> **출처**: [김영한의 자바 중급 2편 강의](https://inf.run/ir9Dw) - Section 5: 컬렉션 프레임워크 - LinkedList

## 노드란?

노드클래스는 내부에 저장할 데이터인 `item`과 다음으로 연결할 노드의 참조인 `next`를 가집니다.

```java
class Node<T> {
    T item;        // 저장할 데이터
    Node<T> next;  // 다음 노드 참조
}
```

## LinkedList의 특징

각각의 노드를 링크(연결)해서 사용하는 자료 구조를 **LinkedList**라고 합니다.

### 장점

노드를 만들고 각 노드를 서로 연결하면:

- 낭비되는 메모리 없이 필요한 메모리를 확보
- 데이터를 추가, 삭제할 때 효율적

### 단점

연결을 유지하기 위한 추가 메모리가 필요합니다.

## LinkedList 순회 방법

링크드 리스트에서 리스트를 순회하거나 탐색하는 방법은 현재 노드의 다음 참조를 따라가면 됩니다.

```
Node1.next → Node2.next → Node3.next → null
```

## LinkedList의 시간 복잡도

연결리스트는 추가나 삭제할 위치를 찾는 것은 느리지만, 데이터를 추가하거나 삭제할 때는 참조값만 변경하면 되므로 빠릅니다.

### 앞쪽 추가/삭제

- **시간 복잡도**: O(1)
- **이유**: 일부 노드의 참조만 변경하면 되므로 빠름

```java
LinkedList<String> list = new LinkedList<>();
list.addFirst("새로운 요소");  // O(1) - 빠름
```

### 중간/뒤쪽 추가/삭제

- **시간 복잡도**: O(n)
- **이유**: 추가할 위치를 찾는 과정이 필요하므로 느림

```java
LinkedList<String> list = new LinkedList<>();
list.add(2, "중간 요소");  // O(n) - 느림 (위치 찾기 필요)
```

## 제네릭과 타입 안전성

연결 리스트에 제네릭을 도입하면 데이터 타입을 컴파일 시 결정할 수 있어 타입 안전성을 확보할 수 있습니다.

```java
LinkedList<String> stringList = new LinkedList<>();  // String만 저장
LinkedList<Integer> intList = new LinkedList<>();    // Integer만 저장
```
