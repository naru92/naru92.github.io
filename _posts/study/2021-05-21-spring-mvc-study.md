---
layout: post
title: Spring MVC 기본기능 익히기
subtitle: 스프링 MVC 동작방식과 원리를 이해하기
categories: study
tags: SPRING
related_posts:
  - category/_posts/study/2021-05-22-spring-mvc-goodsPage.md
comments: true
---

![mvc모델](/assets/mvc모델_zn4v9dbv2.png)

<hr />

❗ 웰컴페이지 만들기
경로: main -> resources -> static -> index.html(생성)

<br />

<hr />




```

<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<ul>
    <li>로그 출력
        <ul>
            <li><a href="/log-test">로그 테스트</a></li>
        </ul>
    </li>
    <!-- -->
    <li>요청 매핑
        <ul>
            <li><a href="/hello-basic">hello-basic</a></li>
            <li><a href="/mapping-get-v1">HTTP 메서드 매핑</a></li>
            <li><a href="/mapping-get-v2">HTTP 메서드 매핑 축약</a></li>
            <li><a href="/mapping/userA">경로 변수</a></li>
            <li><a href="/mapping/users/userA/orders/100">경로 변수 다중</a></li>
            <li><a href="/mapping-param?mode=debug">특정 파라미터 조건 매핑</a></li>
            <li><a href="/mapping-header">특정 헤더 조건 매핑(POST MAN 필요)</a></
            li>
            <li><a href="/mapping-consume">미디어 타입 조건 매핑 Content-Type(POST
                MAN 필요)</a></li>
            <li><a href="/mapping-produce">미디어 타입 조건 매핑 Accept(POST MAN
                필요)</a></li>
        </ul>
    </li>
    <li>요청 매핑 - API 예시
        <ul>
            <li>POST MAN 필요</li>
        </ul>
    </li>
    <li>HTTP 요청 기본
        <ul>
            <li><a href="/headers">기본, 헤더 조회</a></li>
        </ul>
    </li>
    <li>HTTP 요청 파라미터
        <ul>
            <li><a href="/request-param-v1?username=hello&age=20">요청 파라미터
                v1</a></li>
            <li><a href="/request-param-v2?username=hello&age=20">요청 파라미터v2</a></li>
            <li><a href="/request-param-v3?username=hello&age=20">요청 파라미터
                v3</a></li>
            <li><a href="/request-param-v4?username=hello&age=20">요청 파라미터
                v4</a></li>
            <li><a href="/request-param-required?username=hello&age=20">요청
                파라미터 필수</a></li>
            <li><a href="/request-param-default?username=hello&age=20">요청
                파라미터 기본 값</a></li>
            <li><a href="/request-param-map?username=hello&age=20">요청 파라미터
                MAP</a></li>
            <li><a href="/model-attribute-v1?username=hello&age=20">요청 파라미터
                @ModelAttribute v1</a></li>
            <li><a href="/model-attribute-v2?username=hello&age=20">요청 파라미터
                @ModelAttribute v2</a></li>
        </ul>
        </li>
          <li>HTTP 요청 메시지
              <ul>
                  <li>POST MAN</li>
              </ul>
          </li>
          <li>HTTP 응답 - 정적 리소스, 뷰 템플릿
              <ul>
                  <li><a href="/basic/hello-form.html">정적 리소스</a></li>
                  <li><a href="/response-view-v1">뷰 템플릿 v1</a></li>
                  <li><a href="/response-view-v2">뷰 템플릿 v2</a></li>
              </ul>
          </li>
          <li>HTTP 응답 - HTTP API, 메시지 바디에 직접 입력
              <ul>
                  <li><a href="/response-body-string-v1">HTTP API String v1</a></li>
                  <li><a href="/response-body-string-v2">HTTP API String v2</a></li>
                  <li><a href="/response-body-string-v3">HTTP API String v3</a></li>
                  <li><a href="/response-body-json-v1">HTTP API Json v1</a></li>
                  <li><a href="/response-body-json-v2">HTTP API Json v2</a></li>
              </ul>
          </li>
      </ul>
    </body>
  </html>

```
<br />

<hr />

**로깅 간단히 알아보기**

- 실무에선 System.out.pirntln(); 을 쓰지않는다, loging으로 테스트를함(메모리 효율)
- SLF4J 는 인터페이스
- Logback 은 로그라이브러리 구현체 Spring boot에선 대부분 이걸 사용

> 로그 만들어보기
디렉토리 : Springmcv -> basic -> LogTestController.class(생성)


```

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class LogTestController {
    private final Logger log = LoggerFactory.getLogger(getClass());
}

```

-	Logger 생성자 호출 slf4j 를 임포트 할 것에 주의!

___


```

@RestController
public class LogTestController {
    private final Logger log = LoggerFactory.getLogger(getClass());

    @RequestMapping("/log-test")
    public String logTest(){
        String name = "Spring";

        System.out.println("name = " + name); //SysOut
        log.info(" info log={}", name); // log

        return "ok";
    }
}


```

위와 같이 코드를 추가했다.
@RestController 란 리턴값이 문자면 그 문자를 메시지 바디에 넣어 바로 반환해준다.

**테스트**
http://localhost:8080 에 들어가 로그테스트를 해보자

![로그출력](/assets/로그출력.png)

클릭시 return값 ok가 출력된것으로 보아 테스트에 성공했다.

**비교**

```
name = Spring //SysOut 결과   
```

```
name = Spring
        2021-05-21 04:22:48.399  INFO 26864 --- [nio-8080-exec-5] hello.springmvc.basic.LogTestController  :  info log=Spring
        //log 결과

```

로거로 실행한 결과가 일반출력보다 많은 정보 시간, 현재출력한 쓰레드 등등을 알려준다.

<hr />

**application.properties**

```

#hello.springmvc 패키지와 그 하위로그 레벨 설정
logging.level.gello.springmvc = info <- 운영서버는 보통 info레벨로 설정


```

```

log.info(" info log={}", name); <<- {} 하나당 , name 처럼 쉼표로 구분하여 더 넣을수 있음.

```

<br />

<hr />


**요청 매핑**
Basic -> requestmapping(패키지생성) -> MappingController(클래스 생성)

@RequestMapping(“/hello-basic”)

-	URL 호출이 오면 이 메서드가 실행되도록 매핑
-	배열로도 제공되기 떄문에 2개이상의 매개변수를 주어도 된다 { }로 기술

**POSTMAN 으로 테스트해보기**(개발한 API를 테스트(URL로 신호를 보내는 행위)하고, 테스트 결과를 공유하여 API 개발의 생산성을 높여주는 플랫폼)

RequestMapping이기 때문에
![리퀘스트맵핑get](/assets/리퀘스트맵핑get.png)
GET으로 보내도 “OK”
![리퀘스트맵핑post](/assets/리퀘스트맵핑post.png)
POST로 보내도 “OK”

> @RequestMapping은 메서드를 지정해주지 않으면 GET,POST,DLELTE,PUT… 종류와 상관없이 모든 메서드를 받는다.
>
>따라서 원하는 메서드를 지정해서 받기 위해선 아래와 같이
>
>@RequestMapping(value = "/hello-basic" , method = RequestMethod.GET)
Method = RequestMethod.원하는메서드 를 지정해주면 된다.

</br>

<hr />

만약 @RequestMapping(value = "/hello-basic" , method = RequestMethod.GET)와 같은 방법으로
get메서드를 지정시 get방식 호출만 가능하다.

<hr />

**GET 요청**

![리퀘스트겟맵핑ok](/assets/리퀘스트겟맵핑ok.png)
![ok](/assets/ok.png)

>get은 ok가 잘 return됨.

<br />

<hr />

**POST 요청**

![리퀘스트mapping post거절](/assets/리퀘스트mapping%20post거절.png)
![post_method_not_allowed](/assets/post_method_not_allowed.png)

>post요청시 method Not Allowed 해당 요청은 허용되지 않는다는 에러 메시지가 나온다.


위와 같이 메서드를 지정 해줄수도 있지만 **@GetMapping , @PostMapping , @PutMapping, @DeleteMapping, @PaychMapping을 사용**하여 @RequestMapping 대신 사용해 축약 표현도 가능하다.

<br/>

<hr />

**GetMapping의 사용**

```

@GetMapping(value = "mapping-get-v2")
public String mappingGetV2() {
    log.info("mapping-get-v2");
    return "ok";
}

```

@GetMapping – url: “mapping-get-v2” 로 get 메시지를 받아보자.

![@getmapping](/assets/@getmapping.png)

로 보낸 결과 “ok”가 잘 출력됐다. @RequestMapping보다 훨씬 더 직관적이다.
원리는 @GetMapping api문서에 들어가보면 내용에 RequestMethod.GET 이 단순히 설정 되어있다. 편의를 위해 제공하는 것 같다.

___

<br />

#### PathVariable의 사용

@PathVariable(경로 변수) 사용( **중요! URL설계의 핵심!!** )
-URL경로를 탬플릿 형식으로 사용, 값을 PathVariable으로 꺼낸다. 많이 사용하는 방법이다.

```

@GetMapping("/mapping/{userId}")
public String mappingPath(@PathVariable("userId") String data){
    log.info("mappingPath userId={}", data);
    return "ok";
}

```

![@PathVariable(경로 변수) 사용](/assets/@PathVariable(경로%20변수)%20사용.png)

@GetMapping으로 URL주소 mapping/{userId} 를 줬다. 여기 중괄호 PATH안에는 사용자가 URL에 직접 입력하는 값이 PathVariable로 인해 꺼내진다.(위의 실습에선 kang이 변수 {userId} 임)

url주소에 ‘kang’ 을 입력하고 겟방식으로 포스트맨으로 요청을 보냈다.
리턴값 “ok”가 뜨고, 	
h.s.b.requestmapping.MappingController   : mappingPath userId=kang
출력창에 내가 설정한 userid라는 경로에 , kang이 잘 출력됐다.

최근 HTTP API는 위 처럼 리소스 경로에 식별자를 넣는 스타일을 선호 한다고 한다.
비슷한 방법으로 ?useriD=userKang 의 쿼리 파라미터 형식으로 보내는 방법도 있다.

**변수명이 같으면 생략이 가능**

```

@GetMapping("/mapping/{userId}")
public String mappingPath(@PathVariable String userId){
    log.info("mappingPath userId{}", userId);
    return "ok";
}


```

> @GetMapping mapping url인 userId라는 url mapping 값과
@PathVariable의 변수명 userId가 같기 때문에 이전처럼 문제없이 잘 동작했다.

**다중 @PathVariable도 가능하다.**

```

@GetMapping("/mapping/users/{userId}/orders/{orderId}")
public String mappingPath(@PathVariable("userId") String userId, @PathVariable("userId") Long orderId) {
    log.info("mappingPath userId={}, orderId={}", userId,orderId);
    return "ok";
}


```

테스트 결과
requestmapping.MappingController : mappingPath userId=kang, orderId=100
![다중pathvarialbe](/assets/다중pathvarialbe.png)

다중URL도 PathVariable로 템플릿에서 꺼내 잘 출력이 된걸 확인 할 수 있다.

그 밖에 파라미터로 추가 매핑도 가능하다(사용 잘 안함)

```

/**
 * 파라미터로 추가 매핑
 * params="mode",
 * params="!mode"
 * params="mode=debug"
 * params="mode!=debug" (! = )
 * params = {"mode=debug","data=good"}
 */
@GetMapping(value = "/mapping-param", params = "mode=debug")
public String mappingParam() {
    log.info("mappingParam");
    return "ok";
}


```

매개변수 params = “mode=debug”의 뜻은 파라미터에 mode = debug 가 존재한다면 이 메서드가 호출이 된다.

![params 사용](/assets/params%20사용.png)

> 위와 같이 url값을 포스트 맨에 넘기고 get으로 요청하면
requestmapping.MappingController   : mappingParam 과같이 메소드가 호출돼서 출력이 된다.

<br />

<hr />

**특정 헤더로 매핑하는 방법**

```

/**
 * 특정 헤더로 추가 매핑
 * headers="mode",
 * headers="!mode"
 * headers="mode=debug"
 * headers="mode!=debug" (! = )
 */
@GetMapping(value = "/mapping-header", headers = "mode=debug")
public String mappingHeader() {
    log.info("mappingHeader");
    return "ok";
}

```

![header로매핑](/assets/header로매핑.png)

Http 헤더 정보에 “mode=debug”가 있다면 위의 메서드가 호출될것이다.
우선 postman으로 헤더값에 를 셋팅 해주고, url를 호출해 보면

> requestmapping.MappingController: mappingHeader 과 같이 매핑이 잘 되어 메서드가 호출 된다.

<hr />

<br/>

**컨텐츠 타입 헤더로 매핑하는 방법**

consumes = “application/json”의 뜻은 헤더의 컨텐츠 타입이 json일때만 호출된다. 라는 뜻이다.

![consume](/assets/consume.png)
테스트를 위해 포스트맨의 헤더 정보에 json이라 설정 한 후 URL에 요청을 보냈다.

![consumeOK](/assets/consumeOK.png)

> 결과 : requestmapping.MappingController : mappingConsumes 이 출력된것으로 보아 요청이 성공적으로 갔다. 만약 요청이 실패하면 HTTP 상태코드(Unsupproted Media Type) 415를 반환 했을 것이다.

___

<br />

**미디어 타입을 맞춰야 호출이 되는 Accept 헤더 기반으로 매핑하는 방법**

```

@PostMapping(value = "/mapping-produce", produces = "text/html")
public String mappingProduces() {
    log.info("mappingProduces");
    return "ok";
}

```

미디어 타입이 “text/html”이면 메서드가 호출된다.

![produces](/assets/produces.png)
다음 url에 요청을 보냈다.

>requestmapping.MappingController : mappingProduces 호출에 성공하여 매핑 결과가 호출되었다.

<br/>

![Accept모두](/assets/Accept모두_lslnhrinq.png)
포스트 맨의 설정을 살펴보니 위와같이 Accept 범위가 */*이라 모든 미디어 타입을 포함했다.
Aceept를 json으로 바꾸고 실습해보니 406, Not Acceptable 에러가 뜨는 것을 확인할수 있었다.

>*미디어 타입은 스프링에 상수로 셋팅 되어 있어서 위에 실습처럼 produces = "text/html"
라고 적는 것 보다는 MediaType.TEXT_HTML_VALUE 처럼 상수로 적는 것이 더 바람직 하다.*

___

<br />

**요청 매핑 – API 설계 예시**

-	만약 내가 회원 관리를 HTTP API를 만든다 생각하고 매핑을 해보는 실습
-	실제 데이터는 넘기지 않고 URL 매핑만 해보기

### 회원 관리 API

- 회원 목록 조회: GET /users
- 회원 등록: POST /users
- 회원 조회: GET /users/{userId}
- 회원 수정: PATCH /users/{userId}
- 회원 삭제: DELETE /users/{userId}

디렉토리: basic -> requestmapping(패키지) -> MappingClassController 생성

```

@GetMapping("/mapping/users")
public String user() {
 return "get users";
}
@PostMapping("/mapping/users")
public String addUser() {
    return "post user";
}
@GetMapping("/mapping/users/{userId}")
public String findUser(@PathVariable String userId) {
    return "get userId =" + userId;
}

@PatchMapping("/mapping/users/{userId}")
public String updateUser(@PathVariable String userId){
    return "get userId =" + userId;
}
@DeleteMapping("/mapping/users/{userId}")
public String deleteUser(@PathVariable String userId){
    return "delete userId=" + userId;
}

```

이제 postman으로 하나씩 요청을 보내보자. 맵핑만 할거니까 리턴값으로는 메시지를 줘서 잘되는지 확인 했다.

<br />

___

**회원 목록조회 호출**

<p align="left">
<img src="/assets/get%20users.png">
</p>

/mapping/users (get)

<br />

**회원등록 호출**

<p align="left">
<img src="/assets/postUsers.png">
</p>

/mapping/users (post)

<br />

**회원 조회 호출**
<p align="left">
<img src="/assets/get%20users{userId}.png">
</p>

/mapping/users/Kangnaru (get)

<br />

**회원 수정 호출**
<p align="left">
<img src="/assets/update.png">
</p>


/mapping/users/Kangnaru (patch)

<br />

**회원 삭제 호출**

<p align="left">
<img src="/assets/delete.png">
</p>

/mapping/users/Kangnaru (delete)

<hr />

5개 메서드 호출 결과 모두 알맞은 매핑에 잘 호출 됐다!
근데 보면 **/mapping/users/** URL이 모두 포함되어 중복되는 것을 확인할수 있는데, 이렇게 중복되는 URL을 묶어보자.

```

@RestController
@RequestMapping("/mapping/users/")

```

<hr />

위와같이 클래스 위에 **@RequestMapping(“중복되는 url”)**
나의 경우 /mapping/users/를 추가해준뒤 매핑에 준 중복된 URL값을 삭제해주면 된다!


**변경 후**

```

@GetMapping
public String user() {
 return "get users";
}
@PostMapping
public String addUser() {
    return "post user";
}
@GetMapping("/{userId}")
public String findUser(@PathVariable String userId) {
    return "get userId =" + userId;
}

@PatchMapping("{userId}")
public String updateUser(@PathVariable String userId){
    return "update userId =" + userId;
}
@DeleteMapping("{userId}")
public String deleteUser(@PathVariable String userId){
    return "delete userId=" + userId;
}


```

>깔끔해졌다!
요즘은 실무에서도 리소스를 계층 방식으로 사용을 하기 때문에 잘 숙지해두자!

중복되는 URL 지운 @GetMapping을 TEST 해보자
    ![ok](/assets/ok_fkpui826x.png)     잘 동작하는 것을 확인했다.


- 매핑 방법을 공부 했으니 다음은 HTTP 요청이 보내는 데이터들은 스프링 MVC로 어떻게 조회하는지 알아보자


**HTTP 기본 헤더 조회해보기**

디렉토리: basic -> requestMapping - > RequestHeaderController(클래스 생성)

```

public class RequestHeaderController {

    @RequestMapping("/headers")
    public String headers(HttpServletRequest request,
                     HttpServletRequest response,
                     HttpMethod httpMethod,
                     Locale locale,
                     @RequestHeader MultiValueMap<String, String> headerMap,
                     @RequestHeader("host") String host,
                     @CookieValue(value = "myCookie", required = false) String                   cookie){

        log.info("request={}", request);
        log.info("response={}", response);
        log.info("httpMethod={}", httpMethod);
        log.info("locale={}", locale);
        log.info("headerMap={}", headerMap);
        log.info("header host={}", host);
        log.info("myCookie={}", cookie);

        return "ok";
    }


```

위와 같이 스프링은 헤더에 대한 많은 정보를 조회 할수 있다. POST맨으로 URL에 요청을 해보자.

![헤더조회](/assets/헤더조회.png)

>Request , response = 앞 전의 httpServletRequest,Response와 동일
>Locale = ko_KR 가장 순위가 높은 지역이 지정됨
>HeaderMap : 콘텐츠 타입, aceept 등
>Header host = 호스트명,포트
>MyCookie =쿠키정보

*참고*
```

MultiValueMap<String, String> map = new LinkedMultiValueMap();
map.add("keyA", "value1");
map.add("keyA", "value2");
//[value1,value2]
List<String> values = map.get("keyA");

```

>MultiValueMap MAP과 유사한데, 하나의 키에 여러 값을 받을 수 있다. HTTP header, HTTP 쿼리 파라
>미터와 같이 하나의 키에 여러 값을 받을 때 사용한다.
>- keyA=value1&keyA=value2
// “keaA”를 넣으면 값 value1,vlaue2가 나온다.

<br />

<hr />

**HTTP요청 파라미터 – 쿼리 파라미터, HTML Form 방식 공부**

클라이언트 -> 서버로 요청을 보낼 때 다음 3가지 방법을 사용한다.

-	GET - 쿼리 파라미터
/url?username=hello&age=20
바디 없이, URL의 쿼리 파라미터에 데이터를 포함해서 전달
예) 검색, 필터, 페이징등에서 많이 사용하는 방식

<br />

-	POST - HTML Form
content-type: application/x-www-form-urlencoded
메시지 바디에 쿼리 파리미터 형식으로 전달 username=hello&age=20
예) 회원 가입, 상품 주문, HTML Form 사용

<br />

-	HTTP message body에 데이터를 직접 담아서 요청
HTTP API에서 주로 사용, JSON, XML, TEXT
데이터 형식은 주로 JSON 사용 POST, PUT, PATCH

**요청 파라미터 조회하기**
디렉토리 : basic -> request(패키지 생성) -> RequestHeaderController(클래스 만들기)

>요청 파라미터 - 쿼리 파라미터, HTML Form
>
>HttpServletRequest의 request.getParameter() 를 사용하면 get방식과 post방식을 처리 해줄수 있음 , 왜냐면 둘다 형식이 같으므로 구분없이 조회가 가능함. 이것을 간단히 요청 파라미터(request parameter) 조회라고 함.

<hr />

#### requestParamV1

```

@RequestMapping("request-param-v1")
public void requestParamV1(HttpServletRequest request, HttpServletResponse response) throws IOException {
    String username = request.getParameter("username");
    int age = Integer.parseInt(request.getParameter("age"));
    log.info("username ={}, age = {}" , username, age);

    response.getWriter().write("ok");
}

```


단순하게 HttpServletRequest가 제공하는 방식으로 요청 파라미터를 조회 했음.

<hr />

post방식도 테스트 하기위해 테스트용 HTML Form도 만들어보자.
리소스는 /resoureces/static 아래에 두면 스프링이 관리 하기 떄문에 자동으로 인식이됨
여기에 hello-form 이라는 html 폼을 만들어 사용함.

#### hello-form.html

```

<!DOCTYPE html>
<html>
<head> <meta charset="UTF-8">
  <title>Title</title>
</head>
<body>
<form action="/request-param-v1" method="post">
  username: <input type="text" name="username" />
  age: <input type="text" name="age" />
  <button type="submit">전송</button>
</form>
</body>

```

#### requestParamV2

```

@ResponseBody
@RequestMapping("/request-param-v2")
public String requeestParamV2(
        @RequestParam("username") String memberName,
        @RequestParam("age") int memberAge) {
    log.info("username = {} , age = {}" , memberName, memberAge);
    return "ok";
}

```

> HTTP 요청 파라미터 - @RequestParam
스프링이 제공하는 @RequestParm을 사용하여 요청 파라미터를 읽었다.

- @ResponseBody 추가 : view조회를 무시하고 , HTTP 메시지 바디에 직접 해당 내용을 넣음
- @RequestParam : 파라미터 이름으로 값을 바인딩(배정)
- @RequestParam(“username”) String memberName은 v1의 request.getParameter(“username”)과 같은 기능!

#### requestParamV3

```

@ResponseBody
@RequestMapping("/request-param-v3")
public String requeestParamV3(
        @RequestParam String username, //생략시 변수명이 같아야함
        @RequestParam int age) {

    log.info("username = {} , age = {}" , username, age);
    return "ok";

}

```

> V2와 똑같이 @RequestParam을 사용했다. 하지만 parameter와 변수명이 같다면 v2처럼
RequestParam(“username”)의 파라미터 안에 username을 생략하고 위의 코드 처럼 쓸 수 있다!

#### requestParamV4

```

@ResponseBody
@RequestMapping("/request-param-v4")
public String requeestParamV4(String username, int age ) {
    log.info("username = {} , age = {}" , username, age);
    return "ok";

}

```


>이번엔 @RequestParam 에노테이션을 삭제하고 , 맞바로 메서드에 username과 age를 파라미터 값으로 줬다.
**참고!**  String, int , Interger의 기본 데이터 타입이면 @RequestParam이 생략 가능하다.
이렇게 @RequestParam을 생략 하면 스프링 MVC내부에서 required=false 를 적용한다. 파라미터에 값을 줘도 되고 안줘도 된다는 뜻이다.
>
>**하지만** 위와 같은 방법은 너무 생략이 일어나, 명확하게 요청 파라미터에서 데이터를 읽는 다는것을 모를 수 있으니 requestParamV3 방법이 제일 무난하게 쓰이는 것 같다.


**파라미터 필수 여부 – requestParamRequired**

```

@ResponseBody
@RequestMapping("/request-param-required")
public String requeestParamrequired(
        //true가 기본값 요청파라미터에 값이 없으면 badrequest 응답
        //false이지만 int의 기본데이터형인 경우 값을 안줬을시 null이 들어가기 떄문에 500에러가 발생
        //required가 true 이고 받는 데이터가 String인데 ""가(빈문자열) 들어온다면? 그냥 빈문자로 통과된다.
        @RequestParam(required = true) String username,
        @RequestParam(required = false) int age) {
    log.info("username = {} , age = {}", username, age);
    return "ok";
}

```

>앞에서 required = false가 된다 했는데 이 뜻은 파라미터가 없어도 된다는 말이다
반대로 required = true면 파라미터 기본값이 필수로 들어 가야하고, 파라미터 값을 주지 않으면
예외 400 에러코드가 발생한다.

**실습**

![겟파라미터값안줌](/assets/겟파라미터값안줌.png)
http://localhost:8080/request-param-required? 의 매핑값으로 ?뒤의 파라미터 값을 주지 않았을시
 위와같 요청이 올바르지 않다는 에러가 발생한다.

다시 요청 파라미터 필수 값인 유저 네임을 주고 테스트 해보자.
http://localhost:8080/request-param-required?username=hello&age=20 - username값을 줬다 age는 false기 떄문에 안줘도 된다.

![ok](/assets/ok_1vqfwqlif.png)
요청 파라미터를 주니 정상적으로 ok가 리턴된다.

💥주의💥 - **파라미터 이름만 있고 값이 없는 경우는 빈문자로 통과한다.**
> /request-param?username=

와 같이 =뒤에 아무것도 주지 않은경우 오류가 발생하지 않고 빈 문자가 출력된다.

💥주의💥 – **기본형 타입에 null입력**
> /request-param 요청
@RequestParam(required = false) int age

일 때 null을 int에 입력하는 것은 불가능 하다(500 예외 메시지 발생)
따라서 null을 받을 수 있는 Integer로 변경해야한다. 아니면 @RequestParam에 기본값을 주면 된다.

**기본 값 적용 - requestParamDefault**

```

@ResponseBody
    @RequestMapping("/request-param-default")
    public String requeestParamreDefault(
           //default value = 파라미터의 값이 안넘어 왔을시 설정할 기본값
           //requried를 안넣어도됨, 디폴트 벨류가 있기 떄문에 의미가없음
           //defualut value는 빈문자 열에도 기본값이 들어감
            @RequestParam(required = true, defaultValue = "guest") String username,
            @RequestParam(required = false, defaultValue = "-1") int age) {

        log.info("username = {} , age = {}" , username, age);
        return "ok";
}

```

>파라미터에 값이 없는 경우 defaultValue를 사용해 기본값을 적용 할 수 있다.
defaultValue사용시 사실상 requried는 의미가 없다. 또 defaultValue는 빈 문자 경우에도 설정한 기본 값이 들어간다.

<br />

**파라미터를 Map으로 조회하기 – requestParamMap**

```

@ResponseBody
@RequestMapping("/request-param-map")
public String requeestParamreMap(@RequestParam Map<String, Object> paramMap){
    //파라미터의 값이 1개가 확실하다면 Map 을 사용해도 되지만 그렇지 않다면 'MultiValueMap을 사용하자
    //근데 보통 파라미터 값은 1개를 사용하는게 일반적
    log.info("username = {} , age = {}" , paramMap.get("username"),paramMap.get("age"));
    return "ok";
}

```

**HTTP 요청 파라미터 -@ModelAttribute**

실제 개발 요청시 요청 파라미터를 받아서 필요한 객체를 만들고 그 객체에 set(값을 넣어주어야) 한다. 보통 다음과 같은 코드로 값을 넣어줘야 한다.

```

@RequestParam String username;
@RequestParam int age;
HelloData data = new HelloData();
data.setUsername(username);
data.setAge(age);

```

> 하지만 스프링은 @ModelAttribute 에노테이션을 통해 자동으로 이 과정을 스킵한다.
테스트를 위해 HelloData 객체를 만들자

```

HelloData

import lombok.Data;

@Data
public class HelloData {
    private String username;
    private int age;
}

/* import  - lombok.Data <- lombok 스프링에서 거의 필수 아이템
@Getter, @Setter, @Tostring, @EqualsAndHashCode, @RequiredArgsConStructor을 자동적용 */

@ResponseBody
@RequestMapping("/model-attribute-v1")
public String modelAttributeV1(@ModelAttribute HelloData helloData){

log.info("username = {} , age = {}" , helloData.getUsername(),helloData.getAge());
    return "ok";
}

```

메서드 파라미터로 @ModelAttribute를 선언하고 그 안에 방금 만든 HelloData 객체를 넘겼다.
그 다음에 객체 변수로 객체 생성 없이 .getUsername, .getAge로 값을 출력 할 수 있었다.

즉 스프링 MVC는 @ModelAttribute가 있으면 다음과 같은 과정을 거친다.
1.	사용자가 파라미터에 준 HelloData객체를 자동으로 생성한다.
2.	요청 파라미터의 이름으로 HelloData의 프로퍼티를 찾는다. 위에선(username,age)
그리고 해당 프로퍼티의 setter를 호출해서 값을 입력(바인딩) 한다.

<br />

**프로퍼티**

> 예를들어 객체에 getUserName, setUserName 메서드가 있으면 이 객체는 username이라는 프로퍼티를 가지고 있다 라고 말한다.

```

@ModelAttribute 생략 - modelAttributeV2
@ResponseBody
@RequestMapping("/model-attribute-v2")
public String modelAttributeV2(HelloData helloData){
    //생략해도 가능하다;;
    log.info("username = {} , age = {}" , helloData.getUsername(),helloData.getAge());
    return "ok";
}

```

@ModelAttribute도 생략이 가능하다. 그런데 @RequestParam도 생략 할수 있으니 혼란이 발생한다. 스프링은 생략시 다음과 같은 규칙을 적용한다.

> String , int , Integer와 같은 단순 타입 = @RequestParam 적용
나머지 = @ModelAttribute 적용
