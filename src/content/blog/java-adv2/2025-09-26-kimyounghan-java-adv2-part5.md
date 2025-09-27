---
title: "I/O 활용"
pubDate: 2025-09-26
description: "김영한님의 자바 고급 2편 강의 part 5(I/O 활용) 학습 정리"
---

> **출처**: [김영한의 자바 고급 2편 강의](https://inf.run/8ES1C) - Section 5 : I/O 활용

## 데이터 저장 방식

### 메모리 vs 파일 저장

| 저장 방식       | 특징             | 문제점                                |
| --------------- | ---------------- | ------------------------------------- |
| **메모리 저장** | 빠른 접근 속도   | 프로그램 종료 시 데이터 소실 (휘발성) |
| **파일 저장**   | 데이터 영구 보존 | 상대적으로 느린 접근 속도             |

## 자원 관리

### try-with-resources

**자동 자원 정리**를 위한 구문

```java
// 자동으로 close() 호출
try (FileWriter writer = new FileWriter("data.txt")) {
    writer.write("데이터 저장");
} // 자동으로 자원 해제
```

## 데이터 저장 방법 비교

### 1. 텍스트 파일 저장

```java
// 저장: 구분자 사용
FileWriter writer = new FileWriter("data.txt");
writer.write("이름,나이,직업\n");
writer.write("김철수,30,개발자\n");

// 읽기: 수동 파싱 필요
BufferedReader reader = new BufferedReader(new FileReader("data.txt"));
String line = reader.readLine();
String[] parts = line.split(",");  // 수동으로 구분자 처리
```

### 2. DataStream 사용

```java
// 저장: 타입별 저장
DataOutputStream dos = new DataOutputStream(new FileOutputStream("data.dat"));
dos.writeUTF("김철수");  // String
dos.writeInt(30);        // int

// 읽기: 타입별 자동 읽기
DataInputStream dis = new DataInputStream(new FileInputStream("data.dat"));
String name = dis.readUTF();  // 자동으로 String 읽기
int age = dis.readInt();      // 자동으로 int 읽기
```

### 3. Object Serialization (권장하지 않음)

```java
// 객체 직렬화 (문제점 많음)
ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("object.dat"));
oos.writeObject(person);  // 객체 저장

ObjectInputStream ois = new ObjectInputStream(new FileInputStream("object.dat"));
Person restored = (Person) ois.readObject();  // 객체 복원
```

**문제점**: 버전 관리 어려움, 플랫폼 종속성, 성능 이슈

## 현대적 데이터 저장

### JSON (권장)

```java
// JSON 저장 (가볍고 읽기 쉬움)
String json = """
    {
        "name": "김철수",
        "age": 30,
        "job": "개발자"
    }
    """;

FileWriter writer = new FileWriter("data.json");
writer.write(json);
```

**장점**: 가볍고 간결, 사람이 읽기 쉬움, 플랫폼 독립적

### 데이터베이스 (대규모 데이터)

직접 파일 I/O의 한계:

- 데이터 무결성 문제
- 검색 속도 저하
- 보안 취약점
- 백업 복잡성

**해결책**: 데이터베이스 사용으로 효율적 데이터 관리
