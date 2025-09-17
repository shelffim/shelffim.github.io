---
title: "김영한의 자바 중급 1편 강의 - part 11: 예외처리 2"
pubDate: 2025-09-16
description: "김영한님의 자바 중급 1편 강의 part 11(예외처리 2) 학습 정리"
---

> **출처**: [김영한의 자바 중급 1편 강의](https://inf.run/XGzSo) - Section 11: 예외처리 2

## 다중 catch 블록

하나의 try 블록에 여러 개의 catch 블록을 사용할 수 있습니다. 하나의 try 블록에 정상적인 로직을 작성하고 각 catch 블록에 예외 처리 로직을 작성해서 코드의 핵심 흐름을 파악하기 쉽게 만듭니다.

```java
try {
    // 정상적인 로직
    int result = 10 / 0;  // 0으로 나누기 시도
    System.out.println("결과: " + result);
} catch (ArithmeticException e) {
    // 산술 예외 처리
    System.out.println("0으로 나눌 수 없습니다.");
} catch (Exception e) {
    // 기타 예외 처리
    System.out.println("예상치 못한 오류가 발생했습니다.");
}
```

## 예외 처리의 목적

예외를 잡는 주된 목적은 예외 발생 시 프로그램이 갑자기 종료되는 것을 막고, 오류 상황을 처리하여 정상 흐름으로 복귀하거나 다음 단계로 진행하기 위해서입니다.

## finally 블록

finally 블록은 예외 발생 여부와 상관없이 항상 try 블록 종료 시 실행됩니다. finally 블록은 리소스 해제 보장을 위해 사용합니다.

```java
String data = null;
try {
    data = "안녕하세요";
    System.out.println(data.length());  // 정상 실행
} catch (NullPointerException e) {
    System.out.println("데이터가 null입니다.");
} finally {
    System.out.println("finally 블록은 항상 실행됩니다.");
    data = null;  // 리소스 정리
}
```

## 예외 계층 구조

예외를 부모-자식 계층 구조로 구성해서 상위 예외를 통해 관련 예외들을 묶어 일반적인 처리가 가능하고, 하위 특정 예외를 통해 더욱 세분화된 맞춤형 처리를 할 수 있습니다.

예외 계층 구조 시, catch 블록을 자식 예외 클래스부터 부모 예외 클래스 순으로 작성합니다. 상위 예외를 먼저 작성하면 하위 예외는 실행되지 않습니다.

```java
try {
    String str = null;
    System.out.println(str.length());  // NullPointerException 발생
} catch (NullPointerException e) {
    // 구체적인 예외 처리 (자식)
    System.out.println("null 값에 접근했습니다.");
} catch (RuntimeException e) {
    // 일반적인 예외 처리 (부모)
    System.out.println("런타임 예외가 발생했습니다.");
} catch (Exception e) {
    // 최상위 예외 처리
    System.out.println("예외가 발생했습니다.");
}
```

## 체크 예외 vs 언체크 예외

대부분의 예외는 복구 불가능하기 때문에 체크 예외를 선언하면 throws 선언이 늘어나 코드 복잡성이 증가하기 때문에 언체크 예외를 사용해 공통 처리를 더 선호합니다.

## 예외 처리 메서드

exceptionHandler는 예외를 처리하는 메서드를 정의합니다. 예외도 객체이므로 필요하면 instanceof 연산자를 사용하여 예외 타입을 확인하고 처리할 수 있습니다.

```java
public void exceptionHandler(Exception e) {
    if (e instanceof ArithmeticException) {
        System.out.println("산술 예외 발생: 0으로 나눌 수 없습니다.");
    } else if (e instanceof NullPointerException) {
        System.out.println("널 포인터 예외 발생: null 값에 접근했습니다.");
    } else {
        System.out.println("기타 예외 발생");
    }

    e.printStackTrace(); // 예외 발생 시 예외 스택 트레이스를 출력
}
```

## try-with-resources

try-with-resources는 리소스를 자동으로 해제하는 기능을 제공합니다. AutoCloseable 인터페이스를 구현한 객체를 사용하면 try 블록이 종료될 때 자동으로 close() 메서드를 호출하여 리소스를 해제합니다.

```java
// 간단한 예시: Scanner 사용
try (Scanner scanner = new Scanner(System.in)) {
    System.out.println("이름을 입력하세요:");
    String name = scanner.nextLine();
    System.out.println("안녕하세요, " + name + "님!");
    // 자동으로 scanner.close() 호출됨
} catch (Exception e) {
    System.out.println("입력 오류가 발생했습니다.");
}
```

try-with-resources 구문을 사용하면 다음과 같은 장점이 있습니다:

- **리소스 누수 방지**: 자동으로 리소스가 해제되어 메모리 누수 방지
- **코드 간결성 및 가독성 향상**: 명시적인 close() 호출 불필요
- **스코프 범위 한정**: 리소스가 try 블록 내에서만 사용 가능
- **더 빠른 자원 해제**: 예외 발생 시에도 안전하게 리소스 해제
