---
title: UnrealC++ - Delcare Member
description: UnrealC++에서 멤버를 선언하는 방법을 학습합니다
date: 2024-10-28 18:40:00 +09:00
categories: [Unreal, C++]
tags: [C++, Unreal]
pin: true
math: true
mermaid: true
---

# 멤버 선언
---

## 레퍼런스
---

```cpp
// 레퍼런스이기 때문에 보일 위치를 설정함
UPROPERTY(VisibleAnywhere, BlueprintReadOnly, Category=Character)

// UObject로 관리되는 개체는 항상 TObjectPtr로 관리한다
TObjectPtr<class UCharacterMovementComponent> Movement;

// AABCharacterNonPlayer를 상속받은 클래스만 지정 가능
// TObjectPtr은 모든 Actor가 나옴. 이게 편함.
TSubclassOf<class AABCharacterNonPlayer> OpponentClass;

// 약참조. 생명주기를 같이하지 않는 경우 사용
TWeakObjectPtr<class AABItemBox>
```

## 값
---

```cpp
// 값이기 때문에 설정 가능한 위치를 설정함
UPROPERTY(EditAnywhere, BlueprintReadOnly, Category=Character)
```

- VisibleInstanceOnly : 객체 별 값이 다르게 설정
- Transient : 디스크에 저장하지 않음 (휘발성 값)

## 에디터에서 접근하지 않는 경우
---

```cpp
int32 TestCount; // 이런식으로 바로 선언해서 사용하면 됨
```

## 인라인 함수
---

```cpp
// 인라인 함수
FORCEINLINE float GetMaxHp() { return MaxHp; }
```

## 델리게이트
---

- 전방 선언

```cpp
DECLARE_MULTICAST_DELEGATE(FOnChangeHPDelegate) // 파라미터가 없는 델리게이트 선언
DECLARE_MULTICAST_DELEGATE_OneParam(FOnChangeHPDelegate, float /*CurrentHp*/) // 파라미터가 있는 델리게이트 선언
```

- 프로퍼티 선언

```cpp
FOnChangedHPDelegate OnHpChanged;
```

- 등록

```cpp
Stat->OnHpChanged.AddUObject(HpBarWidget, &UABHpBarWidget::UpdateHpBar);
```

- 호출

```cpp
OnHpChanged.Broadcast(CurrentHp);
```

## 함수
---

```cpp
UFUNCTION() // 이거 찾아서 정리 필요
```

## Enum
---

```cpp
UENUM(BlueprintType)
enum class EItemType : uint8
{
	Weapon = 0,
	Potion,
	Scroll
};	
```