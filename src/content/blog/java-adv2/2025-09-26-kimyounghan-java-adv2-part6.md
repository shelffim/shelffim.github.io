---
title: "File, Files"
pubDate: 2025-09-26
description: "김영한님의 자바 고급 2편 강의 part 6(File, Files) 학습 정리"
---

> **출처**: [김영한의 자바 고급 2편 강의](https://inf.run/8ES1C) - Section 6 : File, Files

## 파일 시스템 클래스들

### File vs Files vs Path

| 클래스    | 특징                         | 사용 시기                |
| --------- | ---------------------------- | ------------------------ |
| **File**  | 기본 파일/폴더 조작          | 간단한 작업              |
| **Files** | 향상된 성능, 유틸리티 메서드 | 복잡한 작업, 대규모 파일 |
| **Path**  | 경로 표현                    | Files와 함께 사용        |

## 경로 (Path)

### 절대 경로 vs 정규 경로

```java

Path path = Paths.of("temp/test.txt");
// 절대 경로: 루트부터 시작, 항상 동일한 대상
System.out.println(path.toAbsolutePath());

// 정규 경로: 계산 완료된 경로, 유일함
System.out.println(path.toRealPath());
```

## 파일 생성과 조작

### File 클래스

```java
// File 객체 생성 (파일이 만들어지지 않음)
File file = new File("test.txt");

// 실제 파일 생성
boolean created = file.createNewFile();

// 디렉토리 생성
File dir = new File("newFolder");
boolean dirCreated = dir.mkdir();
```

### Files 클래스 (권장)

```java
// 문자열 파일 쓰기/읽기
Files.writeString(Paths.of("data.txt"), "Hello World");
String content = Files.readString(Paths.of("data.txt"));

// 파일 복사 (빠른 시스템 레벨 복사)
Files.copy(Paths.of("source.txt"), Paths.of("dest.txt"), StandardCopyOption.REPLACE_EXISTING);
```

## 대용량 파일 처리

### 메모리 효율적인 읽기

```java
// ❌ 큰 파일에 부적합: 전체 파일을 메모리에 로드
List<String> lines = Files.readAllLines(Paths.of("large.txt"));

// ✅ 큰 파일에 적합: 스트림 방식으로 한 줄씩 처리
Files.lines(Paths.of("large.txt"))
    .forEach(line -> System.out.println(line));
```

## Files 유틸리티 메서드

### 주요 기능들

```java
// 파일 존재 확인
boolean exists = Files.exists(Paths.of("file.txt"));

// 파일 크기
long size = Files.size(Paths.of("file.txt"));

// 파일 삭제
Files.delete(Paths.of("file.txt"));

// 디렉토리 생성
Files.createDirectory(Paths.of("new/folder"));
```

**특징**: Files는 **정적 메서드**로 제공되어 인스턴스 생성 없이 사용
