---
title: System Range
description: System Range의 개념을 정리합니다
date: 2024-10-28 16:28:00 +09:00
categories: [Programming, CSharp]
tags: [C#, CSharp]
pin: true
math: true
mermaid: true
---

## 배열 범위 접근

```csharp
string str = "ABCDEFGHIJ";

// Includ:2, Exclude:7
var t1 = str[2..7];  // CDEFG
var t2 = str[2..^3]; // CDEFG
```

## System.Range 사용

```csharp
int[] arr = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };

var r1 = new Range(); // Empty
var r2 = new Range(new Index(2), new Index(2, fromEnd:2)); // 3, 4, 5, 6, 7, 8
var r3 = new Range(2, ^2);
Range r4 = 2..^2;
```

## 다양한 사용법
```csharp
int[] arr = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };

// 정적 메소드로 만들기
var r1 = Range.All;
var r2 = Range.StartAt(2);
var r3 = Range.EndAt(2);

// 단축 표기법
var r4 = 2..7;
var r5 = 2..^2;
var r6 = ..2;
var r7 = 2..;
```