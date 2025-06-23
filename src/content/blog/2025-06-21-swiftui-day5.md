---
title: "SwiftUI Day 5 학습 후기"
pubDate: "2025-06-21"
description: "SwiftUI Day 5에서 배운 조건문(if, switch), 삼항 연산자, isEmpty vs count, Comparable 프로토콜 등 핵심 개념을 정리한 학습 회고입니다."
author: "HyunJun"
tags: ["SwiftUI", "Swift", "공부회고", "조건문", "switch", "Comparable"]
---

# SwiftUI Day 5 학습 후기

### 1. 학습 날짜 및 강의 링크

- 📅 2025년 6월 21일
- 🔗 [Hacking with SwiftUI Day 5](https://www.hackingwithswift.com/100/swiftui/5)

---

### 2. 오늘 배운 문법 정리

이번 강의에서는 Swift에서 자주 사용하는 조건문과 관련된 구문을 학습했다.

#### ✅ if문, if-else문

기본적인 조건문으로 가장 많이 사용되며, 특정 조건을 검사해 분기 처리를 한다.

```swift
let age = 20

if age >= 18 {
    print("성인입니다.")
} else {
    print("미성년자입니다.")
}
```

#### ✅ 삼항 조건 연산자

짧고 간결하게 조건 분기를 처리할 수 있는 구문.

```swift
let isLoggedIn = true
let status = isLoggedIn ? "로그인 완료" : "로그인 필요"
```

#### ✅ switch문

Swift의 switch는 다른 언어와는 다르게 더욱 엄격한 방식으로 작동한다.

- 모든 가능한 값(case)을 반드시 처리해야 함
- 각 case마다 `break`가 필요 없음
- 기본적으로 `fallthrough`가 적용되지 않음
- 일치하는 **첫 번째 case만 실행**

```swift
let direction = "북"

switch direction {
case "북":
    print("위로 이동합니다.")
case "남":
    print("아래로 이동합니다.")
default:
    print("방향을 알 수 없습니다.")
}
```

---

### 3. [추가 학습] count == 0 vs isEmpty

`count == 0` 과 `isEmpty`는 같은 결과를 반환하는 것처럼 보이지만, 내부 동작 방식은 다르다.

| 항목         | 동작 방식                      | 성능               |
| ------------ | ------------------------------ | ------------------ |
| `isEmpty`    | `startIndex == endIndex` 확인  | ✅ 빠름            |
| `count == 0` | 전체 문자열 순회하며 길이 계산 | ❌ 상대적으로 느림 |

즉, 단순히 비어 있는지 확인하고 싶을 때는 **`isEmpty`가 더 효율적**이다.  
반면 **정확한 개수(문자 수, 배열 길이 등)를 알고 싶을 때는 `count`를 사용하는 것이 맞다.**

🔗 참고자료: [isEmpty vs count - 블로그](https://imjhk03.github.io/posts/isEmpty-vs-count/)

예시:

```swift
let name = "홍길동"

if !name.isEmpty {
    print("이름이 입력되었습니다.")
}
```

---

### 4. [추가 학습] Comparable 프로토콜

이번 강의에 등장한 예제에서 `Comparable` 프로토콜을 채택한 열거형을 사용했는데,  
궁금해서 `Comparable`이 정확히 뭔지 찾아봤다.

#### ✅ Comparable 프로토콜이란?

- `<`, `<=`, `>=`, `>` 등의 **관계 연산자를 사용할 수 있도록 만들어주는 프로토콜**
- 기본 자료형(Int, Double 등)은 자동으로 비교 가능
- 하지만 **구조체나 클래스 등 복합 타입**은 비교 기준이 명확하지 않기 때문에,  
  프로토콜을 채택할 때 **직접 구현**이 필요하다.

```swift
struct Score: Comparable {
    var value: Int

    static func < (lhs: Score, rhs: Score) -> Bool {
        return lhs.value < rhs.value
    }
}
```

#### ✅ 열거형(enum)에서의 Comparable

- enum은 순서를 가지고 있으므로, **별도의 구현 없이도 `Comparable`을 채택하면 대소 비교 가능**
- 단, 기본 비교 기준은 **정의된 순서(위 → 아래)** 이다.

```swift
enum Priority: Comparable {
    case low, medium, high
}

let a = Priority.low
let b = Priority.high

print(a < b) // true
```

🔗 참고자료: [Comparable 프로토콜 정리 블로그](https://kybeen.tistory.com/149)

---

### 5. [특징 정리] Swift의 switch가 다른 언어와 다른 점

Swift의 `switch` 문은 아래와 같은 특징이 있어 **타 언어 개발자들이 헷갈리기 쉬운 부분**이다.

| 항목                     | Swift                         | Java / C 등  |
| ------------------------ | ----------------------------- | ------------ |
| case별 `break` 필요 여부 | ❌ 필요 없음                  | ✅ 필요함    |
| fallthrough 여부         | ❌ 명시적으로 써야 작동       | ✅ 기본 작동 |
| 모든 case 커버 요구      | ✅ 필수 (아니면 default 필요) | ❌ 선택적    |

또한 Swift는 **조건에 맞는 첫 번째 case만 실행**하므로,  
`fallthrough`가 필요한 경우에는 명시적으로 작성해주어야 한다.

```swift
let grade = "B"

switch grade {
case "A":
    print("우수")
case "B":
    print("양호")
    fallthrough
case "C":
    print("보통")
default:
    print("기타")
}
```

---

### 6. 회고

오늘은 Swift의 조건문을 다양하게 살펴보고,  
단순한 if/else를 넘어서 switch의 구조적 특징까지 체감할 수 있었다.

추가로,

- `isEmpty` vs `count == 0` 비교를 통해 **성능 관점에서의 미묘한 차이**도 이해할 수 있었고,
- `Comparable` 프로토콜을 통해 Swift의 타입 비교가 얼마나 **정교하게 설계되어 있는지** 깨닫게 되었다.

Swift는 단순한 문법 너머로, **의미와 안전성을 강조하는 언어라는 느낌이 강하게 들었다.**  
앞으로도 어떤 기능이 "왜 이렇게 설계됐는지" 고민하며 공부해봐야겠다고 다짐한 하루였다.
