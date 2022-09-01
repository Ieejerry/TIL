Chapter 5. 배열 array

# 2. String배열

<br>

## 2.1 String배열의 선언과 생성

배열의 타입이 String인 경우에도 int배열의 선언과 생성방법은 다르지 않다. 예를 들어 3개의 문자열(String)을 담을 수 있는 배열을 생성하는 문장은 다음과 같다.

``` java
String[] name = new String[3];  // 3개의 문자열을 담을 수 있는 배열을 생성한다.
```

3개의 String타입의 참조변수를 저장하기 위한 공간이 마련되고 참조형 변수의 기본값은 null이므로 각 요소의 값은 null로 초기화 된다.

> null은 어떠한 객체도 가리키고 있지 않다는 뜻이다.

![image](https://ifh.cc/g/S4rNXM.png)

변수의 타입에 따른 기본값은 다음과 같다.

![image](https://ifh.cc/g/acyqYQ.png)

## 2.2 String배열의 초기화

초기화 역시 int배열과 동일한 방법으로 한다. 아래와 같이 배열의 각 요소에 문자열을 지정하면 된다.

``` java
String[] name = new String[3];  // 길이가 3인 String배열을 생성
name[0] = "Kim";
name[1] = "Park";
name[2] = "Yi";
```

또는 괄호[]를 사용해서 다음과 같이 간단히 초기화 할 수도 있다.

``` java
String[] name = new String[] { "Kim", "Park", "Yi" };
String[] name = { "Kim", "Park", "Yi" };    // new String[]을 생략할 수 있음
```

특별히 String클래스만 "Kim"과 같이 큰따옴표만으로 간략히 표현하는 것이 허용되지만, 원래 String은 클래스이므로 아래의 왼쪽처럼 `new`연산자를 통해 객체를 생성해야 한다.

![image](https://ifh.cc/g/WG9asG.png)

![image](https://ifh.cc/g/GglVsp.png)

배열에 실제 객체가 아닌 객체의 주소가 저장되어 있는 것을 볼 수 있다. 이처럼, 기본형 배열이 아닌 경우, 즉, 참조형 배열의 경우 배열에 저장되는 것은 객체의 주소이다.

예제 5-12 / ch5 / ArrayEx12.java
``` java
public class ArrayEx12 {

	public static void main(String[] args) {
		String[] names = { "Kim", "Park", "Yi" };
		
		for (int i = 0; i < names.length; i++) {
			System.out.println("names[" + i + "]:" + names[i]);
		}
		
		String tmp = names[2];	// 배열 names의 세 번째 요소를 tmp에 저장
		System.out.println("tmp: " + tmp);
		names[0] = "Yu";	// 배열 names의 첫 번째 요소를 "Yu"로 변경
		
		for (String str : names) {	// 향상된 for문
			System.out.println(str);
		}
	}	// main

}
```

```
names[0]:Kim
names[1]:Park
names[2]:Yi
tmp: Yi
Yu
Park
Yi
```

예제 5-13 / ch5 / ArrayEx13.java
``` java
public class ArrayEx13 {

	public static void main(String[] args) {
		char[] hex = { 'C', 'A', 'F', 'E' };
		
		String[] binary = { "0000", "0001", "0010", "0011",
							"0100", "0101", "0110", "0111",
							"1000", "1001", "1010", "1011",
							"1100", "1101", "1110", "1111" };
		
		String result = "";
		
		for (int i = 0; i < hex.length; i++) {
			if (hex[i] >= '0' && hex[i] <= '9') {
				result += binary[hex[i] - '0'];	// '8' - '0'의 결과는 8이다.
			} else {	// A~F이면
				result += binary[hex[i] - 'A' + 10];	// 'C' - 'A'의 결과는 2
			}
		}
									// String(char[] value)
		System.out.println("hex: " + new String(hex));
		System.out.println("binary: " + result);
	}

}
```

```
hex: CAFE
binary: 1100101011111110
```

16진수를 2진수로 변환하는 예제이다. 먼저 변환하고자 하는 16진수를 배열 `hex`에 나열한다. 16진수에는 A\~F까지 6개의 문자가 포함되므로 char배열로 처리하였다. 그리고 문자열 배열 `binary`에는 이진수 '0000'부터 '1111'(16진수로 0\~F)까지 모두 16개의 값을 문자열로 저장하였다.

for문을 이용해서 배열 `hex`에 저장된 문자를 하나씩 읽어서 그에 해당하는 이진수 표현을 배열 `binary`에서 얻어 `result`에 덧붙이고 그 결과를 화면에 출력한다.

``` java
result += binary[hex[i] - 'A' + 10];
```

`i`의 값이 0일 때, `hex[0]`의 값은 'C'이므로, 위의 문장은 다음과 같은 과정으로 계산된다.

``` java
→   result += binary[hex[0] - 'A' + 10];    // hex[0]은 'C'
→   result += binary['C' - 'A' + 10];   // 'C' - 'A' → 67 - 65 → 2
→   result += binary[2 + 10];
→   result += binary[12];
→   result += "1100";
```

</br>

## 2.3 char배열과 String클래스

지금까지 여러 문자, 즉 문자열을 저장할 때 String타입의 변수를 사용했다. 사실 문자열이라는 용어는 '문자를 연이어 늘어놓은 것'을 의미하므로 문자배열인 char배열과 같은 뜻이다.

그런데 자바에서는 char배열이 아닌 String클래스를 이용해서 문자열을 처리하는 이유는 String클래스가 char배열에 여러 가지 기능을 추가하여 확장한 것이기 때문이다.

> String클래스는 char배열에 기능(메소드)를 추가한 것이다.

객체지향언어인 자바에서는 char배열과 그에 관련된 기능들을 함께 묶어서 클래스에 정의한다.

char배열과 String클래스의 한 가지 중요한 차이가 있는데, String객체(문자열)는 읽을수만 있을 뿐 내용을 변경할 수 없다.

``` java
String str = "Java";
str = str + "8";    // "Java8"이라는 새로운 문자열이 str에 저장된다.
System.out.println(str);    // "Java8"
```

위의 문장에서 문자열 `str`의 내용이 변경되는 것 같지만, 문자열은 변경할 수 없으므로 새로운 내용의 문자열이 생성된다.

> 변경 가능한 문자열을 다루려면, StringBuffer클래스를 사용하면 된다.

### String클래스의 주요 메소드

String클래스는 상당히 많은 문자열 관련 메소드를 제공하지만 가장 기본적인 몇 가지만 살펴보겠다.

![image](https://ifh.cc/g/6X168t.png)

`charAt`메소드는 문자열에서 지정된 index에 있는 한 문자를 가져온다. 배열과 마찬가지로 `charAt`메소드의 index는 0부터 시작한다.

``` java
String str = "ABCDE";
char ch = str.charAt(3);    // 문자열 str의 4번째 문자 'D'를 ch에 저장
```

![image](https://ifh.cc/g/m7AYyv.png)

`substring()`은 문자열의 일부를 뽑아낼 수 있다. 주의할 것은 범위의 끝은 포함되지 않는다.

``` java
String str = "012345";
String tmp = str.substring(1, 4);   // str에서 index범위 1~4의 문자들을 반환
System.out.println(tmp);    // "123"이 출력된다.
```

`equals()`는 문자열의 내용이 같은지 다른지 확인하는데 사용한다. 기본형 변수의 값을 비교하는 경우 `==`연산자를 사용하지만, 문자열의 내용을 비교할 때는 `equals()`를 사용해야 한다. 그리고 이 메소드는 대소문자를 구분한다. 대소문자를 구분하지 않고 비교하려면 `equals`대신 `equalsIgnoreCase()`를 사용해야한다.

``` java
String str = "abc";
if (str.equals("abc")) {    // str와 "abc"가 내용이 같은지 확인한다.
    ...
}
```

### char배열과 String클래스의 변환

가끔 char배열을 String클래스로 변환하거나, 또는 그 반대로 변환해야하는 경우가 있다. 그럴 때 다음의 코드를 사용하면 된다.

``` java
char[] chArr = { 'A', 'B', 'C' };
String str = new String(chArr); // char배열 → String
char[] tmp = str.toCharArray(); // String → char배열
```

예제 5-14 / ch5 / ArrayEx14.java
``` java
public class ArrayEx14 {

	public static void main(String[] args) {
		String src = "ABCDE";
		for (int i =0; i < src.length(); i++) {
		    char ch = src.charAt(i);	// src의 i번째 문자를 ch에 저장
		    System.out.println("src.charAt(" + i +"): " + ch);
		}
		
		// String을 char[] 변환
		char[] chArr = src.toCharArray();
				
		// char배열(char[])을 출력
		System.out.println(chArr);
	}

}
```

```
src.charAt(0): A
src.charAt(1): B
src.charAt(2): C
src.charAt(3): D
src.charAt(4): E
ABCDE
```

String클래스의 `charAt(int idx)`을 사용하는 방법을 보여주는 예제이다. `charAt(int idx)`은 문자열 중에서 `idx`번째 위치에 있는 문자를 반환한다.

그리고 `println()`로 문자배열을 출력하면 문자열 출력하듯이 문자배열의 모든 요소를 이어서 한 줄로 출력한다.

예제 5-15 / ch5 / ArrayEx15.java
``` java
public class ArrayEx15 {

	public static void main(String[] args) {
		String source = "SOSHELP";
		String[] morse = { ".-", "-...", "-.-.", "-..", ".",
						   "..-.", "--.", "....", "..", ".---",
						   "-.-", ".-..", "--", "-.", "---",
						   ".--.", "--.-", ".-.", "...", "-",
						   "..-", "...-", ".--", "-..-", "-.--",
						   "--.." };
		
		String result = "";
		
		for (int i = 0; i < source.length(); i++) {
			result += morse[source.charAt(i) - 'A'];
		}
		System.out.println("source: " + source);
		System.out.println("morse: " + result);
	}

}
```

```
source: SOSHELP
morse: ...---.........-...--.
```

문자열(String)을 모스(morse)부호로 변환하는 예제이다. 

String의 문자의 개수는 `length()`를 통해서 얻을 수 있고, `charAt(int i)`메소드는 String의 i번째 문자를 반환한다. 그래서 for문의 조건식에 `length()`를 사용하고 `charAt(int i)`를 통해서 `source`에서 한 문자씩 차례대로 읽어올 수 있다.

``` java
    result += morse[source.charAt(i) - 'A'];    // i가 0일 때
→   result += morse[source.charAt(0) - 'A'];    // source.charAt(0)는 첫 번째 문자
→   result += morse['S' - 'A']; // 'S' - 'A' → 83 - 65 → 18
→   result += morse[18];
→   result += "...";    // result = result + "...";와 같다.
```

</br>

## 2.4 커맨드 라인을 통해 입력받기

Scanner클래스의 `nextLine()`외에도 화면을 통해 사용자로부터 값을 입력받을 수 있는 간단한 방법이 있다. 바로 커맨드라인을 이용한 방법인데, 프로그램을 실행할 때 클래스 이름 뒤에 공백문자로 구분하여 여러 개의 문자열을 프로그램에 전달할 수 있다.

만일 실행할 프로그램의 `main`메소드가 담긴 클래스의 이름이 MainTest라고 가정하면 다음과 같이 실행할 수 있다.

```
c:\jdk1.9\work\ch5>java MainTest abc 123
```

커맨드라인을 통해 입력된 두 문자열은 String배열에 담겨서 MainTest클래스의 `main`메소드의 매개변수(`args`)에 전달된다. 그리고는 `main`메소드 내에서 `args[0]`, `args[1]`과 같은 방식으로 커맨드라인으로 부터 전달받은 문자열에 접근할 수 있다. 여기서 `args[0]`은 "abc"이고 `args[1]`은 "123"이 된다.

예제 5-16 / ch5 / ArrayEx16.java
``` java
public class ArrayEx16 {

	public static void main(String[] args) {
		System.out.println("매개변수의 개수: " + args.length);
		for (int i = 0; i < args.length; i++) {
			System.out.println("args[" + i + "] = \"" + args[i] + "\"");
		}
	}

}
```

```
C:\jdk1.8\work\ch5>java ArrayEx16 abc 123 "Hello world"
매개변수의 개수: 3
args[0] = "abc"
args[1] = "123"
args[2] = "Hello world"

C:\jdk1.8\work\ch5>java ArrayEx16 ← 매개변수를 입력하지 않았다.
매개변수의 개수: 0
```

커맨드라인에 입력된 매개변수는 공백문자로 구분하기 때문에 입력될 값에 공백이 있는 경우 큰따옴표(")로 감싸주어야 한다. 그리고 커맨드라인에서 숫자를 입력해도 숫자가 아닌 문자열로 처리된다. 문자열 "123"을 숫자 123으로 바꾸려면 다음과 같이 해야한다.

``` java
int num = Integer.parseInt("123");  // 변수 num에 숫자 123이 저장된다.
```

그리고 커맨드라인에 매개변수를 입력하지 않으면 크기가 0인 배열이 생성되어 `args.length`의 값은 0이 된다. 만일 입력된 매개변수가 없다고 해서 배열을 생성하지 않으면 참조변수 `args`의 값은 null이 될 것이고, 배열 `args`를 사용하는 모든 코드에서 에러가 밸생할 것이다. 이러한 에러를 피하려면, 다음과 같이 `main`메소드에 if문을 추가해줘야 한다.

``` java
public static void main(String[] args) {
    if (args != null) { // args가 null이 아닐 때만 괄호{}의 문장들을 수행
        System.out.println("매개변수의 개수: " + args.length);
    }

    for (int i = 0; i < args.length; i++) {
        System.out.println("args[" + i + "] = \"" + args[i] + "\"");
    }
}
```

그러나 JVM이 입력된 매개변수가 없을 때, null 대신 크기가 0인 배열을 생성해서 `args`에 전달하도록 구현되어있다.

예제 5-17 / ch5 / ArrayEx17.java
``` java
public class ArrayEx17 {

	public static void main(String[] args) {
		if (args.length != 3) {	// 입력된 값의 개수가 3개가 아니면
			System.out.println("usage: java Array17 NUM1 OP NUM2");
			System.exit(0);	// 프로그램을 종료한다.
		}
		
		int num1 = Integer.parseInt(args[0]);	// 문자열을 숫자로 변환한다.
		char op = args[1].charAt(0);	// 문자열을 문자(char)로 변환한다.
		int num2 = Integer.parseInt(args[2]);
		int result = 0;
		
		switch(op) {
			case '+':
				result = num1 + num2;
				break;
			case '-':
				result = num1 - num2;
				break;
			case 'x':
				result = num1 * num2;
				break;
			case '/':
				result = num1 / num2;
				break;
			default :
				System.out.println("지원하지 않는 연산입니다.");
		}
		System.out.println("결과: " + result);
	}

}
```

```
C:\jdk1.8\work\ch5>java ArrayEx17
usage: java ArrayEx17 NUM1 OP NUM2

C:\jdk1.8\work\ch5>java ArrayEx17 10 + 3
결과: 13

C:\jdk1.8\work\ch5>java ArrayEx17 10 x 3
결과 30
```

화면으로부터 사칙연산을 수행하는 수식을 입력받아서 계산하여 그 결과를 보여주는 예제이다. 커맨드라인으로부터 입력받은 데이터느 모두 문자열이므로 숫자와 문자로 변환이 필요하며, `Integer.parseInt()`를 사용했다.