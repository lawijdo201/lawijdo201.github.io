---
title: 'jQuery&Ajax'
date: 2022-10-13 00:00:00
featured_image: 
excerpt: jQuery, Ajax
---

제이쿼리
================

화면의 동적 기능을 자바스크립트보다 좀 더 쉽고 편리하게 개발할 수 있게 해주는 자바스크립트 기반 라이브러리

제이쿼리 특징
-----------------------

* CSS 선택자를 사용해 각 HTML 태그에 접근해서 작업하므로 명료하면서도 읽기 쉬운 형태로 표현함
* 메서드 체인 방식으로 수행하므로 여러 개의 동작(기능)이 한 줄로 수행할 수 있음
* 풍부한 플러그인을 제공하므로 이미 개발된 많은 플러그인을 쉽고 빠르게 이용할 수 있음
* 크로스 브라우징을 제공하므로 브라우저 종류에 상관 없이 동일하게 기능을 수행함

제이쿼리 CDN 호스트 설정 방법
-------------------------

```javascript
<script src = "http://code.jquery.com/jquery-2.2.1.min.js"></script>
```

* 지정한 버전의 제이퀴리를 사용합니다

```javascript
<script src = "http://code.jquery.com/jquery-latest.min.js"></script>
```

* 가장 최신 버전의 제이쿼리를 사용합니다.

제이퀘리의 여러 가지 선택자
--------------------------

|선택자 종류|선택자 표현 방법|설명|
|----------|---------------|----|
|All selector|$("\*")|모든 DOM을 선택합니다.|
|ID Selector|$("#id")|해당되는 id를 가지는 DOM을 선택합니다.|
|Element selector|$("elementName")|해당되는 이름을 가지는 DOM을 선택합니다.|
|class selector|$(".className")|CSS중 해당되는 클래스 이름을 가지는 DOM을 선택합니다.|
|Multiple selector|$("select1, select2, <br> select3, ..., selectN")|해당되는 선택자를 가지는 DOM을 선택합니다.|

jQuery예시
-----

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>ID 셀렉터 연습1</title>
<script  src="http://code.jquery.com/jquery-2.2.1.min.js"></script>
<script type="text/javascript"> 
$(document).ready(function(){				
  alert($("#unique2").html());	
});
</script>
</head>
<body>
  <div class="class1">안녕하세요.</div>
  <div id="unique2">제이쿼리입니다!!</div>
  <div id="unique3">
     <p>제이쿼리는 아주 쉽습니다!!!</p> 
  </div>
</body>
</html>
```

jQuery 두번째 예시
-----

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>ID 셀렉터 연습1</title>
<script  src="http://code.jquery.com/jquery-2.2.1.min.js"></script>
<script type="text/javascript"> 
$(document).ready(function(){				    //페이지 로딩이 끝나면 function{}함수를 실행하세요
  alert($("#unique2").html());	                //id가 unique2인 태그를 검색한 후 html() 메서드를 이용해 태그의 값을 가져온 후, alert시킵니다.
});
</script>
</head>
<body>
  <div class="class1">안녕하세요.</div>
  <div id="unique2">제이쿼리입니다!!</div>
  <div id="unique3">
     <p>제이쿼리는 아주 쉽습니다!!!</p> 
  </div>
</body>
</html>
```

결과
------------

![](/images/Spring_Framework/jQueryResult.jpg)

Ajax란
==============

Ajax란 Asynchronous Javascript(비동기 자바스크립트) + XML의 의미로 자바스크립트를 사용한 비동기 통신, 즉 클라이언트와 서버 간의 XML이나 JSON 데이터를 주고받는 기술

![](/images/Spring_Framework/Ajax.jpg)

제이쿼리 Ajax 사용 형식
---------------------

```html
$.ajax({
    type:"post 또는 get",                      <!--통신 타입을 설정합니다. (post 또는 get 방식으로 선택합니다.)-->
    async:"true 또는 false",                   <!--요청할 url을 설정합니다.-->
    url:"요청할 URL".                          <!--비동기식으로 처리할지의 여부를 설정합니다.(false인 경우 동기식으로 처리합니다.-->
    data:{서버로 전송할 데이터},                <!--서버에 요청할 때 보낼 매개변수를 설정합니다.-->
    dataType:"서버에서 전송받을 데이터 형식",    <!--응답 받을 데이터 타입을 설정합니다.(XML, TEXT, HTML, JSON 등)-->
    success:{                                  <!--요청 및 응답에 성공했을 때 처리 구문을 설정합니다.-->
    //정상 요청, 응답 시 처리
    },
    error:funcion{xhr,status,error){           <!--요청 및 응답에 실패했을 때 처리 구문을 설정합니다.-->
    //오류 발생 시 처리
    }
    complete:function(data,testStatus){        <!--모든 작업을 마친 후 처리 구문을 설정합니다.-->
    //작업 완료 후 처리
    }
});    
```
클라이언트
----------

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>ajax 연습1</title>
  <script  src="http://code.jquery.com/jquery-latest.min.js"></script>
  <script type="text/javascript">
      function fn_process(){
       $.ajax({
         type:"get",
         dataType:"text",
         async:false,  
         url:"http://localhost:8090/pro16/ajaxTest1",
         data: {param:"Hello,jquery"},
         success:function (data,textStatus){
            $('#message').append(data);
         },
         error:function(data,textStatus){
            alert("에러가 발생했습니다.");ㅣ
         },
         complete:function(data,textStatus){
            alert("작업을완료 했습니다");
         }
      });	
   }		
</script>
</head>
<body>
<input type="button" value="전송하기" onClick="fn_process()" /><br><br>
<div id="message"></div>
</body>
</html>
```

서버
------------

```java
@WebServlet("/ajaxTest1")
public class AjaxTest1 extends HttpServlet {
	private static final long serialVersionUID = 1L;

	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		doHandler(request, response);
	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		doHandler(request, response);
	}

	private void doHandler(HttpServletRequest request, HttpServletResponse response)	throws ServletException, IOException {
		request.setCharacterEncoding("utf-8");
		response.setContentType("text/html; charset=utf-8");
		String param = (String) request.getParameter("param");
		System.out.println("param = " + param);
		PrintWriter writer = response.getWriter();
		writer.print("안녕하세요. 서버입니다.");
	}
}
```
Ajax 이용해 서버와 JSON 데이터 주고받기
==============================

### 1. 웹 브라우저에서 서버로 JSON 형식의 정보 전달하기

```java
private void doHandle(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
	request.setCharacterEncoding("utf-8");
	response.setContentType("text/html; charset=utf-8");
	String jsonInfo = request.getParameter("jsonInfo");						//문자열로 전송된 JSON 데이터를 getParameter()를 이용해 가져옵니다.
	try {
		JSONParser jsonParser = new JSONParser();							//JSON 데이터를 처리하기 위해 JSONParser 객체를 생성합니다.
		JSONObject jsonObject = (JSONObject) jsonParser.parse(jsonInfo);	//전송된 JSON 데이터를 파싱합니다.
		System.out.println("* 회원 정보 *");
		System.out.println(jsonObject.get("name"));							//JSON데이터의 name 속성들을 get()에 전달하여 value를 출력합니다.
		System.out.println(jsonObject.get("age"));
		System.out.println(jsonObject.get("gender"));
		System.out.println(jsonObject.get("nickname"));
	} catch (Exception e) {
		e.printStackTrace();
	}
}
```

```javascript
 <script  src="http://code.jquery.com/jquery-latest.min.js"></script> 
 <script>
    $(function() {
        $("#checkJson").click(function() {
    	   var _jsonInfo ='{"name":"박지성","age":"25","gender":"남자","nickname":"날센돌이"}';
    	   $.ajax({
             type:"post",
             async:false, 
             url:"${contextPath}/json",
             data : {jsonInfo: _jsonInfo},			<!--메게변수 이름 jsoninfo로 JSON 데이터를 ajax로 전송합니다.-->
             success:function (data,textStatus){
	     },
	     error:function(data,textStatus){
	        alert("에러가 발생했습니다.");ㅣ
	     },
	     complete:function(data,textStatus){
	     }
	   });  //end ajax	

       });
    });
 </script>
 ```
 
### 2. 서버에서 웹 브라우저로 JSON 형식의 정보 전달하기

* JSON 배열에 정보를 저장하는 과정
	1. memberInfo로 JSONObject 객체를 생성한 후 회원 정보를 name/value쌍으로 저장
	2. membersArray의 JSONArray 객체를 생성한 후 회원 정보를 저장한 JSON 객체를 차례대로 저장
	3. membersArray배열에 회원 정보를 저장한 후 totalObject로 JSONObject 객체를 생성하여 name에는 자바스크립트에서 접근할 때 사용하는 이름인 members를, value에는 membersArray를 최종적으로 저장

```java
private void doHandle(HttpServletRequest request, HttpServletResponse response)
		throws ServletException, IOException {
	request.setCharacterEncoding("utf-8");
	response.setContentType("text/html; charset=utf-8");
	PrintWriter writer = response.getWriter();

	JSONObject totalObject = new JSONObject();
	JSONArray membersArray = new JSONArray();
	JSONObject memberInfo = new JSONObject();

	memberInfo.put("name", "박지성");
	memberInfo.put("age", "25");
	memberInfo.put("gender", "남자");
	memberInfo.put("nickname", "날쌘돌이");
	membersArray.add(memberInfo);

	memberInfo = new JSONObject();
	memberInfo.put("name", "김연아");
	memberInfo.put("age", "21");
	memberInfo.put("gender", "여자");
	memberInfo.put("nickname", "");
	membersArray.add(memberInfo);

	totalObject.put("members", membersArray);

	String jsonInfo = totalObject.toJSONString();
	System.out.print(jsonInfo);
	writer.print(jsonInfo);
}
```
