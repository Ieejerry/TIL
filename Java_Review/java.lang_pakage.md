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