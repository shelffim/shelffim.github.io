---
title: "컬렉션 프레임워크 - 해시(Hash)"
pubDate: 2025-09-20
description: "김영한님의 자바 중급 2편 강의 part 7(컬렉션 프레임워크 - 해시(Hash)) 학습 정리"
---

> **출처**: [김영한의 자바 중급 2편 강의](https://inf.run/ir9Dw) - Section 7 : 컬렉션 프레임워크 - 해시(Hash)

## 배열 검색의 문제점

배열에 데이터를 검색할 때는 모든 데이터를 순회해야 하기 때문에 인덱스를 사용할 수 없습니다. 데이터의 값을 인덱스로 사용하면 데이터를 검색할 때 빠르지만, 입력 값의 범위가 커지면 메모리 낭비가 심합니다.

```java
// 문제: 큰 범위의 값으로 인한 메모리 낭비
int[] arr = new int[1000000];  // 1~1000000까지의 값 저장 시
arr[999999] = 999999;  // 마지막 인덱스만 사용
```

## 해시 인덱스

배열의 크기로 나머지 연산을 하면 결과 값은 배열의 크기를 넘지 않기 때문에 넓은 범위의 값을 인덱스로 사용할 수 있습니다.

원래의 값을 인덱스로 사용하기 위해 계산한 인덱스를 **해시 인덱스**라고 합니다.

```java
// 해시 인덱스 계산
int value = 12345;
int arraySize = 10;
int hashIndex = value % arraySize;  // 12345 % 10 = 5

// 배열 인덱스 5에 값 저장
arr[hashIndex] = value;
```

## 해시 충돌

같은 해시 인덱스가 나오는 것을 **해시 충돌**이라고 합니다.

```java
// 해시 충돌 예시
int value1 = 15;  // 15 % 10 = 5
int value2 = 25;  // 25 % 10 = 5
// 같은 인덱스 5에 저장되어 충돌 발생
```

## 해시 충돌 해결 방법

해시 충돌은 낮은 확률로 일어나기 때문에 같은 해시 인덱스의 값을 같은 인덱스에 함께 저장하기 위해 배열 인덱스에 연결 리스트 같은 자료구조를 연결하여 사용함으로써 해시 충돌을 해결할 수 있습니다.

```
인덱스 0: null
인덱스 1: null
인덱스 2: null
인덱스 3: null
인덱스 4: null
인덱스 5: 15 → 25 → 35  (연결 리스트로 충돌 해결)
인덱스 6: null
...
```

## 해시 테이블 효율성

입력한 데이터의 수가 배열의 크기를 75%를 넘지 않으면 해시 충돌이 자주 일어나지 않습니다.

- **권장 로드 팩터**: 0.75 (75%)
- **예시**: 배열 크기 100 → 데이터 75개까지 효율적

## 해시 코드와 문자열

해시 인덱스는 배열의 인덱스로 사용해야 하므로 양의 정수로만 사용할 수 있습니다. 문자열을 해시 인덱스로 사용하기 위해서는 문자열을 해시 함수를 통해 해시 코드로 변환하고 해시 코드로 해시 인덱스를 만듭니다.

```java
String str = "Hello";
int hashCode = str.hashCode();        // 문자열을 해시 코드로 변환
int hashIndex = hashCode % arraySize; // 해시 코드로 인덱스 계산
```

## 객체의 해시 코드

모든 객체가 자신만의 해시 코드를 표현할 수 있는 기능을 가집니다. 객체의 참조값을 기반으로 해시 코드를 만들기 때문에 객체의 인스턴스가 다르면 해시 코드도 다릅니다.

```java
String str1 = new String("Hello");
String str2 = new String("Hello");
// str1.hashCode() != str2.hashCode() (다른 인스턴스)
```

## hashCode()와 equals() 재정의

해시 자료 구조를 사용하려면 반드시 `hashCode()`와 `equals()` 메서드를 재정의해야 합니다.

### 중요 규칙

두 객체가 `equals()`로 같으면, `hashCode()` 메서드도 같은 값을 반환해야 합니다.

```java
public class Person {
    private String name;
    private int age;

    @Override
    public boolean equals(Object obj) {
        // equals 로직
        return this.name.equals(((Person)obj).name);
    }

    @Override
    public int hashCode() {
        return name.hashCode();  // equals와 일치하는 해시 코드
    }
}
```
