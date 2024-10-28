---
title: UnrealC++ - Player Movement
description: UnrealC++의 이동 관련 기능 정리
date: 2024-10-28 19:09:00 +09:00
categories: [Unreal, C++]
tags: [C++, Unreal]
pin: true
math: true
mermaid: true
---

## 용어 
---

- Desired Rotation (의지, 목표 회전)
- Control Rotation (입력 회전)
- Rotation Rate (회전 속도)

## PlayerController
---

- ControlRotation : 입력에 의한 회전 값

## Pawn
---

- 입력에 의한 회전 값을 Pawn에 바로 적용하려면
    - Use Control Rotation Pitch
    - Use Control Rotation Yaw
    - Use Control Rotation Roll

## SpringArm
---

- Use Pawn Control Rotation
    - Inherit Pitch
    - Inherit Law
    - Inherit Roll
- Do Collision Test
    - 장애물 충돌 적용

## Camera
---

- Use Pawn Control Rotation (1인칭에서 주로 사용)

## CharacterMovement
---

- Movement Mode : None, Walking, Falling
    - MaxWalkSpeed : 최대 이동 속도
    - JumpZVelocity : 점프 최초 속도
    - Rotation Rate : 회전 속도
    - Use Controller Desired Rotation : ControlRotation을 목표로 지정한 속도로 회전
    - Orient Rotation To Movement : 이동 방향에 회전을 맞추기
        - 폰의 회전 옵션과 충돌이 나지 않도록 주의