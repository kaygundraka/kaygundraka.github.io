---
title: Unity Netcode Life Cycle
description: 각종 기능 호출 순서 확인
date: 2024-10-29 22:49:00 +09:00
categories: [Unity, Netcode]
tags: [unity, Netcode]
pin: true
math: true
mermaid: true
---

## 기본 초기화/해제 관련 코드
---

```csharp
private void Awake()
{
    Debug.Log("call Awake()");
}

private void Start()
{
    Debug.Log("call Start()");
}

public override void OnNetworkSpawn()
{
    base.OnNetworkSpawn();

    Debug.Log("call OnNetworkSpawn()");
}

public override void OnNetworkDespawn()
{
    base.OnNetworkDespawn();

    Debug.Log("call OnNetworkDespawn()");
}

public override void OnDestroy()
{
    // Clean up your NetworkBehaviour

    // Always invoked the base
    base.OnDestroy();
}
```

- 씬에 이미 배치되어 있는 경우
  - Awake, Start, OnNetworkSpawn
- 동적 생성
  - Awake, OnNetworkSpawn, Start

- NetworkBehavior가 꺼진 상태로 씬에 배치되어 있는 경우
  - Awake, OnNetworkSpawn, Start (enable될때 호출됨)

## NetworkBehaviour 관련 스폰
---

|Method|Scope|Use case|Context|
|-|-|-|-|
|OnNetworkPreSpawn|NetworkObject|Pre-Spawn initialization|Client and Server|
|OnNetworkSpawn|NetworkObject|During spawn initialization|Client and Server|
|OnNetworkPostSpawn|NetworkObject|Post-spawn initialization|Client and Server|
|OnNetworkSessionSynchronized|All NetworkObjects|New client finished synchronizing|Client-side only|
|OnInSceneObjectsSpawned|In-scene NetworkObjects|New client finished synchronizing or a scene is loaded|Client and Server|


## 각종 업데이트
---

- FixedUpdate, Update LateUpdate에서는 IsSpawned Property로 체크 필요

### 참고
- https://docs-multiplayer.unity3d.com/netcode/current/basics/networkbehavior-synchronize/