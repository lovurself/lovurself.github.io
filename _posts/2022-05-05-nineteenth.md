---
layout: post
title:  "[JavaScript] Canvas API  사용해보기!"
date: 2022-05-05
---
2022-05-05



또또, 노마드 코더 강의를 들었는데 웹용 그림판을 만들어보았다. 강의를 토대로 클론코딩을 해보았고 어떻게 구현하는지 직접 만들어보았다. 작성한 코드 정리도 해보고 좀 더 공부해보려고 한다.



### Canvas API

= html에 canvas 태그와 Javacript를 사용하여 그래픽을 그리기를 할 수 있다. 애니메이션, 게임 그래픽, 데이터 시각화, 사진 조작, 실시간 비디오 처리를 위해 사용되기도 한다. 주로 2D 그래픽을 중점으로 사용되는데, WebGL API도 canvas 태그를 사용하여 2D나 3D 그래픽을 그릴 수 있다.



```html
<canvas id="canvas"></canvas>
```

html을 통해 #canvas라는 canvas를 만들어준다. 그리고 js에서 이 canvas를 불러온다.



```javascript
const canvas = document.getElementById('canvas');
const ctx = canvas.getContext('2d');
```

getContext 메소드로 렌더링될 그림의 대상을 지정하는데 context의 type을 지정해주어야 한다. 

contextType에는 다음 4가지가 있다.

1. 2d : 2d 객체를 생성한다.
2. webgl : 3차원 객체를 생성하며, WebGL의 버전 1을 구현하는 브라우저에서만 사용이 가능하다.
3. webgl2 : 3차원 객체를 생성하며, WebGL의 버전 2를 구현하는 브라우저에서만 사용이 가능하다.
4. bitmaprenderer : 비트맵 이미지로 대체하기 위한 객체를 생성한다.



이번에는 그림판을 구현해본거라 2d를 사용해보았다. 나중에 3d 객체도 만들어보는 것도 재밌을 것 같다.



### 그림판 구현 시 사용한 메소드 정리

1. canvas의 너비와 높이를 지정하기   

   => css로 크기를 지정하면 렌더링 시 좌표를 인식하지 못하기 때문에 css 외에 canvas 태그에 직접 width와 height를 지정하거나 js에서 canvas의 width와 height를 지정해줘야 한다. 그래야 css로 만들어준 그림판 크기 모두에 사용할 수 있다.

2. fillStyle와 strokeStyle   

   => fillStyle 메소드는 도형을 채우는 색을 설정하는 것이고, strokeStyle은 도형의 선 색을 설정하는 것이다. 이번에 그림판 구현할 때 fillStyle은 그림판 전체를 칠하는 것에 사용하였고, strokeStyle은 내가 그리는 선의 색깔을 설정할 때 사용했다.

   색상에 forEach를 사용하여 클릭 시 이벤트가 발생하게 하여 클릭한 색상을 fillStyle과 strokeStyle에 설정해주는 식으로 구현하였다.

3. fillRect   

   => fillRect(색상을 채우기 시작할 x좌표, y좌표, 채울 도형의 width, height) 로 설정 가능하며 이번에는 그림판 전체에 채우는 기능을 구현하였기 때문에 (0, 0, canvas.width, canvas.height)로 설정해주었다. reset 버튼을 클릭하면 초기화된 것처럼 보여주기 위해 다음과 같이 코드를 만들어보았다.

   ```javascript
   if (reset) {
       reset.addEventListener('click', handleReset);
   }
   
   const handleReset = () => {
       ctx.fillStyle = 'white';
       ctx.fillRect(0, 0, CANVAS_SIZE, CANVAS_SIZE);
   }
   ```

4.  lineWidth   

   => 선 굵기를 설정해준다. 설정값은 반드시 양수여야 하고, 초기 설정값은 1.0이다. lineCap은 선의 끝 모양, lineJoin은 선들이 만나는 모서리의 모양을 설정해준다는 것도 같이 알고 있으면 좋을 것 같다.

   선의 굵기를 설정할 때 알아두면 좋은 내용이 잘 정리된 [MDN](https://developer.mozilla.org/ko/docs/Web/API/Canvas_API/Tutorial/Applying_styles_and_colors#line_styles) 을 참고하면 좋을 것 같다! (중간에 lineWidth 예제 참고!!)

5. offsetX과 offsetY   

   => 선을 그을려면 canvas의 x, y좌표를 알아야 한다. 그러기 위해서 offset를 사용한다. offsetX는 x좌표를, offsetY는 Y좌표를 가져온다.

   ```javascript
   const x = canvas.offsetX;
   const y = canvas.offsetY;
   
   // 이때 좌표값은 계속 변화하는데 왜 let을 안썼는가?
   // 이유는 x,y 값을 계속 "업데이트"를 하는 것이면 let을 써야하지만
   // 여기서는 x,y값은 마우스가 움직일 때마다
   // 계속 새로 "만들어"내는 것이기 때문에 const를 사용하는 것이다.
   ```

6. beginPath와 moveTo / lineTo와 stroke   

   => beginPath는 새로운 경로를 만드는 것이고 경로가 생성이 되면 moveTo 메소드가 펜으로 x, y로 지정된 좌표로 옮긴다. 특정 시작점을 설정하기 위해 moveTo 메소드를 사용한다.

   lineTo는 현재의 드로잉 위치에서 x와 y로 지정된 위치까지 선을 그린다. 이전 경로의 끝점이 다음 그려지는 경로의 시작점이 된다. stroke은 선을 이용하여 도형을 그린다. lineTo는 fill이나 stroke와 함께 사용한다. 그래야 도형의 색상이 채워지든 선이 그려지기 때문이다.

   ```javascript
   let painting = false;
   
   const startPainting = (e) => {
       painting = true;
   }
   
   const onMouseMove = (e) => {
       const x = e.offsetX;
       const y = e.offsetY;
   
       // !painting은 painting이 false일 때라는 말이다.
       // painting이 false여야 !painting이 true가 되기 때문!
       if (!painting) {
           ctx.beginPath();
           ctx.moveTo(x,y);
       } else {
           ctx.lineTo(x,y);
           ctx.stroke();
       }
   	// mousedown이 되면 painting이 true가 되고
       // !painting은 false가 되므로 mousedown 동안 lineTo와 stroke로
       // 선이 그려지는 것이다!
   
   }
   
   // 이벤트 발생시키기
   canvas.addEventListener('mousemove', onMouseMove);
   canvas.addEventListener('mousedown', startPainting);
   
   // mousedown은 click과 다르게 처음 누르는 순간 시작하여 뗄때까지 계속 된다.
   ```



위의 메소드들을 이용하여 그림판 canvas를 구현해보았고 색상 변경이나 채우기 색상 선택, 내가 그린 그림 저장하기 등 다양한 기능을 구현하여 그림판을 만들어보았다.

재미있는 클론코딩이었고 다음에 내가 만들 웹페이지에도 이런 것들을 이용해보고 싶다.



[내가 만든 그림판 데모 사이트](http://heyminah.dothome.co.kr/painting_web/)

[내가 만든 그림판 코드](https://github.com/lovurself/Painting-web)

[자료 출처](https://developer.mozilla.org/ko/docs/Web/API/Canvas_API)

