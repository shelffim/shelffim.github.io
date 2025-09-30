---
title: "Command Pattern"
pubDate: 2025-09-29
description: "김영한님의 자바 고급 2편 강의 part 10(채팅 프로그램) 학습 정리"
---

> **출처**: [김영한의 자바 고급 2편 강의](https://inf.run/8ES1C) - Section 10 : 채팅 프로그램

## Command Pattern

### 개념

**요청을 독립적인 객체로 변환**하여 처리하는 디자인 패턴

### 특징

- **분리**: 작업 호출 객체와 작업 수행 객체 분리
- **확장성**: 기존 코드 변경 없이 새로운 명령 추가 가능

## 기존 방식의 문제점

### if-else 구조

```java
// ❌ 새로운 명령어 추가 시 코드 수정 필요
public void handleCommand(String command) {
    if (command.equals("login")) {
        // 로그인 처리
    } else if (command.equals("logout")) {
        // 로그아웃 처리
    }
    // 새 명령어 추가 시 이 메서드 수정 필요
}
```

## Command Pattern 적용

### 기본 구조

```java
// Command 인터페이스
public interface Command {
    void execute();
}

// 구체적인 명령들
public class LoginCommand implements Command {
    public void execute() {
        // 로그인 처리
    }
}

public class LogoutCommand implements Command {
    public void execute() {
        // 로그아웃 처리
    }
}
```

### 사용 예시

```java
// ✅ 새로운 명령어 추가 시 기존 코드 변경 불필요
Map<String, Command> commands = new HashMap<>();
commands.put("login", new LoginCommand());
commands.put("logout", new LogoutCommand());

public void handleCommand(String command) {
    Command cmd = commands.get(command);
    if (cmd != null) {
        cmd.execute();
    }
}
```

## 장단점

### 장점

- **확장성**: 새 명령어 추가 시 기존 코드 변경 불필요
- **유지보수**: 각 기능이 명확히 분리됨
- **재사용성**: 명령 객체를 재사용 가능

### 단점

- **복잡성**: 간단한 작업에도 여러 클래스 생성 필요
- **오버헤드**: 단순한 if문보다 복잡함

## 적용 기준

- **적용 권장**: 기능이 복잡하고 확장이 예상되는 경우
- **적용 비권장**: 단순한 if문으로 해결 가능한 문제
