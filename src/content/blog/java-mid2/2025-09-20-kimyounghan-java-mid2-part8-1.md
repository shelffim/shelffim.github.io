---
title: "컬렉션 프레임워크 - HashSet"
pubDate: 2025-09-20
description: "김영한님의 자바 중급 2편 강의 part 8(컬렉션 프레임워크 - HashSet) 학습 정리"
---

> **출처**: [김영한의 자바 중급 2편 강의](https://inf.run/ir9Dw) - Section 8 : 컬렉션 프레임워크 - HashSet

## Set이란?

Set은 중복을 허용하지 않고, 순서를 보장하지 않는 자료 구조입니다.

```java
Set<String> set = new HashSet<>();
set.add("apple");
set.add("banana");
set.add("apple");  // 중복 추가 시도
System.out.println(set);  // [apple, banana] - 중복 제거됨
```

## Set의 문제점

데이터를 추가할 때 중복 데이터가 있는지 전체 데이터를 항상 확인해야 합니다.

## HashSet의 해결책

해시 알고리즘을 사용하는 Set은 해시 코드를 이용해 데이터 저장 위치를 빠르게 찾습니다.

```java
HashSet<String> hashSet = new HashSet<>();
hashSet.add("data");  // 해시 코드로 빠른 위치 계산
```

## HashSet 검색 과정

HashSet에서 `contains()` 메서드로 데이터를 검색할 때:

1. **해시 인덱스 계산**: 검색할 데이터의 해시 코드로 버킷 위치 찾기
2. **버킷 내 검색**: 해당 버킷 안에서 `equals()` 메서드로 데이터 비교

```
해시 인덱스 → 해당 버킷 → equals() 비교 → 결과
```

## 제네릭과 타입 안전성

HashSet에 제네릭을 도입하면 데이터 타입을 컴파일 시 결정할 수 있어 타입 안전성을 확보할 수 있습니다.

```java
HashSet<String> stringSet = new HashSet<>();  // String만 저장
HashSet<Integer> intSet = new HashSet<>();    // Integer만 저장
```
