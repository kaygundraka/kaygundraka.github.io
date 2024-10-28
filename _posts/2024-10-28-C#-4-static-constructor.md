---
title: Static Constructor
description: Static Constructor의 개념을 정리합니다
author: kaygundraka
date: 2024-10-28 12:28:00 +0800
categories: [Programming, CSharp]
tags: [C#, CSharp]
pin: true
math: true
mermaid: true
---

# Static Constructor

### 타입 생성자라고도 불린다

```csharp
class Point
{
	int x;
	int y;
	static int cnt;
	
	public Point(int x, int y)
	{
		this.x = x;
		this.y = y;
	}
	
	static Point()
	{
		cnt = 0;
	}
}
```

- 타입 생성자
    - static 멤버를 한번만 초기화하는 것을 보장한다
    - 생성자 앞에 static을 붙인다
    - 접근 지정자를 붙이지 않는다 (컴파일러가 자동적으로 private을 붙인다)
    - 인자 없는 생성자만 만들 수 있다

- 호출 규약
    - 객체 생성 혹은 정적 멤버에 접근하는 코드가 있을 때 호출
    - static 생성자가 호출되고 instance 생성자가 호출
    - 여러 객체를 만들어도 한개만 호출
    - thread-safe
    - 여러 타입 생성자가 서로를 상호 참조하면 안됨