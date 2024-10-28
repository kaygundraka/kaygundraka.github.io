---
title: Unity Animation Clip 등록하기
description: 스크립트에서 Unity Animation Event를 등록하여 사용한다
date: 2024-10-28 22:30:00 +09:00
categories: [Unity, AnimationEvent, AnimationHandler]
tags: [unity, animationevent, animationhandler]
pin: true
math: true
mermaid: true
---

Unity를 Animator를 사용하다보면 애니메이션의 특정 지점에서 함수를 호출하고 싶은 경우가 많다. 이럴 때 별도의 AnimationHandlerComponent를 만들어서 Animator와 함께 붙여두면 편리하다

## 예시 코드
---

- 시작과 종료에 핸들러 등록 예시코드

```csharp
private void Start()
{
    var animator = this.GetComponent<Animator>();

    var rac = animator.runtimeAnimatorController;

    for (int i = 0; i < rac.animationClips.Length; i++)
    {
        AnimationClip clip = rac.animationClips[i];

        clip.AddEvent(new AnimationEvent
        {
            time = 0,
            functionName = "AnimationStartHandler",
            stringParameter = clip.name
        });

        clip.AddEvent(new AnimationEvent
        {
            time = clip.length,
            functionName = "AnimationEndHandler",
            stringParameter = clip.name
        });
    }
}

private void AnimationStartHandler(string animationClipName)
{
    // 내용
}

private void AnimationEndHandler(string animationClipName)
{
    
}
```

- 추가 궁금증
  - 같은 Animator를 쓰면 한쪽에서만 등록해도 되는가?
  - 실험해보고 추가 내용 올릴 예정