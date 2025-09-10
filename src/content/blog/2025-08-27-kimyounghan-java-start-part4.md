---
title: "김영한의 자바 기초 강의 - part 4"
pubDate: 2025-08-27
description: "김영한님의 자바 기초 강의 part 4(연산자) 학습 정리"

> **출처**: [김영한의 자바 기초 강의](https://inf.run/PVx3u) - Section 4: 연산자

---

## 연산자 (Operators)

연산자는 **계산을 수행하는 기호**입니다. 자바에서는 다양한 종류의 연산자를 제공합니다.

### 연산자 종류

| 연산자 종류 | 기호 예시              | 설명         |
| ----------- | ---------------------- | ------------ |
| 산술 연산자 | `+, -, *, /, %`        | 숫자 계산    |
| 대입 연산자 | `=`                    | 값 저장      |
| 비교 연산자 | `==, !=, >, <, >=, <=` | 값 비교      |
| 논리 연산자 | `&&, \|\|, !`          | 논리 연산    |
| 증감 연산자 | `++, --`               | 값 증가/감소 |
| 삼항 연산자 | `? :`                  | 조건부 연산  |

---

## 1. 산술 연산자 (Arithmetic Operators)

산술 연산자는 **숫자 데이터를 계산하는 데 사용**됩니다.

### 기본 산술 연산자

```java
int a = 10;
int b = 3;

System.out.println(a + b);  // 13 (덧셈)
System.out.println(a - b);  // 7  (뺄셈)
System.out.println(a * b);  // 30 (곱셈)
System.out.println(a / b);  // 3  (나눗셈)
System.out.println(a % b);  // 1  (나머지)
```

### 핵심 포인트

- **두 개의 피연산자**를 필요로 함
- **같은 타입끼리 계산**하면 결과도 같은 타입 (`int + int = int`)
- **정수 / 정수 = 정수** (소수점 버림)
  ```java
  int result = 10 / 3;  // 결과: 3 (3.333...이 아님)
  ```

---

## 2. 문자열 더하기 (String Concatenation)

자바는 문자열에 `+` 연산자를 사용하면 **문자열을 연결**합니다.

### 문자열 연결 예시

```java
String result1 = "Hello" + "World";  // "HelloWorld"
String result2 = "Hello" + 10;       // "Hello10"
String result3 = 10 + "Hello";       // "10Hello"
```

### 핵심 포인트

- **문자열 + 문자열**: 두 문자열을 연결
- **문자열 + 숫자**: 숫자를 문자열로 변환 후 연결
- **숫자 + 문자열**: 숫자를 문자열로 변환 후 연결

---

## 3. 연산자 우선순위 (Operator Precedence)

연산자 우선순위는 **상식선에서 사용**됩니다.

### 우선순위 예시

```java
int result1 = 2 + 3 * 4;    // 14 (곱셈이 먼저)
int result2 = (2 + 3) * 4;  // 20 (괄호가 먼저)
```

### 핵심 포인트

- **곱셈, 나눗셈**이 **덧셈, 뺄셈**보다 우선
- **괄호**를 사용하면 우선순위 변경 가능
- **애매하면 괄호 사용** 권장

---

## 4. 증감 연산자 (Increment/Decrement Operators)

증감 연산자는 **값을 1씩 증가 또는 감소**시키는 연산자입니다.

### 전위/후위 증감 연산자

```java
int a = 5;

// 전위 증감 (++a, --a)
System.out.println(++a);  // 6 (증가 후 사용)
System.out.println(a);    // 6

int b = 5;
System.out.println(--b);  // 4 (감소 후 사용)
System.out.println(b);    // 4

// 후위 증감 (a++, a--)
int c = 5;
System.out.println(c++);  // 5 (사용 후 증가)
System.out.println(c);    // 6

int d = 5;
System.out.println(d--);  // 5 (사용 후 감소)
System.out.println(d);    // 4
```

### 핵심 포인트

- **`++a`**: a를 1 증가시킨 **후** 사용
- **`a++`**: a를 사용한 **후** 1 증가
- **`--a`**: a를 1 감소시킨 **후** 사용
- **`a--`**: a를 사용한 **후** 1 감소

---

## 5. 비교 연산자 (Comparison Operators)

비교 연산자는 **두 개의 피연산자를 비교**하는 데 사용됩니다.

### 비교 연산자 예시

```java
int a = 10;
int b = 5;

System.out.println(a == b);  // false (같음)
System.out.println(a != b);  // true  (다름)
System.out.println(a > b);   // true  (큼)
System.out.println(a < b);   // false (작음)
System.out.println(a >= b);  // true  (크거나 같음)
System.out.println(a <= b);  // false (작거나 같음)
```

### 문자열 비교

```java
String str1 = "Hello";
String str2 = "Hello";
String str3 = new String("Hello");

System.out.println(str1 == str2);        // true (리터럴 비교)
System.out.println(str1 == str3);        // false (객체 비교)
System.out.println(str1.equals(str3));   // true (내용 비교)
```

### 핵심 포인트

- 비교 결과는 **`true` 또는 `false`** 반환
- **문자열 비교**는 `==`이 아니라 **`.equals()`** 사용
- `==`는 객체 참조 비교, `.equals()`는 내용 비교

---

## 6. 논리 연산자 (Logical Operators)

논리 연산자는 **`true`, `false`를 비교**하는 데 사용됩니다.

### 논리 연산자 예시

```java
boolean a = true;
boolean b = false;

System.out.println(a && b);  // false (AND: 둘 다 참이어야 참)
System.out.println(a || b);  // true  (OR: 하나라도 참이면 참)
System.out.println(!a);      // false (NOT: 참이면 거짓, 거짓이면 참)
```

### 실제 사용 예시

```java
int age = 20;
boolean hasLicense = true;

// AND 연산자: 두 조건 모두 만족
if (age >= 18 && hasLicense) {
    System.out.println("운전 가능");
}

// OR 연산자: 하나라도 만족
if (age < 18 || !hasLicense) {
    System.out.println("운전 불가");
}
```

### 핵심 포인트

- **`&&` (AND)**: 두 조건이 **모두 참**일 때 참
- **`||` (OR)**: 두 조건 중 **하나라도 참**일 때 참
- **`!` (NOT)**: 참이면 거짓, 거짓이면 참

---

## 7. 대입 연산자 (Assignment Operators)

대입 연산자는 **값을 변수에 저장**하는 데 사용됩니다.

### 대입 연산자 예시

```java
int a = 10;

a += 5;   // a = a + 5;  → 15
a -= 3;   // a = a - 3;  → 12
a *= 2;   // a = a * 2;  → 24
a /= 4;   // a = a / 4;  → 6
a %= 3;   // a = a % 3;  → 0
```

### 대입 연산자 종류

| 연산자 | 의미                | 예시                  |
| ------ | ------------------- | --------------------- |
| `=`    | 대입                | `a = 10`              |
| `+=`   | 더한 후 대입        | `a += 5` (a = a + 5)  |
| `-=`   | 뺀 후 대입          | `a -= 3` (a = a - 3)  |
| `*=`   | 곱한 후 대입        | `a *= 2` (a = a \* 2) |
| `/=`   | 나눈 후 대입        | `a /= 4` (a = a / 4)  |
| `%=`   | 나머지 구한 후 대입 | `a %= 3` (a = a % 3)  |

### 핵심 포인트

- **`=`**: 왼쪽 변수에 오른쪽 값 저장
- **복합 대입 연산자**: 연산과 대입을 동시에 수행
- 코드를 **간결하게** 작성할 수 있음

---

## 느낀 점

Swift와 비교했을 때, 자바의 연산자들은 대부분 비슷하지만 몇 가지 차이점이 있다. 특히 문자열 비교에서 `==` 대신 `.equals()`를 사용해야 한다는 점이 인상적이다.
