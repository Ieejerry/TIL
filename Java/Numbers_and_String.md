# 숫자와 문자

> 생활코딩 Java 입문 강의를 들으면서 강의의 내용 정리

프로그래밍 입문자에게 가장 익숙한 데이터 타입(data type)은 숫자와 문자일 것이다. 이번 시간에는 실제로 가장 많이 사용되는 데이터 형인 문자와 숫자를 프로그래밍에서는 어떻게 표현하고 연산하는지 알아보자.

> 데이터 타입은 자료형(資料形) 또는 데이터형이라고도 한다.

</br>

## 숫자

자바에서는 따옴표가 없는 숫자는 숫자로 인식한다.

``` java
System.out.println(1+2);
```
결과 : 3

> 소수점이 없이 딱 떨어지는 숫자를 정수라고 한다.

</br>

``` java
System.out.println(1.2+1.3);
```
결과 : 2.5

> 소수점이 있는 숫자를 실수라고 한다.

</br>

곱하기를 할 때는 *(에스터리스크, Asterisk, 키보드 자판상으로 숫자 8 위)를 사용한다.
``` java
System.out.println(2*5);
```
결과 : 10

</br>

나누기를 할 때는 /(슬래쉬, slash, 키보드 자판상으로 오른쪽 shift 키 왼쪽)를 사용한다.
``` java
System.out.println(6/2);
```
결과 : 3

</br>

> **+,-,*,/ 같은 것들을 연산자라고 칭한다.**

</br>

## 문자와 문자열
자바는 문자(Character)와 문자열(String)을 구분한다. 문자는 한 글자를 의미하고, 문자열은 여러 개의 문자가 결합한 것을 의미한다. 자바에서 문자는 '(작은따옴표)로 감싸야 한다.
``` java
System.out.println('생');
```
문자열은 "(큰따옴표)로 감싸야 한다.
``` java
System.out.println("생활코딩");
```
만약 문자열을 작은 따옴표로 감싸면 에러가 발생한다.
``` java
System.out.println('생활코딩');
```
하나의 문자를 큰따옴표로 감싼다고 에러가 발생하지는 않는다. 한 글자도 문자열이 될 수 있기 때문이다.
``` java
System.out.println("생");
```
문자나 문자열도 + 같은 연산자를 사용하여, 더할 수가 있다.
``` java
System.out.println("생활코딩" + "입니다.");
```
결과 : 생활코딩입니다.

</br>

숫자도 큰 따옴표 안에 넣어주면 문자열로 인식하여 출력한다.
``` java
System.out.println("1" + "1");
```
결과 : 11

</br>

## 이스케이프
만약 문자열 안에 큰 따옴표를 넣고 싶다면 어떻게 해야 할까?
``` java
System.out.println("egoing said "Welcome programming world"");
```
```
Exception in thread "main" java.lang.Error: Unresolved compilation problems: 
    Syntax error, insert ")" to complete MethodInvocation
    Syntax error, insert ";" to complete BlockStatements
    Syntax error on token(s), misplaced construct(s)
    The method programming(String) is undefined for the type datatype
    Syntax error on token "world", ( expected
```
위와 같이 오류가 발생할 것이다.

이런 때는 아래와 같이 처리하면 된다.
``` java
System.out.println("egoing said \"Welcome programming world\"");
```
\를 " 앞에 위치시키면 " 를 문자열의 시작과 끝을 구분하는 구분자가 아니라 단순히 문자로 해석하도록 강제할 수 있다. 이러한 기법을 escape(이스케이프)라고 한다. 즉 큰따옴표가 가진 문법적인 역할에서 도망(escape)쳐서 문자로 인식하도록 한다는 의미다.

</br>

## 여러 줄의 표시
여러 줄을 표시하고 싶을 때는 아래와 같이 하면 된다.
``` java
System.out.println("HTML\nCSS\nJavaScript\n");
```
> \n은 줄바꿈으로 인식한다.

</br>

## 문자의 연산
문자와 문자를 더할 때는 아래와 같이 한다.
``` java
System.out.println("생활"+"코딩");
```
결과 : 생활코딩