---
title: UnrealC++ - Setup AI Class
description: UnrealC++에서 AI Class를 설정합합니다.
date: 2024-10-28 19:15:00 +09:00
categories: [Unreal, C++]
tags: [C++, Unreal, AI]
pin: true
math: true
mermaid: true
---

### 모듈 설정

```cpp
"NavigationSystem", "AIModule", "GameplayTasks"
```

### 클래스

- AIController를 상속 받은 클래스 생성
    - AABAIController
- 생성자에서 연결 추가

```cpp
AIControllerClass = AABAIController::StaticClass();
AutoPossessAI = EAutoPossessAI::PlacedInWorldOrSpawned;
```

### 언리얼 행동 트리 연결하기

- 2 종류의 어셋을 만들어 주어야함
    - Artificial Intelligence
        - Behaviour Tree : 행동 트리
        - Black Board : 의사 결정을 하기 위한 데이터 저장소

### 예시 코드

- header

```cpp
UCLASS()
class ARENABATTLE_API AABAIController : public AAIController
{
	GENERATED_BODY()

public:
	AABAIController();

	void RunAI();
	void StopAI();

protected:
	virtual void OnPossess(APawn* InPawn) override;

private:
	UPROPERTY()
	TObjectPtr<class UBlackboardData> BBAsset;

	UPROPERTY()
	TObjectPtr<class UBehaviorTree> BTAsset;
};
```

- cpp

```cpp
// Fill out your copyright notice in the Description page of Project Settings.

#include "AI/ABAIController.h"

#include "BehaviorTree/BehaviorTree.h"
#include "BehaviorTree/BlackboardData.h"
#include "BehaviorTree/BlackboardComponent.h"

AABAIController::AABAIController()
{
	static ConstructorHelpers::FObjectFinder<UBlackboardData> BBAssetRef(TEXT("/Script/AIModule.BlackboardData'/Game/ArenaBattle/AI/BB_AB_Character.BB_AB_Character'"));
	if (BBAssetRef.Object)
	{
		BBAsset = BBAssetRef.Object;
	}
	
	static ConstructorHelpers::FObjectFinder<UBehaviorTree> BTAssetRef(TEXT("/Script/AIModule.BehaviorTree'/Game/ArenaBattle/AI/BT_AB_Character.BT_AB_Character'"));
	if (BTAssetRef.Object)
	{
		BTAsset = BTAssetRef.Object;
	}
}

void AABAIController::RunAI()
{
	UBlackboardComponent* BlackboardPtr = Blackboard.Get();
	if (UseBlackboard(BBAsset, BlackboardPtr))
	{
		bool RunResult = RunBehaviorTree(BTAsset);
		ensure(RunResult);
	}
}

void AABAIController::StopAI()
{
	UBehaviorTreeComponent* BTComponent = Cast<UBehaviorTreeComponent>(BrainComponent);
	if (BTComponent)
	{
		BTComponent->StopTree();
	}
}

void AABAIController::OnPossess(APawn* InPawn)
{
	Super::OnPossess(InPawn);

	RunAI();
}
```

### Action

- 언리얼에서는 Action을 Task로 부른다
    - BTTaskNode를 상속 받아서 구현
    - 네이밍은 BTTaskNode_Name으로 짓는다

### Service

- BTService를 상속 받음
    - 액션과 동일하게 BTService_Name으로 짓는다