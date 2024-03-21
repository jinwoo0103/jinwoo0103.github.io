---
title: Github 블로그 (Jekyll + Chirpy)에 구글 검색 노출 설정
date: 2024-03-21 23:40:00 +0900
categories: [Github Blog]
tags: []     # TAG names should always be lowercase
---

## 1. Google search console에 url 등록

[Google search console](https://search.google.com/search-console/about) 접속

`시작하기` 누른 후, URL 접두어 영역에 등록할 github 블로그 주소를 입력하고 `계속` 버튼을 눌러주세요.

![google search console url](/assets/img/posts/2024-03-21-github-blog-google/1.png){: width="600" }

소유권 확인 창이 나오면, 아래의 다른 확인 방법에서 `HTML 태그` 방식을 눌러주세요.

![google search console html tag](/assets/img/posts/2024-03-21-github-blog-google/2.png){: width="600" }

`복사`를 눌러 메타 태그를 복사한 후, content 부분 값만 따로 기록해 둡니다.

> 이 때, [2. 블로그에 메타태그 적용](#2-블로그에-메타태그-적용)이 완료되기 전까지는 확인 버튼을 누르지 마세요.
{: .prompt-warning }

```html
<meta name="google-site-verification" content="여기 값 기록" />
```

## 2. 블로그에 메타태그 적용

`_config.yml` 파일에서 `webmaster_verifications` 항목의 `google` 필드에 기록해둔 값을 입력합니다.

```yml
# Site Verification Settings
webmaster_verifications:
  google: 위에서 기록해둔 값 입력
  bing: # fill in your Bing verification code
  alexa: # fill in your Alexa verification code
  yandex: # fill in your Yandex verification code
  baidu: # fill in your Baidu verification code
  facebook: # fill in your Facebook verification code
```

완료했다면 푸시해서 배포까지 진행해주세요.

## 3. 메타태그 적용 확인 및 구글 소유권 확인 완료

배포 완료된 깃헙 블로그에 접속해서 개발자 도구로 head 태그 내에 meta 태그가 제대로 등록되었는지 확인해주세요.

`your-content` 부분에 위에서 입력한 값이 있어야 합니다.

![check blog meta tag](/assets/img/posts/2024-03-21-github-blog-google/3.png)

확인되었다면 [1. Google search console에 url 등록](#1-google-search-console에-url-등록)에서 열어둔 창의 `확인`을 눌러줍니다.

![checked meta tag by google](/assets/img/posts/2024-03-21-github-blog-google/4.png){: width="600" }

위와 같은 창이 나오면 구글이 정상적으로 메타 태그를 인식했다는 뜻입니다.

## 4. 사이트맵 및 RSS 등록

Google search console의 `Sitemaps` 항목에 들어가서 `sitemap.xml`과 `feed.xml`을 등록해주어야 합니다.

입력란에 `sitemap.xml`, `feed.xml`을 각각 순차적으로 입력해주면 완료됩니다.

![google search console sitemaps section](/assets/img/posts/2024-03-21-github-blog-google/5.png)

## 5. 구글 검색에 등록되었는지 확인

Google search console의 `페이지` 항목에 들어가보면 아직 데이터를 처리하는 중이라고 나옵니다.

![google search console page section](/assets/img/posts/2024-03-21-github-blog-google/6.png)

경험자분들에 따르면 실제 구글 검색이 가능하기까지 보통 2-3일, 많게는 일주일까지도 걸린다고 합니다.

2024.03.21 23시경에 sitemap을 제출했는데, 등록되면 본 포스트에도 업데이트해서 알려드리겠습니다.