---
categories: Coding	
tag: Javascript
toc: true
---



# 2022. 06. 02. 수업내용 정리 

## String 객체.. 메소드..

<br>

* 자바스크립트에서의 문자열 표현

  자바스크립트에서 문자열 리터럴은 큰따옴표("")나 작은따옴표('')를 사용하여 손쉽게 만들 수 있습니다.<br>

  ```javascript
  예제
  var firstStr = "이것도 문자열입니다.";      // 큰따옴표를 사용한 문자열
  
  var secondStr = '이것도 문자열입니다.';     // 작은따옴표를 사용한 문자열
  
  var thirdStr = "나의 이름은 '홍길동'이야."  // 작은따옴표는 큰따옴표로 둘러싸인 문자열에만 포함될 수 있음.
  
  var fourthStr = '나의 이름은 "홍길동"이야.' // 큰따옴표는 작은따옴표로 둘러싸인 문자열에만 포함될 수 있음.
  ```

  <br><br>

* 문자열의 길이

  자바스크립트에서 문자열의 길이는 length 프로퍼티에 저장됩니다.<br>

  ```html
  <!DOCTYPE html>
  <html lang="ko">
  
  <head>
  	<meta charset="UTF-8">
  	<title>JavaScript String Object</title>
  </head>
  
  <body>
  
  	<h1>문자열의 길이</h1>
  
  	<script>
  		var strKor = "한글";
  		var strEng = "abcABC";
  		document.write(strKor.length + "<br>");	// 2
  		document.write(strEng.length);			// 6
  	</script>
  	
  </body>
  
  </html>
  ```

  웹페이지 화면 ▼

  ![image-20220608220145082](../../images/2022-06-08-class27(String 객체)/image-20220608220145082.png)

  오랫동안 사용되어 온 아스키(ASCII) 인코딩 환경에서 영문자는 한 글자당 1바이트, 한글은 한 글자당 2바이트로 표현됩니다.<br>

  하지만 UTF-8 인코딩 환경에서는 영문자는 한 글자당 1바이트, 한글은 한 문자당 3바이트로 표현됩니다.

  <br>

  자바스크립트의 length 프로퍼티는 해당 문자열의 총 바이트 수를 저장하는 것이 아닌 글자의 개수만을 저장합니다.

  <br><br>

* 이스케이프 시퀀스(escape sequence)

  자바스크립트는 더욱 다양한 문자 표현을 위해 여러 가지 이스케이프 시퀀스(escape sequence) 방식을 제공합니다.<br>

  자바스크립트에서 제공하는 이스케이프 시퀀스 방식은 다음과 같습니다.<br>

  <br>

  1. 16진수 이스케이프 시퀀스(hexadecimal escape sequence)
  2. 유니코드 이스케이프 시퀀스(unicode escape sequence)
  3. 유니코드 코드 포인트 이스케이프(unicode code point escape)

  <br>

  ```html
  <!DOCTYPE html>
  <html lang="ko">
  
  <head>
  	<meta charset="UTF-8">
  	<title>JavaScript String Object</title>
  </head>
  
  <body>
  
  	<h1>이스케이프 시퀀스</h1>
  
  	<script>
  		// 16진수 이스케이프 시퀀스로 \x 다음은 16진수 수로 인식됨.
  		document.write('\xA2' + "<br>");
  		// 유니코드 이스케이프 시퀀스로 \u 다음은 유니코드로 인식됨.
  		document.write('\u00A2' + "<br>");
  		// ECMAScript 6부터 새롭게 추가된 유니코드 코드 포인트 이스케이프 방식임.
  		document.write(String.fromCodePoint(0x00A2) + "<br>");
  	</script>
  	
  </body>
  
  </html>
  ```

  웹페이지 화면 ▼

  ![image-20220608220536043](../../images/2022-06-08-class27(String 객체)/image-20220608220536043.png)

  ★ String.fromCodePoint() 메소드는 사파리, 익스플로러에서 지원하지 않습니다.

  <br><br>

* 긴 문자열 리터럴을 나누어 표현하기

  자바스크립트에서는 길이가 긴 문자열 리터럴을 보기 좋게 표현하기 위해서 역 슬래시(\)나 결합(+) 연산자를 사용할 수 있습니다.

  ```html
  <!DOCTYPE html>
  <html lang="ko">
  
  <head>
  	<meta charset="UTF-8">
  	<title>JavaScript String Object</title>
  </head>
  
  <body>
  
  	<h1>긴 문자열 리터럴 나누어 표현하기</h1>
  
  	<p>이렇게 줄이 나뉜 문자열은 코드 내에서만 표현되며, 웹 페이지에서는 기존과 같이 하나의 문자열로 표현됩니다.</p>
  	<script>
  		document.write("이 문자열은 아주 긴 문자열입니다. \
  			따라서 몇 번에 걸친 줄 나누기가 필요합니다. \
  			자바스크립트에서는 역슬래시와 문자 결합 연산자를 이용하여 줄을 나눌 수 있습니다.<br>");
  		document.write("이 문자열은 아주 긴 문자열입니다." + 
  			" 따라서 몇 번에 걸친 줄 나누기가 필요합니다." + 
  			" 자바스크립트에서는 역슬래시와 문자 결합 연산자를 이용하여 줄을 나눌 수 있습니다.");
  	</script>
  	
  </body>
  
  </html>
  ```

  웹페이지 화면 ▼

  ![image-20220608220711003](../../images/2022-06-08-class27(String 객체)/image-20220608220711003.png)

  ★ 역 슬래시(\)를 사용한 방식은 ECMAScript의 표준 방식이 아닙니다.<br>
  따라서 특정 웹 브라우저에서는 정상적으로 표현되지 않을 수도 있습니다.

  <br><br>

* String 객체

  자바스크립트에서 문자열은 보통 문자열 리터럴을 사용하여 표현합니다.<br>

  하지만 문자열을 나타낼 때 new 연산자를 사용하여 명시적으로 String 객체를 생성할 수도 있습니다.<br>

  이러한 String 객체는 문자열 값을 감싸고 있는 래퍼(wrapper) 객체입니다.<br>

  ```html
  <!DOCTYPE html>
  <html lang="ko">
  
  <head>
  	<meta charset="UTF-8">
  	<title>JavaScript String Object</title>
  </head>
  
  <body>
  
  	<h1>String 객체</h1>
  
  	<script>
  		var str = "JavaScript";
  		var strObj = new String("JavaScript");
  
  		document.write(str + "<br>");				// "JavaScript"
  		document.write(strObj + "<br>");			// "JavaScript"
  		document.write(typeof str + "<br>");		// string
  		document.write(typeof strObj + "<br>");		// object
  		document.write((str == strObj) + "<br>");	// 문자열 값이 같으므로, true를 반환함.
  		document.write((str === strObj));			// 문자열 값은 같지만 타입이 다르므로, false를 반환함.
  	</script>
  	
  </body>
  
  </html>
  ```

  웹페이지 화면 ▼

  ![image-20220608220843827](../../images/2022-06-08-class27(String 객체)/image-20220608220843827.png)

* String 메소드

  String 메소드는 String 객체에 정의된 문자열과 관련된 작업을 할 때 사용하는 메소드입니다.

  <br>

  1. String.fromCharCode()

  2. String.fromCodePoint()

  <br><br>

* String.fromCharCode() 메소드

  이 메소드는 쉼표로 구분되는 일련의 유니코드에 해당하는 문자들로 구성된 문자열을 반환합니다.<br>

  ```javascript
  예제
  
  String.fromCharCode(65, 66, 67); // "ABC"
  ```

  <br><br>

* String.fromCodePoint() 메소드

  이 메소드는 쉼표로 구분되는 일련의 코드 포인트(code point)에 해당하는 문자들로 구성된 문자열을 반환합니다.

  ```javascript
  예제
  
  String.fromCodePoint(65, 66, 67); // "ABC"
  String.fromCodePoint(0x2F804);    // "\uD87E\uDC04"
  String.fromCodePoint(194564);     // "\uD87E\uDC04"
  ```

  ★ String.fromCodePoint() 메소드는 사파리, 익스플로러에서 지원하지 않습니다.

  <br><br>

* String.prototype 메소드

  모든 String 인스턴스는 String.prototype으로부터 메소드와 프로퍼티를 상속받습니다.<br>

  이렇게 상속받은 String.prototype 메소드를 이용하면, 다음과 같은 문자열 작업을 할 수 있습니다.<br>

   <br>

  1. 문자열에서의 위치 반환

  2. 문자열에서 지정된 위치에 있는 문자 반환

  3. 문자열 추출

  4. 문자열 분리

  5. 문자열 결합

  6. 문자열의 대소문자 변환

  7. 문자열 주위의 공백 제거

  8. 정규 표현식을 이용한 문자열 조작

  <br>

  ★ String 인스턴스의 값은 변경될 수(immutable) 없으므로, 모든 String 메소드는 결괏값으로 새로운 문자열을 생성하여 반환합니다.

  <br><br>

* 문자열에서의 위치 찾기

  다음 메소드는 String 인스턴스에서 특정 문자나 문자열이 처음으로 등장하는 위치나 마지막으로 등장하는 위치를 반환합니다.<br><br>

  \- indexOf()

  \- lastIndexOf()

   <br>

  이 메소드들은 문자열을 찾기 시작할 String 인스턴스의 위치를 두 번째 인수로 전달할 수 있습니다.<br>

  만약 전달받은 특정 문자나 문자열을 찾을 수 없을 때는 -1을 반환합니다.<br>

  ```html
  <!DOCTYPE html>
  <html lang="ko">
  
  <head>
  	<meta charset="UTF-8">
  	<title>JavaScript String Method</title>
  </head>
  
  <body>
  
  	<h1>문자열에서의 위치 찾기</h1>
  
  	<script>
  		var str = "abcDEFabc";
  
  		document.write(str.indexOf('abc') + "<br>");		// 0
  		document.write(str.indexOf('abcd') + "<br>");		// -1
  		document.write(str.indexOf('abc', 3) + "<br><br>");	// 6
  
  		document.write(str.lastIndexOf('abc') + "<br>");	// 6
  		document.write(str.lastIndexOf('d') + "<br>");		// -1
  		document.write(str.lastIndexOf('c'));				// 8
  	</script>
  	
  </body>
  
  </html>
  ```

  웹페이지 화면 ▼

  ![image-20220608221539948](../../images/2022-06-08-class27(String 객체)/image-20220608221539948.png)

  <br><br>

* 문자열에서 지정된 위치에 있는 문자 반환

  다음 메소드는 String 인스턴스에서 전달받은 인덱스에 위치한 문자나 문자 코드를 반환합니다.<br><br>

  \- charAt()

  \- charCodeAt()

  \- charPointAt()

  <br>

  ```html
  <!DOCTYPE html>
  <html lang="ko">
  
  <head>
  	<meta charset="UTF-8">
  	<title>JavaScript String Method</title>
  </head>
  
  <body>
  
  	<h1>문자열에서 지정된 위치에 있는 문자 반환</h1>
  
  	<script>
  		var str = "abcDEFabc";
  
  		document.write(str.charAt(0) + "<br>");			// a
  		document.write(str.charAt(10) + "<br>");		// 빈 문자열
  		document.write(str.charCodeAt(0) + "<br>");		// 97
  		document.write(str.codePointAt(0));				// 97
  	</script>
  	
  </body>
  
  </html>
  ```

  웹페이지 화면 ▼

  ![image-20220608221716965](../../images/2022-06-08-class27(String 객체)/image-20220608221716965.png)

  ★ codePointAt() 메소드는 사파리, 익스플로러에서 지원하지 않습니다.

  <br><br>

* 문자열 추출 

  다음 메소드는 String 인스턴스에서 전달받은 시작 인덱스부터 종료 인덱스 바로 앞까지의 문자열만을 추출하여 만든 새로운 문자열을 반환합니다.

  <br>

  \- slice()

  \- substring()

  \- substr()

  <br>

  ```html
  <!DOCTYPE html>
  <html lang="ko">
  
  <head>
  	<meta charset="UTF-8">
  	<title>JavaScript String Method</title>
  </head>
  
  <body>
  
  	<h1>문자열 추출</h1>
  
  	<script>
  		var str = "abcDEFabc";
  
  		document.write(str.slice(2, 6) + "<br>");		// cDEF
  		document.write(str.slice(-4, -2) + "<br>");		// Fa
  		document.write(str.slice(2) + "<br>");			// cDEFabc
  
  		document.write(str.substring(2, 6) + "<br>");	// cDEF
  		document.write(str.substr(2, 4));				// cDEF
  	</script>
  	
  </body>
  
  </html>
  ```

  웹페이지 화면 ▼

  ![image-20220608221909130](../../images/2022-06-08-class27(String 객체)/image-20220608221909130.png)

  <br><br>

* 문자열 분리

  #### 문자열 분리

  다음 메소드는 String 인스턴스를 구분자(separator)를 기준으로 나눈 후, 나뉜 문자열을 하나의 배열로 반환합니다.<br>

  \- split()

   <br>

  split() 메소드는 인수로 구분자를 전달하지 않으면, 전체 문자열을 하나의 배열 요소로 가지는 길이가 1인 배열을 반환합니다.<br>

  ```html
  <!DOCTYPE html>
  <html lang="ko">
  
  <head>
  	<meta charset="UTF-8">
  	<title>JavaScript String Method</title>
  </head>
  
  <body>
  
  	<h1>문자열 추출</h1>
  
  	<script>
  		var str = "자바스크립트는 너무 멋져요! 그리고 유용해요.";
  
  		document.write(str.split() + "<br>");		// 구분자를 명시하지 않으면 아무런 동작도 하지 않음.
  		document.write(str.split("") + "<br>");		// 한 문자("")씩 나눔.
  		document.write(str.split(" ") + "<br>");	// 띄어쓰기(" ")를 기준으로 나눔.
  		document.write(str.split("!"));				// 느낌표("!"")를 기준으로 나눔.
  	</script>
  	
  </body>
  
  </html>
  ```

  웹페이지 화면 ▼

  ![image-20220608222049981](../../images/2022-06-08-class27(String 객체)/image-20220608222049981.png)

  <br><br>

* 문자열 결합

  다음 메소드는 String 인스턴스에 전달받은 문자열을 결합한 새로운 문자열을 반환합니다.

   <br>

  \- concat()

   <br>

  ```html
  <!DOCTYPE html>
  <html lang="ko">
  
  <head>
  	<meta charset="UTF-8">
  	<title>JavaScript String Method</title>
  </head>
  
  <body>
  
  	<h1>문자열 결합</h1>
  
  	<script>
  		var str = "자바스크립트";
  
  		document.write(str + "<br>");
  		document.write(str.concat("는 너무 멋져요!") + "<br>");
  		document.write(str.concat("는 너무 멋져요!", " 그리고 유용해요!" + "<br>"));
  		document.write(str);
  	</script>
  	
  </body>
  
  </html>
  ```

  웹페이지 화면 ▼

  ![image-20220608222155702](../../images/2022-06-08-class27(String 객체)/image-20220608222155702.png)

  위의 예제에서 여러 번 concat() 메소드를 실행한 후의 변수 str의 문자열은 여전히 처음과 같습니다.<br>

  이처럼 자바스크립트에서 String 인스턴스의 값은 변경될 수(immutable) 없습니다.<br>

  따라서 모든 String 메소드는 결괏값으로 새로운 문자열을 생성하여 반환합니다.

  <br><br>

* 문자열의 대소문자 변환

  다음 메소드는 String 인스턴스의 모든 문자를 대문자나 소문자로 변환한 새로운 문자열을 반환합니다.

   <br>

  \- toUpperCase()

  \- toLowerCase()

   <br>

  ```html
  <!DOCTYPE html>
  <html lang="ko">
  
  <head>
  	<meta charset="UTF-8">
  	<title>JavaScript String Method</title>
  </head>
  
  <body>
  
  	<h1>문자열의 대소문자 변환</h1>
  
  	<script>
  		var str = "JavaScript";
  
  		document.write(str.toUpperCase() + "<br>"); // JAVASCRIPT
  		document.write(str.toLowerCase()); 			// javacript
  	</script>
  	
  </body>
  
  </html>
  ```

  웹페이지 화면 ▼

  ![image-20220608222348753](../../images/2022-06-08-class27(String 객체)/image-20220608222348753.png)

  <br><br>

* 문자열 주위의 공백 제거

  다음 메소드는 String 인스턴스의 양 끝에 존재하는 모든 공백과 줄 바꿈 문자(LF, CR 등)를 제거한 새로운 문자열을 반환합니다.

   <br>

  \- trim()

   <br>

  trim() 메소드는 String 인스턴스의 문자열 값 그 자체에는 영향을 주지 않습니다.

  <br>

  ```html
  <!DOCTYPE html>
  <html lang="ko">
  
  <head>
  	<meta charset="UTF-8">
  	<title>JavaScript String Method</title>
  </head>
  
  <body>
  
  	<h1>문자열 주위의 공백 제거</h1>
  
  	<script>
  		var str = "      JavaScript	";
  
  		document.write(str.trim());
  	</script>
  	
  </body>
  
  </html>
  ```

  웹페이지 화면 ▼

  ![image-20220608222523430](../../images/2022-06-08-class27(String 객체)/image-20220608222523430.png)

  <br><br>

  아래는 위에서 설명한 메소드를 포함한 모든 prototype 메소드를 표로 정리한 것입니다.<br>

  #### 자바스크립트 String.prototype 메소드

  |       메소드        |                             설명                             |
  | :-----------------: | :----------------------------------------------------------: |
  |      indexOf()      | String 인스턴스에서 특정 문자나 문자열이 처음으로 등장하는 위치의 인덱스를 반환함. |
  |    lastIndexOf()    | String 인스턴스에서 특정 문자나 문자열이 마지막으로 등장하는 위치의 인덱스를 반환함. |
  |      charAt()       | String 인스턴스에서 전달받은 인덱스에 위치한 문자를 반환함.  |
  |    charCodeAt()     | String 인스턴스에서 전달받은 인덱스에 위치한 문자의 UTF-16 코드를 반환함. (0 ~ 65535) |
  |    charPointAt()    | String 인스턴스에서 전달받은 인덱스에 위치한 문자의 유니코드 코드 포인트(unicode code point)를 반환함. |
  |       slice()       | String 인스턴스에서 전달받은 시작 인덱스부터 종료 인덱스 바로 앞까지의 문자열을 추출한 새 문자열을 반환함. |
  |     substring()     | String 인스턴스에서 전달받은 시작 인덱스부터 종료 인덱스 바로 앞까지의 문자열을 추출한 새 문자열을 반환함. |
  |      substr()       | String 인스턴스에서 전달받은 시작 인덱스부터 길이만큼의 문자열을 추출한 새로운 문자열을 반환함. |
  |       split()       | String 인스턴스에서 구분자(separator)를 기준으로 나눈 후, 나뉜 문자열을 하나의 배열로 반환함. |
  |      concat()       | String 인스턴스에 전달받은 문자열을 결합한 새로운 문자열을 반환함. |
  |    toUpperCase()    | String 인스턴스의 모든 문자를 대문자로 변환한 새로운 문자열을 반환함. |
  |    toLowerCase()    | String 인스턴스의 모든 문자를 소문자로 변환한 새로운 문자열을 반환함. |
  |       trim()        | String 인스턴스의 양 끝에 존재하는 공백과 모든 줄 바꿈 문자(LF, CR 등)를 제거한 새로운 문자열을 반환함. |
  |      search()       | 인수로 전달받은 정규 표현식에 맞는 문자나 문자열이 처음으로 등장하는 위치의 인덱스를 반환함. |
  |      replace()      | 인수로 전달받은 패턴에 맞는 문자열을 대체 문자열로 변환한 새 문자열을 반환함. |
  |       match()       | 인수로 전달받은 정규 표현식에 맞는 문자열을 찾아서 하나의 배열로 반환함. |
  |     includes()      | 인수로 전달받은 문자나 문자열이 포함되어 있는지를 검사한 후 그 결과를 불리언 값으로 반환함. |
  |    startsWith()     | 인수로 전달받은 문자나 문자열로 시작되는지를 검사한 후 그 결과를 불리언 값으로 반환함. |
  |     endsWith()      | 인수로 전달받은 문자나 문자열로 끝나는지를 검사한 후 그 결과를 불리언 값으로 반환함. |
  | toLocaleUpperCase() | 영문자뿐만 아니라 모든 언어의 문자를 대문자로 변환한 새로운 문자열을 반환함. |
  | toLocaleLowerCase() | 영문자뿐만 아니라 모든 언어의 문자를 소문자로 변환한 새로운 문자열을 반환함. |
  |   localeCompare()   | 인수로 전달받은 문자열과 정렬 순서로 비교하여 그 결과를 정수 값으로 반환함. |
  |     normalize()     | 해당 문자열의 유니코드 표준화 양식(Unicode Normalization Form)을 반환함. |
  |      repeat()       | 해당 문자열을 인수로 전달받은 횟수만큼 반복하여 결합한 새로운 문자열을 반환함. |
  |     toString()      |           String 인스턴스의 값을 문자열로 반환함.            |
  |      valueOf()      |           String 인스턴스의 값을 문자열로 반환함.            |

   

  

   

  

 

