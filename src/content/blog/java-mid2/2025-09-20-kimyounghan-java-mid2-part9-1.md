---
title: "컬렉션 프레임워크 - Set"
pubDate: 2025-09-20
description: "김영한님의 자바 중급 2편 강의 part 9(컬렉션 프레임워크 - Set) 학습 정리"
---

> **출처**: [김영한의 자바 중급 2편 강의](https://inf.run/ir9Dw) - Section 9 : 컬렉션 프레임워크 - Set

## 컬렉션 프레임워크 구조

Collection 인터페이스는 컬렉션 프레임워크의 핵심 인터페이스입니다. 하위 인터페이스로 Set 등이 있습니다.

## Set 인터페이스

Set 인터페이스는 중복을 허용하지 않는 유일한 요소의 집합을 나타내는 컬렉션을 구현합니다. 순서를 보장하지 않으며, 특정 요소가 집합에 있는지 여부를 확인하는데 최적화되어 있습니다.

```
Collection (인터페이스)
    └── Set (인터페이스)
        ├── HashSet (구현체)
        ├── TreeSet (구현체)
        └── LinkedHashSet (구현체)
```

## Set 구현체 종류

### HashSet

해시 자료 구조를 사용해서 요소를 저장하고, 요소들은 특정한 순서 없이 저장됩니다.

```java
Set<String> hashSet = new HashSet<>();
hashSet.add("apple");
hashSet.add("banana");
hashSet.add("apple");  // 중복 제거
```

### LinkedHashSet

HashSet에 Linked List를 추가해서 요소들의 순서를 유지합니다. 순서대로 조회 시 요소들이 추가된 순서대로 반환되기 때문에 데이터의 유일성과 함께 삽입 순서를 유지해야 할 때 적합합니다.

```java
Set<String> linkedHashSet = new LinkedHashSet<>();
linkedHashSet.add("first");
linkedHashSet.add("second");
// 삽입 순서 유지됨
```

### TreeSet

이진 탐색 트리를 개선한 레드-블랙 트리를 내부에서 사용하여 요소들을 정렬된 순서로 저장됩니다. 순서의 기준은 비교자로 변경할 수 있습니다. 데이터들을 정렬된 순서로 유지하면서 집합의 특성을 유지해야 할 때 사용합니다.

```java
Set<Integer> treeSet = new TreeSet<>();
treeSet.add(3);
treeSet.add(1);
treeSet.add(2);
// 자동으로 정렬됨: [1, 2, 3]
```

TreeSet을 사용할 때는 데이터를 정렬하기 위한 기준이 필요한데, Comparable, Comparator를 구현하여 기준을 정할 수 있습니다.

## Iterator 사용법

iterator() 메서드는 컬렉션의 요소를 순회하는 방법을 제공합니다.

- `iterator.hasNext()`: 다음 요소가 있는지 확인
- `iterator.next()`: 다음 요소를 반환

```java
Set<String> set = new HashSet<>();
Iterator<String> iterator = set.iterator();
while (iterator.hasNext()) {
    String element = iterator.next();
}
```

## Set 생성자

Set 구현체의 생성자에 배열은 전달할 수 없지만 List는 전달할 수 있습니다.

```java
List<String> list = Arrays.asList("a", "b", "c");
Set<String> set = new HashSet<>(list);  // List로 생성 가능
```

## 집합 연산

### 합집합

`addAll()` 메서드를 사용합니다.

```java
set1.addAll(set2);  // set1에 set2의 모든 요소 추가
```

### 교집합

`retainAll()` 메서드를 사용합니다.

```java
set1.retainAll(set2);  // set1에 set1과 set2의 공통 요소만 유지
```

### 차집합

`removeAll()` 메서드를 사용합니다.

```java
set1.removeAll(set2);  // set1에서 set2의 요소들을 제거
```
