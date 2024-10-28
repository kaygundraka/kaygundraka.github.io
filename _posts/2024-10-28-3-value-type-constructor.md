---
title: ValueType Constructor
description: ValueType Constructor의 개념을 정리합니다
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

# ValueType Constructor

### ValueType = struct

- ReferenceType과의 차이점
    - class
        - 기본 생성자를 작성하지 않으면 컴파일러가 기본 생성자를 만들어준다
        - 커스텀 생성자가 있으면 컴파일러는 기본 생성자를 만들지 않는다
    - struct
        - 사용자는 기본 생성자를 정의할 수 없다
        - 컴파일러는 기본 생성자를 만들어주지 않는다
        - > CLR : “값 타입의 객체는 언제라도 생성 (생성자가 없이도) 할 수 있다. ”
    - C#만의 제약임
        - IL이나 .net 언어에서는 값 타입도 인자 없는 생성자를 만들 수 있음

- 생성자 호출과 IL
    - clsss
        - > newobj instance void CPoint::.ctor(int32, int32)
    - struct
        - > call instance void SPoint::.ctor(int32, int32)
        - > initobj SPoint

### 주의 사항

1. 값 타입 생성자는 필드 초기화를 할 수가 없다
    - 인자 없는 생성자를 만들 수 없기 때문
2. 멤버가 초기화 되는 경우
    
    ```csharp
    // 멤버가 초기화되지 않음
    SPoint sp1;
    
    // initobj가 불리면서 모든 멤버가 0으로 초기화됨
    SPoint sp2 = new SPoint();
    ```
    
3. 값 타입의 생성자에서는 모든 멤버의 초기값을 제공해야한다