---
title: "SwiftUI Day 3 학습 후기"
pubDate: "2025-06-19"
description: "SwiftUI Day 3에서 배운 reversed, sorted, Dictionary Optional, Set, enum 문법 등 핵심 개념을 정리한 학습 회고입니다."
author: "HyunJun"
tags:
  [
    "SwiftUI",
    "Swift",
    "공부회고",
    "reversed",
    "sorted",
    "Optional",
    "Set",
    "enum",
  ]
---

# SwiftUI Day 3 학습 후기

### 1. 학습한 강의

- 2025년 6월 19일
- Hacking with SwiftUI – Day 3 수강
- [강의 링크](https://www.hackingwithswift.com/100/swiftui/3)

---

### 2. reversed()와 sorted()의 차이

이번 강의에서 `reversed()`와 `sorted()`의 차이를 직접 실습하며 이해했다.

- `reversed()`는 `ReversedCollection<Array<String>>`와 같은 형식으로 출력된다.
- 왜냐하면 `reversed()`는 성능 최적화를 위해 **진짜 배열을 거꾸로 복사해서 만들지 않고**, **원본 배열을 거꾸로 보는 특수한 컬렉션 뷰**를 반환하기 때문이다.

즉, 실제로 거꾸로 된 배열을 메모리에 새로 만드는 것이 아니라, 기존 배열을 거꾸로 "참조"하는 방식이다.

```swift
let presidents = ["Bush", "Obama", "Trump", "Biden"]
print(presidents.reversed())
// 출력 타입: ReversedCollection<Array<String>>
```

- 반면 `sorted()`는 항상 새로운 배열(Array)을 반환한다.
- 정렬된 값을 가진 새로운 배열이 메모리에 생성되므로 출력 시에도 일반 배열처럼 표시된다.

```swift
let cities = ["Tokyo", "Rome", "London", "Budapest"]
print(cities.sorted())
// 출력: ["Budapest", "London", "Rome", "Tokyo"]
```

---

### 3. 딕셔너리에서 값 접근 시 Optional이 나오는 이유

딕셔너리에서 값을 가져올 때, 항상 옵셔널 타입이 반환되는 이유도 이해하게 되었다.

- 딕셔너리는 존재하지 않는 키로 접근할 수 있기 때문에,
- Swift는 **런타임 오류를 방지하기 위해 Optional 타입으로 반환**한다.
- 이로 인해 개발자는 `nil` 여부를 반드시 고려하게 되고,
  결과적으로 안정성이 높아진다.

예시 코드:

```swift
let students = ["홍길동": 90, "이순신": 85]
print(students["홍길동"])   // Optional(90)
print(students["김유신"])   // nil
```

이 옵셔널을 처리하는 방법은 세 가지 정도로 정리된다.

1. `if let`을 사용한 안전한 언래핑:

```swift
if let score = students["김유신"] {
    print("점수는 \(score)점입니다.")
} else {
    print("해당 학생의 점수가 없습니다.")
}
```

2. 강제 언래핑 (`!`) – 비추천:

```swift
print(students["홍길동"]!) // 해당 키가 없으면 런타임 에러
```

3. 기본값 제공 (`??` 연산자):

```swift
let score = students["김유신"] ?? 0
print("점수는 \(score)점입니다.")  // 출력: 점수는 0점입니다.
```

---

### 4. Set의 구조와 Array보다 빠른 이유

Set은 겉으로 보기엔 배열과 유사하지만, 다음과 같은 차이점이 있다:

- **중복된 항목을 허용하지 않는다.**
- **저장 순서가 없다.**

이번에 궁금했던 점은 "왜 Set이 Array보다 빠른가?"였는데, 이건 저장 방식의 차이 때문이었다.

- **Set은 Hash 기반 저장 구조**를 갖는다.
- 값을 저장할 때, Swift는 내부적으로 `hash` 값을 계산해서 해당 값이 저장될 위치를 바로 찾아낸다.
- 반면, **Array는 순차적 저장**이기 때문에 값을 검색할 때 처음부터 끝까지 하나씩 탐색해야 한다.

결론적으로 Set이 검색 성능에서 더 빠를 수밖에 없다.

```swift
var cities: Set = ["서울", "부산", "서울"]
print(cities)  // 중복 없이 출력됨
```

🔗 참고: https://didu-story.tistory.com/431

---

### 5. enum 문법의 새로운 표현 방법

Swift의 열거형(enum)은 기존에는 이렇게만 알고 있었다:

```swift
enum Weekday {
    case monday
    case tuesday
    case wednesday
    case thursday
    case friday
}
```

그런데 Swift에서는 이렇게 축약할 수 있다는 걸 알게 됐다:

```swift
enum Weekday {
    case monday, tuesday, wednesday, thursday, friday
}
```

게다가 열거형 값 재지정 시 타입을 반복할 필요도 없이 `.` 만 쓰면 된다:

```swift
var day = Weekday.monday
day = .tuesday
day = .friday
```

이런 점이 Swift 문법을 더욱 간결하고 읽기 쉽게 만들어주는 요소라고 느꼈다.

---

### 6. 회고

오늘 배운 내용은 기존에 내가 잘못 알고 있던 개념들을 많이 바로잡아줬다.

- `reversed()`가 단순히 배열을 뒤집는 것이 아니라, **메모리를 복사하지 않고 최적화된 방식**으로 작동한다는 점은 매우 인상 깊었다.
- `sorted()`는 항상 배열을 복사해 새로운 배열을 만든다는 점도 명확히 이해하게 됐다.
- 딕셔너리의 옵셔널 처리 방식은 안정성과 관련된 Swift의 철학이 잘 드러나는 부분이었다.
- Set이 빠른 이유가 Hash 구조 때문이라는 것도 실제로 디버깅해보면서 체감했고,
- Enum의 축약 문법은 앞으로 실제 코드에서 자주 활용하게 될 것 같다.

Swift의 내부 작동 원리를 이해하면 할수록, 단순히 외운 문법이 아닌 **이해 기반의 프로그래밍**이 가능해지는 걸 느꼈다.
