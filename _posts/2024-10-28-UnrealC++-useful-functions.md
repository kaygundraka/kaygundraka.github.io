---
title: UnrealC++ - Useful Functions
description: UnrealC++의 편의 기능 정리
date: 2024-10-28 19:09:00 +09:00
categories: [Unreal, C++]
tags: [C++, Unreal]
pin: true
math: true
mermaid: true
---

### 형변환

```cpp
Cast<Type>(Value)

// 체크까지 같이 진행
CastChecked<Type>(Value)
```

### 항시 존재

```cpp
checked(value)
```

### 런타임 조건 체크

```jsx
ensure(CurrentCombo != 0);
```

### PIE 중 특정 클래스의 프로퍼티 값 보기

- DisplayAll ClassName PropertyName

### 디버그 물체 그리기

```cpp
#if ENABLE_DRAW_DEBUG

	FVector CapsuleOrigin = Start + (End - Start) * 0.5f;
	float CapsuleHalfHeight = AttackRange * 0.5f;
	FColor DrawColor = HitDetected ? FColor::Green : FColor::Red;

	DrawDebugCapsule(GetWorld(), CapsuleOrigin, CapsuleHalfHeight, AttackRadius, FRotationMatrix::MakeFromZ(GetActorForwardVector()).ToQuat(), DrawColor, false, 5.0f);
	
#endif
```

### Float 작은 수 비교

```cpp
KINDA_SMALL_NUMBER
```

### 에디터 변경 사항 테스트

- 에디터에서 개체의 값을 변경하면 OnConstruction()이 불림