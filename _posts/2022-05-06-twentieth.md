---
layout: post
title:  "[CSS3] Grid layout으로 반응형 웹 제작방법"
date: 2022-05-06
---
2022-05-06



요즘은 반응형으로 웹페이지를 만들어야 컴퓨터, 태블릿, 모바일에서 그 기기에 맞게 화면이 구성되어 어떤 기기로 웹페이지를 열어도 깨져보이지 않고 원하는 내용을 볼 수 있도록 한다.

반응형을 만들 때 요소들의 크기와 배치 등을 설정하는 것이 제일 중요하고 어려운데, 나는 평소 display를 flex를 하여 배치하고 요소의 크기는 %나 vw 등으로 설정하여 브라우저 크기에 비례하도록 작성을 했었다. 그런데 이제야 css에 grid layout에 대해 알게 되어 이것을 공부하고 정리하여 새 웹페이지를 만들때 적용해보려고 한다.



### Grid layout

= 페이지를 여러 주요 영역으로 나누거나, 크기와 위치나 문서 계층 구조를 정의할 수  있다. 세로 열과 가로 행을 기준으로 요소들을 정렬하여 반응형 웹을 만들 때 유용하게 사용된다.
flex와 같이 정렬해줄 자식 요소를 감싸고 있는 부모요소에 grid를 정의해준다.

<br>
**기본예제를 통해 정리해보기**   

[기본예제 참고자료](https://developer.mozilla.org/ko/docs/Web/CSS/CSS_Grid_Layout)

```html
<div class="wrapper">
    <div class="item-one">one</div>
    <div class="item-two">two</div>
    <div class="item-three">three</div>
    <div class="item-four">four</div>
    <div class="item-five">five</div>
    <div class="item-six">six</div>
</div>
```

```css
.wrapper {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-gap: 10px;
    grid-auto-rows: minmax(100px, auto);
}

.item-one {
    grid-column: 1 / 3;
    grid-row: 1;
}
.item-two {
    grid-column: 2 / 4;
    grid-row: 1 / 3;
}
.item-three {
    grid-column: 1;
    grid-row: 2 / 5;
}
.item-four {
    grid-column: 3;
    grid-row: 3;
}
.item-five {
    grid-column: 2;
    grid-row: 4;
}
.item-six {
    grid-column: 3;
    grid-row: 4;
}
```

![grid 기본예제 웹페이지 모습](https://user-images.githubusercontent.com/98265020/167136471-0694cc46-2e5f-4c9f-8b41-ba8857d98f01.jpeg)

부모요소에 적용
1. display: grid;   
=> 이것을 정의한 부모요소 내의 자식요소를 정의한대로 배치하고 크기를 정하겠다는 것이다.

2. grid-template-columns   
=> 가로 크기를 조정한다. px로도 정의 가능하고, fr로도 크기를 조정할 수 있다.
여기서, fr이란? 유연한 크기를 갖는 단위인데 부모요소의 공간 비율을 분수(fraction)으로 나타낸다.   
그리고 repeat 함수는 많은 열과 행에서 반복되는 부분을 간결하게 작성할 수 있게 한다. 위의 기본 예제에서는 repeat(3, 1fr)로 3개의 열을 똑같은 비율의 요소로 배치하겠다는 것이다.

3. grid-gap   
=> 자식요소간의 간격의 크기를 조정한다. margin과 같은 의미이지 않을까 생각한다.

4. grid-auto-rows   
=> 세로 크기를 조정한다. 기본예제에서 minmax(100px, auto)는 100px은 min 크기, auto는 max 크기이다. 이것은 min크기보다는 크거나 같고, max크기보다는 작거나 같은 크기의 범위를 정의하는 것이다. 여기서는 결국 min크기만 정의되어 있고 max크기는 부모의 최대값과 동일하게 정의한 것이다.

<br>
자식요소에 적용   

1. grid-column    
=> 시작지점과 끝지점을 지정하여 크기와 자리 배치를 정의한다. 부모요소에서 3개의 열을 가질 것이라고 정의했었고 한 행에 3개의 열이 있다는 것을 파악해야 한다. 그럼 item-one은 첫번째 열의 왼쪽 가장자리에서 시작하여 세번째 열의 왼쪽 가장자리까지의 크기를 정의한 것이고, item-two는 두번째 열의 왼쪽 가장자리에서 네번째 열(세번째 열의 오른쪽 가장자리를 정의할 수 없기 때문에)의 왼쪽 가장자리까지 크기를 정의한 것이다. 또는, 열의 순서 번호를 입력하여 번호에 맞는 자리에 배치하고 부모요소의 1/3 크기로 정의한다.

2. grid-row   
=> grid-column과 비슷하지만 행의 시작지점과 끝지점을 지정하여 크기와 자리를 배치한다.

<br>
<br>
<br>

>이번에 새로운 반응형을 만들 때 grid를 사용해보면서 기본예제처럼 코드를 작성해보고 더 필요한 속성이 있으면 더 정리해봐야 할 것 같다.

* 위의 모든 내용은 MDN을 통해서 알 수 있다.
