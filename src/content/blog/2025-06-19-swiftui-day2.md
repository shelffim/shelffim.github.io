---
title: "SwiftUI Day 2 학습 후기"
pubDate: "2025-06-19"
description: "Swift 문자열 보간의 성능적 이점과 사용자 정의 확장성에 대해 학습한 내용을 정리합니다."
author: "HyunJun"
tags: ["Swift", "문자열", "보간", "성능", "공부회고"]
---

# SwiftUI Day 2 학습 후기

## 1. 학습한 내용 요약

- [Hacking with SwiftUI Day 2 수강](https://www.hackingwithswift.com/100/swiftui/2)
- 문자열 연결 방식 두 가지 비교: `+` 연산 vs 문자열 보간(Interpolation)

## 2. 성능 차이 이해

Swift에서 문자열을 연결할 때 흔히 `+` 연산자를 사용하지만, 반복적으로 연결할 경우 성능에 영향을 줄 수 있다.

- `+` 연산은 각 연산마다 **새로운 문자열 인스턴스 생성**
- 반복이 많아질수록 메모리 사용량과 연산 시간이 증가

반면, **문자열 보간**(`\(value)`)은 컴파일러가 내부적으로 **효율적인 버퍼 관리**를 통해 한 번에 연결한다. 덕분에 메모리 및 성능이 최적화된다.

### 코드 예시: 성능 비교

```swift
// + 연산으로 문자열 연결
let luggageCode = "1" + "2" + "3" + "4" + "5"
print(luggageCode) // "12345"

// 문자열 보간으로 연결
let number = 11
let missionMessage = "Apollo \(number) landed on the moon."
print(missionMessage) // "Apollo 11 landed on the moon."
```

실제 대량의 문자열을 다룰 때는 보간 방식이 더 효율적임을 알 수 있다.

## 3. 문자열 보간의 고급 기능

문자열 보간은 단순한 텍스트 결합을 넘어서, **사용자 정의 방식으로 확장**할 수 있다.

- [Super-powered String Interpolation in Swift 5.0](https://www.hackingwithswift.com/articles/178/super-powered-string-interpolation-in-swift-5-0)
- 예를 들어, 특정 타입을 출력할 때 커스텀 포맷을 지정할 수 있다.

### 코드 예시: 사용자 정의 보간

```swift
struct User {
    let name: String
    let age: Int
}

extension String.StringInterpolation {
    mutating func appendInterpolation(_ user: User) {
        appendLiteral("\(user.name) (\(user.age)세)")
    }
}

let user = User(name: "HyunJun", age: 30)
print("사용자 정보: \(user)") // 사용자 정보: HyunJun (30세)
```

## 4. 느낀 점 / 회고

평소에 `+` 연산만 쓰던 습관에서 벗어나, 문자열 보간의 **성능적 이점과 확장성**을 처음으로 체감했다.
Swift는 문법이 단순해 보여도, 내부적으로 효율성과 유연성을 고려한 설계가 많다는 걸 다시 한 번 느꼈다.

앞으로 문자열을 다룰 때는 보간을 적극적으로 활용하고, 필요하다면 사용자 정의 보간도 시도해봐야겠다.
