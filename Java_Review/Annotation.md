Chapter 12. 제네릭스, 열거형, 애너테이션

# 3. 애너테이션(Annotation)

</br>

## 3.1 애너테이션이란?

자바를 개발한 사람들은 소스코드에 대한 문서를 따로 만들기보다 소스코드와 문서를 하나의 파일로 관리하는 것이 낫다고 생각했다. 그래서 소스코드의 주석 `/** ~ */`에 소스코드에 대한 정보를 저장하고, 소스코드의 주석으로부터 HTML문서를 생성해내는 프로그램(javadoc.exe)을 만들어서 사용했다. 다음은 모든 애너테이션의 조상인 `Annotation`인터페이스의 소스코드의 일부이다.

``` java
/**
 * The common interface extended by all annotation types. Note that an
 * interface that manually extends this one does <i>not</i> define
 * an annotation type. Also note that this interface does not itself
 * define an annotation type.
        ...
 * The {@link java.lang.reflect.AnnoationElement} interface discusses
 * compatibility concerns when evolving an annotation type from being
 * non-repeatable to being repeatable.
 *
 * @author Josh Bloch
 * @since 1.5
 */
public interface Annotation {
...
}
```

미리 정의된 태그들을 이용해서 주석 안에 정보를 저장하고, javadoc.exe라는 프로그램이 이 정보를 읽어서 문서를 작성하는데 사용한다.

이 기능을 응용하여, 프로그램의 소스코드 안에 다른 프로그램을 위한 정보를 미리 약속된 형식으로 포함시킨 것이 바로 애너테이션이다. 애너테이션은 주석(comment)처럼 프로그래밍 언어에 영향을 미치지 않으면서도 다른 프로그램에게 유용한 정보를 제공할 수 있다는 장점이 있다.

> 애너테이션(annotation)의 뜻은 주석, 주해, 메모이다.

예를 들어, 자신이 작성한 소스코드 중에서 특정 메소드만 테스트하기를 원한다면, 다음과 같이 `@Test`라는 애너테이션을 메소드 앞에 붙인다. `@Test`는 '이 메소드를 테스트해야 한다.'는 것을 테스트 프로그램에게 알리는 역할을 할 뿐, 메소드가 포함된 프로그램 자체에는 아무런 영향을 미치지 않는다. 주석처럼 존재하지 않는 것이나 다름 없다.

``` java
@Test   // 이 메소드가 테스트 대상임을 테스트 프로그램에게 알린다.
public void method() {
        ...
}
```

테스트 프로그램에게 테스트할 메소드를 일일이 알려주지 않고, 해당 메소드 앞에 애너테이션만 붙이면 된다. 그렇다고 모든 프로그램에게 의미가 있는 것은 아니고, 해당 프로그램에 미리 정의된 종류와 형식으로 작성해야만 의미가 있다. `@Test`는 테스트 프로그램을 제외한 다른 프로그램에게는 아무런 의미가 없는 정보이다.

애너테이션은 JDK에서 기본적으로 제공하는 것과 다른 프로그램에서 제공하는 것들이 있는데, 이느 것이든 그저 약속된 형식으로 정보를 제공하기만 하면 된다.

JDK에서 제공하는 표준 애너테이션은 주로 컴파일러를 위한 것으로 컴파일러에게 유용한 정보를 제공한다. 그리고 새로운 애너테이션을 정의할 때 사용하는 메타 애너테이션을 제공한다.

> JDK에서 제공하는 애너테이션은 'java.lang.annotation'패키지에 포함되어 있다.

</br>

## 3.2 표준 애너테이션

자바에서 기본적으로 제공하는 애너테이션들은 몇 개 없다. 그나마 이들의 일부는 '메타 애너테이션(meta annotation)'으로 애너테이션을 정의하는데 사용되는 애너테이션의 애너테이션이다.

![image](https://ifh.cc/g/fHZG3c.png)

</br>

### @Override

메소드 앞에만 붙일 수 있는 애너테이션으로, 조상의 메소드를 오버라이딩하는 것이라는 걸 컴파일러에게 알려주는 역할을 한다. 아래의 코드에서와 같이 오버라이딩할 때 조상 메소드의 이름을 잘못 써도 컴파일러는 이것이 잘못된 것인지 알지 못한다.

``` java
class Parent {
        void parentMethod() { } 
}

class Child extends Parent {
        void parentmethod() { } // 오버라이딩하려 했으나 실수로 이름을 잘못적음
}
```

오버라이딩할 때는 이처럼 메소드의 이름을 잘못 적는 경우가 많은데, 컴파일러는 그저 새로운 이름의 메소드가 추가된 것으로 인식할 뿐이다. 게다가 실행 시에도 오류가 발생하지 않고 조상의 메소드가 호출되므로 어디서 잘못되었는지 알아내기 어렵다.

![image](https://ifh.cc/g/kdlqc0.png)

그러나 위의 오른쪽 코드와 같이 메소드 앞에 `@Override`라고 애너테이션을 붙이면, 컴파일러가 같은 이름의 메소드가 조상에 있는지 확인하고 없으면, 에러메세지를 출력한다.

</br>

예제 12-9 / ch12 / AnnotationEx1.java

``` java
class Parent {
	void parentMethod() {}
}

class Child extends Parent {
	@Override
	void parentmethod() { }	// 조상 메소드의 이름을 잘못 적었음.
}
```

```
AnnotationEx1.java:6: error: method does not override or implement a method
from a supertype
       @Override
       ^
1 error
```

이 예제를 컴파일하면 위와 같은 에러메세지가 나타난다. 오버라이딩을 해야 하는데 하지 않았다는 뜻이다. `@Override`를 메소드 앞에 붙이지 않았다면 나타나지 않았을 메세지이다.

</br>

### @Deprecated

새로운 버전의 JDK가 소개될 때, 새로운 기능이 추가될 뿐만 아니라 기존의 부족했던 기능들을 개선하기도 한다. 이 과정에서 기존의 기능을 대체할 것들이 추가되어도, 이미 여러 곳에서 사용되고 있을지 모르는 기존의 것들을 함부로 삭제할 수 없다.

그래서 생각해낸 방법이 더 이상 사용되지 않는 필드나 메소드에 `@Deprecated`를 붙이는 것이다. 이 애너테이션이 붙은 대상은 다른 것으로 대체되었으니 더 이상 사용하지 않을 것을 권한다는 의미이다. 예를 들어 `java.util.Date`클래스의 대부분의 메소드에는 `@Deprecated`가 붙어있는데, Java API에서 `Date`클래스의 `getDate()`를 보면 아래와 같이 적혀있다.

``` java
int getDate()
        Deprecated.
        As of JDK version 1.1, replaced by Calendar.get(Calendar.DAY_OF_MONTH).
```

이 메소드 대신에 JDK1.1부터 추가된 `Calendar`클래스의 `get()`을 사용하라는 얘기다. 기존의 것 대신 새로 추가된 개선된 기능을 사용하도록 유도하는 것이다.

만일 `@Deprecated`가 붙은 대상을 사용하는 코드를 작성하면, 컴파일할 때 아래와 같은 메세지가 나타난다.

```
Note: AnnotationEx2.java ues or overrides a deprecated API.
Note: Recomplie with -Xlint:deprecation for details.
```

해당 소스파일이 'deprecated'된 대상을 사용하고 있으며, '-Xlint:deprecation'옵션을 붙여서 다시 컴파일하면 자세한 내용을 알 수 있다는 뜻이다.

</br>

예제 12-10 / ch12 / AnnotationEx2.java

``` java
class NewClass {
	int newField;
	
	int getNewField() { return newField; }
	
	@Deprecated
	int oldField;
	
	@Deprecated
	int getOldField() { return oldField; }
}

public class AnnotationEx2 {
	public static void main(String[] args) {
		NewClass nc = new NewClass();
		
		nc.oldField = 10;	// @Deprecated가 붙은 대상을 사용
		System.out.println(nc.getOldField());	// @Deprecated가 붙은 대상을 사용
	}
}
```

```
c:\jdk1.8\work\ch12>javac AnnotationEx2.java
Note: AnnotationEx2.java uses of overrides a deprecated API.
Note: Recomplie with -Xlint:deprecation for details.

c:\jdk1.8\work\ch12>java AnnotationEx2
10
```

이 예제는 `@Deprecated`가 붙은 대상을 사용해서 고의적으로 위의 메세지가 나타나도록 했다. 메세지가 나타나기는 했지만 컴파일도 실행도 잘되었다. `@Deprecated`가 붙은 대상을 사용하지 않도록 권할 뿐 강제성은 잆기 때문이다.

</br>

### @FunctionalInterface

'함수형 인터페이스(functional interface)'를 선언할 때, 이 애너테이션을 붙이면 컴파일러가 '함수형 인터페이스'를 올바르게 선언했는지 확인하고, 잘못된 경우 에러를 발생시킨다.

> 함수형 인터페이스는 추상 메소드가 하나뿐이어야 한다는 제약이 있다.

``` java
@FunctionalInterface
public interface Runnable {
        public abstract void run();     // 추상 메소드
}
```

</br>

### @SuppressWarnings

컴파일러가 보여주는 경고메세지가 나타나지 않게 억제해준다. 이전 예제에서처럼 컴파일러의 경고메세지는 무시하고 넘어갈 수도 있지만, 모두 확인하고 해결해서 컴파일 후에 어떠한 메세지도 나타나지 않게 해야 한다.

그러나 경우에 따라서는 경고가 발생할 것을 알면서도 묵인해야 할 때가 있는데, 이 경고를 그대로 놔두면 컴파일할 때마다 메세지가 나타난다. 이전 예제에서 확인한 것과 같이 '-Xlint'옵션을 붙이지 않으면 컴파일러는 경고의 자세한 내용을 보여주지 않으므로 다른 경고들을 놓치기 쉽다. 이 떄는 묵인해야하는 경고가 발생하는 대상에 반드시 `@SuppressWarnings`를 붙여서 컴파일 후에 어떤 경고 메세지도 나타나지 않게 해야한다.

`@SuppressWarnings`로 억제할 수 있는 경고 메세지의 종류는 여러 가지가 있는데, JDK의 버전이 올라가면서 앞으로도 계속 추가될 것이다. 이 중에서 주로 사용되는 것은 "deprecation", "unchecked", "rawtypes", "varargs" 정도이다.

"deprecation"은 앞서 살펴본 것과 같이 `@Deprecated`가 붙은 대상을 사용해서 발생하는 경고를, "unchecked"는 제네릭스로 타입을 지정하지 않았을 때 발생하는 경고를, "rawtypes"는 제네릭스를 사용하지 않아서 발생하는 경고를, 그리고 "varagrs"는 가변인자의 타입이 제네릭 타입일 때 발생하는 경고를 억제할 때 사용한다.

억제하려는 경고 메세지를 애너테이션의 뒤에 괄호()안에 문자열로 지정하면 된다.

``` java
@SuppressWarnings("unchecked")  // 제네릭스와 관련된 경고를 억제
ArrayList list = new ArrayList();       // 제네릭 타입을 지정하지 않았음.
list.add(obj);  // 여기서 경고가 발생
```

만일 둘 이상의 경고를 동시에 억제하려면 다음과 같이 한다. 배열에서처럼 괄호{}를 추가로 사용해아한다.

``` java
@SuppressWarnings({"deprecation", "unchecked", "varargs"})
```

`@SuppressWarnings`로 억제할 수 있는 경고 메세지의 종류는 JDK의 버전이 올라가면서 계속 추가될 것이기 때문에, 이전 버전에서는 발생하지 않던 경고가 새로운 버전에서는 발생할 수 있다. 새로 추가된 경고 메세지를 억제하려면, 경고 메세지의 종류를 알아야하는데, -Xlint옵션으로 컴파일해서 나타나는 경고의 내용 중에서 대괄호{}안에 있는 것이 바로 메세지의 종류이다.

> -Xlint:unchecked와 같이 하면 unchecked와 관련된 경고만 표시된다.

```
C:\jdk1.8\work\ch12>javac -Xlint AnnotationTest.java
AnnotationTest.java:15: warning: [rawtypes] found raw type: List
        public static void sort(List list) {
                                ^
        missing type arguments for generic class List<E>
        where E is a type-variable:
          E extends Object declared in interface List
```

위의 경고 메세지를 보면 대괄호[]안에 "rawtypes"라고 적혀있으므로, 이 경고 메세지를 억제하려면 다음과 같이 하면 된다.

``` java
@SuppressWarnings("rawtypes")
public static void sort(List list) {
        ...
}
```

</br>

예제 12-11 / ch12 / AnnotationEx3.java

``` java
import java.util.ArrayList;

class NewClass1 {
	int newField;
	
	int getNewField() {
		return newField;
	}
	
	@Deprecated
	int oldField;
	
	@Deprecated
	int getOldField() {
		return oldField;
	}
}

public class AnnotationEx3 {
	@SuppressWarnings("deprecation")	// deprecation관련 경고를 억제
	public static void main(String[] args) {
		NewClass1 nc = new NewClass1();
		
		nc.oldField = 10;	// @Deprecated가 붙은 대상을 사용
		System.out.println(nc.getOldField());	// @Deprecated가 붙은 대상을 사용
		
		@SuppressWarnings("unchecked")
		ArrayList<NewClass1> list = new ArrayList<>();	// 타입을 지정하지 않음
		list.add(nc);
	}
}
```

```
c:\jdk1.8\work\ch12>javac AnnotationEx3.java

c:\jdk1.8\work\ch12>javac AnnoatationEx3
10
```

`main`메소드 앞에 `@SuppressWarnings("deprecation")`을 붙여서, 이 메소드 내에서 일어나는 'deprecation'과 관련된 모든 경고가 나타나지 않게 했다. 그리고 타입을 지정하지 않은 `ArrayList`객체를 생성한 곳에 `@SuppressWarnings("unchecked")`를 붙여서 경고를 억제했다. 두 애너테이션을 합쳐서 아래와 같이 `main`메소드에서 두 종류의 경고를 모두 억제하도록 할 수도 있다.

``` java
// main메소드 내의 "deprecation"과 "unchecked"관련 경고를 모두 억제한다.
@SuppressWarnings({"deprecation", "unchecked"})
public static void main(String[] args) {
		NewClass1 nc = new NewClass1();
		
		nc.oldField = 10;	// @Deprecated가 붙은 대상을 사용
		System.out.println(nc.getOldField());	// @Deprecated가 붙은 대상을 사용

		ArrayList<NewClass1> list = new ArrayList<>();	// 타입을 지정하지 않음
	}
```

그러나 그렇게 하면 나중에 추가된 코드에서 발생할 수도 있는 경고까지 억제될 수 있으므로 바람직하지 않다. 해당 대상에만 애너테이션을 붙여서 경고의 억제범위를 최소화하는 것이 좋다.

</br>

### SafeVarargs

메소드에 선언된 가변인자의 타입이 non-reifiable타입일 경우, 해당 메소드를 선언하는 부분과 호출하는 부분에서 "unchecked"경고가 발생한다. 해당 코드에 문제가 없다면 이 경고를 억제하기 위해 `@SafeVarargs`를 사용해야 한다.

이 애너테이션은 `static`이나 `final`이 붙은 메소드와 생성자에만 붙일 수 있다. 즉, 오버라이드될 수 있는 메소드에는 사용할 수 없다.

제네릭스에서 살펴본 것과 같이 어떤 타입들은 컴파일 이후에 삭제된다. 컴파일 후에도 제거되지 않는 타입을 reifiable타입이라고 하고, 제거되는 타입을 non-reifiable타입라고 하낟. 제네릭 타입들은 대부분 컴파일 시에 제거되므로 non-reifiable타입이다.

> reifiable은 're(다시) + '-ify(~화 하다)' + '-able(~할 수 있는)'의 합성어로 직역하면, '다시 ~화 할 수 있는'이라는 뜻이다. '리어화이어블'이라고 읽는다. 컴파일 후에도 타입정보가 유지되면 reifiable타입이다.

예를 들어, `java.util.Arrays`의 `asList()`는 다음과 같이 정의되어 있으며, 이 메소드는 매개변수로 넘겨받은 값들로 배열을 만들어서 새로운 `ArrayList`객체를 만들어서 반환하는데 이 과정에서 경고가 발생한다.

> 아래의 코드에 사용된 ArrayList는 Arrays클래스의 내부 클래스이다. java.util.ArrayList와 혼돈하지 말아야 한다.

``` java
public static <T> List<T> asList(T... a) {
        return new ArrayList<T>(a);     // ArrayList(E[] array)를 호출. 경고발생
}
```

`asList()`의 매개변수가 가변인자인 동시에 제네릭 타입이다. 메소드에 선언된 타입 `T`는 컴파일 과정에서 `Object`로 바뀐다. 즉, `Object[]`가 되는 것이다. `Object[]`에는 모든 타입의 객체가 들어있을 수 있으므로, 이 배열로 `ArrayList<T>`를 생성하는 것은 위험하다고 경고하는 것이다. 그러나 `asList()`가 호출되는 부분을 컴파일러가 체크해서 타입 `T`가 아닌 다른 타입이 들어가지 못하게 할 것이므로 위의 코드는 아무런 문제가 없다.

이럴 때는 메소드 앞에 `@SafeVarargs`를 붙여서 '이 메소드의 가변인자는 타입 안정성이 있다.'라고 컴파일러에게 알려서 경고가 발생하지 않도록 해야 한다.

메소드를 선언할 때 `@SafeVarargs`를 붙이면, 이 메소드를 호출하는 곳에서 발생하는 경고를 억제하려면, 메소드 선언뿐만 아니라 메소드가 호출되는 곳에도 애너테이션을 붙여야한다.

그리고 `@SafeVarargs`로 'unchecked'경고는 억제할 수 있지만, 'varargs'경고는 억제할 수 없기 때문에 습관적으로 `@SafeVarargs`와 `@suppressWarnings("unchecked")`를 같이 붙인다.

``` java
@SafeVarargs    // 'unchecked'경고를 억제한다.
@SuppressWarnings("varargs")    // 'varargs'경고를 억제한다.
public static <T> List<T> asList(T... a) {
        return new ArrayList<>(a);
}
```

`@SuppressWarnings("varargs")`를 붙이지 않아도 경고 없이 컴파일 된다. 그러나 -Xlint옵션을 붙여서 컴파일 해보면, 'varargs'경고가 발생한 것을 확일할 수 있다. 그래서 가능하면 이 두 애너테이션을 항상 같이 사용하는 것이 좋다.

</br>

예제 12-12 / ch12 / AnnotationEx4.java

``` java
import java.util.Arrays;

class MyArrayList<T> {
	T[] arr;
	
	@SafeVarargs
	@SuppressWarnings("varargs")
	MyArrayList(T... arr) {
		this.arr = arr;
	}
	
	@SafeVarargs
//	@SuppressWarnings("unchecked")
	public static <T> MyArrayList asList(T... a) {
		return new MyArrayList<>(a);
	}
	
	public String toString() {
		return Arrays.toString(arr);
	}
}

public class AnnotationEx4 {
//	@SuppressWarnings("unchecked")
	public static void main(String[] args) {
		MyArrayList<String> list = MyArrayList.asList("1", "2", "3");
		
		System.out.println(list);
	}
}
```

```
c:\jdk1.8\work\ch12>javac AnnotationEx4.java

c:\jdk1.8\work\ch12>javac -Xlint AnnotationEx4.java
AnnotationEx4.java:15: warning: [varargs] Varargs method could cause heap
pollution from non-reifiable varargs parameter a
        return new MyArrayList<>(a);
                                 ^
1 warning

c:\jdk1.8\work\ch12>
```

위의 컴파일 결과를 보면, 옵션없이 컴파일했을 때는 아무런 경고가 없지만, -Xlint옵션을 붙여서 컴파일했을 때는 'varargs'경고가 발생한 것을 알 수 있다. 아래와 같이 애너테이션을 추가하면, -Xlint옵션으로 컴파일 하여도 경고가 나타나지 않는다.

``` java
        @SafeVarargs
        @SuppressWarnings("varargs")    // 애너테이션을 추가
//      @SuppressWarnings("unchecked")
        public static <T> MyArrayList<T> asList(T... a) {
                return new MyArrayList<>(a);
        }
```

그리고 예제에서 `asList()`의 `@SafaVarargs`를 주석처리하고, `asList()`와 `main()`에 붙은 `@SuppressWarings("unchecked")`를 주석해제해보면, `@SafeVarargs`가 이 두 개의 애너테이션과 같은 효과를 얻는다는 것을 확인할 수 있다.

``` java
//      @SafeVarargs ← 주석처리
        @SuppressWarings("unchecked") ← 주석해제
        public static <T> MyArrayList<T> asList(T... a) {
                return new MyArrayList<>(a);
        }
                ...
        class AnnotationEx3 {
                @SuppressWarnings("uncheckd") ← 주석해제
                public static void main(String args[]) {
```

</br>

## 3.3 메타 애너테이션

메타 애너테이션은 '애너테이션을 위한 애너테이션', 즉 애너테이션에 붙이는 애너테이션으로 애너테이션을 정의할 때 애너테이션의 적용대상(target)이나 유지기간(retention)등을 지정하는데 사용된다.

> 메타 애너테이션은 'java.lang.annotation'패키지에 포함되어 있다.

</br>

### @Target

애너테이션이 적용가능한 대상을 지정하는데 사용된다 아래는 `@SuppressWarings`를 정의한 것인데, 이 애너테이션에 적용할 수 있는 대상을 `@Target`으로 지정하였다. 앞서 언급한 것과 같이 여러 개의 값을 지정할 때는 배열에서처럼 괄호{}를 사용해야한다.

``` java
@Target({TYPE, FIELD, METHOD, PARAMETER, CONSTRUCTOR, LOCAL_VARIABLE})
@Retention(RetentionPolicy.SOURCE)
public @interface SuppressWarings {
        String[] value();
}
```

`@Target`으로 지정할 수 있는 애너테이션 적용대상의 종류는 아래와 같다.

![image](https://ifh.cc/g/7RsGCs.png)

`TYPE`은 타입을 선언할 때, 애너테이션을 붙일 수 있다는 뜻이고 `TYPE_USE`는 해당 타입의 변수를 선언할 때 붙일 수 있다는 뜻이다. 표의 값들은 `java.lang.annotation.ElementType`이라는 열거형에 정의되어 있으며, 아래와 같이 `static import`문을 쓰면 `ElementType.TYPE`을 `TYPE`과 같이 간단히 할 수 있다.

``` java
import static java.lang.annotation.ElementType.*;

@Target({FIELD, TYPE, TYPE_USE})        // 적용대상이 FIELD, TYPE, TYPE_USE
public @interface MyAnnotation { }      // MyAnnotation을 정의

@MyAnnotation   // 적용대상이 TYPE인 경우
class MyClass {
        @MyAnnotation   // 적용대상이 FIELD인 경우
        int i;

        @MyAnnotation   // 적용대상이 TYPE_USE인 경우
        MyClass mc;
}
```

`FIELD`는 기본형에, 그리고 `TYPE_USE`는 참조형에 사용된다.

</br>

### @Retention

애너테이션이 유지(retention)되는 기간을 정의하는데 사용된다. 애너테이션의 유지 정책(retention policy)의 종류는 다음과 같다.

![image](https://ifh.cc/g/mPMF02.png)

`@Override`나 `@SuppressWarnings`처럼 컴파일러가 사용하는 애너테이션은 유지 정책이 'SOURCE'이다. 컴파일러를 직접 작성할 것이 아니면, 이 유지정책은 필요없다.

``` java
@Target(ElementType.METHOD)
@Retention(RetentionPolicy.SOURCE)
public @interface Override {}
```

유지 정책은 'RUNTIME'으로 하면, 실행 시에 '리플렉션(reflection)'을 통해 클래스 파일에 저장된 애너테이션의 정보를 읽어서 처리할 수 있다. `@FunctionalInterface`는 `@Override`처럼 컴파일러가 체크해주는 애너테이션이지만, 실행 시에도 사용되므로 유지정책이 'RUNTIME'으로 되어 있다.

``` java
@Documented
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.TYPE)
public @interface FunctionalInterface {}
```

유지 정책 'CLASS'는 컴파일러가 애너테이션의 정보를 클래스 파일에 저장할 수 있게는 하지만, 클래스 파일이 JVM에 로딩될 때는 애너테이션의 정보가 무시되어 실행 시에 애너테이션에 대한 정보를 얻을 수 없다. 이것이 'CLASS'가 유지정책의 기본값임에도 불구하고 잘 사용되지 않는 이유이다.

> 지역 변수에 붙은 애너테이션은 컴파일러만 인식할 수 있으므로, 유지정책이 'RUNTIME'인 애너테이션을 지역변수에 붙여도 실행 시에는 인식되지 않는다.

</br>

### @Documented

애너테이션에 대한 정보가 javadoc으로 작성한 문서에 포함되도록 한다. 자바에서 제공하는 기본 애너테이션 중에 `@Override`와 `@SuppressWarnings`를 제외하고는 모두 이 메타 애너테이션이 붙어 있다.

``` java
@Documented
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.TYPE)
public @interface FunctionalInterface {}
```

</br>

### @Inherited

애너테이션이 자손 클래스에 상속되도록 한다. `@Inherited`가 붙은 애너테이션을 조상 클래스에 붙이면, 자손 클래스도 이 애너테이션이 붙은 것과 같이 인식된다.

``` java
@Inherited	// @SuperAnno가 자손까지 영향 미치게
@Interface SuperAnno {}

@SuperAnno
class Parent {}

class Child extends Parent {}	// Child에 애너테이션이 붙은 것으로 인식
```

위의 코드에서 `Child`클래스는 애너테이션이 붙지 않았지만, 조상인 `Parent`클래스에 붙은 `@SuperAnno`가 상속되어 `Child`클래스에도 `@SuperAnno`가 붙은 것처럼 인식된다.

</br>

### @Repeatable

보통은 하나의 대상에 한 종류의 애너테이션을 붙이는데, `@Repeatable`이 붙은 애너테이션은 여러 번 붙일 수 있다.

``` java
@Repeatable(ToDos.class)	// ToDo애너테이션을 여러 번 반복해서 쓸 수 있게 한다.
@Interface ToDo {
	String value();
}
```

예를 들어 `@ToDo`라는 애너테이션이 위와 같이 정의되어 있을 때, 다음과 같이 `MyClass`클래스에 `@ToDo`를 여러 번 붙이는 것이 가능하다.

``` java
@ToDo("delete test codes.")
@ToDo("override inherited methods")
class MyClass {
	...
}
```

일반적인 애너테이션과 달리 같은 이름의 애너테이션이 여러 개가 하나의 대상에 적용될 수 있기 때문에, 이 애너테이션들을 하나로 묶어서 다룰 수 있는 애너테이션도 추가로 정의해야 한다.

``` java
@interface ToDos {	// 여러 개의 ToDo애너테이션을 담을 컨테이너 애너테이션 ToDos
	ToDo[] value();	// ToDo애너테이션 배열타입의 요소를 선언. 이름이 반드시 value이어야 함
}

@Repeatable(ToDos.class)	// 괄호 안에 컨테이너 애너테이션을 지정해 줘야한다.
@interface ToDo {
	String value();
}
```

</br>

### @Native

네이티브 메소드(native method)에 의해 참조되는 '상수 필드(constant field)'에 붙이는 애너테이션이다. 아래는 `java.lang.Long`클래스에 정의된 상수이다.

``` java
@Native public static final long MIN_VALUE = 0x8000000000000000L;
```

네이티브 메소드는 JVM이 설치된 OS의 메소드를 말한다. 네이티브 메소드는 보통 C언어로 작성되어 있는데, 자바에서는 메세드의 선언부만 정의하고 구현은 하지 않는다. 그래서 추상 메소드처럼 선언부만 있고 몸통이 없다.

``` java
public class Object {
	private static native void registerNatives();	// 네이티브 메소드

	static {
		registerNatives();	// 네이티브 메소드를 호출
	}

	protected native Object clone() throws CloneNotSupportedException;
	public final native Class<?> getClass();
	public final native void notify();
	public final native void notifyAll();
	public final native void wait(long timeout) throws InterruptedException;
	public native int hashCode();
		...
}
```

이처럼 모든 클래스의 조상인 `Object`클래스의 메소드들은 대부분 네이티브 메소드이다. 네이티브 메소드는 자바로 정의되어 있기 때문에 호출하는 방법은 자바의 일반 메소드와 다르지 않지만 실제로 호출되는 것은 OS의 메소드이다.

그냥 아무런 내용도 없는 네이티브 메소드를 선언해 놓고 호출한다고 되는 것은 아니고, 자바에 정의된 네이티브 메소드와 OS의 메소드를 연결해주는 작업이 추가로 필요하다. 이 역할은 JVM(Java Native Interface)가 한다.

</br>

## 3.4 애너테이션 타입 정의하기

직접 애너네이션을 만들어서 사용해보겠다. 새로운 애너테이션을 정의하는 방법은 아래와 같다. `@`기호를 붙이는 것을 제외하면 인터페이스를 정의하는 것과 동일하다.

``` java
@interface 애너테이션이름 {
	타입 요소이름();	// 애너테이션의 요소를 선언한다.
	...
}
```

엄밀히 말해서 `@Override`는 애너테이션이고 'Override'는 '애너테이션의 타입'이다.

</br>

### 애너테이션의 요소

애너테이션 내에 선언된 메소드를 '애너테이션의 요소(element)'라고 하며, 아래에 선언된 `TestInfo`애너테이션은 다섯 개의 요소를 갖는다.

> 애너테이션에도 인터페이스처럼 상수를 정의할 수 있지만, 디폴트 메소드는 정의할 수 없다.

``` java
@interface TestInfo {
	int count();
	String testedBy();
	String[] testTools();
	TestType testType();	// enum TestType { FIRST, FINAL }
	DateTime testDate();	// 자신이 아닌 다른 애너테이션(@DateTime)을 포함할 수 있다.
}

@interface DateTime {
	String yymmdd();
	String hhmmss();
}
```

애너테이션의 요소는 반환값이 있고 매개변수는 없는 추상 메소드의 형태를 가지며, 상속을 통해 구현하지 않아도 된다. 다만, 애너테이션을 적용할 때 이 요소들의 값을 빠짐없이 지정해주어야 한다. 요소의 이름도 같이 적어주므로 순서는 상관없다.

``` java
@TestInfo {
	count = 3, testedBy = "Kim",
	testTools = {"JUnit", "AutoTester"},
	testType = TestType.FIRST.
	testDate = @DateTime(yymmdd = "160101", hhmmss = "235959")
}
public class NewClass { ... }
```

애너테이션의 각 요소는 기본값을 가질 수 있으며, 기본 값이 있는 요소는 애너테이션을 적용할 때 값을 지정하지 않으면 기본값이 사용된다.

> 기본값으로 null을 제외한 모든 리터럴이 가능하다.

``` java
@interface TestInfo {
	int count() default 1;	// 기본값을 1로 저장
}

@TestInfo // @TestInfo(count = 1)과 동일
public class NewClass { ... }
```

애너테이션 요소가 오직 하나뿐이고 이름이 `value`인 경우, 애너테이션을 적용할 때 요소의 이름을 생략하고 값만 적어도 된다.

``` java
@interface TestInfo {
	String value();
}

@TestInfo("passed")	// @TestInfo(value="passed")와 동일
class NewClass { ... }
```

요소의 타입이 배열인 경우, 괄호{}를 사용해서 여러 개의 값을 지정할 수 있다.

``` java
@interface TestInfo {
	String[] testTools();
}

@Test(testTools={"JUnit", "AutoTester"})	// 값이 여러 개인 경우
@Test(testTools="JUnit")	// 값이 하나일 때는 괄호{} 생략가능
@Test(testTools={})	// 값이 없을 때는 {}가 반드시 필요
```

기본값을 지정할 때도 마찬가지로 괄호{}를 사용할 수 있다.

``` java
@interface TestInfo {
	String[] info() default { "aaa", "bbb" };	// 기본값이 여러 개인 경우. 괄호{} 사용
	String[] info2() default "ccc";	// 기본값이 하나인 경우. 괄호 생략가능
}

@TestInfo	// @TestInfo(info = {"aaa", "bbb"}, info2 = "ccc")와 동일
@TestInfo(info2 = {})	// @TestInfo(info = {"aaa", "bbb"}, info2 = {})와 동일
class NewClass { ... }
```

요소의 타입이 배열일 때도 요소의 이름이 `value`이면, 요소의 이름을 생략할 수 있다. 예를 들어, `@SuppressWarnings`의 경우, 요소의 타입이 String배열이고 이름이 `value`이다.

``` java
@interface SuppressWarnings {
	String[] value();
}
```

그래서 애너테이션을 적용할 때 요소의 이름을 생략할 수 있다.

``` java
//	@SuppressWarnings(value = {"deprecation", "unchecked"})
	@SuppressWarnings({"deprecation", "unchecked"})
	class NewClass { ... }
```

</br>

### java.lang.annotation.Annotation

모든 애너테이션의 조상은 `Annotation`이다. 그러나 애너테이션은 상속이 허용되지 않으므로 아래와 같이 명시적으로 `Annotation`을 조상으로 지정할 수 없다.

``` java
@interface TestInfo extends Annotation {	// 에러. 허용되지 않는 표현
	int count();
	String testedBy();
		...
}
```

게다가 아래의 소스에서 볼 수 있듯이 `Annotation`은 애너테이션이 아니라 일반적인 인터페이스로 정의되어 있다.

``` java
pakage java.lang.annotation;

public interface Annotation {	// Annotation자신은 인터페이스이다.
	boolean equals(Object obj);
	int hashCode();
	String toString();

	Class<? extends Annotation> annotationType();	// 애너테이션의 타입을 반환
}
```

모든 애너테이션의 조상인 `Annotation`인터페이스가 위와 같이 정의되어 있기 때문에, 모든 애너테이션 객체에 대해 `equals()`, `hashCode()`, `toString()`과 같은 메소드를 호출하는 것이 가능하다.

``` java
Class<AnnotationTest> cls = AnnotationTest.class;
Annotation[] annoArr = AnnotationTest.class.getAnnotations();

for(Annotation a : annoArr) {
	System.out.println("toString():"+a.toString());
	System.out.println("hashCode():"+a.hashCode());
	System.out.println("equals():"+a.eqauls());
	System.out.prointln("annotationType():"+a.annotationType());
}
```

위의 코드는 `AnnotationTest`클래스에 적용된 모든 애너테이션에 대해 `toString()`, `hashCode()`, `equals()`를 호출한다.

</br>

### 마커 애너테이션 Marker Annotation

값을 저장할 필요가 없는 경우, 애너테이션의 요소를 하나도 정의하지 않을 수 있다. `Serializable`이나 `Cloneable`인터페이스처럼, 요소가 하나도 정의되지 않은 애너테이션을 마커 애너테이션이라고 한다.

``` java
@Target(ElementType.METHOD)
@Retention(RetentionPolicy.SOURCE)
public @interface Override {}	// 마커 애너테이션. 정의된 요소가 하나도 없다.

@Target(ElementType.METHOD)
@Retention(RetentionPolicy.SOURCE)
public @interface Test {}	// 마커 애너테이션. 정의된 요소가 하나도 없다.
```

</br>

### 애너테이션 요소의 규칙

애너테이션의 요소를 선언할 때 반드시 지켜야 하는 규칙은 다음과 같다.

> - 요소의 타입은 기본형, String, enum, 애너테이션, Class만 허용된다.
> - ()안에 매개변수를 선언할 수 없다.
> - 에외를 선언할 수 없다.
> - 요소를 타입 매개변수로 정의할 수 없다.

``` java
@interface AnnoTest {
	int id = 100;	// OK. 상수 선언. static final int id = 100;
	String major(int i, int j);	// 에러. 매개변수를 선언할 수 없음
	String minor() throws Exception;	// 에러. 예외를 선언할 수 없음
	ArrayList<T> list();	// 에러. 요소의 타입에 타입 매개변수 사용불가
}
```

</br>

예제 12-13 / ch12 / AnnotationEx5.java

``` java
import java.lang.annotation.*;

@Deprecated
@SuppressWarnings("1111")	// 유효하지 않은 애너테이션은 무시된다.
@TestInfo(testedBy="aaa", testDate = @DateTime(yymmdd = "160101", hhmmss = "235959"))
public class AnnotationEx5 {
	public static void main(String[] args) {
		// AnnotationEx5의 Class객체를 얻는다.
		Class<AnnotationEx5> cls = AnnotationEx5.class;
		
		TestInfo anno = (TestInfo)cls.getAnnotation(TestInfo.class);
		System.out.println("anno.testedBy() = " + anno.testedBy());
		System.out.println("anno.testDate().yymmdd() = " + anno.testDate().yymmdd());
		System.out.println("anno.testDate().hhmmss() = " + anno.testDate().hhmmss());
		
		for(String str : anno.testTools())
			System.out.println("testTools = " + str);
		
		System.out.println();
		
		// AnnotataionEx5에 적용된 모든 애너테이션을 가져온다.
		Annotation[] annoArr = cls.getAnnotations();
		
		for(Annotation a : annoArr)
			System.out.println(a);
	}	// main의 끝
}

@Retention(RetentionPolicy.RUNTIME)	// 실행 시에 사용가능하도록 지정
@interface TestInfo {
	int count()	default 1;
	String testedBy();
	String[] testTools()	default "JUnit";
	TestType testType()	default TestType.FIRST;
	DateTime testDate();
}

@Retention(RetentionPolicy.RUNTIME)	// 실행 시에 사용가능하도록 지정
@interface DateTime {
	String yymmdd();
	String hhmmss();
}

enum TestType { FIRST, FINAL }
```

```
anno.testedBy() = aaa
anno.testDate().yymmdd() = 160101
anno.testDate().hhmmss() = 235959
testTools = JUnit

@java.lang.Deprecated(forRemoval=false, since="")
@TestInfo(count=1, testType=FIRST, testTools={"JUnit"}, testedBy="aaa", testDate=@DateTime(yymmdd="160101", hhmmss="235959"))
```

애너테이션을 직접 정의하고, 애너테이션의 요소의 값을 출력하는 방법을 보여주는 예제이다. `AnnotationEx5`클래스에 적용된 애너테이션을 실행시간에 얻으려면, 아래와 같이 하면 된다.

``` java
Class<AnnotationEx5> cls = AnnotationEx5.class;

TestInfo anno = (TestInfo)cls.getAnnotation(TestInfo.class);
```

`AnnotationEx5.class'는 클래스 객체를 의미하는 리터럴이다. 모든 클래스 파일은 클래스로더(Classloader)에 의해 메모리에 올라갈 때, 클래스에 대한 정보가 담긴 객체를 생성하는데 이 객체를 클래스 객체라고 한다. 이 객체를 참조할 때는 '클래스이름.class'의 형식을 사용한다.

클래스 객체에는 해당 클래스에 대한 모든 정보를 가지고 있는데, 애너테이션의 정보도 포함되어 있다.

클래스 객체가 가지고 있는 `getAnnotation()`이라는 메소드에 매개변수로 정보를 얻고자하는 애너테이션을 지정해주거나 `getAnnotations()`로 모든 애너테이션을 배열로 받아 올 수 있다.

``` java
TestInfo anno = (TestInfo)cls.getAnnotation(TestInfo.class);
System.out.println("anno.testedBy() = " + anno.testedBy());

// AnnotationEx5에 적용된 모든 애너테이션을 가져온다.
Annotation[] annoArr = cls.getAnnotations();
```

> Class클래스를 Java API에서 찾아보면 클래스의 정보를 제공하는 다양한 메소드가 정의되어 있는 것을 확인할 수 있다.