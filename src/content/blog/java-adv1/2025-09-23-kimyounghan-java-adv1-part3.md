---
title: "운영체제 기본 개념"
pubDate: 2025-09-23
description: "김영한님의 자바 고급 1편 강의 part 3(스레드 생성과 실행) 학습 정리"
---

> **출처**: [김영한의 자바 고급 1편 강의](https://inf.run/iuVCy) - Section 3 : 스레드 생성과 실행

## 스레드 생성 방법

스레드를 만드는 방법은 **Thread 클래스 상속**과 **Runnable 인터페이스 구현** 두 가지가 있습니다.

### Thread 클래스 상속 방식

```java
class MyThread extends Thread {
    @Override
    public void run() {
        // 스레드가 실행할 코드
    }
}

// 사용
MyThread thread = new MyThread();
thread.start();
```

### Runnable 인터페이스 구현 방식 (권장)

```java
class MyRunnable implements Runnable {
    @Override
    public void run() {
        // 스레드가 실행할 코드
    }
}

// 사용
Thread thread = new Thread(new MyRunnable());
thread.start();
```

## 스레드 실행 과정

1. 스레드 객체 생성
2. `start()` 메서드 호출
3. 스택 공간 할당 및 새로운 스레드 시작
4. `run()` 메서드 실행

**중요**: `main` 스레드는 `start()` 메서드로 실행을 지시할 뿐, `run()` 메서드를 직접 실행하지 않습니다.

## 스레드 실행 순서

스레드는 **동시에 실행**되기 때문에 스레드 간의 실행 순서는 보장되지 않습니다.

## 스레드 종류

### 사용자 스레드 (기본값)

- 프로그램의 주요 작업을 수행
- 작업이 완료될 때까지 실행
- 모든 사용자 스레드가 종료되면 JVM도 종료

### 데몬 스레드

- 백그라운드에서 보조적인 작업 수행
- 사용하지 않는 파일이나 메모리 정리
- 모든 사용자 스레드가 종료되면 자동으로 종료

```java
Thread daemonThread = new Thread(new MyRunnable());
daemonThread.setDaemon(true);  // 데몬 스레드로 설정
daemonThread.start();
```

## 예외 처리

`run()` 메서드는 체크 예외를 밖으로 던질 수 없으므로, `Thread.sleep()` 등을 사용할 때 반드시 예외를 잡아야 합니다.

```java
@Override
public void run() {
    try {
        Thread.sleep(1000);
    } catch (InterruptedException e) {
        // 예외 처리
    }
}
```

## 방식별 장단점

### Thread 클래스 상속

- **장점**: 간단함
- **단점**: 상속의 제한, 유연성 부족

### Runnable 인터페이스 구현 (권장)

- **장점**: 상속에서 자유로움, 코드 분리, 자원 관리 효율적
- **단점**: 코드가 복잡해질 수 있음

## Runnable 공유

여러 스레드가 동일한 Runnable 인스턴스를 사용할 수 있습니다. 이 경우 각 스레드는 독립적인 스택 프레임에서 `run()` 메서드를 실행합니다.
