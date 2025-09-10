---
title: "김영한의 자바 기초 강의 - part 6"
pubDate: 2025-08-30
---

## 반복문 (Loop Statements)

반복문은 **특정 코드를 반복해서 실행**할 때 사용하는 구문입니다.

### 반복문 종류

| 반복문 종류 | 설명                           | 사용 시기                   |
| ----------- | ------------------------------ | --------------------------- |
| `while`     | 조건이 참인 동안 반복          | 반복 횟수가 불확실할 때     |
| `do-while`  | 최소 한 번은 실행 후 조건 검사 | 최소 한 번은 실행해야 할 때 |
| `for`       | 반복 횟수가 정해져 있을 때     | 반복 횟수가 명확할 때       |

### 반복문 흐름 제어

| 문법       | 설명               | 사용 시기                           |
| ---------- | ------------------ | ----------------------------------- |
| `break`    | 반복문 즉시 종료   | 특정 조건에서 반복 중단             |
| `continue` | 현재 반복 건너뛰기 | 특정 조건에서 현재 반복만 건너뛸 때 |

---

## 1. while문 (while Statement)

while문은 **조건이 참인 동안 계속 반복**하는 구문입니다.

### 기본 while문

```java
int number = 1;
int sum = 0;

while (number <= 10) {
    sum += number;
    number++;
}
System.out.println("1부터 10까지의 합: " + sum); // 55
```

### 무한 루프 주의사항

```java
// 위험: 무한 루프 (조건이 항상 참)
int i = 0;
while (i < 5) {
    System.out.println("무한 루프!");
    // i++가 없어서 i는 항상 0
}
```

### 핵심 포인트

- **조건이 참일 때만** 반복 실행
- **조건이 거짓이 되면** while문 종료
- **무한 루프 주의** (조건이 항상 참이 되지 않도록)

---

## 2. do-while문 (do-while Statement)

do-while문은 **최소 한 번은 실행**한 후 조건을 검사하는 구문입니다.

### 기본 do-while문

```java
int count = 0;

do {
    System.out.println("현재 카운트: " + count);
    count++;
} while (count < 3);
```

**출력 결과:**

```
현재 카운트: 0
현재 카운트: 1
현재 카운트: 2
```

### while문과의 차이점

```java
int count = 5;

// while문: 조건이 거짓이므로 실행되지 않음
while (count < 3) {
    System.out.println("while문 실행");
    count++;
}
// 출력: 없음

// do-while문: 최소 한 번은 실행됨
do {
    System.out.println("do-while문 실행");
    count++;
} while (count < 3);
// 출력: do-while문 실행
```

### 핵심 포인트

- **최소 한 번은 반드시 실행**
- **실행 후에 조건 검사**
- **사용자 입력 검증** 등에 유용

---

## 3. for문 (for Statement)

for문은 **반복 횟수가 정해져 있을 때** 사용하는 구문입니다.

### 기본 for문

```java
for (int i = 0; i < 5; i++) {
    System.out.println("현재 i: " + i);
}
```

**출력 결과:**

```
현재 i: 0
현재 i: 1
현재 i: 2
현재 i: 3
현재 i: 4
```

### for문 구조 분석

```java
for (초기식; 조건식; 증감식) {
    // 반복할 코드
}
```

- **초기식**: 반복 변수 선언 및 초기화 (1번만 실행)
- **조건식**: 반복 조건 검사 (매번 실행)
- **증감식**: 반복 변수 증가/감소 (반복 후 실행)

### 초기식에 여러 변수 선언

```java
// 같은 타입의 변수들을 쉼표로 구분
for (int i = 0, j = 10; i < 5 && j > 5; i++, j--) {
    System.out.println("i: " + i + ", j: " + j);
}

// 다른 타입의 변수들도 선언 가능
for (int i = 0, double d = 1.5; i < 3; i++, d += 0.5) {
    System.out.println("i: " + i + ", d: " + d);
}
```

### 핵심 포인트

- **반복 횟수가 명확**할 때 사용
- **초기식, 조건식, 증감식**이 모두 포함
- **초기식에 여러 변수 선언** 가능 (다양한 타입, 쉼표로 구분)
- **배열 순회** 등에 자주 사용

---

## 4. break문 (break Statement)

break문은 **반복문을 즉시 종료**하는 구문입니다.

### 기본 break문

```java
for (int i = 1; i <= 10; i++) {
    if (i == 5) {
        break; // i가 5가 되면 반복문 종료
    }
    System.out.println("현재 i: " + i);
}
```

**출력 결과:**

```
현재 i: 1
현재 i: 2
현재 i: 3
현재 i: 4
```

### while문에서의 break

```java
int number = 1;
while (true) { // 무한 루프
    if (number > 5) {
        break; // 조건 만족 시 루프 종료
    }
    System.out.println("숫자: " + number);
    number++;
}
```

### 핵심 포인트

- **반복문을 즉시 종료**
- **조건부 종료**에 유용
- **성능 최적화**에 도움

---

## 5. continue문 (continue Statement)

continue문은 **현재 반복을 건너뛰고 다음 반복**으로 넘어가는 구문입니다.

### 기본 continue문

```java
for (int i = 1; i <= 5; i++) {
    if (i == 3) {
        continue; // i가 3일 때 건너뛰기
    }
    System.out.println("현재 i: " + i);
}
```

**출력 결과:**

```
현재 i: 1
현재 i: 2
현재 i: 4
현재 i: 5
```

### while문에서의 continue

```java
int i = 0;
while (i < 5) {
    i++;
    if (i == 3) {
        continue; // 3일 때 건너뛰기
    }
    System.out.println("현재 i: " + i);
}
```

### 핵심 포인트

- **현재 반복만 건너뛰기**
- **특정 조건 제외** 처리에 유용
- **반복문은 계속 실행**

---

## 6. 중첩 반복문 (Nested Loops)

중첩 반복문은 **반복문 안에 또 다른 반복문**을 사용하는 구문입니다.

### 기본 중첩 for문

```java
for (int i = 1; i <= 3; i++) {
    for (int j = 1; j <= 3; j++) {
        System.out.println("i: " + i + ", j: " + j);
    }
}
```

**출력 결과:**

```
i: 1, j: 1
i: 1, j: 2
i: 1, j: 3
i: 2, j: 1
i: 2, j: 2
i: 2, j: 3
i: 3, j: 1
i: 3, j: 2
i: 3, j: 3
```

### 중첩 반복문에서의 break와 continue

```java
for (int i = 1; i <= 3; i++) {
    for (int j = 1; j <= 3; j++) {
        if (j == 2) {
            break; // 안쪽 반복문만 종료됨
        }
        System.out.println("i: " + i + ", j: " + j);
    }
}
```

**출력 결과:**

```
i: 1, j: 1
i: 2, j: 1
i: 3, j: 1
```

### break와 continue의 범위

```java
// break: 안쪽 반복문만 종료
for (int i = 1; i <= 2; i++) {
    for (int j = 1; j <= 3; j++) {
        if (j == 2) {
            break; // j 반복문만 종료, i 반복문은 계속
        }
        System.out.println("i: " + i + ", j: " + j);
    }
}

// continue: 안쪽 반복문의 현재 반복만 건너뛰기
for (int i = 1; i <= 2; i++) {
    for (int j = 1; j <= 3; j++) {
        if (j == 2) {
            continue; // j=2일 때만 건너뛰기
        }
        System.out.println("i: " + i + ", j: " + j);
    }
}
```

### 핵심 포인트

- **반복문 안에 반복문** 사용
- **2차원 배열 처리** 등에 유용
- **성능 고려** 필요 (복잡도 증가)
- **break/continue는 가장 가까운 반복문**에만 적용

---

## Swift와의 차이점

### 반복문 비교

| 특징               | Java                           | Swift            |
| ------------------ | ------------------------------ | ---------------- |
| **for문 문법**     | `for (초기식; 조건식; 증감식)` | `for i in 1...5` |
| **while문**        | 동일                           | 동일             |
| **do-while**       | `do-while`                     | `repeat-while`   |
| **break/continue** | 동일                           | 동일             |

### Java vs Swift 문법 비교

```java
// Java for문 - 여러 변수 선언 가능
for (int i = 1, j = 10; i <= 5 && j >= 6; i++, j--) {
    System.out.println("i: " + i + ", j: " + j);
}

// Java while문
int i = 1;
while (i <= 5) {
    System.out.println("숫자: " + i);
    i++;
}
```

```swift
// Swift for문 - 범위 기반, 여러 변수 선언 불가
for i in 1...5 {
    print("숫자: \(i)")
}

// Swift while문
var i = 1
while i <= 5 {
    print("숫자: \(i)")
    i += 1
}
```

### 주요 차이점

1. **Java의 for문**은 **C 스타일** (초기식, 조건식, 증감식)
2. **Swift의 for문**은 **범위 기반** (`for i in 1...5`)
3. **Java는 초기식에 다양한 타입 변수 선언 가능**, **Swift는 불가능**
4. **Java의 do-while** vs **Swift의 repeat-while**
5. **기본 동작은 유사**하지만 **문법이 다름**

---

## 느낀 점

반복문을 학습하면서 Java의 for문과 Swift의 for문의 차이가 인상적이었다. Java의 `for (int i = 0; i < 5; i++)` 문법은 더 명시적이고 제어하기 쉽지만, Swift의 `for i in 1...5` 문법은 더 직관적이고 읽기 쉽다.
