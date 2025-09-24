---
title: "메모리 가시성"
pubDate: 2025-09-24
description: "김영한님의 자바 고급 1편 강의 part 6(메모리 가시성) 학습 정리"
---

> **출처**: [김영한의 자바 고급 1편 강의](https://inf.run/iuVCy) - Section 6 : 메모리 가시성

## 메모리 가시성 문제

멀티스레드 환경에서 **한 스레드가 변경한 변수 값을 다른 스레드에서 즉시 확인할 수 없는** 문제입니다.

### 발생 원인

각 스레드가 자신의 **캐시 메모리**에서 값을 읽어오기 때문에, 메인 메모리와의 동기화가 지연됩니다.

```java
// 문제가 발생할 수 있는 코드
class Counter {
    private int count = 0;  // 메모리 가시성 문제 가능성

    public void increment() {
        count++;  // 스레드 A가 변경
    }

    public int getCount() {
        return count;  // 스레드 B가 읽기
    }
}
```

## volatile 키워드

### 해결 방법

변수의 값이 변경되면 **즉시 메인 메모리에 반영**하고, 읽기 시에도 **항상 메인 메모리에서 읽도록** 강제합니다.

```java
class SafeCounter {
    private volatile int count = 0;  // volatile 추가

    public void increment() {
        count++;  // 즉시 메인 메모리 반영
    }

    public int getCount() {
        return count;  // 메인 메모리에서 읽기
    }
}
```

### 특징

- **장점**: 메모리 가시성 문제 해결
- **단점**: 성능 저하 (캐시 사용 불가)

## Happens-Before 관계

자바 메모리 모델에서 **스레드 간 변경 사항 가시성을 보장**하는 핵심 개념입니다.

### 예시

A 작업이 B 작업보다 **Happens-Before 관계**에 있다면:

- A 작업의 변경 내용이 B 작업 시작 전에 메모리에 반영됨

## 결론

`volatile` 또는 **스레드 동기화 기법**을 사용하면 메모리 가시성 문제를 해결할 수 있습니다.
