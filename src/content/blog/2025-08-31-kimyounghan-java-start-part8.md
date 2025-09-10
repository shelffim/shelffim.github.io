---
title: "김영한의 자바 기초 강의 - part 8"
pubDate: 2025-08-31
description: "김영한님의 자바 기초 강의 part 8(훈련) 학습 정리"
---

> **출처**: [김영한의 자바 기초 강의](https://inf.run/PVx3u) - Section 8: 훈련

## 입력과 출력 (Input and Output)

자바에서는 Scanner 클래스를 통해 사용자 입력을 받고, System.out을 통해 결과를 출력할 수 있습니다.

### 주요 개념

| 개념                     | 설명                      | 중요도          |
| ------------------------ | ------------------------- | --------------- |
| **Scanner**              | 사용자 입력을 받는 클래스 | 사용자 상호작용 |
| **System.out.println()** | 출력 후 줄바꿈            | 결과 표시       |
| **System.out.print()**   | 출력 후 같은 줄 유지      | 연속 출력       |

---

## 1. Scanner 클래스

### Scanner란?

**Scanner**는 사용자의 입력을 받아서 처리하는 클래스입니다. 다양한 타입의 데이터를 입력받을 수 있으며, 키보드, 파일, 문자열 등 다양한 소스에서 데이터를 읽을 수 있습니다.

### Scanner 기본 사용법

```java
import java.util.Scanner;

public class ScannerExample {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("이름을 입력하세요: ");
        String name = scanner.nextLine();  // 문자열 입력
        System.out.println("안녕하세요, " + name + "님!");

        System.out.print("나이를 입력하세요: ");
        int age = scanner.nextInt();  // 정수 입력
        System.out.println("나이: " + age + "세");

        System.out.print("키를 입력하세요: ");
        double height = scanner.nextDouble();  // 실수 입력
        System.out.println("키: " + height + "cm");
    }
}
```

### Scanner 메서드 종류

| 메서드         | 설명                       | 예시            |
| -------------- | -------------------------- | --------------- |
| `nextLine()`   | 한 줄 전체를 문자열로 입력 | `"Hello World"` |
| `nextInt()`    | 정수 입력                  | `42`            |
| `nextDouble()` | 실수 입력                  | `3.14`          |

### Scanner 사용 시 주의사항

```java
import java.util.Scanner;

public class ScannerCaution {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("나이를 입력하세요: ");
        int age = scanner.nextInt();  // 정수 입력 후 엔터키가 버퍼에 남음

        System.out.print("이름을 입력하세요: ");
        String name = scanner.nextLine();  // 빈 문자열이 입력될 수 있음!

        System.out.println("나이: " + age);
        System.out.println("이름: '" + name + "'");  // 빈 문자열 출력

    }
}
```

**해결 방법:**

```java
// nextInt() 후 nextLine() 사용 시
int age = scanner.nextInt();
scanner.nextLine();  // 버퍼의 엔터키 제거
String name = scanner.nextLine();  // 정상적으로 입력받음
```

### 핵심 포인트

- **import 문 필수**: `import java.util.Scanner;`
- **Scanner 생성**: `Scanner scanner = new Scanner(System.in);`
- **다양한 타입 지원**: 문자열, 정수, 실수, 불린 등
- **버퍼 관리 주의**: `nextInt()` 후 `nextLine()` 사용 시 주의

---

## 2. 출력 방식

### System.out.println() vs System.out.print()

자바에서는 두 가지 주요 출력 방식을 제공합니다.

### println() - 줄바꿈 출력

```java
System.out.println("첫 번째 줄");
System.out.println("두 번째 줄");
System.out.println("세 번째 줄");
```

**출력 결과:**

```
첫 번째 줄
두 번째 줄
세 번째 줄
```

### print() - 같은 줄 유지

```java
System.out.print("Hello");
System.out.print("World");
System.out.print("!");
```

**출력 결과:**

```
HelloWorld!
```

### 출력 방식 비교

| 메서드      | 설명                   | 줄바꿈 | 사용 예시                      |
| ----------- | ---------------------- | ------ | ------------------------------ |
| `println()` | 출력 후 다음 줄로 이동 | ✅     | `System.out.println("Hello");` |
| `print()`   | 출력 후 같은 줄 유지   | ❌     | `System.out.print("Hello");`   |

### 개행문자 (Escape Character)

자바에서 `\n`은 **개행문자(줄바꿈 문자)**로, 출력 시 다음 줄로 이동하는 역할을 합니다.

```java
System.out.print("첫 번째 줄\n");
System.out.print("두 번째 줄");
System.out.print("세 번째 줄");
```

**출력 결과:**

```
첫 번째 줄
두 번째 줄세 번째 줄
```

### 핵심 포인트

- **println()**: 출력 후 자동으로 줄바꿈 (`\n` 포함)
- **print()**: 출력 후 같은 줄에 유지
- **`\n`**: 개행문자로 수동 줄바꿈 가능
- **혼합 사용**: 상황에 맞게 적절히 선택

---

## Swift와의 차이점

| 특징          | Java                        | Swift                 |
| ------------- | --------------------------- | --------------------- |
| **입력**      | `Scanner` (타입별 메서드)   | `readLine()` (옵셔널) |
| **출력**      | `System.out.println()`      | `print()`             |
| **import**    | `import java.util.Scanner;` | 불필요                |
| **타입 변환** | 자동                        | 수동 변환 + 언패킹    |

### 주요 차이점

1. **Java의 Scanner**는 `nextInt()`, `nextDouble()` 등 다양한 타입을 직접 입력받을 수 있음
2. **Swift의 readLine()**은 옵셔널을 반환하므로 `??` 또는 `!`로 언패킹 필요
3. **Java는 import 필요**, **Swift는 기본 제공**
4. **Java의 출력**은 `System.out` 사용, **Swift는 `print()` 사용**
5. **Java**: `System.out.println()`과 `print()`, **Swift**: `print()`만 사용

---

## 느낀 점

Scanner 클래스를 학습하면서 Java의 사용자 입력 처리 방식이 Swift보다 더 편리하다는 것을 알게 되었다. 특히 Java는 `nextInt()`, `nextDouble()` 같은 타입별 메서드를 제공하여 직접 해당 타입으로 입력받을 수 있지만, Swift는 `readLine()`으로 문자열만 받고 언패킹과 수동으로 타입 변환을 해야 한다는 차이점이 인상적이었다.

이런 차이점의 근본적인 이유는 **두 언어의 주요 용도가 다르기 때문**이다. **Java는 서버, 데스크톱, 웹 개발** 등에서 콘솔로 입력을 받는 경우가 많아서 편리한 입출력 기능을 제공하는 반면, **Swift는 모바일 앱 개발**을 중점적으로 설계되어 **UI 컴포넌트 중심**으로 입력을 받기 때문이다.

출력 방식에서도 Java의 `println()`과 `print()`의 구분이 명확해서 언제 줄바꿈이 필요한지 쉽게 제어할 수 있다는 점이 좋았다. Swift의 `print()`는 기본적으로 줄바꿈이 포함되어 있어서 Java의 `println()`과 유사하다.

다만 Java에서 `nextInt()` 후 `nextLine()`을 사용할 때 버퍼에 남은 엔터키 때문에 빈 문자열이 입력되는 문제는 처음에는 당황스러웠지만, `scanner.nextLine()`을 한 번 더 호출해서 해결할 수 있다는 것을 배웠다.
