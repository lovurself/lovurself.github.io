---
layout: post
title:  "[JavaScript] localStorage을 이제야 알게 되다니..."
date: 2022-04-26
---
2022-04-26



최근에 노마드 코더 니꼴라스님의 강의를 듣고 있는데 완전 신기한 걸 알게 되었다. 이걸 이제야 알게 된 걸 보면 그동안 공부를 제대로 안했나보다. 아무튼 localStorage에 대해 정리해보려고 한다.



## Web Storage API   

브라우저에서 키와 값의 쌍을 쿠키보다 훨씬 직관적으로 저장할 수 있다고 한다. Web Storage는 두가지 방식이 있고 Window 객체에 속성으로 포함되어 있다.

1. sessionStorage   

   => 브라우저나 탭이 닫힐 때까지만 데이터를 저장하고 데이터를 서버로 전송하지 않는다.

2. localStorage   

   => 유효기간 없이 데이터를 저장할 수 있고, 자바스크립트를 사용하거나 브라우저 캐시나 로컬 저장 데이터를 지워야지만 사라진다. 저장공간이 크다는게 장점이다.



**window.sessionStorage나 window.localStorage로 접근하면 Storage 객체에 뭐가 있는지 알 수 있다.**

[자료 출처](https://developer.mozilla.org/ko/docs/Web/API/Web_Storage_API)



### Storage   

= 특정 도메인을 위한 세션 저장소나 로컬 저장소의 접근 경로로, 데이터를 추가, 수정, 삭제를 할 수 있다.

도메인의 세션 저장소 수정은 sessionStorage, 로컬 저장소 수정은 localStorage에서.



### sessionStorage    

= 현재 페이지의 세션 저장 공간에 접근할 수 있는 객체

* 데이터는 브라우저나 탭에서 나가면 제거가 된다.
* 대신 브라우저나 탭이 열려있는 상태에서 새로고침이나 페이지 복구를 해도 남아 있다.
* 새로운 탭을 열면 최상위 브라우징 맥락의 값을 가진 새로운 세션을 생성한다.
* 같은 URL 주소를 가지고 있어도 탭을 열때마다 각각 새로운 sessionStorage를 가진다.
* 페이지 프로토콜별로 구분한다. 즉, HTTP와 HTTPS는 다른 세션에 저장된다.
* 키와 값은 항상 문자열로 저장하며, 정수는 자동으로 문자열로 변환해서 저장한다.

[자료 출처](https://developer.mozilla.org/ko/docs/Web/API/Window/sessionStorage)



### localStorage   

= 현재 페이지의 로컬 저장 공간에 접근할 수 있는 객체

* 현재 페이지를 나가도 로컬 저장소에 저장되어 있기 때문에 데이터는 사라지지 않는다. 
* 저장한 데이터는 브라우저 세션끼지 공유된다. 
* 만약에 '사생활 보호 모드'를 설정한 후 생성된 데이터는 탭이 닫힐 때 사라진다.
* 페이지 프로토콜별로 구분한다. 즉, HTTP와 HTTPS는 다른 세션에 저장된다.
* 키와 값은 항상 문자열로 저장하며, 정수는 자동으로 문자열로 변환해서 저장한다.



**localStorage 사용하기**   

1. setItem = 항목 추가   

   ```js
   localStorage.setItem('키', '값');
   ```

2. getItem = 항목 읽기   

   ```js
   const 변수명 = localStorage.getItem('키');
   ```

3. removeItem = 항목 제거   

   ```js
   localStorage.removeItem('키');
   ```

4. clear = 항목 모두 제거   

   ```js
   localStorage.clear();
   ```

[자료 출처](https://developer.mozilla.org/ko/docs/Web/API/Window/localStorage)



### 예제

노마드 코더 강의를 통해서 이름을 입력하면 그 이름을 저장해두고 인사말을 보여주는 것을 구현해보았다.

```js
const loginForm = document.querySelector('.login_form');
const loginInput = document.querySelector('.login_form input');
const greeting = document.querySelector('#greeting');

const HIDDEN_CLASSNAME = "hidden";
const USERNAME_KEY = "username";

const paintGreetings = (username) => {
    greeting.innerText = `반가워요! ${username}님`;
    greeting.classList.remove(HIDDEN_CLASSNAME);
}

const onLoginSubmit = (e) => {
    e.preventDefault();
    loginForm.classList.add(HIDDEN_CLASSNAME);
    const username = loginInput.value;
    localStorage.setItem(USERNAME_KEY, username); // localStorage 사용
    paintGreetings(username);
}

const savedUsername = localStorage.getItem(USERNAME_KEY); // localStorage 사용

if (savedUsername === null) {
    loginForm.classList.remove(HIDDEN_CLASSNAME);    
    loginForm.addEventListener("submit", onLoginSubmit);
} else {
    loginForm.classList.add(HIDDEN_CLASSNAME);
    paintGreetings(savedUsername);
}
```

