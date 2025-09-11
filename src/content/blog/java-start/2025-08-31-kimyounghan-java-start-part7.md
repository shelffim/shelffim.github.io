---
title: "김영한의 자바 기초 강의 - part 7"
pubDate: 2025-08-30
description: "김영한님의 자바 기초 강의 part 7(스코프와 형변환) 학습 정리"
---

> **출처**: [김영한의 자바 기초 강의](https://inf.run/PVx3u) - Section 7: 스코프와 형변환

## 스코프와 형변환 (Scope and Type Casting)

스코프와 형변환은 변수의 접근 범위를 제어하고, 다양한 데이터 타입 간의 변환을 통해 유연한 프로그래밍을 지원합니다.

### 주요 개념

| 개념              | 설명                                | 중요도           |
| ----------------- | ----------------------------------- | ---------------- |
| **스코프**        | 변수의 접근 가능한 범위             | 메모리 효율성    |
| **지역 변수**     | 코드 블록 내에서만 접근 가능한 변수 | 변수 관리        |
| **자동 형변환**   | 작은 타입에서 큰 타입으로 자동 변환 | 타입 안전성      |
| **명시적 형변환** | 개발자가 직접 타입 변환 지정        | 데이터 손실 주의 |

---

## 1. 스코프 (Scope)

### 스코프란?

**스코프**는 변수의 접근 가능한 범위를 의미합니다. 변수는 선언된 위치에 따라 접근할 수 있는 범위가 결정됩니다.

### 스코프가 존재하는 이유

- **메모리 효율성**: 변수가 필요한 범위에서만 메모리를 사용
- **코드 복잡성 감소**: 변수명 충돌 방지 및 코드 가독성 향상
- **안전성**: 의도하지 않은 변수 접근 방지

### 지역 변수 (Local Variable)

지역 변수는 코드 블록 `{}` 내에서 선언된 변수로, 다음과 같은 특징을 가집니다:

```java
{
    int x = 10;  // 지역 변수 선언
    System.out.println("블록 내부: " + x);  // 접근 가능
}
// System.out.println("블록 외부: " + x);  // 컴파일 오류!
```

**출력 결과:**

```
블록 내부: 10
```

### 지역 변수의 특징

```java
public class ScopeExample {
    public static void main(String[] args) {
        int outer = 100;

        {
            int inner = 50;
            System.out.println("외부 변수: " + outer);  // 접근 가능
            System.out.println("내부 변수: " + inner);  // 접근 가능
        }

        System.out.println("외부 변수: " + outer);  // 접근 가능
        // System.out.println("내부 변수: " + inner);  // 컴파일 오류!
    }
}
```

### 핵심 포인트

- **해당 코드 블록이 끝나면 변수 소멸**
- **코드 블록 내에서만 접근 가능**
- **메모리 효율적 사용**
- **변수명 충돌 방지**

> **좋은 프로그래밍 습관**: 변수는 꼭 필요한 범위로 한정해서 사용하는 것이 좋습니다. 좋은 프로그램은 적절한 제약이 있는 프로그램입니다.

---

## 2. 형변환 (Type Casting)

### 형변환이란?

**형변환**은 변수의 타입을 다른 타입으로 변경하는 것을 의미합니다. 자바에서는 데이터 타입 간의 변환을 통해 다양한 연산을 수행할 수 있습니다.

### 형변환의 기본 원칙

- **작은 범위 → 큰 범위**: 자동으로 허용 (자동 형변환)
- **큰 범위 → 작은 범위**: 명시적 형변환 필요 (데이터 손실 위험)

### 자동 형변환 (Implicit Casting)

작은 범위 타입에서 큰 범위 타입으로 대입할 때 자동으로 형변환이 이루어집니다.

```java
int intValue = 100;
long longValue = intValue;  // int → long 자동 형변환
double doubleValue = intValue;  // int → double 자동 형변환

System.out.println("int: " + intValue);      // 100
System.out.println("long: " + longValue);    // 100
System.out.println("double: " + doubleValue); // 100.0
```

### 명시적 형변환 (Explicit Casting)

큰 범위 타입에서 작은 범위 타입으로 대입할 때는 괄호를 사용하여 명시적으로 형변환을 해야 합니다.

```java
double doubleValue = 3.14;
int intValue = (int) doubleValue;  // double → int 명시적 형변환

System.out.println("double: " + doubleValue);  // 3.14
System.out.println("int: " + intValue);        // 3 (소수점 버림)
```

### 형변환 주의사항

```java
// 오버플로우 예시
int maxInt = Integer.MAX_VALUE;  // 2147483647
long longValue = maxInt + 1L;    // 2147483648
int backToInt = (int) longValue; // -2147483648 (오버플로우!)

System.out.println("원본 int: " + maxInt);
System.out.println("long 변환: " + longValue);
System.out.println("다시 int: " + backToInt);
```

**출력 결과:**

```
원본 int: 2147483647
long 변환: 2147483648
다시 int: -2147483648
```

### 핵심 포인트

- **자동 형변환**: 작은 타입 → 큰 타입 (안전)
- **명시적 형변환**: 큰 타입 → 작은 타입 (위험)
- **데이터 손실 주의**: 소수점 버림, 오버플로우
- **값이 변하는 것이 아니라 표현 방식이 변경**

---

## Swift와의 차이점

### 스코프 비교

| 특징            | Java                | Swift        |
| --------------- | ------------------- | ------------ |
| **스코프 규칙** | 코드 블록 `{}` 기반 | 동일         |
| **변수 선언**   | `int x = 10;`       | `var x = 10` |
| **접근 범위**   | 블록 내에서만       | 동일         |

### 형변환 비교

| 특징              | Java                | Swift                |
| ----------------- | ------------------- | -------------------- |
| **자동 형변환**   | 작은 타입 → 큰 타입 | **제한적**           |
| **명시적 형변환** | `(int) value`       | `Int(value)`         |
| **타입 안전성**   | 런타임 검사         | **컴파일 타임 검사** |

### 문자열 연결 비교

| 특징            | Java                       | Swift                 |
| --------------- | -------------------------- | --------------------- |
| **자동 형변환** | `"Hello" + 2` → `"Hello2"` | ❌ 컴파일 오류        |
| **문자열 보간** | `"Hello" + 2`              | `"Hello\(2)"`         |
| **명시적 변환** | 자동 처리                  | `"Hello" + String(2)` |
| **타입 안전성** | 런타임 처리                | **컴파일 타임 검사**  |

### Java vs Swift 문법 비교

```java
// Java 형변환
int intValue = 100;
long longValue = intValue;  // 자동 형변환
double doubleValue = (double) intValue;  // 명시적 형변환

// Java 문자열 연결 (자동 형변환)
String result1 = "Hello" + 2;        // "Hello2"
String result2 = "Hello" + 2.5;      // "Hello2.5"
String result3 = "Hello" + true;     // "Hellotrue"

// Java 스코프
{
    int localVar = 50;
    System.out.println(localVar);
}
```

```swift
// Swift 형변환
let intValue = 100
let longValue = Int(intValue)  // 명시적 형변환 필요
let doubleValue = Double(intValue)  // 명시적 형변환 필요

// Swift 문자열 연결 (문자열 보간 사용)
let result1 = "Hello\(2)"        // "Hello2"
let result2 = "Hello\(2.5)"      // "Hello2.5"
let result3 = "Hello\(true)"     // "Hellotrue"

// Swift 명시적 형변환
let result4 = "Hello" + String(2)  // "Hello2"

// Swift 스코프
{
    let localVar = 50
    print(localVar)
}
```

### 주요 차이점

1. **Java의 자동 형변환**은 더 관대함 (작은 타입 → 큰 타입)
2. **Swift의 형변환**은 더 엄격함 (대부분 명시적 변환 필요)
3. **Java는 런타임에 타입 검사**, **Swift는 컴파일 타임에 타입 검사**
4. **Java의 문자열 연결**은 자동 형변환 지원 (`"Hello" + 2`)
5. **Swift의 문자열 연결**은 문자열 보간 사용 (`"Hello\(2)"`)
6. **스코프 규칙은 두 언어 모두 유사**

---

## 느낀 점

스코프와 형변환을 학습하면서 Java의 타입 시스템이 Swift보다 더 유연하다는 것을 알게 되었다. 특히 Java의 자동 형변환은 개발 편의성을 높여주지만, 반대로 예상치 못한 타입 변환이 일어날 수 있는 위험도 있다.

Swift는 타입 안전성을 중시하여 대부분의 형변환을 명시적으로 요구하는 반면, Java는 개발자의 편의성을 고려하여 자동 형변환을 제공한다는 차이점이 인상적이었다.

스코프의 경우 두 언어 모두 비슷한 규칙을 가지고 있어서 이해하기 쉬웠다. 변수를 필요한 범위에서만 사용하는 것이 메모리 효율성과 코드 가독성에 도움이 된다는 점을 다시 한번 깨달았다.

앞으로 형변환을 사용할 때는 데이터 손실 가능성을 항상 고려하고, 명시적 형변환이 필요한 경우 주의깊게 사용해야겠다.
