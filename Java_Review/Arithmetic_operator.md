Chapter 3. 연산자

# 3. 산술 연산자

산술 연산자에는 사칙 연산자(+, -, *, /)와 나머지 연산자(%)가 있다.

</br>

## 3.1 사칙 연산자 + - * /

사칙 연산자, 덧셈(\+), 뺄셈(\-), 곱셈(\*), 나눗셈(\/)은 프로그래밍에 가장 많이 사용되는 연산자들이다. 곱셈(\*), 나눗셈(\/), 나머지(\%) 연산자가 덧셈(\+), 뺄셈(\-)연산자보다 우선순위가 높으므로 먼저 처리된다.

그리고 피연산자가 정수형인 경우, 나누는 수로 0을 사용할 수 없다. 만일 0으로 나눈다면, 실행 시에 에러가 발생할 것이다.

예제 3-5 / ch3 / OperatorEx5.java
``` java
public class OperatorEx5 {

	public static void main(String[] args) {
		int a = 10;
		int b = 4;
		
		System.out.printf("%d + %d = %d%n", a, b, a + b);
		System.out.printf("%d - %d = %d%n", a, b, a - b);
		System.out.printf("%d * %d = %d%n", a, b, a * b);
		System.out.printf("%d / %d = %d%n", a, b, a / b);
		System.out.printf("%d / %f = %f%n", a, (float)b, a + (float)b);
	}

}
```

```
10 + 4 = 14
10 - 4 = 6
10 * 4 = 40
10 / 4 = 2
10 / 4.000000 = 14.000000
```

두 변수 `a`와 `b`에 각각 10과 5를 저장하여 사칙연산을 수행하고 그 결과를 출력하는 예제이다. 한 가지 눈여겨볼 것은 10을 4로 나눈 결과가 2.5가 아닌 2라는 것이다.

``` java
int   int   int
10  /  4  →  2  // 소수점 이하는 버려진다.
```

나누기 연산자의 두 피연산자가 모두 `int`타입인 경우, 연산결과 역시 `int`타입이다. 그래서 실제 연산결과는 2.5일지라도 `int`타입의 값인 2를 결과로 얻는다. `int`타입은 소수점을 저장하지 못하므로 정수만 남고 소수점 이하는 버려지기 때문이다. 이 때, 반올림이 발생하지 않는다.

그래서 올바른 연산결과를 얻기 위해서는 두 피연산자 중 어느 한 쪽을 실수형으로 형변환해야 한다. 그래야만 다른 한 쪽도 같이 실수형으로 자동 형변환되어 결국 실수형의 값을 결과로 얻는다.

``` java
int    float       float     float      float
10  /  4.0f   →    10.0f  /  4.0f   →   2.5f
```

위의 연산과정을 보면, 두 피연산자의 타입이 일치하지 않으므로 `int`타입보다 범위가 넓은 `float`타입으로 일치시킨 후에 연산을 수행하는 것을 알 수 있다. 이제 `float`타입과 `float`타입의 연산이므로 연산결과 역시 `float`타입이다.

``` java
System.out.println(3 / 0);	// 실행하면, 오류(ArithmeticException) 발생
System.out.println(3 / 0.0);	// Infinity가 출력됨
```

그리고 피연산자가 정수형인 경우, 나누는 수로 0을 사용할 수 없다. 만일 0으로 나누면, 컴파일은 정상적으로 되지만 실행 시 오류(`ArithmeticException`)가 발생한다.

부동 소수점값이 `0.0f`, `0.0d`로 나누는 것은 가능하지만 그 결과는 Infinity(무한대)이다. 나눗셈 연산자 `/`와 나머지 연산자 `%`의 피연산자가 무한대(Infinity) 또는 0.0인 경우의 결과를 표로 정리하였다.

> NaN은 'Not a Number'를 줄인 것으로, 숫자가 아니라는 뜻이다.

![image](https://ifh.cc/g/pasKz3.png)

예제 3-6 / ch3 / OperatorEx6.java
``` java
public class OperatorEx6 {

	public static void main(String[] args) {
		byte a = 10;
		byte b = 20;
		byte c = a + b;	// 명시적으로 형변환이 필요하다.
		System.out.println(c);
	}

}
```

```java
Exception in thread "main" java.lang.Error: Unresolved compilation problem: 
	Type mismatch: cannot convert from int to byte

	at OperatorEx6.main(OperatorEx6.java:7)
```

이 예제를 컴파일하면 위와 같은 에러가 발생한다. 발생한 위치는 5번째 줄이다. `a`와 `b`는 모두 `int`형보다 작은 `byte`형이기 때문에 연산자 `+`는 이 두 개의 피연산자들의 자료형을 `int`형으로 변환한 다음 연산(덧셈)을 수행한다.

그래서 `a + b`의 연산결과는 `byte`형이 아닌 `int`형(4 byte)인 것이다. 4 byte의 값을 1 byte의 변수에 형변환없이 저장하려고 했기 때문에 에러가 발생하는 것이다.

예제 3-7 / ch3 / OperatorEx7.java
``` java
public class OperatorEx7 {

	public static void main(String[] args) {
		byte a = 10;
		byte b = 30;
		byte c = (byte)(a * b);
		System.out.println(c);
	}

}
```

```
44
```

이 예제를 실행하면 44가 화면에 출력된다. `10 * 30`의 결과는 300이지만, 큰 자료형에서 작은 자료형으로 변환하면 데이터의 손실이 발생하므로 값이 바뀔 수 있다. 300은 `byte`형의 범위를 넘기 때문에 `byte`형으로 변환하면 데이터 손실이 발생하여 결국 44가 `byte`형 변수 `c`에 저장된다.

예제 3-8 / ch3 / OperatorEx8.java
``` java
public class OperatorEx8 {

	public static void main(String[] args) {
		int a = 1_000_000;	// 1,000,000 1백만
		int b = 2_000_000;	// 2,000,000 2백만
		
		long c = a * b;	// a * b = 2,000,000,000,000 ?
		
		System.out.println(c);
	}

}
```

```
-1454759936
```

식 `a * b`의 결과 값을 담는 변수 `c`의 자료형이 `long`타입(8 byte)이기 때문에 2×10<sup>12</sup>을 저장하기에 충분하므로 '2000000000000'이 출력될 것 같지만, 결과는 전혀 다른 값이 출력된다.

그 이유는 `int`타입의 연산결과는 `int`타입이기 때문이다. `a * b`의 결과가 이미 `int`타입의 값(-1454759936)이므로 `long`형으로 자동 형변환 되어도 값은 변하지 않는다.

``` java
	long c = a * b;
→	long c = 1000000 * 2000000;
→	long c = -1454759936;
```

올바른 결과를 얻으려면 아래와 같이 변수 `a`또는 `b`의 타입을 `long`으로 형변환해야 한다.

``` java
	long c = (long)a * b;
→	long c = (long)1000000 * 2000000;
→	long c = 1000000L * 2000000;
→	long c = 1000000L * 2000000L;
→	long c = 2000000000000L;
```

예제 3-9 / ch3 / OperatorEx9.java
``` java
public class OperatorEx9 {

	public static void main(String[] args) {
		long a = 1_000_000 * 1_000_000;
		long b = 1_000_000 * 1_000_000L;
		
		System.out.println("a = " + a);
		System.out.println("b = " + b);
	}

}
```

```
a = -727379968
b = 1000000000000
```

이 예제는 예제 3-8과 비슷한 내용의 예제인데, '1000000 * 1000000'의 결과가 10<sup>12</sup>임에도 불구하고, -727379968이라는 결과가 출력되었다. 그 이유는 `int`타입과 `int`타입의 연산결과는 `int`타입인데, 연산겨로가가 `int`타입의 최대값인 약 2×10<sup>9</sup>을 넘으므로 오버플로우(overflow)가 발생했기 때문이다. 이미 오버플로우가 발생한 값을 아무리 `long`타입의 변수에 저장을 해도 소용이 없다.

```
  int       int         int
1000000 * 1000000 → -727379968	오버플로우 발생

  int       long       long       long          long
1000000 * 1000000L → 1000000L * 1000000L → 1000000000000L
```

그러나 '1000000 * 1000000L'은 `int`타입과 `long`타입의 연산이기 때문에 그 결과가 `long`타입이다. `long`타입은 연산결과인 10<sup>12</sup>을 저장할 수 있는 타입이므로 올바른 결과를 얻을 수 있다.

예제 3-10 / ch3 / Operator10.java
``` java
public class OperatorEx10 {

	public static void main(String[] args) {
		int a = 1000000;
		
		int result1 = a * a / a;	// 1000000 * 1000000 / 1000000
		int result2 = a / a * a;	// 1000000 / 1000000 * 1000000
		
		System.out.printf("%d * %d / %d = %d%n", a, a, a, result1);
		System.out.printf("%d / %d * %d = %d%n", a, a, a, result2);		
	}

}
```

```
1000000 * 1000000 / 1000000 = -727
1000000 / 1000000 * 1000000 = 1000000
```

1,000,000에 1,000,000을 먼저 곱한 후에 나누는 것과 먼저 나눈 후 에 곱하는 것의 연산 결과가 다르다는 것을 알 수 있다. 먼저 곱하는 경우 `int`의 범위를 넘어서기 때문에 예상했던 것과 다른 결과가 나온다.

```
	1000000 * 1000000 / 1000000
→	-727379968 / 1000000	오버플로우 발생
→	-727

	1000000 / 1000000 * 1000000
→	1 * 1000000
→	1000000
```

예제 3-11 / ch3 / OperatorEx11.java
``` java
public class OperatorEx11 {

	public static void main(String[] args) {
		char a = 'a';
		char d = 'd';
		char zero = '0';
		char two = '2';
		
		System.out.printf("'%c' - '%c' = %d%n", d, a, d - a);
		System.out.printf("'%c' - '%c' = %d%n", two, zero, two - zero);
		System.out.printf("'%c' = %d%n", a, (int)a);
		System.out.printf("'%c' = %d%n", d, (int)d);
		System.out.printf("'%c' = %d%n", zero, (int)zero);
		System.out.printf("'%c' = %d%n", two, (int)two);
	}

}
```

```
'd' - 'a' = 3
'2' - '0' = 2
'a' = 97
'd' = 100
'0' = 48
'2' = 50
```

문자는 실제로 해당 문자의 유니코드(부호없는 정수)로 바뀌어 저장되므로 문자간의 사칙연산은 정수간의 연산과 동일하다. 주로 문자간의 뺄셈을 하는 경우가 대부분이며, 문자 '2'를 숫자로 변환하려면 다음과 같이 문자 '0'을 빼주면 된다.

```
'2' - '0' → 50 - 48 → 2
```

문자 '2'의 유니코드는 50이고, 문자 '0'은 48이므로, 두 문자간의 뺄셈은 2를 결과로 얻는다. 아래의 표는 유니코드의 일부분인데, '0'\~'9'까지의 문자가 연속적으로 배치되어 있는 것을 알 수 있다. 그렇기 때문에 해당 문자에서 '0'을 빼주면 숫자로 변환되는 것이다.

![image](https://ifh.cc/g/7Hqjc2.png)

'A'\~'Z'와 'a'\~'z' 역시 연속적으로 배치되어 있기 때문에, 문자 'd'에서 문자 'a'를 빼면 다음과 같이 처러된다.

```
'd' - 'a' → 100 - 97 → 3
```

예제 3-12 / ch3 / OperatorEx12.java
``` java
public class Operator12 {

	public static void main(String[] args) {
		char c1 = 'a';	// c1에는 문자 'a'의 코드값인 97이 저장된다.
		char c2 = c1;	// c1에 저장되어 있는 값이 c2에 저장된다.
		char c3 = ' ';	// c3를 공백으로 초기화 한다.
		
		int i = c1 + 1;	// 'a' + 1 → 97 + 1 →98
		
		c3 = (char)(c1 + 1);
		c2++;
		c2++;
		
		System.out.println("i = " + i);
		System.out.println("c2 = " + c2);
		System.out.println("c3 = " + c3);
	}

}
```

```
i = 98
c2 = c
c3 = b
```

`c1 + 1`을 계산할 때, `c1`이 `char`형이므로 `int`형으로 변환한 후 덧셈연산을 수행하게 된다 `c1`에 저장되어 있는 코드값이 변환되어 `int`형 값이 되는 것이다. 따라서 `c1 + 1`은 `97 + 1`이 되고 결과적으로 `int`형 변수 `i`에는 98이 저장된다.

`c2++`은 형변환 없이 `c2`에 저장되어 있는 값을 1 증가시키므로, 예제에서는 원래 저장되어 있던 값인 97이 1씩 두 번 증가되어 99가 된다. 코드값이 10진수로 99인 문자는 'c'이다. 따라서 `c2`를 출력하면 , 'c'가 화면에 나타나는 것이다.

> c2++; 대신에 c2 = c2 + 1;을 사용하면 에러가 발생한다. c2 + 1의 열산결과는 int형이며, 그 결과를 다시 c2에 담으려면 형변환 연산자를 사용하여 char형으로 형변환해야 하기 때문이다.

예제 3-13 / ch3 / OperatorEx13.java
``` java
public class OperatorEx13 {

	public static void main(String[] args) {
		char c1 = 'a';
		
//		char c2 = c1 + 1;	// 라인 7 : 컴파일 에러발생
		char c2 = 'a' + 1;	// 라인 8 : 컴파일 에러없음
		
		System.out.println(c2);
	}

}
```

```
b
```

상수 또는 리터럴 간의 연산은 실행과정동안 변하는 값이 아니기 때문에, 컴파일 시에 컴파일러가 계산해서 그 결과로 대체함으로써 코드를 보다 효율적으로 만든다.

그러나 라인 7와 같이 수식에 변수가 들어가 있는 경우에는 컴파일러가 미리 계산을 할 수 없기 때문에 컴파일 에러가 발생한다.

예제 3-14 / ch3 / OperatorEx14.java
``` java
public class OperatorEx14 {

	public static void main(String[] args) {
		char c = 'a';
		for (int i = 0; i < 26; i++) {	// 블럭{} 안의 문장을 26번 반복한다.
			System.out.print(c++);		// 'a'부터 26개의 문자를 출력한다.
		}
		System.out.println();
		
		c = 'A';
		for (int i = 0; i < 26; i++) {	// 블럭{} 안의 문장을 26번 반복한다.
			System.out.print(c++);		// 'A'부터 26개의 문자를 출력한다.
		}
		System.out.println();
		
		c = '0';
		for (int i = 0; i < 10; i++) {	// 블럭{} 안의 문장을 10번 반복한다.
			System.out.print(c++);		// '0'부터 10개의 문자를 출력한다.
		}
		System.out.println();
	}

}
```

```
abcdefghijklmnopqrstuvwxyz
ABCDEFGHIJKLMNOPQRSTUVWXYZ
0123456789
```

> println 메소드는 값을 출력하고 줄을 바꾸지만, print 메소드는 줄을 바꾸지 않고 출력한다. 매개변수 없이 println 메소드를 호출하면, 아무 것도 출력하지 않고 단순히 줄을 바꾸고 다음 줄의 처음으로 출력위치를 이동시킨다.

예제 3-15 / ch3 / OperatorEx15.java
``` java
public class OperatorEx15 {

	public static void main(String[] args) {
		char lowerCase = 'a';
		char upperCase = (char)(lowerCase - 32);
		System.out.println(upperCase);
	}

}
```

```
A
```

소문자를 대문자로 변경하려면, 대문자 A가 소문자 a보다 코드값이 32가 적으므로 소문자 a의 코득밧에서 32를 빼면 되고, 반대로 대문자를 소문자로 변환하려면 대문자의 코드값에 32를 더해주면 된다.

> char형과 int형 간의 뺄셈연산 결과는 int형이므로, 연산 후 char형으로 다시 형변환해야 한다.

예제 3-16 / ch3 / OperatorEx16.java
``` java
public class OperatorEx16 {

	public static void main(String[] args) {
		float pi = 3.141592f;
		float shortPi = (int)(pi * 1000) / 1000f;
		System.out.println(shortPi);
	}

}
```

```
3.141
```

`int`형 간의 나눗셈 `int / int`를 수행하면 결과가 `float`나 `double`이 아닌 `int`이다. 그리고 나눗셈의 결과를 반올림 하는 것이 아니라 버린다.

예제 3-17 / ch3 / OperatorEx17.java
``` java
public class OperatorEx17 {

	public static void main(String[] args) {
		double pi = 3.141592;
		double shortPi = (int)(pi * 1000 + 0.5) / 1000.0;
		
		System.out.println(shortPi);
	}

}
```

```
3.142
```

위의 수식에서 제일 먼저 수행되는 것은 괄호 안의 `pi * 1000`이다. `pi`가 `double`이고 	`1000`이 정수형이니까 연산의 결과는 `double`인 `3141.592`가 된다. 그리고 여기에 0.5를 더하면 `3142.092`가 된다.

```
	(int)(3141.592 + 0.5) / 1000.0
→	(int)(3142.092) / 1000.0
```

그 다음엔 형변환 연산자에 의해서 형변환되어 `3142.092`가 `3142`가 된다.

```
3142 / 1000.0
```

`int`와 `double`의 연산이므로, `int`가 `double`로 변환된 다음, `double`과 `double`의 연산이 수행된다.

```
3142.0 / 1000.0 → 3.142
```

`double`과 `double`의 나눗셈이므로 결과는 `double`인 `3.142`가 된다. 마일 `1000.0`이 아닌 1000으로 나누었다면, `3.142`가인 3을 결과로 얻었을 것이다.

예제 3-18 / ch3 / OperatorEx18.java
``` java
public class OperatorEx18 {

	public static void main(String[] args) {
		double pi = 3.141592;
		double shortPi = Math.round(pi * 1000) / 1000.0;
		System.out.println(shortPi);
	}

}
```

```
3.142
```

`round` 메소드는 매개변수로 받은 값을 소수점 첫째자리에서 반올림을 하고 그 결과를 정수로 돌려주는 메소드이다. 그래서 `Math.round(3141.592)`의 결과는 `3142`이다.

``` java
	Math.round(pi * 1000) / 1000.0
→	Math.round(3.141592 * 1000) / 1000.0
→	Math.round(3141.592) / 1000.0
→	3142 / 1000
→	3.142
```

</br>

## 3.2 나머지 연산자 %

나머지 연산자는 왼쪽의 피연산자를 오른쪽 피연산자로 나누고 난 나머지 값을 결과로 반환하는 연산자이다. 그리고 나눗셈에서처럼 나누는 수(오른쪽 피연산자)로 0을 사용할 수 없다. 나머지 연산자는 주로 짝수, 홀수 또는 배수 검사 등에 주로 사용된다.

예제 3-19 / ch3 / Operator19.java
``` java
public class OperatorEx19 {

	public static void main(String[] args) {
		int x = 10;
		int y = 8;
		
		System.out.printf("%d을 %d로 나누면, %n", x, y);
		System.out.printf("몫은 %d이고, 나머지는 %d입니다.%n", x / y, x % y);
	}

}
```

```
10을 8로 나누면, 
몫은 1이고, 나머지는 2입니다.
```

예제 3-20 / ch3 / Operator20.java
``` java
public class OperatorEx20 {

	public static void main(String[] args) {
		System.out.println(-10%8);
		System.out.println(10%-8);
		System.out.println(-10%-8);
	}

}
```

```
-2
2
-2
```

나머지 연산자(%)는 나누는 수로 음수도 허용한다. 그러나 부호는 무시되므로 결과는 음수의 절대값으로 나눈 나머지와 결과가 같다.