---
title: Github 블로그 (Jekyll + Chirpy)에 댓글 기능 추가 (giscus)
date: 2024-03-21 20:51:00 +0900
categories: [Github Blog]
tags: []     # TAG names should always be lowercase
---

## 1. giscus app 추가

아래 링크를 통해 깃헙 블로그 레포지토리에 giscus app 추가

[https://github.com/apps/giscus](https://github.com/apps/giscus)

## 2. Discussions 활성화

`Settings` -> `General` 의 `Features` 섹션에서 `Discussions` 체크

![activate discussions](/assets/img/posts/2024-03-21-github-blog-giscus/1.webp)

이후 레포 상단바를 보면 `Discussions` 항목이 추가되어 있어야 합니다.

![check activated discussions](/assets/img/posts/2024-03-21-github-blog-giscus/2.webp)

## 3. Discussions에 Comments 카테고리 추가

`Discussions` 탭에서 Categories 목록 옆의 수정 아이콘을 눌러 카테고리를 추가할 수 있습니다.

![how to add category](/assets/img/posts/2024-03-21-github-blog-giscus/3.webp)

다음 화면에서 `New Category` 버튼을 누른 후, 아래와 같이 설정하여 추가해 주세요.

- Category name: Comments
- Discussion Format: Announcement

정상적으로 완료됐다면 다음과 같이 `Comments` 항목이 추가된 걸 확인할 수 있습니다.

![check added category](/assets/img/posts/2024-03-21-github-blog-giscus/4.webp){: width="300" }

## 4. giscus 설정값 가져오기

[https://giscus.app/ko](https://giscus.app/ko)

위 링크의 저장소 항목에 `myusername/myrepo` 형식으로 입력하면, 필요한 설정을 다 완료했는지 알 수 있습니다.

![giscus setting](/assets/img/posts/2024-03-21-github-blog-giscus/5.webp)

이후 해당 페이지의 아래에 있는 옵션들을 선택해주시면 됩니다.

필수적으로 해 주어야 할 항목은 Discussion 카테고리 선택 입니다.

[3. Discussions에 Comments 카테고리 추가](#3-discussions에-comments-카테고리-추가) 에서 만들었던 `Comments`로 지정해주면 됩니다.

![giscus discussion setting](/assets/img/posts/2024-03-21-github-blog-giscus/6.webp)

나머지 옵션들의 경우 저는 그대로 두었습니다.

이후 아래쪽에 다음과 같이 코드가 생성되는데, 이 코드를 기억해두시면 됩니다.

```html
<script src="https://giscus.app/client.js"
  data-repo="jinwoo0103/jinwoo0103.github.io" - 본인 것으로 수정
  data-repo-id="your-repo-id" - 본인 것으로 수정
  data-category="Comments"
  data-category-id="your-category-id" - 본인 것으로 수정
  data-mapping="pathname"
  data-strict="0"
  data-reactions-enabled="1"
  data-emit-metadata="0"
  data-input-position="bottom"
  data-theme="preferred_color_scheme"
  data-lang="ko"
  crossorigin="anonymous"
  async>
</script>
```

## 5. Chirpy config에 설정 추가

`_config.yml` 파일의 `comments` 항목을 수정해야 합니다.

- `provider`를 `active`로 수정 후, 값에는 `giscus` 입력
  - 내부 코드에서 `provider`에 대한 참조가 없고, `active`에 대한 참조만 있어서 수정하니 잘 동작합니다.
- `giscus` 하위 항목에 [4. giscus 설정값 가져오기](#4-giscus-설정값-가져오기) 에서 저장해 둔 코드 참조해서 입력

```yml
comments:
  # Global switch for the post comment system. Keeping it empty means disabled.
  active: giscus
  # The provider options are as follows:
  disqus:
    shortname: # fill with the Disqus shortname. › https://help.disqus.com/en/articles/1717111-what-s-a-shortname
  # utterances settings › https://utteranc.es/
  utterances:
    repo: # <gh-username>/<repo>
    issue_term: # < url | pathname | title | ...>
  # Giscus options › https://giscus.app
  giscus:
    repo: jinwoo0103/jinwoo0103.github.io - 본인 것으로 수정
    repo_id: your-repo-id - 본인 것으로 수정
    category: Comments
    category_id: your-category-id - 본인 것으로 수정
    mapping: # optional, default to 'pathname'
    strict: # optional, default to '0'
    input_position: # optional, default to 'bottom'
    lang: # optional, default to the value of `site.lang`
    reactions_enabled: # optional, default to the value of `1`
```

## 6. 변경사항 배포 후 확인

변경사항을 레포지토리에 푸시한 후, 잘 동작하는지 확인!