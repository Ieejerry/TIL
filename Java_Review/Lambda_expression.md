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

</br>

## 1.4 java.util.function패키지

대부분의 메소드는 타입이 비슷하다. 매개변수가 없거나 한 개 또는 두 개, 반환 값은 없거나 한 개. 게다가 제네릭 메소드로 정의하면 매개변수나 반환 타입이 달라도 문제가 되지 않는다. 그래서 `java.util.function`패키지에 일반적으로 자주 쓰이는 형식의 메소드를 함수형 인터페이스로 미리 정의해 놓았다. 매번 새로운 함수형 인터페이스를 정의하지 말고, 가능하면 이 패키지의 인터페이스를 활용하는 것이 좋다.

그래야 함수형 인터페이스를 정의된 메소드 이름도 통일되고, 재사용성이나 유지보수 측면에서도 좋다. 자주 쓰이는 가장 기본적인 함수형 인터페이스는 다음과 같다.

![image](https://ifh.cc/g/xwdm1X.png)

매개변수와 반환값의 유무에 따라 5개의 함수형 인터페이스가 정의되어 있고, `Function`의 변형으로 `Predicate`가 있는데, 반환값이 boolean이라는 것만 제외하면 `Function`과 동일하다. `Predicate`는 조건식을 함수로 표현하는데 사용된다.

> 타입 문자 'T'는 'Type'을, 'R'은 'Return Type'을 의미한다.

</br>

### 조건식의 표현에 사용되는 Predicate

`Predicate`는 `Function`의 변형으로, 반환타입이 boolean이라는 것만 다르다. `Predicate`는 조건식을 람다식으로 표현하는데 사용된다.

> 수학에서 결과로 true 또는 false를 반환하는 함수를 '프레디케이트(predicate)'라고 한다.

``` java
Predicate<String> isEmptyStr = s -> s.length() == 0;
String s = "";

if(isEmptyStr.test(s))  // if(s.length() == 0)
    System.out.println("This is an empty String.");
```

</br>

### 매개변수가 두 개인 함수형 인터페이스

매개변수의 개수가 2개인 함수형 인터페이스는 이름 앞에 접두사 'Bi'가 붙는다.

> 매개변수의 타입으로 보통 'T'를 사용하므로, 알파벳에서 'T'의 타음 문자인 'U', 'V', 'W'를 매개변수의 타입으로 사용하는 것일 뿐 별다른 의미는 없다.

![image](https://ifh.cc/g/Ak87pG.png)

> Supplier는 매개변수는 없고 반환값만 존재하는데, 메소드는 두 개의 값을 반환할 수 없으므로 BiSupplier가 없는 것이다.

두 개 이상의 매개변수를 갖는 함수형 인터페이스가 필요하다면 직접 만들어서 써야한다. 만일 3개의 매개변수를 갖는 함수형 인터페이스를 선언한다면 다음과 같을 것이다.

``` java
@FunctionalInterface
interface TriFunction<T, U, V, R> {
    R apply(T t, U u, V v);
}
```

</br>

### UnaryOperator와 BinaryOperator

`Function`의 또 다른 변형으로 `UnaryOperator`와 `BinaryOperator`가 있는데, 매개변수의 타입과 반환타입의 타입이 모두 일치한다는 점만 제외하고는 `Function`과 같다.

> UnaryOperator와 BinaryOperator의 조상은 각각 Function과 BiFunction이다.

![image](https://ifh.cc/g/O88g4Z.png)

</br>

### 컬렉션 프레임워크와 함수형 인터페이스

컬렉션 프레임워크의 인터페이스에 다수의 디폴트 메소드가 추가되었는데, 그 중의 일부는 함수형 인터페이스를 사용한다. 다음은 그 메소드들의 목록이다.

> 단순화하기 위해 와일드 카드는 생략하였다.

![image](https://ifh.cc/g/TT6rZb.png)

`Map`인터페이스에 있는 `compute`로 시작하는 메소드들은 맵의 `value`를 변환하는 일을 하고 `merge()`는 `Map`을 병합하는 일을 한다. 이 메소드들을 어떤 식으로 사용하는 지는 다음의 예제를 보겠다.

</br>

예제 14-4 / ch14 / LambdaEx4.java

``` java
import java.util.*;

public class LambdaEx4 {
	public static void main(String[] args) {
		ArrayList<Integer> list = new ArrayList<>();
		for(int i = 0; i < 10; i++)
			list.add(i);
		
		// list의 모든 요소를 출력
		list.forEach(i -> System.out.print(i + ","));
		System.out.println();
		
		// list에서 2 또는 3의 배수를 제거한다.
		list.removeIf(x -> x % 2 == 0 || x % 3 == 0);
		System.out.println(list);
		
		list.replaceAll(i -> i * 10);	// list의 각 요소에 10을 곱한다.
		System.out.println(list);
		
		Map<String, String> map = new HashMap<>();
		map.put("1", "1");
		map.put("2", "2");
		map.put("3", "3");
		map.put("4", "4");
		
		// map의 모든 요소를 (k, v)의 형식으로 출력한다.
		map.forEach((k, v) -> System.out.print("{" + k + ", " + v + "} ,"));
		System.out.println();
	}
}
```

```
0,1,2,3,4,5,6,7,8,9,
[1, 5, 7]
[10, 50, 70]
{1, 1} ,{2, 2} ,{3, 3} ,{4, 4} ,
```

함수형 인터페이스들을 사용하는 예제이다.

</br>

예제 14-5 / ch14 / LambdaEx5.java

``` java
import java.util.function.*;
import java.util.*;

public class LambdaEx5 {
	public static void main(String[] args) {
		Supplier<Integer> s = () -> (int)(Math.random() * 100) + 1;
		Consumer<Integer> c = i -> System.out.print(i + ", ");
		Predicate<Integer> p = i -> i % 2 == 0;
		Function<Integer, Integer> f = i -> i / 10 * 10;	// i의 일의 자리를 없앤다.
		List<Integer> list = new ArrayList<>();
		makeRandomList(s, list);
		System.out.println(list);
		printEvenNum(p, c, list);
		List<Integer> newList = doSomething(f, list);
		System.out.println(newList);
	}
	
	static <T> List<T> doSomething(Function<T, T> f, List<T> list) {
		List<T> newList = new ArrayList<T>(list.size());
		
		for(T i : list) {
			newList.add(f.apply(i));
		}
		
		return newList;
	}
	
	static <T> void printEvenNum(Predicate<T> p, Consumer<T> c, List<T> list) {
		System.out.print("[");
		for(T i : list) {
			if(p.test(i))
				c.accept(i);
		}
		System.out.println("]");
	}
	
	static <T> void makeRandomList(Supplier<T> s, List<T> list) {
		for(int i =0; i < 10; i++) {
			list.add(s.get());
		}
	}
}
```

```
[2, 95, 2, 88, 36, 82, 70, 43, 1, 25]
[2, 2, 88, 36, 82, 70, ]
[0, 90, 0, 80, 30, 80, 70, 40, 0, 20]
```

### 기본형을 사용하는 함수형 인터페이스

지금까지 함수형 인터페이스는 매개변수와 반환값의 타입이 모두 제네릭 타입이었는데, 기본형 타입의 값을 처리할 때도 래퍼(wrapper)클래스를 사용해왔다. 그러나 기본형 대신 래퍼클래스를 사용하는 것은 당연히 비효율적이다. 그래서 보다 효율적으로 처리할 수 있도록 기본형을 사용하는 함수형 인터페이스들이 제공된다.

![image](https://ifh.cc/g/na7ySt.png)

이전 예제를 기본형을 사용하는 함수형 인터페이스로 변경하면 다음과 같다.

</br>

예제 14-6 / ch14 / LambdaEx6.java

``` java
import java.util.function.*;
import java.util.*;

public class LambdaEx6 {
	public static void main(String[] args) {
		IntSupplier s = () -> (int)(Math.random() * 100) + 1;
		IntConsumer c = i -> System.out.print(i + ", ");
		IntPredicate p = i -> i % 2 == 0;
		IntUnaryOperator op = i -> i / 10 * 10;	// i의 일의 자리를 없앤다.
		
		int[] arr = new int[10];
		
		makeRandomList(s, arr);
		System.out.println(Arrays.toString(arr));
		printEvenNum(p, c, arr);
		int[] newArr = doSomething(op, arr);
		System.out.println(Arrays.toString(newArr));
	}
	
	static void makeRandomList(IntSupplier s, int[] arr) {
		for(int i = 0; i < arr.length; i++) {
			arr[i] = s.getAsInt();	// get()이 아니라 getAsInt()임에 주의
		}
	}
	
	static void printEvenNum(IntPredicate p, IntConsumer c, int[] arr) {
		System.out.print("[");
		for(int i : arr) {
			if(p.test(i))
				c.accept(i);
		}
		System.out.println("]");
	}
	
	static int[] doSomething(IntUnaryOperator op, int[] arr) {
		int[] newArr = new int[arr.length];
		
		for(int i = 0; i < newArr.length; i++) {
			newArr[i] = op.applyAsInt(arr[i]);	// apply()가 아님에 주의
		}
		
		return newArr;
	}
}
```

```
[12, 56, 82, 2, 95, 28, 21, 23, 75, 51]
[12, 56, 82, 2, 28, ]
[10, 50, 80, 0, 90, 20, 20, 20, 70, 50]
```

위 예제에서 만일 아래와 같이 `IntUnaryOperator`대신 `Function`을 사용하면 에러가 발생한다.

``` java
Function f = (a) -> 2 * a;  // 에러. a의 타입을 알 수 없으므로 연산불가
```

매개변수 `a`와 반환 값의 타입을 추정할 수 없기 때문이다. 그래서 아래와 같이 타입을 지정해 주어야한다.

``` java
// OK. 매개변수 타입과 반환타입이 Integer
Function<Integer, Integer> f = (a) -> 2 * a;
```

또는 아래와 같이 `Function` 대신 `IntFunction`을 사용할 수도 있지만, `IntUnaryOperator`가 `Function`이나 `InFunction`보다 오토박싱&언박싱의 횟수가 줄어들어 더 성능이 좋다.

``` java
// OK. 매개변수 타입은 int, 반환타입은 Integer
IntFunction<Integer> f = (a) -> 2 * a;
```

`IntFunction`, `ToIntFunction`, `IntToLongFunction`은 있어도 `IntToIntFunction`은 없는데, 그 이유는 `IntUnaryOperator`가 그 역할을 하기 때문이다. 매개변수의 타입과 반환타입이 일치할 때는 앞서 배운 것처럼 `Function`대신 `UnaryOperator`을 사용해야한다.

</br>

## 1.5 Function의 합성과 Predicate의 결합

`java.util.function`패키지의 함수형 인터페이스에는 추상메소드 외에도 디폴트 메소드와 static 메소드가 정의되어 있다. `Function`과 `Predicate`에 정의된 메소드에 대해서만 살펴보겠다. 그 이유는 다른 함수형 인터페이스의 메소드도 유사하기 때문이다.

> 원래 Function인터페이스는 반드시 두 개의 타입을 지정해 줘야하기 때문에, 두 타입이 같아도 Function<T>라고 쓸 수 없다. Function<T, T>라고 써야 한다.

``` java
Function
default <V> Function<T, V> andThen(Function<? super R, ? extends V> after)
default <V> Function<V, R> compose(Function<? super V, ? extends T> before)
static <T> Function<T, T> identity()

Predicate
default Predicate<T> and(Predicate<? super T> other)
default Predicate<T> or(Predicate<? super T> other)
default Predicate<T> negate()
static <T> Predicate<T> isEqual(Object targetRef)
```

</br>

### Function의 합성

수학에서 두 함수를 합성해서 하나의 새로운 함수를 만들어낼 수 있다는 것처럼, 두 람다식을 합성해서 새로운 람다식을 만들 수 있다. 두 함수의 합성은 어느 함수를 먼저 적용하느냐에 따라 달리진다. 함수 `f`, `g`가 있을 때, `f,andThen(g)`는 함수 `f`를 먼저 적용하고, 그 다음에 함수 `g`를 적용한다. 그리고 `f.compose(g)`는 반대로 `g`를 먼저 적용하고 `f`를 적용한다.

![image](https://ifh.cc/g/2nsSVH.png)

</br>

![image](https://ifh.cc/g/CnhVPV.png)

예를 들어, 문자열을 숫자로 변환하는 함수 `f`와 숫자를 2진 문자열로 변환하는 함수 `g`를 `andThen()`으로 합성하여 새로운 함수 `h`를 만들어낼 수 있다.

``` java
Function<String, Integer> f = (s) -> Integer.parseInt(s, 16);
Function<Integer, String> g = (i) -> Integer.toBinaryString(i);
Function<String, String> h = f.andThen(g);
```

함수 `h`의 제네릭 타입이 `<String, String>`이다. 즉, String을 입력받아서 String을 결과로 반환한다. 예를 들어 함수 `h`에 문자열 "FF"를 입력하면, 결과로 "11111111"을 얻는다.

![image](https://ifh.cc/g/4sKrxR.png)

이번엔 `compose()`를 이용해서 두 함수를 반대의 순서로 합성해보겠다.

``` java
Function<Integer, String> g = (i) -> Integer.toBinaryString(i);
Function<String, Integer> f = (s) -> Integer.parseInt(s, 16);
Function<Integer, Integer> h = f.compose(g);
```

이전과 달리 함수 `h`의 제네릭 타입이 `<Integer, Integer>`이다. 함수 `h`에 숫자 2를 입력하면, 결과로 16을 얻는다.

> 함수 f는 "10"을 16진수로 인식하기 때문에 16을 결과로 얻는다.

![image] (https://ifh.cc/g/5lGMLK.png)

그리고 `identity()`는 함수를 적용하기 이전과 이후가 동일한 '항등 함수'가 필요할 때 사용한다. 이 함수를 람다식으로 표현하면 `x -> x`이다. 아래의 두 문장은 동등하다.

> 항등 함수는 함수에 x를 대입하면 결과가 x인 함수를 말한다. f(x) = x

``` java
    Function<String, String> f = x -> x;
//  Function<String, String> f = Function.identity();   // 위의 문장과 동일

    System.out.println(f.apply("AAA")); // AAA가 그대로 출력됨
```

항등 함수는 잘 사용되지 않는 편이며, 나중에 배울 `map()`으로 변환작업할 때, 변환없이 그대로 처리하고자할 때 사용된다.

</br>

### Predicate의 결합

여러 조건식을 논리 연산자인 &&(and), ||(or), !(not)으로 연결해서 하나의 식을 구성할 수 있는 것처럼, 여러 `Predicate`를 `and()`, `or()`, `negate()`로 연결해서 하나의 새로운 `Predicate`로 결합할 수 있다.

``` java
Predicate<Integer> p = i -> i < 100;
Predicate<Integer> q = i -> i < 200;
Predicate<Integer> r = i -> i % 2 == 0;
Predicate<Integer> notP = p.negate();   // i >= 100

// 100 <= i && (i < 200 || i % 2 == 0)
Predicate<Integer> all = notP.and(q.or(r));
System.out.println(all.test(150));  // true
```

이처럼 `and()`, `or()`, `negate()`로 여러 조건식을 하나로 합칠 수 있다. 물론 아래와 같이 람다식을 직접 넣어도 된다.

``` java
Predicate<Integer> all = notP.and(i -> i < 200>).or(i -> i % 2 == 0);
```

> Predicate의 끝에 negate()를 붙이면 조건식 전체가 부정이 된다.

그리고 static메소드인 `isEqual()`은 두 대상을 비교하는 `Predicate`를 만들 때 사용한다. 먼저, `isEqual()`의 매개변수로 비교대상을 하나 지정하고, 또 다른 비교대상은 `test()`의 매개변수로 지정한다.

``` java
Predicate<String> p = Predicate.isEqual(str1);
boolean result = p.test(str2);  // str1과 str2가 같은지 비교하여 결과를 반환
```

위의 두 문장을 합치면 아래와 같다. 오히려 아래의 문장이 이해하기 더 쉽다.

``` java
// str1과 str2가 같은지 비교
boolean result = Predicate.isEqual(str1).test(str2);
```

</br>

예제 14-7 / ch14 / LambdaEx7.java

``` java
import java.util.function.*;

public class LambdaEx7 {
	public static void main(String[] args) {
		Function<String, Integer> f = (s) -> Integer.parseInt(s, 16);
		Function<Integer, String> g = (i) -> Integer.toBinaryString(i);
		
		Function<String, String> h = f.andThen(g);
		Function<Integer, Integer> h2 = f.compose(g);
		
		System.out.println(h.apply("FF"));	// "FF" → 255 → "11111111"
		System.out.println(h2.apply(2));	// 2 → "10" → 16
		
		Function<String, String> f2 = x -> x;	// 항등 함수(identity function)
		System.out.println(f2.apply("AAA"));	// AAA가 그대로 출력됨
		
		Predicate<Integer> p = i -> i < 100;
		Predicate<Integer> q = i -> i < 200;
		Predicate<Integer> r = i -> i % 2 == 0;
		Predicate<Integer> notP = p.negate();	// i >= 100
		
		Predicate<Integer> all = notP.and(q.or(r));
		System.out.println(all.test(150));	// true
		
		String str1 = "abc";
		String str2 = "abc";
		
		// str1과 str2가 같은지 비교한 결과를 반환
		Predicate<String> p2 = Predicate.isEqual(str1);
		boolean result = p2.test(str2);
		System.out.println(result);
	}
}
```

```
11111111
16
AAA
true
true
```

</br>

## 1.6 메소드 참조

람다식이 하나의 메소드만 호출하는 경우에는 '메소드 참조(method reference)'라는 방법으로 람다식을 간략히 할 수 있다. 예를 들어 문자열을 정수로 변환하는 람다식은 아래와 같이 작성할 수 있다.

``` java
Function<String, Integer> f = (String s) -> Integer.parseInt(s);
```

보통은 이렇게 람다식을 작성하는데, 이 람다식을 메소드로 표현하면 아래와 같다.

> 람다식은 엄밀히 말하자면 익명클래스의 객체지만 간단히 메소드가 적었다.

``` java
Integer wrapper(String s) { // 이 메소드의 이름은 의미없다.
    return Integer.parseInt(s);
}
```

이 `wrapper`메소드는 별로 하는 일이 없다. 그저 값을 받아서 `Integer.parseInt()`에게 넘겨주는 일만 할 뿐이다.

``` java
Function<String, Integer> f = (String s) -> Integer.parseInt(s);
                                ↓
Function<String, Integer> f = Integer::parseInt;    // 메소드 참조
```

위 메소드 참조에서 람다식의 일부가 생략되었지만, 컴파일러는 생략된 부분을 우변의 `parseInt`메소드의 선언부로부터, 또는 좌변의 `Function`인터페이스에 지정된 제네릭 타입으로부터 쉽게 알아낼 수 있다.

한 가지 예를 더 들어보겠다. 아래의 람다식을 메소드 참조조 변경하겠다.

``` java
BiFunction<String, String, Boolean> f = (s1, s2) -> s1.equals(s2);
```

참조변수의 `f`의 타입만 봐도 람다식이 두 개의 String타입의 매개변수를 받는다는 것을 알 수 있으므로, 람다식의 매개변수들은 없어도 된다. 위의 람다식에서 매개변수들을 제거해서 메소드 참조로 변경하면 아래와 같다.

``` java
BiFunction<String, String, Boolean> f = (s1, s2) -> s1.equals(s2);
                                ↓
BiFunction<Stirng, String, Boolean> f = String::equals; // 메소드 참조
```

매개변수 `s1`과 `s2`를 생략해버리고 나면 `equals`만 남는데, 두 개의 String을 받아서 Boolean을 반환하는 `equals`라는 이름의 메소드는 다른 클래스에도 존재할 수 있기 때문에 `equals`앞에 클래스 이름은 반드시 필요하다.

메소드 참조를 사용할 수 있는 경우가 한 가지 더 있는데, 이미 생성된 객체의 메소드를 람다식에서 사용한 경우에는 클래스 이름 대신 그 객체의 참조변수를 직어줘야 한다.

``` java
MyClass = obj = new MyClass();
Function<String, Boolean> f = (x) -> obj.equals(x); // 람다식
Function<String, Boolean> f2 = obj::equals; // 메소드 참조
```

지금까지 3가지 경우의 메소드 참조에 대해서 알아봤는데, 정리하면 다음과 같다.

![image](https://ifh.cc/g/jrGsWp.png)

> 하나의 메소드만 호출하는 람다식은 '클래스이름::메소드이름' 또는 '참조변수::메소드이름'으로 바꿀 수 있다.

</br>

### 생성자의 메소드 참조

생성자를 호출하는 람다식도 메소드 참조로 변환할 수 있다.

``` java
Supplier<MyClass> s = () -> new MyClass();  // 람다식
Supplier<MyClass> s = MyClass::new; // 메소드 참조
```

매개변수가 있는 생성자라면, 매개변수의 개수에 따라 알맞은 함수형 인터페이스를 사용하면 된다. 필요하다면 함수형 인터페이스를 새로 정의해야 한다.

``` java
Function<Integer, MyClass> f = (i) -> new MyClass();    // 람다식
Function<Integer, MyClass> f2 = MyClass::new;   // 메소드 참조

BiFunction<Integer, String, MyClass> bf = (i, s) -> new MyClass(i, s);
BiFunction<Integer, String, MyClass> bf2 = MyClass::new;    // 메소드 참조
```

그리고 배열을 생성할 때는 아래와 같이 하면 된다.

``` java
Function<Integer, int[]> f = x -> new int[x];   // 람다식
Function<Integer, int[]> f2 = int[]::new;   // 메소드 참조
```

메소드 참조는 람다식을 마치 static변수처럼 다룰 수 있게 해준다. 메소드 참조는 코드를 간략히 하는데 유용해서 많이 사용된다.