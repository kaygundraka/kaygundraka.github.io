---
title: Optional Parameter
description: Optional Parameter의 개념을 정리합니다
author: kaygundraka
date: 2024-10-28 14:28:00 +0900
categories: [Programming, CSharp]
tags: [C#, CSharp]
pin: true
math: true
mermaid: true
---

## 상속 관계에서의 주의점

```csharp
class Base
{
	public virtual void Foo(int a = 10)
	{
		Console.WriteLine("Base = {0}", a);
	}
}

class Derived : Base
{
	public override void Foo(int a = 20)
	{
		Console.WriteLine("Derived = {0}", a);
	}
}

class Program
{
	public static void Main()
	{
		Base b = new Derived();
		b.Foo(); // Derived = 10 출력됨
	}
}
```

- 옵셔널 파라미터가 설정되는 시간은 컴파일 타임이다
- 객체의 가상 함수를 호출하는 시점은 런타임이다
- 위의 두 차이로 인해서 Dervied 클래스의 가상 함수가 호출되지만, 옵셔널 파라미터의 값은 Base 것을 사용한다

## 값 타입에서의 주의점

```csharp
struct SPoint
{
	public SPoint(int a = 10, int b = 10)
	{
		Console.WriteLine("a = {0}, b = {1}", a, b);
	}
}

class Program
{
	public static void Main()
	{
		SPoint sp1 = new SPoint(5, 5); // a = 5, b = 5
		SPoint sp2 = new SPoint(10);   // a = 10, b = 5
		SPoint sp3 = new SPoint();     // a = 0, b = 0
	}
}
```

- 해석
    - SPoint(5, 5), SPoint(10)은 생성자가 불린다 → IL : call
    - SPoint()는 메모리만 잡고 초기화한다 → IL : initobj
- Struct에서는 되도록 사용하지 않는 것이 좋겠다