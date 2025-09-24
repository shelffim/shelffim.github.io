---
title: "스레드 제어 2"
pubDate: 2025-09-24
description: "김영한님의 자바 고급 1편 강의 part 5(스레드 제어와 생명 주기 2) 학습 정리"
---

> **출처**: [김영한의 자바 고급 1편 강의](https://inf.run/iuVCy) - Section 5 : 스레드 제어와 생명 주기 관리 2

## 스레드 인터럽트 (Interrupt)

### 문제점: Boolean 플래그 방식

단순한 boolean 플래그로 스레드를 정지시키는 방법은 **즉시 응답하지 않는** 문제가 있습니다.

### interrupt() 메서드

`sleep()`, `wait()`, `join()` 메서드 호출 시 `InterruptedException`을 발생시켜 스레드를 대기 상태에서 즉각 벗어나게 합니다.

```java
Thread workerThread = new Thread(() -> {
    try {
        Thread.sleep(5000);  // 5초 대기
    } catch (InterruptedException e) {
        System.out.println("인터럽트됨!");
    }
});

workerThread.start();
Thread.sleep(1000);
workerThread.interrupt();  // 즉시 인터럽트
```

### 인터럽트 상태 확인 메서드

| 메서드            | 설명                        | 사용 시기   |
| ----------------- | --------------------------- | ----------- |
| `isInterrupted()` | 상태 확인만 (변경하지 않음) | 상태 체크용 |
| `interrupted()`   | 상태 확인 후 자동 해제      | 직접 체크용 |

```java
// 권장: interrupted() 사용
if (Thread.interrupted()) {
    // 자원 정리 후 종료
    return;
}

// 상태 확인만 필요한 경우
if (Thread.currentThread().isInterrupted()) {
    // 인터럽트 상태만 확인
}
```

## 기타 스레드 제어 메서드

### Thread.stop() - 사용 금지

- **문제**: 언제 어디서 멈출지 예측 불가
- **결과**: 자원 정리 어려움
- **결론**: **사용하지 말 것**

### Thread.yield() - CPU 양보

```java
// CPU 사용 기회를 다른 스레드에게 양보
Thread.yield();
```

**특징**:

- `RUNNABLE` 상태 유지
- 다른 스레드가 실행될 수 있음 (보장되지 않음)
- `sleep()`보다 가벼움 (상태 전환 없음)
