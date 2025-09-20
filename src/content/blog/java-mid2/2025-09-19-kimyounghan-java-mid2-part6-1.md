---
title: "의존관계 주입(DI)"
pubDate: 2025-09-19
description: "김영한님의 자바 중급 2편 강의 part 6(컬렉션 프레임워크 - List) 학습 정리"
---

> **출처**: [김영한의 자바 중급 2편 강의](https://inf.run/ir9Dw) - Section 6 : 컬렉션 프레임워크 - List

## 의존관계 주입(DI)이란?

의존관계 주입(DI)이란 객체가 자신의 의존 대상을 직접 생성하지 않고, 외부(생성자 등)에서 제공받는 것을 의미합니다.

```java
// 의존관계 주입 전 (직접 생성)
public class OrderService {
    private PaymentService paymentService = new CardPaymentService();  // 직접 생성
}

// 의존관계 주입 후 (외부에서 주입)
public class OrderService {
    private PaymentService paymentService;

    public OrderService(PaymentService paymentService) {  // 외부에서 주입
        this.paymentService = paymentService;
    }
}
```

## 컴파일 타임 vs 런타임 의존관계

### 컴파일 타임 의존관계

소스 코드 상에서 나타나는 정적인 의존관계로 주로 인터페이스나 추상 클래스에 의존합니다.

### 런타임 의존관계

프로그램이 실행되는 시점에 실제로 생성된 인스턴스와 연결되는 동적인 의존관계입니다. 런타임 시점에는 구현 클래스의 인스턴스와 관계를 맺습니다.

## DI의 효과

의존관계 주입을 통해 클라이언트 코드는:

- **컴파일 타임**: 추상화에 의존
- **런타임**: 외부에서 주입된 구체적인 구현체와 관계를 맺음

## 생성자 주입

생성자 주입은 클래스의 생성자를 통해 의존 객체를 전달받는 방식입니다. 필요에 따라 다른 구현체로 쉽게 변경할 수 있습니다.

```java
// 인터페이스
interface PaymentService {
    void pay(int amount);
}

// 구현체 1
class CardPaymentService implements PaymentService {
    public void pay(int amount) {
        System.out.println("카드로 " + amount + "원 결제");
    }
}

// 구현체 2
class BankPaymentService implements PaymentService {
    public void pay(int amount) {
        System.out.println("계좌이체로 " + amount + "원 결제");
    }
}

// 클라이언트 코드
public class OrderService {
    private PaymentService paymentService;

    public OrderService(PaymentService paymentService) {  // 생성자 주입
        this.paymentService = paymentService;
    }

    public void processOrder(int amount) {
        paymentService.pay(amount);
    }
}
```

## 전략 패턴

전략 패턴은 알고리즘을 클라이언트 코드의 변경 없이 동적으로 교체할 수 있게 하는 디자인 패턴입니다.

위의 예시에서 `PaymentService`는 전략 패턴의 예시로, 결제 방식을 동적으로 변경할 수 있게 해줍니다.
