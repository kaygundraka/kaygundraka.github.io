---
title: System Index
description: System Index의 개념을 정리합니다
author: kaygundraka
date: 2024-10-28 15:28:00 +0900
categories: [Programming, CSharp]
tags: [C#, CSharp]
pin: true
math: true
mermaid: true
---

## 배열 역순 접근

```csharp
int[] arr = { 1, 2, 3, 4, 5 };

// 0부터 시작 0, 1, 2, 3, 4
int s = arr[2];

// 뒤에서 1부터 시작
int d = arr[^2];

Console.WriteLine($"{0}, {1}", s, d);
// Output : 3, 4
```

## System.Index 사용

```csharp
int[] arr = { 1, 2, 3, 4, 5 };

int s1 = arr[2];
Index si = new Index(2);
int s2 = arr[si];

int d1 = arr[1];
Index di = new Index(2, fromEnd: true);
int d2 = arr[di];
```

## System.Index 객체를 만드는 다양한 방법

```csharp
Index i1 = new Index(1);
Index i2 = new Index(1, fromEnd: true);

Index i3 = Index.FromStart(1);
Index i4 = Index.FreomEnd(1);

Index i5 = 1;
Index i6 = ^1;
```

## 사용자 정의 클래스와 System.Index
```csharp
public class Sentence
{
	public string str = "";
	
	public int Length = { get { return str.Length; }}
	public int Count = { get { return str.Length; }}
	
	public string this[int idx] { get { return str[idx]; }}
	public string this[Index index] { get { return str[idx]; }}
}

public class Program
{
	public static void Main()
	{
		var s = new Sentence();
		s.str = "Test";
		
		var c = s[^1];
		// IL이 시도해보는 것 (int형은 부르지 않는다)
		// 1. this[Index(1, fromEnd: true)
		// 2. s[s.Length - 1]
		// 3. S[s.Count - 1]
	}
}
```