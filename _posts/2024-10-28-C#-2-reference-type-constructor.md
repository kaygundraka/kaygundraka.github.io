---
title: ReferenceType Constructor
description: ReferenceType Constructor 개념을 정리합니다
author: kaygundraka
date: 2024-10-28 10:28:00 +0900
categories: [Programming, CSharp]
tags: [C#, CSharp]
pin: true
math: true
mermaid: true
---

# ReferenceType Constructor

### ReferenceType = class

- 객체가 생성되면
  - 메모리가 먼저 초기화
  - 이후에 생성자가 불린다

- 작성한 생성자가 없다면
    - 클래스 타입에 따라
        - class
            - 컴파일러가 매개변수가 없는 .ctor() 생성
        - abstract class
            - protected (family) 생성자
        - static class
            - 생성자가 제공되지 않음
- 상속
    - 호출 : 부모 클래스의 생성자 → 파생 클래스의 생성자
        - IL로 확인하면 파생 클래스의 생성자에서 부모 클래스의 생성자를 부른다
        - 기본적으로 인자가 없는 생성자가 호출된다
    - 생성자를 protected에 놓으면
        - 파생 클래스는 객체 생성 가능 (추상적 존재)
        - 부모 클래스는 객체 생성 불가능 (구채적 존재)
    - 필드 초기화의 원리
        
        ```csharp
        class Derived : Base
        {
        	int a = 10;
        	int b;
        	
        	public Derived()
        	{
        		// a = 10
        		// Base()
        		b = 10;
        	}
        } 
        ```
        
        - 동작
            - 필드 초기화
            - 기반 클래스의 생성자
            - 생성자 안에 있는 초기화 코드
        - 주의
            - C++에서는 기반 클래스의 생성자에서 가상 함수가 동작하지 않지만 c#에서는 동작한다
            - 생성자 안에서는 가상 함수를 가능한 사용하지 않는다