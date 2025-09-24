---
title: "스레드 생명 주기"
pubDate: 2025-09-24
description: "김영한님의 자바 고급 1편 강의 part 4(스레드 제어와 생명 주기 1) 학습 정리"
---

> **출처**: [김영한의 자바 고급 1편 강의](https://inf.run/iuVCy) - Section 4 : 스레드 제어와 생명 주기 관리 1

## 스레드 상태 (Thread State)

스레드는 **6가지 상태**를 가지며, 상태는 getState() 메서드를 통해 확인할 수 있다.

| 상태            | 설명                                  | 예시                           |
| --------------- | ------------------------------------- | ------------------------------ |
| `NEW`           | 스레드 생성 후 `start()` 호출 전 상태 | `new Thread()`                 |
| `RUNNABLE`      | 실행 중이거나 실행 준비 완료 상태     | CPU 사용 중 또는 스케줄러 대기 |
| `BLOCKED`       | 동기화 락을 기다리는 상태             | `synchronized` 블록 대기       |
| `WAITING`       | 무기한 대기 상태                      | `wait()` 호출                  |
| `TIMED_WAITING` | 시간 제한 대기 상태                   | `sleep(1000)` 호출             |
| `TERMINATED`    | 스레드 실행 완료 상태                 | `run()` 메서드 종료            |

## 상태 전환

### 1. NEW → RUNNABLE

```java
Thread thread = new Thread(new MyRunnable());
// thread.getState() == Thread.State.NEW

thread.start();
// thread.getState() == Thread.State.RUNNABLE
```

### 2. RUNNABLE → 대기 상태들

```java
// WAITING
synchronized(lock) {
    lock.wait();  // RUNNABLE → WAITING
}

// TIMED_WAITING
Thread.sleep(1000);  // RUNNABLE → TIMED_WAITING

// BLOCKED
synchronized(lock) {  // 다른 스레드가 락을 가지고 있다면 RUNNABLE → BLOCKED
    // ...
}
```

### 3. 대기 상태 → RUNNABLE

- 락을 얻거나
- `wait()`, `sleep()` 메서드가 종료되면
- 다시 `RUNNABLE` 상태로 전환

### 4. RUNNABLE → TERMINATED

```java
@Override
public void run() {
    // 작업 수행
} // run() 메서드 종료 시 RUNNABLE → TERMINATED
```
