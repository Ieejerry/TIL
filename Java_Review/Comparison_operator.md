Chapter 3. 연산자

# 4. 비교 연산자

비교 연산자는 두 피연산자를 비교하는 데 사용되는 연산자다. 주로 조건문과 반복문의 조건식에 사용되며, 연산결과는 오직 `true`와 `false` 둘 중의 하나이다.

비교 연산자 역시 이항 연산자이므로 비교하는 피연산자의 타입이 서로 다를 경우에는 자료형의 범위가 큰 쪽으로 자동 형변환하여 피연산자의 타입을 일치시킨 후에 비교한다.

</br>

## 4.1 대소비교 연산자 < > <= >=

두 피연산자의 값의 크기를 비교하는 연산자이다. 참이면 `true`를, 거짓이면 `false`를 결과로 반환한다. 기본형 중에서는 `boolean`형을 제외한 나머지 자료형에 다 사용할 수 있지만 참조형에는 사용할 수 없다.

![image](https://ifh.cc/g/QBsl7L.png)

> '>='와 같이 두 개의 기호로 이루어진 연산자는 '=>'와 같이 기호의 순서를 바꾸거나 '> ='와 같이 중간에 공백이 들어가서는 안 된다.

예제 3-31 / ch3 / OperatorEx21.java
``` java
public class OperatorEx21 {

	public static void main(String[] args) {
		System.out.printf("10 == 10.f 	\t %b%n", 10 == 10.f);
		System.out.printf("'0' == 0 	\t %b%n", '0' == 0);
		System.out.printf("'A' == 65 	\t %b%n", 'A' == 65);
		System.out.printf("'A' > 'B' 	\t %b%n", 'A' > 'B');
		System.out.printf("'A' + 1 != 'B' 	\t %b%n", 'A' + 1 != 'B');
	}

}
```

```
10 == 10.f 		 true
'0' == 0 		 false
'A' == 65 		 true
'A' > 'B' 		 false
'A' + 1 != 'B' 		 false
```

비교 연산자도 이항 연산자이므로 연산을 수행하기 전에 형변환을 통해 두 피연자의 타입을 같게 맞춘 다음 피연산자를 비교한다. `10 == 10.0f`에서 `10`은 `int`타입이고 `10.0f`는 `float`타입이므로, `10`을 `float`로 변환한 다음에 비교한다. 두 값이 `10.0f`로 같으므로 결과로 `true`를 얻게 된다.

``` java
    10    == 10.0f
→   10.0f == 10.0f
→   true
```

문자 'A'의 유니코드는 10진수로 65이고, 'B'는 66, '0'은 48이므로 나머지 식들은 다음과 같은 과정으로 연산된다.

``` java
'0' == 0  → 48 == 0  → false
'A' == 65 → 65 == 65 → true

'A' > 'B' → 65 > 66  → false
'A' + 1 != 'B' → 65 + 1 != 66 → 66 != 66 → false
```

예제 3-22 / ch3 / OperatorEx22.java
``` java
public class OperatorEx22 {

	public static void main(String[] args) {
		float f = 0.1f;
		double d = 0.1;
		double d2 = (double)f;
		
		System.out.printf("10.0 == 10.0f %b%n", 10.0 == 10.0f);
		System.out.printf("0.1 == 0.1f %b%n", 0.1 == 0.1f);
		System.out.printf("f = %19.17f%n", f);
		System.out.printf("d = %19.17f%n", d);
		System.out.printf("d2 = %19.17f%n", d2);
		System.out.printf("d == f %b%n", d == f);
		System.out.printf("d == d2 %b%n", d == d2);
		System.out.printf("d2 == f %b%n", d2 == f);
		System.out.printf("(float)d == f %b%n", (float)d == f);
	}

}
```

```
10.0 == 10.0f true
0.1 == 0.1f false
f = 0.10000000149011612
d = 0.10000000000000000
d2 = 0.10000000149011612
d == f false
d == d2 false
d2 == f true
(float)d == f true
```

정수형과 달리 실수형은 근사값으로 저장되므로 오차가 발생할 수 있다.

`10.0f`는 오차없이 저장할 수 있는 값이라서 `double`로 형변환해도 그대로 `10.0`이 되지만, `0.1f`는 저장할 떄 2진수로 변환하는 과정에서 오차가 발생한다. `double`타입의 상수인 `0.1`도 저장되는 과정에서 오차가 발생하지만, `float`타입의 리터럴인 `0.1f`보다 적은 오차로 저장된다.

``` java
float f = 0.1f; // f에 0.10000000149011612로 저장된다.
double d = 0.1; // d에 0.10000000000000001로 저장된다.
```

`float`타입의 값을 `double`타입으로 형변환하면, 부호와 지수는 달라지지 않고 그저 가수의 빈자리를 0으로 채울 뿐이므로 `0.1f`를 `double`타입으로 형변화해도 그 값은 전혀 달라지지 않는다. 즉, `float`타입의 값을 정밀도가 더 높은 `double`타입으로 형변환했다고 해서 오차가 적어지는 것이 아니다.

> 아래 그림에서 지수부의 값도 달라진 것처럼 보이지만, float타입과 double타입의 기저(bias)의 차이에 의한 것일 뿐 달라지지 않았다.

![image](https://ifh.cc/g/NV1PHV.png)

식 `d == f`가 연산되는 과정을 단계별로 살펴보면 다음과 같다. 최종결과는 `false`이다. 변수 `f`를 `double`타입으로 형변환해도 값이 변하지 않았다.

``` java
    d == f
→   d == (double)f
→   0.10000000000000001 == (double)0.10000000149011612
→   0.10000000000000001 == 0.10000000149011612
→   false
```

마찬가지로 변수 `d2`에 변수 `f`의 값을 `double`로 형변환해서 저장해도, `f`의 값이 그대로 `d2`에 저장된다. 그래서 `d2 == f`의 결과가 `true`가 된다.

``` java
    double d2 = (double)f;
→   double d2 = (double)0.10000000149011612;
→   double d2 = 0.10000000149011612;

    d2 == f
→   0.10000000149011612 == 0.10000000149011612
→   true
```

`float`타입의 값과 `double`타입의 값을 비교하려면 `double`타입의 값을 `float`타입으로 형변환한 당므에 비교해야 한다. 그래야만 올바른 결과를 얻을 수 있다. 어느 정도의 오차는 무시하고 두 타입의 값을 앞에서 몇 자리만 잘라서 비교할 수도 있다.

``` java
    (float)d == f
→   (float)0.10000000000000001 == 0.10000000149011612
→   0.10000000149011612 == 0.10000000149011612
→   true
```

### 문자열의 비교

두 문자열을 비교할 때는, 비교 연산자 `==`대신 `equals()`라는 메소드를 사용해야 한다. 비교 연산자는 두 문자열이 완전히 같은 것인지 비교할 뿐이므로, 문자열의 내용이 같은지 비교하기 위해서는 `equals()`를 사용하는 것이다. `equals()`는 비교하는 두 문자열이 같으면 `true`를, 다르면 `false`를 반환한다.

``` java
String str = new String("abc");

// equals()는 두 문자열의 내용이 같으면 true, 다르면 false
boolean result = str.equals("abc"); // 내용이 같으므로 result에 true가 저장됨
```

원래 `String`은 클래스이므로, 아래와 같이 `new`를 사용해서 객체를 생성해야 한다.

``` java
String str = new String("abc"); // String클래스의 객체를 생성
String str = "abc"; // 위의 문장을 간단히 표현
```

그러나 특별히 `String`만 `new`를 사용하지 않고, 위와 같이 간단히 쓸 수 었게 허용한다.

예제 3-23/ ch3 / OperatorEx23.java
``` java
public class OperatorEx23 {

	public static void main(String[] args) {
		String str1 = "abc";
		String str2 = new String("abc");
		
		System.out.printf("\"abc\" == \"abc\" ? %b%n", "abc" == "abc");
		System.out.printf(" str1 == \"abc\" ? %b%n", str1 == "abc");
		System.out.printf(" str2 == \"abc\" ? %b%n", str2 == "abc");
		System.out.printf("str1.equals(\"abc\") ? %b%n", str1.equals("abc"));
		System.out.printf("str2.equals(\"abc\") ? %b%n", str2.equals("abc"));
		System.out.printf("str2.equals(\"ABC\") ? %b%n", str2.equals("ABC"));
		System.out.printf("str2.equalsIgnoreCase(\"ABC\") ? %b%n", str2.equalsIgnoreCase("ABC"));
	}

}
```

```
"abc" == "abc" ? true
 str1 == "abc" ? true
 str2 == "abc" ? false
str1.equals("abc") ? true
str2.equals("abc") ? true
str2.equals("ABC") ? false
str2.equalsIgnoreCase("ABC") ? true
```

`str2`와 `"abc"`의 내용이 같은데도 `==`로 비교하면, `false`를 결과로 얻는다. 내용은 같지만 서로 다른 객체라서 그런 것이다. 그러나 `equals()`는 객체가 달라도 내용이 같으면 `true`를 반환한다. 그래서 문자열을 비교할 때는 항상 `equals()`를 사용해야 한다.

만일 대소문자를 구별하지 않고 비교하고 싶으면, `equalsIgnoreCase()`를 사용하면 된다.