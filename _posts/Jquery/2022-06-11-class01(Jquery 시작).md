---
categories: Coding	
tag: Jquery
toc: true
author_profile: false
---



# 2022. 06. 09. 수업내용 정리 #1/2

## jQuery 개요.. 기본..

<br>

* 제이쿼리(jQuery)

  제이쿼리(jQuery)는 오픈 소스 기반의 자바스크립트 라이브러리입니다.<br>

  제이쿼리는 여러분의 웹 사이트에 자바스크립트를 더욱 손쉽게 활용할 수 있게 해줍니다.<br>

  또한, 제이쿼리를 사용하면 짧고 단순한 코드로도 웹 페이지에 다양한 효과나 연출을 적용할 수 있습니다.<br>

  이러한 제이쿼리는 오늘날 가장 인기 있는 자바스크립트 라이브러리 중 하나입니다.

  <br>

  <br>

* 제이쿼리의 역사

  제이쿼리는 2006년 미국의 존 레식(John Resig)이 뉴욕시 바캠프(Barcamp)에서 처음으로 소개하였습니다.<br>

  현재는 jQuery Team이라는 개발자 그룹이 jQuery Foundation을 통해 개발과 유지 보수를 담당하고 있습니다.

  <br><br>

* 제이쿼리의 장점

  현재 많이 사용되고 있는 자바스크립트 라이브러리는 다음과 같습니다.

   <br>

  - 프로토타입(Prototype)

  - 도조(Dojo)

  - GWT(Google Web Toolkit)

  - MochiKit

  <br> 이렇게 수많은 자바스크립트 라이브러리 중에서도 제이쿼리가 특히 많이 사용되는 이유는 다음과 같습니다.

  <br>

  1. 제이쿼리는 주요 웹 브라우저의 구버전을 포함한 대부분의 브라우저에서 지원됩니다.

  2. HTML DOM을 손쉽게 조작할 수 있으며, CSS 스타일도 간단히 적용할 수 있습니다.

  3. 애니메이션 효과나 대화형 처리를 간단하게 적용해 줍니다.

  4. 같은 동작을 하는 프로그램을 더욱 짧은 코드로 구현할 수 있습니다.

  5. 다양한 플러그인과 참고할 수 있는 문서가 많이 존재합니다.

  6. 오픈 라이선스를 적용하여 누구나 자유롭게 사용할 수 있습니다.

  <br><br>

* 제이쿼리 버전

  제이쿼리는 jQuery Foundation을 통해 버전 개발 및 유지 보수가 진행되고 있습니다. <br>

  현재 각 제이쿼리 버전별 최신 버전은 다음과 같습니다.

  <br>

  1. 버전 1 : jQuery 1.12.4

  2. 버전 2 : jQuery 2.2.4

  3. 버전 3 : jQuery 3.2.1

  <br>

  2014년 10월에 배포된 제이쿼리 버전 3은 제이쿼리의 차세대 표준입니다.<br>

  제이쿼리 버전 3은 기존 버전과의 호환성을 유지한 채 더욱 간결하게 작성되고, 더욱 빠르게 동작하도록 변경되었습니다.<br>

  2017년 3월에는 제이쿼리 버전 3의 최신 버전인 3.2.1 버전이 발표되었습니다.

  <br><br>

* 제이쿼리 적용

  제이쿼리는 자바스크립트 라이브러리이므로, 제이쿼리 파일은 자바스크립트 파일(.js 파일) 형태로 존재합니다.<br>

  따라서 웹 페이지에서 제이쿼리를 사용하기 위해서는 제이쿼리 파일을 먼저 웹 페이지에 로드(load)해야 합니다.

   <br>

  웹 페이지에 제이쿼리 파일을 로드하는 방법은 다음과 같습니다.

   <br>

  1. 제이쿼리 파일을 다운받아 로드하는 방법

  2. CDN(Content Delivery Network)을 이용하여 로드하는 방법

​		<br>        <br>

* 제이쿼리 파일을 다운받아 로드하는 방법

  최신 버전의 제이쿼리 파일은 다음 공식 사이트에서 다운받을 수 있습니다.

    <br>

  [jQuery.com : http://jquery.com/download =>](http://jquery.com/download/)

    <br>

  이렇게 다운받은 제이쿼리 파일을 서버에 저장하고, 다음 <script>태그를 웹 페이지의 <head>태그 내에 삽입하면 됩니다.

  ```html
  문법
  
  <head>
      <script src="/파일경로/제이쿼리파일명.js"></script>
  </head>
  ```

  ```html
  예제
  
  <head>
      <script src="/media/jquery-1.12.4.min.js"></script>
  </head>
  ```

    <br>  <br>

* CDN을 이용하여 로드하는 방법

  CDN(Content Delivery Network)이란 웹 사이트의 접속자가 서버에서 콘텐츠를 다운받아야 할 때, 자동으로 가장 가까운 서버에서 다운받도록 하는 기술입니다.  <br>

  CDN site : https://cdnjs.com/libraries/jquery <br>

  이 기술을 이용하면 특정 서버에 트래픽이 집중되지 않고, 콘텐츠 전송 시간이 매우 빨라지는 장점이 있습니다.  <br>

  이러한 CDN을 이용하면 제이쿼리 파일을 서버에 따로 저장하지 않아도 제이쿼리를 사용할 수 있습니다.<br>

  현재 이용할 수 있는 제이쿼리의 CDN은 다음과 같으며, 어떤 CDN을 이용하더라도 같은 동작을 합니다.<br>

  ```html
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.6.0/jquery.min.js" integrity="sha512-894YE6QWD5I59HgZOGReFYm4dnWc1Qt5NtvYSaNcOP+u1T9qYdvdihz0PPSiiqn/+/3e7Jo4EaG7TubfWGUrMQ==" crossorigin="anonymous" referrerpolicy="no-referrer"></script>
  
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.6.0/jquery.js" integrity="sha512-n/4gHW3atM3QqRcbCn6ewmpxcLAHGaDjpEBu4xZd47N0W2oQ+6q7oc3PXstrJYXcbNU1OHdQ1T7pAP+gi5Yu8g==" crossorigin="anonymous" referrerpolicy="no-referrer"></script>
  
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.6.0/jquery.slim.js" integrity="sha512-HNbo1d4BaJjXh+/e6q4enTyezg5wiXvY3p/9Vzb20NIvkJghZxhzaXeffbdJuuZSxFhJP87ORPadwmU9aN3wSA==" crossorigin="anonymous" referrerpolicy="no-referrer"></script>
  
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.6.0/jquery.slim.min.js" integrity="sha512-6ORWJX/LrnSjBzwefdNUyLCMTIsGoNP6NftMy2UAm1JBm6PRZCO1d7OHBStWpVFZLO+RerTvqX/Z9mBFfCJZ4A==" crossorigin="anonymous" referrerpolicy="no-referrer"></script>
  
  https://cdnjs.cloudflare.com/ajax/libs/jquery/3.6.0/jquery.min.map
  
  https://cdnjs.cloudflare.com/ajax/libs/jquery/3.6.0/jquery.slim.min.map
  ```

  ````html
  <!DOCTYPE html>
  <html lang="ko">
  
  <head>
  	<meta charset="UTF-8">
  	<title>jQuery Intro</title>
  	<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.12.4/jquery.min.js"></script>
  	<script>
  		$(function() {
  			$("p").on("click", function() {
  				$("p").css("color", "red");
  			});
  		});
  	</script>
  </head>
  
  <body>
  
  	<p>이제부터 제이쿼리를 다 같이 공부해보죠!!<br>
  	마우스로 글씨를 클릭해보세요!!</p>
  	
  </body>
  
  </html>
  ````

  웹페이지 화면 ▼

  ![image-20220611170137917](../../images/2022-06-11-class1(Jquery 시작)/image-20220611170137917.png)

  <br><br>

* 제이쿼리 문법

  제이쿼리를 사용하면 아주 간편하게 HTML 요소를 선택하고, 그렇게 선택된 요소에 손쉽게 특정 동작을 설정할 수 있습니다.<br>

  제이쿼리의 기본 문법은 다음과 같습니다.<br>

  ```html
  문법
  
  $(선택자).동작함수();
  ```

  달러($) 기호는 제이쿼리를 의미하고, 제이쿼리에 접근할 수 있게 해주는 식별자입니다.<br>

  선택자를 이용하여 원하는 HTML 요소를 선택하고, 동작 함수를 정의하여 선택된 요소에 원하는 동작을 설정합니다.

  <br>

  <br>

* $() 함수

  $() 함수는 선택된 HTML 요소를 제이쿼리에서 이용할 수 있는 형태로 생성해 주는 역할을 합니다.<br>

  $() 함수의 인수로는 HTML 태그 이름뿐만 아니라, CSS 선택자를 전달하여 특정 HTML 요소를 선택할 수 있습니다.<br>

  이러한 $() 함수를 통해 생성된 요소를 제이쿼리 객체(jQuery object)라고 합니다.<br>

  제이쿼리는 이렇게 생성된 제이쿼리 객체의 메소드를 사용하여 여러 동작을 설정할 수 있습니다.

  <br><br>

* Document 객체의 reday() 메소드

  자바스크립트 코드는 웹 브라우저가 문서의 모든 요소를 로드한 뒤에 실행되어야 합니다.<br>

  보통은 별다른 문제가 발생하지 않지만, 다음과 같은 경우에는 오류가 발생합니다.

  <br>

  - 아직 생성되지 않은 HTML 요소에 속성을 추가하려고 할 경우

  - 아직 로드되지 않은 이미지의 크기를 얻으려고 할 경우

  <br>

  다음 예제는 아직 생성되지 않은 HTML 요소에 속성을 추가하는 예제입니다.<br>

  ```html
  <!DOCTYPE html>
  <html lang="ko">
  
  <head>
  	<meta charset="UTF-8">
  	<title>jQuery Syntax</title>
  	<script src="https://code.jquery.com/jquery-1.12.4.min.js"></script>
  	<script>
  		function func() {
  			addAttribute();		// 아이디가 "para"인 HTML 요소에 속성을 추가함.
  			createElement();		// 아이디가 "para"인 HTML 요소를 생성함.
  		}
  		function createElement() {
  			var criteriaNode = document.getElementById("text");
  			var newNode = document.createElement("p")
  			newNode.innerHTML = "새로운 단락입니다.";
  			newNode.setAttribute("id", "para");
  			document.body.insertBefore(newNode, criteriaNode);
  		}
  		function addAttribute() {
  			document.getElementById("para").setAttribute("style", "color: red");
  		}
  	</script>
  </head>
  
  <body>
  
  	<h1>아직 생성되지 않은 HTML 요소에 속성 추가</h1>
  
  	<button onclick="func()">속성 추가!</button>
  	<p id="text"></p>
  	
  </body>
  
  </html>
  ```

  웹페이지 화면 ▼

  ![image-20220611170629250](../../images/2022-06-11-class1(Jquery 시작)/image-20220611170629250.png)

  위의 예제에서 addAttribute() 함수는 아이디가 "para"인 HTML 요소에 새로운 속성을 추가하는 함수입니다.

  또한, createElement() 함수는 아이디가 "para"인 HTML 요소를 생성하여 추가해 주는 함수입니다.

  위의 예제에서는 아이디가 "para"인 HTML 요소가 생성되기 전에 해당 요소에 속성을 추가해 주는 addAttribute() 함수가 호출되므로, Uncaught TypeError가 발생하여 실행중이던 스크립트는 중지될 것입니다.

  만약 먼저 호출되는 addAttribute() 함수를 createElement() 함수 뒤에 호출하면, 정상적으로 동작할 것입니다.

  

