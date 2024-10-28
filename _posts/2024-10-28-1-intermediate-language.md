---
title: IL Intermediate Language
description: IL의 기본 개념을 정리합니다
author: kaygundraka
date: 2024-10-28 15:28:00 +0800
categories: [Programming, CSharp]
tags: [C#, CSharp, IL]
pin: true
math: true
mermaid: true
image:
  path: /commons/devices-mockup.png
  lqip: data:image/webp;base64,UklGRpoAAABXRUJQVlA4WAoAAAAQAAAADwAABwAAQUxQSDIAAAARL0AmbZurmr57yyIiqE8oiG0bejIYEQTgqiDA9vqnsUSI6H+oAERp2HZ65qP/VIAWAFZQOCBCAAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
  alt: Responsive rendering of Chirpy theme on multiple devices.
---

## IL : Intermediate Language

- Common Intermediate Language라고도 불림
    - CPU와 OS에 독립적인 기계어 코드
    - 가상 머신(CLR : Common Language Runtime) 위에서 동작

- 실행 파일에서 IL 보기
  > ildasm Sample.exe /out Sample.txt

- il 빌드
  > ilasm File.il

## 기본 문법
```
.assembly foo {} // 어셈블리 매니페스트. foo는 임의 네임. 현재 어셈블리 정의
.assembly extern mscorlib {} // 외부에 있는 라이브러리 어셈블리 사용

// .method : 함수임을 알림
// static : 글로벌 함수임을 지정
// cil managed : 관성적으로 붙임
.method static void foo() cil managed
{
	.entrypoint // 프로그램의 시작점을 알림
	
	ldc.i4.1 // push 1 (ldc=stack, i4=32byte, 1=value)
	ldc.i4.2 // push 2
	call void goo(int32 a, int32 b) // 함수 호출. 반환 값 포함 전체 형식 작성 필요
	ret // 함수 끝에 적어야함
}

.method static void goo(int32 a, int32 b) cil managed
{
	// [mscorlib] 어셈블리에 있는 WrtieLine() 출력
	// 네임스페이스 공간은 .로
	// 클래스 공간은 ::로 표현
	// ldstr : 문자열 스택 공간. Load String
	// String이 클래스인지 Struct인지 모르기 때문에 명시 필요
	ldstr "Hello, IL"
	call void [mscorlib]System.Console::WriteLine(class System.String)
	
	ret
}

.method static void foo() cil managed
{
	// C# Code
	// int x = 2;
	// int y = 20;
	// Console.WriteLine("{0}, {1}", x, y);

	.locals init(int32 x, int32 y)
	
	idc.i4.2 // push 2
	stloc.0  // x = 2 : store local variable 0번째의 의미
	
	idc.i4.s 20 // push 20
	stloc.1     // y = 2 : store local variable 0번째의 의미
	
	ldstr "{0}, {1}"
	
	ldloc.0 // x : Load Local Variable
	box int32 // int32를 object 타입으로 Boxing 해야함
	
	ldloc.1 // y : Load Local Variable
	box int32
	
	call void [mscorlib]System.Console::WriteLine(class System.String, object, object)
	
	ret
}
```

## 클래스 기본 문법
```
.assembly foo {}
.assembly extern mscorlib {}

.class public Program
{
	.method public instance void foo() cil managed
	{
		ldstr "Hello, IL"
		call void [mscorlib]System.Console::WriteLine(string)
		ret
	}
	
	// specialname rtspecialname 특별한 함수임을 clr에 알림
	.method public specialname rtspecialname instance void .ctor() cil managed
	{
		// 기반 클래스 생성자 호출
		ldarg.0 // this : Load Arguments 0
		call instance void [mscorlib]System.Object::.ctor()
		ret
	}
	
	.method public static void Main() cil managed
	{
		.entrypoint
		
		// Program p = new Program()
		.locals init(class Program V_0)
		
		// newobj : 메모리에 새 객체 생성
		// instance void Program::.ctor() : 객채의 생성자 호출
		newobj instance void Program::.ctor()
		stloc.0
		
		ldloc.0
		callvirt instance void Program::foo()
		ret
	}
}
```