---
title: UnrealC++ - Singleton Class
description: UnrealC++에서 싱글톤 클래스 사용법을 학습합니다
date: 2024-10-28 18:50:00 +09:00
categories: [Unreal, C++]
tags: [C++, Unreal, singleton]
pin: true
math: true
mermaid: true
---

# 싱글톤 클래스 등록
---

- 기본 제공 싱글톤 클래스
  - 게임 인스턴스
  - 애셋 매니저
  - 게임 플레이 관련 액터 (게임 모드, 게임 스테이트)
  - 프로젝트에 싱글톤으로 등록한 언리얼 오브젝트
    - ProjectSettings
      - Engine - General Settings
        - Default Class
          - Advanced

## 임의 싱글톤 만들기
---

- 언리얼 오브젝트 상속 받아서 만듬 : UObject
- Get() 함수는 직접 만들어야 함
    
```cpp
UABGameSingleton& UABGameSingleton::Get()
{
    UABGameSingleton* Singleton = CastChecked<UABGameSingleton>(GEngine->GameSingleton);
    if (Singleton)
    {
        return *Singleton;
    }

    UE_LOG(LogABGameSingleton, Error, TEXT("Invalid Game Singleton"));
    return *NewObject<UABGameSingleton>();
}
```