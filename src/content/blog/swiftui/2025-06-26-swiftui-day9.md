---
title: "SwiftUI Day 9 학습 후기"
pubDate: "2025-06-26"
description: "SwiftUI Day 9에서 배운 Closures, 후행 클로저, 함수형 프로그래밍 등 핵심 개념을 정리한 학습 회고입니다."
author: "HyunJun"
tags:
  [
    "SwiftUI",
    "Swift",
    "공부회고",
    "Closures",
    "후행클로저",
    "함수형프로그래밍",
    "map",
    "filter",
  ]
---

# SwiftUI Day 9 학습 후기

### 1. 학습 날짜 및 강의 링크

- 📅 2025년 6월 26일
- 🔗 [Hacking with SwiftUI Day 9](https://www.hackingwithswift.com/100/swiftui/9)

---

### 2. 오늘 배운 핵심 문법: Closures (클로저)

이번에는 **Swift의 클로저**에 대해 학습했다.  
클로저는 Swift에서 가장 복잡하면서도 강력한 기능 중 하나로,  
함수형 프로그래밍의 핵심 개념이자 SwiftUI에서 광범위하게 사용되는 기능이다.

---

### 3. 클로저란 무엇인가?

#### ✅ 클로저의 정의

클로저는 **익명 함수**로, 변수에 직접 할당하거나 다른 함수에 매개변수로 전달할 수 있다.

```swift
// 일반 함수
func greet(name: String) {
    print("안녕하세요, \(name)님!")
}

// 클로저 표현식
let greetClosure = { (name: String) in
    print("안녕하세요, \(name)님!")
}

// 사용법
greet(name: "홍길동")
greetClosure("홍길동")
```

#### ✅ 클로저의 특징

- **함수를 변수에 직접 할당** 가능
- **다른 함수의 매개변수로 전달** 가능
- **별도 함수 생성 없이** 즉시 사용 가능
- **나중에 실행할 코드를 저장**하는 용도

---

### 4. 클로저 기본 문법

#### ✅ 클로저 표현식 구조

```swift
{ (매개변수들) -> 반환타입 in
    // 클로저 내용
}
```

#### ✅ 매개변수가 있는 클로저

```swift
let add = { (a: Int, b: Int) -> Int in
    return a + b
}

let result = add(5, 3) // 8
```

#### ✅ 매개변수 없이 값을 반환하는 클로저

```swift
let getRandomNumber = { () -> Int in
    return Int.random(in: 1...100)
}

let random = getRandomNumber()
```

---

### 5. 후행 클로저 (Trailing Closures)

#### ✅ 후행 클로저 기본 사용법

클로저가 함수의 마지막 매개변수일 때, 괄호 밖으로 빼낼 수 있다.

```swift
// 일반적인 클로저 사용
let numbers = [1, 2, 3, 4, 5]
let doubled = numbers.map({ (number: Int) -> Int in
    return number * 2
})

// 후행 클로저 사용
let doubledTrailing = numbers.map { (number: Int) -> Int in
    return number * 2
}
```

#### ✅ [추가 학습] 외부 매개변수 이름의 의미

```swift
func makeArray(size: Int, using generator: () -> Int) -> [Int] {
    var numbers = [Int]()
    for _ in 0..<size {
        let newNumber = generator()
        numbers.append(newNumber)
    }
    return numbers
}

// 후행 클로저 사용
let rolls = makeArray(size: 50) {
    Int.random(in: 1...20)
}
```

**왜 `using`이라는 외부 매개변수 이름을 사용했을까?**

- **함수를 더 의도적으로 읽기 좋게 만들기 위함**
- Swift의 **함수 이름 자체가 설명문**이 되도록 하는 디자인 철학
- `makeArray(size: 50, using: { ... })` → "50 크기의 배열을 만들되, 다음 생성기를 사용해서"

---

### 6. 약식 구문 (Shorthand Syntax)

#### ✅ 타입 추론 활용

```swift
let numbers = [1, 2, 3, 4, 5]

// 전체 문법
let doubled = numbers.map({ (number: Int) -> Int in
    return number * 2
})

// 타입 추론으로 간소화
let doubled = numbers.map({ number in
    return number * 2
})

// return 생략
let doubled = numbers.map({ number in
    number * 2
})

// 매개변수 이름 생략 ($0, $1, ...)
let doubled = numbers.map({ $0 * 2 })

// 후행 클로저 + 약식 구문
let doubled = numbers.map { $0 * 2 }
```

#### ✅ 약식 구문 사용 시 주의사항

- **매개변수가 많거나 복잡한 경우**에는 가독성을 위해 매개변수 이름을 사용하는 것을 권장
- **간단한 변환 작업**에는 약식 구문이 유용

---

### 7. 고차 함수 (Higher-Order Functions)

#### ✅ filter() 함수

조건에 대해 `true`를 반환하는 모든 항목을 포함하는 새로운 배열을 반환한다.

```swift
let numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

// 짝수만 필터링
let evenNumbers = numbers.filter { $0 % 2 == 0 }
print(evenNumbers) // [2, 4, 6, 8, 10]

// 5보다 큰 수만 필터링
let largeNumbers = numbers.filter { $0 > 5 }
print(largeNumbers) // [6, 7, 8, 9, 10]
```

#### ✅ map() 함수

배열의 모든 항목을 변환하고 변환된 모든 항목을 새로운 배열로 반환한다.

```swift
let numbers = [1, 2, 3, 4, 5]

// 숫자를 문자열로 변환
let stringNumbers = numbers.map { "숫자 \($0)" }
print(stringNumbers) // ["숫자 1", "숫자 2", "숫자 3", "숫자 4", "숫자 5"]

// 제곱 계산
let squared = numbers.map { $0 * $0 }
print(squared) // [1, 4, 9, 16, 25]

// 다른 타입으로 변환 가능
let isEven = numbers.map { $0 % 2 == 0 }
print(isEven) // [false, true, false, true, false]
```

---

### 8. 클로저를 사용하는 이유

#### ✅ 1. 작업 완료 후 실행할 동작을 나중에 지정

#### ✅ 2. 비동기 작업 중 앱이 멈추지 않게 하기

---

### 9. [추가 학습] 다른 언어의 클로저 유사 기능

#### 🔹 Kotlin의 람다 (Lambda)

```kotlin
// Kotlin 람다 예시
fun downloadData(url: String, callback: (String) -> Unit) {
    // 네트워크 요청 처리 (예시)
    Thread {
        Thread.sleep(1000) // 1초 후
        callback("데이터 도착")
    }.start()
}

// 사용
downloadData("https://example.com") { result ->
    println("받은 데이터: $result")
}
```

#### 🔹 Flutter의 Future와 async/await

```dart
// Flutter 예시
void fetchData(Function(String) callback) {
  Future.delayed(Duration(seconds: 1), () {
    callback("서버 응답 완료");
  });
}

// 사용
fetchData((data) {
  print("데이터 받음: $data");
});
```

#### 🔹 공통점

- **함수형 프로그래밍** 지원
- **비동기 처리**에 활용
- **코드의 재사용성**과 **가독성** 향상
- **콜백 패턴** 구현

---

### 10. 회고

오늘은 Swift의 **클로저**에 대해 깊이 있게 학습할 수 있었다.  
처음에는 문법이 복잡해 보였지만, 실제 사용 예제를 통해 **왜 클로저가 필요한지** 이해할 수 있었다.

특히 **후행 클로저**와 **약식 구문**을 통해 Swift가 **가독성과 편의성**을 어떻게 균형있게 제공하는지 배울 수 있었다.

> 📌 **"클로저는 언젠가 하고 싶은 일이 있지만, 꼭 지금이 되는 것은 아닌 기능을 저장하는 용도로 사용된다."**

다른 언어들과의 비교를 통해 **함수형 프로그래밍의 보편성**을 느낄 수 있었고,  
Swift의 `using` 같은 외부 매개변수 이름을 통해 **Swift의 디자인 철학**을 다시 한번 체감할 수 있었다.

클로저는 SwiftUI에서 광범위하게 사용되므로, 이번 학습이 앞으로의 SwiftUI 개발에 큰 도움이 될 것 같다.  
복잡하지만 강력한 기능이므로 꾸준히 연습하고 익숙해져야겠다.
