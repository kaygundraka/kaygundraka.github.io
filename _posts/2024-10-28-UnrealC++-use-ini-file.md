---
title: UnrealC++ - Use INI File
description: UnrealC++에서 INI File을 사용합니다.
date: 2024-10-28 19:08:00 +09:00
categories: [Unreal, C++]
tags: [C++, Unreal, AssetManager]
pin: true
math: true
mermaid: true
---

### 방법

- 프로젝트 폴더 - Config - DefaultAreanBattle.ini 추가

```cpp
[/Script/ArenaBattle.ABCharacterNonPlayer]
+NPCMeshes=/Game/InfinityBladeWarriors/Character/CompleteCharacters/SK_CharM_Barbarous.SK_CharM_Barbarous
+NPCMeshes=/Game/InfinityBladeWarriors/Character/CompleteCharacters/sk_CharM_Base.sk_CharM_Base
+NPCMeshes=/Game/InfinityBladeWarriors/Character/CompleteCharacters/SK_CharM_Bladed.SK_CharM_Bladed
+NPCMeshes=/Game/InfinityBladeWarriors/Character/CompleteCharacters/SK_CharM_Cardboard.SK_CharM_Cardboard
+NPCMeshes=/Game/InfinityBladeWarriors/Character/CompleteCharacters/SK_CharM_Forge.SK_CharM_Forge
+NPCMeshes=/Game/InfinityBladeWarriors/Character/CompleteCharacters/SK_CharM_FrostGiant.SK_CharM_FrostGiant
+NPCMeshes=/Game/InfinityBladeWarriors/Character/CompleteCharacters/SK_CharM_Golden.SK_CharM_Golden
+NPCMeshes=/Game/InfinityBladeWarriors/Character/CompleteCharacters/SK_CharM_Natural.SK_CharM_Natural
+NPCMeshes=/Game/InfinityBladeWarriors/Character/CompleteCharacters/SK_CharM_Pit.SK_CharM_Pit
+NPCMeshes=/Game/InfinityBladeWarriors/Character/CompleteCharacters/SK_CharM_Ragged0.SK_CharM_Ragged0
+NPCMeshes=/Game/InfinityBladeWarriors/Character/CompleteCharacters/SK_CharM_RaggedElite.SK_CharM_RaggedElite
+NPCMeshes=/Game/InfinityBladeWarriors/Character/CompleteCharacters/SK_CharM_Ram.SK_CharM_Ram
+NPCMeshes=/Game/InfinityBladeWarriors/Character/CompleteCharacters/SK_CharM_Robo.SK_CharM_Robo
+NPCMeshes=/Game/InfinityBladeWarriors/Character/CompleteCharacters/SK_CharM_Shell.SK_CharM_Shell
+NPCMeshes=/Game/InfinityBladeWarriors/Character/CompleteCharacters/SK_CharM_solid.SK_CharM_solid
+NPCMeshes=/Game/InfinityBladeWarriors/Character/CompleteCharacters/SK_CharM_Standard.SK_CharM_Standard
+NPCMeshes=/Game/InfinityBladeWarriors/Character/CompleteCharacters/SK_CharM_Tusk.SK_CharM_Tusk
+NPCMeshes=/Game/InfinityBladeWarriors/Character/CompleteCharacters/SK_CharM_Warrior.SK_CharM_Warrior
```

- 클래스 헤더에 멤버 선언

```cpp
UCLASS(config=ArenaBattle)
class ARENABATTLE_API AABCharacterNonPlayer : public AABCharacterBase
{
	GENERATED_BODY()

public:
	UPROPERTY(config)
	TArray<FSoftObjectPath> NPCMeshes;
};

```

- 왜 굳이 이렇게 하는지를 아직 모르겠음
    - 쓰는 이유를 찾아보자
    - https://reitbe.github.io/unrealengine5/2024/04/04/unreal-ini-file-manual.html