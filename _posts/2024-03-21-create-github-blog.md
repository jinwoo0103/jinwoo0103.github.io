---
title: Github 블로그 만들기 (Jekyll + Chirpy)
date: 2024-03-21 15:27:00 +0900
categories: [Github Blog]
tags: []     # TAG names should always be lowercase
---

> 본 글에서는 macOS 환경을 기준으로 설명합니다.
{: .prompt-warning }

## Jekyll 준비

### 1. ruby 설치 (rbenv)

맥에도 기본적으로 ruby가 설치되어 있지만, 편의성을 위해 [rbenv](https://github.com/rbenv/rbenv)를 많이 사용합니다.

```shell
# homebrew 사용해서 rbenv 설치
$ brew update
$ brew install rbenv ruby-build

# rbenv 설치 확인
$ rbenv -v
rbenv 1.2.0

# list latest stable versions:
$ rbenv install -l
3.0.6
3.1.4
3.2.3
3.3.0
...

# 현재 가장 최신 버전인 3.3.0 설치
$ rbenv install 3.3.0

# ruby 설치 확인
$ rbenv versions
* system (set by /Users/jinwoo/.rbenv/version)
  3.3.0

# set the default Ruby version for this machine
$ rbenv global 3.3.0

# 원하는 버전으로 선택되었는지 확인
$ rbenv versions
  system
* 3.3.0 (set by /Users/jinwoo/.rbenv/version)

# 최종 확인
$ ruby -v
ruby 3.3.0 (2023-12-25 revision 5124f9ac75) [arm64-darwin23]
```

### 2. jekyll 설치

```shell
$ gem install jekyll bundler

# jekyll 설치 확인
$ jekyll -v
jekyll 4.3.3

# bundler 설치 확인
$ bundler -v
Bundler version 2.5.6
```

## Github 준비

> Chirpy 공식 페이지에서 소개하는 [Fork 방식](https://chirpy.cotes.page/posts/getting-started/#option-2-github-fork)은 깃헙 잔디가 심어지지 않는다고 합니다.  
본 글에서는 다른 방식으로 진행할 예정이니 Fork 방식으로 진행하실 분들은 위의 링크를 참고해주세요.
{: .prompt-warning }

### 1. Github 레포지토리 생성

- 레포명: `<본인의 github id>.github.io`
- `Add a README file` 체크

![create new github repository](/assets/img/posts/2024-03-21-create-github-blog/1.png)

### 2. Github Pages 설정
`Setting` -> `Pages` 에서 `Build and deplopment` 의 `Source` 부분 `Gitub Actions` 로 수정

![Apply github actions](https://chirpy-img.netlify.app/posts/20180809/pages-source-dark.png){: width="300" }


### 3. 깃헙 레포지토리 Clone

자세한 방식은 생략하겠습니다.

```shell
$ cd <클론할_경로>
$ git clone <SSH 주소>
```

## Chirpy 테마 적용하기

### 1. Chirpy 테마 레포지토리 다운로드

Download ZIP 눌러주시고 압축 해제 해주세요. (경로 기억하기)

![create new github repository](/assets/img/posts/2024-03-21-create-github-blog/2.png){: width="300" }

### 2. 클론한 레포지토리에 Chirpy 테마 파일 복사하기

> `.github` 폴더 등 숨김처리된 파일들도 모두 복사되어야 합니다. (초기 설정에 필요)
{: .prompt-warning }

```shell
# 레포지토리 경로로 이동
$ cd <레포지토리_경로>

# README.md 삭제
$ rm README.md

# Chirpy 테마 레포지토리 복사하기
$ cp -r <압축_푼_폴더_경로>/*(D) . # 숨김 처리된 파일까지 복사

# 숨김 처리된 파일까지 복사되었는지 확인
$ ls -al
```

### 3. 커밋하기

```shell
$ git add --all
$ git commit -m "Copied jekyll-theme-chirpy repo"
```

### 4. `tools/init` 스크립트 수정

초기 설정을 해주는 `tools/init` 스크립트는 Fork 방식으로 진행된다고 가정하고 작성되었기 때문에, 약간의 수정이 필요합니다.

다음과 같이 `main` 함수의 `checkout_latest_release` 부분을 주석처리해주면 됩니다.

참고: [해당 작업 커밋](https://github.com/jinwoo0103/jinwoo0103.github.io/commit/272ff3487daecbd72bae4191d8488138c1c71c3f)
(추가로 저는 pnpm을 사용을 위해 모든 npm을 pnpm으로 수정해 주었습니다.)

```shell
main() {
  check_env
  # checkout_latest_release
  init_files
  commit
}
```

작업 완료 후 커밋까지 해 주셔야 합니다. (누락시 다음 과정 진행 불가)
```shell
$ git add --all
$ git commit -m "Edited tools/init script"
```

### 5. 초기 설정

```shell
$ bash tools/init
```

정상적으로 완료되면 커밋이 생성되어 있어야 합니다.

```shell
$ git log
commit ...
Author: ...
Date: ...

    chore: initialize the environment

```

완료되었다면 푸시해주세요.
```shell
$ git push origin main
```

## 배포 확인하기

레포지토리의 `Actions` 탭에 가면 `chore: initialize the environment` 이름의 워크플로우가 하나 있습니다.
해당 워크플로우가 성공하면, `https://<본인의 github id>.github.io`에 배포가 완료되었습니다.