---
categories: Coding	
tag: Java
toc: true
author_profile: false
---

# 2023. 01. 10. 수업 내용 정리

##  Scanner, SimpleDateFormat, StringBuilder

<br>

# 기타 클래스

## Scanner
* `Scanner (java.util.Scanner)` 클래스는 파일 및 사용자 입력을 처리하기 위한 클래스이다. 주로 사용자 입력을 처리하기 위해 사용한다.
* 사용자 입력을 처리하기 위해서는 생성자(Constructor)의 전달 인자로, `inputStream` 타입의 객체인 `System.in`을 전달해야 한다.
* 비정적 메서드(객체(인스턴스) 메서드)
   * `next()` : 사용자가 입력한 문자열을 반환한다. 
   * `nextBoolean()` : 사용자가 입력한 논리값(`booelan`)을 반환한다.
   * `nextByte()` : 사용자가 입력한 정수값(`byte`)을 반환한다.
   * `nextDouble()` : 사용자가 입력한 실수값(`double`)을 반환한다.
   * `nextFloat()` : 사용자가 입력한 실수값(`float`)을 반환한다.
   * `nextInt()` : 사용자가 입력한 정수값(`int`)을 반환한다.
   * `nextLong()` : 사용자가 입력한 정수값(`long`)을 반환한다.
   * `nextShort()` : 사용자가 입력한 정수값(`short`)을 반환한다.
   * `nextLine()` : 사용자가 입력한 문자열(`String`)값을 반환하는데 분리자(개행자=Enter)를 제외하지 않는다.

## SimpleDateFormat
* `SimpleDateFormat`(`java.text.SimpleDateFormat`) 클래스는 어떠한 `date``(java.util.Date)`타입의 날짜 및 시간을 가지는 객체를 쉽게 특정 패턴에 맞게 문자열화할 수 있게 도와준다. 
* `applyPattern(String x)` : 객체가 가지는 패턴을 `x`로 지정한다. 해당 전달 인자는 생성자(Constructor)의 전달 인자로 갈음(다른 것으로 바꾸어 대신하다)할 수 있다.  
* `format(Date x)` : `Date``(java.util.Date)` 타입의 객체 `x`가 가진 날짜와 시간을 `SimpleDateFormat` 타입의 객체가 가지고 있는 패턴에 맞게 문자열화하여 반환한다. 
* `parse(String x)` : `SimpleDateFormat` 객체가 가진 패턴으로 문자열 `x`를 분석하여 새로운 `Date` 타입의 객체로 반환한다.
* `toPattern()` : 객체가 가지고 있는 패턴을 문자열(`String`)로 반환한다. 
*  패턴 
    * `yy` : 두 자리 년도
    * `yyyy` : 네 자리 년도 
    * `M` : 한 자리 월
    * `MM` : 두 자리 월
    * `MMM` : 시스템 언어상의 월(영어 : 1 → Jan, 한국어 : 1 → 1월)
    * `w` : 1년 중 몇 번째 주
    * `W` : 월중 몇 번째 주 
    * `D` : 연중 몇 번째 일
    * `d` : 연중 몇 번쨰 일(한 자리의 일)
    * `dd` : 두 자리 일
    * `H` : 한 자리 시(24시제)
    * `HH` : 두 자리 시(24시제)
    * `h` : 한 자리 시(12시제)
    * `hh` : 두 자리 시(12시제)
    * `a` : 오전/오후(영어 : AM/PM)
    * `m` : 한 자리 분
    * `mm` : 두 자리 분
    * `s` : 한 자리 초
    * `ss` : 두 자리 초
    * `S` : 한 자리 밀리초
    * `SS` : 두 자리 밀리초 
    * `SSS` : 세 자리 밀리초 


## StringBuilder
* `StringBuilder(java.lang.StringBuilder)` 클래스는  문자열 이어붙이기(Concatenation)를 할 때 사용한다. 객체 자체가 문자열 리터럴을 의미하지 않으며 최종적으로 toString() 메서드를 호출해야 객체가 가지고 있는 이어 붙여진 문자열 하나가 반환된다.
* `appned(* x)` : (★) 모든 타입을 지원하는 매개변수인 `x`를 객체가 가진 문자열 마지막에 이어 붙인다.
* `charAt(int x)` : 객체가 가진 문자열을 문자 배열로 하였을 때 `x`번째 문자(`char`)를 반환한다.
* `delete(int x, int y)` : 객체가 가진 문자열을 문자 배열로 하였을 때 `x`번째 부터 `y`번째 까지의 문자를 제거한다.
* `deleteCharAt(int x)` : 객체가 가진 문자열을 문자 배열로 하였을 때 `x`번째 문자를 제거한다.
* `indexOf(String x)` : 객체가 가진 문자열 중 `x`를 포함하는 시작 점의 순번(`int`)을 반환한다.
* `insert(int x, String y)` : `x`번째에 `y`문자열을 삽입한다. 
* `lastIndexOf(String x)` : 객체가 가진 문자열 중 `x`를 포함하는 마지막 시작 점의 순번(`int`)을 반환한다.
* `toString` : (★) 객체가 가진 내용을 문자열(`String`)로 반환한다.
