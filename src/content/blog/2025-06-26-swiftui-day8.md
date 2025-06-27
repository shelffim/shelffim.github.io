---
title: "SwiftUI Day 8 학습 후기"
pubDate: "2025-06-26"
description: "SwiftUI Day 8에서 배운 함수 오류 처리, 기본값, 배열 성능 최적화 등 핵심 개념을 정리한 학습 회고입니다."
author: "HyunJun"
tags:
  [
    "SwiftUI",
    "Swift",
    "공부회고",
    "오류처리",
    "throws",
    "기본값",
    "배열성능",
    "더블링",
  ]
---

# SwiftUI Day 8 학습 후기

### 1. 학습 날짜 및 강의 링크

- 📅 2025년 6월 26일
- 🔗 [Hacking with SwiftUI Day 8](https://www.hackingwithswift.com/100/swiftui/8)

---

### 2. 오늘 배운 핵심 문법: 오류 처리와 기본값

이번에는 **함수의 오류 처리 방법**과 **매개변수 기본값**에 대해 학습했다.  
Swift의 안전한 오류 처리 시스템과 성능 최적화에 대한 깊이 있는 내용까지 다루었다.

---

### 3. 매개변수 기본값 (Default Values)

#### ✅ 기본값 설정 방법

함수 호출 시 매개변수를 생략할 수 있도록 기본값을 제공할 수 있다.

```swift
func greet(name: String, greeting: String = "안녕하세요") {
    print("\(greeting), \(name)님!")
}

// 기본값 사용
greet(name: "홍길동") // "안녕하세요, 홍길동님!"

// 기본값 재정의
greet(name: "김철수", greeting: "반갑습니다") // "반갑습니다, 김철수님!"
```

#### ✅ 여러 기본값 사용

```swift
func createUser(name: String, age: Int = 25, city: String = "서울", isActive: Bool = true) {
    print("사용자: \(name), 나이: \(age), 도시: \(city), 활성화: \(isActive)")
}

createUser(name: "박영희") // 기본값 사용
createUser(name: "이민수", age: 30) // 일부만 재정의
```

---

### 4. 함수의 오류 처리 (Error Handling)

Swift의 오류 처리는 **4단계 과정**으로 이루어진다.

#### ✅ 1단계: 오류 정의

먼저 발생할 수 있는 오류를 정의한다.

```swift
enum PasswordError: Error {
    case short
    case obvious
    case simple
}
```

#### ✅ 2단계: 오류를 던지는 함수 작성

함수가 자체적으로 처리하지 않고 오류를 던질 경우, 반환 유형 전에 `throws`를 표기한다.

```swift
func checkPassword(_ password: String) throws -> String {
    if password.count < 5 {
        throw PasswordError.short
    }

    if password == "12345" {
        throw PasswordError.obvious
    }

    if password == "password" {
        throw PasswordError.simple
    }

    if password.count < 8 {
        return "OK"
    } else if password.count < 10 {
        return "Good"
    } else {
        return "Excellent"
    }
}
```

#### ✅ 3단계: do-try-catch로 오류 처리

```swift
let string = "12345"

do {
    let result = try checkPassword(string)
    print("비밀번호 등급: \(result)")
} catch PasswordError.short {
    print("비밀번호가 너무 짧습니다.")
} catch PasswordError.obvious {
    print("비밀번호가 너무 명확합니다.")
} catch PasswordError.simple {
    print("비밀번호가 너무 단순합니다.")
} catch {
    print("알 수 없는 오류가 발생했습니다: \(error.localizedDescription)")
}
```

#### ✅ 4단계: try? 와 try! 사용

```swift
// try? - 오류 발생 시 nil 반환
if let result = try? checkPassword("안전한비밀번호") {
    print("결과: \(result)")
}

// try! - 오류 발생 시 앱 크래시 (위험!)
let result = try! checkPassword("매우안전한비밀번호")
```

---

### 5. 배열 성능 최적화

#### ✅ removeAll()의 keepingCapacity 옵션

```swift
var numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

// 기본값 (keepingCapacity: false)
numbers.removeAll() // 메모리도 함께 해제

// keepingCapacity: true
numbers.removeAll(keepingCapacity: true) // 항목만 제거, 메모리는 유지
```

#### ✅ [추가 학습] Swift 배열의 메모리 관리

Swift는 **성능 최적화**를 위해 배열에 약간의 여유분을 포함한 메모리를 확보한다.

```swift
var array = [1, 2, 3]
// 실제로는 3개 이상의 항목을 저장할 수 있는 메모리가 할당됨
```

#### ✅ [추가 학습] 더블링 (Doubling) 전략

Swift 배열의 메모리 확장 방식:

1. **여유 공간이 있는 경우**: 새 항목을 기존 메모리에 추가
2. **여유 공간이 없는 경우**: 새로운 더 큰 메모리에 기존 데이터를 복사하고 새 데이터 추가

```swift
var numbers = [1, 2, 3]
// 초기: 3개 항목 + 여유 공간

numbers.append(4)
// 여유 공간이 있으므로 기존 메모리에 추가

numbers.append(contentsOf: [5, 6, 7, 8, 9, 10])
// 여유 공간 부족 → 더블링 발생
// 새로운 메모리 할당 + 기존 데이터 복사
```

#### ✅ [추가 학습] 더블링 전략의 장점

**왜 매번 메모리를 늘리지 않고 더블링을 사용할까?**

| 전략                 | 장점                  | 단점               |
| -------------------- | --------------------- | ------------------ |
| **매번 메모리 증가** | 메모리 효율적         | O(n²) 시간 복잡도  |
| **더블링 전략**      | O(1) 평균 시간 복잡도 | 약간의 메모리 낭비 |

**더블링의 장점:**

- **평균적으로 O(1) 성능**: append가 자주 일어나도 평균적으로 성능을 유지
- **작업 빈도 감소**: 배열이 커질수록 메모리 재할당 빈도가 점점 줄어듦
- **분할상환 분석**: 전체적으로 봤을 때 효율적

```swift
// 예시: 1부터 1000까지 추가
var array: [Int] = []

for i in 1...1000 {
    array.append(i)
    // 메모리 재할당은 약 10번 정도만 발생 (log₂(1000) ≈ 10)
}
```

🔗 참고자료: [Swift의 Array는 무한대로 커질까?](https://velog.io/@kirri1124/Swift의-Array는-무한대로-커질까), [Array Doubling/분할상환분석](https://zeddios.tistory.com/62)

---

### 6. 성능 최적화 팁

#### ✅ 배열 사용 시 주의사항

```swift
// ❌ 비효율적: 매번 새로운 배열 생성
var result: [Int] = []
for i in 1...1000 {
    result = result + [i] // 새로운 배열 생성
}

// ✅ 효율적: append 사용
var result: [Int] = []
for i in 1...1000 {
    result.append(i) // 기존 배열에 추가
}

// ✅ 더 효율적: 초기 용량 지정
var result = [Int]()
result.reserveCapacity(1000) // 초기 용량 예약
for i in 1...1000 {
    result.append(i)
}
```

---

### 7. 회고

오늘은 Swift의 **안전한 오류 처리 시스템**과 **성능 최적화**에 대해 깊이 있게 학습할 수 있었다.

특히 **더블링 전략**에 대한 학습이 가장 인상적이었다. 처음에는 "왜 매번 메모리를 늘리지 않을까?"라는 의문이 있었지만,  
분할상환 분석을 통해 **전체적인 성능 관점에서 더블링이 훨씬 효율적**이라는 것을 이해할 수 있었다.

> 📌 **"더블링 전략은 append가 자주 일어나도 평균적으로 O(1) 성능을 유지하며, 배열이 커질수록 메모리 재할당 빈도가 점점 줄어든다."**

Swift의 오류 처리 시스템도 매우 체계적이었다.  
`throws`, `do-try-catch` 패턴을 통해 **컴파일 타임에 오류 처리를 강제**하고,  
**런타임에 안전하게 오류를 처리**할 수 있다는 점이 인상적이었다.

`removeAll(keepingCapacity: true)` 같은 세밀한 성능 제어 옵션도 Swift가 **개발자에게 얼마나 많은 제어권을 제공하는지** 보여주는 좋은 예시였다.

앞으로도 Swift의 **"왜 이렇게 설계되었는가?"**와 **"어떻게 성능을 최적화할 수 있는가?"**에 대한 고민을 계속하며 학습해나가야겠다.
