---
title: "네트워크 - 프로그램1"
pubDate: 2025-09-26
description: "김영한님의 자바 고급 2편 강의 part 8(네트워크 - 프로그램1) 학습 정리"
---

> **출처**: [김영한의 자바 고급 2편 강의](https://inf.run/8ES1C) - Section 8 : 네트워크 - 프로그램1

## 네트워크 프로그래밍 기본

### InetAddress

호스트 이름으로 **IP 주소 조회** 가능

```java
// 도메인 → IP 변환
InetAddress address = InetAddress.getByName("google.com");
System.out.println(address);  // IP 주소 출력
```

## 소켓 (Socket)

### 개념

**클라이언트와 서버 간의 네트워크 연결점**

- IP 주소 + 포트 번호로 특정 프로그램과 연결
- 데이터 송수신을 위한 추상적 개념

### Socket vs ServerSocket

| 구분             | 역할                           | 사용 시기                     |
| ---------------- | ------------------------------ | ----------------------------- |
| **Socket**       | 클라이언트 연결 및 데이터 통신 | 클라이언트, 서버의 실제 통신  |
| **ServerSocket** | TCP 연결만 담당                | 서버에서 클라이언트 연결 대기 |

## 서버 프로그래밍

### 단일 스레드 서버 (문제점)

```java
// 단일 스레드 서버
ServerSocket serverSocket = new ServerSocket(8080);

while (true) {
    Socket clientSocket = serverSocket.accept();  // 연결 대기 (블로킹)

    // 클라이언트 처리 (동시 처리 불가)
    handleClient(clientSocket);
}
```

**문제**: 한 번에 하나의 클라이언트만 처리 가능

### 멀티스레드 서버 (해결책)

```java
// 멀티스레드 서버
ServerSocket serverSocket = new ServerSocket(8080);

while (true) {
    Socket clientSocket = serverSocket.accept();  // 연결 수락만

    // 새 스레드에서 클라이언트 처리
    new Thread(() -> handleClient(clientSocket)).start();
}
```

**장점**: 여러 클라이언트 동시 처리 가능

## 자원 관리

### finally 블록의 문제점

```java
// ❌ 문제: 핵심 예외가 가려질 수 있음
try {
    // 네트워크 작업
} finally {
    socket.close();  // 새 예외 발생 시 핵심 예외 손실
}
```

### try-with-resources (권장)

```java
// ✅ 해결: 자동 자원 관리
try (Socket socket = new Socket("localhost", 8080)) {
    // 네트워크 작업
} // 자동으로 socket.close() 호출
```

**장점**:

- 자동 자원 정리
- 핵심 예외와 정리 예외 모두 추적 가능
