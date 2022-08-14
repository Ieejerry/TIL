Chapter 2. 변수

# 2. 변수의 타입

우리가 주로 사용하는 깂(data)의 종류(type)는 크게 '문자와 숫자'로 나눌 수 있으며, 숫자는 다시 '정수와 실수'로 나눌 수 있다.

![image](https://ifh.cc/g/mZSBro.png)

이러한 값(data)의 종류(type)에 따라 값이 저장될 공간의 크기와 저장형식을 정의한 것이 자료형(data type)이다. 자료형에는 문자형(char), 정수형(byte, short, int, long), 실수형(float, double) 등이 있으며, 변수를 선언할 때는 저장하려는 값의 특성을 고려하여 가장 알맞은 자료형을 변수의 타입으로 선택하면 된다.

### 기본형과 참조형

자료형은 크게 '기본형'과 '참조형' 두 가지로 나눌 수 있는데, **기본형 변수는 실제 값(data)을 저장**하는 반면, **참조형 변수**는 어떤 값이 저장되어 있는 **주소(memory address)를 값으로 갖는다.** 자바는 C언어와 달리 참조형 변수 간의 연산을 할 수 없으므로 실제 연산에 사용되는 것은 모두 기본형 변수이다.

> 메모리에는 1 byte 단위로 일련번호가 붙어있는데, 이 번호를 '메모리 주소(memory address)' 또는 간단히 '주소'라고 한다. 객체의 주소는 객체가 저장된 메로리 주소를 뜻한다.

> **기본형(primiitive type)**   
\- 논리형(boolean), 문자형(char), 정수형(byte, short, int, long), 실수형(float, double) 계산을 위한 실제 값을 저장한다. 모두 8개   
**참조형(reference type)**   
\- 객체의 주소를 저장한다. 8개의 기본형을 제외한 나머지 타입

참조형 변수(또는 참조변수)를 선언할 때는 변수의 타입으로 클래스의 이름을 사용하므로 클래싀 이름이 참조변수의 타입이 된다.

다음은 참조변수를 선언하는 방법이다. 기본형 변수와 같이 변수이름 앞에 타입을 적어 주는데 참조변수의 타입은 클래스의 이름이다.

> **클래스이름 변수이름;    // 변수의 타입이 기본형이 아닌 것들은 모두 참조변수이다.**

다음은 `Date`클래스 타입의 참조변수 `today`를 선언한 것이다. 참조변수는 `null` 또는 객체의 주소를 값으로 갖으며 참조변수의 초기화는 다음과 같이 한다.

``` java
Date today = new Date();    // Date객체를 생성해서, 그 주소를 today에 저장
```

객체를 생성하는 연산자 `new`의 결과는 생성된 객체의 주소이다. 이 주소가 대입연산자 `'='`에 의해서 참조변수 `today`를 통해서 생성된 객체를 사용할 수 있게 된다.

> 참조형 변수는 `null` 또는 객체의 주소(4 byte, 0x0~0xFFFFFFFF)를 값으로 갖는다. `null`은 어떤 객체의 주소도 저장되지 않음을 뜻한다. 단, JVM이 32 bit가 아니라 64 bit라면 참조형 변수의 크기는 8 byte가 된다.

</br>

## 2.1 기본형(primitive type)

기본형에는 모두 8개의 타입(자료형)이 있으며, 크게 논리형, 문자형, 정수형, 실수형으로 구분된다.

![image](https://ifh.cc/g/rPXfpO.png)

문자형인 `char`는 문자를 내부적으로 정수(유니코드)로 저장하기 때문에 정수형과 별반 다르지 않으며, 정수형 또는 실수형과 연산도 가능하다. 반면에 `boolean`은 다른 기본형과의 연산이 불가능하다. 즉, `boolean`을 제외한 나머지 7개의 기본형은 서로 연산과 변환이 가능하다.

정수는 가장 많이 사용되므로 타입을 4가지나 제공한다.

일반적으로 `int`를 많이 사용한다. 왜냐하면, `int`는 CPU가 가장 효율적으로 처리할 수 있는 타입이기 때문이다. 효율적인 실행보다 메모리를 절약하려면, `byte`나 `short`을 선택하면 된다.

> 4개의 정수형(byte, short, int, long)주엥서 int형이 기본 자료형(default data type)이며, 실수형(float, double)중에서는 double이 기본 자료형이다.

![image](https://ifh.cc/g/dlBdRV.png)

- `boolean`은 `true`와 `false` 두 가지 값만 표현할 수 있으면 되므로 가장 작은 크기인 1 byte.
- `char`는 자바에서 유니코드(2 byte 문자체계)를 사용하므로 2 byte.
- `byte`는 크기가 1 byte라서 `byte`
- `int`(4 byte)를 기준으로 짧아서 `short`(2 byte), 길어서 `long`(8 byte), (short <=> long)
- `float`는 실수값을 부동소수점(floating-point)방식으로 저장하기 때문에 `float`
- `double`은 `float`보다 두 배의 크기(8 byte)를 갖기 때문에 `double`

![image](https://ifh.cc/g/hKww2N.png)

> float과 double은 양의 범위만 적은 것이다. 음의 번위는 양의 범위에 음수 부호(-)를 붙이면 된다.

정수형(`byte`, `short`, `int`, `long`)의 경우 '−2^n~2^n−1'(n은 비트 수)

실수형은 정수형과 저장형식이 달라서 같은 크기라도 훨씬 큰 값을 표현할 수 있으나 오차가 발생할 수 있다는 단점이 있다. 그래서 정밀도(precision)가 중요한데, 정밀도가 높을수록 발생할 수 있는 오차의 범위가 줄어든다. 아래의 표를 보면 `float`의 정밀도는 7자리인데, 이것은 10진수로 7자리의 수를 오차없이 저장할 수 있다는 뜻이다.

![image](https://ifh.cc/g/tGWtNq.png)

</br>

## 2.2 상수와 리터럴

'상수(constant)'는 변수와 마찬가지로 '값을 저장할 수 있는 공간'이지만, 벼누소아 달리 한 번 값을 저장하면 다른 값으로 변경할 수 없다. 상수를 선언하는 방법은 변수와 동일하며, 단지 변수의 타입 앞에 키워드 `'final'`을 붙여주기만 하면 된다.

``` java
final int MAX_SPEED = 10;   // 상수 MAX_SPEED를 선언 & 초기화
```

그리고 상수는 반드시 사용하기 전에 초기화해야 하며, 그 후 부터는 상수의 값을 변경하는 것이 허용되지 않는다.

``` java
final int MAX_SPEED;    // OK,  선언
MAX_SPEED = 100;    // OK, 초기화
final int MAX_VALUE = 100;  // OK, 선언과 동시에 초기화
MAX_VALUE = 200;    // 에러, 상수의 값은 변경할 수 없음
```

### 리터럴

원래 12, 123, 3.14, 'A'와 같은 값들이 '상수'인데, 프로그래밍에서는 상수를 '값을 한 번 저장하면 변경할 수 없는 저장공간'으로 정의하였기 때문에 이와 구분하기 위해서 상수를 다른 이름으로 불러야만 했다. 그래서 상수 대신 리터럴이라는 용어를 사용한다. 많은 사람들이 리터럴이라는 용어를 어려워하는데, 리터럴은 단지 우리가 기존에 알고 있던 '상수'의 다른 이름일 뿐이다.

> **변수(variable)**    하나의 값을 저장하기 위한 공간   
**상수(constant)**  값을 한 번만 저장할 수 있는 공간   
**리터럴(literal)** 그 자체로 값을 의미하는 것

![image](https://ifh.cc/g/hFaDS6.png)

### 상수가 필요한 이유

``` java
int triangleArea = (20 * 10) / 2;   // 삼격형의 면적을 구하는 공식
int rectangleArea = 20 * 10;    // 사각형의 면적을 구하는 공식
```

위의 코드는 삼각형과 사각형의 면적을 구해서 변수에 저장한다.

`20`과 `10`이 아닌 다른 값을 이용해서 결과를 얻고 싶다면 여러 곳을 수정해야 한다.

``` java
final int WIDTH = 20;   // 폭
final int HEIGHT = 10;  // 높이

int triangleArea = (WIDTH * HEIGHT) / 2;    // 삼각형의 면적을 구하는 공식
int rectangleArea = WIDTH * HEIGHT;    // 사각형의 면적을 구하는 공식
```

이전 코드에 비해 면적을 구하는 공식의 의미가 명확해졌다. 그리고 다른 값으로 계산할 때도 여러 곳을 수정할 필요없이 상수의 초기화만 다른 값으로 해주면 된다.

### 리터럴의 타입과 접미사

변수에 타입이 있는 것처럼 리터럴에도 타입이 있다. 변수의 타입은 저장될 '값의 타입(리터럴의 타입)'에 의해 결정되므로, 만일 리터럴에 타입이 없다면 변수의 타입도 필요없을 것이다.

![image](https://ifh.cc/g/Xn3TPb.png)

정수형과 실수형에는 여러 타입이 존재하므로, 리터럴에 접미사를 붙여서 타입을 구분한다. 정수형의 경우, `long`타입의 리터럴에 접미사 'l' 또는 'L'를 붙이고, 접미사가 없으면 `int`타입의 리터럴이다. `byte`와 `short`타입의 리터럴은 별도로 존재하지 않으며 `byte`와 `short`타입의 변수에 값을 저장할 때는 `int`타입의 리터럴을 사용한다.

10진수 이외에도 2, 8, 16진수로 표현된 리터럴을 변수에 저장할 수 있으며, 16진수라는 것을 표시하기 위해 리터럴 앞에 접두사 '0x' 또는 '0X'를, 8진수의 경우에는 '0'을 붙인다.

> 접두사 '0x', '0X', '0b', '0B', '0'은 알파벳이 아니라 숫자이다. 2진 리터럴은 JDK 1.7부터 추가되었다.

``` java
int octNum = 010;   // 8진수 10, 10진수로 8
int hexNum = 0x10;  // 16진수 10, 10진수로 16
int binNum = 0b10;  // 2진수 10, 10진수로 2
```

그리고 JDK 1.7부터 정수형 리터럴의 중간에 구분자 '_'를 넣을 수 있게 되어서 큰 숫자를 편하게 읽을 수 있게 되었다.

``` java
long big = 100_000_000_000L;    // long big = 100000000000L;
long hex = 0xFFFF_FFFF_FFFF_FFFFL;  // long hex = 0xFFFFFFFFFFFFFFFFL;
```

``` java
float pi = 3.14f;   // 접미사 f 대신 F를 사용해도 된다.
double rate = 1.618d;   // 접미사 d 대신 D를 사용해도 된다.
```

실수형 리터럴에는 접미사를 붙여서 타입을 구분하며, `float`타입 리터럴에는 'f'를, `double`타입 리터럴에는 'd'를 붙인다. 정수형에서는 `int`가 기본 자료형인 것처럼 실수형에서는 `double`이 기본 자료형이라서 접미사 'd'는 생략이 가능하다. 실수형 리터럴인데, 접미사가 없으면 `double`타입 리터럴인 것이다.

``` java
float pi = 3.14;    // 에러, float타입 변수에 double타입 리터럴 저장불가
double rate = 1.618;    // OK, 접미사 d는 생략할 수 있다.
```

위의 문장에서 `3.14`는 접미사가 붙지 않았으므로 `float`타입 리터럴이 아니라 `double`타입 리터럴로 간주된다. 그래서 `3.14`가 `float`타입의 범위에 속한 값임에도 불구하고 컴파일 시에 에러가 발생한다. 에러를 피하려면 `3.14f`와 같이 접미사를 붙여야 한다.

리터럴의 접두사와 접미사는 대소문자를 구별하지 않으므로, 대문자와 소문자 중에서 어떤 것을 사용해도 상관없지만, 소문자 'l'의 경우 숫자 '1'과 헷갈리기 쉬우므로 대문자인 'L'를 사용하는 것이 좋다.

> 리터럴에 접미사가 붙는 타입은 long, float, double뿐인데, double은 생략가능하므로 long과 float의 리터럴에 접미사를 붙이는 것만 신경쓰면 된다.

리터럴에 소수점이나 10의 제곱을 나타내는 기호 E 또는 e, 그리고 접미사 f, F, d, D를 포함하고 이으면 실수형 리터럴로 간주된다.

![image](https://ifh.cc/g/yNXSZ7.png)

참고로 잘 쓰이진 않지만, 기호 p를 이용해서 실수 리터럴을 16진 지수형태로 표현할 수도 있다. p는 2의 제곱을 의미하며, p의 왼쪽에는 16진수를 적고, 오른쪽에는 지수를 10진 정수로 적는다. p는 대소문자 모두 가능하며, p가 퐇ㅁ된 리터럴은 실수형이다.

![image](https://ifh.cc/g/qd3Oqh.png)

### 타입의 불일치

리터럴의 타입은 저장될 변수의 타입과 일치하는 것이 보통이지만, 타입이 달라도 저장범위가 젋은 타입에 좁은 타입의 값을 저장하는 것은 허용된다.

``` java
int i = 'A';    // OK, 문자 'A'의 유니코드인 65가 변수 i에 저장된다.
long l = 123;   // OK, int보다 long타입이 더 범위가 넓다.
double d = 3.14f;   // OK, float보다 double타입이 더 범위가 넓다.
```

그러나 리터럴의 값이 변수의 타입의 범위를 넘어서거나, 리터럴의 타입이 변수의 타입보다 저장범위가 넓으면 컴파일 에러가 발생한다.

``` java
int i = 0x123456789;    // 에러, int타입의 범위를 넘는 값을 저장
float f = 3.14; // 에러, float타입보다 double타입의 범위가 넓다.
```

`3.14`는 `3.14d`에서 접미사가 생략된 것으로 `double`타입이다. 이 값을 `float`타입으로 표현할 수 있지만, `double`타입의 리터럴이므로 `float`타입의 변수에 저장할 수는 없다.

`byte`와 `short`타입의 리터럴은 따로 존재하지 않으므로 `int`타입의 리터럴을 사용한다. 단, `short`타입의 변수가 저장할 수 있는 범위에 속한 것이어야 한다.

``` java
byte b = 65;    // OK, byte타입에 저장 가능한 범위의 int타입 리터럴
short s = 0x1234;   // OK, short타입에 저장 가능한 범위의 int타입 리터럴
```

### 문자 리터럴과 문자열 리터럴

`'A'`와 같이 작은 따옴표로 문자 하나를 감싼 것을 '문자 리터럴'이라고 한다. 두 문자 이상은 큰 따옴표로 감싸야 하며 '문자열 리터럴'이라고 한다.

> 문자열은 '문자의 연속된 나열'이라는 뜻이며, 영어로 'string'이라고 한다.

``` java
char ch = 'J';  // char ch = 'Java'; 이렇게 할 수 없다.
String name = "Java";   // 변수 name에 문자열 리터럴 "Java"를 저장
```

`char`타입의 변수는 단 하나의 문자만 저장할 수 있으므로, 여러 문자(문자열)를 저장하기 위해서는 `String`타입을 사용해야 한다.

문자열 리터럴은 ""안에 아무런 문자도 넣지 않는 것을 허용하며, 이를 빈 문자열(empty string)이라고 한다. 그러나 문자 리터럴은 반드시 ''안에 하나의 문자가 있어야 한다.

``` java
String str = "";    // OK, 내용이 없는 빈 문자열
char ch = '';   // 에러, ''안에 반드시 하나의 문자가 필요
char ch = ' ';  // OK, 공백 문자(blank)로 변수 ch를 초기하
```

원래 `String`은 클래스이므로 아래와 같이 객체를 생성하는 연산자 `new`를 사용해야 하지만 특별히 위와 같은 표현도 허용한다.

``` java
String name = new String("Java");   // String 객체를 생성
```

그리고 결합 연산자(덧셈 연산자, +)를 이용하여 문자열을 결합할 수 있어서 다음과 같이 할 수 있다.

``` java
String name = "Ja" + "va";  // name은 "Java"
String str = name + 8.0;    // str은 "Java8.0"
```

결합 연산자(덧셈 연산자, +)는 피연산자가 모두 숫자일 때는 두 수를 더하지만, 피연산자 중 어느 한 쪽이 `String`이면 나머지 한 쪽을 먼저 `String`으로 변환한 다음 두 `String`을 결합한다.

> 문자열 + **any type** => 문자열 + **문자열** => 문자열   
**any type** + 문자열 => **문자열** + 문자열 => 문자열

덧셈 연산자는 왼쪽에서 오른쪽의 반향으로 연산을 수행하기 때문에 결합순서에 따라 결과가 달라진다는 것을 주의해야 한다.

예제 2-3 / ch2 / StringEx.java
``` java
public class StringEx {

	public static void main(String[] args) {
		String name = "Ja" + "va";
		String str = name + 8.0;
		
		System.out.println(name);
		System.out.println(str);
		System.out.println(7 + " ");
		System.out.println(" " + 7);
		System.out.println(7 + "");
		System.out.println("" + 7);
		System.out.println("" + "");
		System.out.println(7 + 7 + "");
		System.out.println("" + 7 + 7);
	}

}
```

```
Java
Java8.0
7 
 7
7
7

14
77
```

</br>

## 2.3 형상화된 출력 - printf()

같은 값이라도 다른 형식으로 출력하고 싶을 때가 있다. 예를 들면, 소수점 둘째자리까지만 출력한다던가, 정수를 16진수나 8진수로 출력한다던가, 이럴 때 `printf()`를 사용하면 된다.

`printf()`는 '지시자(specifier)'를 통해 변수의 값을 여러 가지 형식으로 변환하여 출력하는 기능을 가지고 있다. '지시자'는 값을 어떻게 출력할 것인지를 지정해주는 역할을 한다. 정수형 변수에 저장된 값을 10진 정수로 출력할 때는 지시자 `'%d'`를 사용하며, 변수의 값을 지정된 형식으로 변환해서 지시자대신 넣는다. 예를 들어 `int`타입의 변수 `age`의 값이 14일 때, `printf()`는 지시자 `'%d'` 대신 14를 넣어서 출력한다.

``` java
    System.out.printf("age:%d", age);
=>  System.out.printf("age:%d", 14);
=>  System.out.printf("age:14");    // "age:14"가 화면에 출력된다
```

만일 출력하려는 값이 2개라면, 지시자도 2개를 사용해야하며 출력될 값과 지시자의 순서는 일치해야 한다. 물론 3개 이상의 값도 지시자를 지정해서 출력할 수 있으며 개수의 제한은 없다.

``` java
    System.out.printf("age:%d year:%d", age, year);
=>  System.out.printf("age:%d year:%d", 14, 2017);
=>  System.out.printf("age:14 year:2017";
    // "age:14 year:2017"이 화면에 출력된다.
```

`println()`과 달리 `printf()`는 출력 후 줄바꿈을 하지 않는다. 줄바꿈을 하려면 지시자 `'%n'`을 따로 넣어줘야 한다.

> '%n' 대신 '\n'을 사용해도 되지만, OS마다 줄바꿈 문자가 다를 수 있기 때문에 '%n'을 사용하는 것이 더 안전하다.

``` java
System.out.printf("age:%d", age);   // 출력 후 줄바꿈을 하지 않는다.
System.out.printf("age:%d%n", age); // 출력 후 줄바꿈을 한다.
```

`printf()`의 지시자 중에서 자주 사용되는 것만 뽑아보면 다음과 같다.

![image](https://ifh.cc/g/kwCL3Q.png)

예제 2-4 / ch2 / PrintfEx1.java
``` java
public class PrintfEx1 {

	public static void main(String[] args) {
		byte b = 1;
		short s = 2;
		char c = 'A';
		
		int finger = 10;
		long big = 100_000_000_000L;	// long big = 100000000000L;
		long hex = 0xFFFF_FFFF_FFFF_FFFFL;  // long hex = 0xFFFFFFFFFFFFFFFFL;
		
		int octNum = 010;   // 8진수 10, 10진수로 8
		int hexNum = 0x10;  // 16진수 10, 10진수로 16
		int binNum = 0b10;  // 2진수 10, 10진수로 2
		
		System.out.printf("b=%d%n", b);
		System.out.printf("s=%d%n", s);
		System.out.printf("c=%c, %d, %n", c, (int)c);
		System.out.printf("finger=[%5d]%n", finger);
		System.out.printf("finger=[%-5d]%n", finger);
		System.out.printf("finger=[%05d]%n", finger);
		System.out.printf("big=%d%n", big);
		System.out.printf("hex=%#x%n", hex);	// '#'은 접두사(16진수, 0x, 8진수 0)
		System.out.printf("octNum=%o, %d%n", octNum, octNum);
		System.out.printf("hexNum=%x, %d%n", hexNum, hexNum);
		System.out.printf("binNum=%s, %d%n", Integer.toBinaryString(binNum), binNum);
	}

}
```

```
b=1
s=2
c=A, 65, 
finger=[   10]
finger=[10   ]
finger=[00010]
big=100000000000
hex=0xffffffffffffffff
octNum=10, 8
hexNum=10, 16
binNum=10, 2
```

아래의 결과를 보면, '0'은 공백을 0으로 채워주고, '-'는 왼쪽 정렬을 해주는 역할을 한다는 것을 알 수 있다.

``` java
System.out.printf("finger=[%5d]%n", finger);    // finger=[   10]
System.out.printf("finger=[%-5d]%n", finger);   // finger=[10   ]
System.out.printf("finger=[%05d]%n", finger);   // finger=[00010]
```

지시자 `%x`와 `%o`에 `#`를 사용하면 접두사 `0x`와 `0`이 각각 붙는다. 그리고 `%X`는 16진수에 사용되는 접두사와 영문자를 대문자로 출력한다.

``` java
System.out.printf("hex=%x%n", hex); // hex=ffffffffffffffff
System.out.printf("hex=%#x%n", hex);    // hex=0xffffffffffffffff
System.out.printf("hex=%#X%n", hex);    // hex=0XFFFFFFFFFFFFFFFF
```

10진수를 2진수로 출력해주는 지시자는 없기 때문에, 정수를 2진 문자열로 변환해주는 `Integer.toBinaryString(int i)`를 사용해야 한다. 이 메소드는 정수를 2진수로 변환해서 문자열로 반환하므로 지시자 `%s`를 사용해야 한다.

``` java
System.out.printf("binNum=%s%n", Integer.toBinaryString(binNum));
```

그리고 C언어에서는 `char`타입의 값을 지사자 `%d`로 출력할 수 있지만, 자바에서는 허용이 되지 않는다. 아래와 같이 `int`타입으로 형변환해야만 `%d`로 출력할 수 있다.

``` java
System.out.printf("c=%c, %d, %n", c, (int)c);   // 형변환이 꼭 필요하다.
```

예제 2-5 / ch2 / PrintfEx2.java
``` java
public class PrintfEx2 {

	public static void main(String[] args) {
		String url = "www.codechobo.com";
		
		float f1 = .10f;	// 0.10, 1.0e-1
		float f2 = 1e1f;	// 10.0, 1.0e1, 1.0e + 1
		float f3 = 3.15e3f;
		double d = 1.23456789;
		
		System.out.printf("f1=%f, %e, %g%n", f1, f1, f1);
		System.out.printf("f2=%f, %e, %g%n", f2, f2, f2);
		System.out.printf("f3=%f, %e, %g%n", f3, f3, f3);
		
		System.out.printf("d=%f%n", d);
		System.out.printf("d=%14.10f%n", d);	// 전체 15자리 중 소수점 10자리
		
		System.out.printf("[1234567890123456789]%n");
		System.out.printf("[%s]%n", url);
		System.out.printf("[%20s]%n", url);
		System.out.printf("[%-20s]%n", url);	// 왼쪽 정렬
		System.out.printf("[%.8s]%n", url);		// 왼쪽에서 8글자만 출력
	}

}
```

```
f1=0.100000, 1.000000e-01, 0.100000
f2=10.000000, 1.000000e+01, 10.0000
f3=3150.000000, 3.150000e+03, 3150.00
d=1.234568
d=  1.2345678900
[1234567890123456789]
[www.codechobo.com]
[   www.codechobo.com]
[www.codechobo.com   ]
[www.code]
```

실수형 값의 출력에 사용되는 지시자는 `%f`, `%e`, `%g`가 있는데, `%f`가 주로 쓰이고 `%e`는 지수형태로 출력할 때, `%g`는 값을 간략하게 표현할 때 사용한다.

`%f`는 기본적으로 소수점 아래 6자리까지만 출력하기 때문에 소수점 아래 7자리에서 반올림한다.

지시자 `%s`에도 숫자를 추가하면 원하는 만큼의 출력공간을 확보하거나 문자열의 일부만 출력할 수 있다.

``` java
System.out.printf("[%s]%n", url);   // 문자열의 길이만큼 출력공간을 확보
System.out.printf("[%20s]%n", url); // 최소 20글자 출력공간 확보, (우측 정렬)
System.out.printf("[%-20s]%n", url);    // // 최소 20글자 출력공간 확보, (좌측 정렬)
System.out.printf("[%.8s]%n", url); // 왼쪽에서 8글자만 출력
```

지정된 숫자보다 문자열의 길이가 적으면 빈자리는 공백으로 출력된다. 공백이 없는 경우 기본적으로 우측 끝에 문자열을 붙이지만, '-'를 붙이면 좌측 끝에 붙인다. 그리고 '.'을 붙이면 문자열의 일부만 출력할 수 있다.

</br>

## 2.4 화면에서 입력받기 - Scanner

`Scanner`클래스를 사용하려면 아래의 한 문장을 추가해야 한다.

``` java
import java.util.*; // Scanner 클래스를 사용하기 위해 추가
```

그 다음엔 `Scanner`클래스의 객체를 생성한다.

``` java
Scanner scanner = new Scanner(System.in);   // Scanner 클래스의 객체를 생성
```

그리고 `nextLine()`이라는 메소드를 호출하면, 입력대기 상태에 있다가 입력을 마치고 '엔터키(Enter)'를 누르면 입력한 내용이 문자열로 반환된다.

``` java
String input = scanner.nextLine();  // 입력받은 내용을 input에 저장
int num = Integer.parseInt(input);  // 입력받은 내용을 int타입의 값은 변환
```

만일 입력받은 문자열을 숫자로 변환하려면, `Integer.parseInt()`라는 메소드를 이용해야 한다. 이 메소드는 문자열을 `int`타입의 정수로 변환하다.

> 만일 문자열을 float타입의 값으로 변환하길 원하면, Float.parseFloat()를 사용해야 한다.

`Scanner`클래스에는 `nextLine()`나 `nextFloat()`와 같이 변환없이 숫자로 바로 입력받을 수 있는 메소드들이 있고, 이 메소드들을 사용하면 문자열을 숫자로 변환하는 수고는 하지 않아도 된다.

``` java
int num = scanner.nextInt();    // 정수를 입력받아서 변수 num에 저장
```

그러나 이 메소드들은 화면에서 연속적으로 값을 입력받아서 사용하기에 까다롭다.

예제 2-6 / ch2 / ScannerEx.java
``` java
import java.util.Scanner;

public class ScannerEx {

	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
		
		System.out.print("두자리 정수를 하나 입력해주세요.>");
		String input = scanner.nextLine();
		int num = Integer.parseInt(input);	// 입력받은 문자열을 수샂로 변환
		
		System.out.println("입력내용 :" + input);
		System.out.printf("num=%d%n", num);
	}

}
```

```
두자리 정수를 하나 입력해주세요.>22
입력내용 :22
num=22
```