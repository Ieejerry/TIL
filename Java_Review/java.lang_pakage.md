Chapter 9. java.lang패키지와 유용한 클래스

## 1 java.lang패키지

java.lang패키지는 자바프로그래밍에 가장 기본이 되는 클래스들을 포함하고 있다. 그렇기 때문에 java.lang패키지의 클래스들은 import문 없이도 사용할 수 있게 되어 있다.

</br>

## 1.1 Object클래스

`Object`클래스는 모든 클래스의 최고 조상이기 때문에 `Object`클래스의 멤버들은 모든 클래스에서 바로 사용이 가능하다.

![image](https://ifh.cc/g/Wcf7DX.png)

`Object`클래스는 멤버변수는 없고 오직 11개의 메소드만 가지고 있다. 이 메소드들은 모든 인스턴스가 가져야 할 기본적인 것들이다.

</br>

### equals(Object obj)

매개변수로 객체의 참조변수를 받아서 비교하여 그 결과를 boolean값으로 알려주는 역할을 한다. 아래의 코드는 `Object`클래스에 정의도어 있는 `equals`메소드의 실제 내용이다.

``` java
public boolean equals(Object obj) {
    return (this == obj);
}
```

위의 코드에서 알 수 있듯이 두 객체의 같고 다름을 참조변수의 값으로 판단한다. 그렇기 때문에 서로 다른 두 객체를 `equals`메소드로 비교하면 항상 `false`를 결과로 얻게 된다.

> 객체를 생성할 때, 메모리의 비어있는 공간을 찾아 생성하므로 서로 다른 두 개의 객체가 같은 주소를 갖는 일은 있을 수 없다. 두 개 이상의 참조변수가 같은 주소값을 갖는 것(한 객체를 참조하는 것)은 가능하다.

예제 9-1 / ch9 / EqualsEx1.java

``` java
class Value {
	int value;
	
	Value(int value) {
		this.value = value;
	}
}

public class EqualsEx1 {
	public static void main(String[] args) {
		Value v1 = new Value(10);
		Value v2 = new Value(10);
		
		if(v1.equals(v2)) System.out.println("v1과 v2는 같습니다.");
		else System.out.println("v1과 v2는 다릅니다.");
		
		v2 = v1;
		
		if(v1.equals(v2)) System.out.println("v1과 v2는 같습니다.");
		else System.out.println("v1과 v2는 다릅니다.");
	}	// main
}
```

```
v1과 v2는 다릅니다.
v1과 v2는 같습니다.
```

`value`라는 멤버변수를 갖는 `Value`클래스를 정의하고, 두 개의 `Value`클래스의 인스턴스 생성한 다음 `equals`메소드를 이용해서 두 인스턴스를 비교하도록 했다. `equals`메소드는 주소값으로 비교를 하기 때문에, 두 `Value`인스턴스의 멤버변수 `value`의 값이 10으로 서로 같을지라도 `equals`메소드로 비교한 결과는 `false`일 수 밖에 없다.

![image](https://ifh.cc/g/lBNhlp.png)

하지만, `v2 == v1;`을 수행한 후에는 참조변수 `v2`는 `v1`이 참조하고 있는 인스턴스의 주소값이 저장되므로 `v2`도 `v1`과 같은 주소값이 저장된다. 그래서 이번에는 `v1.equals(v2)`의 결과가 `true`가 되는 것이다.

![image](https://ifh.cc/g/Qq9Q9a.png)

`Object`클래스로부터 상속받은 `equals`메소드는 결국 두 개의 참조변수가 같은 객체를 참조하고 있는지, 즉 두 참조변수에 저장된 값(주소값)이 같은지를 판단하는 기능밖에 할 수 없다는 것을 알 수 있다. `equals`메소드로 `Value`인스턴스가 가지고 있는 `value`값을 비교하게 하려면 `Value`클래스에서 `equals`메소드를 오버라이딩하여 주소가 아닌 객체의 저장된 내용을 비교하도록 변경하면 된다.

예제 9-2 / ch9 / EqualsEx2.java

``` java
class Person {
	long id;
	
	public boolean equals(Object obj) {
		if(obj instanceof Person) return id == ((Person)obj).id;	// obj가 Object타입이므로 id값을 참조하기 위해서는 Person타입으로 형변환이 필요하다.
		else return false;	// 타입이 Person이 아니면 값을 비교할 필요도 없다.
	}
	
	Person(long id) {
		this.id = id;
	}
}

public class EqualsEx2 {
	public static void main(String[] args) {
		Person p1 = new Person(801108111222L);
		Person p2 = new Person(801108111222L);
		
		if(p1 == p2) System.out.println("p1과 p2는 같은 사람입니다.");
		else System.out.println("p1과 p2는 다른 사람입니다.");
		
		if(p1.equals(p2)) System.out.println("p1과 p2는 같은 사람입니다.");
		else System.out.println("p1과 p2는 다른 사람입니다.");
	}
}
```

```
p1과 p2는 다른 사람입니다.
p1과 p2는 같은 사람입니다.
```

`equals`메소드가 `Person`인스턴스의 주소값이 아닌 멤버변수 `id`의 값을 비교하도록 하기위해 `equals`메소드를 다음과 같이 오버라이딩했다. 이렇게 함으로써 서로 다른 인스턴스일지라도 같은 `id`(주민등록번호)를 가지고 있다면 `equals`메소드로 비교했을 때 `true`를 결과로 얻게 할 수 있다.

``` java
public boolean equals(Object obj) {
		if(obj != null && obj instanceof Person) return id == ((Person)obj).id;
		else return false;
	}
```

`String`클래스 역시 `Object`클래스의 `equals`메소드를 그대로 사용하는 것이 아니라 이처럼 오버라이딩을 통해서 `String`인스턴스가 갖는 문자열 값을 비교하도록 되어있다. 그렇기 때문에 같은 내용의 문자열을 갖는 두 `String`인스턴스에 `equals`메소드를 사용하면 항상 `true`값을 얻는 것이다.

> String클래스뿐만 아니라, Data, File, wrapper클래스(Integer, Double, 등)의 equals메소드도 주소값이 아닌 내용을 비교하도록 오버라이딩되어 있다. 그러나 의외로 StringBuffer클래스는 오버라이딩되어 있지 않다.

![image](https://ifh.cc/g/d1drBa.png)

</br>

### hashCode()

이 메소드는 해싱(hashing)기법에 사용되는 '해시함수(hash function)'를 구현한 것이다. 해싱은 데이터관리기법 중의 하나인데 다량의 데이터를 저장하고 검색하는 데 유용하다. 해시함수는 찾고자하는 값을 입력하면, 그 값이 저장된 위치를 알려주는 해시코드(hash code)를 반환한다.

일반적으로 해시코드가 같은 두 객체가 존재하는 것이 가능하지만, `Object`클래스에 정의된 `hashCode`메소드는 객체의 주소값으로 해시코드를 만들어 반환하기 때문에 32 bit JVM에서는 서로 다른 두 객체는 결코 같은 해시코드를 가질 수 없었지만, 64 bit JVM에서는 8 byte 주소값으로 해시코드(4 byte)를 만들기 때문에 해시코드가 중복될 수 있다.

클래스의 인스턴스변수 값으로 객체의 같고 다름을 판단해야하는 경우라면 `equals`메소드 뿐만 아니라 `hashCode`메소드도 적절히 오버라이딩해야 한다. 같은 객체라면 `hashCode`메소드를 호출했을 때의 결과값인 해시코드도 같아야 하기 때문이다.

예제 9-3 / ch9 / HashCodeEx1.java

``` java
public class HashCodeEx1 {
	public static void main(String[] args) {
		String str1 = new String("abc");
		String str2 = new String("abc");
		
		System.out.println(str1.equals(str2));
		System.out.println(str1.hashCode());
		System.out.println(str2.hashCode());
		System.out.println(System.identityHashCode(str1));
		System.out.println(System.identityHashCode(str2));
	}
}
```

```
true
96354
96354
515132998
1694819250
```

`String`클래스는 문자열의 내용이 같으면, 동일한 해시코드를 반환하도록 `hashCode`메소드가 오버라이딩되어 있기 때문에, 문자열의 내용이 같은 `str1`과 `str2`에 대해 `hashCode()`를 호출하면 항상 동일한 해시코드값을 얻는다.

반면에 `System.identityHashCode(Object x)`는 `Object`클래스의 `hashCode`메소드처럼 객체의 주소값으로 해시코드를 생성하기 때문에 모든 객체에 대해 항상 다른 해시코드값을 반환할 것을 보장한다. 그래서 `str1`과 `str2`가 해시코드는 같지만 서로 다른 객체라는 것을 알 수 있다.

> System.identityHashCode(Object x)의 호출결과는 실행 할 때마다 달라질 수 있다.

</br>

### toString()

이 메소드는 인스턴스에 대한 정보를 문자열(String)로 제공할 목적으로 정의한 것이다. 인스턴스의 정보를 제공한다는 것은 대부분의 경우 인스턴스 변수에 저장된 값들을 문자열로 표현한다는 뜻이다.

`Object`클래스에 정의된 `toString()`은 아래와 같다.

``` java
public String toString() {
    return getClass().getName() + "@" + Integer.toHexString(hashCode());
}
```

클래스를 작성할 때 `toString()`을 오버라이딩하지 않는다면, 위와 같은 내용이 그대로 사용될 것이다. 즉, `toString()`을 호출하면 클래스이름에 16진수의 해시코드를 얻게 된다.

> getClass()와 hachCode() 역시 Object클래스에 정의된 것이므로 인스턴스 생성없이 바로 호출할 수 있다.

예제 9-4 / ch9 / CardToString.java

``` java
class Card {
	String kind;
	int number;
	
	Card() {
		this("SPADE", 1);
	}
	
	Card(String kind, int number) {
		this.kind = kind;
		this.number = number;
	}
}

public class CardToString {
	public static void main(String[] args) {
		Card c1 = new Card();
		Card c2 = new Card();
		
		System.out.println(c1.toString());
		System.out.println(c2.toString());
	}
}
```

```
Card@75a1cd57
Card@515f550a
```

`Card`인스턴스 두 개를 생성한 다음, 각 인스턴스에 `toString()`을 호출한 결과를 출력했다. `Card`클래스에서 `Object`클래스로부터 상속받은 `toString()`을 오버라이딩하지 않았기 때문에 `Card`인스턴스에 `toString()`을 호출하면, `Object`클래스의 `toString()`이 호출된다.

그래서 위의 결과에 클래스이름과 해시코드가 출력되었다. 서로 다른 인스턴스에 대해서 `toString()`을 호출하였으므로 클래스의 이름은 같아도 해시코드값이 다르다는 것을 확인할 수 있다.

예제 9-5 / ch9 / ToStringTest.java

``` java
public class ToStringTest {
	public static void main(String[] args) {
		String str = new String("KOREA");
		java.util.Date today = new java.util.Date();
		
		System.out.println(str);
		System.out.println(str.toString());
		System.out.println(today);
		System.out.println(today.toString());
	}
}
```

```
KOREA
KOREA
Mon Oct 10 14:27:11 KST 2022
Mon Oct 10 14:27:11 KST 2022
```

위으 결과에서 알 수 있듯이 `String`클래스와 `Date`클래스의 `toString()`을 호출하였더니 클래스이름과 해시코드 대신 다른 결과가 출력되었다.

`String`클래스의 `toString()`은 `String`인스턴스가 갖고 있는 문자열을 반환하도록 오버라이딩되어 있고, `Date`클래스의 경우, `Date`인스턴스가 갖고 있는 날짜와 시간을 문자열로 변환하여 반환하도록 오버라이딩되어 있다.

이처럼 `toString()`은 일반적으로 인스턴스나 클래스에 대한 정보 또는 인스턴스 변수들의 값을 문자열로 변환하여 반환하도록 오버라이딩되는 것이 보통이다.

이제 `Card`클래스에서도 `toString()`을 오버라이딩해서 보다 쓸모 있는 정보를 제공할 수 있도록 바꿔보겠다.

예제 9-6 / ch9 / CardToString2.java

``` java
class Card2 {
	String kind;
	int number;
	
	Card2() {
		this("SPADE", 1);	// Card(String kind, int number)를 호출
	}
	
	Card2(String kind, int number) {
		this.kind = kind;
		this.number = number;
	}
	
	public String toString() {
		return "kind : " + kind + ", number : " + number;	// Card인스턴스의 kind와 number를 문자열로 반환한다.
	}
}

public class CardToString2 {
	public static void main(String[] args) {
		Card2 c1 = new Card2();
		Card2 c2 = new Card2("HEART", 10);
		
		System.out.println(c1.toString());
		System.out.println(c2.toString());
	}
}
```

```
kind : SPADE, number : 1
kind : HEART, number : 10
```

`Card2`인스턴스의 `toString()`을 호출하면 인스턴스가 갖고 있는 인스턴스변수 `kind`와 `number`의 값을 문자열로 변환하여 반환하도록 `toString()`을 오버라이딩했다. 오버라이딩할 때, `Object`클래스에 정의된 `toString()`의 접근 제어자가 `public`이므로 `Card`클래스의 `toString()`의 접근제어자도 `public`으로 했다.

조상에 정의된 메소드를 자손에서 오버라이딩할 때는 조상에 정의된 접근범위보다 같거나 더 넓어야 하기 때문이다. `Object`클래스에서 `toString()`의 접근 제어자가 `public`이므로, 이를 오버라이딩하는 `Card2`클래스에서는 `toString()`의 접근 제어자를 `public`으로 할 수 밖에 없다.

</br>

### clone()

이 메소드는 자신을 복제하여 새로운 인스턴스를 생성하는 일을 한다. 어떤 인스턴스에 대해 작업을 할 때, 원래의 인스턴스는 보존하고 `clone`메소드를 이용해서 새로운 인스턴스를 생성하여 작업을 하면 작업이전의 값이 보존되므로 작업에 실패해서 원래의 상태로 되돌리거나 변경되기 전의 값을 참고하는데 도움이 된다.

`Object`클래스에 정의된 `clone()`은 단순히 인스턴스변수의 값만 복사하기 때문에 참조타입의 인스턴스변수가 있는 클래스는 완전히 인스턴스 복제가 이루어지지 않는다.

예를 들어 배열의 경우, 복제된 인스턴스도 같은 배열의 주소를 갖기 때문에 복제된 인스턴스의 작업이 원래의 인스턴스에 영향을 미치게 된다. 이런 경우 `clone`메소드를 오버라이딩해서 새로운 배열을 생성하고 배열의 내용을 복사하도록 해야 한다.

예제 9-7 / ch9 / CloneEx1.java

``` java
class Point implements Cloneable {
	int x, y;
	
	Point(int x, int y) {
		this.x = x;
		this.y = y;
	}
	
	public String toString() {
		return "x = " + x + ", y = " + y;
	}
	
	public Object clone() {
		Object obj = null;
		try {
			obj = super.clone();	// clone()은 반드시 예외처리를 해주어야 한다.
		} catch (CloneNotSupportedException e) {}
		return obj;
	}
}

public class CloneEx1 {
	public static void main(String[] args) {
		Point original = new Point(3, 5);
		Point copy = (Point)original.clone();	// 복제(clone)해서 새로운 객체를 생성
		System.out.println(original);
		System.out.println(copy);
	}
}
```

```
x = 3, y = 5
x = 3, y = 5
```

`clone()`을 사용하려면, 먼저 복제할 클래스가 `Cloneable`인터페이스를 구현해야하고, `clone()`을 오버라이딩하면서 접근 제어자를 `protected`에서 `public`으로 변경한다. 그래야만 상속관계가 없는 다른 클래스에서 `clone()`을 호출할 수 있다.

``` java
public class Object {
        ...
    protected native Object clone() throws CloneNotSuppoertedException;
        ...
}
```

> Object클래스의 clone()은 Cloneable을 구현하지 않은 클래스 내에서 호출되면 예외를 발생시킨다.

마지막으로 조상클래스의 `clone()`을 호출하는 코드가 포함된 try-catch문을 작성한다.

``` java
class Point implements Cloneable {  // ① Cloneable인터페이스를 구현한다.
    ...
    public Object clone() { // ② 접근제어자를 protected에서 public으로 변경
        Object obj = null;
        try {
            obj = super.clone();    // ③ try-catch내에서 조상클래스의 clone()을 호출
        } catch(CloneNotSuppertedException e) {}
        return obj;
    }
}
```

`Cloneable`인터페이스를 구현한 클래스의 인스턴스만 `clone()`을 통한 복제가 가능한데, 그 이유는 인스턴스의 데이터를 보호하기 위해서이다. `Cloneable`인터페이스가 구현되어 있다는 것은 클래스 작성자가 복제를 허용한다는 의미이다.

</br>

### 공변 변환타입

JDK1.5부터 '공변 변환타입(covariant return type)'이라는 것이 추가되었는데, 이 기능은 오버라이딩할 때 조상 메소드의 반환타입을 자손 클래스의 타입으로 변경을 허용하는 것이다.

아래의 코드는 예제9-7의 `clone()`의 반환타입을 `Object`에서 `Point`로 변경한 것이다. 즉, 조상의 타입에서 자손의 타입으로 변경한 것이다. 그리고 return문에 `Point`타입으로 형변환도 추가하였다. 예전에는 오버라이딩할 때 조상에 선언된 메소드의 반환타입을 그대로 사용해야 했다.

``` java
public Object clone() { // ① 반환타입을 Object에서 Point로 변경
        Object obj = null;
        try {
            obj = super.clone();
        } catch(CloneNotSuppertedException e) {}
        return (Point)obj;  // ② Point타입으로 형변환한다.
    }
```

이처럼 '공변 반환타입'을 사용하면, 조상의 타입이 아닌, 실제로 반환되는 자손 객체의 타입으로 반환할 수 있어서 번거로운 형변환이 줄어든다는 장점이 있다.

![image](https://ifh.cc/g/qah0QY.png)

예제 9-7이 공변 반환타입을 사용하도록 직접 변경해서 실행해보겠다.

예제 9-8 / ch9 / CloneEx2.java

``` java
import java.util.*;

public class CloneEx2 {
	public static void main(String[] args) {
		int[] arr = { 1, 2, 3, 4, 5 };
		int[] arrClone = arr.clone();	// 배열 arr을 복제해서 같은 내용의 새로운 배열을 만든다.
		arrClone[0] = 6;
		
		System.out.println(Arrays.toString(arr));
		System.out.println(Arrays.toString(arrClone));
	}
}
```

```
[1, 2, 3, 4, 5]
[6, 2, 3, 4, 5]
```

`clone()`을 이용해서 배열을 복사하는 예제이다. 배열도 객체이기 때문에 `Object`클래스를 상속받으며, 동시에 `Cloneable`인터페이스와 `Serializable`인터페이스가 구현되어 있다. 그래서 `Object`클래스의 멤버들을 모두 상속받는다. `Object`클래스에는 `protected`로 정의되어있는 `clone()`을 배열에서는 `public`으로 오버라이딩하였기 때문에 예제처럼 직접 호출이 가능하다. 그리고 원본과 같은 타입을 반환하므로 형변환이 필요 없다.

일반적으로는 배열을 복사할 때, 같은 길이의 새로운 배열을 생성한 다음에 `System.arraycopy()`를 이용해서 내용을 복사하지만, 이처럼 `clone()`을 이용해서 간단하게 복사할 수 있다.

아래의 두 코드는 같은 결과를 얻는다. 어느 쪽을 사용해도 상관없다.

![image](https://ifh.cc/g/F6TDpl.png)

배열 뿐만 아니라 `java.util`패키지의 `Vector`, `ArrayList`, `LinkedList`, `HashSet`, `TreeSet`, `HashMap`, `TreeMap`, `Calendar`, `Date`와 같은 클래스들이 이와 같은 방식으로 복제가 가능하다.

``` java
ArrayList list = new ArrayList();
    ...
ArrayList list2 = (ArrayList)list.clone();
```

</br>

### 얇은 복사와 깊은 복사

`clone()`은 단순히 객체에 저장된 값을 그대로 복제할 뿐, 객체가 참조하고 있는 객체까지 복제하지 않는다. 예제9-8에서처럼 기본형 배열인 경우에는 아무런 문제가 없지만, 객체배열을 `clone()`으로 복제하는 경우에는 원본과 복제본이 같은 객체를 공유하므로 완전한 복제라고 보기 어렵다. 이러한 복제(복사)를 '얇은 복사(shallow copy)'라고 한다. 얕은 복사에서는 원본을 변경하면 복사본도 영향을 받는다.

반면에 원본이 참조하고 있는 객체까지 복제하는 것을 '깊은 복사(deep copy)'라고 하며, 깊은 복사에서는 원본과 복사본이 서로 다른 객체를 참조하기 때문에 원본의 변겨잉 복사본에 영향을 미치지 않는다.

예를 들어 `Circle`클래스가 아래와 같이 `Point`타입의 참조변수를 포함하고 있고, `clone()`은 단순히 `Object`클래스의 `clone()`을 호출하도록 정의되어 있을 때,

``` java
class Circle implements Cloneable {
    Point p;    // 원점 - 참조변수
    double r;   // 반지름

    Circle(Point p, double r) {
        this.p = p;
        this.r = r;
    }

    public Circle clone() {
        Object obj = null;

        try {
            obj = super.clone();    // 조상인 Object의 clone()을 호출한다.
        } catch(CloneNotSupportedException e) {}

        return (Circle)obj;
    }
}
```

`Circle`인스턴스 `c1`을 생성하고, `clone()`으로 복제해서 `c2`를 생성하면,

``` java
Circle c1 = new Circle(new Point(1, 1), 2.0);
Circle c2 = c1.clone(); // 얕은 복사
```

아래의 왼쪽 그림처럼, `c1`과 `c2`는 같은 `Point`인스턴스를 가리키게 외므로 완전한 복제라고 볼 수 없다.

![image](https://ifh.cc/g/OdTVZL.png)

위의 오른쪽 그림처럼 `c1`과 `c2`가 각각의 `Point`인스턴스를 가리키도록 해보겠다.

예제 9-9 / ch9 / ShallowDeepCopy.java

``` java
class Circle implements Cloneable {
	Point2 p; // 원점
	double r;	// 반지름
	
	Circle(Point2 p, double r) {
		this.p = p;
		this.r = r;
	}
	
	public Circle shallowCopy() {	// 얕은 복사
		Object obj = null;
		
		try {
			obj = super.clone();
		} catch (CloneNotSupportedException e) {}
		return (Circle)obj;
	}
	
	public Circle deepCopy() {	// 깊은 복사
		Object obj = null;
		
		try {
			obj = super.clone();
		} catch (CloneNotSupportedException e) {}
		
		Circle c = (Circle)obj;
		c.p = new Point2(this.p.x, this.p.y);
		
		return c;
	}
	
	public String toString() {
		return "[p = " + p + ", r = " + r + "]";
	}
}

class Point2 {
	int x, y;
	
	Point2(int x, int y) {
		this.x = x;
		this.y = y;
	}
	
	public String toString() {
		return "(" + x + ", " + y + ")";
	}
}

public class ShallowDeepCopy {
	public static void main(String[] args) {
		Circle c1 = new Circle(new Point2(1, 1), 2.0);
		Circle c2 = c1.shallowCopy();
		Circle c3 = c1.deepCopy();
		
		System.out.println("c1 = " + c1);
		System.out.println("c2 = " + c2);
		System.out.println("c3 = " + c3);
		
		c1.p.x = 9;
		c1.p.y = 9;
		System.out.println("= c1의 변경 후 = ");
		System.out.println("c1 = " + c1);
		System.out.println("c2 = " + c2);
		System.out.println("c3 = " + c3);
	}
}
```

```
c1 = [p = (1, 1), r = 2.0]
c2 = [p = (1, 1), r = 2.0]
c3 = [p = (1, 1), r = 2.0]
= c1의 변경 후 = 
c1 = [p = (9, 9), r = 2.0]
c2 = [p = (9, 9), r = 2.0]
c3 = [p = (1, 1), r = 2.0]
```

인스턴스 `c1`을 생성한 후에 얕은 복사로 `c2`를 생성하고, 깊은 복사로 `c3`를 생성하였다.

``` java
Circle c1 = new Circle(new Point2(1, 1), 2.0);
Circle c2 = c1.shallowCopy();
Circle c3 = c1.deepCopy();
```

위 상황을 그림으로 표현하면 다음과 같다.

![image](https://ifh.cc/g/ZodllD.png)

그 다음에 `c1`이 가리키고 있는 `Point`인스턴스의 `x`와 `y`의 값을 9로 변경한다.

``` java
c1.p.x = 9;
c1.p.y = 9;
```

`c1`을 변경했을 뿐인데, `c2`도 영향을 받는다. 그러나 `c3`는 전혀 영향을 받지 않는다.

![image](https://ifh.cc/g/ljkLcm.png)

`shallowCopy()`의 내용을 보면, 단순히 `Object`클래스의 `clone()`을 호출할 뿐이다.

``` java
public Circle shallowCopy() {	// 얕은 복사
	Object obj = null;

	try {
		obj = super.clone();
	} catch(CloneNotSupportedException e) {}

	return (Circle)obj;
}
```

`Object`클래스의 `clone()`은 원본 객체가 가지고 있는 값만 그대로 복사한다. 즉 얕은 복사를 한다.

``` java
Circle c = (Circle)obj;
c.p = new Point(this.p.x, this.p.y);
```

`deepCopy()`는 `shallowCopy()`에 위의 두 줄을 추가하여, 복제된 객체가 새로운 `Point`인스턴스를 참조하도록 했다. 원본이 참조하고 있는 객체까지 복사한 것이다.

</br>

### getClass()

이 메소드는 자신이 속한 클래스의 `Class`객체를 반환하는 메소드인데, `Class`객체는 이름이 'Class'인 클래스의 객체이다. `Class`클래스는 아래와 같이 정의되어 있다.

``` java
public final class Calss implements ... {	// Class클래스
	...
}
```

`Class`객체는 클래스의 모든 정보를 담고 있으며, 클래스 당 1개만 존재한다. 그리고 클래스파일이 '클래스 로더(ClassLoader)'에 의해서 메모리에 올라갈 때, 자동으로 생성된다.

클래스 로더는 실행 시에 필요한 클래스를 도엊ㄱ으로 메모리에 로드하는 역할을 한다. 먼저 기존에 생성된 클래스 객체가 메모리에 존재하는지 확인하고, 있으면 객체의 참조를 반환하고 없으면 클래스 패스(classpath)에 지정된 경로를 따라서 클래스 파일을 찾는다.

못 찾으면 `ClassNotFoundException`이 발생하고, 찾으면 해당 클래스 파일을 읽어서 `Class`객체로 변환한다.

그러니까 파일 형태로 저장되어 있는 클래스를 읽어서 `Class`클래스에 정의된 형식으로 변환하는 것이다. 즉, 클래스 파일을 읽어서 사용하기 편한 형태로 저장해 놓은 것이 클래스 객체이다.

> 클래스 파일을 메모리에 로드하고 변환하는 일은 클래스 로더가 한다.

</br>

### Class객체를 얻는 방법

클래스의 정보가 필요할 때, 먼저 `Class`객체에 대한 참조를 얻어 와야 하는데, 해당 `Class`객체에 대한 참조를 얻는 방법은 여러 가지가 있다.

``` java
class cObj = new Card().getClass;	// 생성된 객체로 부터 얻는 방법
class cObj = Card.class;	// 클래스 리터럴(*.class)로 부터 얻는 방법
class cObj = Class.forName("Card");	// 클래스 이름으로 부터 얻는 방법
```

특히 `forName()`은 특정 클래스 파일, 예를 들어 데이터베이스 드라이버를 메모리에 올릴 때 주로 사용한다.

`Class`객체를 이용하면 클래스에 정의된 멤버의 이름이나 개수 등, 클래스에 대한 모든 정보를 얻을 수 있기 때문에 `Class`객체를 통해서 객체를 생성하고 메소드를 호출하는 등 보다 동적인 코드를 작성할 수 있다.

``` java
Card c = new Card();	// new연산자를 이용해서 객체 생성
Card c = Card.class.newInstanec();	// Class객체를 이용해서 객체 생성
```

> newInstance()는 InstantiationException이 발생할 수 있으므로 예외처리가 필요하다.

예제 9-10 / ch9 / ClassEx1.java

``` java
final class Card3 {
	String kind;
	int num;
	
	Card3() {
		this("SPADE", 1);
	}
	
	Card3(String kind, int num) {
		this.kind = kind;
		this.num = num;
	}
	
	public String toString() {
		return kind + ":" + num;
	}
}

public class ClassEx1 {
	public static void main(String[] args) throws Exception {
		Card3 c = new Card3("HEART", 3);	// new연산자로 객체 생성
		Card3 c2 = Card3.class.newInstance();	// Class객체를 통해서 객체 생성
		
		Class cObj = c.getClass();
		
		System.out.println(c);
		System.out.println(c2);
		System.out.println(cObj.getName());
		System.out.println(cObj.toGenericString());
		System.out.println(cObj.toString());
	}
}
```

```
HEART:3
SPADE:1
Card3
final class Card3
class Card3
```

</br>

### 1.2 String클래스

기존의 다른 언어에서는 문자열을 char형의 배열로 다루었으나 자바에서는 문자열을 위한 클래스를 제공한다. 그것이 바로 `String`클래스인데, `String`클래스는 문자열을 저장하고 이를 다루는데 필요한 메소드를 함께 제공한다.

</br>

### 변경 불가능한(immutable) 클래스

`String`클래스에는 문자열을 저장하기 위해서 문자형 배열 참조변수(char[]) `value`를 인스턴스 변수로 정의해놓고 있다. 인스턴스 생성 시 생성자의 매개변수로 입력받는 문자열은 이 인스턴스변수(`value`)에 문자열 배열(char[])로 저장된다.

> String클래스는 앞에 final이 붙어 있으므로 다른 클래스의 조상이 될 수 없다.

``` java
public fianl class String implements java.io.Serializable, Comparable {
	private char[] value;
		...
}
```

한번 생성된 `String`인스턴스가 갖고 있는 문자열은 읽어올 수만 있고, 변경할 수는 없다.

예를 들어 아래의 코드와 같이 '+'연산자를 이용해서 문자열을 결합하는 경우 인스턴스내의 문자열이 바뀌는 것이 아니라 새로운 문자열("ab")이 담긴 `String`인스턴스가 생성되는 것이다.

![image](https://ifh.cc/g/ZcCVpw.png)

이처럼 덧셈연산자 '+'를 사용해서 문자열을 결합하는 것은 매 연산 시 마다 새로운 문자열을 가진 `String`인스턴스가 생성되어 메모리공간을 차지하게 되므로 가능한 결합횟수를 줄이는 것이 좋다.

문자열간의 결합이나 추출 등 문자열을 다루는 작업이 많이 필요한 경우에는 `String`클래스 대신 `StringBuffer`클래스를 사용하는 것이 좋다. `StringBuffer`인스턴스에 저장된 문자열은 변경이 가능하므로 하나의 `StringBuffer`인스턴스만으로도 문자열을 다루는 것이 가능하다.

</br>

### 문자열 비교

문자열을 만들 때는 두 가지 방법, 문자열 리터럴을 지정하는 방법과 `String`클래스의 생성자를 사용해서 만드는 방법이 있다.

``` java
String str1 = "abc";	// 문자열 리터럴 "abc"의 주소가 str1에 저장됨
String str2 = "abc";	// 문자열 리터럴 "abc"의 주소가 str2에 저장됨
String str3 = new String("abc");	// 새로운 String인스턴스를 생성
String str4 = new String("abc");	// 새로운 String인스턴스를 생성
```

`String`클래스의 생성자를 이용한 경우에는 `new`연산자에 의해서 메모리할당이 이루어지기 때문에 항상 새로운 `String`인스턴스가 생성된다. 그러나 문자열 리터럴은 이미 존재하는 것을 재사용하는 것이다.

> 문자열 리터럴은 클래스가 메모리에 로드될 때 자동적으로 미리 생성된다.

![image](https://ifh.cc/g/oWP2S5.png)

`equals()`를 사용했을 때는 두 문자열의 내용("abc")을 비교하기 때문에 두 경우 모두 `true`를 결과로 얻는다. 하지만, 각 `String`인스턴스의 주소를 등가비교연산자 `==`로 비교했을 떄는 결과가 다르다.

예제 9-11 / ch9 / StringEx1.java

``` java
public class SringEx1 {
	public static void main(String[] args) {
		String str1 = "abc";
		String str2 = "abc";
		System.out.println("String str1 = \"abc\";");
		System.out.println("String str2 = \"abc\";");
		
		System.out.println("str1 == str2 ? " + (str1 == str2));
		System.out.println("str1.equals(str2) ? " + str1.equals(str2));
		System.out.println();
		
		String str3 = new String("\"abc\"");
		String str4 = new String("\"abc\"");
		
		System.out.println("String str3 = new String(\"abc\");");
		System.out.println("String str4 = new String(\"abc\");");
		
		System.out.println("str3 == str4 ? " + (str3 == str4));
		System.out.println("str3.equals(str4) ? " + str3.equals(str4));
	}
}
```

```
String str1 = "abc";
String str2 = "abc";
str1 == str2 ? true
str1.equals(str2) ? true

String str3 = new String("abc");
String str4 = new String("abc");
str3 == str4 ? false
str3.equals(str4) ? true
```

</br>

### 문자열 리터럴

자바 소스파일에 포함된 모든 문자열 리터럴은 컴파일 시에 클래스 파일에 저장된다. 이 때 같은 내용의 문자열 리터럴은 한번만 저장된다. 문자열 리터럴도 `String`인스턴스이고, 한번 생성하면 내용을 변경할 수 없으니 하나의 인스턴스를 공융하면 된다.

예제 9-12 / ch9 / StringEx2.java

``` java
public class StringEx2 {
	public static void main(String[] args) {
		String s1 = "AAA";
		String s2 = "AAA";
		String s3 = "AAA";
		String s4 = "BBB";
	}
}
```

String리터럴들은 컴파일시에 클래스파일에 저장된다.

그래서 위의 예제를 실행하면 "AAA"를 담고 있는 `String`인스턴스가 하나 생성된 후, 참조변수 `s1`, `s2`, `s3`는 모두 이 `String`인스턴스를 참조하게 된다.

![image](https://ifh.cc/g/cYw2hd.png)

클래스 파일에는 소스파일에 포함된 모든 리터럴의 목록이 있다. 해당 클래스 파일이 클래스 로더에 의해 메모리에 올라갈 때, 이 리터럴의 목록에 있는 리터럴들이 JVM내에 있는 '상수 저장소(constant pool)'에 저장된다. 이 때, 이곳에 "AAA"와 같은 문자열 리터럴이 자동적으로 생성되어 저장되는 것이다.

</br>

### 빈 문자열(empty string)

char형 배열도 길이가 0인 배열을 생성할 수 있고, 이 배열을 내부적으로 가지고 있는 문자열이 바로 빈 문자열이다.

`String s = "";`과 같은 문장이 있을 때, 참조변수 `s`가 참조하고 있는 `String`인스턴스는 내부에 `new char[0]`과 같이 길이가 0인 char형 배열을 저장하고 있는 것이다.

``` java
char[] chArr = new char[0];	// 길이가 0인 char배열
int[] iArr = {};	// 길이가 0인 int배열
```

길이가 0이기 때문에 아무런 문자도 저장할 수 없는 배열이라 무의미하게 느껴지겠지만 어쨋든 이러한 표현이 가능하다.

그러나 `String s == "":`과 같은 표현이 가능하다고 해서 `char c = "";`와 같은 표현도 가능한 것은 아니다. char형 변수에는 반드시 하나의 문자를 지정해야한다.

![image](https://ifh.cc/g/YRWWkS.png)

일반적으로 변수를 선언할 때, 각 타입의 기본값으로 초기화 하지만 String은 참조형 타입의 기본값인 `null`보다는 빈 문자열로, char형은 기본값인 `\u0000` 대신 공백으로 초기화 하는 것이 보통이다.

>  '\u0000'은 유니코드의 첫 번째 문자로써 아무런 문자도 지정되지 않은 빈 문자이다.

예제 9-13 / ch9 / StringEx3.java

``` java
public class StringEx3 {
	public static void main(String[] args) {
		// 길이가 0인 char배열을 생성한다.
		char[] cArr = new char[0];	// char[] cArr = {};와 같다.
		String s = new String(cArr);	// String s = new String("");와 같다.
		
		System.out.println("cArr.length = " + cArr.length);
		System.out.println("@@@" + s + "@@@");
	}
}
```

```
cArr.length = 0
@@@@@@
```

길이가 0인 배열을 생성해서 char형 배열 참조변수 `cArr`를 초기화 해주었다. 길이가 0이긴 해도 배열이 생성되며 생성된 배열의 주소값이 참조변수 `cArr`에 저장된다.

</br>

### String클래스의 생성자와 메소드

아래의 표는 `String`클래스 내에 정의된 생성자와 메소드의 목록이다. 전체 목록은 아니고, 자주 사용될만한 것들만 뽑았는데도 거의 다 포함되었다.

![image](https://ifh.cc/g/GpKRQk.png)

> CharSequence는 JDK1.4부터 추가된 인터페이스로 String, StringBuffer 등의 클래스가 구현하였다.

> contains(CharSequence s), replace(CharSequence old, CharSequence nw)는 JDK1.5부터 추가되었다.

> java.util.Date dd = new java.util.Date()에서 생성된 Date인스턴스는 현재 시간을 갖는다.

</br>

### join()과 StringJoiner

`join()`은 여러 문자열 사이에 구분자를 넣어서 결합한다. 구분자로 문자열을 자르는 `split()`과 반대의 작업을 한다고 생각하면 이해하기 쉽다.

``` java
String animals = "dog,cat,bear";
String[] arr = animals.split(",");	// 문자열을 ','를 구분자로 나눠서 배열에 저장
String str = String.join("-", arr);	// 배열의 문자열을 '-'로 구분해서 결합
System.out.println(str);	// dog-cat-bear
```

`java.util.StringJoiner`클래스를 사용해서 문자열을 결합할 수도 있는데, 사용하는 방법은 간단하다.

``` java
StringJoiner sj = new StringJoiner(",", "[", "]");
String[] strArr = { "aaa", "bbb", "ccc" };

for(String s : strArr)
	sj.add(s.toUpperCase());

System.out.println(sj.toString());	// [AAA,BBB,CCC]
```

> join()과 java.util.StringJoiner는 JDK1.8부터 추가되었다.

예제 9-14 / ch9 / StringEx4.java

``` java
import java.util.StringJoiner;

public class StringEx4 {
	public static void main(String[] args) {
		String animals = "dog,cat,bear";
		String[] arr = animals.split(",");
		
		System.out.println(String.join("-", arr));
		
		StringJoiner sj = new StringJoiner("/", "[", "]");
		for(String s : arr)
			sj.add(s);
		
		System.out.println(sj.toString());
	}
}
```

```
dog-cat-bear
[dog/cat/bear]
```

</br>

### 유니코드의 보충문자

위 표의 메소드 중에 매개변수의 타입이 char인 것들이 있고, int인 것들도 있다. 매개변수의 타입이 int인 이유는 확장된 유니코드를 다루기 위해서이다.

유니코드는 원래 2 byte, 즉 16비트 문자체계인데, 이걸로도 모자라서 20비트로 확장하게 되었다. 그래서 하나의 문자를 char타입으로 다루지 못하고, int타입으로 다룰 수 밖에 없다. 확장에 의해 새로 추가된 문자들을 '보충 문자(supplementray character)'라고 하는데, `String`클래스의 메소드 중에서는 보충 문자를 지우너하는 것이 있고 지원하지 않는 것도 있다. 매개변수가 `int ch`인 것들은 보충문자를 지원하는 것이고, `char ch`인 것들은 지원하지 않는 것들이다.

</br>

### 문자 인코딩 변환

`getBytes(String charsetName)`를 사용하면, 문자열의 문자 인코딩을 다른 인코딩으로 변경할 수 있다. 자바가 UTF-16을 사용하지만, 문자열 리터럴에 포함되는 문자들은 OS의 인코딩을 사용한다. 한글 윈도우즈의 경우 문자 인코딩으로 CP949를 사용하며, UTF-8로 변경하려면, 아래와 같이 한다.

> 사용가능한 문자 인코딩 목록은 'System.out.println(java.nio.charse.Charset.availableCharsets());'로 모두 출력할 수 있다.

``` java
byte[] utf8_str = "가".getBytes("UTF-8");	// 문자열을 UTF-8로 변환
String str = new String(utf8_str, "UTF-8");	// byte배열을 문자열로 변환
```

서로 다른 문자 인코딩을 사용하는 컴퓨터 간에 데이터를 주고받을 때는 적절한 문자 인코딩이 필요하다. 그렇지 않으면 알아볼 수 없는 내용의 문서를 보게 된다.

예제 9-15 / ch9 / StringEx5.java

``` java
import java.util.StringJoiner;

public class StringEx5 {
	public static void main(String[] args) throws Exception {
		String str = "가";
		
		byte[] bArr = str.getBytes("UTF-8");
		byte[] bArr2 = str.getBytes("CP949");
		
		System.out.println("UTF-8 : " + joinByteArr(bArr));
		System.out.println("CP949 : " + joinByteArr(bArr2));
		
		System.out.println("UTF-8 : " + new String(bArr, "UTF-8"));
		System.out.println("CP949 : " + new String(bArr2, "CP949"));
	}
	
	static String joinByteArr(byte[] bArr) {
		StringJoiner sj = new StringJoiner(":", "[", "]");
		
		for(byte b : bArr)
			sj.add(String.format("%02X", b));
		return sj.toString();
	}
}
```

```
UTF-8 : [EA:B0:80]
CP949 : [B0:A1]
UTF-8 : 가
CP949 : 가
```

</br>

### String.format()

`format()`은 형식화된 문자열을 만들어내는 간단한 방법이다. `printf()`하고 사용법이 완전히 똑같다.

``` java
String str = String.format("%d 더하기 %d는 %d입니다.", 3, 5, 3 + 5);
System.out.println(str);	// 3 더하기 5는 8입니다.
```

</br>

### 기본형 값을 String으로 변환

기본형을 문자열로 변경하는 방법은 숫자에 빈 문자열 ""을 더해주기만 하면 된다. 이 외에도 `valueOf()`를 사용하는 방법도 있다. 성능은 `valueOf()`가 더 좋지만, 빈 문자열을 더하는 방법이 간단하고 편하기 때문에 성능향상이 필요한 경우에만 `valueOf()`를 쓰면 된다.

``` java
int i = 100;
String str1 = i + "";	// 100을 "100"으로 변환하는 방법1
String str2 = String.valueOf(i);	// 100을 "100"으로 변환하는 방법2
```

> 참조변수에 String을 더하면, 참조변수가 가리키는 인스턴스의 toString()을 호출하여 String을 얻은 다음 결합한다.

</br>

### String을 기본형 값으로 변환

반대로 `String`을 기본형으로 변환하는 방법도 간단하다. `valueOf()`를 쓰거나 `parseInt()`를 사용하면 된다.

``` java
int i = Integer.parseInt("100");	// "100"을 100으로 변환하는 방법1
int i2 = Integer.valueOf("100");	// "100"을 100으로 변환하는 방법2
```

원래 `valueOf()`의 반환 타입은 int가 아니라 Integer인데, 오토박싱(auto-boxing)에 의해 Integer가 int로 자동 변환된다.

``` java
Interger i2 = Integer.valueOf("100");	// 원래의 반환 타입이 Interger
```

예전에는 `parseInt()`와 같은 메소드를 많이 썼는데, 메소드의 이름을 통일하기 위해 `valueOf()`가 나중에 추가되었다. `valueOf(String s)`는 메소드 내부에서 그저 `parseInt(String s)`를 호출할 뿐이므로, 두 메소드는 반환 타입만 다르지 같은 메소드이다.

``` java
public static Integer valueOf(String s) throws NumberFormatException {
	return Interger.valueOf(parseInt(s, 10));	// 여기서 10은 10진수를 의미
}
```

기본형과 문자열간의 변환방법을 정리하면 다음과 같다.

![image](https://ifh.cc/g/nYmsFT.png)

> byte, short을 문자열로 변경할 때는 String valueOf(int i)를 사용하면 된다.

> 문자열 "A"를 문자 'A'로 변환하려면 char ch = "A".charAt(0);과 같이 하면 된다.

Boolean, Byte와 같이 기본형 타입의 이름의 첫 글자가 대문자인 것은 래퍼 클래스(wrapper class)이다. 기본형 값을 감싸고 있는 클래스라는 뜻에서 붙여진 이름으로 기본형을 클래스로 표현한 것이다.

예제 9-16 / ch9 / StringEx6.java

``` java
public class StringEx6 {
	public static void main(String[] args) {
		int iVal = 100;
		String strVal = String.valueOf(iVal);	// int를 String으로 변환한다.
		
		double dVal = 200.0;
		String strVal2 = dVal + "";	// String으로 변환하는 또 다른 방법
		
		double sum = Integer.parseInt("+" + strVal) + Double.parseDouble(strVal2);
		
		double sum2 = Integer.valueOf(strVal) + Double.valueOf(strVal2);
		
		System.out.println(String.join("", strVal, "+", strVal2, "=") + sum);
		System.out.println(strVal + "+" + strVal2 + "=" + sum2);
	}
}
```

```
100+200.0=300.0
100+200.0=300.0
```

이 예제는 문자열과 기본형간의 변환의 예를 보여준다. `parseInt()`나 `parseFloat()`같은 메소드는 문자열에 공백 또는 문자가 포함되어 있는 경우 변환 시 예외(NumberFormatException)가 발생할 수 있으므로 주의해야 한다. 그래서 문자열 양끝의 공백을 제거해주는 `trim()`을 습관적으로 같이 사용하기도 한다.

``` java
int val = Integer.parseInt(" 123 ".trim());	// 문자열 양 끝의 공백을 제거 후 변환
```

그러나 부호를 의미하는 '+'나 소수점을 의미하는 '.'와 float형 값을 뜻하는 f와 같은 자료형 접미사는 허용된다. 단, 자료형에 알맞은 변환을 하는 경우에만 허용된다.

> '+'가 포함된 문자열이 parseInt()로 변환가능하게 된 것은 JDK1.7부터이다.

> Integer클래스의 static int parseInt(String s, int radix)를 사용하면 16진수 값으로 표현된 문자열도 변환할 수 있기 때문에 대소문자 구별 없이 a, b, c, d, e, f도 사용할 수 있따. int result = Integer.parseInt("a", 16);의 경우 result에는 정수 값 10이 저장된다.(16진수 a는 10진수로는 10을 뜻한다.)

예제 9-17 / ch9 / StringEx7.java

``` java
public class StringEx7 {
	public static void main(String[] args) {
		String fullName = "Hello.java";
		
		// fullName에서 '.'의 위치를 찾는다.
		int index = fullName.indexOf('.');
		
		// fullName의 첫번째 글자부터 '.'이 있는 곳까지 문자열을 추출한다.
		String fileName = fullName.substring(0, index);
		
		// '.'의 다음 문자부터 시작해서 문자열의 끝까지 추출한다.
		// fullName.substring(index + 1, fullName.length());의 결과와 같다.
		String ext = fullName.substring(index + 1);
		
		System.out.println(fullName + "의 확장자를 제외한 이름은 " + fileName);
		System.out.println(fullName + "의 확장자는 " + ext);
	}
}
```

```
Hello.java의 확장자를 제외한 이름은 Hello
Hello.java의 확장자는 java
```

위 예제는 `substring`메소드를 이용하여 한 문자열에서 내요으이 일부를 추출하는 예이다. `substring(int start, int end)`를 사용할 때 주의해야 할 점은 매개변수로 사용되는 문자열에서 각 문자의 위치를 뜻하는 index가 0부터 시작한다는 것과 `strat`부터 `end`의 범위 중 `end`위치에 있는 문자는 결과에 포함되지 않는다.

> end에서 start값을 빼면 substring에 의해 추출될 글자의 수가 된다.

> substring이 철자에 주의해야 한다. subString이 아니다.

![image](https://ifh.cc/g/FK0s02.png)

![image](https://ifh.cc/g/dQ57nR.png)

</br>

## 1.3 StringBuffer클래스와 StringBuilder클래스

`String`크랠스는 인스턴스를 생성할 때 지정된 문자열을 변경할 수 없지만 `StringBuffer`클래스는 변경이 가능하다. 내부적으로 문자열 편집을 위한 버퍼(buffer)를 가지고 있으며, `StringBuffer`인스턴스를 생성할 때 그 크기를 지정할 수 있다.

이 때, 편집할 문자열의 길이를 고려하여 버퍼의 길이를 충분히 잡아주는 것이 좋다. 편집 중인 문자열이 버퍼의 길이를 넘어서게 되면 버퍼의 길이를 늘려주는 작업이 추가로 수행되어야하기 때문에 작업효율이 떨어진다.

`StringBuffer`클래스는 `String`클래스와 같이 문자열을 저장하기 위한 char형 배열의 참조변수를 인스턴스변수로 선언해 놓고 있다. `StringBuffer`인스턴스가 생성될 때, char형 배열이 생성되며 이 때 생성된 char형 배열을 인스턴스변수 `value`가 참조하게 된다.

``` java
public final class StringBuffer implements java.io.Serializable {
	private char[] value;
		...
}
```

</br>

### StringBuffer의 생성자

`StringBuffer`클래스의 인스턴스를 생성할 때, 적절한 길이의 char형 배열이 생성되고, 이 배열은 문자열을 저장하고 편집하기 위한 공간(buffer)으로 사용된다.

`StringBuffer`인스턴스를 생성할 때는 생성자 `StringBuffer(int length)`를 사용해서 `StringBuffer`인스턴스에 저장될 문자열의 길이를 고려하여 충분히 여유있는 크기로 지정하는 것이 좋다. `StringBuffer`인스턴스를 생성할 때, 버퍼의 크기를 지정해주지 않으면 16개의 문자를 저장할 수 있는 크기의 버퍼를 생성한다.

``` java
public StringBuffer(int length) {
	value = new char[length];
	shared = false;
}

public StringBuffe() {
	this(16);	// 버퍼의 크기를 지정하지 않으면 버퍼의 크기는 16이 된다.
}

public StringBuffer(String str) {
	this(str.length() + 16);	// 지정한 문자열의 길이보다 16이 더 크게 버퍼를 생성한다.
	append(str);
}
```

아래의 코드는 `StringBuffer`클래스의 일부인데, 버퍼의 크기를 변경하는 내용의 코드이다. `StringBuffer`인스턴스로 문자열을 다루는 작업을 할 때, 버퍼의 크기가 작업하려는 문자열의 길이보다 작을 때는 내부적으로 버퍼의 크기를 증가시키는 작업이 수행된다.

배열의 길이는 변경될 수 없으므로 새로운 길이의 배열을 생성한 후에 이전 배열의 값을 복사해야 한다.

``` java
...
// 새로운 길이(newCapacity)의 배열을 생성한다. newCapacity는 정수값이다.
char newValue[] = new char[newCapacity];

// 배열 value의 내용을 배열 newValue로 복사한다.
System.out.arraycopy(value, 0, newValue, 0, count);	// count는 문자열의 길이
value = newValue;	// 새로 생성된 배열의 주소를 참조변수 value에 저장
```

이렇게 함으로써 `StringBuffer`클래스의 인스턴스변수 `value`는 길이가 증가된 새로운 배열을 참조하게 된다.

</br>

### StringBuffer의 변경

`String`과 달리 `StringBuffer`는 내용을 변경할 수 있다. 예를 들어 아래와 같이 `StringBuffer`를 생성하였다고 가정하겠다.

![image](https://ifh.cc/g/3K2M5t.png)

그리고 `sb`에 문자열 "123"을 추가하면,

![image](https://ifh.cc/g/jXRKTW.png)

`append()`는 반환타입이 `StringBuffer`인데 자신의 주소를 반환한다. 그래서 아래와 같은 문장이 수행되면, `sb`에 새로운 문자열이 추가되고 `sb`자신의 주소를 반환하여 `sb2`에는 `sb`의 주소인 0x100이 저장된다.

![image](https://ifh.cc/g/rkJzzG.png)

`sb`와 `sb2`가 모두 같은 `StringBuffer`인스턴스를 가리키고 있으므로 같은 내용이 출력된다. 그래서 하나의 `StringBuffer`인스턴스에 대해 아래와 같이 연속적으로 `append()`를 호출하는 것이 가능하다.

![image](https://ifh.cc/g/8dVwBn.png)

오른쪽 코드의 밑줄 친 부분이 `sb`이므로 여기에 다시 `append()`를 호추할 수 있는 것이다. 만일 `append()`의 반환타입이 `void`라면 이렇게 할 수 없다.

> StringBuffer클래스에는 append()처럼 객체 자신을 반환하는 메소드들이 많이 있다.

</br>

### StringBUffer의 비교

`String`클래스에서는 `equals`메소드를 오버라이딩해서 문자열의 내용을 비교하도록 구현되어 있지만, `StringBuffer`클래스는 `equals`메소드를 오버라이딩하지 않아서 `StringBuffer`클래스의 `equals`메소드를 사용해도 등가비교연산자(==)로 비교한 것과 같은 결과를 얻는다.

``` java
StringBuffer sb = new StringBuffer("abc");
StringBuffer sb2 = new StringBuffer("abc");

System.out.println(sb == sb2);	// false
System.out.println(sb.equals(sb2));	// false
```

반면에 `toString()`은 오버라이딩되어 있어서 `StringBuffer`인스턴스에 `toString()`을 호출하면, 담고있는 문자열을 `String`으로 변환한다.

그래서 `StringBuffer`인스턴스에 담긴 문자열을 비교하기 위해서는 `StringBuffer`인스턴스에 `toString()`을 호출해서 `String`인스턴스를 얻은 다음, 여기에 `equals`메소드를 사용해서 비교해야한다.

``` java
String s = sb.toString();
String s2 = sb2.toString();

System.out.println(s.equals(s2));	// true
```

예제 9-18 / ch9 / StringBufferEx1.java

``` java
public class StringBufferEx1 {
	public static void main(String[] args) {
		StringBuffer sb = new StringBuffer("abc");
		StringBuffer sb2 = new StringBuffer("abc");
		
		System.out.println("sb == sb2 ? " + (sb == sb2));
		System.out.println("sb.equals(sb2) ? " + sb.equals(sb2));
		
		// StringBuffer의 내용을 String으로 변환한다.
		String s = sb.toString();	// String s = new String(sb);와 같다.
		String s2 = sb2.toString();
		
		System.out.println("s.equals(s2) ? " + s.equals(s2));
	}
}
```

```
sb == sb2 ? false
sb.equals(sb2) ? false
s.equals(s2) ? true
```

</br>

### StringBuffer클래스의 생성자와 메소드

`StringBuffer`클래스 역시 문자열을 다루기 위한 것이기 때문에 `String`클래스와 유사한 메소드를 많이 가지고 있다. 그리고 `StringBuffer`는 추가, 변경, 삭제와 같이 저장된 내용을 변경할 수 있는 메소드들이 추가로 제공된다.

![image](https://ifh.cc/g/GO7jR2.png)

예제 9-15 / ch9 / StringBufferEx2.java

``` java
public class StringBufferEx2 {
	public static void main(String[] args) {
		StringBuffer sb = new StringBuffer("01");
		StringBuffer sb2 = sb.append(23);
		sb.append('4').append(56);
		
		StringBuffer sb3 = sb.append(78);
		sb3.append(9.0);
		
		System.out.println("sb = " + sb);
		System.out.println("sb2 = " + sb2);
		System.out.println("sb3 = " + sb3);
		
		System.out.println("sb = " + sb.deleteCharAt(10));
		System.out.println("sb = " + sb.delete(3, 6));
		System.out.println("sb = " + sb.insert(3, "abc"));
		System.out.println("sb = " + sb.replace(6, sb.length(), "END"));
		
		System.out.println("capacity = " + sb.capacity());
		System.out.println("length = " + sb.length());
	}
}
```

```
sb = 0123456789.0
sb2 = 0123456789.0
sb3 = 0123456789.0
sb = 01234567890
sb = 01267890
sb = 012abc67890
sb = 012abcEND
capacity = 18
length = 9
```

</br>

### StringBuilder란?

`StringBuffer`는 멀티쓰레드에 안전(thread safe)하도록 동기화되어 있다. 멀티쓰레드 동기화는 `StringBuffer`의 성능을 떨어뜨린다. 그래서 멀티쓰레드로 작성된 프로그램이 아닌 경우, `StringBuffer`의 동기화는 불필요하게 성능만 떨어뜨리게 된다.

그래서 `StringBuffer`에서 쓰레드의 동기화만 뺀 `StringBuilder`가 새로 추가되었다. `StringBuilder`는 `StringBUffer`와 완전히 똑같은 기능으로 작성되어 있어서, 소스코드에서 `StringBuffer`대신 `StringBuilder`를 사용하도록 바꾸기만 하면 된다.

![image](https://ifh.cc/g/JyOKSf.png)

</br>

## 1.4 Math클래스

`Math`클래스는 기본적인 수학계산에 유용한 메소드로 구성되어 있다.

`Math`클래스의 생성자는 접근 제어자가 private이기 때문에 다른 클래스에서 `Math`인스턴스를 생성할 수 없도록 되어있다. 그 이유는 클래스 내에 인스턴스변수가 하나도 없어서 인스턴스를 생성할 필요가 없기 때문이다. `Math`클래스의 메소드는 모두 static이며, 아래와 같이 2개의 상수만 정의해 놓았다.

``` java
public static final double E = 2.7182818284590452354;	// 자연로그의 밑
public static final double PI = 3.14159265358979323846;	// 원주율
```

</br>

### 올림, 버림, 반올림

소수점 n번째 자리에서 반올림한 값을 얻기 위해서는 `round()`를 사용해야 하는데, 이 메소드는 항상 소수점 첫째자리에서 반올림을 해서 정수값(long)을 결과로 돌려준다.

원하는 자리 수에서 반올림된 값을 얻기 위해서는 간단히 10의 n제곱으로 곱한 후, 다시 곱한 수로 나눠주기만 하면 된다.

![image](https://ifh.cc/g/yl9nqA.png)

만일 정수형 값인 100 또는 100L로 나눈다면, 결과는 정수형 값을 얻게 된다. 위의 경우 100.0대신 100으로 나누다면, 90이라는 정수값을 결과로 얻게 된다. 정수형간의 연산에서는 반올림이 이루어지지 않는다.

예제 9-20 / ch9 / MathEx1.java

``` java
import static java.lang.Math.*;
import static java.lang.System.*;

public class MathEx1 {
	public static void main(String[] args) {
		double val = 90.7552;
		out.println("round(" + val + ") = " + round(val));	// 반올림
		
		val *= 100;
		out.println("round(" + val + ") = " + round(val));	// 반올림
		
		out.println("round(" + val + ") / 100 = " + round(val) / 100);	// 반올림
		out.println("round(" + val + ") / 100.0 = " + round(val) / 100.0);	// 반올림
		out.println();
		out.printf("ceil(%3.1f) = %3.1f%n", 1.1, ceil(1.1));	// 올림
		out.printf("floor(%3.1f) = %3.1f%n", 1.1, floor(1.1));	// 버림
		out.printf("round(%3.1f) = %d%n", 1.1, round(1.1));	// 반올림
		out.printf("round(%3.1f) = %d%n", 1.5, round(1.5));	// 반올림
		out.printf("rint(%3.1f) = %f%n", 1.5, rint(1.5));	// 반올림
		out.printf("round(%3.1f) = %d%n", -1.5, round(-1.5));	// 반올림
		out.printf("rint(%3.1f) = %f%n", -1.5, rint(-1.5));	// 반올림
		out.printf("ceil(%3.1f) = %f%n", -1.5, ceil(-1.5));	// 올림
		out.printf("floor(%3.1f) = %f%n", -1.5, floor(-1.5));	// 버림
	}
}
```

```
round(90.7552) = 91
round(9075.52) = 9076
round(9075.52) / 100 = 90
round(9075.52) / 100.0 = 90.76

ceil(1.1) = 2.0
floor(1.1) = 1.0
round(1.1) = 1
round(1.5) = 2
rint(1.5) = 2.000000
round(-1.5) = -1
rint(-1.5) = -2.000000
ceil(-1.5) = -1.000000
floor(-1.5) = -2.000000
```

`Math`클래스에 속한 메소드들을 활용하는 예제이다. 코드를 간단히 하기 위해 정적 import문을 추가했다.

``` java
import static java.lang.Math.*;
import static java.lang.System.*;
```

`rint()`도 `round()`처럼 소수점 첫 째자리에서 반올림하지만, 반환값이 double이다.

``` java
out.printf("round(%3.1f) = %d%n", 1.5, round(1.5));	// 반환값이 int
out.printf("rint(%3.1f) = %f%n", 1.5, rint(1.5));	// 반환값이 double
```

그리고 `rint()`는 두 정수의 정가운데 있는 값은 가장 가까운 짝수 정수를 반환한다.

``` java
out.printf("round(%3.1f) = %d%n", -1.5, round(-1.5));	// -1
out.printf("rint(%3.1f) = %f%n", -1.5, rint(-1.5));	// -2.0
```

`round()`는 소수점 첫째자리가 5일 떄, 더 큰 값으로 반올림하니까 -1이 되지만, `rint()`는 -1.5와 같이 홀수(-1.0)와 짝수(-2.0)의 딱 중간에 있는 경우 짝수(-2.0)를 결과로 반환한다. 그리고 음수에서는 양수와 달리 -1.5를 버림(floor)하면 -2.0이 된다.

``` java
out.printf("ceil(%3.1f) = %f%n", -1.5, ceil(-1.5));	// -1.0
out.printf("floor(%3.1f) = %f%n", -1.5, floor(-1.5));	// -2.0
```

</br>

### 예외를 발생시키는 메소드

메소드 이름에 `Exact`가 포함된 메소드들이 JDK1.8부터 새로 추가되었다. 이들은 정수형간의 연산에서 발생할 수 있는 오버플로우(overflow)를 감지하기 위한 것이다.

``` java
int addExact(int x, int y)	// x + y
int subtractExact(int x, int y)	// x - y
int multiplyExact(int x, int y)	// x * y
int incrementExact(int a)	// a++
int decrementExact(int a)	// a--
int negateExact(int a)	// -a
int toIntExact(long value)	// (int)value = int로의 형변환
```

연산자는 단지 결과를 반환할 뿐, 오버플로우의 발생여부에 대해 알려주지 않는다. 그러나 위의 메소드들은 오버플로우가 발생하면, 예외(ArithmeticException)를 발생시킨다.

예제 9-27 / ch9 / MathEx2.java

``` java
import static java.lang.Math.*;
import static java.lang.System.*;

public class MathEx2 {
	public static void main(String[] args) {
		int i = Integer.MIN_VALUE;
		
		out.println("i = " + i);
		out.println("-i = " + (-i));
		
		try {
			out.printf("negateExact(%d) = %d%n", 10, negateExact(10));
			out.printf("negateExact(%d) = %d%n", -10, negateExact(-10));
			out.printf("negateExact(%d) = %d%n", i, negateExact(i));	// 예외 발생
		} catch (ArithmeticException e) {
			// i를 long타입으로 형변환 다음에 negateExact(long a)를 호출
			out.printf("negateExact(%d) = %d%n", (long)i, negateExact((long)i));
		}
	}	// main의 끝
}
```

```
i = -2147483648
-i = -2147483648
negateExact(10) = -10
negateExact(-10) = 10
negateExact(-2147483648) = 2147483648
```

변수 `i`에 int타입의 최소값인 `Integer.MIN_VALUE`를 저장한 다음에, 부호연산자로 `i`의 부호를 반대로 바꾸었다. 그런데, 실행결과에서 `-i`의 값을 보면 부호가 바뀌지 않고 `i`의 값 그대로이다. 정수형의 최소값에 비트전환연산자`~`를 적용하면, 최대값이 되는데 여기에 1을 더하니까 오버플로우가 발생한다.

![image](https://ifh.cc/g/Dm6dgd.png)

그래서 int의 최소값이 다시 원래의 값이 되어버렸다. 예제에서는 try-catch문을 사용해서 오버플로우가 발생하면, `i`를 long타입으로 형변환하여 `negateExact(long a)`를 호출하도록 작성하였다.

실행결과를 보면 오버플로우로 인한 예외가 발생했지만, catch블럭에 의해 예외가 처리되어 올바른 결과가 출력된 것을 확인할 수 있다.

</br>

### 삼각함수와 지수, 로그

예제 9-22 / ch9 / MathEx3.java

``` java
import static java.lang.Math.*;
import static java.lang.System.*;

public class MathEx3 {
	public static void main(String[] args) {
		int x1 = 1, y1 = 1;	// (1, 1)
		int x2 = 2, y2 = 2;	// (2, 2)
		
		double c = sqrt(pow(x2 - x1, 2) + pow(y2 - y1, 2));
		double a = c * sin(PI / 4);	// PI / 4 rad = 45 degree
		double b = c * cos(PI / 4);
//		double b = c * cos(toRadians(45));
		
		out.printf("a = %f%n", a);
		out.printf("b = %f%n", b);
		out.printf("c = %f%n", c);
		out.printf("angle = %f rad%n", atan2(a, b));
		out.printf("angle = %f degree%n%n", atan2(a, b) * 180 / PI);
//		out.printf("angle = %f degree%n%n", toDegrees(atan2(a, b)));
		out.printf("24 * log10(2) = %f%n", 24 * log10(2));	// 7.224720
		out.printf("53 * log10(2) = %f%n%n", 53 * log10(2));	// 15.954590
	}
}
```

```
a = 1.000000
b = 1.000000
c = 1.414214
angle = 0.785398 rad
angle = 45.000000 degree

24 * log10(2) = 7.224720
53 * log10(2) = 15.954590
```

두 점(x1, y1), (x2, y2)간의 거리는 c는 	$\sqrt{(x2-x1)^2+(y2-y1)^2}$로 구할 수 있다.

제곱근을 계산해주는 `sqrt()`와 n제곱을 계산해주는 `pow()`를 사용해서 식을 구성하면 다음과 같다. 

``` java
double c = sqrt(pow(x2-x1, 2) + pow(y2-y1, 2));
```

예제에서 `x1`과 `y1`의 값은 1이고, `x2`와 `y2`의 값은 2니까, 이 값들을 대입하면 다음과 같이 계산된다.

``` java
	double c = sqrt(pow(2-1, 2) + pow(y2-y1, 2));
→	double c = sqrt(pow(1, 2) + pow(1, 2));	// pow(1, 2)는 1의 2제곱
→	double c = sqrt(1.0 + 1.0);
→	double c = sqrt(2.0);
→	double c = 1.414214;
```

![image](https://ifh.cc/g/rBXxHL.png)

a와 b를 구하는 수학공식은 위와 같으며, 이 공식을 자바로 작성하면 다음과 같다.

> Math클래스에는 원주율 PI와 자연로그의 밑인 E가 상수로 정의되어 있다.

``` java
	double a = c * sin(PI / 4);	// PI / 4 rad = 45 degree
	double b = c * cos(PI / 4);
//	double b = c * cos(toRadians(45));	// 각도를 라디안을 변환
```

삼각함수는 매겨변수의 단위가 '라디안(radian)'이므로, 45도를 '라디안(radian)'단위의 값으로 변횐해야 한다. '180˚ * π rad'이므로, '45˚ = π/4 rad'이다. 아니면, `toRadians(double angdeg)`을 이용할 수도 있다. 이 메소드의 반환값은 double이다.

``` java
	out.printf("angle = %f rad%n", atan2(a, b));
	out.printf("angle = %f degree%n%n", atan2(a, b) * 180 / PI);
//	out.printf("angle = %f degree%n%n", toDegrees(atan2(a, b)));
```

`atan2`메소드는 직각 삼각형에서 두 변의 길이 a, b를 알면 끼인각θ를 구해준다. 이 메소드의 결과값 역시 단위가 라디안이므로 도(degree)단위로 변환하려면 '180/PI'를 곱하거나 `toDegrees(double angrad)`를 이용하면 된다.

25자리의 2진수는 10진수로 몇 자리의 값인지를 알아내려면 다음의 식을 풀어야한다.

2<sup>24</sup> = 10<sup>x</sup>

이 식의 양변에 상용로그(log<sub>10</sub>)를 취하면, 다음과 같은 식이 된다.

24 * log<sub>10</sub>2 = x

이 식은 아래와 같이 계산할 수 있으며, 결과는 약 7.2이다. 즉, 24자리의 2진수는 10진수로 7자리의 값을 표현할 수 있다

``` java
	out.printf("24 * log10(2) = %f%n", 24 * log10(2));	// 7.224720
	out.printf("53 * log10(2) = %f%n%n", 53 * log10(2));	// 15.954590
```

그래서 float타입의 정밀도가 7자리인 것이다. 마찬가지로 double타입의 정밀도는 15자리임을 알 수 있다.

> float타입의 가수는 23자리지만, 정규호를 통해 1자리를 더 확보할 수 있으므로 실제로 저장할 수 있는 가수는 24자리이다. double타입 역시 52 + 1 = 53자리이다.

</br>

### StricMath클래스

`Math`클래스는 최대한의 성능을 얻기 위해 JVM이 설치된 OS의 메소드를 호출해서 사용한다 즉, OS에 의존적인 계산을 하고 있다. 예를 들어 부동소수점 계산의 경우, 반올림의 처리방법 설정이 OS마다 다를 수 있기 때문에 자바로 작성된 프로그램임에도 불구하고 컴퓨터마다 결과가 다를 수 있다.

이러한 차이를 없애기 위해 성능은 다소 포기하는 대신, 어떤 OS에서 실행되어도 항상 같은 결과를 얻도록 `Math`클래스를 새로 작성한 것이 `StricMath`클래스이다.

</br>

### Math클래스의 메소드

![image](https://ifh.cc/g/4zGCXy.png)

</br>

## 1.5 래퍼(wrapper)클래스

객체지향 개념에서 모든 것은 객체로 다루어져야 한다. 그러나 자바에서는 8개의 기본형을 객체로 다루지 않는데 이것이 바로 자바가 완전한 객체지향 언어가 아니라는 얘기를 듣는 이유이다. 그 대신 보다 높은 성능을 얻을 수 있었다.

때로는 기본형(primitive type) 변수도 어쩔 수 없이 객체로 다뤄야 하는 경우가 있다. 예를 들면, 매개변수로 객체를 요구할 때, 기본형 값이 아닌 객체로 저장해야할 때, 객체간의 비교가 필요할 때 등등의 경우에는 기본형 값들을 객체로 변환하여 작업을 수행해야 한다.

이 때 사용하는 것이 래퍼(wrapper)클래스이다. 8개의 기본형을 대표하는 8개의 래퍼클래스가 있는데, 이 클래스들을 이용하면 기본형 값을 개겣로 다룰 수 있다.

char형과 int형을 제외한 나머지는 자료형 이름의 첫 글자를 대문자로 한 것이 각 래퍼 클래스의 이름이다.

래퍼 클래스의 생성자는 매개변수로 문자열이나 각 자료형의 값들을 인자로 받는다. 이 때 주의해야 할 것은 생성자의 매개변수로 문자열을 제공할 때, 각 자료형에 알맞은 문자열을 사용해야한다는 것이다. 예를 들어 `new Integer("1.0");`과 같이 하면 `NumberFormatException`이 발생한다.

아래의 코드는 int형의 래퍼 클래스인 `Integer`클래스의 실제코드이다.

``` java
public final class Integer extends Number implements Comparable {
		...
	private int value;
	...
}
```

이처럼 래퍼 클래스들은 객체생성 시에 생성자의 인자로 주어진 각 자료형에 알맞은 값을 내부적으로 저장하고 있으며, 이에 관련된 여러 메소드가 정의되어있다.

![image](https://ifh.cc/g/WOAOk6.png)

예제 9-23 / ch9 / WrapperEx1.java

``` java
public class WrapperEx1 {
	public static void main(String[] args) {
		Integer i = new Integer(100);
		Integer i2 = new Integer(100);
		
		System.out.println("i==i2 ? " + (i==i2));
		System.out.println("i.equals(i2) ? " + i.equals(i2));
		System.out.println("i.compareTo(i2)="+i.compareTo(i2));
		System.out.println("i.toStirng()="+i.toString());
		
		System.out.println("MAX_VALUE="+Integer.MAX_VALUE);
		System.out.println("MIN_VALUE="+Integer.MIN_VALUE);
		System.out.println("SIZE="+Integer.SIZE+" bits");
		System.out.println("BYTES="+Integer.BYTES+" bytes");
		System.out.println("TYPE="+Integer.TYPE);
	}
}
```

```
i==i2 ? false
i.equals(i2) ? true
i.compareTo(i2)=0
i.toStirng()=100
MAX_VALUE=2147483647
MIN_VALUE=-2147483648
SIZE=32 bits
BYTES=4 bytes
TYPE=int
```

래퍼 클래스들은 모두 `equals()`가 오버라이딩되어 있어서 주소값이 아닌 객체가 가지고 있는 값을 비교한다. 그래서 실행결과를 보면 `equals()`를 이용한 두 `Integer`객체의 비교결과가 `true`라는 것을 알 수 있다. 오토박싱이 된다고 해도 `Integer`객체에 비교연산자를 사용할 수 없다. 대신 `compareTo()`를 제공한다.

그리고 `toString()`도 오버라이딩되어 있어서 객체가 가지고 있는 값을 문자열로 변환하여 변환한다. 이 외에도 래퍼 클래스들은 `MAX_VALUE`, `MIN_VALUE`, `SIZE`, `BYTES`, `TYPE`등의 static상수를 공통적으로 가지고 있다.

> BYTES는 JDK1.8부터 추가되었다.

</br>

### Number클래스

이 클래스는 추상클래스로 내부적으로 숫자를 멤버변수로 갖는 래퍼 클래스들의 조상이다. 아래의 그림은 래퍼 클래스의 상속계층도인데, 기본형 중에서 숫자와 관련된 래퍼 클래스들은 모두 `Number`클래스의 자손이다.

![image](https://ifh.cc/g/YfCVhj.png)

그 외에도 `Number`클래스 자손으로 `BigInteger`아 `BigDecimal` 등이 있는데, `BigInteger`는 long으로도 다룰 수 없는 큰 범위의 정수를, `BigDecimal`은 double로도 다룰 수 없는 큰 범위의 부동 소수점수를 처리하기 위한 것으로 연산자의 역할을 대신하는 다양한 메소드를 제공한다.

참고로 `Number`클래스의 실제 소스는 아래와 같다. 객체가 가지고 있는 값을 숫자와 관련된 기본형으로 변환하여 반환하는 메소드들을 정의하고 있다.

``` java
public abstract class Number implements java.io.Serializable {
	public abstract int intValue();
	public abstract long longValue();
	public abstract float floatValue();
	public abstract double doubleValue();

	public byte byteValue() {
		return (byte)intValue();
	}

	public short shortValue() {
		return (short)intValue();
	}
}
```

</br>

### 문자열을 숫자로 변환하기

문자열을 숫자로 변환할 때는 아래의 방법 중 하나를 선택해서 사용하면 된다.

``` java
int i = new Integer("100").intValue();	// floatValue(), longValue(), ...
int i2 = Integer.parseInt("100");	// 주로 이 방법을 많이 사용.
Integer i3 = Integer.valueOf("100");
```

래퍼 클래스의 '타입.parse타입(String s)'형식의 메소드와 '타입.valueOf()'메소드를 정리한 것이다. 둘 다 문자를 숫자로 바꿔주는 일을 하지만, 전자는 반환값이 기본형(primitive type)이고 후자는 반환값이 래퍼 클래스 타입이라는 차이가 있다.

![image](https://ifh.cc/g/OCDQYv.png)

JDK1.5부터 도입된 '오토박싱(autoboxing)' 기능 때문에 반환값이 기본형일 때와 래퍼 클래스일 때의 차이가 없어졌다. 그래서 그냥 구별없이 `valueOf()`를 쓰는 것도 괜찮은 방법이다. 단, 성능은 `valueOf()`가 조금 더 느리다.

![image](https://ifh.cc/g/BzRwy3.png)

문자열이 10진수가 아닌 다른 진법(radix)의 숫자일 때도 변환이 가능하도록 다음과 같은 메소드가 제공된다.

``` java
static int parseInt(String s, int raidx)	// 문자열 s를 radix진법으로 인식
static Integer valueOf(String s, int radix)
```

문자열 "100"이 2진법의 숫자라면 10진수로 4이고, 8진법의 숫자라면 10진수로 64이고, 16진법의 숫자라면 10진수로 256이 된다. 참고로 2진수 100은 100<sub>(2)</sub>와 같이 표기한다.

``` java
	int i4 = Integer.parseInt("100", 2);	// 100(2) -> 4
	int i5 = Integer.parseInt("100", 8);	// 100(8) -> 64
	int i6 = Integer.parseInt("100", 16);	// 100(16) -> 256
	int i7 = Integer.parseInt("FF", 16);	// FF(16) -> 255
//	int i8 = Integer.parseInt("FF");	// NumberFormatException발생
```

16진법에서는 'A~F'의 문자도 허용되므로 `Integer.parseInt("FF", 16)`와 같은 코드가 가능하지만, 진법을 생략하면 10진수로 간주하기 때문에 `Integer.parseInt("FF")`에서는 `NumberFormatException`이 발생한다.

예제 9-24 / ch9 / wrapperEx2.java

``` java
public class WrapperEx2 {
	public static void main(String[] args) {
		int i = new Integer("100").intValue();
		int i2 = Integer.parseInt("100");
		Integer i3 = Integer.valueOf("100");
		
		int i4 = Integer.parseInt("100", 2);	// 100(2) -> 4
		int i5 = Integer.parseInt("100", 8);	// 100(8) -> 64
		int i6 = Integer.parseInt("100", 16);	// 100(16) -> 256
		int i7 = Integer.parseInt("FF", 16);	// FF(16) -> 255
//		int i8 = Integer.parseInt("FF");	// NumberFormatException발생
		
		Integer i9 = Integer.valueOf("100", 2);
		Integer i10 = Integer.valueOf("100", 8);
		Integer i11 = Integer.valueOf("100", 16);
		Integer i12 = Integer.valueOf("FF", 16);
//		Integer i13 = Integer.valueOf("FF");	// NumberFormatException발생
		
		System.out.println(i);
		System.out.println(i2);
		System.out.println(i3);
		System.out.println("100(2) -> "+i4);
		System.out.println("100(8) -> "+i5);
		System.out.println("100(16) -> "+i6);
		System.out.println("FF(16) -> "+i7);
		
		System.out.println("100(2) -> "+i9);
		System.out.println("100(8) -> "+i10);
		System.out.println("100(16) -> "+i11);
		System.out.println("FF(16) -> "+i12);
	}
}
```

```
100
100
100
100(2) -> 4
100(8) -> 64
100(16) -> 256
FF(16) -> 255
100(2) -> 4
100(8) -> 64
100(16) -> 256
FF(16) -> 255
```

</br>

### 오토박싱 & 언박싱(autoboxing & unboxing)

JDK1.5이전에는 기본형과 참조형 간의 연산이 불가능했기 때문에, 래퍼 클래스로 기본형을 객체로 만들어서 연산해야 했다.

``` java
int i = 5;
Integer iObj = new Integer(7);

int sum = i + iObj;	// 에러. 기본형과 참조형 간의 덧셈 불가(JDK1.5 이전)
```

그러나 이제는 기본형과 참조형 간의 덧셈이 가능하다. 자바 언어의 규칙이 바뀐 것은 아니고, 컴파일러가 자도응로 변환하는 코드를 넣어주기 때문이다. 아래의 경우, 컴파일러가 `Integer`객체를 int타입의 값으로 변환해주는 `intValue()`를 추가해준다.

![image](https://ifh.cc/g/9d9VVz.png)

이 외에도 내부적으로 객체 배열을 가지고 있는 `Vector`클래스나 `ArrayList`클래스에 기본형 값을 저장해야할 때나 형변환이 필요할 때도 컴파일러가 자동적으로 코드를 추가해 준다. 기본형 값을 래퍼 클래스의 객체로 자동 형변환해주는 것을 '오토박싱(autoboxing)'이라고 하고, 반대로 변환하는 것을 '언박싱(unboxing)'이라고 한다.

``` java
ArrayList<Integer> list = new ArrayList<Integer>();
list.add(10);	// 오토박싱. 10 → new Integer(10)

int value = list.get(0);	// 언박싱. new Integer(10) → 10
```

위의 코드에서 알 수 있듯이 `ArrayList`에 숫자를 저장하거나 꺼낼 때, 기본형 값을 래퍼 클래스의 객체로 변환하지 않아도 되므로 편리하다.

에제 9-25 / ch9 / WrapperEx3.java

``` java
public class WrapperEx3 {
	public static void main(String[] args) {
		int i = 10;
		
		// 기본형을 참조형으로 형변환(형변환 생략가능)
		Integer intg = (Integer)i;	// Integer intg = Integer.valueOf(i);
		Object obj = (Object)i;	// Object obj = (Object)Integer.valueOf(i);
		
		Long lng = 100L;	// Long lng = new Long(100L);
		
		int i2 = intg + 10;	// 참조형과 기본형간의 연산 가능
		long l = intg + lng;	// 참조형 간의 덧셈도 가능
		
		Integer intg2 = new Integer(20);
		int i3 = (int)intg2;	// 참조형을 기본형으로 형변환도 가능(형병환 생략가능)
		
		Integer intg3 = intg2 + i3;
		
		System.out.println("i = " + i);
		System.out.println("intg = " + intg);
		System.out.println("obj = " + obj);
		System.out.println("lng = " + lng);
		System.out.println("intg + 10 = " + i2);
		System.out.println("intg + lng = " + l);
		System.out.println("intg2 = " + intg2);
		System.out.println("i3 = " + i3);
		System.out.println("intg2 + i3 = " + intg3);
	}
}
```

```
i = 10
intg = 10
obj = 10
lng = 100
intg + 10 = 20
intg + lng = 110
intg2 = 20
i3 = 20
intg2 + i3 = 40
```

이 예제는 오토박싱(autoboxing)을 이용해서 기본형과 참조형 간의 형변환과 연산을 수행하는 예를 보여준다. 지금까지 배워온 것과는 달리 기본형과 참조형 간의 형변환도 가능할 뿐만 아니라, 심지어는 참조형 간의 연산도 가능하다.

![image](https://ifh.cc/g/RNt6tn.png)