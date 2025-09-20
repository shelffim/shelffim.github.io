---
title: "컬렉션 프레임워크 - ArrayList"
pubDate: 2025-09-19
description: "김영한님의 자바 중급 2편 강의 part 4(컬렉션 프레임워크 - ArrayList) 학습 정리"
---

> **출처**: [김영한의 자바 중급 2편 강의](https://inf.run/ir9Dw) - Section 4: 컬렉션 프레임워크 - ArrayList

## 배열 vs 리스트

### 배열의 특징

배열은 순서가 있고 중복을 허용하지만 크기가 정적으로 고정됩니다.

```java
int[] arr = new int[5];  // 크기가 5로 고정
```

### 리스트의 특징

리스트는 순서가 있고 중복을 허용하지만 크기가 동적으로 변할 수 있습니다.

```java
ArrayList<Integer> list = new ArrayList<>();  // 크기가 동적으로 변함
```

## ArrayList란?

ArrayList란 리스트 자료 구조를 사용하는데, 내부 데이터는 배열에 보관하는 것입니다.

## ArrayList의 시간 복잡도

- **마지막 위치 추가/삭제**: O(1) - 배열 이동 없이 바로 접근
- **중간 위치 추가/삭제**: O(n) - 데이터를 이동시켜야 하기 때문

```java
ArrayList<String> list = new ArrayList<>();
list.add("마지막");     // O(1) - 빠름
list.add(0, "첫번째");  // O(n) - 느림 (모든 요소 이동)
```

## 제네릭과 타입 안전성

데이터 구조에 제네릭을 도입하면 데이터 타입을 컴파일 시 결정할 수 있어 타입 안전성을 확보할 수 있습니다.

```java
ArrayList<String> stringList = new ArrayList<>();  // String만 저장 가능
ArrayList<Integer> intList = new ArrayList<>();    // Integer만 저장 가능
```

## ArrayList의 단점

1. **메모리 낭비**: 정확한 크기를 알지 못하면 메모리가 낭비됩니다
2. **비효율적인 중간 삽입/삭제**: 데이터를 앞이나 중간에 추가하거나 삭제할 때 비효율적입니다

## 다음 단계

이런 단점을 해결한 자료 구조는 **LinkedList**입니다.
