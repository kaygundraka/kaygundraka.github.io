---
title: Github Blog 만들기
description: Github Blog + jekyll + chirpy 테마 적용하기
date: 2024-10-28 16:55:00 +09:00
categories: [Github, Blog]
tags: [Github, Blog, jekyll, chirpy]
pin: true
math: true
mermaid: true
---

## 과정

1. GitHub Repo 만들기
2. 로컬에 jekyll + chirpy 설치하기
3. Github에 올리기

## Github Repo 만들기

- 설정 내용
  - Name : 아이디 + github.io 이름으로 설정
  - Type : public으로 설정

## Git Clone 후 .gitignore 추가
```
# Bundler cache
.bundle
vendor
Gemfile.lock

# Jekyll cache
.jekyll-cache
_site

# RubyGems
*.gem

# NPM dependencies
node_modules
package-lock.json

# IDE configurations
.idea
.vscode

# Misc
# assets/js/dist  ### 주석 처리
```

## Rubby 설치

- mac 기준 brew 최신화
  - > brew update

- ruby 설치 관리자 rbenv 설치
  - > brew install rbenv

- rbenv로 ruby 설치
  - 깃헙 페이지 버전 확인 : https://pages.github.com/versions/
  - > rbenv install 루비버전
  - > rbenv rehash
  - > rbenv global 루비버전

- 루비 환경 설정 변경
  - > vi ~/.zshrc
  - > eval "$(rbenv init -)"

## jekyll 설치

- 이전에 사용 중이던 터미널 재시작 후 gem을 통해 설치
  - > gem install jekyll

## github에서 테마 받기

- 파일을 다운 받아서 내 github 폴더에 복사 후 붙여넣기
  - https://www.irgroup.org/posts/jekyll-chirpy/

- 로컬에서 실행 테스트
  - > bundle update
  - > bundle exec jekyll serve --liveReload
  - localhost:4000 접속

- 잘되면 github에 작업 내용 push

## github 설정 변경

- Repo 설정 변경 
  - settings - github pages - Build and deployment
  - Github Action으로 변경
  - Configuration 파일 생성
    - > .github/workflows/jekyll.yml
  - build에서 Build with Jekyll 위에 npm 빌드 단계 추가
    - > name: npm build
    - > run: npm install && npm run build

## Github Action 확인

- Github 빌드 에러 확인
  - 혹시 버전 차이가 나면 다운 그레이드