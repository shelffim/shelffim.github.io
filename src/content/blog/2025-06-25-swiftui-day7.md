---
title: "SwiftUI Day 7 학습 후기"
pubDate: "2025-06-25"
description: "SwiftUI Day 7에서 배운 함수 작성법, return문, 튜플 반환, 매개변수 라벨링 등 핵심 개념을 정리한 학습 회고입니다."
author: "HyunJun"
tags: ["SwiftUI", "Swift", "공부회고", "함수", "매개변수", "튜플", "return"]
---

# SwiftUI Day 7 학습 후기

### 1. 학습 날짜 및 강의 링크

- 📅 2025년 6월 25일
- 🔗 [Hacking with SwiftUI Day 7](https://www.hackingwithswift.com/100/swiftui/7)

---

### 2. 오늘 배운 핵심 문법: 함수 (Functions)

이번에는 **Swift의 함수**에 대해 학습했다.  
함수는 코드를 재사용 가능한 단위로 묶어주는 핵심적인 기능으로,  
매개변수 전달, 값 반환, 그리고 Swift만의 독특한 매개변수 라벨링 시스템까지 다루었다.

---

### 3. 기본 함수 작성법

#### ✅ 함수 선언과 호출

```swift
func greet(name: String) {
    print("안녕하세요, \(name)님!")
}

greet(name: "홍길동")
```

#### ✅ 매개변수가 있는 함수

```swift
func add(a: Int, b: Int) {
    print("\(a) + \(b) = \(a + b)")
}

add(a: 5, b: 3)
```

---

### 4. return문으로 값 반환하기

#### ✅ 기본적인 값 반환

```swift
func multiply(a: Int, b: Int) -> Int {
    return a * b
}

let result = multiply(a: 4, b: 5)
print(result) // 20
```

#### ✅ [추가 학습] return 키워드 생략

Swift는 **단일 표현식 함수**에서 `return` 키워드를 생략할 수 있다.

```swift
// return 키워드 사용
func square(number: Int) -> Int {
    return number * number
}

// return 키워드 생략 (단일 표현식)
func square(number: Int) -> Int {
    number * number
}
```

#### ✅ [추가 학습] 조건문에서의 return 생략

Swift는 정말 똑똑해서, 새로운 변수를 만들지 않고 값을 반환하려고 할 때는  
간단한 if문에서도 `return` 키워드를 생략할 수 있다.

```swift
func getStatus(isLoggedIn: Bool) -> String {
    if isLoggedIn {
        "로그인 완료"
    } else {
        "로그인 필요"
    }
}
```

---

### 5. 튜플로 여러 값 반환하기

#### ✅ 튜플 반환 기본

```swift
func getUserInfo() -> (name: String, age: Int, city: String) {
    return ("홍길동", 25, "서울")
}

let user = getUserInfo()
print("이름: \(user.name), 나이: \(user.age), 도시: \(user.city)")
```

#### ✅ 튜플 구조 분해

```swift
func getCoordinates() -> (x: Int, y: Int) {
    return (10, 20)
}

let (x, y) = getCoordinates()
print("x: \(x), y: \(y)")
```

---

### 6. Swift의 매개변수 라벨링 시스템

#### ✅ 외부 매개변수와 내부 매개변수

Swift는 **외부 매개변수(External Parameter)**와 **내부 매개변수(Internal Parameter)**를 구별한다.

```swift
func greet(to name: String) {
    print("안녕하세요, \(name)님!")
}

greet(to: "홍길동")
```

- `to`: 외부 매개변수 (함수 호출 시 사용)
- `name`: 내부 매개변수 (함수 내부에서 사용)

#### ✅ 외부 매개변수 생략 (\_ 사용)

```swift
func greet(_ name: String) {
    print("안녕하세요, \(name)님!")
}

greet("홍길동") // 매개변수 이름 없이 호출
```

#### ✅ 가변 매개변수 (Variadic Parameters)

```swift
func sum(_ numbers: Int...) -> Int {
    var total = 0
    for number in numbers {
        total += number
    }
    return total
}

let result = sum(1, 2, 3, 4, 5) // 15
```

---

### 7. [추가 학습] Swift vs Python 매개변수 비교

#### 🔹 Python의 키워드 인자

Python에서는 키워드 인자를 사용할 경우, 호출 시 순서를 바꿔도 괜찮다.

```python
def greet(name, age, city):
    print(f"이름: {name}, 나이: {age}, 도시: {city}")

# 순서를 바꿔도 정상 작동
greet(age=25, city="서울", name="홍길동")
```

#### 🔹 Swift의 엄격한 매개변수 순서

Swift는 **파라미터 이름과 순서가 모두 함수 호출의 일부분**으로 취급한다.

```swift
func greet(name: String, age: Int, city: String) {
    print("이름: \(name), 나이: \(age), 도시: \(city)")
}

// 순서를 바꾸면 컴파일 에러!
// greet(age: 25, city: "서울", name: "홍길동") // ❌ 에러
greet(name: "홍길동", age: 25, city: "서울") // ✅ 정상
```

#### 🔹 Swift의 설계 철학

Swift는 **사람이 읽기 쉬운 코드**와 **컴파일러가 확실히 체크하는 안정성**을 추구한다.

- 매개변수 순서가 고정되어 있어 **코드의 의도가 명확**해진다
- 컴파일 타임에 **잘못된 호출을 미리 방지**할 수 있다
- **코드 가독성**이 향상된다

---

### 8. [추가 학습] Array, Set, Dictionary, Tuple 비교

Swift에서 여러 값을 다룰 때 사용하는 **컬렉션 타입들**의 차이점과 언제 사용하면 좋을지 정리해보았다.

#### 🔹 Array (배열)

**특징:**

- **순서가 있는** 컬렉션
- **중복 허용**
- **인덱스로 접근** (0부터 시작)
- **동일한 타입**의 요소만 저장

**언제 사용할까?**

- 순서가 중요한 데이터 (예: 할 일 목록, 시간순 정렬된 데이터)
- 중복이 허용되어야 하는 경우
- 인덱스로 빠른 접근이 필요한 경우

```swift
// 할 일 목록 (순서 중요)
var todoList = ["운동하기", "공부하기", "운동하기"] // 중복 허용
print(todoList[0]) // "운동하기"

// 시간순 정렬된 데이터
let timeSlots = ["09:00", "10:00", "11:00", "12:00"]
```

#### 🔹 Set (집합)

**특징:**

- **순서가 없는** 컬렉션
- **중복 불허용**
- **빠른 검색** (해시 기반)
- **동일한 타입**의 요소만 저장

**언제 사용할까?**

- 중복을 제거해야 하는 경우
- 포함 여부를 빠르게 확인해야 하는 경우
- 순서가 중요하지 않은 고유한 값들의 집합

```swift
// 고유한 태그들 (순서 무관, 중복 불허)
var tags: Set<String> = ["Swift", "iOS", "SwiftUI", "Swift"] // 중복 제거됨
print(tags) // ["Swift", "iOS", "SwiftUI"]

// 빠른 포함 여부 확인
if tags.contains("Swift") {
    print("Swift 태그가 있습니다!")
}
```

#### 🔹 Dictionary (딕셔너리)

**특징:**

- **키-값 쌍**으로 구성
- **순서가 없는** 컬렉션 (Swift 5.0 이후로는 삽입 순서 유지)
- **키는 중복 불허용**, 값은 중복 허용
- **빠른 키 기반 검색**

**언제 사용할까?**

- 키를 통해 값을 빠르게 찾아야 하는 경우
- 연관된 데이터를 저장해야 하는 경우
- 설정값, 사용자 정보 등 구조화된 데이터

```swift
// 사용자 정보 (키-값 쌍)
var userInfo: [String: String] = [
    "name": "홍길동",
    "email": "hong@example.com",
    "city": "서울"
]

// 빠른 값 접근
if let name = userInfo["name"] {
    print("사용자 이름: \(name)")
}

// 설정값 저장
var settings: [String: Bool] = [
    "darkMode": true,
    "notifications": false,
    "autoSave": true
]
```

#### 🔹 Tuple (튜플)

**특징:**

- **고정된 개수**의 값들을 그룹화
- **다른 타입**의 값들을 함께 저장 가능
- **순서가 있는** 컬렉션
- **임시적인 데이터 그룹화**에 적합

**언제 사용할까?**

- 함수에서 여러 값을 반환할 때
- 임시적으로 관련된 데이터를 묶을 때
- 간단한 데이터 구조가 필요할 때

```swift
// 함수에서 여러 값 반환
func getUserInfo() -> (name: String, age: Int, isActive: Bool) {
    return ("홍길동", 25, true)
}

// 좌표 정보
let coordinates = (x: 10, y: 20)
print("x: \(coordinates.x), y: \(coordinates.y)")

// 임시 데이터 그룹화
let person = (name: "김철수", age: 30, city: "부산")
```

---

### 9. 컬렉션 타입 선택 가이드

| 상황                           | 추천 타입        | 이유                      |
| ------------------------------ | ---------------- | ------------------------- |
| 순서가 중요하고 중복 허용      | **Array**        | 인덱스 접근, 순서 보장    |
| 중복 제거가 필요하고 순서 무관 | **Set**          | 빠른 검색, 중복 자동 제거 |
| 키-값 쌍으로 데이터 저장       | **Dictionary**   | 빠른 키 기반 접근         |
| 함수에서 여러 값 반환          | **Tuple**        | 간단하고 효율적           |
| 복잡한 데이터 구조             | **Struct/Class** | 타입 안전성, 재사용성     |

#### 🔹 성능 비교

```swift
// Array: 인덱스 접근 O(1), 검색 O(n)
let array = [1, 2, 3, 4, 5]
let first = array[0] // 빠름

// Set: 검색 O(1), 순서 없음
let set: Set = [1, 2, 3, 4, 5]
let contains = set.contains(3) // 매우 빠름

// Dictionary: 키 기반 접근 O(1)
let dict = ["a": 1, "b": 2, "c": 3]
let value = dict["a"] // 빠름
```

---

### 10. 회고

오늘은 Swift의 함수 시스템을 깊이 있게 학습할 수 있었다.  
특히 **매개변수 라벨링 시스템**은 Swift만의 독특한 특징으로,  
처음에는 복잡해 보였지만 **코드의 명확성과 안전성을 위한 설계**라는 점에서 매우 합리적이라고 느꼈다.

Python과의 비교를 통해 Swift가 **왜 이렇게 엄격하게 설계되었는지** 이해할 수 있었고,  
`return` 키워드 생략 같은 **Swift의 스마트한 기능들**도 인상적이었다.

> 📌 **"Dennis Ritchie가 함수 호출이 정말, 정말 싸다고 말해서 모두가 작은 함수들을 만들고 모듈화하기 시작했다. 몇 년 후에 함수 호출이 여전히 비싸다는 것을 알게 되었고, 우리 코드의 50%가 단지 함수들을 호출하는 데 시간을 보내고 있었다. Dennis이 우리를 속였지만, 이미 늦었다. 우리는 모두 중독되어 있었다..."**

이 일화처럼 함수는 **코드 재사용성과 모듈화**의 핵심이지만,  
Swift는 이를 **안전하고 읽기 쉬운 방식**으로 구현했다는 점이 인상적이었다.

앞으로도 Swift의 **"왜 이렇게 설계되었는가?"**에 대한 고민을 계속하며 학습해나가야겠다.
