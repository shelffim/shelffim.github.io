---
title: "네트워크 - 자원정리"
pubDate: 2025-09-27
description: "김영한님의 자바 고급 2편 강의 part 9(네트워크 - 프로그램2) 학습 정리"
---

> **출처**: [김영한의 자바 고급 2편 강의](https://inf.run/8ES1C) - Section 9 : 네트워크 - 프로그램2

## 자원 관리 방법

### finally 블록의 문제점

```java
// ❌ 문제: 핵심 예외가 가려질 수 있음
try {
    socket.connect();
    socket.send(data);
} finally {
    socket.close();  // 새 예외 발생 시 핵심 예외 손실
}
```

**문제점**: `finally` 블록에서 예외가 발생하면 **핵심 예외가 가려질 수 있음**

### try-with-resources (권장)

```java
// ✅ 해결: 자동 자원 관리
try (Socket socket = new Socket("localhost", 8080)) {
   socket.send(data); // 네트워크 작업
} // 자동으로 socket.close() 호출
```

**장점**:

- 자동 자원 정리
- 핵심 예외와 정리 예외 모두 추적 가능

## try-with-resources 사용 제한

### 사용할 수 없는 경우

1. **블록 외부 자원**: try 블록 외부에서 선언된 자원은 자동 정리 안됨
2. **특정 시점 정리**: 서버 종료 등 블록 외부 시점에 정리가 필요한 경우

### finally 블록이 유용한 경우

```java
ServerSocket serverSocket = new ServerSocket(8080);

try {
    // 서버 로직
} finally {
    serverSocket.close();  // 서버 종료 시점에 정리
}
```

## 셧다운 훅 (Shutdown Hook)

### 개념

프로세스 종료 시 **자원 정리나 로그 기록** 등의 종료 작업을 수행하는 기능

### 종료 방식별 동작

| 종료 방식     | 셧다운 훅 동작                  |
| ------------- | ------------------------------- |
| **정상 종료** | ✅ 작동 (Ctrl+C, System.exit()) |
| **강제 종료** | ❌ 작동 안함 (kill -9)          |

### 사용법

```java
Runtime.getRuntime().addShutdownHook(new Thread(() -> {
    System.out.println("자원 정리 중...");
    serverSocket.close();
}));
```

**주의**: 강제 종료 시에는 셧다운 훅이 실행되지 않으므로, 자원 정리를 위한 **대기 시간**을 고려해야 함

## 결론

- **일반적인 자원**: try-with-resources 사용
- **서버 등 특별한 자원**: finally 블록 + 셧다운 훅 조합
