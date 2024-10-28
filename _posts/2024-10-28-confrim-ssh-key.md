---
title: 로컬 SSH 키 확인
description: 맥과 윈도우에서 로컬 SSH 키 확인하기
date: 2024-10-28 16:55:00 +09:00
categories: [Github, Environment]
tags: [Github, ssh, depolykey]
pin: true
math: true
mermaid: true
---

개인적으로 Github 사용시 데스크탑과 랩탑에서 새로운 저장소를 Clone 할 때, 이전에 만들어둔 SSH 키를 다시 찾아서 사용할 때가 있다.

다시 찾기 어렵지 않지만 한번 설정해두면 다시 확인하는 경우가 많지 않아서 메모해둔다.

### Windows

1. Windows PoserShell에 명령어 입력
2. > cd ~/.ssh
3. 키가 존재한다면 notepad로 public 키 파일을 연다
4. > notepad sshkey.pub

### Mac

1. 터미널을 연다
2. > cd ~/.ssh
3. 윈도우와 동일하게 vi로 public 키 파일을 연다
4. > vi sshkey.pub
