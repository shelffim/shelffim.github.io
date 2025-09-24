---
title: "스레드 제어 1"
pubDate: 2025-09-24
description: "김영한님의 자바 고급 1편 강의 part 4(스레드 제어와 생명 주기 1) 학습 정리"
---

> **출처**: [김영한의 자바 고급 1편 강의](https://inf.run/iuVCy) - Section 4 : 스레드 제어와 생명 주기 관리 1

## 스레드 완료 대기 문제

스레드로 작업을 수행할 때, **main 스레드는 다른 스레드의 완료를 기다리지 않고** 바로 다음 코드를 실행합니다.

```java
Thread workerThread = new Thread(new WorkerTask());
workerThread.start();
System.out.println("Main 스레드는 즉시 실행됨");  // WorkerTask 완료 전에 실행
```

## 부적절한 대기 방법들

### 1. Thread.sleep() 사용

- **문제**: 대기 시간이 부정확하고, 작업 완료 시점을 모름
- **단점**: 너무 짧으면 작업 미완료, 너무 길면 비효율적

### 2. 반복문으로 상태 확인

- **문제**: CPU 자원 낭비, 성능 저하
- **단점**: 계속되는 루프로 인한 부하

## join() 메서드

**적절한 해결책**으로 스레드 완료를 기다리는 메서드입니다.

### join() - 무한 대기

```java
Thread workerThread = new Thread(new WorkerTask());
workerThread.start();
workerThread.join();  // 작업 완료까지 대기
System.out.println("작업 완료 후 실행");
```

### join(milliseconds) - 시간 제한 대기

```java
Thread workerThread = new Thread(new WorkerTask());
workerThread.start();

if (workerThread.join(3000)) {  // 3초 대기
    System.out.println("작업 완료");
} else {
    System.out.println("시간 초과 - 추가 처리 필요");
}
```

**주의**: 시간 제한으로 중간에 나올 경우, 결과가 없을 수 있으므로 추가 오류 처리가 필요합니다.
