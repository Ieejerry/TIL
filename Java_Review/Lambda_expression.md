Chapter 14. 람다와 스트림

# 1. 람다식(Lambda expression)

</br>

## 1.1 람다식이란?

람다식(Lambda expression)은 간단히 말해서 메소드를 하나의 '식(expression)'으로 표현한 것이다. 람다식은 함수를 간략하면서도 명확한 식으로 표현할 수 있게 해준다.

메소드를 람다식으로 표현하면 메소드의 이름과 반환값이 없어지므로, 람다식을 '익명 함수(anonymous function)'이라고도 한다.

``` java
int[] arr = new int[5];
Arrays.setAll(arr, (i) -> (int)(Math.random() * 5) + 1);
```

위의 문장에서 `() -> (int)(Math.random() * 5) + 1`이 바로 람디식이다. 이 람다식이 하는 일을 메소드로 표현하면 다음과 같다.

``` java
int method() {
    return (int)(Math.random() * 5) + 1;
}
```

위의 메소드보다 람다식이 간결하면서도 이해하기 쉽다. 게다가 모든 메소드는 클래스에 포함되어야 하므로 클래스도 새로 만들어야 하고, 객체도 생성해야만 비로소 이 메소드를 호출할 수 있다. 그러나 람다식은 이 모든 과정없이 오직 람다식 자체만으로도 이 메소드의 역할을 대신할 수 있다.

게다가 람다식은 메소드의 매개변수로 전달되어지는 것이 가능하고, 메소드의 결과로 반환할 수도 있다. 람다식으로 인해 메소드를 변수처럼 다루는 것이 가능해진 것이다.

</br>

## 1.2 람다식 작성하기

람다식은 '익명 함수'답게 메소드에서 이름과 반환타입을 제거하고 매개변수 선언부와 몸통{} 사이에 `->`를 추가한다.

![image](https://ifh.cc/g/dWzvza.png)

예를 들어 두 값중에 큰 값을 반환하는 메소드 `max`를 람다식으로 변환하면, 아래의 오른쪽과 같이 된다.

![image](https://ifh.cc/g/MLsyDm.png)

반환값이 있는 메소드의 경우, return문 대신 '식(expression)'으로 대신할 수 있다. 식의 연산결과가 자동적으로 반환값이 된다. 이때는 '문장(statement)'이 아닌 '식'이므로 끝에 `;`를 붙이지 않는다.

![image](https://ifh.cc/g/4kGShG.png)

람다식에 선언된 매겨변수의 타입은 추론이 가능한 경우는 생략할 수 있는데, 대부분의 경우에 생략가능하다. 람다식에 반환타입이 없는 이유도 항상 추론이 가능하기 때문이다.

![image](https://ifh.cc/g/csQY22.png)

> '(int a, b) -> a > b ? a : b'와 같이 두 매개변수 중 어느 하나의 타입만 생략하는 것은 허용되지 않는다.

아래와 같이 선언된 매개변수가 하나뿐인 경우에는 괄호()를 생략할 수 있다. 단, 매개변수의 타입이 있으면 괄호()를 생략할 수 없다.

![image](https://ifh.cc/g/aGvClo.png)

마찬가지로 괄호{} 안의 문장이 하나일 때는 괄호{}를 생략할 수 있다. 이 때 문장의 끝에 `;`을 붙이지 않아야 한다.

![image](https://ifh.cc/g/K1YGL2.png)

그러나 괄호{} 안의 문장이 return문일 경우 괄호{}를 생략할 수 없다.

``` java
(int a, int b) -> { return a > b ? a : b; } // OK
(int a, int b) -> return a > b ? a : b  // 에러
```

아래의 표는 메소드를 람다식으로 변환하여 보여준다.

![image](https://ifh.cc/g/Q9bJrN.png)

</br>

## 1.3 함수형 인터페이스(Functional Interface)

자바에서 모든 메소드는 클래스 내에 포함되어야 하는데, 람다식은 익명 클래스의 객체와 동일하다.

![image](https://ifh.cc/g/LfRR1l.png)

위의 오른쪽 코드에서 메소드 이름 `max`는 임의로 붙인 것일 뿐 의미는 없다. 람다식으로 저으이된 익명 객체의 메소드는 참조변수가 있어야 객체의 메소드를 호출할 수 있으니 이 익명 객체의 주소를 `f`라는 참조변수에 저장하겠다.

> 타입 f = (int a, int b) -> a > b ? a : b; // 참조변수의 타입은?

참조변수 `f`의 타입은 참조형이니 클래스 또는 인터페이스가 가능하다. 그리고 람다식과 동등한 메소드가 정의되어 있는 것이어야 한다. 그래야만 참조변수로 익명 객체(람다식)의 메소드를 호출할 수 있기 때문이다.

예를 들어 아래와 같이 `max()`라는 메소드가 정의된 `MyFunction`인터페이스가 정의되어 있다고 가정하겠다.

``` java
interface MyFunction() {
    public abstract int max(int a, int b);
}
```

그러면 이 인터페이스를 구현한 익명 클래스의 객체는 다음과 같이 생성할 수 있다.

``` java
MyFunction f = new MyFunction() {
                    public int max(int a, int b) {
                        return a > b ? a : b;
                    }
                };

int big = f.max(5, 3);  // 익명 객체의 메소드를 호출
```

`MyFunction`인터페이스에 정의된 메소드 `max()`는 람다식 `(int a, int b) -> a > b ? a : b`과 메소드의 선언부가 일치한다. 그래서 위 코드의 익명 객체를 람다식으로 아래와 같이 대체할 수 있다.

``` java
MyFunction f = (int a, int b) -> a > b ? a : b; // 익명 객체를 람다식으로 대체
int big = f.max(5, 3);  // 익명 객체의 메소드를 호출
```

이처럼 `MyFunction`인터페이스를 구현한 익명 객체를 람다식으로 대체가 가능한 이유는 람다식도 실제로는 익명 객체이고, `MyFunction`인터페이스를 구현한 익명 객체의 메소드 `max()`와 람다식의 매개변수의 타입과 개수 그리고 반환값이 일치하기 때문이다.

람다식을 다루기 위한 인터페이스를 '함수형 인터페이스(functional interface)'라고 한다.

``` java
@FunctionalInterface
interface MyFunction {  // 함수형 인터페이스 MyFunction을 정의
    public abstract int max(int a, int b);
}
```

단, 함수형 인터페이스에는 오직 하나의 추상 메소드만 정의되어 있어야 한다는 제약이 있다. 그래야 람다식과 인터페이스의 메소드가 1:1로 연결될 수 있기 때문이다. 반면에 static메소드와 default메소드의 개수에는 제약이 없다.

> '@FunctionalInterface'를 붙이면, 컴파일러가 함수형 인터페이스를 올바르게 정의하였는지 확인해주므로, 꼭 붙이도록 하는게 좋다.

기존에는 아래와 같이 인터페이스의 메소드 하나를 구현하는데도 복잡하게 해야 했는데,

``` java
List<String> list = Arrays.asList("abc", "bbb", "ddd", "aaa");

Collections.sort(list, new Comparator<String>() {
    public int compare(String s1, String s2) {
        return s2.compareTo(s1);
    }
});
```

이제 람다식으로 아래와 같이 간단히 처리할 수 있게 되었다.

``` java
List<String> list = Arrays.asList("abc", "aaa", "bbb", "ddd", "aaa");
Collections.sort(list, (s1, s2) -> s2.compareTo(s1));
```

</br>

### 함수형 인터페이스 타입의 매개변수와 반환타입

함수형 인터페이스 `MyFunction`이 아래와 같이 정의되어 있을 때,

``` java
@FunctionalInterface
interface MyFunction {
    void myMethod();    // 추상 메소드
}
```

메소드의 매개변수가 `MyFunction`타입이면, 이 메소드를 호출할 때 람다식을 참조하는 참조변수를 매개변수로 지정해야한다는 뜻이다.

``` java
void aMethod(MyFunction f) {
    f.myMethod();
}
        ...
MyFunction f = () -> System.out.println("myMethod()");
aMethod(f);
```

또는 참조변수 없이 아래와 같이 직접 람다식을 매개변수로 지정하는 것도 가능하다.

> aMethod(**() -> System.out.println("myMethod()")**);  // 람다식을 매개변수로 지정

그리고 메소드의 반환타입이 함수형 인터페이스타입이라면, 이 함수형 인터페이스의 추상메소드와 동등한 람다식을 가리키는 참조변수를 반환하거나 람다식을 직접 변환할 수 있다.

``` java
MyFunction myMethod() {
    MyFunction f = () -> {};
    return f;   // 이 줄과 윗 줄을 한 줄로 줄이면, return () -> {};
}
```

람다식을 참조변수로 다룰 수 있다는 것은 메소드를 통해 람다식을 주고받을 수 있다는 것을 의미한다. 즉, 변수처럼 메솓를 주고받는 것이 가능해진다.

사실상 메소드가 아니라 객체를 주고받는 것이라 근본적으로 달리진 것은 아무것도 없지만, 람다식 덕분에 예전보다 코드가 더 간결하고 이해하기 쉬워졌다.

</br>

예제 14-1 / ch14 / LambdaEx1.java

``` java
@FunctionalInterface
interface MyFunction {
	void run();	// public abstract void run();
}

public class LambdaEx1 {
	static void execute(MyFunction f) {	// 매개변수의 타입이 MyFunction인 메소드
		f.run();
	}
	
	static MyFunction getMyFunction() {	// 매개변수의 타입이 MyFunction인 메소드
		MyFunction f = () -> System.out.println("f3.run()");
		return f;
	}
	
	public static void main(String[] args) {
		// 람다식으로 MyFunction의 run()을 구현
		MyFunction f1 = () -> System.out.println("f1.run()");
		
		MyFunction f2 = new MyFunction() {	// 익명클래스로 run()을 구현
			public void run() {	// public을 반드시 붙여야 함
				System.out.println("f2.run()");
			}
		};
		
		MyFunction f3 = getMyFunction();
		
		f1.run();
		f2.run();
		f3.run();
		
		execute(f1);
		execute( () -> System.out.println("run()") );
	}
}
```

```
f1.run()
f2.run()
f3.run()
f1.run()
run()
```

</br>

### 람다식의 타입과 형변환

함수형 인터페이스로 람다식을 참조할 수 있는 것일 뿐, 람다식의 타입이 함수형 인터페이스의 타입과 일치하는 것은 아니다. 람다식은 익명 객체이고 익명 객체는 타입이 없다. 정확히는 타입은 있지만 컴파일러가 임의로 이름을 정하기 때문에 알 수 없는 것이다. 그래서 대입 연산자의 양변의 타입을 일치시키기 위해 아래와 같이 형변환이 필요하다.

``` java
MyFuction f = (MyFunction)(() -> {});   // 양변의 타입이 다르므로 형변환이 필요
```

람다식은 `MyFunction`인터페이스를 직접 구현하지 않았지만, 이 인터페이스를 구현한 클래스의 객체와 완전히 동일하기 때문에 위와 같은 형변환을 허용한다. 그리고 이 형변환은 생략가능하다.

람다식은 이름이 없을 뿐 분명히 객체인데도, 아래와 같이 Object타입을 형변환 할 수 없다. 람다식은 오직 함수형 인터페이스로만 형변환이 가능하다.

``` java
Object obj = (Object)(() -> {});    // 에러. 함수형 인터페이스로만 형변환 가능
```

굳이 Object타입으로 형변환하려면, 먼저 함수형 인터페이스로 변환해야 한다.

``` java
Object obj = (Object)(MyFunction)(() -> {});
String str = ((Object)(MyFunction)(() -> {})).toString();
```

</br>

예제 14-2 / ch14 / LambdaEx2.java

``` java
@FunctionalInterface
interface MyFunction2 {
	void myMethod();	// public abstract void myMethod();
}

public class LambdaEx2 {
	public static void main(String[] args) {
		MyFunction2 f = () -> {};	// MyFunction f = (MyFunction)(() -> {});
		Object obj = (MyFunction2)(() -> {});	// Object타입으로 형변환이 생략됨
		String str = ((Object)(MyFunction2)(() -> {})).toString();
		
		System.out.println(f);
		System.out.println(obj);
		System.out.println(str);
		
//		System.out.println(() -> {});	// 에러. 람다식은 Object타입으로 형변환 안됨
		System.out.println((MyFunction2)(() -> {}));
//		System.out.println((MyFunction2)(() -> {}).toString());	// 에러
		System.out.println(((Object)(MyFunction2)(() -> {})).toString());
	}
}
```

```
LambdaEx2$$Lambda$1/0x0000000800000bf8@6a38e57f
LambdaEx2$$Lambda$2/0x0000000800001000@277c0f21
LambdaEx2$$Lambda$3/0x0000000800001218@e6ea0c6
LambdaEx2$$Lambda$4/0x0000000800001430@43556938
LambdaEx2$$Lambda$5/0x0000000800001648@7a46a697
```

실행결과를 보면, 컴파일러가 람다식의 타입을 어떤 형식으로 만들어내는지 알 수 있다. 일반적인 익명 객체라면, 객체의 타입이 '외부클래스이름$번호'와 같은 형식으로 타입이 결정되었을텐데, 람다식의 타입은 외부클래스이름$$Lambda$번호'와 같은 형식으로 되어있다.

</br>

### 외부 변수를 참조하는 람다식

람다식도 익명 객체, 즉 익명 클래스의 인스턴스이므로 람다식에서 외부에 선언된 변수에 접근하는 규칙은 익명 클래스에서 동일하다. 아래의 예제는 예제 7-35를 람다식을 사용해서 변경한 것이다.

</br>

예제 14-3 / ch14 / LambdaEx3.java

``` java
@FunctionalInterface
interface MyFunction3 {
	void myMethod();
}

class Outer {
	int val = 10;	// Outer.this.val
	
	class Inner {
		int val = 20;	// this.val
		
		void method(int i) {	// void method(final int i) {
			int val = 30;	// final int val = 30;
//			i = 10;	// 에러. 상수의 값을 변경할 수 없음.
			
			MyFunction3 f = () -> {
				System.out.println("i : " + i);
				System.out.println("val : " + val);
				System.out.println("this.val : " + ++this.val);
				System.out.println("Outer.this.val : " + ++Outer.this.val);
			};
			
			f.myMethod();
		}
	}	// Inner클래스의 끝
}	// Outer클래스의 끝

public class LambdaEx3 {
	public static void main(String[] args) {
		Outer outer = new Outer();
		Outer.Inner inner = outer.new Inner();
		inner.method(100);
	}
}
```

```
i : 100
val : 30
this.val : 21
Outer.this.val : 11
```

이 예제는 람다식 내에서 외부에 선언된 변수에 접근하는 방법을 보여준다. 람다식 내에서 참조하는 지역변수는 final이 붙지 않았어도 상수로 간주된다. 람다식 내에서 지역변수 `i`와 `val`을 참조하고 있으므로 람다식 내에서나 다른 어느 곳에서도 이 변수들의 값을 변경하는 일은 허용되지 않는다.

반면에 `Inner`클래스와 `Outer`클래스의 인스턴스 변수인 `this.val`과 `Outer.this.val`은 상수로 간주되지 않으므로 값을 변경해도 된다.

``` java
void method(int i) {	// void method(final int i) {
    int val = 30;	// final int val = 30;
    i = 10;	// 에러1. 상수의 값을 변경할 수 없음.
    
    MyFunction3 f = (i) -> {    // 에러2. 외부 지역변수와 이름이 중복됨.
        System.out.println("i : " + i);
        System.out.println("val : " + val);
        System.out.println("this.val : " + ++this.val);
        System.out.println("Outer.this.val : " + ++Outer.this.val);
    };
```

그리고 외부 지역변수와 같은 이름의 람다식 매개변수는 허용되지 않는다.(에러2)