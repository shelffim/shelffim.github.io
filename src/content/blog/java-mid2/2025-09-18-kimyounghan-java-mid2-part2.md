---
title: "김영한의 자바 중급 2편 강의 - part 2: 제네릭 1"
pubDate: 2025-09-18
description: "김영한님의 자바 중급 2편 강의 part 2(제네릭 1) 학습 정리"
---

> **출처**: [김영한의 자바 중급 2편 강의](https://inf.run/ir9Dw) - Section 2: 제네릭 1

## 제네릭이 필요한 이유

여러 데이터 타입을 저장하기 위해 타입별 클래스를 계속 만들면 코드 중복이 발생하고 수정이나 관리하기 어렵습니다. 또한 데이터를 꺼낼 때 형변환(다운 캐스팅)을 시도하여 런타임 오류 위험이 있습니다.

```java
// 제네릭 없이 사용하는 경우
Object obj1 = "문자열";
Object obj2 = 123;

String str = (String) obj1;  // 형변환 필요
Integer num = (Integer) obj2;  // 형변환 필요
```

## 제네릭이란?

제네릭은 여러 타입을 다룰 수 있게 해주며, 코드의 재사용성을 높이면서 타입 안전성을 제공합니다. 제네릭은 사용할 타입을 미리 결정하지 않습니다.

```java
// 제네릭을 사용하는 경우
Box<String> stringBox = new Box<>();
Box<Integer> intBox = new Box<>();

stringBox.setItem("문자열");
intBox.setItem(123);

String str = stringBox.getItem();  // 형변환 불필요
Integer num = intBox.getItem();    // 형변환 불필요
```

## 제네릭의 타입 안전성

제네릭을 사용하여 특정 타입 객체를 만들었을 때, 해당 타입과 다른 종류의 데이터를 넣으면 컴파일 오류가 발생합니다.

```java
Box<String> stringBox = new Box<>();
stringBox.setItem("문자열");
// stringBox.setItem(123);  // 컴파일 오류! String 타입만 허용
```

## 제네릭 타입 매개변수 명명 규칙

제네릭의 타입 매개변수는 일반적으로 대문자를 사용하고 단어의 첫글자를 사용하는 관례를 따릅니다.

- `T`: Type (일반적인 타입)
- `E`: Element (컬렉션의 요소)
- `K`: Key (맵의 키)
- `V`: Value (맵의 값)
- `N`: Number (숫자 타입)

```java
public class Box<T> {
    private T item;

    public void setItem(T item) {
        this.item = item;
    }

    public T getItem() {
        return item;
    }
}
```

## 제네릭 타입 제약사항

제네릭의 타입 인자(<>: 다이아몬드)에는 기본 타입을 사용할 수 없습니다. 대신 래퍼 클래스를 사용해야 합니다.

```java
// 잘못된 사용
// Box<int> intBox = new Box<>();  // 컴파일 오류!

// 올바른 사용
Box<Integer> intBox = new Box<>();
Box<Double> doubleBox = new Box<>();
Box<Boolean> booleanBox = new Box<>();
```
