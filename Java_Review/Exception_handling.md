Chapter 7. 예외처리 exception handling

# 1. 예외처리(exception handling)

</br>

## 1.1 프로그램 오류

프로그램이 실행 중 어떤 원인에 의해서 오작동을 하거나 비정상적으로 종료되는 경우가 있다. 이러한 결과를 초래하는 원인은 프로그램 에러 또는 오류라고 한다.

이를 발생시점에 따라 '컴파일 에러(complie-time error)'와 런타임 에러(runtime error)'로 나눌 수 있는데, 글자 그대로 '컴파일 에러'는 컴파일 할 때 발생하는 에러이고 프로그램의 실행도중에 발생하는 에러를 '런타임 에러'라고 한다. 이 외에도 '논리적 에러(logical error)'가 있는데, 컴파일도 잘되고 실행도 잘되지만 의도한 것과 다르게 동작하는 것을 말한다.

> **컴파일 에러** 컴파일 시에 발생하는 에러   
> **런타임 에러** 실행 시에 발생하는 에러   
> **논리적 에러** 실행은 되지만, 의도와 다르게 동작하는 것

소스코드를 컴파일 하면 컴파일러가 소스코드(*.java)에 대해 오타나 잘못된 구문, 자료형 체크 등의 기본적인 검사를 수행하여 오류가 있는지를 알려 준다. 컴파일러가 알려 준 에러들을 모두 수정해서 컴파일을 성공적으로 마치고 나면, 클래스 파일(*.class)이 생성되고, 생성된 클래스 파일을 생성할 수 있게 되는 것이다.

하지만 컴파일을 에러없이 성공적으로 마쳤다고 해서 프로그램의 실행 시에도 에러가 발생하지 않는 것은 아니다. 컴파일러가 소스코드의 기본적인 사항은 컴파일 시에 모두 걸러 줄 수는 있지만, 실행도중에 발생할 수 있는 잠재적인 오류까지 검사할 수 없기 때문에 컴파일은 잘되었어도 실행 중에 에러에 의해서 잘못된 결과를 얻거나 프로그램이 비정상적으로 종료될 수 있다.

런타임 에러를 방지하기 위해서는 프로그램의 실행도중 발생할 수 있는 모든 경우의 수를 고려하여 이에 대한 대비를 하는 것이 필요하다. 자바에서는 실행 시(runtime) 발생할 수 있는 프로그램 오류를 '에러(error)'와 '예외(exception)', 두 가지로 구분하였다.

에러는 메모리 부족(OutOfMemoryError)이나 스택오버플로우(StackOverflowError)와 같이 일단 발생하면 복구할 수 없는 심각한 오류이고, 예외는 발생하더라도 수습될 수 있는 비교적 덜 심각한 것이다.

에러가 발생하면, 프로그램의 비정상적인 종료를 막을 길이 없지만, 예외는 발생하더라도 프로그래머가 이에 대한 적절한 코드를 미리 작성해 놓음으로써 프로그램의 비정상적인 종료를 막을 수 있다.

> **에러(error)** 프로그램 코드에 의해서 수습될 수 없는 심각한 오류   
> **예외(exception)** 프로그램 코드에 의해서 수습될 수 있는 다소 미약한 오류

</br>

## 1.2 예외 클래스의 계층구조

자바에서는 실행 시 발생할 수 있는 오류(Exception과 Error)를 크래스로 정의하였다. 모든 클래스이 조상은 `Object`클래스이므로 `Exception`과 `Error`클래스 역시 `Object`클래스의 자손이다.

![image](https://ifh.cc/g/FMzgl9.png)

모든 예외의 최고 조상은 `Exception`클래스이며, 상속계층도를 `Exception`클래스로부터 도식화하면 다음과 같다.

![image](https://ifh.cc/g/YplH4P.png)

예외 클래스들은 다음과 같이 두 그룹으로 나눠질 수 있다.

> 1. Exception클래스와 그 자손들(위 그림의 윗부분, RuntimeException과 자손들 제외)
> 2. RuntimeException클래스와 그 자손들(위 그림의 아랫부분)

`RuntimeException`클래스들은 주로 프로그래머의 실수에 의해서 발생될 수 있는 예외들로 자바의 프로그래밍 요소들과 관계가 깊다.

`Exception`클래스들은 주로 외부의 영향으로 발생할 수 있는 것들로서, 프로그램의 사용자들의 동작에 의해서 발생하는 경우가 많다.

> **Exception클래스들** 사용자의 실수와 같은 외적인 요인에 의해 발생하는 예외   
> **RuntimeException클래스들** 프로그래머의 실수로 발생하는 예외

</br>

## 1.3 예외처리하기 - try-catch문

예외처리(exception handling)란, 프로그램 실행 시 발생할 수 있는 예기치 못한 예외의 발생에 대비한 코드를 작성하는 것이며, 예외처리의 목적은 예외의 발생으로 인한 실행 중인 프로그램의 갑작스런 비정상 종료를 막고, 정상적인 실행상태를 유지할 수 있도록 하는 것이다.

> **예외처리(exception handling)의**   
**정의 -** 프로그램 실행 시 발생할 수 있는 예외에 대비한 코드를 작성하는 것   
**목적 -** 프로그램의 비정상 종료를 막고, 정상적인 실행상태를 유지하는 것

> 에러와 예외는 모두 실행 시(runtime) 발생하는 오류이다.

발생한 예외를 처리하지 못하면, 프로그램은 비정상적으로 종료되며, 처리되지 못한 예외(uncaught exception)는 JVM의 '예외처리기(UncaughtExceptionHandler)'가 받아서 예외의 원인을 화면에 출력한다.

예외를 처리하기 위해서는 try-catch문을 사용하며, 그 구조는 다음과 같다.

``` java
try {
    // 예외가 발생할 가능성이 있는 문장들을 넣는다.
} catch(Exception1 e1) {
    // Exception1이 발생했을 경우, 이를 처리하기 위한 문장을 적는다.
} catch(Exception2 e2) {
    // Exception2이 발생했을 경우, 이를 처리하기 위한 문장을 적는다.
} catch(ExceptionN eN) {
    // ExceptionN이 발생했을 경우, 이를 처리하기 위한 문장을 적는다.
}
```

하나의 try블럭 다음에는 여러 종류의 예외를 처리할 수 있도록 하나 이상의 catch블럭이 올 수 있으며, 이 중 발생한 예외의 종류와 일치하는 단 한 개의 catch블럭만 수행된다. 발생한 예외의 종류와 일치하는 catch블럭이 없으면 예외는 처리되지 않는다.

> if문과 달리 try블럭이나 catch블럭 내에 포함된 문장이 하나뿐이어도 괄호{}를 생략할 수 없다.

예제 8-1 / ch8 / ExceptionEx1.java

``` java
public class ExceptionEx1 {
	public static void main(String[] args) {
		try {
			try { } catch(Exception e) { }
		} catch (Exception e) {
			try { } catch(Exception e) { }	// 에러. 변수 e가 중복 선언되었다.
		}	// try-catch의 끝
		
		try {
			
		} catch (Exception e) {

		}	// try-catch의 끝
	}	// main메소드의 끝
}
```

위의 예제는 아무 일도 하지 않는다. 단순히 try-catch문의 사용 예를 보여 주기 위해서 작성한 코드이다. 이처럼 하나의 메소드 내에 여러 개의 try-catch문이 사용될 수 있으며, try블럭 또는 catch블럭에 또 다른 try-catch문이 포함될 수 있다. catch블럭 내의 코드에서도 예외가 발생할 수 있기 때문이다. catch블럭의 괄호 내에 선언된 변수는 catch블럭 내에서만 유효하기 때문에, 위의 모든 catch블럭에 참조변수 `e`하나 만을 사용해도 된다.

그러나 catch블럭 내에 또 하나의 try-catch문이 포함된 경우, 같은 이름의 참조변수를 사용해서는 안 된다. 각 catch블럭에 선언된 두 참조변수의 영역이 서로 겹치므로 다른 이름을 구현해야만 서로 구별되기 때문이다.

따라서 위의 예제에서 catch블럭 내의 try-catch문에 선언되어 있는 참조변수의 이름을 `e`가 아닌 다른 것으로 바꿔야 한다.

예제 8-2 / ch8 / ExceptionEx2.java

``` java
public class ExceptionEx2 {
	public static void main(String[] args) {
		int number = 100;
		int result = 0;
		
		for(int i = 0; i < 10; i++) {
			result = number / (int)(Math.random() * 10);	// 7번째 라인
			System.out.println(result);
		}
	}	// main의 끝
}
```

```
50
20
Exception in thread "main" java.lang.ArithmeticException: / by zero
	at ExceptionEx2.main(ExceptionEx2.java:7)
```

위의 예제는 변수 `number`에 젖아되어 있는 값 100을 0~9사이의 임의의 정수로 나눈 것과 출력하는 일을 10번 반복한다.

`random()`을 사용했기 때문에 매번 실행할 때마다 결과가 다르겠지만, 대부분의 경우 10번이 출력되기 이전에 예외가 발생하여 프로그램이 비정상적으로 종료된다.

결과에 나타난 메세지를 보면 예외의 발생원인과 위치를 알 수 있다. 미 메세제를 보면, 0으로 나누려 했기 때문에 `ArithmeticException`이 발생했고, 발생위치는 `ExceptionEx2`클래스의 `main`메소드(ExceptionEx2.java의 7번째 라인)라는 것을 알 수 있다.

`ArithmeticException`은 산술연산과정에서 오류가 있을 때 발생하는 예외이며, 정수는 0으로 나누는 것이 금지되어있기 때문에 발생했다. 하지만, 실수를 0으로 나누는 것은 금지되어있지 않으며 예외가 발생하지 않는다.

예외처리구문을 추가해서 실행도중 예외가 발생하더라도 프로그램이 실행 도중에 비정상적으로 종료되지 않도록 수정하겠다.

예제 8-3 / ch8 / ExceptionEx3.java

``` java
public class ExceptionEx3 {
	public static void main(String[] args) {
		int number = 100;
		int result = 0;
		
		for(int i = 0; i < 10; i++) {
			try {
				result = number / (int)(Math.random() * 10);	// 7번째 라인
				System.out.println(result);				
			} catch (ArithmeticException e) {
				System.out.println("0");
			}	// try-catch의 끝
		}
	}	// main의 끝
}
```

```
16
20
11
0   ← ArithmeticException이 발생해서 0이 출력되었다.
25
100
25
33
14
12
```

위의 예제는 예제 8-2에 단순히 try-catch문을 추가한 것이다. `ArithmeticException`이 발생했을 경우에는 0을 화면에 출력하도록 했다. 위의 결과에서 보면, 4번째에 0이 출력되었는데 그 이유는 for문의 4번째 반복에서 `ArithmeticException`이 발생했기 때문이다.

그래서 `ArithmeticException`에 해당하는 catch블럭을 찾아서 그 catch블럭 내의 문장들을 실행한 다음 try-catch문을 벗어나 for문의 다음 반복을 계속 수행하여 작업을 모두 마치고 정상적으로 종료되었다. 만일 예외처리를 하지 않았다면, 세 번째 줄까지만 출력되고 예외가 발생해서 프로그램이 비정상적으로 종료된다.

</br>

## 1.4 try-catch문에서의 흐름

try-catch문에서, 예외가 발생한 경우와 발생하지 않았을 때의 흐름(문장의 실행순서)이 달라지는데, 이래에 이 두 가지 경우에 따른 문장 실행순서를 정리하였다.

> ▶ try블럭 내에서 예외가 발생한 경우,   
> 1. 발생한 예외와 일치하는 catch블럭이 있는지 확인한다.
> 2. 일치하는 catch블럭을 찾게 되면, 그 catch블럭 내의 문장들을 수행하고 전체 try-catch문을 빠져나가서 그 다음 문장을 계속해서 수행한다. 만일 일치하는 catch블럭을 찾지 못하면, 예외는 처리되지 못한다.
>
> ▶ try블럭 내에서 예외가 발생하지 않은 경우,   
> 1. catch블럭을 거치지 않고 전체 try-catch문을 빠져나가서 수행을 계속한다.

예제 8-4 / ch8 / ExceptionEx4.java

``` java
public class ExceptionEx4 {
	public static void main(String[] args) {
		System.out.println(1);
		System.out.println(2);
		try {
			System.out.println(3);
			System.out.println(4);
		} catch (Exception e) {
			System.out.println();	// 실행되지 않는다.
		}	// try-catch의 끝
		System.out.println(6);
	}	// main메소드의 끝
}
```

```
1
2
3
4
6
```

위의 예제에서는 예외가 발생하지 않았으므로 catch블럭의 문장이 실행되지 않았다. 다음의 예제는 위의 예제를 변경해서, try블럭에서 예외가 발생하도록 했다.

예제 8-5 / ch8 / ExceptionEx5.java

``` java
public class ExceptionEx5 {
	public static void main(String[] args) {
		System.out.println(1);
		System.out.println(2);
		try {
			System.out.println(3);
			System.out.println(0 / 0);	// 0으로 나눠서 고의로 ArithmeticException을 발생시킨다.
			System.out.println();	// 실행되지 않는다.
		} catch (Exception e) {
			System.out.println(5);
		}	// try-catch의 끝
		System.out.println(6);
	}	// main의 끝
}
```

```
1
2
3
5
6
```

위의 예제의 결과를 보면, 1, 2, 3을 출력한 다음 try블럭에서 예외가 발생했기 때문에 try블럭을 바로 벗어나서 `System.out.println(4);`는 실행되지 않는다. 그리고는 발생한 예외에 해당하는 catch블럭으로 이동하여 문장들을 수행한다. 다음엔 전체 try-catch문을 벗어나서 그 다음 문장을 실행하여 6을 화면에 출력한다.

try블럭에서 예외가 발생하면, 예외가 발생한 위치 이후에 있는 try블럭의 문장들은 수행되지 않으므로, try블럭에 포함시킬 코드의 범위를 잘 선택해야한다.

</br>

## 1.5 예외의 발생과 catch블럭

catch블럭은 괄호()와 블럭{} 두 부분으로 나눠져 있는데, 괄호()내에는 처리하고자 하는 예외와 같은 타입의 참조변수 하나를 선언해야한다.

예외가 발생하면, 발생한 예외에 해당하는 클래스의 인스턴스가 만들어 진다. 예제 8-5에서는 `ArithmeticException`이 발생했으므로 `ArithmeticException`인스턴스가 생성된다. 예외가 발생한 문장이 try블럭에 포함되어 있따면, 이 예외를 처리할 수 있는 catch블럭이 있는지 찾게 된다.

첫 번째 catch블럭부터 차례로 내려가면서 catch블럭의 괄호()내에 선언된 참조변수의 종류와 생ㅅ어된 예외클래스의 인스턴스에 `instanceof`연산자를 이용해서 검사하게 되는데, 검사결과가 `true`인 catch블럭을 만날 때까지 검사는 계속된다.

검사결과가 `true`인 catch블럭을 찾게 되면 블럭에 있는 문장들을 모두 수행한 후에 try-catch문을 빠져나가고 예외는 처리되지만, 검사결과가 `true`인 catch블럭이 하나도 없으면 예외는 처리되지 않는다.

모든 예외 클래스는 `Exception`클래스의 자손이므로, catch블럭의 괄호{}에 `Exception`클래스 타입의 참조변수를 선언해 놓으면 어떤 종류의 예외가 발생하더라도 이 catch블럭에 의해서 처리된다.

예제 8-6 / ch8 / ExceptionEx6.java

``` java
public class ExceptionEx6 {
	public static void main(String[] args) {
		System.out.println(1);
		System.out.println(2);
		try {
			System.out.println(3);
			System.out.println(0 / 0);
			System.out.println(4);	// 실행되지 않는다.
		} catch (Exception e) {
			System.out.println(5);
		}	// try-catch의 끝
		System.out.println(6);
	}	// main의 끝
}
```

```
1
2
3
5
6
```

이 예제는 예제 8-5를 변경한 것인데, 결과는 같다. catch블럭의 괄호()에 `ArithmeticException`타입의 참조변수 대신에 `Exception`클래스의 참조변수를 선언하였다.

`ArithmeticException`클래스는 `Exception`클래스의 자손이므로 `ArithmeticException`인스턴스와 `Exception`클래스와의 `instanceof`연산결과가 `true`가 되어 `Exception`클래스타입의 참조변수를 선언한 catch블럭의 문장들이 수행되고 예외는 처리되는 것이다.

예제 8-7 / ch8 / ExceptionEx7.java

``` java
public class ExceptionEx7 {
	public static void main(String[] args) {
		System.out.println(1);
		System.out.println(2);
		try {
			System.out.println(3);
			System.out.println(0 / 0);	// 0으로 나눠서 ArithmeticException을 발생시킨다.
			System.out.println(4);	// 실행되지 않는다.
		} catch (ArithmeticException ae) {
			if(ae instanceof ArithmeticException) {
				System.out.println("true");
			}
			System.out.println("ArithmeticException");
		} catch (Exception e) {
			System.out.println("Exception");
		}	// try-catch의 끝
		System.out.println(6);
	}	// main의 끝
}
```

```
1
2
3
true
ArithmeticException
6
```

위의 예제에서는 두 개의 catch블럭, `ArithmeticException`클래스 타입의 참조변수를 선언한 것과 `Exception`클래스 타입의 참조변수를 선언한 것을 사용하였다.

try블럭에서는 `ArithmeticException`이 발생하였으므로 catch블럭을 하나씩 차례로 검사하게 되는데, 첫 번째 검사에서 일치하는 catch블럭을 찾았기 때문에 두 번째 catch블럭은 검사하지 않게 된다. 만일 try블럭 내에서 `ArithmeticException`이 아닌 다른 종류의 예외가 발생한 경우에는 두 번째 catch블럭인 `Exception`클래스 타입의 참조변수를 선언한 곳에서 처리되었을 것이다.

이처럼, try-catch문의 마지막에 `Exception`클래스 타입의 참조변수를 선언한 catch블럭을 사용하면, 어떤 종류의 예외가 발생하더라도 이 catch블럭에 의해 처리되도록 할 수 있다.

### printStackTrace()와 getMessage()

예외가 발생했을 때 생성되는 예외 클래스의 인스턴스에는 발생한 예외에 대한 정보가 담겨 있으며, `getMessage()`와 `printStackTrace()`를 통해서 이 정보들을 얻을 수 있다.

catch블럭의 괄호()에 선언된 참조변수를 통해 이 인스턴스에 접근할 수 있다. 이 참조변수는 선언된 catch블럭 내에서만 사용 가능하며, 자주 사용되는 메소드는 다음과 같다.

> **printStackTrace()** 예외발생 당시의 호출스택(Call Stack)에 있었던 메소드의 정보와 예외 메세지를 화면에 출력한다.   
> **getMessage()** 발생한 예외클래스의 인스턴스에 저장된 메세지를 얻을 수 있다.

예제 8-8 / ch8 / ExceptionEx8.java

``` java
public class ExceptionEx8 {
	public static void main(String[] args) {
		System.out.println(1);
		System.out.println(2);
		try {
			System.out.println(3);
			System.out.println(0 / 0);	// 예외 발생
			System.out.println(4);	// 실행되지 않는다.
		} catch (ArithmeticException ae) {
			ae.printStackTrace();	// 참조변수 ae를 통해, 생성된 ArithmeticException인스턴스에 접근할 수 있다.
			System.out.println("예외 메세지 : " + ae.getMessage());
		}	// try-catch의 끝
		System.out.println(6);
	}	// main메소드의 끝
}
```

```
1
2
3
java.lang.ArithmeticException: / by zero
	at ExceptionEx8.main(ExceptionEx8.java:7)
예외 메세지 : / by zero
6
```

위의 예제의 결과는 예외가 발생해서 비정상적으로 종료되었을 때의 결과와 비슷하지만 예외는 try-catch문에 의해 처리되었으며 프로그램은 정상적으로 종료되었다.

그 대신 `ArithmeticException`인스턴스의 `printStackTrace()`를 사용해서, 호출스택(call stack)에 대한 정보와 예외 메세지를 출력하였다. 이처럼 try-catch문으로 예외처리를 하여 예외가 발생해도 비정상적으로 종료하지 않도록 해주는 동시에, `printStackTrace()` 또는 `getMessage()`와 같은 메소드를 통해서 예외의 발생원인을 알 수 있다.

> printStackTrace(PrintStream s) 또는 printStackTrace(PrintWriter s)를 사용하면 발생한 예외에 대한 정보를 파일에 저장할 수도 있다.

### 멀티 catch블럭

JDK1.7부터 여러 catch블럭을 `|`기호로 이용해서, 하나의 catch블럭으로 합칠 수 있게 되었으며, 이를 '멀티 catch블럭'이라 한다. 아래의 코드에서 알 수 있듯이 '멀티 catch블럭'을 이용하면 중복된 코드를 줄일 수 있다. 그리고 `|`기호로 연결할 수 있는 예외 클래스의 개수에는 제한이 없다.

> 멀티 catch블럭에 사용되는 '|'는 논리 연산자가 아니라 기호이다.

![image](https://ifh.cc/g/yM6h1V.png)

만일 멀티 catch블럭의 `|`기호로 연결된 예외 클래스가 조상과 자손의 관계에 있다면 컴파일 에러가 발생한다.

``` java
try {
    ...
} catch (ParentException | ChildException e) {  // 에러
    e.printStackTrace();
}
```

왜냐하면, 두 예외 클래스가 조상과 조상의 관계에 있다면, 그냥 다음과 같이 조상 클래스만 써주는 것과 똑같기 때문이다. 불필요한 코드는 제거하라는 의미에서 에러가 발생하는 것이다.

``` java
try {
    ...
} catch (ParentException e) {
    e.printStackTrace();
}
```

그리고 멀티 catch는 하나의 catch블럭으로 여러 예외를 처리하는 것이기 때문에, 발생한 예외를 멀티 catch블럭으로 처리하게 되었을 때, 멀티 catch블럭 내에서는 실제로 어떤 예외가 발생한 것인지 알 수 없다. 그래서 참조변수 `e`로 멀티 catch블럭에 `|`기호로 연결된 예외 클래스들의 공통 분모인 조상 예외 클래스에 선언된 멤버만 사용할 수 있다.

``` java
try {
    ...
} catch(ExceptionA | ExceptionB e) {
    e.methodA();    // 에러. ExceptionA에 선언된 methodA()는 호출불가

    if(e instanceof ExceptionA) {
        ExceptionA e1 = (ExceptionA)e;
        e1.methodA();   // OK. ExceptionA에 선언된 메소드 호출가능
    } else {    // if(e instanceof ExceptionB)
        ...
    }
    e.printStackTrace();
}
```

필요하다면, 위와 같이 `instanceof`로 어떤 예외가 발생한 것인지 확인하고 개별적으로 처리할 수는 있다.

마지막으로 멀티 catch블럭에 선언된 참조변수 `e`는 상수이므로 값을 변경할 수 없다는 제약이 있는데, 이것은 여러 catch블럭이 하나의 참조변수를 공유하기 때문에 생기는 제약으로 실제로 참조변수의 값을 바꿀 일은 없다.

</br>

## 1.6 예외 발생시키기

키워드 `throw`를 사용해서 프로그래머가 고의로 예외를 발생시킬 수 있으며, 방법은 아래의 순서를 따르면 된다.

> 1. **먼저 연산자 new를 이용해서 발생시키려는 예외 클래스의 객체를 만든 다음**   
Exception e = new Exception("고의로 발생시켰음");
> 2. **키워드 throw를 이용해서 예외를 발생시킨다.**   
throw e;

예제 8-9 / ch8 / ExceptionEx9.java

``` java
public class ExceptionEx9 {
	public static void main(String[] args) {
		try {
			Exception e = new Exception("고의로 발생시켰음.");
			throw e;	// 예외를 발생시킴
//			throw new Exception("고의로 발생시켰음.");	// 위의 두 줄을 한 줄로 줄여 쓸 수 있다.
		} catch (Exception e) {
			System.out.println("에러메세지 : " + e.getMessage());
			e.printStackTrace();
		}
		System.out.println("프로그램이 정상 종료되었음.");
	}
}
```

```
에러메세지 : 고의로 발생시켰음.
java.lang.Exception: 고의로 발생시켰음.
	at ExceptionEx9.main(ExceptionEx9.java:4)
프로그램이 정상 종료되었음.
```

`Exception`인스턴스를 생성할 때, 생성자에 `String`을 넣어 주면, 이 `String`이 `Exception`인스턴스에 메세지로 저장된다. 이 메세지는 `getMessage()`를 이용해서 얻을 수 있다.

예제 8-10 / ch8 / ExceptionEx10.java

``` java
public class ExceptionEx10 {
	public static void main(String[] args) {
		throw new Exception();	// Exception을 고의로 발생시킨다.
	}
}
```

```
Exception in thread "main" java.lang.Error: Unresolved compilation problem: 
	Unhandled exception type Exception

	at ExceptionEx10.main(ExceptionEx10.java:3)
```

이 예제를 작성한 후에 컴파일 하면, 위와 같은 에러가 발생하며 컴파일이 완료되지 않을 것이다. 예외처리가 되어야 할 부분에 예외처리가 되어 있지 않다는 에러이다. 위의 결과에서 알 수 있는 것처럼, 분류한 `Exception클래스들(Exception클래스와 그 자손들)'이 발생할 가능성이 있는 문장들에 대해 예외처리를 해주지 않으면 컴파일조차 되지 않는다.

예제 8-11 / ch8 / ExceptionEx11.java

``` java
public class ExceptionEx11 {
	public static void main(String[] args) {
		throw new RuntimeException();	// RuntimeException을 고의로 발생시킨다.
	}
}
```

```
Exception in thread "main" java.lang.RuntimeException
	at ExceptionEx11.main(ExceptionEx11.java:3)
```

이 예제는 예외처리를 하지 않았음에도 불구하고 이전의 예제와는 달리 성공적으로 컴파일될 것이다. 그러나 실행하면, 위의 실행결과처럼 `RuntimeException`이 발생하여 비정상적으로 종료될 것이다.

이 예제가 명백히 `RuntimeException`을 발생시키는 코드를 가지고 있고, 이에 대한 예외처리를 하지 않았음에도 불구하고 성공적으로 컴파일 되었다.

이 장의 앞부분에서 설명한 것과 같이 `RuntimeException`클래스와 그 자손(RuntimeException클래스들)'에 해당하는 예외는 프로그래머에 의해 실수로 발생하는 것들이기 때문에 예외처리를 강제하지 않는 것이다. 만일 `RuntimeException`클래스들에 속하는 예외가 발생할 가능성이 있는 코드에도 예외처리를 필수로 해야 한다면, 아래와 같이 참조 변수와 배열이 사용되는 모든 곳에 예외처리를 해주어야 한다.

``` java
try {
    int[] arrr = new int[10];

    System.out.println(arr[0]);
} catch(ArrayIndexOutOfBoundsException ae) {
    ...
} catch(NullPointerException ne) {
    ...
}
```

컴파일러가 예외처리를 확인하지 않는 `RuntimeException`클래스들은 'unchecked예외'라고 부르고, 예외처리를 확인하는 `Exception`클래스들은 'checked예외'라고 부른다.

</br>

## 1.7 메소드에 예외 선언하기

메소드에 예외를 선언하려면, 메소드의 선언부에 키워드 `throws`를 사용해서 메소드 내에서 발생할 수 있는 예외를 적어주기만 하면 된다. 그리고 예외가 여러 개일 경우에는 쉼표(,)로 구분한다.

``` java
void method1() throws Exception1, Exception2, ... , ExceptionN {
	// 메소드의 내용
}
```

> 예외를 발생시키는 키워드 throw와 예외를 메소드에 선언할 때 쓰이는 throws를 잘 구분해야 한다.

만일 아래와 같이 모든 예외의 최고조상인 `Exception`클래스를 메소드에 선언하면, 이 메소드는 모든 종류의 예외가 발생할 가능성이 있다는 뜻이다.

``` java
void method() throws Exception {
	// 메소드의 내용
}
```

이렇게 예외를 선언하면, 이 예외뿐만 아니라 그 자손타입의 예외까지도 발생할 수 있다. 오버라이딩할 떄는 단순히 선언된 예외의 개수가 아니라 상속관계까지 고려해야 한다.

메소드의 선언부에 예외를 선언함으로써 메소드를 사용하려는 사람이 메소드의 선언부를 보았을 때, 이 메소드를 사용하기 위해서는 어떠한 예외들이 처리되어져야 하는지 쉽게 알 수 있다.

메소드에 예외를 선언할 때 일반적으로 `RuntimeException`클래스들은 적지 않는다. 이 들을 메소드 선언부의 `throws`에 선언한다고 해서 문제가 되지는 않지만, 보통 반드시 처리해주어야 하는 예외들만 선언한다.

사실 예외를 메소드의 `throws`에 명시하는 것은 예외를 처리하는 것이 아니라, 자신(예외가 발생할 가능성이 있는 메소드)을 호출한 메소드에 예외를 전달하여 예외처리를 떠맡기는 것이다.

예외를 전달받은 메소드가 또 다시 자신을 호출한 메소드에게 전달할 수 있으며, 이런 식으로 계속 호출스택에 있는 메소드들을 따라 전달되다가 제일 마지막에 있는 `main`메소드에서도 예외가 처리되지 않으면, `main`메소드마저 종료되어 프로그램이 전체가 종료된다.

예제 8-12 / ch8 / ExceptionEx12.java

``` java
public class ExceptionEx12 {
	public static void main(String[] args) {
		method1();	// 같은 클래스내의 static멤버이므로 객체생성없이 직접 호출가능.
	}	// main의 끝
	
	static void method1() throws Exception {
		method2();
	}	// method1의 끝
	
	static void method2() throws Exception {
		throw new Exception();
	}	// method2의 끝
}
```

```
Exception in thread "main" java.lang.Error: Unresolved compilation problem: 
	Unhandled exception type Exception

	at ExceptionEx12.main(ExceptionEx12.java:3)
```

위의 실행결과를 보면, 프로그램의 실행도중 `java.lang.Exception`이 발생하여 비정상적으로 종료했다는 것과 예외가 발생했을 때 호출스택(call stack)의 내용을 알 수 있다.

위의 결과로부터 다음과 같은 사실을 알 수 있다.

> 1. 예외가 발생했을 때, 모두 3개의 메소드(main, method1, method2)가 호출스택에 있었으며,
> 2. 예외가 발생한 곳은 제일 윗줄에 있는 method2()라는 것과
> 3. main메소드가 method1()을, 그리고 method2()를 호출했다는 것을 알 수 있다.

위의 예제를 보면, `method2()`에서 `throw new Exception();`문장에 의해 예외가 강제적으로 발생했으나 `try-catch`문으로 예외처리를 해주지 않았으므로, `method2()`는 종료되면서 예외를 자신을 호출한 `method1()`에게 넘겨준다. `method1()`에서도 역시 예외처리를 해주지 않았으므로 종료되면서 `main`메소드에게 예외를 넘겨준다.

그러나 `main`메소드에서 조차 예외처리를 해주지 않았으므로 `main`메소드가 종료되어 프로그램이 예외로 인해 비정상적으로 종료되는 것이다.

이처럼 예외가 발생한 메소드에서 예외처리를 하지 않고 자신을 호출한 메소드에게 예외를 넘겨줄 수는 없지만, 이것으로 예외가 처리된 것은 아니고 예외를 단순히 전달만 하는 것이다. 결국 어느 한 곳에서는 반드시 `try-catch`문으로 예외처리를 해주어야 한다.

예제 8-13 / ch8 / ExceptionEx13.java

``` java
public class ExceptionEx13 {
	public static void main(String[] args) {
		method1();// 같은 클래스내의 static멤버이므로 객체생성없이 직접 호출가능.
	}	// main메소드의 끝
	
	static void method1() {
		try {
			throw new Exception();
		} catch (Exception e) {
			System.out.println("method1메소드에서 예외가 처리되었습니다.");
			e.printStackTrace();
		}
	}	// method1의 끝
}
```

```
method1메소드에서 예외가 처리되었습니다.
java.lang.Exception
	at ExceptionEx13.method1(ExceptionEx13.java:8)
	at ExceptionEx13.main(ExceptionEx13.java:3)
```

예외는 처리되었지만, `printStackTrace()`를 통해 예외에 대한 정보를 화면에 출력하였다. 예외가 `method1()`에서 발생했으며, `main`메소드가 `method1()`을 호출했음을 알 수 있다.

예제 8-14 / ch8 / ExceptionEx14.java

``` java
public class ExceptionEx14 {
	public static void main(String[] args) {
		try {
			method1();
		} catch (Exception e) {
			System.out.println("main메소드에서 예외가 처리되었습니다.");
			e.printStackTrace();
		}
	}	// main메소드의 끝

	static void method1() throws Exception {
		throw new Exception();
	}	// method1()의 끝
}	// class이 끝
```

```
main메소드에서 예외가 처리되었습니다.
java.lang.Exception
	at ExceptionEx14.method1(ExceptionEx14.java:12)
	at ExceptionEx14.main(ExceptionEx14.java:4)
```

두 예제  모두 `main`메소드가 `method1()`을 호출하며, `method1()`에서 예외가 발생한다. 차이점은 예외처리 방법에 있다.

예제 8-13은 `method1()`에서 예외처리를 했고, 예제 8-14는 `method1()`에서 예외를 선언하여 자신을 호출하는 메소드(`main`메소드)에 예외를 전달했으며, 호출한 메소드(main메소드)에서는 `try-catch`문으로 예외처리를 했다.

예제 8-13처럼 예외가 발생한 메소드(method1)내에서 처리되어지면, 호출한 메소드(main메소드)에서는 예외가 발생했다는 사실조차 모르게 된다.

예제 8-14처럼 예외가 발생한 메소드에서 예외를 처리하지 않고 호출한 메소드로 넘겨주면, 호출한 메소드에서는 `method1()`을 호출한 라인에서 예외가 발생한 것으로 간주되어 이에 대한 처리를 하게 된다.

이처럼 예외가 발생한 메소드 `method1()`에서 예외를 처리할 수도 있고, 예외가 발생한 메소드를 호출한 `main`메소드에서 처리할 수도 있다. 또는 두 메소드가 예외처리를 분담할 수도 있다.

예제 8-15 / ch8 / ExceptionEx15.java

``` java
import java.io.File;

public class ExceptionEx15 {
	public static void main(String[] args) {
		// command line에서 입력받은 값을 이름으로 갖는 파일을 생성한다.
		File f = createFile(args[0]);
		System.out.println(f.getName() + " 파일이 성공적으로 생성되었습니다.");
	}	// main의 끝
	
	static File createFile(String fileName) {
		try {
			if (fileName == null || fileName.equals("")) {
				throw new Exception("파일이름이 유효하지 않습니다.");
			} 
		} catch (Exception e) {
				// fileName이 부적절한 경우, 파일 이름을 '제목없듬.tx'로 한다.
				fileName = "제목없음.txt";
		} finally {
			File f = new File(fileName);	// File클래스의 객체를 만든다.
			createNewFile(f);	// 생성된 객체를 이용해서 파일을 생성한다.
			return f;
		}	// createFile메소드의 끝
	}
	
	static void createNewFile(File f) {
		try {
			f.createNewFile();	// 파일을 생성한다.
		} catch (Exception e) { }
	}	// createNewFile메소드의 끝
}
```

```
C:\jdk1.8\work\ch8>java ExcetionEx15 "test.txt"
test.txt 파일이 성공적으로 생성되었습니다.

C:\jdk1.8\work\ch8>java Exception15 ""
제목없음.txt 파일이 성공적으로 생성되었습니다.

C:\jdk1.8\work\ch8>dir *.txt

드라이브 C에 레이블이 없습니다
볼륨 일련 번호 251C-08DD
디렉터리 C:\jdk1.8\work\ch8

제목없음 TXT 0 15-12-04 0:47 제목없음.txt
TEST TXT 0 05-12-04 0:47 test.txt
```

이 예제는 예외가 발생한 메소드에서 직접 예외를 처리하도록 되어 있다. `creatFile`메소드를 호출한 `main`메소드에서는 예외가 발생한 사실을 알지 못한다. 적절하지 못한 파일이름(fileName)이 입력되면, 예외를 발생시키고, `catch`블럭에서, 파일이름을 '제목없음.txt'로 설정해서 파일을 생성한다. 그리고 `finally`블럭에서는 예외의 발생여부에 관계없이 파일을 생성하는 일을 한다.

예제 8-16 / ch8 / ExceptionEx16.java

``` java
import java.io.File;

public class ExceptionEx16 {
	public static void main(String[] args) {
		try {
			File f = createFile(args[0]);
			System.out.println(f.getName() + "파일이 성공적으로 생성되었습니다.");
		} catch (Exception e) {
			System.out.println(e.getMessage() + "다시 입력해 주시기 바랍니다.");
		}
	}	// main메소드의 끝
	
	static File createFile(String fileName) throws Exception {
		if(fileName == null || fileName.equals("")) {
			throw new Exception("파일이름이 유효하지 않습니다.");
		}
		File f = new File(fileName);	// File클래스의 객체를 만든다.
		// File객체의 createNewFile메소드를 이용해서 실제 파일을 생성한다.
		f.createNewFile();
		return f;	// 생성된 객체의 참조를 반환한다.
	}	// createFile메소드의 끝
}	// 클래스의 끝
```

```
C:\jdk1.8\work\ch8>java ExceptionEx22 test2.txt
test2.txt파일이 성공적으로 생성되었습니다.

C:\jdk1.8\work\ch8>java ExceptionEx22 ""
파일이름이 유효하지 않습니다. 다시 입력해 주시기 바랍니다.
```

이 예제에서는 예외가 발생한 `createFile`메소드에서 잘못 입력된 파일이름을 임의로 처리하지 않고, 호출한 `main`메소드에게 예외가 발생했음을 알려서 파일이름을 다시 입력 받도록 하였다.

예제 8-15와는 달리 `createFile`메소드에 예외를 선언했기 때문에, `File`클래스의 `createNewFile()`에 대한 예외처리를 하지 않아도 되므로 `createNewFile(File f)`메소드를 굳이 따로 만들지 않았다. 두 예제 모두 커맨드라인으로부터 파일이름을 입력 받아서 파일을 생성하는 일을 하며, 파일 이름을 잘못 입력했을 때(null 또는 빈 문자열일 때) 예외가 발생하도록 되어 있다.

차이점은 예외의 처리방법에 있다. 예제 8-15는 예외가 발생한 `createFile`메소드 자체내에서 처리를 하며, 예제 8-16은 `createFile`메소드를 호출한 메소드(main메소드)에서 처리한다.

이처럼 예외가 발생한 메소드 내에서 자체적으로 처리해도 되는 것은 메소드 내에서 `try-catch`문을 사용해서 처리하고, 두 번째 예제처럼 메소드에 호출 시 넘겨받아야 할 값(fileName)을 다시 받아야 하는 경우(메소드 내에서 자체적으로 해결이 안되는 경우)에는 예외를 메소드에 선언해서, 호출한 메소드에서 처리해야한다.

</br>

## 1.8 finally블럭

`finally`블럭은 예외의 발생여부에 상관없이 실행되어야할 코드를 포함시킬 목적으로 사용된다. `try-catch`문의 끝에 선택적으로 덧붙여 사용할 수 있으며, `try-catch-finally`의 순서로 구성된다.

``` java
try {
	// 예외가 발생할 가능성이 있는 문장들을 넣는다.
} catch(Exception e1) {
	// 예외처리를 위한 문장을 적는다.
} finally {
	// 예외의 발생여부에 관계없이 항상 수행되어야하는 문장들을 넣는다.
	// finally블럭은 try-catch문의 맨 마지막에 위치해야한다.
}
```

예외가 발생한 경우에는 'try → catch → finally'의 순으로 실행되고, 예외가 발생하지 않은 경우에는 'try → finally'의 순으로 실행된다.

예제 8-17 / ch8 / FinallyTest.java

``` java
public class FinallyTest {
	public static void main(String[] args) {
		try {
			startInstall();	// 프로그램 설치에 필요한 준비를 한다.
			copyFiles(); // 파일들을 복사한다.
			deleteTempFiles();	// 프로그램 설치에 사용된 임시파일들을 삭제한다.
		} catch (Exception e) {
			e.printStackTrace();
			deleteTempFiles();	// 프로그램 설치에 사용된 임시파일들을 삭제한다.
		}	// try-catch의 끝
	}	// main의 끝
	
	static void startInstall() {
		/* 프로그램 설치에 필요한 준비를 하는 코드를 적는다. */
	}
	static void copyFiles() { /* 파일들을 복사하는 코드를 적는다. */ }
	static void deleteTempFiles() { /* 임시파일들을 삭제하는 코드를 적는다. */ }
}
```

이 예제가 하는 일은 프로그램설치를 위한 준비를 하고 파일들을 복사하고 설치가 완료되면, 프로글매을 설치하는데 사용된 임시파일들을 삭제하는 순서로 진행된다.

프로그램의 설치과정 중에 예외가 발생하더라도, 설치에 사용된 임시파일들이 삭제되도록 `catch`블럭에 `deleteTempFiles()`메소드를 넣었다.

결국 try블럭의 문장을 수행하는 동안에(프로그램을 설치하는 과정에), 예외의 발생여부에 관계없이 `deleteTempFiles()`메소드는 실행되어야 하는 것이다.

이럴 때 finally블럭을 사용하면 좋다. 아래의 코드는 위의 예제를 finally블럭을 사용해서 변경한 것이며, 두 예제의 기능은 동일하다.

예제 8-18 / ch8 / FinallyTest2.java

``` java
public class FinallyTest2 {
	public static void main(String[] args) {
		try {
			startInstall();	// 프로그램 설치에 필요한 준비를 한다.
			copyFiles();	// 파일들을 복사한다.
		} catch (Exception e) {
			e.printStackTrace();
		} finally {
			deleteTempFiles();	// 프로그램 설치에 사용된 임시파일들을 삭제한다.
		}	// try-catch의 끝
	}	// main의 끝
	
	static void startInstall() {
		/* 프로그램 설치에 필요한 준비를 하는 코드를 적는다. */
	}
	static void copyFiles()	{ /* 파일들을 복사하는 코드를 적는다. */ }
	static void deleteTempFiles() { /* 임시파일들을 삭제하는 코드를 적는다. */ }
}
```

예제 8-19 / ch8 / FinallyTest3.java

``` java
public class FinallyTest3 {
	public static void main(String[] args) {
		// method1()은 static메소드이므로 인스턴스 생성없이 직접 호출이 가능하다.
		FinallyTest3.method1();
		System.out.println("method1()의 수행을 마치고 main메소드로 돌아왔습니다.");
	}	// main메소드의 끝
	
	static void method1() {
		try {
			System.out.println("method1()이 호출되었습니다.");
			return;	// 현재 실행 중인 메소드를 종료한다.
		} catch (Exception e) {
			e.printStackTrace();
		} finally {
			System.out.println("method1()의 finally블럭이 실행되었습니다.");
		}
	}	// method1메소드의 끝
}
```

```
method1()이 호출되었습니다.
method1()의 finally블럭이 실행되었습니다.
method1()의 수행을 마치고 main메소드로 돌아왔습니다.
```

위의 결과에서 알 수 있듯이, try블럭에서 return문이 실행되는 경우에도 finally블럭의 문장들이 먼저 실행된 후에, 현재 실행 중인 메소드를 종료한다.

이와 마찬가지로 catch블럭의 문장 수행 중에 return문을 만나도 finally블럭의 문장들은 수행된다.

</br>

## 1.9 자동 자원 반환 - try-with-resources문

JDK1.7부터 try-with-resources문이라는 try-catch문의 변형이 새로 추가되었다.

주로 입출력에 사용되는 클래스 중에서는 사용한 후에 꼭 닫아 줘야 하는 것들이 있다. 그래야 사용했던 자원(resources)이 반환되기 때문이다.

``` java
try {
	fis = new FileInputStream("score.dat");
	dis = new DataInputStream(fis);
		...
} catch(IOException ie) {
	ie.printStackTrace();
} finally {
	dis.close();	// 작업 중에 예외가 발생하더라도, dis가 닫히도록 finally블럭에 넣음
}
```

위의 코드는 `DataInputStream`을 사용해서 파일로부터 데이터를 읽는 코드인데, 데이터를 읽는 도중에 예외가 발생하더라도 `DataInputStream`이 닫히도록 finally블럭 안에 `close()`를 넣었다. 여기까지는 별 문제가 없어 보이는데, 진짜 문제는 `close()`가 예외를 발생시킬 수 있다는데 있다. 그래서 위의 코드는 아래와 같이 해야 올바른 것이 된다.

``` java
try {
	fis = new FileInputStream("score.dat");
	dis = new DataInputStream(fis);
		...
} catch(IOException ie) {
	ie.printStackTrace();
} finally {
	try {
		if(dis != null) dis.close();
	} catch(IOException ie) {
		ie.printStackTrace();
	}
}
```

finally블럭 안에 `try-catch`문을 추가해서 `close()`에서 발생할 수 있는 예외를 처리하도록 변경했는데, 코드가 복잡해져서 별로 보기에 좋지 않다. 더 나쁜 것은 try블럭과 finally블럭에서 모두 예외가 발생하면, try블럭의 예외는 무시된다는 것이다.

이러한 점을 개선하기 위해서 try-with-resources문이 추가된 것이다. 위의 코드를 try-with-resources문으로 바꾸면 다음과 같다.

``` java
// 괄호() 안에 두 문장 이상 넣을 경우 ';'로 구분한다.
try(FileInputStream fis = new FileInputStream("score.dat"); DataInputStream dis = new DataInputStream(fis)) {

	while(true) {
		score = dis.readInt();
		System.out.println(score);
		sum += score;
	}
} catch(EOFException e) {
	System.out.println("점수의 총합은 " + sum + "입니다.");
} catch(IOException ie) {
	ie.printStackTrace();
}
```

try-with-resources문의 괄호()안에 객체를 생성하는 문장을 넣으면, 이 객체는 따로 `close()`를 호출하지 않아도 try블럭을 벗어나는 순간 자동적으로 `close()`가 호출된다. 그 다음에 catch블럭 또는 finally블럭이 수행된다.

> try블럭의 괄호()안에 변수를 선언하는 것도 가능하며, 선언된 변수는 try블럭 내에서만 사용할 수 있다.

이처럼 try-with-resources문에 의해 자동으로 객체의 `close()`가 호출될 수 있으려면, 클래스가 `AutoCloseable`이라는 인터페이스를 구현한 것이어야만 한다.

``` java
public interface AutoCloseable {
	void close() throws Exception;
}
```

위의 인터페이스는 각 클래스에 적절히 자원 반환작업을 하도록 구현되어 있다. 그런데, 위의 코드를 잘 보면 `close()`도 `Exception`을 발생시킬 수 있다.

예제 8-20 / ch8 / TryWithResourceEx.java

``` java
class CloseableResource implements AutoCloseable {
	public void exceptionWork(boolean exception) throws WorkException {
		System.out.println("exceptionWork("+ exception+")가 호출됨");
		
		if(exception) throw new WorkException("WorkException발생.");
	}
	
	public void close() throws CloseException {
		System.out.println("close()가 호출됨");
		throw new CloseException("CloseException발생.");
	}
}

class WorkException extends Exception {
	WorkException(String msg) { super(msg); }
}

class CloseException extends Exception {
	CloseException(String msg) { super(msg); }
}

public class TryWithResourceEx {
	public static void main(String[] args) {
		try(CloseableResource cr = new CloseableResource()) {
			cr.exceptionWork(false);	// 예외가 발생하지 않는다.
		} catch (WorkException e) {
			e.printStackTrace();
		} catch (CloseException e) {
			e.printStackTrace();
		}
		System.out.println();
		
		try(CloseableResource cr = new CloseableResource()) {
			cr.exceptionWork(true);	// 예외가 발생한다.
		} catch (WorkException e) {
			e.printStackTrace();
		} catch (CloseException e) {
			e.printStackTrace();
		}
	}	// main의 끝
}
```

```
exceptionWork(false)가 호출됨
close()가 호출됨
CloseException: CloseException발생.

	at CloseableResource.close(TryWithResourceEx.java:10)
	at TryWithResourceEx.main(TryWithResourceEx.java:26)
exceptionWork(true)가 호출됨
close()가 호출됨
WorkException: WorkException발생.
	at CloseableResource.exceptionWork(TryWithResourceEx.java:5)
	at TryWithResourceEx.main(TryWithResourceEx.java:34)
	Suppressed: CloseException: CloseException발생.
		at CloseableResource.close(TryWithResourceEx.java:10)
		at TryWithResourceEx.main(TryWithResourceEx.java:35)
```

`main`메소드에 두 개의 try-catch문이 있는데, 첫 번째 것은 `close()`에서만 예외를 발생시키고, 두 번째 것은 `exceptionWork()`와 `close()`에서 모두 예외를 발생시킨다.

첫 번째는 일반적인 예외가 발생했을 때와 같은 형태로 출력되었지만, 두 번째는 출력형태가 다르다. 먼저 `exceptionWork()`에서 발생한 예외에 대한 내용이 출력되고, `close()`에서 발생한 예외는 '억제된(suppressed)'이라는 의미의 머리말과 함께 출력되었다.

두 예외가 동시에 발생할 수는 없기 때문에, 실제 발생한 예외를 `WorkException`으로 하고, `CloseException`은 억제된 예외로 다룬다. 억제된 예외에 대한 정보는 실제로 발생한 예외인 `WorkException`에 저장된다.
`Throwable`에는 억제된 예외와 관련된 다음과 같은 메소드가 정의되어 있다.

> **void addSuppressd(Throwable exception)** 억제된 예외를 추가
> **Throwable[] getSuppressed()** 억제된 예외(배열)를 반환

만일 기존의 try-catch문을 사용했다면, 먼저 발생한 `WorkException`은 무시되고, 마지막으로 발생한 `CloseException`에 대한 내용만 출력되었을 것이다.

</br>

## 1.10 사용자정의 예외 만들기

기존의 정의된 예외 클래스 외에 필요에 따라 프로그래머가 새로운 예외 클래스를 정의하여 사용할 수 있다. 보통 `Exception`클래스 또는 `RuntimeException`클래스로부터 상속받아 클래스를 만들지만, 필요에 따라 알맞은 예외 클래스를 선택할 수 있다.

``` java
class MyException extends Exception {
	MyException(String msg) {	// 문자열을 매겨변수로 받는 생성자
		super(msg);	// 조상인 Exception클래스의 생성자를 호출한다.
	}
}
```

`Exception`클래스로부터 상속받아서 `MyException`클래스를 만들었다. 필요하다면, 멤버 변수나 메소드를 추가할 수 있다. `Exception`클래스는 생성 시에 `String`값을 받아서 메세지로 저장할 수 있다. 여러분이 만든 사용자정의 예외 클래스도 메세지를 저장할 수 있으려면, 위에서 보는 것과 같이 `String`을 매개변수로 받는 생성자를 추가해주어야 한다.

``` java
class MyException extends Exception {
	// 에러 코드 값을 저장하기 위한 필드를 추가했다.
	private final int ERR_CODE;	// 생성자를 통해 초기화 한다.

	MyException(String msg, int errCode) {	// 생성자
		super(msg);
		ERR_CODE = errCode;
	}

	MyException(String msg) {	// 생성자
		this(msg, 100);	// ERR_CODE를 100(기본값)으로 초기화한다.
	}

	public int getErrCode() {	// 에러 코드를 얻을 수 있는 메소드도 추가했다.
		return ERR_CODE;	// 이 메소드는 주로 getMessage()와 함께 사용될 것이다.
	}
}
```

이전의 코드를 좀 더 개선하여 메세지뿐만 아니라 에러코드 값도 저장할 수 있도록 `ERR_CODE`와 `getErrCode()`를 `MyException`클래스의 멤버로 추가했다. 이렇게 함으로써 `MyException`이 발생했을 때, catch블럭에서 `getMessage()`와 `getErrCode()`를 사용해서 에러코드와 메세지를 모두 얻을 수 있다.

기존의 예외 클래스는 주로 `Exception`을 상속받아서 'checked예외'로 작성하는 경우가 많았지만, 요즘은 예외처리를 선택적으로 할 수 있도록 `RuntimeException`을 상속받아서 작성하는 쪽으로 바뀌어가고 있다. 'checked예외'는 반드시 예외처리를 해주어야 하기 때문에 예외처리가 불필요한 경우에도 try-catch문을 넣어서 코드가 복잡해지기 때문이다.

예제 8-21 / ch8 / NewExceptionTest.java

``` java
class SpaceException extends Exception {
	SpaceException(String msg) {
		super(msg);
	}
}

class MemoryException extends Exception {
	MemoryException(String msg) {
		super(msg);
	}
}

public class NewExceptionTest {
	public static void main(String[] args) {
		try {
			startInstall();	// 프로그램 설치에 필요한 준비를 한다.
			copyFiles();	// 파일들을 복사한다.
		} catch (SpaceException e) {
			System.out.println("에러 메세지 : " + e.getMessage());
			e.printStackTrace();
			System.out.println("공간을 확보한 후에 다시 설치하시기 바랍니다.");
		} catch (MemoryException me) {
			System.out.println("에러 메세지 : " + me.getMessage());
			me.printStackTrace();
			System.gc();	// Garbage Collection을 수행하여 메모리를 늘려준다.
			System.out.println("다시 설치를 시도하세요.");
		} finally {
			deleteTempFiles();	// 프로그램 설치에 사용된 임시파일들을 삭제한다.
		}	// try의 끝
	}	// main의 끝
	
	static void startInstall() throws SpaceException, MemoryException {
		if(!enoughSpace())	// 충분한 설치 공간이 없으면
			throw new SpaceException("설치할 공간이 부족합니다.");
		if(!enoughMemory())	// 충분한 메모리가 없으면
			throw new MemoryException("메모리가 부족합니다.");
	}	// startInstall메소드의 끝
	
	static void copyFiles() { /* 파일들을 복사하는 코드를 적는다. */ }
	static void deleteTempFiles() { /* 임시파일들을 삭제하는 코드를 적는다. */ }
	
	static boolean enoughSpace() {
		// 설치하는데 필요한 공간이 있는지 확인하는 코드를 적는다.
		return false;
	}
	
	static boolean enoughMemory() {
		// 설치하는데 필요한 메모리공간이 있는지 확인하는 코드를 적는다.
		return true;
	}
}	// NewExceptionTest클래스의 끝
```

```
에러 메세지 : 설치할 공간이 부족합니다.
SpaceException: 설치할 공간이 부족합니다.
	at NewExceptionTest.startInstall(NewExceptionTest.java:34)
	at NewExceptionTest.main(NewExceptionTest.java:16)
공간을 확보한 후에 다시 설치하시기 바랍니다.
```

`MemoryException`과 `SpaceException`, 이 두 개의 사용자정의 예외 클래스를 새로 만들어서 사용했다 `SpaceException`은 프로그램을 설치하려는 곳에 충분한 공간이 없을 경우에 발생하도록 했으며, `MemoryException`은 설치작업을 수행하는데 메모리가 충분히 확보되지 않았을 경우에 발생하도록 하였다.

이 두 예외는 `startInstall()`을 수행하는 동안에 발생할 수 있으며, `enoughSpace()`와 `enoughMemory()`의 실행결과에 따라서 발생하는 예외의 종류가 달리지도록 했다.

</br>

## 1.11 예외 되던지기(exception re-throwing)

한 메소드에서 발생할 수 있는 예외가 여럿인 경우, 몇 개는 try-catch문을 통해서 메소드 내에서 자체적으로 처리하고, 그 나머지는 선언부에 지정하여 호출한 메소드에서 처리하도록 함으로써, 양쪽에서 나눠서 처리되도록 할 수 있다.

그리고 심지어는 단 하나의 예외에 대해서도 예외가 발생한 메소드와 호출한 메소드, 양쪽에서 처리하도록 할 수 있다.

이것은 예외를 처리한 후에 인위적으로 다시 발생시키는 방법을 통해서 가능한데, 이것을 '예외 되던지기(exception re-throwing)'라고 한다.

먼저 예외가 발생할 가능성이 있는 메소드에서 try-catch문을 사용해서 예외를 처리해주고 catch문에서 필요한 작업을 행한 후에 throw문을 사용해서 예외를 다시 발생시킨다. 다시 발생한 예외는 이 메소드를 호출한 메소드에게 전달되고 호출한 메소드의 try-catch문에서 예외를 또다시 처리한다.

이 방법은 하나의 예외에 대해서 예외가 발생한 메솓와 이를 호출한 메소드 양쪽 모두에서 처리해줘야 할 작업이 있을 때 사용된다. 이 때 주의할 점은 예외가 발생할 메소드에서는 try-catch문을 사용해서 예외처리를 해줌과 동시에 메소드의 선언부에 발생한 예외를 `throws`에 지정해줘야 한다.

예제 8-22 / ch8 / ExceptionEx17.java

``` java
public class ExceptionEx17 {
	public static void main(String[] args) {
		try {
			method1();
		} catch (Exception e) {
			System.out.println("main메소드에서 예외가 처리되었습니다.");
		}
	}	// main메소드의 끝
	
	static void method1() throws Exception {
		try {
			throw new Exception();
		} catch (Exception e) {
			System.out.println("method1메소드에서 예외가 처리되었습니다.");
			throw e;	// 다시 예외를 발생시킨다.
		}
	}	// method1메소드의 끝
}
```

```
method1메소드에서 예외가 처리되었습니다.
main메소드에서 예외가 처리되었습니다.
```

결과에서 알 수 있듯이 `method1()`과 `main`메소드 양쪽의 catch블럭이 모두 수행되었음을 알 수 있다. `method1()`의 catch블럭에서 예외를 처리하고도 throw문을 통해 다시 예외를 발생 시켰다. 그리고 이 예외를 `main`메소드 한 번 더 처리하였다.

반환값이 있는 return문의 경우, catch블럭에도 return문이 있어야 한다. 예외가 발생했을 경우에도 값을 반환해야하기 때문이다.

``` java
static int method1() {
	try {
		System.out.println("method1()이 호출되었습니다.");
		return 0;	// 현재 실행 중인 메소드를 종료한다.
	} catch(Exception e) {
		e.printStackTrace();
		return 1;	// catch블럭 내에도 return문이 필요하다.
	} finally {
		System.out.println("method1()의 finally블럭이 실행되었습니다.");
	}
}	// method1메소드의 끝
```

또는 catch블럭에서 예외 되던지기를 해서 호출한 메소드로 예외를 전달하면, return문이 없어도 된다. 그래서 검증에서도 assert문 대신 AssertError를 생성해서 던진다.

``` java
static int method1() throws Exception {	// 예외를 선언해야 함
	try {
		System.out.println("method1()이 호출되었습니다.");
		return 0;	// 현재 실행 중인 메소드를 종료한다.
	} catch(Exception e) {
		e.printStackTrace();
		// return 1;	// catch블럭 내에도 return문이 필요하다.
		throw new Exception();	// return문 대신 예외를 호출한 메소드로 전달
	} finally {
		System.out.println("method1()의 finally블럭이 실행되었습니다.");
	}
}	// method1메소드의 끝
```

> finally블럭 내에도 return문을 사용할 수 있으며, try블럭이나 catch블럭의 retun문 다음에 수행된다. 최종적으로 finally블럭 내의 return문의 값이 반환된다.

</br>

## 1.12 연결된 예외(chained exception)

한 예외가 다른 예외를 발생시킬 수도 있다. 예를 들어 예외 A가 예외 B를 발생시켰다면, A를 B의 '원인 예외(cause exception)'라고 한다. 아래의 코드는 예제 8-21의 일부를 변경한 것으로, `SpaceException`을 원인 예외로 하는 `InstallException`을 발생시키는 방법을 보여준다.

``` java
try {
	startInstall();	// SpaceException 발생
	copyFiles();
} catch(SpaceException e) {
	InstallException ie = new InstallException("설치중 예외발생");	// 예외 생성
	ie.initCause(e);	// InstallException의 원인 예외를 SpaceException으로 지정
	throw ie;	// InstallException을 발생시킨다.
} catch(MemoryException me) {
	...
}
```

먼저 `InstallException`을 생성한 후에, `initCause()`로 `SpaceException`을 `InstallException`의 원인 예외로 등록한다. 그리고 `throw`로 이 예외를 던전다.

`initCause()`는 `Exception`클래스의 조상인 `Throwable`클래스에 정의되어 있기 때문에 모든 예외에서 사용가능하다.

> **Throwable initCause(Throwable cause) 지정한 예외를 원인 예외로 등록**
> **Throwable getCause() 원인 예외를 반환**

원인 예외로 등록해서 다시 예외를 발생시키는 이유는 여러가지 예외를 하나의 큰 분류의 예외로 묶어서 다루기 위해서이다.

그렇다고 아래와 같이 `InstallException`을 `SpaceException`과 `MemoryException`의 조상으로 해서 catch블럭을 작성하면, 실제로 발생한 예외가 어떤 것이닞 알 수 없다는 문제가 생긴다. 그리고 `SpaceException`과 `MemoryException`의 상속관계를 변경해야 한다는 것도 부담이다.

``` java
try {
	startInstall();	// SpaceException 발생
	copyFiles();
} catch(InstallException e) {	// InstallException은
	e.printStackTrace();	// SpaceException과 MemoryException의 조상
}
```

그래서 생각한 것이 예외가 원인 예외를 포함할 수 있게 한 것이다. 이렇게 하면, 두 예외는 상속관계가 아니어도 상관없다.

``` java
public class Throwable implements Serializable {
		...
	private Throwable cause = this;	// 객체 자신(this)을 원인 예외로 등록
		...
}
```

또 다른 이유는 checked예외를 unchecked예외로 바꿀 수 있도록 하기 위해서이다.

checked예외를 unchecked예외로 바꾸면 예외처리가 선택적이 되므로 억지로 예외처리를 하지 않아도 된다.

``` java
static void startInstall() throws SpaceException, MemoryException {
	if(!enoughSpace())	// 충분한 설치 공간이 없으면
		throw new SpaceException("설치할 공간이 부족합니다.");
	
	if(!enoughMemory())	// 충분한 메모리가 없으면
		throw new MemoryException("메모리가 부족합니다.");
}
```

``` java
static void startInstall() throws SpaceException {
	if(!enoughSpace())	// 충분한 설치 공간이 없으면
		throw new SpaceException("설치할 공간이 부족합니다.");
	
	if(!enoughMemory())	// 충분한 메모리가 없으면
		throw new RuntimeException (new MemoryException("메모리가 부족합니다."));
}	// startInstall메소드의 끝
```

`MemoryException`은 `Exception`의 자손이므로 반드시 예외를 처리해야하는데, 이 예외를 `RuntimeException`으로 감싸버렸기 때문에 unchecked예외가 되었다. 그래서 더 이상 `startInstall()`의 선언부에 `MemoryException`을 선언하지 않아도 된다. 참고로 위의 코드에서는 `initCause()`대신 `RuntimeException`의 생성자를 사용했다.

``` java
RuntimeException(Throwable cause)	// 원인 예외를 등록하는 생성자
```

예제 8-23 / ch8 / ChainedExceptionEx.java

``` java
class InstallException extends Exception {
	InstallException(String msg) {
		super(msg);
	}
}

class SpaceException extends Exception {
	SpaceException(String msg) {
		super(msg);
	}
}

class MemoryException extends Exception {
	MemoryException(String msg) {
		super(msg);
	}
}

public class ChainedExceptionEx {
	public static void main(String[] args) {
		try {
			install();
		} catch (InstallException e) {
			e.printStackTrace();
		} catch (Exception e) {
			e.printStackTrace();
		}
	}	// main의 끝
	
	static void install() throws InstallException {
		try {
			startInstall();	// 프로그램 설치에 필요한 준비를 한다.
			copyFiles();	// 파일들을 복사한다.
		} catch (SpaceException se) {
			InstallException ie = new InstallException("설치 중 예외발생");
			ie.initCause(se);
			throw ie;
		} catch (MemoryException me) {
			InstallException ie = new InstallException("설치 중 예외발생");
			ie.initCause(me);
			throw ie;
		} finally {
			deleteTempFiles();	// 프로그램 설치에 사용된 임시파일들을 삭제한다.
		}	// try의 끝
	}
	
	static void startInstall() throws SpaceException, MemoryException {
		if(!enoughSpace()) {	// 충분한 설치 공간이 없으면
			throw new SpaceException("설치할 공간이 부족합니다.");
		}
		
		if(!enoughMemory()) {	// 충분한 메모리가 없으면
			throw new MemoryException("메모리가 부족합니다.");
//			throw new RuntimeException(new MemoryException("메모리가 부족합니다."));
		}
	}
	
	static void copyFiles() { /* 파일들을 복사하는 코드를 적는다. */ }
	static void deleteTempFiles() { /* 임시파일들을 삭제하는 코드를 적는다. */ }
	
	static boolean enoughSpace() {
		// 설치하는데 필요한 공간이 있는지 확인하는 코드를 적는다.
		return false;
	}
	
	static boolean enoughMemory() {
		// 설치하는데 필요한 메모리공간이 있는지 확인하는 코드를 적는다
		return true;
	}
}	// ExceptionTest클래스의 끝
```

```
InstallException: 설치 중 예외발생
	at ChainedExceptionEx.install(ChainedExceptionEx.java:35)
	at ChainedExceptionEx.main(ChainedExceptionEx.java:22)
Caused by: SpaceException: 설치할 공간이 부족합니다.
	at ChainedExceptionEx.startInstall(ChainedExceptionEx.java:49)
	at ChainedExceptionEx.install(ChainedExceptionEx.java:32)
	... 1 more
```