---
title: "SwiftUI Day 6 학습 후기"
pubDate: "2025-06-23"
description: "SwiftUI Day 6에서 배운 반복문(for, while), break, continue, Labeled Statement 등 핵심 개념을 정리한 학습 회고입니다."
author: "HyunJun"
tags:
  [
    "SwiftUI",
    "Swift",
    "공부회고",
    "반복문",
    "for",
    "while",
    "break",
    "continue",
    "Labeled Statement",
  ]
---

# SwiftUI Day 6 학습 후기

### 1. 학습 날짜 및 강의 링크

- 📅 2025년 6월 23일
- 🔗 [Hacking with SwiftUI Day 6](https://www.hackingwithswift.com/100/swiftui/6)

---

### 2. 오늘 배운 핵심 문법: 반복문과 흐름 제어

이번에는 **Swift의 반복문**과 관련된 문법들을 학습했다.  
대표적으로 `for`, `while`, `continue`, `break`를 다루었고,  
추가적으로 **Labeled Statement**에 대해 공부했다.

---

### 3. 반복문 문법 정리

#### ✅ for-in 반복문

컬렉션 또는 범위를 순회하며 반복할 때 사용한다.

```swift
for number in 1...5 {
    print("현재 숫자: \(number)")
}
```

#### ✅ while 반복문

조건을 먼저 검사한 후 반복할 때 사용한다.

```swift
var i = 0
while i < 3 {
    print("i는 \(i)")
    i += 1
}
```

---

### 4. 흐름 제어: break & continue

#### 🔹 `break`

- 반복문 전체를 즉시 종료한다.

```swift
for num in 1...10 {
    if num == 5 {
        break
    }
    print(num)
}
// 1 ~ 4 출력됨
```

#### 🔹 `continue`

- 현재 반복만 건너뛰고 다음 반복으로 넘어간다.

```swift
for num in 1...5 {
    if num == 3 {
        continue
    }
    print(num)
}
// 1, 2, 4, 5 출력됨
```

---

### 5. [추가 학습] Labeled Statement (레이블 문)

기본적으로 `break`와 `continue`는 **가장 가까운 반복문에만 적용**된다.  
하지만 복잡한 중첩 루프에서 **특정 반복문을 명시적으로 제어하고 싶을 때**는  
**레이블(Labeled Statement)**를 사용할 수 있다.

```swift
outerLoop: for i in 1...3 {
    for j in 1...3 {
        if i * j == 4 {
            break outerLoop
        }
        print("i: \(i), j: \(j)")
    }
}
```

- 위 예제에서 `break outerLoop`는 **바깥 for문 전체를 종료**시킨다.
- 반복문 앞에 `label:`을 붙여 **지정한 루프만 정확히 제어할 수 있다.**

---

### 6. 회고

오늘은 Swift의 반복문 기본 문법과 흐름 제어에 대해 학습했다.  
`for-in`, `while`, `break`, `continue`는 대부분의 언어와 유사하지만,  
Swift의 **Labeled Statement**는 눈에 띄는 기능 중 하나였다.

하지만 개인적으로는 Labeled Statement가 **좋은 코드 스타일은 아니라고 생각**한다.  
`break outerLoop` 같은 방식은 **코드 가독성을 떨어뜨리고**,  
**중첩된 반복문을 사용하도록 유도하는 안티 패턴**이 될 수 있기 때문이다.

> 📌 [Manuel Meyer](https://medium.com/better-programming/labeled-statements-in-swift-how-to-give-loops-a-name-44e6fd374d9b)의 댓글에서처럼,  
> **"Labeled statements are a language feature that lets you control overly complicated code. But the better solution is: Don't write overly complicated code."**

> 📌 [rwgrier.medium.com](https://rwgrier.medium.com/swift-labeled-statements-3624ff30e0e7) 블로그 역시 **"라벨은 복잡한 제어를 가능하게는 하지만, 코드를 명확하게 만들지 않는다."**고 말하며,  
> 가장 좋은 해결책은 **애초에 중첩 반복문을 최소화하는 구조 설계**라는 점에 공감했다.

따라서 앞으로는 이런 제어 구조가 필요할 정도로 복잡한 루프가 생긴다면,  
**코드를 다시 분리하거나 로직을 함수화하는 리팩토링**을 먼저 고민하려고 한다.
