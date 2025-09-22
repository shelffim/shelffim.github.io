---
title: "정렬"
pubDate: 2025-09-22
description: "김영한님의 자바 중급 2편 강의 part 11(컬렉션 프레임워크 - 순회, 정렬, 전체 정리) 학습 정리"
---

> **출처**: [김영한의 자바 중급 2편 강의](https://inf.run/ir9Dw) - Section 11 : 컬렉션 프레임워크 - 순회, 정렬, 전체 정리

## 배열 정렬

`Arrays.sort()` 메서드를 사용하여 배열을 정렬할 수 있습니다.

`Comparator` 인터페이스를 구현하여 정렬 기준을 정할 수 있습니다.

## Comparator 인터페이스

```java
public interface Comparator<T> {
    int compare(T o1, T o2);
}
```

### compare 메서드의 반환값 규칙

- 첫 번째 인수(o1)가 더 작으면: **음수** (예: -1)
- 두 값이 같으면: **0**
- 첫 번째 인수(o1)가 더 크면: **양수** (예: 1)

### 정렬 알고리즘의 동작 원리

정렬 알고리즘은 두 요소를 비교할 때 `compare` 메서드를 호출합니다:

- `compare(a, b)`가 **음수**를 반환하면 → `a`가 `b`보다 앞에 와야 함
- `compare(a, b)`가 **양수**를 반환하면 → `a`가 `b`보다 뒤에 와야 함

배열 `[5, 2, 8, 1]`을 정렬한다고 가정해보면:

- `compare(5, 2)` → 5 > 2이므로 양수 반환 → 5가 2보다 뒤에 와야 함
- `compare(2, 8)` → 2 < 8이므로 음수 반환 → 2가 8보다 앞에 와야 함

이런 식으로 계속 비교하면서 최종적으로 `[1, 2, 5, 8]`이 됩니다.

### 정렬 기준을 반대로 만드는 방법

#### 방법 1: reversed() 메서드 사용

```java
Arrays.sort(array, Comparator.naturalOrder().reversed());
```

#### 방법 2: compare 메서드에서 -1 곱하기

```java
public int compare(Integer o1, Integer o2) {
    return -1 * o1.compareTo(o2);
}
```

## Comparable 인터페이스

Comparable는 "비교 가능한"이라는 뜻으로, Comparable 인터페이스를 구현하면 객체에 비교 기능을 추가할 수 있습니다. 사용자 정의 객체에 기본 정렬 기준을 부여하려면 Comparable 인터페이스를 구현하면 됩니다.

## 정렬 우선순위

1. **Comparator**: 가장 높은 우선순위
2. **Comparable**: 두 번째 우선순위
3. **에러**: 둘 다 없으면 런타임 오류 발생

비교자를 별도로 구현해서 정렬 메서드에 전달하면 전달된 비교자가 항상 우선권을 가집니다.

## List 정렬

List를 기본 정렬할 때는 `list.sort(null)` 메서드를 사용하고, 별도의 비교자로 비교하고 싶다면 비교자를 넘겨주면 됩니다.

## 권장사항

객체의 정렬이 필요한 경우 **Comparable 인터페이스를 구현하는 것이 좋습니다**.
