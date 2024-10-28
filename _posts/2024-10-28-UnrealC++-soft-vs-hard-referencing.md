---
title: UnrealC++ - Soft vs Hard Referencing
description: UnrealC++에서 레퍼런스를 선언/사용하는 방식을 설명합니다.
date: 2024-10-28 18:45:00 +09:00
categories: [Unreal, C++]
tags: [C++, Unreal]
pin: true
math: true
mermaid: true
---

## 하드 레퍼런싱
---

- 액터 로딩시 TObjectPtr로 선언한 언리얼 오브젝트도 메모리에 로딩됨

## 소프트 레퍼런싱
---

- 게임 진행에 필수적인 언리얼 오브젝트는 이렇게 선언해도 되지만 아이템의 경우는?
- 데이터 라이브러리에 1000종의 아이템 목록이 있을때, 이를 모두 다 로딩할 것인가?
- 이때 소프트 레퍼런싱을 사용
    - TSoftObjectPtr로 선언하고 대신 에셋 주소 문자열을 지정
    - 필요시 에셋 로딩이 가능하도록 구현을 변경할 수 있으나 애셋 로딩 시간이 소요됨

## 소프트 레퍼런싱 예시
---

```cpp
// 선언
TSoftObjectPtr<USkeletalMesh> WeaponMesh;

// 사용
UABWeaponItemData* WeaponItemData = Cast<UABWeaponItemData>(InItemData);
	
if (InItemData)
{
	if (WeaponItemData->WeaponMesh.IsPending())
	{
		WeaponItemData->WeaponMesh.LoadSynchronous();
	}

	Weapon->SetSkeletalMesh(WeaponItemData->WeaponMesh.Get());
}
```

### 현재 게임에 로딩 되어 있는 스켈레탈 메시 목록을 살펴보기

- Obj List Class=SkeletalMesh