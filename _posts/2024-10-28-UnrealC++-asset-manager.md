---
title: UnrealC++ - AssetManager
description: UnrealC++에서 어셋 매니저를 사용합니다.
date: 2024-10-28 19:05:00 +09:00
categories: [Unreal, C++]
tags: [C++, Unreal, AssetManager]
pin: true
math: true
mermaid: true
---

### 설명

- 싱글톤 클래스
- 엔진이 초기화될 때 제공되며, 애셋 정보를 요청해 받을 수 있음
- PrimaryAssetId를 사용해 프로젝트 내 애셋의 주소를 얻어올 수 있음
- PrimaryAssetId
    - 태그 + 이름
        - PrimaryAssetTag
        - PrimaryAssetName
        - 두 가지 키 조합으로 구성되어 있음
    - 특정 태그를 가진 모든 에셋 목록을 가져올 수 있음

### 설정

- ABItemData라는 에셋 태그를 지정
- ProjectSettings - AssetManager에서 해당 에셋들이 담긴 폴더를 지정

### 코드

```cpp
// ItemData
virtual FPrimaryAssetId GetPrimaryAssetId() const override
{
	return FPrimaryAssetId("ABItemData", GetFName());
}

// ItemBox
UAssetManager& Manager = UAssetManager::Get();

TArray<FPrimaryAssetId> Assets;
Manager.GetPrimaryAssetIdList(TEXT("ABItemData"), Assets);
ensure(0 < Assets.Num());

int32 RandomIndex = FMath::RandRange(0, Assets.Num() - 1);
FSoftObjectPtr AssetPtr(Manager.GetPrimaryAssetPath(Assets[RandomIndex]));
if (AssetPtr.IsPending())
{
	AssetPtr.LoadSynchronous();
}
Item = Cast<UABItemData>(AssetPtr.Get());
ensure(Item);
```