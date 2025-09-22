---
title: "Map"
pubDate: 2025-09-21
description: "김영한님의 자바 중급 2편 강의 part 10(컬렉션 프레임워크 - Map, Stack, Queue) 학습 정리"
---

> **출처**: [김영한의 자바 중급 2편 강의](https://inf.run/ir9Dw) - Section 10 : 컬렉션 프레임워크 - Map, Stack, Queue

## Map이란?

Map은 키-값의 쌍을 저장하는 자료 구조로, 키는 중복을 허용하지 않고, 값은 중복을 허용합니다. 키를 통해 빠르게 검색할 수 있고, 순서를 유지하지 않습니다.

```java
Map<String, Integer> map = new HashMap<>();
map.put("apple", 100);
map.put("banana", 200);
```

## Map 구현체 종류

Map 인터페이스로 HashMap, TreeMap, LinkedHashMap 등 여러 구현 클래스가 있습니다.

### HashMap

해시를 사용해서 요소를 저장하기 때문에 삽입, 삭제, 검색 작업은 일반적으로 **O(1)**의 성능을 가집니다.

### LinkedHashMap

연결리스트를 사용하여 입력 순서에 따라 순회가 가능합니다. 대부분의 작업은 **O(1)**의 성능을 가집니다.

### TreeMap

레드-블랙 트리를 사용하여 정렬된 순서로 요소를 저장합니다. 대부분의 작업은 **O(log n)**의 성능을 가집니다.

## Map 조회 방법

### keySet() - 모든 키 조회

`keySet()` 메서드를 호출하면 Set으로 모든 key를 조회할 수 있습니다.

```java
Set<String> keys = map.keySet();
```

### values() - 모든 값 조회

`values()` 메서드를 호출하면 Collection으로 모든 value를 조회할 수 있습니다.

```java
Collection<Integer> values = map.values();
```

## Entry 객체

Entry는 키-값의 쌍으로 이루어진 간단한 객체로 Map 내부에서 사용됩니다.

## Map 데이터 조작

### 값 덮어쓰기

Map에 값을 저장할 때 같은 키에 다른 값을 저장하면 기존 값을 덮어씁니다.

```java
map.put("apple", 100);
map.put("apple", 150);  // 기존 값 100이 150으로 덮어써짐
```

### 조건부 저장

`putIfAbsent()` 메서드를 호출하면 키가 없는 경우에만 데이터를 저장하고 싶을 때 사용합니다.

```java
map.putIfAbsent("orange", 300);  // 키가 없을 때만 저장
```

## HashSet과 HashMap의 관계

HashSet의 구현은 HashMap의 구현을 사용합니다.

## Map 사용 시 주의사항

Map의 key로 사용되는 객체는 `hashCode()`와 `equals()` 메서드를 재정의해야 합니다.
