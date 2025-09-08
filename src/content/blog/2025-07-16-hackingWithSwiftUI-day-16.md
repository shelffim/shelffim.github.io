---
title: "Hacking with SwiftUI - Day 16"
pubDate: 2025-07-16
description: "SwiftUI 기초 학습 - Form, NavigationStack, @State, 양방향 바인딩을 활용한 WeSplit 체크 분할 앱 프로젝트 시작"
tags:
  [
    "SwiftUI",
    "iOS",
    "개발학습",
    "HackingWithSwift",
    "Form",
    "NavigationStack",
    "@State",
    "양방향바인딩",
    "ForEach",
    "WeSplit",
  ]
---

# Hacking with SwiftUI - Day 16

## 📋 프로젝트 개요

**WeSplit** - 체크 분할 앱을 만들어 SwiftUI의 기본 개념들을 학습합니다.

### 🎯 학습 목표

- Form과 NavigationStack 사용법
- @State를 통한 상태 관리
- 양방향 바인딩 이해
- 반복적인 뷰 생성

---

## 🏗️ 프로젝트 구조

### 기본 파일 구성

```
WeSplitApp.swift      - 앱 실행을 위한 진입점
ContentView.swift     - 메인 UI 구성
Assets.xcassets      - 앱 이미지 자산
Preview Assets.xcassets - 미리보기 이미지
```

---

## 🧩 핵심 컴포넌트

### 1. Form

- **용도**: 스크롤 가능한 컨트롤 목록 생성
- **포함 요소**: 텍스트 필드, 토글 스위치, 버튼 등
- **특징**: 정적 컨트롤과 사용자 상호작용 컨트롤 모두 지원

### 2. Section

- **용도**: Form을 논리적 섹션으로 분할
- **기능**: 각 섹션에 제목 추가 가능
- **장점**: 코드 구조화 및 가독성 향상

### 3. NavigationStack

- **용도**: Form을 감싸서 네비게이션 영역 생성
- **주요 메서드**:
  - `navigationTitle()`: 타이틀 설정
  - `navigationBarTitleDisplayMode(.inline)`: 작은 타이틀 모드

### 4. Button

```swift
Button() {
    // 버튼 클릭 시 실행할 동작
} label: {
    // 버튼에 표시될 라벨
}
```

### 5. Picker

- **용도**: 선택 목록 생성
- **기능**: 사용자가 선택할 수 있는 옵션 제공

---

## 🔄 상태 관리

### @State

- **목적**: UI 상태 저장 및 관리
- **특징**: 값이 변경되면 자동으로 UI 업데이트
- **사용법**: `@State private var 변수명 = 초기값`

---

## 🔗 양방향 바인딩

### 문제 상황

```swift
struct ContentView: View {
    @State private var name = ""

    var body: some View {
        Form {
            TextField("Enter your name", text: name)  // ❌ 컴파일 에러
            Text("Hello, world!")
        }
    }
}
```

### 문제 원인

- TextField는 양방향 바인딩을 요구
- 단순히 `name` 값을 전달하는 것이 아니라 `$name`으로 바인딩 필요

### 해결 방법

```swift
TextField("Enter your name", text: $name)  // ✅ 올바른 바인딩
```

### 양방향 바인딩의 개념

- **정의**: UI와 상태 값이 서로 영향을 주고받는 관계
- **동작**: 사용자 입력 → 상태 변경 → UI 업데이트

---

## 🔁 반복적인 뷰 생성

### ForEach

- **용도**: 배열과 범위를 반복하여 동적으로 뷰 생성
- **필수 요소**: `id: \.self` - 각 항목을 고유하게 식별
- **장점**: 코드 중복 제거 및 유지보수성 향상

---

## 💡 핵심 포인트

1. **Form**은 다양한 컨트롤을 체계적으로 배치하는 컨테이너
2. **@State**는 UI 상태를 관리하는 핵심 도구
3. **양방향 바인딩**은 사용자 입력과 상태를 연결하는 필수 개념
4. **ForEach**는 반복적인 UI 요소를 효율적으로 생성
