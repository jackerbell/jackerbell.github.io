---
categories: Coding	
tag: Java
toc: true
author_profile: false
---

# 2023. 01. 04. 수업 내용 정리

# String 클래스

## 정적 메서드 
<br>

1. `copyValueOf(char[] x)`: `valueOf(char[] x)`와 동일하다.
2. `format(String x, Object... y)` : 매개변수 `x` 에 명시된 형식에 인자인 값(들) `y`를 순차적으로 집어 넣어 새로운 문자열(`String`)로 반환한다. 
<br>

3. `join(String x, String... y)` : 매개변수 `y`가 가지는 문자열(`String`)들 사이에 `x`를 넣어 이어 붙인 새로운 문자열(`String`)을 반환한다.
   >```java
   >String[] cities = {"서울", "대전", "대구", "부산"};
   >System.out.println(String.join(" ~ ", cities )); // "서울 ~ 대전 ~ 대구 ~ 부산"
   >```
<br>

4. `valueOf(boolean x)` : 전달받은 `x`를 문자열(`String`)로 반환한다.
5. `valueOf(char x)` : 전달받은 `x`를 문자열로 반환한다.
6. `valueOf(char[] x)` : 전달받은 문자 배열(`char[]`)인 배개변수 `x`를 문자열(`String`)로 반환한다.
7. `valueOf(double x)` : 전달받은 `x`를 문자열(`String`)로 반환한다.
8. `valueOf(float x)` : 전달받은 `x`를 문자열(`String`)로 반환한다.
9. `valueOf(int x)` : 전달받은 `x`를 문자열(`String`)로 반환한다.
10. `valueOf(long x)` : 전달받은 `x`를 문자열(`String`)로 반환한다.

<br>

## 객체메서드(비정적 메서드)

<br>

1. `charAt(x)`:`x`번째 문자를 반환한다. 이때 `x`는 `0`부터 시작함에 유의한다. 
    >```java
    > String message = "Hello";
    > char secondChar = message.charAt(1);
    > System.out.println(secondChar); // e  
    >```
    <br>

2. `contact(String x)`:호출 대상인 문자열 끝에 문자열 `x`를 이어 붙인 문자열(`String`)을 반환한다.
    >```java
    >String h = "Hello";
    >String w = "World";
    >String message = h.contact(w); // 문자열 h 뒤에 w 문자열을 이어붙인 문자열을 반환..
    >System.out.println(message); // HelloWorld
    >```
    <br>

3. `contains(String x)`:호출 대상인 문자열이 매개변수인 문자열 `x`를 내용으로 포함하는가에 대한 여부(`boolean`)를 반환한다.
    >```java
    >String message = "Hello World!";
    >System.out.println(message.contains("Hello"));
    >System.out.println(message.contains("World"));
    >System.out.println(message.contains("Hi"));
    >```
    <br>

4. `contentEquals(String x)`: 호출 대상인 문자열이 가지는 내용과 매개변수인 문자열 `x`가 가지는 내용이 같은가에 대한 여부(`boolean`)를 반환한다. `equals(...)`메서드의 용도와 유사하다.
   >```java
   >String message1 = "Hello World!";
   >String message2 = "Hello World?";
   >System.out.println(message1.contentEquals(message2)); // false
   >```
   <br>

5. `endsWith(String x)`: 호출 대상인 문자열이 가지는 내용이 매개변수인 문자열 `x`로 끝나는가에 대한 여무(`boolean`)를 반환한다.
   >```java
   >String message = "Hello World!"; 
   >System.out.println(message.endsWith("!")); // true
   >System.out.println(message.endsWith("d!")); // true
   >System.out.println(message.endsWith("rld!")); // true
   >System.out.println(message.endsWith("World!")); // false
   >```
   <br>

6. `equals(Object x)`: 호출 대상이 매개변수인 `Object` `x`와 동일한가에 대한 여부(`boolean`)를 반환한다. 단, `x`가 문자열(`String`)타입으로 형변환 가능한 경우, `contentEquals(...)` 메서드와 동일하게 작동한다.
   >```java
   >String message1 = "Hello World!"; 
   >String message2 = "Hello World?";
   >System.out.println(message1.equals(message2)); //false
   >```
   <br>

7. `equalsIgnoreCase(String x)`: `contentEquals(...)` 메서드와 동일하지만 호출 대상이 되는 문자열과 매개변수인 문자열을 비교할 때 대소문자를 가리지 않는다는 차이가 있다.
   >```java
   >String message1 = "Hello World!"; 
   >String message2 = "Hello WorlD?";
   >System.out.println(message1.equals(message2)); //false
   >System.out.println(message1.equalsIgnoreCase(message2)); //true
   >```
   <br>

8. `indexOf(String x)`:호출 대상이 가지는 내용 중 매개변수인 문자열`x`의 내용에 대한 시작점인 순번(`int`)을 반환한다. 없다면 `-1`을 반환한다. 단 `x`를 여러번 포함하고 있다면 가장 빠른 순번을 반환한다.
   >```java
   >String alphabet = "ABCDEF"
   >System.out.println(alphabet.indexOf("C")); //2
   >System.out.println(alphabet.indexOf("CDE")); //2
   >System.out.println(alphabet.indexOf("Z")); //-1
   >```
   >
   >```java
   >String message = "Apple, Banana, Orange, Sweet Orange, Black Orange, Color Orange, Oranges, More Oranges";
   >Systme.out.println(message.indexOf("Orange")); // 8
   >```
   <br>

9. `isEmpty()`: 호출 대상인 문자열의 내용이 없는가(빈 문자열인가)에 대한 여부(`boolean`)를 반환한다.
<br>


10. `lastIndexOf(String x)`:`indexOf(...)` 메서드와 동일하나 `x`를 여러번 포함하고 있는 경우 마지막 순번을 반환한다. 어떠한 문자열이 어떤 문자열을 한 번만 포함하는가의 여부를 `indexOf` 메서드와 `lastIndexOf` 메서드의 호출 결과가 같음을 보고 알 수 있다. 
   >```java
   >String message = "Banana, Orange, Sweet Orange, Black Orange, Color Orange, Oranges, More Oranges";
   >Systme.out.println(message.lastIndexOf("Orange")); // 72
   >```
<br>

11. `length()`: 호출 대상인 문자열이 가지는 문자의 개수를 반환한다. 배열의 속성()
   >```java
   >System.out.println("한글English1234".length()); //12
   >```
<br>

12. `matches(String x)`: 호출 대상인 문자열이 가지는 내용이 매개변수인 문자열 `x`에 대한 정규표현식(Regular Expression)에 상응하는가에 대한 여부(`boolean`)를 반환한다. (어려움)
   >```java
   >String someInput = "12345";
   >System.out.println(someInput.matches("^([0-9]{5}$)")); // true
   >```
<br>

13. `repeat(int x)`: 호출 대상인 문자열의 내용을 `x`번 반복한 새로운 문자열(`String`)을 반환한다.
   >```java
   >String aaa = "a".repeat(10);
   >System.out.println(aaa); // "aaaaaaaaa"
   >```
<br>

14. `replace(String x, String y)`: 호출 대상인 문자열의 내용에서 문자열 `x`를 찾아 문자열 `y`로 치환한 새로운 문자열(`String`)을 반환한다. 
   >```java
   >String diet = "밥, 야채1, 야채2, 야채3";
   >System.out.println(diet.replace("야채","고기")); // "밥, 고기1, 고기2, 고기3"
   >```
<br>

15. `replaceAll(String x, String y)`: 호출 대상인 문자열의 내용에서 문자열 `x`인 정규표현식에 일치하는 내용을 `y`치환한 새로운 문자열(`String`)을 반환한다. 
   >```java
   >String input = "제 휴대폰 번호는 010-1234-5678입니다.";
   >System.out.println(input.replaceAll("[^0-9]","")); // 01012345678
   >```
<br>

16. `split(String x)`: 호출 대상이되는 문자열에서 매개변수인 문자열 `x`를 기준으로 나눈 문자열 배열(`String[]`)을 반환한다. 만약 `x`에 빈 문자열을 전달하면, 문자 단위로 자른 문자열 배열을 반환한다. 이때 나누는 기준이 되는 `x`는 사라짐으로 유의한다. 또한 나누는 기준 `x`를 포함하고 있지 않다면 호출 대상이 되는 문자열의 내용을 그대로 가지는 길이가 1인 문자열 배열을 반환한다.
   >```java
   >String input = "Hello? Nice to meet you!";
   >String[] inputArray = input.split(" ");
   >for(int i = 0 ; i < inputArray.length; i++){
   >   Systme.out.println(i+":"+inputArray[i]);
   >}
   >// 0: Hello?
   >// 1: Nice
   >// 2: to
   >// 3: meet
   >// 4: you!
   >```
<br>

17. `startsWith(String x)`: 호출 대상이 되는 문자열의 내용이 매개변수인 문자열 `x`로 시작하는가에 대한 여부(`boolean`)를 반환한다.
   >```java
   >String message = "Hello World!";
   >System.out.println(message.startsWith("hello")); // false
   >System.out.println(message.startsWith("Hell")); // true
   >System.out.println(message.startsWith("Hello W")); // true
   >System.out.println(message.startsWith("Hello World")); // true
   >```
<br>

18. `strip()`: 호출 대상이되는 문자열의 **앞, 뒤**에 있는 공백(유니코드 상 공백 포함)을 모두 제거한 새로운 문자열을 반환한다.
   >```java
   >String message = "    A   B  C DE      ";
   >System.out.println(message.strip()); // "A   B  C DE"
   >```
<br>

19. `stripLeading()`: 호출 대상이되는 문자열의 **앞**에 있는 공백(유니코드 상 공백 포함)을 모두 제거한 새로운 문자열(`String`)을 반환한다.
   >```java
   >String message = "    A   B  C DE      ";
   >System.out.println(message.stripLeading()); // "A   B  C DE        "
   >```
<br>

20. `stripTrailing()`: 호출 대상이되는 문자열의 **뒤**에 있는 공백(유니코드 상 공백 포함)을 모두 제거한 새로운 문자열(`String`)을 반환한다.
   >```java
   >String message = "    A   B  C DE      ";
   >System.out.println(message.stripTrailing()); // "    A   B  C DE"
   >```
<br>

21. `subString(int x, int y)`: 호출 대상이되는 문자열이 가지는 문자들의 순번 상에서 `x`번부터 `y`번 앞까지의 내용을 새로운 문자열로 만들어 반환한다.
   >```java
   >String message = "ABCDEF";
   >System.out.println(message.subString(2,3)) // "C"
   >```
<br>

22. `toCharArray()`: 호출 대상이 되는 문자열이 가지는 내용을 문자 배열(`char[]`)로 반환한다.
<br>

23. `toLowerCase()`: 호출 대상이 되는 문자열이 가지는 알파벳 중 대문자인 것을 소문자로 치환한 새로운 문자열(`String`)을 반환한다.
   >```java
   > String message = "Hello Very Glad to See You";
   >System.out.println(message.toLowerCase());  // "hello very glad to see you" 
   >```
<br>

24. `toUpperCase()`: 호출 대상이 되는 문자열이 가지는 알파벳 중 소문자인 것을 대문자로 치환한 새로운 문자열(`String`)을 반환한다.
   >```java
   > String message = "hello very glad to see you";
   >System.out.println(message.toUpperCase());  // HELLO VERY GLAD TO SEE YOU"
   >```
<br>

25. `trim()`: 호출 대상이되는 문자열의 앞, 뒤에 있는 공백(유니코드 상 20번 이하)을 모두 제거한 새로운 문자열(String)을 반환한다. 특별한 목적이 잇는 것이 아니라면 `strip()`을 대신 사용하자.
   >```java
   >String message = "   A B C D E    ";
   >Systme.out.println(message.trim()); // "A B C D E"
   >```
<br>
