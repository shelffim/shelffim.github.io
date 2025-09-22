---
title: "순회"
pubDate: 2025-09-22
description: "김영한님의 자바 중급 2편 강의 part 11(컬렉션 프레임워크 - 순회, 정렬, 전체 정리) 학습 정리"
---

> **출처**: [김영한의 자바 중급 2편 강의](https://inf.run/ir9Dw) - Section 11 : 컬렉션 프레임워크 - 순회, 정렬, 전체 정리

## 순회란?

순회란 자료 구조에 들어있는 데이터를 차례대로 접근해서 처리하는 것을 뜻하는데, 각각의 자료 구조마다 데이터를 접근하는 방법이 다릅니다.

## Iterable과 Iterator 인터페이스

모든 자료 구조를 동일한 방법으로 순회할 수 있는 방법을 제공하기 위해 **Iterable**, **Iterator** 인터페이스를 제공합니다.

### Iterable 인터페이스

반복 가능한 객체를 나타내는 인터페이스로, Iterator 반복자를 반환합니다.

### Iterator 인터페이스

반복자를 나타내는 인터페이스로, 데이터를 차례대로 접근하는 방법을 제공합니다.

- `hasNext()`: 다음 요소가 있는지 확인
- `next()`: 다음 요소를 반환

```java
List<String> list = Arrays.asList("a", "b", "c");
Iterator<String> iterator = list.iterator();
while (iterator.hasNext()) {
    String item = iterator.next();
    System.out.println(item);
}
```

## Iterable vs Iterator

- **Iterable**: 순회 가능 상태를 부여하기 위한 인터페이스
- **Iterator**: 실제 순회 방법을 제공하는 인터페이스

Iterator는 단독으로 사용할 수 없습니다. Iterable 인터페이스를 구현한 클래스에서 `iterator()` 메서드를 호출하여 얻을 수 있습니다.

## for-each 문 사용

Iterable 인터페이스를 구현한 객체에 대해서 **for-each 문**을 사용할 수 있습니다.

```java
List<String> list = Arrays.asList("a", "b", "c");
for (String item : list) {
    System.out.println(item);
}
```

## 컬렉션 프레임워크와 순회

### Collection 계열

Collection 인터페이스는 Iterable 인터페이스를 구현하고 있고, List, Set, Queue 인터페이스도 Iterable 인터페이스를 구현하고 있습니다.

### Map의 순회

Map의 경우는 Iterable 인터페이스를 구현하고 있지 않지만 `keySet()`, `values()`를 호출하면 Collection을 반환하기 때문에 key나 value를 순회할 수 있습니다.

```java
Map<String, Integer> map = new HashMap<>();
map.put("a", 1);
map.put("b", 2);

// 키 순회
for (String key : map.keySet()) {
    System.out.println(key);
}

// 값 순회
for (Integer value : map.values()) {
    System.out.println(value);
}
```
