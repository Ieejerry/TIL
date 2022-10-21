Chapter 9. java.lang패키지와 유용한 클래스

# 2. 유용한 클래스

</br>

## 2.1 java.util.Objects클래스

`Object`클래스의 보조 클래스로 `Math`클래스처럼 모든 메소드가 `static`이다. 객체의 비교나 널 체크(null check)에 유용하다.

`isNull()`은 해당 객체가 널인지 확인해서 null이면 true를 반환하고 아니면 false를 반환한다. `nonNull()`은 `isNull()`과 정반대의 일을 한다. 즉, `!Objects.isNull(obj)`와 같다.

``` java
static boolean isNull(Object obj)
static boolean nonNull(Object obj)
```

그리고 `requireNonNull()`은 해당 객체가 널이 아니어야 하는 경우에 사용한다. 만일 객체가 널이면, `NullPointException`을 발생시킨다. 두 번째 매개변수로 지정하는 문자열은 예외의 메세지가 된다.

``` java
static <T> T requireNonNull(T obj)
static <T> T requireNonNull(T obj, String message)
static <T> T requireNonNull(T obj, Supplier<String> messageSupplier)
```

예전 같으면, 매개변수의 유효성 검사를 다음과 같이 해야 하는데, 이제는 `requireNonNull()`의 호출만으로 간단히 끝낼 수 있다.

``` java
void setName(String name) {
    if(name==null)
        throw new NullPointException("name must not be null.");

    this.name = name;
}
```

<center>↓</center>

``` java
void setName(String name) {
    this.name = Objects.requireNonNull(name, "name must not be null.");
}
```

`Objects`에 `compare()`는 두 비교대상이 같으면 0, 크면 양수, 작으면 음수를 반환한다.

``` java
static int compare(Object a, Object b, Object c)
```

이 메소드는 `a`와 `b` 두 객체를 비교하는데, 두 객체를 비교하는데 사용할 비교 기준이 필요하다. 그 역할을 하는 것이 Comparator이다.

``` java
static boolean equals(Object a, Obejct b)
static boolean deepEquals(Object a, Object b)
```

`Objects`클래스에도 `equals()`가 있는데, 이 메소드의 장점은 null검사를 하지 않아도 된다.

``` java
if(a!=null&&a.equals(b)) {  // a가 null인지 반드시 확인해야 한다.
    ...
}
```

<center>↓</center>

``` java
if(Objects.equals(a, b)) {  // 매개변수의 값이 null인지 확인할 필요가 없다.
    ...
}
```

`equals()`의 내부에서 `a`와 `b`의 널 검사를 하기 때문에 따로 널 검사를 위한 조건식을 따로 넣지 않아도 된다.

``` java
public static boolean equals(Object a, Object b) {
    return(a == b) || (a != null && a.equals(b));
}
```

`a`와 `b`가 모두 널인 경우에는 참을 반환한다는 점을 빼고는 특별한 것이 없다. `deepEquals()`는 객체를 재귀적으로 비교하기 때문에 다차원 배열의 비교도 가능하다.

``` java
String[][] str2D = new String[][]{{"aaa", "bbb"}, {"AAA", "BBB"}};
String[][] str2D2 = new String[][]{{"aaa", "bbb"}, {"AAA", "BBB"}};

System.out.println(Objects.equals(str2D, str2D2));  // false
System.out.println(Objects.deepEquals(str2D, str2D2));  // true
```

``` java
static String toString(Object o)
static String toString(Object o, String nullDefault)
```

`toString()`도 `equals()`처럼, 내부적으로 널 검사를 한다는 것 빼고는 특별한 것이 없다. 두 번째 메소드는 o가 널일 때, 대신 사용할 값을 지정할 수 있어서 유용하다.

마지막으로 `hashCode()`인데, 이것 역시 내부적으로 널 검사를 한 후에 `Object`클래스의 `hashCode()`를 호출할 뿐이다.

``` java
static int hashCode(Object o)
static int hash(Object... values)
```

보통은 클래스에 선언된 인스턴스의 변수들의 `hashCode()`를 조합해서 반환하도록, `hashCode()`를 오버라이딩하는데, 그 대신 매개변수의 타입이 가변인자인 두 번째 메소드를 사용하면 편리하다.

예제 9-26 / ch9 / ObjectsTest.java

``` java
import java.util.*;
import static java.util.Objects.*;	// Objects클래스의 메소드를 static import

public class ObjectsTest {
	public static void main(String[] args) {
		String[][] str2D = new String[][] {{"aaa", "bbb"}, {"AAA", "BBB"}};
		String[][] str2D_2 = new String[][] {{"aaa", "bbb"}, {"AAA", "BBB"}};
		
		System.out.print("str2D = {");
		for(String[] tmp : str2D)
			System.out.print(Arrays.toString(tmp));
		System.out.println("}");
		
		System.out.print("str2D_2= {");
		for(String[] tmp : str2D_2)
			System.out.print(Arrays.toString(tmp));
		System.out.println("}");
		
		System.out.println("equals(str2D, str2D_2)=" + Objects.equals(str2D, str2D_2));
		System.out.println("deepEquals(str2D, str2D_2)=" + Objects.deepEquals(str2D, str2D_2));
		
		System.out.println("isNull(null) =" + isNull(null));
		System.out.println("nonNull(null) =" + nonNull(null));
		System.out.println("hashCode(null) =" + Objects.hashCode(null));
		System.out.println("toString(null) =" + Objects.toString(null));
		System.out.println("toString(null, \"\") =" + Objects.toString(null, ""));
		
		Comparator c = String.CASE_INSENSITIVE_ORDER;	// 대소문자 구분 안하는 비교
		
		System.out.println("compare(\"aa\", \"bb\")=" + compare("aa", "bb", c));
		System.out.println("compare(\"bb\", \"aa\")=" + compare("bb", "aa", c));
		System.out.println("compare(\"ab\", \"AB\")=" + compare("ab", "AB", c));
	}
}
```

```
str2D = {[aaa, bbb][AAA, BBB]}
str2D_2= {[aaa, bbb][AAA, BBB]}
equals(str2D, str2D_2)=false
deepEquals(str2D, str2D_2)=true
isNull(null) =true
nonNull(null) =false
hashCode(null) =0
toString(null) =null
toString(null, "") =
compare("aa", "bb")=-1
compare("bb", "aa")=1
compare("ab", "AB")=0
```

static import문을 사용했음에도 불구하고 `Object`클래스의 메소드와 일므이 같은 것들은 충돌이 난다. 즉, 컴파일러가 구별을 못한다. 그럴 때는 클래스의 이름을 붙여줄 수밖에 없다. 그리고 `String`클래스에 상수로 정의되어 있는 `Comparator`가 있어서 그걸 사용해서 `compare()`를 호출했다.

``` java
Comparator c = String.CAsE_INSENSITIVE_ORDER;   // 대소문자 구분안하는 비교
    ...
System.out.println("compare(\"ab\", \"AB\")=" + compare("ab", "AB", c));
```

이 `Comparator`는 문자열을 대소문자 구분하지 않고 비교할 때 사용하기 위한 것이다. 그래서 아래와 같이 "ab"와 "AB"를 비교한 결과가 0, 즉 두 문자열이 같다는 결과가 나온다.