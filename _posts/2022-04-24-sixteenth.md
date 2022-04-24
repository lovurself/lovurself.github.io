---
layout: post
title:  "[HTML5] meta 태그에 대하여"
date: 2022-04-24
---
2022-04-24



개인 포트폴리오를 만들 때 emmet으로 html을 선언하고 head는 language, title, link 정도만 수정하고 거의 대부분을 body에만 작성하기 바빴었다. 그런데 어떤 유튜브 동영상을 봤는데 head에 meta 태그로 아주 여러가지 설정을 할 수 있는 걸 알게 되었다. 그래서 오늘 한번 정리를 해보려고 한다.



## meta tag

= 해당 문서에 대한 정보인 metadata(메타데이터)를 정의할 때 사용, meta 태그로 정의된 정보는 브라우저나 검색 엔진, 다른 웹서비스에서 사용하게 된다.



### meta tag의 종류



name 속성이나 http-equiv 속성이 명시되었다면 반드시 content 속성도 함께 명시해야 하며, 두 속성이 아니라면 content 속성을 명시할 수 없다.

일단, emmet으로 자동으로 생성되는 meta 태그부터 알아보자!

1. meta charset="UTF-8"

   => 해당 문서의 문자 인코딩 방식을 utf-8로 하겠다고 명시하는 것

2. meta http-equiv="X-UA-Compatible" content="IE=edge"

   => content 속성에 명시된 값에 대한 HTTP 헤더를 제공한다는 것이다. 이때 인터넷 익스플로러(IE)는 여러가지 버전이 있고, 이 버전 차이로 버전마다 보여지는 것이 달라지기 때문에 표준모드로 볼 수 있도록 설정하는 것이다. IE=edge는 버전 중에 가장 최신 표준모드를 선택하는 것이다.

   ([참고한 자료](https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=pts4779&logNo=221238716152))

3. meta name="viewport" content="width=device-width, initial-scale=1.0"

   => 모든 기기에서 웹페이지가 잘 보이도록 viewport를 설정하는 것인데, 브라우저가 웹페이지를 렌더링할 때 동작하는 방법을 알려주고 viewport의 크기를 알 수 있다.



4. meta name="keyword" content="키워드명"

   => 검색 엔진을 위한 키워드들을 정의하는 것, 내 웹페이지를 보여주기 위해 사람들이 검색할 만한 키워드를 정의하는 것이다.

5. meta name="description" content="설명"

   => 내가 만든 웹페이지에 대한 설명을 정의하는 것이다. 내가 설명한 글을 보고 사람들이 자신이 검색한 것과 관련이 있는지 판단할 수 있도록 하는데, 자세하고 정확한 내용을 작성해야 클릭할 확률을 높인다.

6. meta name="author" content="작성자명"

   => 문서의 저자를 정의하는 것이다.



가장 기본적인 내용만 정리해본 것이고 더 자세히 정리된 블로그를 찾아서 공유한다.

[메타태그(META TAG) 속성정리 및 사용 방법 - BLOG.MUNILIVE.COM](https://blog.munilive.com/posts/meta-tag-property-and-use-method.html)
