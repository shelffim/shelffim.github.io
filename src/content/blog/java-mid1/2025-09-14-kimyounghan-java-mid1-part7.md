---
title: "김영한의 자바 중급 1편 강의 - part 7: 날짜와 시간"
pubDate: 2025-09-14
description: "김영한님의 자바 중급 1편 강의 part 7(날짜와 시간) 학습 정리"
---

> **출처**: [김영한의 자바 중급 1편 강의](https://inf.run/XGzSo) - Section 7: 날짜와 시간

## 📅 날짜와 시간 라이브러리가 필요한 이유

1. **날짜와 시간 차이 계산**
2. **윤년 계산**
3. **일광 절약 시간 변환**
4. **타임존 계산**

> 💡 **중요**: 모든 날짜 클래스는 불변이다. 변경이 필요한 경우 새로운 객체를 생성해서 반환하므로 반환값을 꼭 받아야 한다.

> ⚠️ **주의**: `LocalDate`, `LocalTime`, `LocalDateTime`은 세계 시간대를 고려하지 않아서 타임존이 적용되지 않는다. 특정 지역의 날짜와 시간만 고려할 때 사용한다.

## 🗓️ LocalDate

### 생성 방법

- `now()`: 현재 시간을 기준으로 생성
- `of()`: 특정 날짜를 기준으로 생성, 년, 월, 일을 입력받아 생성

### 계산 방법

- `plusDays()`: 일 추가
- 다양한 `plusXXX()`: 다양한 단위 추가

## ⏰ LocalTime

### 생성 방법

- `now()`: 현재 시간을 기준으로 생성
- `of()`: 특정 시간을 기준으로 생성, 시, 분, 초를 입력받아 생성

### 계산 방법

- `plusSeconds()`: 초 추가
- 다양한 `plusXXX()`: 다양한 단위 추가

## 📆 LocalDateTime

### 생성 방법

- `now()`: 현재 날짜와 시간을 기준으로 생성
- `of()`: 특정 날짜와 시간을 기준으로 생성

### 분리 방법

- `toLocalDate()`: 날짜 분리
- `toLocalTime()`: 시간 분리

### 합체 방법

- `LocalDateTime.of(localDate, localTime)`: 날짜와 시간을 합친다.

### 계산 방법

- 다양한 `plusXXX()`: 특정 날짜와 시간을 더한다.

### 비교 방법

- `isBefore()`: 현재 날짜와 시간이 이전이라면 true를 반환한다.
- `isAfter()`: 현재 날짜와 시간이 이후라면 true를 반환한다.
- `isEqual()`: 현재 날짜와 시간이 같다면 true를 반환한다.

## 🌍 ZonedDateTime

`ZonedDateTime`은 타임존을 고려하여 날짜와 시간을 계산할 때 사용한다. 시간대를 고려해야 할 때 실제 사용하는 날짜와 시간 정보를 나타내는 데 적합하다. 구체적인 지역 시간대를 다룰 때 사용하며, 일광 절약 시간을 자동으로 처리할 수 있다.

### ZoneId

- 자바는 타임존을 `ZoneId` 클래스로 제공한다.

#### 생성 방법

- `ZoneId.systemDefault()`: 시스템 기본 타임존을 반환한다.
- `ZoneId.of(String zoneId)`: 특정 타임존을 반환한다.

### ZonedDateTime

#### 생성 방법

- `now()`: 현재 날짜와 시간을 기준으로 생성, ZoneId는 현재 시스템을 따른다.
- `of()`: 특정 날짜와 시간을 기준으로 생성, ZoneId를 추가해야 한다. LocalDateTime에 ZoneId를 추가해서 생성할 수 있다.

#### 타임존 변경 방법

- `withZoneSameInstant(ZoneId zoneId)`: 타임존을 변경한다. 타임존에 맞추어 시간도 변경된다.

## ⏱️ OffsetDateTime

`OffsetDateTime`은 타임존은 없고 고정된 오프셋만 포함한다. UTC로부터의 고정된 오프셋을 나타내는 데 적합하다. ZoneId가 없으므로 일광 절약 시간제가 적용되지 않는다. 지역 시간대의 복잡성을 고려하지 않는다.

### 생성 방법

- `now()`: 현재 날짜와 시간을 기준으로 생성
- `of()`: 특정 날짜와 시간을 기준으로 생성, ZoneOffset을 추가해야 한다.

## ⚡ Instant

`Instant`는 UTC를 기준으로 하는, 시간의 한 지점을 나타낸다. 날짜와 시간을 나노초 정밀도로 표현한다. Epoch 시간을 다루는 클래스이다. 전세계적인 시간 기준이 필요하거나 시간대 변환 없이 시간 계산이 필요하거나 데이터 저장 및 교환 할 때 사용한다.

### 장점

- **시간대 독립성**: 시간대에 영향을 받지 않아 어디서나 동일한 시점을 가리키는데 유용하다.
- **고정된 기준점**: UTC를 기준으로 하기 때문에, 시간 계산 및 비교가 명확하고 일관된다.

### 단점

- **사용자 친화적이지 않다**
- **시간대 정보 부재**: 시간대 정보가 없기 때문에 특정 지역의 날짜와 시간으로 변환하려면 추가적인 작업이 필요하다.

### 생성 방법

- `now()`: UTC를 기준 현재 시간의 Instant를 생성
- `from()`: 다른 타입의 날짜와 시간을 기준으로 Instant를 생성
- `ofEpochSecond(long epochSecond)`: Epoch 시간을 기준으로 Instant를 생성, 0초를 선택하면 1970년 1월 1일 0시 0분 0초를 의미한다.

### 계산 방법

- `plusSeconds()`: 초 추가
- 다양한 `plusXXX()`: 다양한 단위 추가

### 조회 방법

- `getEpochSecond()`: Epoch 시간을 기준으로 흐른 초를 반환한다.

## 📊 Period

`Period`는 두 날짜 사이의 간격을 년, 월, 일 단위로 나타낸다.

### 주요 메서드

- `getYears()`, `getMonths()`, `getDays()`

### 생성 방식

- `of(년, 월, 일)`: 특정 기간을 지정해서 Period를 생성
- `ofDays()`, `ofMonths()`, `ofYears()`

### 기간 차이

- `Period.between(startDate, endDate)`: 두 날짜 사이의 기간을 반환한다.

## ⏳ Duration

`Duration`은 두 시간 사이의 간격을 시, 분, 초(나노초) 단위로 나타낸다.

### 주요 메서드

- `toHours()`, `toMinutes()`, `getSeconds()`, `getNano()`

### 생성 방법

- `of()`: 특정 시간을 지정해서 Duration을 생성
  - `ofSeconds()`, `ofMinutes()`, `ofHours()`

### 시간 차이

- `Duration.between(startDate, endDate)`: 두 시간 사이의 시간을 반환한다.

## 🔧 ChronoField & ChronoUnit

### ChronoField

날짜와 시간의 필드를 조회하려면 `ChronoField`를 사용한다. 날짜와 시간의 필드는 열거형으로 정의되어 있다.

### ChronoUnit

날짜와 시간을 조작하려면 `ChronoUnit`을 사용한다. 날짜와 시간을 조작하는 단위는 열거형으로 정의되어 있다.

## 📝 포맷팅 & 파싱

### 포맷팅

날짜와 시간 데이터를 원하는 포멧의 문자열로 변경하는 것

- `DateTimeFormatter` 클래스를 사용해서 `ofPattern()` 메서드를 사용해서 포멧을 지정할 수 있다.

### 파싱

문자열을 날짜와 시간 데이터로 변경하는 것

- `DateTimeFormatter` 클래스를 사용해서 `parse(Date, formatter)` 메서드를 사용해서 파싱할 수 있다.
