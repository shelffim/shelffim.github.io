---
title: "채팅 프로그램"
pubDate: 2025-09-29
description: "김영한님의 자바 고급 2편 강의 part 10(채팅 프로그램) 학습 정리"
---

> **출처**: [김영한의 자바 고급 2편 강의](https://inf.run/8ES1C) - Section 10 : 채팅 프로그램

## 실시간 통신과 다중 스레드

### 동시성 확보

실시간 통신에서 **사용자 입력 대기 중에도 서버 메시지를 받기 위해** 다중 스레드 사용

```java
// 입력과 수신을 별도 스레드로 분리
Thread inputThread = new Thread(() -> {
    // 사용자 입력 처리
});

Thread receiveThread = new Thread(() -> {
    // 서버 메시지 수신
});
```

### 자원 관리

```java
// 입력 스트림 종료
System.in.close();
```

## 디자인 패턴 적용

### Command Pattern

**요청을 객체로 캡슐화**하여 if-else 구조를 대체하는 디자인 패턴

```java
// Map으로 명령어 처리
Map<String, Command> commands = new HashMap<>();
commands.put("login", new LoginCommand());
commands.put("logout", new LogoutCommand());
```

### Null Object Pattern

**null 대신 안전한 기본 객체**를 반환하여 NullPointerException을 방지하는 디자인 패턴

```java
// getOrDefault로 안전한 처리
Command command = commands.getOrDefault(input, new DefaultCommand());
command.execute();
```

## 스레드 안전성

### 읽기 전용 Map

- **초기화 후 변경 없음**: 여러 스레드가 동시 접근해도 안전
- **동시성 문제 없음**: 데이터 조회만 수행
