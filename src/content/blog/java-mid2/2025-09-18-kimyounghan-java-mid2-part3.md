---
title: "김영한의 자바 중급 2편 강의 - part 3: 제네릭 2"
pubDate: 2025-09-18
description: "김영한님의 자바 중급 2편 강의 part 3(제네릭 2) 학습 정리"
---

> **출처**: [김영한의 자바 중급 2편 강의](https://inf.run/ir9Dw) - Section 3: 제네릭 2

## 제네릭의 장점

제네릭을 사용하면 컴파일 시 타입 안전성을 높이고, 다양한 타입에 재사용 가능한 코드를 작성할 수 있습니다.

## 제네릭 타입 매개변수의 한계

제네릭에서 타입 매개변수를 사용하면 Object 타입으로 추론되기 때문에 어떤 타입이든 들어올 수 있고, Object의 메서드만 호출할 수 있습니다.

```java
public class Box<T> {
    private T item;

    public void setItem(T item) {
        this.item = item;
        // item.toString();  // Object 메서드만 호출 가능
        // item.length();    // String 메서드는 호출 불가 (T가 String인지 확실하지 않음)
    }
}
```

## 제네릭 타입 제한 (extends)

제네릭 타입 매개변수에 제약을 걸어서 타입의 상한을 제한하는 것이 좋습니다. 제네릭 타입 매개변수에 extends 키워드를 사용해 타입의 상한을 제한하면 해당 타입과 그 자식 타입만 허용하고, 해당 타입의 메서드를 호출할 수 있습니다.

```java
public class NumberBox<T extends Number> {
    private T item;

    public void setItem(T item) {
        this.item = item;
        // Number의 메서드 호출 가능
        System.out.println(item.doubleValue());
    }
}

// 사용 예시
NumberBox<Integer> intBox = new NumberBox<>();  // 가능
NumberBox<Double> doubleBox = new NumberBox<>();  // 가능
// NumberBox<String> stringBox = new NumberBox<>();  // 컴파일 오류!
```

## 제네릭 클래스 vs 제네릭 메서드

### 제네릭 클래스

제네릭 클래스는 인스턴스가 생성될 때 전달되는 인자를 보고 타입을 결정합니다.

```java
public class Box<T> {
    private T item;

    public void setItem(T item) {
        this.item = item;
    }
}

// 사용 시 타입 결정
Box<String> stringBox = new Box<>();  // T는 String으로 결정
```

### 제네릭 메서드

제네릭 메서드는 메서드를 실제 호출할 때 전달되는 인자를 보고 타입을 결정합니다. 제네릭 메서드는 인스턴스 메서드와 static 메서드 모두 사용할 수 있습니다.

```java
public class Util {
    // 제네릭 메서드
    public static <T> T getFirst(T[] array) {
        return array[0];
    }

    // 인스턴스 제네릭 메서드
    public <T> void printItem(T item) {
        System.out.println(item);
    }
}

// 사용 예시
String[] strings = {"a", "b", "c"};
String first = Util.getFirst(strings);  // T는 String으로 결정
```

## static 메서드와 제네릭

static 메서드는 인스턴스 생성 없이 사용할 수 있기 때문에 클래스 제네릭 타입 매개변수를 사용할 수 없습니다. static 메서드에 제네릭을 도입하려면 제네릭 메서드를 사용해야 합니다.

```java
public class Box<T> {
    private T item;

    // static 메서드에서 클래스 제네릭 타입 사용 불가
    // public static void printItem(T item) { }  // 컴파일 오류!

    // 제네릭 메서드로 해결
    public static <U> void printItem(U item) {
        System.out.println(item);
    }
}
```

## 타입 매개변수 우선순위

제네릭 타입과 제네릭 메서드의 타입 매개변수가 같으면 제네릭 타입보다 제네릭 메서드가 높은 우선순위를 가집니다. 그렇지만 둘의 이름을 다르게 하는 것이 좋습니다.

```java
public class Box<T> {
    // 제네릭 메서드의 T가 클래스의 T보다 우선순위가 높음
    public <T> void method(T item) {
        // 여기서 T는 메서드의 타입 매개변수
    }
}
```

## 와일드카드 (?)

와일드카드는 이미 정의된 제네릭 타입의 객체를 메서드 인자 등으로 받을 때, 좀 더 유연하게 사용하고 다루기 위해 사용됩니다. 일반적인 메서드에 인자로 제네릭 타입을 받을 때 와일드카드를 사용합니다.

```java
public class Util {
    // 와일드카드 사용
    public static void printBox(Box<?> box) {
        Object item = box.getItem();
        System.out.println(item);
    }
}
```

## 와일드카드 상한 제한 (extends)

와일드카드도 extends 키워드를 사용해 타입의 상한을 제한하는 것이 가능합니다. `? extends T`가 T 타입의 상위 타입만 입력 받을 수 있습니다.

```java
public class Util {
    public static void printNumber(Box<? extends Number> box) {
        Number number = box.getItem();
        System.out.println(number.doubleValue());
    }
}

// 사용 예시
Box<Integer> intBox = new Box<>();
Box<Double> doubleBox = new Box<>();
Util.printNumber(intBox);    // 가능
Util.printNumber(doubleBox); // 가능
```

## 와일드카드 하한 제한 (super)

와일드카드는 super 키워드를 사용해 타입의 하한을 제한하는 것이 가능합니다. `? super T`가 T 타입의 하위 타입만 입력 받을 수 있습니다.

```java
public class Util {
    public static void addNumber(Box<? super Integer> box) {
        box.setItem(100);  // Integer 타입만 설정 가능
    }
}
```

## 제네릭 vs 와일드카드 사용 권장사항

제네릭 타입이나 제네릭 메서드는 꼭 필요한 상황에서만 사용하고 그렇지 않은 상황이면 와일드카드를 사용하는 것을 권장합니다.

## 제한된 와일드카드의 반환 타입

제네릭 타입 메서드에서 제한된 와일드카드를 인자로 받고 반환하는 메서드의 반환 타입은 제한된 와일드카드로 표현됩니다.

예시: 제네릭 타입 `Box<T>`가 있고, `Box<? extends Number>`를 인자로 받는 메서드가 있습니다. 이 메서드 안에서 인자로 받은 `Box` 객체에서 `box.getItem()` 메서드를 호출하면 반환되는 값의 타입은 `Number` 타입입니다. 실제로는 `Integer`, `Double`, `Long` 등이 들어있을 수 있지만, 메서드 내부에서는 `Number` 타입으로만 접근할 수 있습니다.

```java
public class Util {
    public static Number getNumber(Box<? extends Number> box) {
        return box.getItem();  // Number 타입으로 반환
    }
}
```

## 제네릭의 런타임 제약사항

제네릭 정보는 컴파일러가 추론하기 때문에 런타임에는 제네릭 정보가 존재하지 않습니다. instanceof 연산자를 사용해서 제네릭 타입을 확인할 수 없고 new 연산자를 사용해서 제네릭 타입의 인스턴스를 반환할 수 없습니다.

```java
public class Box<T> {
    // 런타임에 제네릭 정보 확인 불가
    public T checkType(Object obj) {
        // if (obj instanceof T) { }  // 컴파일 오류!
        //return new T();             // 컴파일 오류!
    }
}
```
