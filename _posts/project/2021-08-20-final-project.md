---
layout: post
title: 반려동물 용품 판매 쇼핑몰
subtitle: bitcamp final project
categories: project
tags: project
comments: true
published: true
---
## 개요
> 2021.06.21 ~ 2021.08.20 진행된 비트캠프 웹 개발 과정 프로젝트 입니다.

- 목차
  1. 제작 동기 및 목표
  2. 개발환경 []()
  3. 프로젝트 일정
  4. ER 다이어 그램
  5. 화면 구현
  6. 마치며

---
## 제작동기 및 목표

프로젝트 구상시 새로운 아이템을 창출해 내기보다 학원에서 배운 내용이 모두 포함 되어 있으며
실무에도 많이 쓰는 로직이 포함된 쇼핑몰로 선정, 아이템은 반려동물 시장 급증과 팀원의 취향이 반영돼
프로젝트를 구상 하였음.

## Spring 의존 주입 관계도
![의존주입관계도](/assets/의존주입관계도.png)

***
## 개발 환경

Server : Java 1.8
웹 : Spring 4.x, Spring Boot 2.4.2 ,Spring Security 5.x
DB : Oracle 11g
Build : Maven
Client : Bootstrap

***
## 프로젝트 일정 ##

#### 2021/06/23 ~ 2021/08/20

![개발일정](/assets/개발일정.png)

***

## ERD
---
![petopia_ERD](/assets/petopia_ERD.png)

***


## 프로젝트 구성
---
- 프로젝트 구성

*.CLASS*
![본인이만든CLASS파일](/assets/본인이만든CLASS파일.png)

*.JSP*

![jsp본인분량](/assets/jsp본인분량.png)


***


## 화면구현
---
- ### 메인페이지
![main](/assets/main_sd7b6a1ct.png)

#### ① 로그인시 권한에 따라 상단 메뉴가 바뀝니다.
##### main.jsp 일부
```
//시큐리티 태그 라이브러리를 이용하여 유저를 3종류로 분류합니다.

 <sec:authorize access="isAnonymous()"></sec>
 <sec:authorize access="ROLE_MEMBER"></sec>
 <sec:authorize access="ROLE_ADMIN"></sec>

```

#### ② 상품검색
##### 상품을 검색 할 수 있습니다.

![상품검색설명](/assets/상품검색설명.png)
<hr />


- ### 상품
![메인페이지 구성](/assets/메인페이지%20구성.png)

#### ① 테마에 따라 리스트를 뿌립니다.( ex) 인기상품,추천상품... )


#### ② 오늘 본 상품(상품 클릭시 쿠키에 저장합니다.)
main.jsp 일부

쿠키 생성과 조회는 jquery 쿠키 라이브러리를 사용 했습니다.
데이터가 없다면 상품이 없다는 텍스트가 들어가고, 있다면 페이징 처리가 들어갑니다.
최근본 상품은 1페이지에 1개씩 뿌려집니다. , 후에 화면을 그려주는 함수를 호출합니다.

```
/

//쿠키가 있는지 확인후 없으면 빈배열을 만들고, 있으면 itemList 에 담습니다.
if($.cookie('itemList') == null){
            var itemList = [];   
            }else{
           var itemList = [];    
             itemList = JSON.parse($.cookie('itemList'));

            }
```

```


  if($("#noData").length == 0 && itemList == "null" ){
             $("#right_zzim ul").append('<p class="noData">최근 본 상품이<br> 없습니다.</p>');
             $("#paging").hide();
             $("#recentCnt").text('');

          }else if(itemList !=  "null") {
             var Cpage;   // 현재 페이지
             var pagingSize = 1;   
             function chkRecent(a){
             var itemID = JSON.parse($.cookie('itemList'));
             $("#right_zzim ul").html('');    
             if(itemID) {
                var list =  itemID.split(',');
                var totcount = itemID.length ;   //
                var totpage = Math.ceil(totcount / pagingSize) *1;

                console.log('totcount = ' +  totcount + "totpage = " + totpage);

                Cpage = (totpage >= a )? a:1;
                Cpage = (Cpage <1)? totpage:Cpage;
                console.log('현재페이지 = ' + Cpage);
                var start = (Cpage-1) * pagingSize;    

                for (i = start ; i <= start+(pagingSize-1) ;i++){
                var thisItem = itemID[i];
                   if(thisItem){
                      var itemId = thisItem.product_idx;
                      var itemImg = thisItem.fileName;
                   $("#right_zzim ul").append('<li><a href="#" target="_top"><img src="/petopia/images/'+itemImg+'" width="75" border=1></a><div class="detail"><a href="javascript:removeRecentItem(\''+thisItem+ Cpage +'\')" class="btn_delete">삭제</a></div></li>')

                   }
                }
                $("#paging").show();

```

#### ③ 클릭시 해당 상품으로 이동합니다.
main.jsp 일부

![상품하나보기](/assets/상품하나보기.png)

#### ④장바구니(비로그인/로그인 모두 사용)

main.jsp 일부
![장바구니AJAX](/assets/장바구니AJAX.png)
*비회원인 경우 JSESSIONID가 회원 아이디로 저장됩니다.

#### ⑤위시리스트(로그인유저만 사용)
장바구니와 마찬가지로 ajax송신을 통해 db에 저장됩니다.
장바구니와 분류는 cartType(1.장바구니 / 2.위시리스트) 로 분류합니다.

<hr/>

- ### 관리자페이지

#### 관리자 메인페이지
![어두민 메인](/assets/어두민%20메인.png)
간단한 관리자 관리용 정보와, 통계를 볼 수 있습니다.

#### 관리자 상품페이지
![어드민_상품](/assets/어드민_상품.png)
상품의 정보를 볼 수 있으며 필터검색이 가능합니다.
![상품필터정렬](/assets/상품필터정렬.png)
필터 정렬은 ajax송신을 통해 선택된 옵션에따라 정렬 방식을 바꾸어
리스트를 다시 뿌리는 방식으로 구현 하였습니다.

**상품등록**
![어드민 상품등록](/assets/어드민%20상품등록.png)
상품등록시 color_option을 제외한 모든 값은 필수 값이며, 파일첨부(이미지)의 썸네일을 볼 수
있도록 구현 하였습니다. 또한 간단한 유효성 검사를 넣어 올바른 값이 들어 갈 수 있도록 하였습니다.


**상세보기**
![어드민 상품 상세보기](/assets/어드민%20상품%20상세보기.png)
상품의 정보를 모달창을 띄워 상세 볼 수 있게 구현하였습니다.
수정버튼을 누를시 상품 수정 페이지로 이동합니다.



**상품수정/삭제**
상품의 수정,삭제가 가능합니다. ajax송신으로 구현하였습니다.
![상품수정ajax](/assets/상품수정ajax.png)
<br/>

#### 관리자 배송페이지
관리자가 배송현황을 확인하는 페이지이며, ajax송신으로 배송상태 변경이 가능합니다.
![어드민 배송](/assets/어드민%20배송.png)
![어드민 배송상태 변경](/assets/어드민%20배송상태%20변경.png)
<br/>

#### 관리자 회원 페이지
회원리스트 조회가 가능합니다.
![어드민_맴버](/assets/어드민_맴버.png)

회원 상세보기입니다. 회원의 삭제(탈퇴)가 가능합니다.
![어드민 회원보기](/assets/어드민%20회원보기.png)
<br/>

#### 관리자 주문 페이지
회원/비회원의 주문정보를 조회합니다.
![어드민 주문보기](/assets/어드민%20주문보기.png)
<br/>

#### 관리자 통계페이지
드롭다운 형식으로 선택된 통계 보기가 가능합니다.
chart.js 를 통해 구현하였습니다.

statisticsList.jsp 일부

1.ajax송신으로 데이터를 받아온다.


```

$.getJSON("http://localhost:8282/admin/getStatistics1", function(data){
  $.each(data, function(inx, obj){

    chartLabels1.push(obj.member_joindate);
    chartData1.push(obj.member_joincount);
    console.log(obj.member_joindate);

  });

  createChart();

  console.log("create Chart1")

});

```

2.차트의 큰 틀을 변수에 담아둔다.

```

var lineChartData1 = {

    labels : chartLabels1,

    datasets : [
            {
            label : "회원수",
            fillColor : "rbga(151,187,205,0.2)",
            strokeColor : "rbga(151,187,205,1)",
            pointColor : "rbga(151,187,205,1)",
            pointStrokeColor : "#fff",
            pointHighlightFill : "#fff",
            pointHighlightStroke : "rbga(151,187,205,1)",
            data : chartData1
            }

           ]
}

```

3. 차트를 그린다.

```

function createChart(){

  var ctx = document.getElementById("chart").getContext("2d");

  LineChartDemo = Chart.Line(ctx,{
    data : lineChartData1,
      options :{
        scales : {
          yAxes : [{
            ticks :{
            beginAtZero : true
          }
        }]
      }
    }
  })
}

});

```

결과화면
![통계보기](/assets/통계보기.png)



- ### 이벤트
 hangman(낱말 맞추기) 게임입니다.
 쇼핑몰 이름 'Petopia' 를 맞출시 정답이라는 메시지와 함께 포인트 적립창이 띄워집니다.

![event_hangman](/assets/event_hangman.png)
![event_result](/assets/event_result.png)

- ### 공지사항
관리자로 접속시 글을 남길수 있습니다.
데이터는 form전송 방식으로 구현하였습니다.

notice.jsp 일부

```
<sec:authorize access="hasRole('ROLE_ADMIN')">
		<div class="text-right">
		<a href="${root}/notice/register?board_id=1" class="btn btn-defalut">글작성</a>
		</div>
</sec:authorize>
```

![관리자공지사항](/assets/관리자공지사항.png)

또한 관리자가 글을 클릭했을시 아래와 같이 수정/삭제 버튼이 활성화됩니다.

```
<sec:authorize access="hasRole('ROLE_ADMIN')">							 
			<a href="${root }notice/modify?board_id=1&content_idx=${board.content_idx}">
					 <button class="btn btn-warning notice_button1">수정</button></a>

			<a id=removeButton href="${root}notice/remove?board_id=1&content_idx=${board.content_idx}">
						<button class="btn btn-danger notice_button2">삭제</button></a>
</sec:authorize>
```

![관리자공지사항글작성](/assets/관리자공지사항글작성.png)


- ### QnA
자주묻는질문,문의하기,문의내역조회,고객센터 탭으로 이루어져 있습니다.

![qnamain](/assets/qnamain.png)
.
![문의하기](/assets/문의하기_47m93i6bm.png)
문의하기는 회원 아이디로 접속시 id가 다음과 같이 자동으로 입력되며
문의 내용을 적을 수 있습니다.

![문의등록](/assets/문의등록_wpk2wxqhj.png)
등록시 등록완료라는 메시지와 함께 등록이 완료됩니다.
<hr/>

## 기타
전체 코드는 아래의 깃 주소에 있습니다.<br />
git: https://github.com/naru92/Petopia_project



**첫 프로젝트 이다 보니 어려운점도 많았고, 여러가지 어수선한 상황들이 겹쳐 만족하지 못하는 결과물이었지만
프로젝트 기간 중 많은걸 배웠습니다. 앞으로 어떤 프로젝트들과 업무를 접할진 모르겠으나, 지금 보다는 훨씬 더 좋은 결과물을 낼 수 있을거라는 자신감을 얻은 시간이었습니다.**
