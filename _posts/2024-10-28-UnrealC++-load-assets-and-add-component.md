---
title: UnrealC++ - Load Assets And Add Component
description: UnrealC++에서 어셋을 로딩하고 컴포넌트를 추가합니다.
date: 2024-10-28 19:03:00 +09:00
categories: [Unreal, C++]
tags: [C++, Unreal, Assets, Component]
pin: true
math: true
mermaid: true
---

## 어셋 로딩
---

`ConstructorHelpers`  : 생성자에서 특정 어셋을 레퍼런싱하기 위해 사용한다

```cpp
// Class : Static한 데이터의 경우
static ConstructorHelpers::FClassFinder<APawn> DefaultPawnClassRef(TEXT("/Script/ArenaBattle.ABCharacterPlayer"));
if (DefaultPawnClassRef.Class)
{
	DefaultPawnClass = DefaultPawnClassRef.Class;
}

// Ref를 카피할 때, 블루 프린트로 형변환 하는게 아니라면 '' 구문을 제거하고 뒤에 _C를 붙여야함

// Object : 인스턴스화 되어 있는 경우
static ConstructorHelpers::FObjectFinder<USkeletalMesh> CharacterMeshRef(TEXT("/Script/Engine.SkeletalMesh'/Game/Characters/Mannequins/Meshes/SKM_Quinn_Simple.SKM_Quinn_Simple'"));
if (CharacterMeshRef.Object)
{
	mesh->SetSkeletalMesh(CharacterMeshRef.Object);
}
```

## 컴포넌트 추가
---

### 액터

- 액터에 부착할 수 있는 컴포넌트 중 트랜스폼이 없는 컴포넌트
- 액터의 기능을 확장할 때 컴포넌트로 분리해 모듈화할 수 있음

Header

```cpp
UPROPERTY(VisibleAnywhere, BlueprintReadWrite, Category=Mesh)
TObjectPtr<class UStaticMeshComponent> Body;
```

CPP

```cpp
Body = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("Body"));
```