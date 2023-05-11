---
categories: Coding	
tag: Java
toc: true
---

# 2023. 01. 09. 수업 내용 정리

##  Math, Integer, Double 클래스...

<br>

# Math 클래스
* Math 클래스(`java.lang.Math`)는 수학과 관련된 유틸리티(Utility)성 기능을 포함하고 있다. (유틸리티성 클래스 : 어떠한 클래스가 유틸리티의 성질을 가질 때 이가 가지는 모든 멤버는 정적이어야하며, 객체화가 불가능해야 한다.)
* Math 클래스는 유틸리티성 클래스로, 객체화가 불가능하다.

<br><br>
## 정적 멤버 필드(Static Member Field)
* `E` : 자연 상수(_e_) 
* `PI` : 파이(_𝝅_) 

<br><br>
## 정적 메서드(Static Method)
* `abs(x)` : 어떠한 숫자(`int`, `long`, `float`, `double` 등)의 절댓값(Absolute)을 반환한다.
* `addExact(x,y)`  : 정수(`int`,`long`)인 `x`와 `y`를 더한 값을 반환한다. 단, 오버플로우(Overflow) 가 발생할 경우 예외(오류)를 발생시킨다.
* `cbrt(x)` : 실수(`double`) `x`에 대해 세제곱근(Cube Root)인 실수(`double`)를 반환한다.
* `ceil(x)` : 실수(`double`) `x`를 올림(Ceiling)한 실수(`double`)를 반환한다.  
* `cos(x)` : 실수(`double`) `x`에 대한 코사인값인 실수(`double`)를 반환한다. 
* `floor(x)` : 실수(`double`) `x`를 내림(Floor)한 실수(`double`)를 반환한다.
* `log(x)` : 실수(`double`) `x`에 대한 자연로그값인 실수(`double`)를 반환한다. 
* `log10(x)` : 실수(`double`) `x`에 대한 상용로그값인 실수(`double`)를 반환한다. 
* `max(x, y)` : 숫자(`int`,`long`,`float`,`double` 등)인 `x`와 `y` 중 큰 값을 반환한다. 
* `min(x, y)` : 숫자(`int`,`long`,`float`,`double` 등)인 `x`와 `y` 중 작은 값을 반환한다.
* `multiplyExact(x, y)` : 정수(`int`,`long`)인 `x`와 `y`의 곱을 반환한다. 단, 오버플로우(Overflow)가 발생할 경우 예외를 발생시킨다.
* `pow(x, y)` : 실수(`double`)인 `x`와 `y`에 대해 `x`의 `y`승(Power)인 실수(`double`)를 반환한다.
* `random()` : 0 이상 1 미만의 실수 중 랜덤한 실수(`double`)를 반환한다. 
* `sin(x)` : 실수(`double`) `x`에 대한 사인(Sine)값인 실수(`double`)를 반환한다. 
* `sqrt(x)` : 실수(`double`) `x`에 대한 제곱근(Square Root)인 실수(`double`)를 반환한다.
* `subtractExact(x, y)` : 정수(`int`,`long`)인 `x`에서 `y`를 뺀 값을 반환한다. 단, 오버플로우(Overflow)가 발생할 경우 예외를 발생시킨다.
* `tan(x` : 실수(`double`) `x`에 대한 탄젠트(Tangent)값인 실수(`double`)를 반환한다.
* `toIntExact(x)` : 큰 정수(`long`)인 `x`를 작은 정수(`int`)로 변환하여 반환한다. 단, 오버플로우(Overflow)가 발생할 경우 예외를 발생시킨다. 


<br><br><br><br>

# Integer 클래스
* Integer(`java.lang.Integer`) 클래스는 정수와 관련된 기능 및 정수 **값 자체**(객체)로도 작동한다.
* 정수 값을 받되, 간혹 고의적으로 `null` 값이 지정되어야 하는 경우가 있다면, `int` 대신 `Integer` 타입을 사용하기도 한다.

<br><br>
## 정적 멤버 필드(Static Member Field)
* `MAX_VALUE` : 정수(`int`)타입이 가질 수 있는 가장 큰 값이다.
* `MIN_VALUE` : 정수(`int`)타입이 가질 수 있는 가장 작은 값이다.

<br><br>
## 정적 메서드(Static Method)
* `max(int x, int y)` : `java.lang.Math.max(x, y)`를 호출한 결과이다.
* `min(int x, int y)` : `java lang.Math.min(x, y)`를 호출한 결과이다. 
* `parseInt(String x)` : 문자열(`String`)인 매개변수 `x`를 정수(`int`)로 변환하여 반환한다. 단, 변환이 불가능한 경우, `NumberFormatException` 예외가 발생할 수 있음으로 유의한다. 
* `toBinaryString(int x)` : 정수(`int`) `x`를 이진법으로 바꾼 문자열(`String`)로 반환한다. 
* `toHexString(int x)` : 정수(`int`) `x`를 16진법으로 바꾼 문자열(`String`)로 반환한다.
* `toOctalString(int x)` : 정수(`int`) `x`를 8진법으로 바꾼 문자열(`String`)로 반환한다. 
* `valueOf(int x)` : `x`를 `Integer` 타입으로 반환하여 반환한다. 
* `valueOf(String x)` : 문자열(`String`) `x`를 `Integer` 타입으로 변환하여 반환한다. 

<br><br>
## 비정적 메서드(Non-static(Instance) Method)
* `byteValue()` : 객체가 가진 정수(`int`) 값을 `byte`로 변환하여 반환한다.
* `doubleValue()` : 객체가 가진 정수(`int`) 값을 `double`로 반환하여 반환한다. 
* `equeals(Object o)` : `Object` 인 `o`가 `Integer`로 변환될 수 있고, 해당 값이 객체의 값과 같은가의 여부(`boolean`)를 반환한다. 
* `floatValue()` : 객체가 가진 정수(`int`) 값을 `float`으로 변환하여 반환한다.
* `intValue()` : 객체가 가진 정수(`int`) 값을 반환한다.
* `longValue()` : 객체가 가진 정수(`int`) 값을 `long`으로 변환하여 반환한다.
* `shortValue()` : 객체가 가진 정수(`int`) 값을 `short`로 변환하여 반환한다.
* `toString()` : 객체가 가진 정수(`int`) 값을 `String`으로 변환하여 반환한다.

<br><br><br><br>

# Double 클래스
* Double(`java.lang.Double`) 클래스는 실수와 관련된 기능 및 정수 값 자체(객체)로도 작동한다. 
* 실수 값을 받되, (간혹) 고의적으로 `null` 값이 지정되어야 하는 경우가 있다면, `double` 대신 `Double` 타입을 사용하기도 한다. 

<br><br>
## 정적 멤버 필드(Static Member Field)
* `MAX_VALUE` : 실수(`double`)타입이 가질 수 있는 가장 큰 값이다.
* `MIN_VALUE` : 실수(`double`)타입이 가질 수 있는 가장 작은 값이다.
* `NaN` : 숫자가 아님(Not a Number)에 대한 값이다. 구현은 `0`을 `0`으로 나눈 값으로 초기화되어 있다. 
* `NEGATIVE_INFINITY` : 음의 무한수에 대한 값이다. 구현은 `-1` 을 `0`으로 나눈 값으로 초기화되어 있다.
* `POSITIVE_INFINITY` : 음의 무한수에 대한 값이다. 구현은 `1` 을 `0`으로 나눈 값으로 초기화되어 있다.

<br><br>
## 정적 메서드(Static Method)
* `isFinite(double x)` : 실수(`double`) `x`가 유한수인가에 대한 여부(`boolean`)를 반환한다. 
* `isInfinite(double x)` : 실수(`double`) `x`가 무한수인가에 대한 여부(`boolena`)를 반환한다.
* `isNaN(double x)` : 실수(`double`) `x`가 숫자가 아닌 값(Not a number)인가에 대한 여부(`boolean`)를 반환한다. 
* `max(double x, double y)` : `java.lang.Math.max(x, y)`를 호출한 결과이다.
* `min(double x, double y)` : `java.lang.Math.min(x, y)`을 호출한 결과이다.
* `parseDouble(String x)` : 문자열(`String`)인 매개변수 `x`를 실수(`double`)로 변환하여 반환한다. 단, 변환이 불가능한 경우, `NumberFormatException` 예외가 발생할 수 있음으로 유의한다. 
* `toHexString(double x)` : 실수(`double`) `x`를 16진법으로 바꾼 문자열(`String`)로 반환한다. 
* `valueOf(double x)` : 실수(`double`) `x`를 `Double` 타입으로 변환하여 반환한다.
* `valueOf(String x)` : 문자열(`String`) `x`를 `Double` 타입으로 변환하여 반환한다.

<br><br>
## 비정적 메서드(Non-static(instance) Method)
* `byteValue()` : 객체가 가진 실수(`double`) 값을 `byte`로 변환하여 반환한다.
* `doubleValue()` : 객체가 가진 실수(`double`) 값을 `double`로 반환하여 반환한다.
* `equeals(Object o)` : `Object` 인 `o`가 `Integer`로 변환될 수 있고, 해당 값이 객체의 값과 같은가의 여부(`boolean`)를 반환한다.
* `floatValue()` : 객체가 가진 실수(`double`) 값을 `float`으로 변환하여 반환한다.
* `intValue()` : 객체가 가진 실수(`double`) 값을 반환한다.
* `isInfinite()` : 객체가 가진 실수(`double`)가 무한수인가에 대한 여부(`boolean`)를 반환한다. 
* `isNaN()` : 객체가 가진 실수(`double`)가 숫자가 아닌 값(Not a Number)인가에 대한 여부(`boolean`)를 반환한다. 
* `longValue()` : 객체가 가진 실수(`double`) 값을 `long`으로 변환하여 반환한다.
* `shortValue()` : 객체가 가진 실수(`double`) 값을 `short`로 변환하여 반환한다.
* `toString()` : 객체가 가진 실수(`double`) 값을 `String`으로 변환하여 반환한다.

<br><br><br><br>
