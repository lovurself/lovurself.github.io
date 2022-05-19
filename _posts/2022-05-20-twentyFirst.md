---
layout: post
title:  "[CSS3] position의 종류"
date: 2022-05-20
---
2022-05-20



최근에 면접을 보게 되었는데 기술면접 질문 중에 정말 기본적인 position의 종류에 대한 질문을 받았다. 제대로 대답을 못하고 모르고 있던 정보도 알려주셔서 이번에 position에 대해 공부해보려고 한다.



### position

=> 요소들을 배치하는 속성이다. position에는 static, relative, absolute, sticky가 있다. position을 지정해준 다음 top, bottom, left, right 속성으로 위치를 설정할 수 있다.



1. static   

   => "정적인"이란 뜻처럼 top, bottom, left, right 속성으로 아무런 영향을 받지 않는다. position의 기본값이다.



2. relative   

   => **자기 자신을 기준**으로 top, bottom, left, right 속성값에 따라 offset을 적용한다. 레이아웃에서 relative 요소가 차지하는 공간은 static일때와 같다.

   상대적인 위치를 지정하는 요소이다.

   > offset이란?
   >
   > 상대적인 위치를 잡아줄 떄 사용하기 때문에 기준이 되는 요소를 지정해주어야 한다. 기준이 되는 요소는 html일수도 있고 body일수도 있고 부모 요소일수도 있다. 기준이 되는 요소에 따라 top, bottom, left, right의 시작점이 달라진다.

   ```html
     <body>
         <div
           style="
             position: relative;
             background-color: aqua;
             width: 50px;
             height: 50px;
             top: 50px;
             left: 50px;
           "
         ></div>
         <div
           style="
             position: relative;
             background-color: green;
             width: 300px;
             height: 300px;
             top: 100px;
           "
         >
           <div
             style="
               position: relative;
               background-color: yellow;
               width: 50px;
               height: 50px;
               top: 50px;
               left: 50px;
             "
           ></div>
         </div>
     </body>
   ```

   ![relative](https://user-images.githubusercontent.com/98265020/169075291-0c192ae6-cc78-4120-939c-213ee8cf8894.png)

   그리고 요소는 문서의 흐름에 따라 배치한다. 그래서 위의 사진을 보면 파란 상자는 자신의 기준에서 50px씩 떨어진 곳에 위치하고 초록 상자는 문서의 흐름상 파란 상자 다음이기 때문에 원래 파란 상자의 위치의 다음이 기준이 되어 100px 떨어진 곳에 위치한 것이다. 그리고 노란 상자는 초록 상자가 기준이 되어 50px씩 떨어진 곳에 위치했다.



3. absolute   

   => 가장 가까운 위치의 조상 요소에 대해 상대적으로 배치한다.  만약에 조상 요소 중에 위치를 지정한 요소가 없다면 초기의 컨테이닝 블록을 기준을 삼는다. (나는 absolute는 기준이 되는 상자 위에 떠있는 요소가 된다고 생각한다.)

   절대적인 위치를 지정하는 요소이다.

   > 컨테이닝 블록이란?
   >
   > 요소의 위치와 크기를 지정하는데 사용하는 블록을 의미하고, 컨테이닝 블록은 position이 무엇이냐에 따라 변경된다.

   ```html
   <body>
       <div style="position: relative">
         <div
           style="
             position: absolute;
             background-color: aqua;
             width: 50px;
             height: 50px;
             top: 150px;
             left: 150px;
             z-index: 1;
           "
         ></div>
         <div
           style="
             position: relative;
             background-color: green;
             width: 300px;
             height: 300px;
             top: 100px;
           "
         >
           <div
             style="
               position: absolute;
               background-color: yellow;
               width: 50px;
               height: 50px;
               top: -50px;
               left: 50px;
             "
           ></div>
         </div>
       </div>
     </body>
   ```

   ![absolute](https://user-images.githubusercontent.com/98265020/169328516-26d16308-b3ad-4fd9-82da-1e21ea4b94b5.png)

   absolute는 문서의 흐름을 깨고 공중에 떠있는 것처럼 된다. 그래서 파란상자 다음에 초록상자가 쌓이기 때문에 파란상자에 z-index에 값을 줘서 초록 상자 위에서 보일 수 있도록 했다. 그리고 파란상자와 초록상자는 기준 요소가 같기 때문에 같은 기준선에서 top, left 값만큼 움직인 위치에 배치된다. 그리고 노란 상자는 초록상자가 부모요소로 기준 상자가 되어 top, left 값만큼 움직인 위치에 배치된다. 이때 top의 값이 마이너스로 아래가 아닌 위로 움직인다.



4. fixed   

   => fixed는 다른 것과 다르게 기준이 되는 것이 뷰포트이다. 그래서 scroll를 내려도 그자리 그대로 위치한다. fixed는 요소가 뷰포트에 붙인 것처럼 보인다. 그래서 모든 페이지에 똑같은 위치에 두고 싶은 아이콘이나 요소에 적용하여 사용할 수 있다. (나는 메뉴에 자주 사용했다.)

   fixed 또한 문서의 흐름을 깨고 차곡차곡 쌓임을 만든다. 그래서 z-index로 쌓임의 순서를 변경할 수 있다. 

   절대적인 위치를 지정하는 요소이다.



5. sticky   

   => sticky는 내가 설정한 위치가 되기 전에는 static으로 위치하다가 설정한 위치에 도착하면 fixed처럼 되는 속성이다. 그래서 꼭 설정된 위치를 작성해야 한다.

   그런데 sticky가 확실하게 보이려면 조상 요소가 스크롤이 되어야 한다. 조상요소에 overflow가 hidden, scroll, auto, overlay를 설정하면 된다.

   그리고 다음 컨텐츠의 모서리를 만나면 해제된다.

    (사용해본 적이 없고, 면접에서 면접관님이 질문해주셔서 알게 되었다.)



**접근성 문제**   

* 화면을 확대했을 때 absolute나 fixed로 된 요소가 내용을 가리지 않도록 주의해야 한다.

* fixed나 sticky와 같이 스크롤에 관련된 요소는 브라우저와 기기의 성능에 따라 유지되지 못하는 접근성 문제가 발생할 수 있다고 한다.   

  => will-change: transform을 추가하는 방법이 있다고 한다. 이것은 직접 적용해보고 경험해봐야 알 것 같다.

  > will-change란?
  >
  > 요소에 예상되는 변화의 종류에 관한 힌트를 브라우저에게 알려주는 것이다. 실제 요소가 변화되기 전에 미리 브라우저는 적절하게 최적화할 수 있다. 그런데 이 속성을 너무 남발하면 그것도 문제가 될 수 있기 때문에 적당히 사용해야 한다.
  >
  > [will-change 설명](https://developer.mozilla.org/ko/docs/Web/CSS/will-change)



[position 관련 내용 참고](https://developer.mozilla.org/ko/docs/Web/CSS/position)
