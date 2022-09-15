Chapter 6. 객체지향 프로그래밍1

# 4. 오버로딩(overloading)

</br>

## 4.1 오버로딩이란?

메소드도 변수와 마찬가지로 같은 클래스 내에서 서로 구별될 수 있어야 하기 때문에 각기 다른 이름을 가져야 한다. 그러나 자바에서는 한 클래스 내에 이미 사용하려는 이름과 같은 이름을 가진 메소드가 있더라도 매개변수의 개수 또는 타입이 다르면, 같은 이름을 사용해서 메소드를 정의할 수 있다.

이처럼, 한 클래스 내에 같은 이름의 메소드를 여러 개 정의하는 것을 '메소드 오버로딩(method overloading)' 또는 간단히 '오버로딩(overloading)'이라 한다.

오버로딩(overloading)의 사전적 의미는 '과적하다', 즉, 많이 싣는 것을 뜻한다. 보통 하나의 메소드 이름에 하나의 기능만을 구현해야하는데, 하나의 메소드 이름으로 여러 기능을 구현하기 때문에 붙여진 이름이라 생각할 수 있다.

</br>

## 4.2 오버로딩의 조건

같은 이름의 메소드를 정의한다고 해서 무조건 오버로딩인 것은 아니다. 오버로딩이 성립하기 위해서는 다음과 같은 조건을 만족해야 한다.

> 1. 메소드 이름이 같아야 한다.
> 2. 매개변수의 개수 또는 타입이 달라야 한다.

비록 메소드의 이름이 같다 하더라도 매개변수가 다르면 서로 구별될 수 있기 때문에 오버로딩이 가능한 것이다. 위의 조건을 만족시키지 못하는 메소드는 중복 정의로 간주되어 컴파일 시에 에러가 발생한다. 그리고 오버로딩된 메소드들은 매개변수에 의해서만 구별될 수 있으므로 **변환 타입은 오버로딩을 구현하는데 아무런 영향을 주지 못한다**

</br>

## 4.3 오버로딩의 예

오버로딩의 예로 가장 대표적인 것은 `println`메소드이다. `println`메소드를 호출할 때 매개변수로 지정하는 값의 타입에 따라서 호출되는 `println`메소드가 달라진다.

`PrintStream`클래스에는 어떤 종류의 매개변수를 지정해도 출력할 수 있도록 아래와 같이 10개의 오버로딩된 `println`메소드를 정의해놓고 있다.

``` java
void println()
void println(boolean x)
void println(char x)
void println(char[] x)
void println(double x)
void println(float x)
void println(int x)
void println(long x)
void println(Object x)
void println(String x)
```

`println`메소드를 호출할 때 매개변수로 넘겨주는 값의 타입에 따라서 위의 오버로딩된 메소드들 중의 하나가 선택되어 실행되는 것이다.

몇 가지 에를 들어 오버로딩에 대해 자세히 설명하겠다.

``` java
[보기 1]
int add(int a, int b) { return a + b; }
int add(int x, int y) { return x + y; }
```

위의 두 메소드는 매개변수의 이름만 다를 뿐 매개변수의 타입이 같기 때문에 오버로딩이 성립하지 않는다. 매개변수의 이름이 다르면 메소드 내에서 사용되는 변수의 이름이 달라질 뿐, 아무런 의미가 없다. 그래서 이 두 메소드는 정확히 같은 것이다.

``` java
[보기 2]
int add(int a, int b) { return a + b; }
long add(int a, int b) { return (long)(a + b); }
```

이번 경우는 리턴타입만 다른 경우이다. 매개변수의 타입과 개수가 일치하기 때문에 `add(3, 3)`과 같이 호출하였을 때 어떤메소드가 호출된 것인지 결정할 수 없기 때문에 오버로딩으로 간주되지 않는다.

``` java
[보기 3]
long add(int a, long b) { return a + b; }
long add(long a, int b) { return a + b; }
```

두 메소드 모두 int형과 long형 매개변수가 하나씩 선언되어 있지만, 서로 순서가 다른 경우이다. 이 경우에는 호출 시 매개변수의 값에 의해 호출될 메소드가 구분될 수 있으므로 중복된 메소드 정의가 아닌, 오버로딩으로 간주한다.

이처럼 단지 매개변수의 순서만을 다르게 하여 오버로딩을 구현하면, 사용자가 매개변수의 순서를 외우지 않아도 되는 장점이 있지만, 오히려 단점이 될 수도 있기 때문에 주의해야 한다.

예를 들어 `add(3, 3L)`과 같이 호출되면 첫 번째 메소드가, `add(3L, 3)`과 같이 호출되면 두 번째 메소드가 호출된다. 단, 이 경우에는 `add(3, 3)`과 같이 호출할 수 없다. 이와 같이 호출할 경우, 두 메소드 중 어느 메소드가 호출된 것인지 알 수 없기 때문에 메소드를 호출하는 곳에서 컴파일 에러가 발생한다.

``` java
[보기 4]
int add(int a, int b) { return a + b; }
long add(long a, long b) { return a + b; }
long add(int[] a) {     // 배열의 모든 요소의 합을 반환한다.
    long result = 0;

    for(int i = 0; i <a.length; i++) {
        result += a[i];
    }
    return result;
}
```

위의 메소드들은 모두 바르게 오버로딩되어 있다. 정의된 매개변수가 서로 다르긴 해도, 세 메소드 모두 매개변수로 넘겨받은 값을 더해서 그 결과를 돌려주는 일을 한다.

같은 일을 하지만 매개변수를 달리해야하는 경우에, 이와 같이 이름은 같고 매개변수를 다르게 하여 오버로딩을 구현한다.

</br>

## 4.4 오버로딩의 장점

만일 메소드도 변수처럼 단지 이름만으로 구별된다면, 한 클래스내의 모든 메소드들은 이름이 달라야한다. 그렇다면, 이전에 예로 들었던 10가지의 `println`메소드들은 각기 다른 이름을 가져야 한다.

예를 들면, 아래와 같은 방식으로 메소드 이름이 변경되어야 한다.

``` java
void println()
void printlnBoolean(boolean x)
void printlnChar(char x)
void printlnDouble(double x)
void printlnString(String x)
```

모두 근본적으로는 같은 기능을 하는 메소드들이지만, 서로 다른 이름을 가져야 하기 때문에 메소드를 작성하는 쪽에서는 이름을 짓기도 어렵고, 메소드를 사용하는 쪽에서는 이름을 일일이 구분해서 기억해야하기 때문에 서로 부담이 된다.

하지만 오버로딩을 통해 여러 메소드들이 `println`이라는 하나의 이름으로 정의될 수 있다면, `println`이라는 이름만 기억하면 되므로 기억하기도 쉽고 이름도 짧게 할 수 있어서 오류의 가능성을 많이 줄일 수 있다. 그리고 메소드의 이름만 보고도 '이 메소드들은 이름이 같으니, 같은 기능을 하겠구나'라고 쉽게 예측을 할 수 있게 된다.

또 하나의 장점은 메소드의 이름을 절약할 수 있다는 것이다. 하나의 이름으로 여러 개의 메소드를 정의할 수 있으니, 메소드의 이름을 짓는데 고민을 덜 수 있는 동시에 사용되었어야 할 메소드 이름을 다른 메소드의 이름으로 사용할 수 있기 때문이다.

예제 6-21 / ch6 / OverloadingTest.java

``` java
public class OverloadingTest {

	public static void main(String[] args) {
		MyMath3 mm = new MyMath3();
		System.out.println("mm.add(3, 3) 결과: " + mm.add(3, 3));
		System.out.println("mm.add(3L, 3) 결과: " + mm.add(3L, 3));
		System.out.println("mm.add(3, 3L) 결과: " + mm.add(3, 3L));
		System.out.println("mm.add(3L, 3L) 결과: " + mm.add(3L, 3L));
		
		int[] a = { 100, 200, 300 };
		System.out.println("mm.add(a) 결과: " + mm.add(a));
	}

}

class MyMath3 {
	int add(int a, int b) {
		System.out.print("int add(int a, int b) - ");
		return a + b;
	}
	
	long add(int a, long b) {
		System.out.print("long add(int a, long b) - ");
		return a + b;
	}
	
	long add(long a, int b) {
		System.out.print("long add(long a, int b) - ");
		return a + b;
	}
	
	long add(long a, long b) {
		System.out.print("long add(long a, long b) - ");
		return a + b;
	}
	
	int add(int[] a) {
		System.out.print("int add(int[] a) - ");
		int result = 0;
		for(int i = 0; i < a.length; i++) {
			result += a[i];
		}
		return result;
	}
}
```

```
int add(int a, int b) - mm.add(3, 3) 결과: 6
long add(long a, int b) - mm.add(3L, 3) 결과: 6
long add(int a, long b) - mm.add(3, 3L) 결과: 6
long add(long a, long b) - mm.add(3L, 3L) 결과: 6
int add(int[] a) - mm.add(a) 결과: 600
```

> add(3L, 3), add(3, 3L), add(3L, 3L)의 결과는 모두 6이지만, System.out.println(6L);을 수행하면 6이 출력된다. 리터럴의 접미사는 출력되지 않는다.

``` java
System.out.println("mm.add(3, 3) 결과: " + mm.add(3, 3));
```

`add`메소드가 `println`메소드보다 어떻게 먼저 출력되었냐면, `println`메소드가 결과를 출력하려면, `add`메소드의 결과가 먼저 계산되어야하기 때문이다. 간단히 위의 문장이 아래의 두 문장을 하나로 합친 것이라고 생각하면 이해가 쉽다.

``` java
int result = mm.add(3, 3);
System.out.println("mm.add(3, 3) 결과: " + add(3, 3));
```

</br>

## 4.5 가변인자(varargs)와 오버로딩

기존에는 메소드의 매개변수 개수가 고정적이었으나 JDK1.5부터 동적으로 지정해 줄 수 있게 되었으며, 이 기능을 '가변인자(variable argumemt)'라고 한다.

가변인자는 **'타입... 변수명'** 과 같은 형식으로 선언하며, `PrintStream`클래스의 `printf()`가 대표적인 예이다.

``` java
public PrintStream printf(String format, Object... args) { ... }
```

위와 같이 가변인자 외에도 매개변수가 더 있다면, 가변인자를 매개변수 중에서 제일 마지막에 선언해야 한다. 그렇지 않으면, 컴파일 에러가 발생한다. 가변인자인지 아닌지를 구별할 방법이 없기 때문에 허용하지 않는다.

``` java
// 컴파일 에러 발생 - 가변인자는 항상 마지막 매개변수이어야 한다.
public PrintStream printf(Object... args, String format) {
    ...
}
```

만일 여러 문자열을 하나로 결합하여 반환하는 `concatenate`메소드를 작성한다면, 아래와 같이 매개변수의 개수를 다르게 해서 여러 개의 메소드를 작성해야 한다.

``` java
String concatenate(String s1, String s2) { ... }
String concatenate(String s1, String s2, String s3) { ... }
String concatenate(String s1, String s2, String s3, String s4) { ... }
```

이럴 때, 가변인자를 사용하면 메소드 하나로 간단히 대체할 수 있다.

``` java
String concatenate(String... str) { ... }
```

이 메소드를 호출할 때는 아래와 같이 인자의 개수를 가변적으로 할 수 있다. 심지어는 인자가 아예 없어도 되고 배열도 인자가 될 수 있다.

``` java
System.out.println(concatenate());          // 인자가 없음
System.out.println(concatenate("a"));       // 인자가 하나
System.out.println(concatenate("a", "b"));  // 인자가 둘
System.out.println(concatenate(new String[] { "A", "B" })); // 배열도 가능
```

가변인자는 내부적으로 배열을 이용하는 것이다. 그래서 가변인자가 선언된 메소드를 호출할 때마다 배열이 새로 생성된다. 가변인자가 편리하지만, 이런 비효율이 숨어있으므로 꼭 필요한 경우에만 가변인자를 사용하면 된다.

그러면 가변인자는 아래와 같이 매개변수의 타입을 배열로 하는 것과 어떤 차이가 있는지 알아보겠다.

``` java
String concatenate(String[] str) { ... }

String result = concatenate(new String[0]); // 인자로 배열을 저장 
String result = concatenate(null);          // 인자로 null을 저장 
String result = concatenate();             // 에러. 인자가 필요함. 
```

매개변수의 타입을 배열로 하면, 반드시 인자를 지정해 줘야하기 때문에, 위의 코드에서처럼 인자를 생략할 수 없다. 그래서 `null`이나 길이가 0인 배열을 인자로 지정해주야 하는 불편함이 있다.

예제 6-22 / ch6 / VarArgsEx.java

``` java
public class VarArgsEx {

	public static void main(String[] args) {
		String[] strArr = { "100", "200", "300" };
		
		System.out.println(concatenate("", "100", "200", "300"));
		System.out.println(concatenate("-", strArr));
		System.out.println(concatenate(",", new String[] { "1", "2", "3" }));
		System.out.println("[" + concatenate(",", new String[0]) + "]");
		System.out.println("[" + concatenate(",") + "]");
	}

	static String concatenate(String delim, String... args) {
		String result = "";
		
		for(String str : args) {
			result += str + delim;
		}
		
		return result;
	}
	
//	static String concatenate(String... args) {
//		return concatenate("", args);
//	}
}	// class
```

```
100200300
100-200-300-
1,2,3,
[]
[]
```

`concatenate`메소드는 매개변수로 입력된 문자열에 구분자를 사이에 포함시켜 결합해서 반환한다. 가변인자로 매개변수를 선언했기 때문에 문자열을 개수의 제약없이 매개변수로 지정할 수 있다.

``` java
String[] strArr = new String[] { "100", "200", "300" };
System.out.println(concatenate("-", strArr));
```

위의 두 문장을 하나로 합치면 아래와 같이 쓸 수 있다.

``` java
System.out.println(concatenate("-", new String[] { "100", "200", "300" }));
```

그러나 아래와 같은 문장은 허용되지 않은다는 것을 주의해야 한다.

``` java
system.out.println(concatenate("-", { "100", "200", "300" }));
```

위의 예제에서는 주석처리하였지만, `concatenate메소드의 또 다른 오버로딩된 메소드가 있다.

``` java
static String concatenate(String delim, String... args) {
    String result = "";

    for(String str : args) {
        result += str + delim;
    }

    return result;
}

static String concatenate(String... args) {
    return concatenate("", args);
}
```

이 두 메소드는 별 문제가 없어 보이지만 위의 예제에서 주석을 풀고 컴파일을 하면 아래와 같이 컴파일에러가 발생한다.

```
Exception in thread "main" java.lang.Error: Unresolved compilation problems: 
	The method concatenate(String, String[]) is ambiguous for the type VarArgsEx
	The method concatenate(String, String[]) is ambiguous for the type VarArgsEx

	at VarArgsEx.main(VarArgsEx.java:7)
```

에러의 내용을 살펴보면 두 오버로딩된 메소드가 구분되지 않아서 발생하는 것임을 알 수 있다. 가변인자를 선언한 메소드를 오버로딩하면, 메소드를 호출했을 때 이와 같이 구별되지 못하는 경우가 발생하기 쉽기 때문에 주의해야 한다. 가능하면 가변인ㅇ자를 사용한 메소드는 오버로딩하지 않는 것이 좋다.