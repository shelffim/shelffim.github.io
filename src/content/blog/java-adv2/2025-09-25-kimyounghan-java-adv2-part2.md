---
title: "문자 인코딩"
pubDate: 2025-09-25
description: "김영한님의 자바 고급 2편 강의 part 2(문자 인코딩) 학습 정리"
---

> **출처**: [김영한의 자바 고급 2편 강의](https://inf.run/8ES1C) - Section 2 : 문자 인코딩

## 컴퓨터의 문자 처리

### 기본 개념

- **비트**: 데이터의 최소 단위 (0 또는 1)
- **바이트**: 8비트
- **인코딩**: 문자 → 숫자 변환
- **디코딩**: 숫자 → 문자 변환

### 문자 집합의 필요성

컴퓨터는 **숫자로만 처리**하므로, 문자를 인식하려면 **문자 집합**이 필요합니다.

## 문자 인코딩 표준

### ASCII (초기 표준)

- **영어 알파벳**과 일부 기호만 지원
- **비영어권 문자** 표현 불가

### UTF-8 (현재 표준)

| 특징          | 설명                              |
| ------------- | --------------------------------- |
| **호환성**    | ASCII와 완벽 호환                 |
| **가변 길이** | 1바이트 ~ 4바이트                 |
| **효율성**    | 공간 활용 및 네트워크 효율성 우수 |

```java
// UTF-8 문자열 처리
String korean = "안녕하세요";
String english = "Hello";

// 바이트 배열로 변환
byte[] koreanBytes = korean.getBytes(StandardCharsets.UTF_8);
byte[] englishBytes = english.getBytes(StandardCharsets.UTF_8);

System.out.println("한글 바이트 수: " + koreanBytes.length);  // 15바이트
System.out.println("영어 바이트 수: " + englishBytes.length);  // 5바이트
```

## 인코딩 문제

### 깨진 글자 발생 원인

**저장 시 인코딩 ≠ 읽을 때 디코딩**

```java
// 문제 상황 예시
String text = "안녕하세요";

// UTF-8로 저장
byte[] utf8Bytes = text.getBytes(StandardCharsets.UTF_8);

// 잘못된 인코딩으로 읽기 (문제 발생)
String wrong = new String(utf8Bytes, StandardCharsets.ISO_8859_1);
System.out.println(wrong);  // 깨진 글자 출력
```

### 해결 방법

```java
// 올바른 인코딩 사용
String correct = new String(utf8Bytes, StandardCharsets.UTF_8);
System.out.println(correct);  // "안녕하세요" 정상 출력
```

## Charset 클래스

자바에서 문자 집합을 다루기 위한 클래스입니다.

```java
// Charset 사용 예시
Charset utf8 = StandardCharsets.UTF_8;
Charset euckr = Charset.forName("EUC-KR");

String text = "테스트";
byte[] bytes = text.getBytes(utf8);
String decoded = new String(bytes, utf8);
```
