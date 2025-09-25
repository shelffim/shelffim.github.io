---
title: "I/O 기본 2"
pubDate: 2025-09-25
description: "김영한님의 자바 고급 2편 강의 part 4(I/O 기본 2) 학습 정리"
---

> **출처**: [김영한의 자바 고급 2편 강의](https://inf.run/8ES1C) - Section 4 : I/O 기본 2

## 문자 스트림 (Reader/Writer)

### 문자와 바이트의 차이

컴퓨터는 **이진 형태**로만 데이터를 저장하므로, 문자를 저장하려면 **바이트로 변환**해야 합니다.

```java
// 문자 → 바이트 변환
String text = "안녕하세요";
byte[] bytes = text.getBytes(StandardCharsets.UTF_8);  // 문자 집합 지정 필수

// 바이트 → 문자 변환
String decoded = new String(bytes, StandardCharsets.UTF_8);
```

### Reader/Writer의 장점

**인코딩/디코딩을 자동 처리**하여 문자 단위로 입출력 가능

## 편의 클래스들

### FileWriter/FileReader

내부적으로 `OutputStreamWriter`/`InputStreamReader`를 사용하는 **편의 클래스**

```java
// FileWriter 사용 (간단)
OutputStreamWriter writer = new OutputStreamWriter(new FileOutputStream("test.txt"), UTF_8)
writer.write("Hello World");
```

```java
// 문자 스트림 사용
FileWriter writer = new FileWriter("output.txt", UTF_8)
writer.write("안녕하세요");  // 자동으로 UTF-8 인코딩

FileReader reader = new FileReader("input.txt", UTF_8)
int data;
while ((data = reader.read()) != -1) {
    System.out.print((char) data);  // 자동으로 UTF-8 디코딩
}
```

### BufferedReader

**줄 단위 읽기**를 지원하는 버퍼 스트림

```java
BufferedReader reader = new BufferedReader(new FileReader("input.txt", UTF_8), 8192)
String line;
while ((line = reader.readLine()) != null) {  // 줄 단위로 읽기
    System.out.println(line);
}
```

### PrintStream

`System.out`에서 사용되는 스트림으로, **파일 출력**에도 활용 가능

```java
PrintStream ps = new PrintStream(new FileOutputStream("output.txt"))
ps.println("Hello World");  // print() 메서드들 사용 가능
ps.printf("숫자: %d", 42);
```

## 데이터 스트림

### DataOutputStream/DataInputStream

**기본 데이터 타입**을 바이트로 변환하여 저장/읽기

```java
// 데이터 저장
DataOutputStream dos = new DataOutputStream(new FileOutputStream("data.dat"))
dos.writeInt(42);           // int 타입 저장
dos.writeUTF("안녕");        // String 타입 저장
dos.writeBoolean(true);     // boolean 타입 저장

// 데이터 읽기
DataInputStream dis = new DataInputStream(new FileInputStream("data.dat"))
int number = dis.readInt();        // int 타입 읽기
String text = dis.readUTF();       // String 타입 읽기
boolean flag = dis.readBoolean();  // boolean 타입 읽기
```

## 스트림 계층 구조

### 기본 스트림 → 보조 스트림

| 계층            | 역할                    | 예시                                  |
| --------------- | ----------------------- | ------------------------------------- |
| **기본 스트림** | 데이터 원본과 직접 연결 | `FileOutputStream`, `FileInputStream` |
| **보조 스트림** | 추가 기능 제공          | `BufferedWriter`, `DataOutputStream`  |

```java
// 계층적 구성 예시
FileOutputStream fos = new FileOutputStream("file.txt");
BufferedOutputStream bos = new BufferedOutputStream(fos);
PrintStream ps = new PrintStream(bos);

ps.println("데이터");  // 최종 출력
```
