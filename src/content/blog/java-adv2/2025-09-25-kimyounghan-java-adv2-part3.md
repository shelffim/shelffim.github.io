---
title: "I/O 기본 1"
pubDate: 2025-09-25
description: "김영한님의 자바 고급 2편 강의 part 3(I/O 기본 1) 학습 정리"
---

> **출처**: [김영한의 자바 고급 2편 강의](https://inf.run/8ES1C) - Section 3 : I/O 기본 1

## I/O 스트림 기본 개념

### 스트림이란?

자바에서 **외부 데이터와 프로그램 간의 데이터 교환**을 위한 표준화된 방식입니다.

- **입력 스트림**: 외부 데이터 → 자바 프로그램
- **출력 스트림**: 자바 프로그램 → 외부 데이터
- **단방향**: 스트림은 한 방향으로만 데이터가 흐름

## 파일 입출력

### 파일 출력 (FileOutputStream)

```java
// 파일 생성 및 데이터 출력
FileOutputStream fos = new FileOutputStream("test.txt", true);
String data = "Hello World";
fos.write(data.getBytes());  // byte[] 단위 출력
fos.write('A');              // byte 단위 출력
```

| 옵션    | 설명                        |
| ------- | --------------------------- |
| `true`  | 기존 파일에 데이터 추가     |
| `false` | 기존 파일 덮어쓰기 (기본값) |

### 파일 입력 (FileInputStream)

```java
// 파일에서 데이터 읽기
FileInputStream fis = new FileInputStream("test.txt");
byte[] buffer = new byte[1024];
int bytesRead = fis.read(buffer);  // buffer.length만큼 데이터를 읽어와 buffer에 저장하고, 실제로 읽은 바이트 수를 반환한다

// 모든 데이터 한 번에 읽기
byte[] allData = fis.readAllBytes();

// 파일 끝 확인
int data = fis.read();
if (data == -1) {
    System.out.println("파일 끝에 도달");
}
```

**중요**: 외부 자원 사용 시 **반드시 `close()` 호출** 필요

## 버퍼링과 성능

### 문제점: 시스템 호출 오버헤드

바이트 단위 입출력 시 **운영체제에 개별 시스템 호출**이 발생하여 성능 저하

### 해결책: 버퍼링

```java
// 버퍼 사용 예시
FileOutputStream fos = new FileOutputStream("output.txt");
BufferedOutputStream bos = new BufferedOutputStream(fos);

// 버퍼에 데이터 모아서 한 번에 출력
bos.write("Large data...".getBytes());
bos.flush();  // 버퍼 내용 강제 출력
```

**효과**: 시스템 호출 횟수 감소 → 성능 향상

## 스트림 종류

### 기본 스트림 vs 보조 스트림

| 구분            | 설명                                 | 예시                                          |
| --------------- | ------------------------------------ | --------------------------------------------- |
| **기본 스트림** | 독립적 존재, 데이터 원본과 직접 연결 | `FileInputStream`, `FileOutputStream`         |
| **보조 스트림** | 기본 스트림에 연결, 추가 기능 제공   | `BufferedInputStream`, `BufferedOutputStream` |

### 성능 비교

```java
// 1. 직접 버퍼 사용 (최고 성능)
byte[] buffer = new byte[8192];
// 직접 버퍼 관리

// 2. 보조 스트림 사용 (편의성 우선)
BufferedInputStream bis = new BufferedInputStream(fis);

// 3. 한 번에 읽기 (작은 파일)
byte[] allData = fis.readAllBytes();
```

## 사용 가이드

- **작은 파일**: `readAllBytes()` / `writeAllBytes()` 사용
- **큰 파일 + 성능 중요**: 직접 버퍼 관리
- **편의성 우선**: 버퍼 보조 스트림 사용
