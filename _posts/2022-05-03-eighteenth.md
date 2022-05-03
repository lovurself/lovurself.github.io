---
layout: post
title:  "[CSS3] flexbox 사용법"
date: 2022-05-03
---
2022-05-03



국비수업을 들을 때 강사님께서 알려준 요소들을 배치하는 방법에는 float, position, flexbox가 있었다. 나는 flexbox를 아주 애용하는 편이다. 그래서 이번에 정확하게 정리를 해보려고 한다.



### flexbox

= flexible box module로 부모 내의 자식 요소들을 정리해주는 속성이다.



부모의 박스에 display: flex;를 지정해주고 자식 요소를 가로방향으로 배치할 것인지 세로방향으로 배치할것인지에 따라 주축과 교차축이 달라진다.

* 주축 : 자식 요소들이 배치되는 기본 축을 말한다.
* 교차축 : 주축과 수직인 축을 교차축이라고 한다.



![flexbox - row](https://user-images.githubusercontent.com/98265020/166466533-9d061cf9-8c27-47b2-95f6-2e4c2c34e4de.png)

위의 사진처럼 주축이 가로이면 교차축은 세로가 되는 것이다.



![flexbox - column](https://user-images.githubusercontent.com/98265020/166466544-b5352eea-a9d5-481a-8273-bea4e42496c7.png)

그리고 위의 사진처럼 주축이 세로이면 교차축은 가로가 되는 것이다.

주축을 설정하는 속성은 flex-direction이며 row, row-reverse, column, column-reverse가 있다. 각각 reverse를 붙여진 것은 자식 요소의 순서가 정반대가 된다는 뜻이다.

주축의 시작과 끝, 교차축의 시작과 끝을 알아야 요소를 정렬할 때 쉽게 설정할 수 있다.



**justify-content**   

1. flex-start : 자식요소들이 주축의 시작에 배치
2. center : 자식요소들이 주축의 가운데에 배치
3. flex-end : 자식요소들이 주축의 끝에 배치
4. space-between : 자식요소들의 양쪽 끝 요소가 각각 주축의 시작과 끝에 배치되고 나머지 요소들이 균일한 간격으로 배치
5. space-around : 자식요소들의 둘레에 대해 균일한 간격으로 배치
6. space-evenly : 자식요소들의 각각 양쪽이 균일한 간격으로 배치

![justify-content](https://studiomeal.com/wp-content/uploads/2020/01/10-1.jpg)

[자료출처](https://studiomeal.com/archives/197)



**align-items**   

1. flex-start : 자식요소들이 교차축의 시작에 배치
2. center : 자식요소들이 교차축의 가운데에 배치
3. flex-end : 자식요소들이 교차축의 끝에 배치
4. baseline : 자식요소들을 텍스트의 baseline의 기준으로 배치
5. stretch : 부모 요소의 교차축의 끝까지 채움



**flex-wrap**   

1. nowrap : 부모 요소의 너비에 맞게 자식요소의 사이즈가 변형
2. wrap : 부모요소의 너비에 맞게 넘치는 자식요소는 다음 줄에 배치
3. wrap-reverse : 자식요소들의 배치 순서가 정반대로 되는 것



> 위의 속성들은 정렬시킬 요소들의 부모 요소에 정의하는 것이고, 이제부터 정리하는 것은 자식요소 각각에 정의해주는 것이다.



**align-self**   

= 부모요소에서 설정해준 align-items를 각각의 자식요소에 특별하게 정의할 수 있다. 여러개의 자식요소 중에 하나씩 다르게 배치하고 싶을 때 사용한다.

1. auto
2. stretch
3. baseline
4. flex-start
5. center
6. flex-end

![flexbox-big](https://user-images.githubusercontent.com/98265020/166472629-4b4dcc88-30df-454e-af0d-0a62c478544a.jpg)



내가 자주 사용하는 속성을 위주로 정리해보았고 추가할 내용이 있다면 추후에 새로 포스팅을 하거나 이 글을 수정을 하려고 한다.

