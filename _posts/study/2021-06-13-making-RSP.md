---
layout: post
title:  "Javascript 가위바위보"
subtitle:   "Javascript 웹페이지 동적구성과 Dom객체의 이해"
categories: study
tags: JAVASCRIPT
comments: true
---




![ezgif.com-gif-maker](/assets/ezgif.com-gif-maker.gif)

---

**2020/6/13**
## 가위바위보 만들기 With Javascript

**개발도구**  
ATOM 1.58.0

### HTML

```

<!DOCTYPE html>
<html lang="ko" dir="ltr">
  <head>
    <meta charset="utf-8">
    <title>가위바위보 document객체를 이용하여 만들기</title>
    <link rel="index.css">
  </head>
  <body>
<section class = "game">

  <div class="palyer">
    <div class="user-palyer">
        <h3>사용자</h>

    </div>
    <div class="com-palyer">
        <h3>컴퓨터</h>

    </div>
  </div>

  <div class="intro fadeIn">
    <h1 class="winner">가위 바위 보!</h1>
    <button class="start_button">시작하기</button>
  </div>

  <div class="match fadeOut">
    <!--기본 그림은 주먹으로 시작하게 하기-->
    <div class="selectRSP">
        <img class ="user-select" type="image/png" src="rsp_rock_user.png" alt="">
        <img class ="com-select" type="image/png" src="rsp_rock_com.png" alt="">
    </div>

  <div class="options">

    <button id ="가위" class="가위">가위</button>
    <button id ="바위" class="바위">바위</button>
    <button id ="보" class="보">보</button>

  </div>



</section>
<script src="index.js"></script>
</body>
</html>

```

- 화면 구성은 div태그 전체를 section 태그로 두른 후
결과창 (사용자,컴퓨터) , 시작메뉴, 가위바위보 그림이 들어갈곳 , 가위바위보 선택 버튼
크게 전체 한개의 섹션을 만들고 안을 4개의  div tag로 구성했다.

<br />
<hr />

#### index.html 화면

![가위바위보 이미지구성](/assets/가위바위보%20이미지구성.png)

<p align="center">순수 html파일(사용자 계정명, 컴퓨터 계정명 , 가위바위보 문구(승패나타낼것) , 이미지 2개, 가위바위보 버튼 각 1개씩 으로 구성)</p>

<br/>

<hr/>



![가위바위보이미지](/assets/가위바위보이미지.png)
<p align="center">이미지 파일은 위의 가위바위보 소스를 이용했고, 무료 배포 이미지를 사용했다. 각각 손모양을 그림판으로 오려 사용했다.</p>

<br/>

![배경rgb](/assets/배경rgb.png)
<p align="center">RGB(161,219,231) 배경 이미지는 따로 없어서  그림 이미지와 RGB색을 맞춰서 CSS로 값을 주었다.</p>


<br/>

***

#### index.css

```

*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

section{
  height: 100vh;
  background-color: rgb(161,219,231);
}

.palyer {
  color: white;
  height: 20vh;
  display: flex;
  justify-content: space-around;
  align-items: center;
}

.palyer h3 {
  font-size: 30px;
}


.intro {
  color: white;
  height: 50vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-around;

}

.intro h1{
  font-size: 50px;
}

.intro button , .match button {
  width: 150px;
  height: 50px;
  background: none;
  border: none;
  color: white;
  font-size: 20px;
  background-color: rgb(151,185,230);
  border-radius: 5px;
  cursor: pointer;
}

.match{
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

.winner {
  color: white;
  text-align: center;
  font-size: 50px;
}

.selectRSP, .options{
  display: flex;
  justify-content: space-around;
  align-items: center;
}

#가위, #바위, #보 {
  width: 100px;
  font-weight: bold;
}

div.fadeOut{
  opacity: 0;
  pointer-events: none;
}


div.fadeIn{
  opacity: 1;
  pointer-events: all;
}

```

>float대신 빠르게 레이아웃을 구성하려고 flex로 레이아웃을 잡았고 내용과 아이템 정렬은 각각 space-around 속성과 center 속성으로 구성했다. 특별한 점은 div.fadein과 div.fadeout에 포인터 옵션을 주어 사용자가 클릭을 인지하게 하여 자바스크립트 코드 작성시 게임 시작과 게임 진행 구분을 클릭 이벤트(버튼 사라짐)를 통해 구성할 것이다.

​<br/>

* transform: translate(?%, ?%);  x,y 축으로 이동

* opacity : 요수의 불투명도 지정

* pointer : 마우스 위치시 손가락 모양 나오게함

<br />
<hr />

#### CSS를 적용한 화면

<br/>

**CSS적용된 HTML**
![css적용화면](/assets/css적용화면.png)

***

#### JAVASCRIPT

<br/>

**index.js**
입력대신 클릭 이벤트를 통해 버튼으로 가위바위보를 구현하였다.

```

var game = function() {

  //게임시작 함수
  var startGame = function() {
    var playBtn = document.querySelector('.intro button');
    var introScreen = document.querySelector('.intro');
    var match = document.querySelector('.match');


    playBtn.addEventListener('click' , function(){
      var hidebutton = document.querySelector('.intro .start_button').style.visibility = 'hidden';
      introScreen.classList.add('fadeOut');
      match.classList.add('fadeIn');
    });
  };
  //게임 진행시키기
  var playMatch = function(){
    options = document.querySelectorAll('.options button');
    //유저 클릭이벤트 결과
    userResult = document.querySelector('.user-select');
    //컴퓨터 클릭이벤트 결과
    comResult = document.querySelector('.com-select');

    //유저와 컴퓨터 선택
    var computerOptions = ['가위','바위','보'];
      //forEach를 통해 옵션(가위 바위, 보)에 클릭이벤트를 모두 부여
      options.forEach(option => {
      option.addEventListener('click', function(){

      //컴퓨터의 패 고르기(Math.random)
      var computerSelect = Math.floor(Math.random() * 3);
      var computerChoise = computerOptions[computerSelect];


     //함수 resultCompare() 호출 , 승/패 를 판단
      resultCompare(this.textContent, computerChoise);

      //여기서 this.는 사용자가 클릭으로 선택한 객체가 됨.  //누르는 것마다 이미지 변경하기위해 변수를 동적으로 함
      userResult.src = `rsp_${this.innerHTML}_user.png`;  //선택에 따른 이미지 주소 변경
      comResult.src = `rsp_${computerChoise}_com.png`;     //선택에 따른 이미지 주소 변경

      });
    });
};
//승패 여부
var resultCompare = function(playerChoice, computerChoice) {

  승/패 innerHTML의 텍스트를 담을 변수 winner 선언
  var winner = document.querySelector('.intro .winner');
  //무승부일시
  if (playerChoice === computerChoice) {
    winner.innerHTML = "무승부";
      return;
  }
  //유저가 바위일시
  if(playerChoice === '바위'){
    if(computerChoice === '가위'){
       winner.innerHTML = "사용자 승리";

       return;
    }else{
       winner.innerHTML ="컴퓨터 승리";
       return;
    }
  }
//유저가 보 일시
if(playerChoice === '보'){
  if(computerChoice === '바위'){
     winner.innerHTML = "사용자 승리";
     return;
  }else{
     winner.innerHTML ="컴퓨터 승리";
     return;
  }
}

//유저가 가위일시
if(playerChoice === '가위'){
  if(computerChoice === '보'){
     winner.innerHTML = "사용자 승리";
     return;
  }else{
     winner.innerHTML ="컴퓨터 승리";
     return;
  }
}
}





  //내부함수 부르기
  startGame();
  playMatch();

};
//겜 시작
game();


```

>실행 순서
game() -> startGame() -> playMatch() -> resultCompare()

​<br/>

주로 사용한 자바 스크립트 내장함수

- document.querySelector -HTML 요소를 가져오는데 사용했다.
- innerHTML - HTML태그내의 안의 내용을 String 값으로 출력
- addEventListener(이벤트 , 실행함수) - 이벤트 생성에 사용

---

**마무리**

원래 사용자의 '가위','바위','보' 입력을 받아 게임을 진행 시키려고 하였으나, dom객체와 이벤트를 배운 직후라 사용 빈도가 많은 Click 이벤트를 넣어보는게 더욱더 좋을거 같아서 클릭으로 진행되는 가위바위보 게임을 만들었는데, 훨씬 ui구성 적으로 괜찮았던거 같았다. 아직 능수능란하게 객체를 다룰 레벨은 아니였지만, 자바스크립트의 스코프 개념과 동작 방식을 좀 알 수 있었던 공부였다.
