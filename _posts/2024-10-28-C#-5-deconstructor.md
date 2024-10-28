---
title: Deconstructor
description: Deconstructor의 개념을 정리합니다
date: 2024-10-28 13:28:00 +09:00
categories: [Programming, CSharp]
tags: [C#, CSharp]
pin: true
math: true
mermaid: true
---

```csharp
public class Test
{
	public int x;
	public int y;
	
	public Test(int x, int y)
	{
		this.x = x;
		this.y = y;
	}
	
	public void Deconstructor(out int a, out int b)
	{
		a = this.x;
		b = this.y;
	}
}

public class Program
{
	public static void Main()
	{
		Test test = new Test(1, 2);

		// test.Deconstructor(out int a, out int b);
		var (a, b) = test;
		Console.WriteLine($"{0}, {1}", a, b);
		// Output : 1, 2		
	}
}
```

- 객체의 필드 값을 꺼낼때 사용
- 반환된 결과는 Tuple로 반환
- 소멸자와 혼동하지 않도록 주의
- C# 7.0부터 사용 가능