---
date: 2020-02-19 22:30:00
layout: post
title: 나만의 GitHub 페이지를 구글에서 검색이 가능하도록 설정 해보자!
subtitle: Google search Console 을 통해 나의 깃허브 페이지를 구글에서도 검색 가능하게 해보자!
description: GitHub 페이지를 구글에서 검색이 가능하게 설정할 수 있다!
image: 
optimized_image: /assets/img/banner/github.png
category: github
tags:
  - github
  - page
  - google
  - google search Console
author: madfalc0n
paginate: true
comments: true
---


# 내가만든 Github blog를 구글에서도 검색이 가능하게 해보자!

깃허브로 만든 페이지의 경우 일반적으로 구글에서 검색이 불가능하게 되어있다. 우리는 추가적인 설정을 통해 구글에서도 검색이 가능하도록 설정이 가능하다



## Google  Search Console 가입 및 사이트페이지 추가

1. [Google Search Console](https://search.google.com/search-console/about)에 먼저 가입을 하자. 구글 계정이 있다면 패쓰

2. 가입완료 후 시작하기 클릭

   <img src="/assets/img/contents/git/image-20200219215924196.png" alt="image-20200219215924196" style="zoom:80%;" />

3. 나의  깃허브 블로그 주소를 입력한다.

   <img src="/assets/img/contents/git/image-20200219220113568.png" alt="image-20200219220113568" style="zoom:80%;" />

   > 나는 URL 접두어를 사용했다. `https://madfalc0n.github.io` 이런식으로 입력하면 되겠다.

4. html 파일 다운로드 후 자신의 `_config.yml` 파일이 있는 깃허브 루트 디렉토리에 복사한다.

   - 만약 소유권 확인 되지 않을 경우엔 `_config.yml`의 url 경로를 제대로 설정해주어야 한다.
   - url: `https://madfalc0n.github.io/`이런식으로

   <img src="/assets/img/contents/git/image-20200219220536118.png" alt="image-20200219220536118" style="zoom:80%;" />

<img src="/assets/img/contents/git/image-20200219221517903.png" alt="image-20200219221517903" style="zoom:80%;" />

5. 루트 경로에 똑같이 `sitemap.xml` 을 생성하고 아래의 소스코드를 추가한다.

   - 보통 jekyll 테마를 추가한 경우 sitemap.xml이 자동으로 생성 되는 것으로 알고있다.
   - 만약 그렇지 않다면 수동으로 넣어주자!

{% raw %}
   ```xml
   ---
   ---
      <?xml version="1.0" encoding="UTF-8"?>
      <urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
          {% for page in site.pages %}
              <url>
                  <loc>{{ page.url | prepend: site.baseurl | prepend: site.url }}</loc>
                  {% if page.layout == 'main' %}
                      <changefreq>weekly</changefreq>
                      <priority>1</priority>
                      <lastmod>{{ site.time | date: "%Y-%m-%d" }}</lastmod>
                  {% else %}
                      <changefreq>monthly</changefreq>
                      <priority>0.5</priority>
                  {% endif %}
              </url>
          {% endfor %}
          {% for post in site.posts %}
              <url>
                  <loc>{{ post.url | prepend: site.baseurl | prepend: site.url }}</loc>
                  <changefreq>weekly</changefreq>
                  <priority>0.8</priority>
                  <lastmod>{{ post.date | date: "%Y-%m-%d" }}</lastmod>
              </url>
          {% endfor %}
          {% for author in site.authors %}
              <url>
                  <loc>{{ author.url | prepend: site.baseurl | prepend: site.url }}</loc>
                  <changefreq>monthly</changefreq>
                  <priority>0.5</priority>
              </url>
          {% endfor %}
      </urlset>
   ```
{% endraw %}



6. 구글 서치 콘솔 메인에서 아래에서 사이트맵 주소표시하여 제출 

   <img src="/assets/img/contents/git/image-20200219222629572.png" alt="image-20200219222629572" style="zoom:80%;" />



7. 성공적으로 제출 되었는지 확인

   <img src="/assets/img/contents/git/image-20200219222703721.png" alt="image-20200219222703721" style="zoom:80%;" />
   
   