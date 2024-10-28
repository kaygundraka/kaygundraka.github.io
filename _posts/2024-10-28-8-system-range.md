---
title: System Range
description: System Range의 개념을 정리합니다
author: kaygundraka
date: 2024-10-28 15:28:00 +0800
categories: [Programming, CSharp]
tags: [C#, CSharp]
pin: true
math: true
mermaid: true
image:
  path: /commons/devices-mockup.png
  lqip: data:image/webp;base64,UklGRpoAAABXRUJQVlA4WAoAAAAQAAAADwAABwAAQUxQSDIAAAARL0AmbZurmr57yyIiqE8oiG0bejIYEQTgqiDA9vqnsUSI6H+oAERp2HZ65qP/VIAWAFZQOCBCAAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
  alt: Responsive rendering of Chirpy theme on multiple devices.
---

# System.Range

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