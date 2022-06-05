---
categories: Coding	
tag: Javascript
---



# 2022. 06. 02. 수업내용 정리 

## Number 객체, 메소드

<br>

* 자바스크립트에서의 수 표현

  정수와 실수를 따로 구분하지 않고, 모든 수를 실수 하나로만 표현합니다.<br>

  자바스크립트에서 모든 숫자는 IEEE 754 국제 표준에서 정의한 64비트 부동 소수점 수로 저장됩니다.<br>

  <br>

  64비트 부동 소수점 수(double precision floating point number)는 메모리에 다음과 같은 형태로 저장됩니다.<br>

  |      0 ~ 51 비트      |     52 ~ 62 비트      |       63 비트        |
  | :-------------------: | :-------------------: | :------------------: |
  | 총 52비트의 가수 부분 | 총 11비트의 지수 부분 | 총 1비트의 부호 부분 |

  이러한 64비트 부동 소수점 수의 정밀도는 정수부는 15자리까지, 소수부는 17자리까지만 유효합니다.<br><br>

  ```html
  <!--예제_64비트 부동 소수점 수의 정밀도-->
  <!DOCTYPE html> 
  <html lang="ko"> 
  
  <head>
  	<meta charset="UTF-8">
  	<title>JavaScript Number Object</title>
  </head>
  
  <body>
  
  	<h1>64비트 부동 소수점 수의 정밀도</h1>
  
  	<script>
  		var x = 999999999999999;	// 15자리의 정수부
  		var y = 9999999999999999;	// 16자리의 정수부
  		var z = 0.1 + 0.2
  
  		document.write(x + "<br>");		// 999999999999999
  		document.write(y + "<br>");		// 10000000000000000
  		document.write(z);				// 0.30000000000000004
  	</script>
  	
  </body>
  
  </html>
  ```

  웹페이지 화면 ▼

  ![객체예시24](../../images/2022-06-05-class24(Number객체)/객체예시24.png)

위의 예제에서 변수 z의 값을 살펴봅면 오차가 발생했음을 알 수 있습니다.<br>

이렇게 부동 소수점 수를 가지고 수행하는 산술 연산의 결과값은 언제나 오차가 발생할 가능성을 가지고 있습니다.<br>

이것은 자바스크립트만이 문제가 아닌 부동 소수점 수를 가지고 실수를 표현하는 모든 프로그래밍 언어에서의 문제점입니다.<br>

자바스크립트에서는 이러한 오차를 없애기 위해 정수의 형태로 먼저 변환하여 계산을 수행하고, 다시 실수의 형태로 재변환하는 방법을 사용할 수도 있습니다.<br>

```javascript
var z = (0.2 * 10 + 0.1 * 10) / 10; // 0.3
```

<br><br>

* 진법 표현

  자바스크립트에서는 기본적으로 **10진법**을 사용하여 수를 표현합니다.<br>

   하지만 0x 접두사를 사용하여 16진법으로 수를 표현할 수도 있습니다.<br>

  ```html
  <!DOCTYPE html>
  <html lang="ko">
  
  <head>
  	<meta charset="UTF-8">
  	<title>JavaScript Number Object</title>
  </head>
  
  <body>
  
  	<h1>16진법으로 수 표현</h1>
  
  	<script>
  		var x = 0xAB;			// 16진법으로 표현된 10진수 171
  		var y = 29;				// 10진법으로 표현된 10진수 29
  
  		document.write(x + y);	// 두 수 모두 10진법으로 자동으로 변환되어 계산됨. -> 200
  	</script>
  	
  </body>
  
  </html>
  ```

  웹페이지 화면 ▼

  ![객체예시25](../../images/2022-06-05-class24(Number객체)/객체예시25.png)

  <br>

  위의 예제처럼 자바스크립트에서는 산술 연산 시 모든 수가 10진수로 자동 변환되어 계산됩니다.<br>

  또한, 숫자에  toString() 메소드를 사용하여 해당 숫자를 여러 진법의 형태로 변환할 수 있습니다.<br>

  ```html
  <!DOCTYPE html>
  <html lang="ko">
  
  <head>
  	<meta charset="UTF-8">
  	<title>JavaScript Number Object</title>
  </head>
  
  <body>
  
  	<h1>여러 진법의 형태로 변환</h1>
  
  	<script>
  		var num = 256;
  
  		document.write(num.toString(2) + "<br>");	//  2진법으로 변환 : 100000000
  		document.write(num.toString(8) + "<br>");	//  8진법으로 변환 : 400
  		document.write(num.toString(10) + "<br>");	// 10진법으로 변환 : 256
  		document.write(num.toString(16) + "<br>");	// 16진법으로 변환 : 100
  
  		// 2진수로 변환한 결괏값을 문자열로 반환함.
  		document.write(num.toString(2) + "<br>");	// 100000000
  		// 문자열을 숫자로 나눴기 때문에 자동으로 10진수로 변환되어 산술 연산된 결괏값
  		document.write(num.toString(2) / 2);		// 50000000
  	</script>
  	
  </body>
  
  </html>
  ```

  웹페이지 화면 ▼

  ![객체예시26](../../images/2022-06-05-class24(Number객체)/객체예시26.png)

  toString() 메소드는 해당 숫자의 진법을 실제로 바꿔주는 것이 아닌, 전달된 진법으로 변환된 형태의 문자열을 반환해 주는 것입니다.

  <br>

  <br>

* Infinity

  자바스크립트에서는 양의 무한대를 의미하는 Infinity 값과 음의 무한대를 의미하는 -Infinity 값을 사용할 수 있습니다.<br>

  Infinity 값은 사용자가 임의로 수정할 수 없는 읽기 전용 값이며, 자바스크립트의 어떤 수보다도 큰 수로 취급됩니다.<br>

  ```html
  <!DOCTYPE html>
  <html lang="ko">
  
  <head>
  	<meta charset="UTF-8">
  	<title>JavaScript Number Object</title>
  </head>
  
  <body>
  
  	<h1>Infinity</h1>
  
  	<script>
  		var x = 10 / 0;				// 숫자를 0으로 나누면 Infinity를 반환함.
  		var y = Infinity * 1000		// Infinity에 어떠한 수를 산술 연산해도 Infinity를 반환함.
  		var z = 1 / Infinity		// Infinity의 역수는 0을 반환함.
  
  		document.write(x + "<br>");	// Infinity
  		document.write(y + "<br>");	// Infinity
  		document.write(z);			// 0
  	</script>
  	
  </body>
  
  </html>
  ```

  웹페이지 화면 ▼

  ![객체예시27](../../images/2022-06-05-class24(Number객체)/객체예시27.png)

  <br><br>

* NaN

  **NaN(Not A Number)**는 숫자가 아니라는 의미로, 정의되지 않은 값이나 표현할 수 없는 값을 가리킵니다.<br>

  0을 0으로 나누거나, 숫자로 변환할 수 없는 피연산자는 산술 연산을 시도하는 경우에 반환되는 읽기 전용 값입니다.<br>

  ```html
  <!DOCTYPE html>
  <html lang="ko">
  
  <head>
  	<meta charset="UTF-8">
  	<title>JavaScript Number Object</title>
  </head>
  
  <body>
  
  	<h1>NaN(Not A Number)</h1>
  
  	<script>
  		var x = 100 - "10";			// "10"은 자동으로 숫자로 변환되어 계산됨.
  		var y = 100 - "문자열";		// "문자열"은 숫자로 변환할 수 없기 때문에 NaN을 반환함.
  		var z = 0 / 0;				// 0을 0으로 나눌 수 없기 때문에 NaN을 반환함.
  
  		document.write(x + "<br>");	// 90
  		document.write(y + "<br>");	// NaN
  		document.write(z);			// NaN
  	</script>
  	
  </body>
  
  </html>
  ```

  웹페이지 화면 ▼

  ![객체예시28](../../images/2022-06-05-class24(Number객체)/객체예시28.png)

  자바스크립트의 전역 함수 중 하나인 **isNaN() 함수**를 사용하면, 전달받은 값이 숫자인지 아닌지를 판단해 줍니다.<br>

  ```html
  <!DOCTYPE html>
  <html lang="ko">
  
  <head>
  	<meta charset="UTF-8">
  	<title>JavaScript Number Object</title>
  </head>
  
  <body>
  
  	<h1>isNaN() 함수</h1>
  
  	<script>
  		var x = 100 * "문자열";
  
  		if(isNaN(x)) { // 전달된 값이 숫자인지 아닌지를 검사함.
  			document.write("변수 x의 값은 숫자가 아닙니다.");
  		} else {
  			document.write("변수 x의 값은 숫자입니다.");
  		}
  	</script>
  	
  </body>
  
  </html>
  ```

  웹페이지 화면 ▼

  ![객체예시29](../../images/2022-06-05-class24(Number객체)/객체예시29.png)

  <br><br>

* null, undefined, NaN, Infinity에 대한 비교

  자바스크립트에서는 약간은 비슷한 것 같으면서도 전혀 다른 4가지 값을 제공하고 있습니다.<br>

  <br>

  * null은 object 타입이며, 아직 **'값'**이 정해지지 않은 것을 의미하는 값입니다.
  * undefined는 null과 달리 하나의 타입이며, **'타입'**이 정해지지 않은 것을 의미하는 값이기도 합니다.
  * NaN은 number 타입이며, **'숫자가 아님'**을 의미하는 숫자입니다.
  * Infinity는 number 타입이며, **'무한대'**를 의미하는 숫자입니다.

​	<br>

자바스크립트는 타입 검사가 매우 유연한 언어이고 문맥에 따라 다음과 같이 자동으로 타입 변환이 이루어집니다.<br>

|    값     | Boolean 문맥 | Number 문맥 | String 문맥 |
| :-------: | :----------: | :---------: | :---------: |
|   null    |    false     |      0      |   'null'    |
| undefined |    false     |     NaN     | 'undefined' |
|    NaN    |    false     |     NaN     |    'NaN'    |
| Infinity  |     true     |  Infinity   | 'Infinity'  |

```html
<!DOCTYPE html>
<html lang="ko">

<head>
	<meta charset="UTF-8">
	<title>JavaScript Number Object</title>
</head>

<body>

	<h1>null, undefined, NaN, Infinity</h1>

	<script>
		document.write((typeof null) + "<br>");
		document.write((typeof undefined) + "<br>");
		document.write((typeof NaN) + "<br>");
		document.write((typeof Infinity) + "<br><br>");

		document.write(Boolean(null) + "<br>");
		document.write(Boolean(undefined) + "<br>");
		document.write(Boolean(NaN) + "<br>");
		document.write(Boolean(Infinity) + "<br><br>");

		document.write(Number(null) + "<br>");
		document.write(Number(undefined) + "<br>");
		document.write(Number(NaN) + "<br>");
		document.write(Number(Infinity) + "<br><br>");

		document.write(String(null) + "<br>");
		document.write(String(undefined) + "<br>");
		document.write(String(NaN) + "<br>");
		document.write(String(Infinity));
	</script>
	
</body>

</html>
```

웹페이지 화면 ▼

![객체예시30](../../images/2022-06-05-class24(Number객체)/객체예시30.png)

<br><br>

* Number 객체

  자바스크립트에서 숫자는 보통 숫자 리터럴을 사용하여 표현합니다.<br>

  하지만 수를 나타낼 때 new 연산자를 사용하여 명시적으로 Number 객체를 생성할 수도 있습니다.<br>

  이러한 Number 객체는 숫자 값을 감싸고 있는 **래퍼(wrapper) 객체**입니다.<br>

  ```html
  <!DOCTYPE html>
  <html lang="ko">
  
  <head>
  	<meta charset="UTF-8">
  	<title>JavaScript Number Object</title>
  </head>
  
  <body>
  
  	<h1>Number 객체</h1>
  
  	<script>
  		var x = 100;						// 숫자 리터럴
  		var y = new Number(100);			// Number 객체
  
  		document.write(x + "<br>");			// 100
  		document.write(y + "<br>");			// 100
  		document.write(typeof x + "<br>");	// number 타입
  		document.write(typeof y + "<br>");	// object 타입
  	</script>
  	
  </body>
  
  </html>
  ```

  웹페이지 화면 ▼

  ![객체예시31](../../images/2022-06-05-class24(Number객체)/객체예시31.png)

  <br>

  동등 연산자(==)는 리터럴 값과 객체의 값이 같으면 true를 반환합니다.<br>

  하지만 일치 연산자(===)는 숫자 리터럴과 Number 객체의 타입이 다르므로, 언제나 false를 반환합니다.<br>

  ```html
  <!DOCTYPE html>
  <html lang="ko">
  
  <head>
  	<meta charset="UTF-8">
  	<title>JavaScript Number Object</title>
  </head>
  
  <body>
  
  	<h1>Number 객체</h1>
  
  	<script>
  		var x = 100;						// 숫자 리터럴 100
  		var y = new Number(100);			// Number 객체 100
  
  		document.write((x == y) + "<br>");	// 값이 같으므로 true
  		document.write(x === y);			// 서로 다른 객체이므로 false
  	</script>
  	
  </body>
  
  </html>
  ```

  웹페이지 화면 ▼

  ![객체예시32](../../images/2022-06-05-class24(Number객체)/객체예시32.png)

  ★new 연산자를 사용하여 객체를 생성할 때에는 매우 많은 추가 연산을 해야만 합니다.<br>

  따라서 가능한 숫자 리터럴을 사용하여 수를 표현하고, Number 객체는 래퍼 객체로만 활용하는 것이 좋습니다.

  <br><br>

* Number 메소드

  Number 객체에 정의되어 있는 숫자와 관련된 작업을 할 때 사용하는 메소드입니다.<br>

  가장 많이 사용되는 대표적인 Number 메소드는 다음과 같습니다.<br>

  <br>

  1. Number.parseFloat()
  2. Number.parseInt()
  3. Number.isNaN()
  4. Number.isFinite()
  5. Number.isInteger()
  6. Number.isSafeInteger()<br><br>

* Number.parseFloat() 메소드

  Number.parseFloat() 메소드는 문자열을 파싱(parsing)하여, 문자열에 포함된 숫자 부분을 실수 형태로 변환합니다.<br>

  문자열에 여러 개의 숫자가 존재하면, 그중에서 첫 번째 숫자만을 실수 형태로 반환합니다.<br><br>

  이 메소드는 전역 함수인 parseFloat() 함수와 완전히 같은 동작을 수행합니다.<br>

  ```html
  <!DOCTYPE html>
  <html lang="ko">
  
  <head>
  	<meta charset="UTF-8">
  	<title>JavaScript Number Method</title>
  </head>
  
  <body>
  
  	<h1>Number.parseFloat() 메소드</h1>
  
  	<script>
  		document.write(Number.parseFloat("12") + "<br>");			// 12
  		document.write(Number.parseFloat("12.34") + "<br>");		// 12.34
  		document.write(Number.parseFloat("12문자열") + "<br>");		// 12
  		document.write(Number.parseFloat("12 34 56") + "<br>");		// 12
  		document.write(Number.parseFloat("문자열 56"));				// NaN
  	</script>
  	
  </body>
  
  </html>
  ```

  웹페이지 화면 ▼

  ![image-20220605175845511](../../images/2022-06-05-class24(Number객체)/image-20220605175845511.png)

  <br><br>

* Number.parseInt() 메소드

  Number.parseInt() 메소드는 문자열을 파싱하여, 문자열에 포함된 숫자 부분을 정수 형태로 반환합니다.<br>

  문자열에 여러 개의 숫자가 존재하면, 그중에서 첫 번째 숫자만을 정수 형태로 반환합니다.<br>

  <br>

  이 메소드는 전역 함수인 parseInt() 와 완전히 같은 동작을 수행합니다.<br>

  ```html
  <!DOCTYPE html>
  <html lang="ko">
  
  <head>
  	<meta charset="UTF-8">
  	<title>JavaScript Number Method</title>
  </head>
  
  <body>
  
  	<h1>Number.parseInt() 메소드</h1>
  
  	<script>
  		document.write(Number.parseInt("12") + "<br>");			// 12
  		document.write(Number.parseInt("12.34") + "<br>");		// 12
  		document.write(Number.parseInt("12문자열") + "<br>");	// 12
  		document.write(Number.parseInt("12 34 56") + "<br>");	// 12
  		document.write(Number.parseInt("문자열 56"));			// NaN
  	</script>
  	
  </body>
  
  </html>
  ```

  웹페이지 화면 ▼

  ![image-20220605180421907](../../images/2022-06-05-class24(Number객체)/image-20220605180421907.png)

  <br><br>

* Number.isNaN() 메소드

  Number.isNaN() 메소드는 전달된 값이 NaN인지 아닌지를 검사합니다.<br><br>

  이 메소드는 전역함수인 isNaN() 함수가 가지고 있던 숫자로의 강제 변환에 따라 발생하는 문제를 더는 겪지 않게 해줍니다.<br>

  이 메소드는 오직 숫자인 값에서만 동작하며, 그 값이 NaN인 경우에만 treu를 반환합니다.<br>

  ```html
  <!DOCTYPE html>
  <html lang="ko">
  
  <head>
  	<meta charset="UTF-8">
  	<title>JavaScript Number Method</title>
  </head>
  
  <body>
  
  	<h1>Number.isNaN() 메소드</h1>
  
  	<script>
  		document.write(Number.isNaN(NaN) + "<br>");			// true
  		document.write(Number.isNaN(0 / 0) + "<br><br>");	// true
  
  		// 다음은 전역 함수인 isNaN()에서 잘못된 결과를 반환하는 예제임.
  		document.write(isNaN("NaN") + "<br>");				// true
  		document.write(isNaN(undefined) + "<br>");			// true
  		document.write(isNaN("문자열") + "<br><br>");		// true
  
  		// Number.isNaN() 메소드에서는 맞는 결과를 반환하고 있음.
  		document.write(Number.isNaN("NaN") + "<br>");		// false
  		document.write(Number.isNaN(undefined) + "<br>");	// false
  		document.write(Number.isNaN("문자열"));				// false
  	</script>
  	
  </body>
  
  </html>
  ```

  웹페이지 화면 ▼

  ![image-20220605180657301](../../images/2022-06-05-class24(Number객체)/image-20220605180657301.png)

  <br><br>

* Number.isFinite() 메소드

  Number.isFinite() 메소드는 전달된 값이 유한한 수인지 아닌지를 검사합니다.<br>

  이 메소드는 전역 함수인 isFinite() 함수처럼 전달된 값을 숫자로 강제 변환하지 않습니다.<br>

  이 메소드는 오직 셀 수 있는 값에서만 동작하며, 그 값이 유한한 경우에만 true를 반환합니다.<br>

  ```html
  <!DOCTYPE html>
  <html lang="ko">
  
  <head>
  	<meta charset="UTF-8">
  	<title>JavaScript Number Method</title>
  </head>
  
  <body>
  
  	<h1>Number.isFinite() 메소드</h1>
  
  	<script>
  		document.write(Number.isFinite(0) + "<br>");		// true
  		document.write(Number.isFinite(3e45) + "<br><br>");	// true
  
  		document.write(Number.isFinite(Infinity) + "<br>");	// false
  		document.write(Number.isFinite(NaN) + "<br><br>");	// false
  
  		// 다음은 전역 함수인 isFinite()에서 잘못된 결과를 반환하는 예제임.
  		document.write(isFinite("0") + "<br>");				// true
  		document.write(isFinite(null) + "<br><br>");		// true
  
  		// Number.isFinite() 메소드에서는 맞는 결과를 반환하고 있음.
  		document.write(Number.isFinite("0") + "<br>");		// false
  		document.write(Number.isFinite(null));				// false
  	</script>
  	
  </body>
  
  </html>
  ```

  웹페이지 화면 ▼

  ![image-20220605181256698](../../images/2022-06-05-class24(Number객체)/image-20220605181256698.png)

  <br><br>

* Number.isInteger() 메소드

  Number.isInteger() 메소드는 전달된 값이 정수인지 아닌지를 검사합니다.<br>

  전달된 값이 정수이면 true를 반환하며, 정수가 아니거나  NaN, Infinity와 같은 값은 모두 false를 반환합니다.<br>

  ```html
  <!DOCTYPE html>
  <html lang="ko">
  
  <head>
  	<meta charset="UTF-8">
  	<title>JavaScript Number Method</title>
  </head>
  
  <body>
  
  	<h1>Number.isInteger() 메소드</h1>
  
  	<script>
  		document.write(Number.isInteger(0) + "<br>");			// true
  		document.write(Number.isInteger(-100) + "<br><br>");	// true
  
  		document.write(Number.isInteger(0.1) + "<br>");			// false
  		document.write(Number.isInteger("문자열") + "<br>");	// false
  		document.write(Number.isInteger(Infinity) + "<br>");	// false
  		document.write(Number.isInteger(true));					// false
  	</script>
  	
  </body>
  
  </html>
  ```

  웹페이지 화면 ▼

  ![image-20220605181517146](../../images/2022-06-05-class24(Number객체)/image-20220605181517146.png)

  <br><br>

* Number.isSafeInteger() 메소드

  Number.isSafeInteger() 메소드는 전달된 값이 안전한 정수(safe integer)인지 아닌지를 검사합니다.<br>

  <br>

  안전한 정수(safe integer)란 IEEE 754 국제 표준에서 정의한 64비트 부동 소수점 수로 정확히 표현되는 정수를 의미합니다.<br>

  -(2<sup>53</sup> - 1)부터 (2<sup>53</sup> - 1)까지의 모든 정수가 안전한 정수에 포함됩니다.<br>

  ```html
  <!DOCTYPE html>
  <html lang="ko">
  
  <head>
  	<meta charset="UTF-8">
  	<title>JavaScript Number Method</title>
  </head>
  
  <body>
  
  	<h1>Number.isSafeInteger() 메소드</h1>
  
  	<script>
  		document.write(Number.isSafeInteger(10) + "<br>");						// true
  		document.write(Number.isSafeInteger(Math.pow(2, 53) - 1) + "<br><br>");	// true
  
  		document.write(Number.isSafeInteger(Math.pow(2, 53)) + "<br>");			// false
  		document.write(Number.isSafeInteger(Infinity) + "<br>");				// false
  		document.write(Number.isSafeInteger(NaN) + "<br>");						// false
  		document.write(Number.isSafeInteger(3.14));								// false
  	</script>
  	
  </body>
  
  </html>
  ```

  웹페이지 화면 ▼

  ![image-20220605182053726](../../images/2022-06-05-class24(Number객체)/image-20220605182053726.png)

  <br><br>

* Number.prototype 메소드

  모든 Number 인스턴스는 Number.prototype으로부터 메소드와 프로퍼티를 상속받습니다.<br>

  가장 많이 사용되는 대표적인 Number.prototype 메소드는 다음과 같습니다.<br>

   <br>

  1. Number.prototype.toExponential()

  2. Number.prototype.toFixed()

  3. Number.prototype.toPrecision()

  4. Number.prototype.toString()

  5. Number.prototype.valueOf()

  <br><br>

* toExponential() 메소드

  Number 인스턴스의 값을 지수 표기법으로 변환한 후, 그 값을 문자열로 반환합니다.<br>

  이 때 전달받은 값은 지수 표기법에서 소수 부분의 자릿수로 사용됩니다.<br>

  ```html
  원형
  numObj.toExponential([소수부분의자릿수])
  ```

  ```html
  <!DOCTYPE html>
  <html lang="ko">
  
  <head>
  	<meta charset="UTF-8">
  	<title>JavaScript Number Method</title>
  </head>
  
  <body>
  
  	<h1>toExponential() 메소드</h1>
  
  	<script>
  		var num = 12.3456; // Number 인스턴스를 생성함.
  
  		document.write(num.toExponential() + "<br>");		// 1.23456e+1
  		document.write(num.toExponential(2) + "<br>");		// 1.23e+1
  		document.write(num.toExponential(4) + "<br>");		// 1.2346e+1
  		document.write(12.3456.toExponential());			// 1.23456e+1
  	</script>
  	
  </body>
  
  </html>
  ```

  웹페이지 화면 ▼

  ![image-20220605182439159](../../images/2022-06-05-class24(Number객체)/image-20220605182439159.png)

  <br><br>

* toFixed() 메소드

  Number 인스턴스의 소수 부분 자릿수를 전달받은 값으로 고정한 후, 그 값을 문자열로 반환합니다.<br>

  ```html
  원형
  numObj.toFixed([소수부분의자릿수])
  ```

  ```html
  <!DOCTYPE html>
  <html lang="ko">
  
  <head>
  	<meta charset="UTF-8">
  	<title>JavaScript Number Method</title>
  </head>
  
  <body>
  
  	<h1>toFixed() 메소드</h1>
  
  	<script>
  		var num = 3.14159265; // Number 인스턴스를 생성함.
  
  		document.write(num.toFixed() + "<br>");			// 3
  		document.write(num.toFixed(2) + "<br>");		// 3.14
  		document.write(num.toFixed(4) + "<br>");		// 3.1416
  		document.write(3.14159265.toFixed(6));			// 3.141593
  	</script>
  	
  </body>
  
  </html>
  ```

  웹페이지 화면 ▼

  ![image-20220605182613435](../../images/2022-06-05-class24(Number객체)/image-20220605182613435.png)

  <br><br>

* toPrecision() 메소드

  이 메소드는 Number 인스턴스의 가수와 소수 부분을 합친 자릿수를 전달받은 값으로 고정한 후, 그 값을 문자열로 반환합니다.

  ```html
  원형
  numObj.toString([진법])
  ```

  ```html
  <!DOCTYPE html>
  <html lang="ko">
  
  <head>
  	<meta charset="UTF-8">
  	<title>JavaScript Number Method</title>
  </head>
  
  <body>
  
  	<h1>toString() 메소드</h1>
  
  	<script>
  		var num = 255; // Number 인스턴스를 생성함.
  
  		document.write(num.toString() + "<br>");		// 255
  		document.write((255).toString() + "<br>");		// 255
  		document.write((3.14).toString() + "<br>");		// 3.14
  		document.write(num.toString(2) + "<br>");		// 11111111
  		document.write((100).toString(16) + "<br>");	// 64
  		document.write((-0xff).toString(2));			// -11111111
  	</script>
  	
  </body>
  
  </html>
  ```

  웹페이지 화면 ▼

  ![image-20220605182941187](../../images/2022-06-05-class24(Number객체)/image-20220605182941187.png)

  ★숫자 리터럴에 toString() 메소드를 사용할 때에는 반드시 괄호(())를 사용하여 숫자 리터럴을 감싸줘야 합니다.<br>
  그렇지 않으면 자바스크립트는 SyntaxError를 발생한 후, 프로그램을 중지시킬 것입니다.

  <br><br>

* toString() 메소드

  이 메소드는 Number 인스턴스의 값을 문자열로 반환합니다.<br>

  전달받은 값에 해당하는 진법으로 우선 값을 변환한 후, 그 값을 문자열로 반환합니다.<br>

  ```html
  원형
  numObj.toString([진법])
  ```

  ```html
  <!DOCTYPE html>
  <html lang="ko">
  
  <head>
  	<meta charset="UTF-8">
  	<title>JavaScript Number Method</title>
  </head>
  
  <body>
  
  	<h1>toString() 메소드</h1>
  
  	<script>
  		var num = 255; // Number 인스턴스를 생성함.
  
  		document.write(num.toString() + "<br>");		// 255
  		document.write((255).toString() + "<br>");		// 255
  		document.write((3.14).toString() + "<br>");		// 3.14
  		document.write(num.toString(2) + "<br>");		// 11111111
  		document.write((100).toString(16) + "<br>");	// 64
  		document.write((-0xff).toString(2));			// -11111111
  	</script>
  	
  </body>
  
  </html>
  ```

  웹페이지 화면 ▼

  ![image-20220605183100073](../../images/2022-06-05-class24(Number객체)/image-20220605183100073.png)

  ★숫자 리터럴에 toString() 메소드를 사용할 때에는 반드시 괄호(())를 사용하여 숫자 리터럴을 감싸줘야 합니다.<br>
  그렇지 않으면 자바스크립트는 SyntaxError를 발생한 후, 프로그램을 중지시킬 것입니다.

  <br>

  <br>

* valueOf() 메소드

  이 메소드는 Number 인스턴스가 가지고 있는 값을 반환합니다.<br>

  ```html
  원형
  numObj.valueOf()
  ```

  ```html
  <!DOCTYPE html>
  <html lang="ko">
  
  <head>
  	<meta charset="UTF-8">
  	<title>JavaScript Number Method</title>
  </head>
  
  <body>
  
  	<h1>valueOf() 메소드</h1>
  
  	<script>
  		var numObj = new Number(123); 	// 123의 값을 가지는 Number 인스턴스를 생성함.
  		document.write(typeof numObj + "<br>");	// object
  
  		var num = numObj.valueOf();
  		document.write(num + "<br>");	// 123
  		document.write(typeof num);		// number
  	</script>
  	
  </body>
  
  </html>
  ```

  웹페이지 화면 ▼

  ![image-20220605183317432](../../images/2022-06-05-class24(Number객체)/image-20220605183317432.png)

  

  

  

