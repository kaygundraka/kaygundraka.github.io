---
title: UnrealC++ - Use CSV File
description: UnrealC++에서 CSV File을 사용합니다.
date: 2024-10-28 19:07:00 +09:00
categories: [Unreal, C++]
tags: [C++, Unreal, AssetManager]
pin: true
math: true
mermaid: true
---

### 설명

- DataAsset과 유사하게 FTableRowBase를 상속받은 구조체를 선언
- 엑셀의 Name 컬럼을 제외한 컬럼과 동일하게 UPROPERTY 속성을 선언
    - Name이 항상 필요 (키)
- 엑셀 데이터를 csv로 익스포트한 후 언리얼엔진에 임포트

### 설정

- 언리얼 프로젝트에 폴더를 만들어서 csv파일 넣기
    - ex: GameData/Items.csv
- 임의 struct를 만들어서 csv 컬럼과 맞추기

```cpp
#pragma once

#include "CoreMinimal.h"
#include "Engine/DataTable.h"
#include "ABCharacterStat.generated.h"

USTRUCT(BlueprintType)
struct FABCharacterStat : public FTableRowBase
{
	GENERATED_BODY();

public:
	FABCharacterStat() {}

	UPROPERTY(EditAnywhere, BlueprintReadOnly, Category=Stat)
	float MaxHp;
};
```