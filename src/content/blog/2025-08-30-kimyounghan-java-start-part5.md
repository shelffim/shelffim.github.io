---
title: "김영한의 자바 기초 강의 - part 5"
pubDate: 2025-08-30
description: "김영한님의 자바 기초 강의 part 5(조건문) 학습 정리"

> **출처**: [김영한의 자바 기초 강의](https://inf.run/PVx3u) - Section 5: 조건문

---

## 조건문 (Conditional Statements)

조건문은 **특정 조건에 따라 다른 코드를 실행**하는 구문입니다. 자바에서는 다양한 조건문을 제공하여 프로그램의 흐름을 제어할 수 있습니다.

### 조건문 종류

| 조건문 종류  | 설명             | 사용 시기                        |
| ------------ | ---------------- | -------------------------------- |
| `if`         | 단일 조건 검사   | 하나의 조건만 확인할 때          |
| `if-else`    | 조건에 따른 분기 | 두 가지 경우로 나눌 때           |
| `if-else-if` | 다중 조건 검사   | 여러 조건을 순차적으로 확인할 때 |
| `switch`     | 값에 따른 분기   | 특정 값에 따라 다른 동작을 할 때 |
| 삼항 연산자  | 간단한 조건 분기 | 한 줄로 간단한 조건 처리할 때    |

---

## 1. if문 (if Statement)

if문은 **특정 조건이 참인지 확인**하고, 조건이 참일 경우 특정 코드를 실행하는 구문입니다.

### 기본 if문

```java
int age = 20;

if (age >= 18) {
    System.out.println("성인입니다.");
}
```

### if문 관례

```java
// 권장: 중괄호 사용
if (age >= 18) {
    System.out.println("성인입니다.");
}

// 가능하지만 비권장: 중괄호 생략
if (age >= 18)
    System.out.println("성인입니다.");
```

### 핵심 포인트

- **중괄호 사용 권장** (가독성, 유지보수성 향상)
- 조건이 **참일 때만** 중괄호 안의 코드 실행
- 조건은 **boolean 타입**이어야 함

---

## 2. if-else문 (if-else Statement)

if-else문은 **조건이 참일 경우와 거짓일 경우**를 모두 처리하는 구문입니다.

### 기본 if-else문

```java
int age = 16;

if (age >= 18) {
    System.out.println("성인입니다.");
} else {
    System.out.println("미성년자입니다.");
}
```

### 핵심 포인트

- **두 가지 경우**로만 나눌 때 사용
- 조건이 **참이면 if 블록**, **거짓이면 else 블록** 실행
- **반드시 둘 중 하나**만 실행됨

---

## 3. if-else-if문 (if-else-if Statement)

if-else-if문은 **여러 개의 조건을 순차적으로 검사**하는 구문입니다.

### 기본 if-else-if문

```java
int score = 75;

if (score >= 90) {
    System.out.println("A등급");
} else if (score >= 80) {
    System.out.println("B등급");
} else if (score >= 70) {
    System.out.println("C등급");
} else {
    System.out.println("D등급");
}
```

### 효율성 비교

```java
// 비효율적: 모든 조건을 검사
if (score >= 90) {
    System.out.println("A등급");
}
if (score >= 80 && score < 90) {
    System.out.println("B등급");
}
if (score >= 70 && score < 80) {
    System.out.println("C등급");
}

// 효율적: 첫 번째로 만족하는 조건에서 중단
if (score >= 90) {
    System.out.println("A등급");
} else if (score >= 80) {
    System.out.println("B등급");
} else if (score >= 70) {
    System.out.println("C등급");
}
```

### 핵심 포인트

- **첫 번째로 참인 조건**에서 실행 후 **나머지 조건은 검사하지 않음**
- **불필요한 조건 검사를 피해** 성능 향상
- **순서가 중요**함 (위에서부터 차례대로 검사)

---

## 4. switch문 (switch Statement)

switch문은 **특정 변수의 값에 따라 분기 처리**하는 구문입니다.

### 기본 switch문

```java
int day = 3;

switch (day) {
    case 1:
        System.out.println("월요일");
        break;
    case 2:
        System.out.println("화요일");
        break;
    case 3:
        System.out.println("수요일");
        break;
    default:
        System.out.println("기타");
        break;
}
```

### break문의 중요성

```java
int day = 1;

switch (day) {
    case 1:
        System.out.println("월요일");
        // break가 없으면 다음 case도 실행됨!
    case 2:
        System.out.println("화요일");
        break;
    case 3:
        System.out.println("수요일");
        break;
}
// 출력: 월요일, 화요일 (둘 다 출력됨)
```

### switch문 특징

```java
String grade = "B";

switch (grade) {
    case "A":
        System.out.println("우수");
        break;
    case "B":
        System.out.println("양호");
        break;
    case "C":
        System.out.println("보통");
        break;
    // default는 생략 가능
}
```

### 핵심 포인트

- **단순히 값이 같은지만** 비교
- **break문이 없으면** 일치하는 case 이후의 모든 case 실행
- **default문은 생략 가능**
- **정수, 문자, 문자열, 열거형** 등에 사용 가능

---

## 5. 새로운 switch문 형식 (Enhanced Switch)

Java 14부터 도입된 **새로운 switch문 형식**은 코드를 더 간결하고 가독성 있게 만들어줍니다.

### 새로운 switch문 문법

```java
int day = 3;

String dayName = switch (day) {
    case 1 -> "월요일";
    case 2 -> "화요일";
    case 3 -> "수요일";
    case 4 -> "목요일";
    case 5 -> "금요일";
    default -> "주말";
};

System.out.println(dayName); // "수요일"
```

### 여러 줄 처리

```java
int score = 85;

String grade = switch (score / 10) {
    case 10, 9 -> "A등급";
    case 8 -> "B등급";
    case 7 -> "C등급";
    case 6 -> "D등급";
    default -> {
        System.out.println("점수를 다시 확인해주세요.");
        yield "F등급";
    }
};
```

### 새로운 switch문의 장점

- **break문 불필요** (자동으로 break 적용)
- **값을 반환**할 수 있음
- **여러 case를 한 줄에** 처리 가능 (`case 10, 9 ->`)
- **코드가 더 간결**하고 가독성 향상

---

## 6. 삼항 연산자 (Ternary Operator)

삼항 연산자는 **간단한 조건 분기**를 한 줄로 처리할 수 있는 연산자입니다.

### 기본 삼항 연산자

```java
int age = 20;
String status = (age >= 18) ? "성인" : "미성년자";
System.out.println(status); // "성인"
```

### 중첩 삼항 연산자

```java
int score = 75;
String grade = (score >= 90) ? "A" :
               (score >= 80) ? "B" :
               (score >= 70) ? "C" : "D";
```

### 핵심 포인트

- **조건 ? 참일때값 : 거짓일때값** 형태
- **간단한 조건 분기**에만 사용 권장
- **중첩 사용 시 가독성 저하** 주의

---

## Swift와의 차이점

### switch문 비교

| 특징                  | Java      | Swift            |
| --------------------- | --------- | ---------------- |
| **default 필수 여부** | 선택사항  | **필수**         |
| **break 필요 여부**   | 필요      | **불필요**       |
| **fallthrough**       | 기본 동작 | 명시적 작성 필요 |
| **모든 case 커버**    | 선택적    | **필수**         |

### 1. fallthrough 동작 방식

#### Java의 fallthrough (기본 동작)

```java
int day = 1;

switch (day) {
    case 1:
        System.out.println("월요일");
        // break가 없으면 자동으로 다음 case도 실행됨 (fallthrough)
    case 2:
        System.out.println("화요일");
        // break가 없으면 자동으로 다음 case도 실행됨
    case 3:
        System.out.println("수요일");
        break; // 여기서 멈춤
}
// 출력: 월요일, 화요일, 수요일
```

#### Swift의 fallthrough (명시적 작성 필요)

```swift
let day = 1

switch day {
case 1:
    print("월요일")
    // Swift는 자동으로 break됨 (fallthrough 안됨)
case 2:
    print("화요일")
case 3:
    print("수요일")
default:
    print("기타")
}
// 출력: 월요일 (하나만 출력)

// Swift에서 fallthrough를 원한다면 명시적으로 작성
switch day {
case 1:
    print("월요일")
    fallthrough  // 명시적으로 fallthrough 작성해야 함
case 2:
    print("화요일")
    fallthrough
case 3:
    print("수요일")
default:
    print("기타")
}
// 출력: 월요일, 화요일, 수요일
```

### 2. 모든 케이스 커버 (Exhaustive Matching)

#### Java (선택적)

```java
// Java에서는 모든 케이스를 처리하지 않아도 됨
String grade = "B";

switch (grade) {
    case "A":
        System.out.println("우수");
        break;
    case "B":
        System.out.println("양호");
        break;
    // "C", "D", "F" 케이스가 없어도 컴파일 오류 없음
    // default도 생략 가능
}
```

#### Swift (필수)

```swift
// Swift에서는 모든 케이스를 처리해야 함
let grade = "B"

switch grade {
case "A":
    print("우수")
case "B":
    print("양호")
// "C", "D", "F" 케이스가 없으면 컴파일 오류!
// 모든 가능한 값을 처리하거나 default가 반드시 필요
default:  // 필수!
    print("기타")
}
```

### 3. Java의 새로운 switch문

```java
// Java 14+ 새로운 switch문
String result = switch (value) {
    case 1 -> "하나";
    case 2 -> "둘";
    default -> "기타";
};
```

```swift
// Swift switch문
let result = switch value {
case 1: "하나"
case 2: "둘"
default: "기타"  // Swift에서는 default가 필수!
}
```

### 주요 차이점

1. **Swift의 switch문**은 **모든 가능한 값을 반드시 처리**해야 함
2. **Java의 switch문**은 **default가 선택사항**이지만, Swift는 **필수**
3. **Java의 새로운 switch문**은 Swift와 유사한 문법을 제공
4. **Swift는 더 엄격한 타입 안전성**을 제공
5. **Java의 fallthrough**는 기본 동작, **Swift의 fallthrough**는 명시적 작성 필요

---

## 느낀 점

조건문을 학습하면서 Swift와 Java의 차이점이 흥미로웠다. 특히 Swift에서는 switch문의 default가 필수이고 모든 case를 커버해야 하는 반면, Java에서는 선택사항이라는 점이 인상적이었다.

Java의 새로운 switch문 형식은 Swift와 매우 유사해서, 언어 간의 문법이 점점 수렴해가는 것 같다는 생각이 들었다. 삼항 연산자는 간단한 조건 분기에 매우 유용하지만, 중첩 사용 시 가독성이 떨어질 수 있어서 적절히 사용해야겠다.

if-else-if문의 효율성 부분도 새로웠는데, 첫 번째로 만족하는 조건에서 중단되기 때문에 조건의 순서가 중요하다는 점을 배웠다. 앞으로 조건문을 작성할 때 이런 부분들을 고려해서 더 효율적인 코드를 작성해보고 싶다.

### 언어 철학의 차이

조건문을 통해 Java와 Swift의 언어 철학 차이를 명확히 알게 되었다. **Java는 단순성과 생산성 향상**을 추구하는 반면, **Swift는 안전성을 추구**한다는 것을 확인할 수 있었다.

- **Java의 철학**: 개발자가 원하는 만큼만 처리하고, 빠른 개발을 위해 유연성을 제공
- **Swift의 철학**: 모든 경우를 명시적으로 처리하여 런타임 오류를 방지하고 안전성을 보장

이런 개발 언어들이 추구하는 바를 알게 되면서, 각 언어의 설계 철학이 개발자의 코딩 스타일과 프로젝트의 특성에 따라 어떻게 영향을 미치는지 이해할 수 있었다. Java는 "빠르고 간단하게" 개발할 수 있게 도와주고, Swift는 "안전하고 견고하게" 개발할 수 있게 도와준다는 차이점이 인상적이었다. 앞으로 다른 언어를 학습할 때도 이런 철학적 차이점을 고려해보고 싶다.
