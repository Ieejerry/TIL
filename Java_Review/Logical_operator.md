Chapter 3. 연산자

# 5. 논리 연산자

논리 연산자는 둘 이상의 조건을 '그리고(AND)'나 '또는(OR)'으로 연결하여 하나의 식으로 표현할 수 있게 해준다.

</br>

## 5.1 논리 연산자 - &&, ||, !

논리 연산자 `&&`는 우리말로 '그리고(AND)'에 해당하며, 두 피연산자가 모두 `true`일 때만 `true`를 결과로 얻는다. `||`는 '또는(OR)'에 해당하며, 두 피연산자 중 어느 한 쪽만 `true`이어도 `true`를 결과로 얻는다. 그리고 논린 연산자는 피연산자로 `boolean`형 또는 `boolean`형 값을 결과로 하는 조건식만 허용한다.

> **||(OR)결합** 피연산자 중 어느 한 쪽만 true이면 true를 결과로 얻는다.   
**&&(AND결합)** 피연산자 양쪽 모두 true이어야 true를 결과로 얻는다.

![image](https://ifh.cc/g/66aPNz.png)

하나의 식에 `&&`와 `||`가 같이 포함된 경우, `&&`가 `||`보다 우선순위가 높기 때문에 `&&`가 먼저 연산이 되는데, 괄호를 사용해서 우선순위를 명확히 해주는 것이 좋다.

예제 3-24 / ch3 / OperatorEx24.java
``` java
public class OperatorEx24 {

	public static void main(String[] args) {
		int x = 0;
		char ch = ' ';
		
		x = 15;
		System.out.printf("x = %2d, 10 < x && x < 20 = %b%n", x, 10 < x && x <20);
		
		x = 6;
		System.out.printf("x = %2d, x%%2 == 0 || x %% 3 == 0 && x %% 6 != 0 = %b%n", x, x % 2 == 0 || x % 3 == 0 && x % 6 != 0);

		System.out.printf("x = %2d, (x%%2 == 0 || x %% 3 == 0) && x %% 6 != 0 = %b%n", x, (x % 2 == 0 || x % 3 == 0) && x % 6 != 0);
		
		ch = '1';
		System.out.printf("ch = '%c', '0' <= ch && ch <= '9' = %b%n", ch, '0' <= ch && ch <= '9');
		
		ch = 'a';
		System.out.printf("ch = '%c', 'a' <= ch && ch <= 'z' = %b%n", ch, 'a' <= ch && ch <= 'z');
		
		ch = 'A';
		System.out.printf("ch = '%c', 'A' <= ch && ch <= 'Z' = %b%n", ch, 'A' <= ch && ch <= 'Z');
		
		ch = 'q';
		System.out.printf("ch = '%c', ch == 'q' || ch == 'Q' = %b%n", ch, ch == 'q' || ch == 'Q');
	}

}
```

```
x = 15, 10 < x && x < 20 = true
x =  6, x%2 == 0 || x % 3 == 0 && x % 6 != 0 = true
x =  6, (x%2 == 0 || x % 3 == 0) && x % 6 != 0 = false
ch = '1', '0' <= ch && ch <= '9' = true
ch = 'a', 'a' <= ch && ch <= 'z' = true
ch = 'A', 'A' <= ch && ch <= 'Z' = true
ch = 'q', ch == 'q' || ch == 'Q' = true
```

예제 3-25 / ch3 / OperatorEx25.java
``` java
import java.util.Scanner;

public class OperatorEx25 {

	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
		char ch = ' ';
		
		System.out.printf("문자를 하나 입력하세요.>");
		
		String input = scanner.nextLine();
		ch = input.charAt(0);
		
		if ('0' <= ch && ch <= '9') {
			System.out.printf("입력하신 문자는 숫자입니다.%n");
		}
		
		if (('a' <= ch && ch <= 'z') || ('A' <= ch && ch <= 'Z')) {
			System.out.printf("입력하신 문자는 영문자입니다.%n");
		}
	}	// main

}
```

```
문자를 하나 입력하세요.>7
입력하신 문자는 숫자입니다.
```

```
문자를 하나 입력하세요.>a
입력하신 문자는 영문자입니다.
```

이 예제는 사용자로부터 하나의 문자를 입력받아서 숫자인지 영문자인지 확인한다. 조건문 `if`는 괄호()안에 연산결과가 참인 경우 블럭{}내의 문장을 수행한다. 그래서 아래의 코드는 `'0' <= ch && ch <= '9'`가 참일 때, 화면에 '입력하신 문자는 숫자입니다.'라고 출력한다.

``` java
if ('0' <= ch && ch <= '9') {
    printf("입력하신 문자는 숫자입니다.%n");
}
```

### 효율적인 연산(short circuit evaluation)

논리 연산자의 또 다른 특징은 효율적인 연산을 한다는 것이다. OR연산 `||`의 경우, 두 피연산자 중 어느 한 쪽만 '참'이어도 전체 연산결과가 '참'이므로 좌측 피연산자가 'true(참)'이면, 우측 피연산자의 값은 평가하지 않는다.

![image](https://ifh.cc/g/bBS2KS.png)

AND연산 `&&`의 경우도 마찬가지로 어느 한 쪽만 '거짓(false)'이어도 전체 연산결과가 '거짓(false)'이므로 좌측 피연산자가 '거짓(false)'이면, 우측 피연산자는 평가하지 않는다.

![image](https://ifh.cc/g/FHKRRr.png)

그래서 같은 조건식이라도 피연산자의 위치에 따라서 연산속도가 달라질 수 있는 것이다. OR연산 `||`의 경우에는 연산결과가 '참'일 확률이 높은 피연산자를 연산자의 왼쪽에 놓아야 더 빠른 연산결과를 얻을 수 있다.

예제 3-26 / ch3 / OperatorEx26.java
``` java
public class OperatorEx26 {

	public static void main(String[] args) {
		int a = 5;
		int b = 0;
		
		System.out.printf("a = %d, b = %d%n", a, b);
		System.out.printf("a != 0 || ++b != 0 = %b%n", a != 0 || ++b != 0);
		System.out.printf("a = %d, b = %d%n", a, b);
		System.out.printf("a == 0 && ++b != 0 = %b%n", a == 0 && ++b != 0);
		System.out.printf("a = %d, b = %d%n", a, b);
	}

}
```

```
a = 5, b = 0
a != 0 || ++b != 0 = true
a = 5, b = 0
a == 0 && ++b != 0 = false
a = 5, b = 0
```

변수 `b`에 증감 연산자 `++`을 사용해서 우측 피연산자가 처리되면, `b`의 값이 증가하도록 했다.

그러나 실행겨롸에서 알 수 있듯이, 두 번의 논리연산 후에도 `b`의 값은 여전히 0인 채로 남이있다. '`||`(OR)'의 경우는 좌측 피연산자(a != 0)가 참이라서, 그리고 '`&&`(AND)'의 경우는 좌측 피연산자(a == 0)가 거짓이라서 우측 피연산자를 평가하지 않았기 때문이다.

### 논리 부정 연산자 !

이 연산자는 피연산자가 `true`이면 `false`를, `false`이면 `true`를 결과로 반환한다. 간단히 말해서, `true`와 `false`를 반대로 바꾸는 것이다.

![image](https://ifh.cc/g/cLwMZt.png)

어떤 값에 논리 부정 연산자 `!`를 반복적으로 적용하면, 참과 거짓이 차례대로 반복된다. 그래서 '토글 버튼(toggle button)'을 논리적으로 구현할 수 있다.

논리 부정 연산자 `!`가 주로 사용되는 곳은 조건문과 반복문의 조건식이며, 이 연산자를 잘 사용하면 조건식이 보다 이해하기 쉬워진다.

예제 3-27 / ch3 / OperatorEx27.java
``` java
public class OperatorEx27 {

	public static void main(String[] args) {
		boolean b = true;
		char ch = 'C';
		
		System.out.printf("b = %b%n", b);
		System.out.printf("!b = %b%n", !b);
		System.out.printf("!!b = %b%n", !!b);
		System.out.printf("!!!b = %b%n", !!!b);
		System.out.println();
		
		System.out.printf("ch = %c%n", ch);
		System.out.printf("ch < 'a' || ch > 'z' = %b%n", ch < 'a' || ch > 'z');
		System.out.printf("!('a' <= ch && ch <= 'z' = %b%n", !('a' <= ch && ch <= 'z'));
		System.out.printf("  'a' <= ch && ch <= 'z' = %b%n", 'a' <= ch && ch <= 'z');
	}	// main의 끝

}
```

```
b = true
!b = false
!!b = true
!!!b = false

ch = C
ch < 'a' || ch > 'z' = true
!('a' <= ch && ch <= 'z' = true
  'a' <= ch && ch <= 'z' = false
```

식 `!!b`가 평가되는 과정은 아래와 같다. 단항연산자는 결합방향이 오른쪽에서 왼쪽이므로 피연산자와 가까운 것부터 먼저 연산된다. 그래서 피연산자의 `b`와 가까운 논리 부정 연산자 `!`가 먼저 수행되어 `false`를 결과로 얻는다. 그리고 이 값에 다시 `!`연산을 수행하므로 `true`를 결과로 얻는다.

``` java
    !!b
→   !!true  가까운 연산자가 먼저 연산된다.
→   !false  !true의 결과는 false이다.
→   true    !false의 결과는 true이다.
```

</br>

## 5.2 비트 연산자 & | ^ ~ << >>

비트 연산자는 피연산자를 비트단위로 논리 연산한다. 피연산자로 시루는 허용하지 않는다. 정수(문자 포함)만 허용한다.

> **|(OR연산자)** 피연산자 중 한 쪽의 값이 1이면, 1을 결과로 얻는다. 그 외에는 0을 얻는다.   
**&(AND연산자)** 피연산 양 쪽이 모두 1이어야만 1을 결과로 얻는다. 그 외에는 0을 얻는다.   
**^(XOR연산자)** 피연산자의 갑싱 소로 다를 때만 1을 결과로 얻는다. 그 외에는 0을 얻는다.

![iamge](https://ifh.cc/g/8RWGyG.png)

비트OR연산자 `|`는 주로 특정 비트의 값을 변경할 때 사용한다.

비트AND연산자 `&`는 주로 특정 비트의 값을 뽑아낼 때 사용한다.

비트XOR연산자 `^`는 두 피연산자의 비트가 다를 때만 1이 된다. 그리고 같은 값으로 두고 XOR연산을 수행하면 원래의 값으로 돌아오는 특징이 있어서 간단한 암호화에 사용된다.

예제 3-28 / ch3 / OperatorEx28.java
``` java
public class OperatorEx28 {

	public static void main(String[] args) {
		int x = 0xAB, y = 0xF;
		
		System.out.printf("x = %#X \t\t%s%n", x, toBinaryString(x));
		System.out.printf("y = %#X \t\t%s%n", y, toBinaryString(y));
		System.out.printf("%#X | %#X = %#X \t%s%n", x, y, x | y, toBinaryString(x | y));
		System.out.printf("%#X & %#X = %#X \t%s%n", x, y, x & y, toBinaryString(x & y));
		System.out.printf("%#X ^ %#X = %#X \t%s%n", x, y, x ^ y, toBinaryString(x ^ y));
		System.out.printf("%#X ^ %#X ^ %#X = %#X %s%n", x, y, y, x ^ y ^ y, toBinaryString(x ^ y ^ y));
	}	// main의 끝
	
	static String toBinaryString(int x) {
		String zero = "00000000000000000000000000000000";
		String tmp = zero + Integer.toBinaryString(x);
		return tmp.substring(tmp.length() - 32);
	}

}
```

```
x = 0XAB 		00000000000000000000000010101011
y = 0XF 		00000000000000000000000000001111
0XAB | 0XF = 0XAF 	00000000000000000000000010101111
0XAB & 0XF = 0XB 	00000000000000000000000000001011
0XAB ^ 0XF = 0XA4 	00000000000000000000000010100100
0XAB ^ 0XF ^ 0XF = 0XAB 00000000000000000000000010101011
```

비트연산의 결과를 2진수로 출력하기 위해 `toBinaryString()`이라는 메소드를 작성해서 사용하였다. 이 메소드는 4 byte의 정수를 32자리의 2진수로 변환한다.

### 비트 전환 연산자 ~

이 연산자는 피연산자를 2진수로 표현했을 떄, 0은 1로, 1은 0으로 바꾼다. 논리부정 연산자 `!`와 유사하다.

![image](https://ifh.cc/g/xr6LcP.png)

비트 전환 연산자 `~`에 의해 '비트 전환'되고 나면, 부호있는 타입의 피연산자는 부호가 반대로 변경된다. 즉, 피연산자의 '1의 보수'를 얻을 수 있는 것이다. 그래서 비트전환연산자를 '1의 보수'연산자라고도 한다.

예제 3-29 / ch3 / OperatorEx29.java
``` java
public class OperatorEx29 {

	public static void main(String[] args) {
		byte p = 10;
		byte n = -10;
		
		System.out.printf(" p = %d \t%s%n", p, toBinaryString(p));
		System.out.printf(" ~p = %d \t%s%n", ~p, toBinaryString(~p));
		System.out.printf(" ~p + 1 = %d \t%s%n", p, toBinaryString(~p + 1));
		System.out.printf(" ~~p = %d \t%s%n", ~~p, toBinaryString(~~p));
		System.out.println();
		System.out.printf(" n = %d%n", n);
		System.out.printf("~(n - 1) = %d%n", ~(n - 1));
	}	// main의 끝

	static String toBinaryString(int x) {
		String zero = "00000000000000000000000000000000";
		String tmp = zero + Integer.toBinaryString(x);
		return tmp.substring(tmp.length() - 32);
	}

}
```

```
 p = 10 	00000000000000000000000000001010
 ~p = -11 	11111111111111111111111111110101
 ~p + 1 = 10 	11111111111111111111111111110110
 ~~p = 10 	00000000000000000000000000001010

 n = -10
~(n - 1) = 10
```

양의 정수 `p`가 있을 때, `p`에 대한 음의 정수를 얻으려면 `~p + 1`을 계산하면 된다.

반대로 음의 정수 n이 있을 때, n에 대한 양의 정수를 얻으려면 `~( n - 1)`을 계산하면 된다. 물론 부호 연산자 `-`를 사용하면 되므로, 이렇게 복잡하게 변환하지 않는다.

### 쉬프트 연산자 << >>

이 연산자는 피연산자의 각 자리(2진수로 표현했을 때)를 '오른쪽(>>)' 또는 '왼쪽(<<)'으로 이동(shift)한다고 해서 '쉬프트 연산자(shift operator)'라고 이름 붙여졌다.

쉬프트 연산자 자리이동으로 저장범위를 벗어난 값들은 버려지고 빈자리는 0으로 채워진다.


`<<`연산자의 경우, 피연산자의 부호에 상관없이 각 자리를 왼쪽으로 이동시키며 빈칸을 0으로만 채우면 되지만, `>>`연산자는 오른쪽으로 이동시키기 때문에 부호있는 정수는 부호를 유지하기 위해 왼쪽 피연산자가 음수인 경우 빈자리르 1로 채운다. 물론 양수일 때는 0으로 채운다.

쉬프트 연산자의 좌측 피연산자는 산술변환이 적용되어 `int`보다 작은 타입은 `int`타입으로 자동 변환되고 연산결과 역시 `int`타입이 된다 그러나 쉬프트 연산자는 다른 이항연산자들과 달리 피연산자의 타입을 일치시킬 필요가 없기 때문에 우측 피연산자에는 산술변환이 적용되지 않는다.

2진수 n자리를 왼쪽으로 이동하면 피연산자를 2<sup>n</sup>으로 곱한 결과를, 오른쪽으로 이동하면 피연산자 2<sup>n</sup>으로 나눈 결과를 얻는다.

> **x << n은 x * 2<sup>n</sup>의 결과와 같다.**   
**x >> n은 x / 2<sup>n</sup>의 결과와 같다.**

`x << n` 또는 `x >> n`에서, n의 값이 자료형의 bit수 보다 크면, 자료형의 bit수로 나눈 나머지만큼만 이동한다. 예를 들어 `int`타입이 4 byte(=32 bit)인 경우, 자리수를 32번 바꾸면 결국 제자리로 돌아오기 때문에, '8 >> 32'는 아무 일도 하지 않는다. ' 8 >> 34'는 34를 32로 나눈 나머지인 2만큼만 이동하는 '8 >> 2'를 수행한다. 당연히 n은 정수만 가능하며, 음수인 경우, 부호없는 정수로 자동 변환된다.

`<<`연산자를 사용하는 것이 나눗셈 `/` 또는 곱셉 `*` 연산자를 사용하는 것보다 빠르다.

그러나 프로그램의 실행속도도 중요하지만 프로그램을 개발할 때 코드의 가독성(readability)도 중요하다. 쉬프트 연산자가 속도가 빠르긴 해도 곱셈이나 나눗셈 연산자보다는 가독성이 떨어진다. 쉬프트 연산자보다 곱셈 또는 나눗셈 연산자를 주로 사용하고, 보다 빠른 실행속도가 요구되어지는 곳만 쉬프트 연산자를 사용하는 것이 좋다.

예제 3-30 / ch3 / OperatorEx30.java
``` java
public class OperatorEx30 {
	// 10진 정수를 2진수로 변환하는 메소드
	static String toBinaryString(int x) {
		String zero = "00000000000000000000000000000000";
		String tmp = zero + Integer.toBinaryString(x);
		return tmp.substring(tmp.length() - 32);
	}
	
	public static void main(String[] args) {
		int dec = 8;
		
		System.out.printf("%d >> %d = %4d \t%s%n", dec, 0, dec >> 0, toBinaryString(dec >> 0));
		System.out.printf("%d >> %d = %4d \t%s%n", dec, 1, dec >> 1, toBinaryString(dec >> 1));
		System.out.printf("%d >> %d = %4d \t%s%n", dec, 2, dec >> 2, toBinaryString(dec >> 2));
		System.out.printf("%d << %d = %4d \t%s%n", dec, 0, dec << 0, toBinaryString(dec << 0));
		System.out.printf("%d << %d = %4d \t%s%n", dec, 1, dec << 1, toBinaryString(dec << 1));
		System.out.printf("%d << %d = %4d \t%s%n", dec, 2, dec << 2, toBinaryString(dec << 2));
		System.out.println();
		
		dec = -8;
		
		System.out.printf("%d >> %d = %4d \t%s%n", dec, 0, dec >> 0, toBinaryString(dec >> 0));
		System.out.printf("%d >> %d = %4d \t%s%n", dec, 1, dec >> 1, toBinaryString(dec >> 1));
		System.out.printf("%d >> %d = %4d \t%s%n", dec, 2, dec >> 2, toBinaryString(dec >> 2));
		System.out.printf("%d << %d = %4d \t%s%n", dec, 0, dec << 0, toBinaryString(dec << 0));
		System.out.printf("%d << %d = %4d \t%s%n", dec, 1, dec << 1, toBinaryString(dec << 1));
		System.out.printf("%d << %d = %4d \t%s%n", dec, 2, dec << 2, toBinaryString(dec << 2));
		System.out.println();
		
		dec = 8;
		
		System.out.printf("%d >> %2d = %4d \t%s%n", dec, 0, dec >> 0, toBinaryString(dec >> 0));
		System.out.printf("%d >> %2d = %4d \t%s%n", dec, 32, dec >> 32, toBinaryString(dec >> 32));		
	}	// main의 끝

}
```

```
8 >> 0 =    8 	00000000000000000000000000001000
8 >> 1 =    4 	00000000000000000000000000000100
8 >> 2 =    2 	00000000000000000000000000000010
8 << 0 =    8 	00000000000000000000000000001000
8 << 1 =   16 	00000000000000000000000000010000
8 << 2 =   32 	00000000000000000000000000100000

-8 >> 0 =   -8 	11111111111111111111111111111000
-8 >> 1 =   -4 	11111111111111111111111111111100
-8 >> 2 =   -2 	11111111111111111111111111111110
-8 << 0 =   -8 	11111111111111111111111111111000
-8 << 1 =  -16 	11111111111111111111111111110000
-8 << 2 =  -32 	11111111111111111111111111100000

8 >>  0 =    8 	00000000000000000000000000001000
8 >> 32 =    8 	00000000000000000000000000001000
```

예제 3-31 / ch3 / OperatorEx31.java
``` java
public class OperatorEx31 {

	public static void main(String[] args) {
		int dec = 1234;
		int hex = 0xABCD;
		int mask = 0xF;
		
		System.out.printf("hex = %X%n", hex);
		System.out.printf("%X%n", hex & mask);
		
		hex = hex >> 4;
		System.out.printf("%X%n", hex & mask);
		
		hex = hex >> 4;
		System.out.printf("%X%n", hex & mask);
		
		hex = hex >> 4;
		System.out.printf("%X%n", hex & mask);
	}	// main의 끝

}
```

```
hex = ABCD
D
C
B
A
```

쉬프트 연산자와 비트 AND연산자를 이용해서 16진수를 끝에서부터 한자리씩 뽑아내는 예제이다. 비트 AND연산자는 두 bit가 모두 1일 때만 1이 되므로 0xABCD와 0x000F를 비트 AND연산하면 마지막 자리만 남고 나머지자리는 모두 0이 된다.

그 다음엔 쉬프트 연산자로 0xABCD를 2진수로 4자리를 오른쪽으로 이동한다. 2진수 4자리는 16진수로 한자리에 해당하므로 0xABCD는 0x0ABC가 된다.

0x0ABC에서 다시 0xF로 비트AND연산을 수행하면 0xABCD의 오른쪽 끝에서 두번쨰 자리인 0xC를 결과로 얻을 수 있다.

