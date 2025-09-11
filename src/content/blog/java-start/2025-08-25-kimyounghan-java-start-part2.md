---
title: "김영한의 자바 기초 강의 - part 2"
pubDate: 2025-08-25
description: "김영한님의 자바 기초 강의 part 2(HelloWorld) 학습 정리"

> **출처**: [김영한의 자바 기초 강의](https://inf.run/PVx3u) - Section 2: HelloWorld

---

## HelloJava.java 코드

```java
public class HelloJava {

    public static void main(String[] args) {
        System.out.println("hello java");
        //System.out.println("hello java2"); 한 줄 주석

        /* 여러 줄 주석
        System.out.println("hello java3");
        System.out.println("hello java4");
        */
    }

}
```

IntelliJ 환경 설정을 마치고 HelloJava.java 파일을 생성하고 코드를 작성하고 실행했다.

## 코드 설명

- **`public class HelloJava`**: 클래스를 선언하는 부분이고, 파일명과 클래스 이름이 같아야 한다.
- **`public static void main(String[] args)`**: main 메서드로 자바는 `main(String[] args)` 메서드를 찾아서 실행한다. 프로그램의 시작점 역할을 한다.
- **`System.out.println()`**: 값을 콘솔에 출력하는 기능이다.
- **`;`**: 세미콜론으로 문장의 끝을 나타낸다. 필수이다.
- **`//`**: 한 줄 주석으로 이 기호 이후의 모든 텍스트는 주석으로 처리된다.
- **`/* */`**: 여러 줄 주석으로 이 사이의 모든 텍스트는 주석으로 처리된다.

## 자바의 동작 원리

- 자바는 모두 표준 스펙에 맞도록 개발되어 있다.
- 자바 프로그램은 자바가 설치된 모든 OS에서 실행할 수 있다.
- 자바 개발자는 특정 OS에 맞추어 개발을 하지 않아도 된다.
- 자바 소스 파일(.java)을 개발자가 작성하면 자바 컴파일러를 사용하여 소스 코드를 컴파일 한다. 컴파일 과정을 통해 JVM이 이해할 수 있는 바이트코드(.class)로 변환된다. JVM이 실행되면서 프로그램이 작동한다.

## 느낀 점

Swift에서는 별도의 main 함수 없이 코드를 바로 실행할 수 있는데, Java는 main 메서드라는 정해진 진입점을 반드시 가져야 한다는 점이 까다로운 부분이다. 또한 모든 문장 끝에 세미콜론을 붙여야 하는데 이것도 생각보다 까다로운 부분이다. 하지만 한번 작성하면 어디서든 실행된다는 점이 매우 편리하다.
