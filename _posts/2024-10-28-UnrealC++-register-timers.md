---
title: UnrealC++ - Register Timers
description: UnrealC++에서 타이머를 등록합니다.
date: 2024-10-28 19:02:00 +09:00
categories: [Unreal, C++]
tags: [C++, Unreal, Timer]
pin: true
math: true
mermaid: true
---

### 핸들 선언

```cpp
FTimerHandle ComboTimerHandle;
```

### 타이머 등록

```cpp
GetWorld()->GetTimerManager().SetTimer(ComboTimerHandle, this, &AABCharacterBase::ComboCheck, ComboEffectiveTime, false);	
```

### 타이머 해제

```cpp
ComboTimerHandle.Invalidate();
```

### 타이머 람다 등록 예시

```cpp
FTimerHandle DeadTimerHandle;
	GetWorld()->GetTimerManager().SetTimer(DeadTimerHandle, FTimerDelegate::CreateLambda([&]()
	{
		Destroy();	
	}
	), DeadEventDelayTime, false);
```