Chapter 7. 객체지향 프로그래밍2

# 2. 오버라이딩(overriding)

</br>

## 2.1 오버라이딩이란?

조상 클래스로부터 상속받은 메소드의 내용을 변경하는 것을 오버라이딩이라고 한다. 상속받은 메소드를 그대로 사용하기도 하지만, 자손 클래스의 자신에 맞게 변경해야하는 경우가 많다. 이럴 때 조상의 메소드를 오버라이딩한다.

> override의 사전적 의미는 '~위에 덮어쓰다(overwrite)'이다.

2차원 좌표계의 한 점을 표현하기 위한 `Point`클래스가 있을 때, 이를 조상으로 하는 `Point3D`클래스, 3차원 좌표계의 한 점을 표현하기 위한 클래스를 다음과 같이 새로 작성하였다.

``` java
class Point {
    int x;
    int y;

    String getLocation() {
        return "x : " + x + ", y : " + y;
    }
}

class Point3D extends Point {
    int z;

    String getLocation() {
        return "x : " + x + ", y : " + y + ", z : " + z;
    }
}
```

`Point`클래스의 `getLocation()`은 한 점의 x, y좌표를 문자열로 반환하도록 작성되었다. 이 두 클래스는 서로 상속관계에 있으므로 `Point3D`클래스는 `Point`클래스로부터 `getLocation()`을 상속받지만, `Point3D`클래스는 3차원 좌표계의 한 점을 표현하기 위한 것이므로 조상인 `Point`클래스로부터 상속받은 `getLocation()`은 `Point3D`클래스에 맞지 않는다. 그래서 이 메소드를 `Point3D`클래스 자신에 맞게 z축의 좌표값도 포함하여 반환하도록 오버라이딩하였다.

`Point`클래스를 사용하던 사람들은 새로 작성된 `Point3D`클래스가 `Point`클래스의 자손이므로 `Point3D`클래스의 인스턴스에 대해서 `getLocation()`을 호출하면 `Point`클래스의 `getLocation()`이 그랬듯이 점의 좌표를 문자열로 얻을 수 있을 것이라고 기대할 것이다.

그렇기 때문에 새로운 메소드를 제공하는 것보다 오버라이딩을 하는 것이 바른 선택이다.

</br>

## 2.2 오버라이딩의 조건

오버라이딩은 메솓의 내용만을 새로 작성하는 것이므로 메소드의 선언부는 조상의 것과 완전히 일치해야 한다. 그래서 오버라이딩이 성립하기 위해서는 다음과 같은 조건을 만족해야 한다.

> 자손 클래스에서 오버라이딩하는 메소드는 조상 클래스의 메소드와
> - 이름이 같아야 한다.
> - 매개변수가 같아야 한다.
> - 반환타입이 같아야 한다.

> JDK1.5부터 '공변 반환타입(covariant retrun type)'이 추가되어, 반환타입을 자손 클래스의 타입으로 변경하는 것은 가능하도록 조건이 완화되었다.

한마디로 요약하면 선언부가 서로 일치해야 한다는 것이다. 다만 접근 제어자(access modifier)와 예외(exception)는 제한된 조건 하에서만 다르게 변경할 수 있다.

1. 접근 제어자는 조상 클래스의 메소드보다 좁은 범위로 변경할 수 없다.

만일 조상클래스에 정의된 메소드의 접근 제어자가 protected라면, 이를 오버라이딩하는 자손 클래스의 메소드는 접근 제어자가 protected나 public이어야 한다. 대부분의 경우 같은 범위의 접근 제어자를 사용한다. 접근 제어자의 접근범위를 넓은 것에서 좁은 것 순으로 나열하면 public, protected, (default), private이다.

2. 조상 클래스의 메소드보다 많은 수의 예외를 선언할 수 없다.

아래의 코드를 보면 `Child`클래스의 `parentMethod()`에 선언된 예외의 개수가 조상인 `Parent`클래스이 `parentMethod()`에 선언된 예외의 개수보다 적으므로 바르게 오버라이딩 되었다.

``` java
class Parent {
    void parentMethod() throws IOException, SQLException {
        ...
    }
}

class Child extends Parent {
    void parentMethod() throws IOException {
        ...
    }
    ...
}
```

여기서 주의해야할 점은 단순히 선언된 예외의 개수의 문제가 아니다.

``` java
class Child extends Parent {
    void parentMethod() throws Exception {
        ...
    }
    ...
}
```

만일 위와 같이 오버라이딩을 하였다면, 분명히 조상 클래스에 정의된 메소드보다 적은 개수의 예외를 선언한 것처럼 보이지만 `Exception`은 모든 예외의 최고 조상이므로 가장 만흔 개수의 예외를 던질 수 있도록 선언한 것이다.

그래서 예외의 개수는 적가나 같아야 한다는 조건을 만족시키지 못하는 잘못된 오버라이딩이다.

> 조상 클래스의 메소드를 자손 클래스에서 오버라이딩할 때
> 1. 접근 제어자를 조상 클래스의 메소드보다 좁은 범위로 변경할 수 없다.
> 2. 예외는 조상 클래스의 메소드보다 많이 선언할 수 없다.
> 3. 인스턴스메소드를 static메소드로 또는 그 반대로 변경할 수 없다.

</br>

오버로딩과 오버라이딩은 서로 혼동하기 쉽지만 사실 그 차이는 명백하다. 오버로딩은 기존에 없는 새로운 메소드를 추가하는 것이고, 오버라이딩은 조상으로부터 상속받은 메소드의 내용을 변경하는 것이다.

> **오버로딩(overloading)** 기존에 없는 새로운 메소드를 정의하는 것(new)   
**오버라이딩(overriding)** 상속받은 메소드와 내용을 변경하는 것(change, modify)

아래의 코드를 보고 오버로딩과 오버라이딩을 구별할 수 있어야 한다.

``` java
class Parent {
    void parentMethod() {}
}

class Child extends Parent {
    void parentMethod() {}  // 오버라이딩
    void parentMethod(int i) {} // 오버로딩

    void childMethod() {}
    void childMethod(int i) {}  // 오버로딩
    void childMethod() {}   // 에러. 중복정의 되었음 already defined in Child
}
```

</br>

## 2.4 super

`super`는 자손 클래스에서 조상 클래스로부터 상속받은 멤버를 참조하는데 사용되는 참조변수이다. 멤버변수와 지역변수의 이름이 같을 때 `this`를 붙여서 구별했듯이 상속받은 멤버와 자신의 멤버와 이름이 같을 때는 `super`를 붙여서 구별할 수 있다.

조상 클래스로부터 상속받은 멤버도 자손 클래스 자신의 멤버이므로 `super`대신 `this`를 사용할 수 있다. 그래도 조상 클래스의 멤버와 자손 클래스의 멤버가 중복 정의되어 서로 구별해야하는 경우에만 `super`를 사용하는 것이 좋다.

조상의 멤버와 자신의 멤버를 구별하는데 사용된다는 점을 제외하고는 `super`와 `this`는 근본적으로 같다. 모든 인스턴스메소드에는 자신이 속한 인스턴스의 주소가 지역변수로 저장되는데, 이것이 참조변수인 `this`와 `super`의 값이 된다.

static메소드(클래스메소드)는 인스턴스와 관련이 없다. 그래서 `this`와 마찬가지로 `super` 역시 static메소드에서는 사용할 수 없고 인스턴스 메소드에서만 사용할 수 있다.

예제 7-5 / ch7 / SuperTest.java

``` java
class Parent {
	int x = 10;
}

class Child extends Parent {
	void method() {
		System.out.println("x = " + x);
		System.out.println("this.x = " + this.x);
		System.out.println("super.x = " + super.x);
	}
}

public class SuperTest {
	public static void main(String[] args) {
		Child c = new Child();
		c.method();
	}
}
```

```
x = 10
this.x = 10
super.x = 10
```

이 경우 `x`, `this.x`, `super.x` 모두 같은 변수를 의미하므로 모두 같은 값이 출력되었다.

예제 7-6 / ch7 / SuperTest2.java

``` java
class Parent2 {
	int x = 10;
}

class Child2 extends Parent2 {
	int x = 20;
	
	void method() {
		System.out.println("x = " + x);
		System.out.println("this.x = " + this.x);
		System.out.println("super.x = " + super.x);
	}
}

public class SuperTest2 {
	public static void main(String[] args) {
		Child2 c = new Child2();
		c.method();
	}
}
```

```
x = 20
this.x = 20
super.x = 10
```

이전 예제와 달리 같은 이름의 멤버변수가 조상 클래스인 `Parent`에도 있고 자손 클래스인 `Child`클래스에도 있을 때는 `super.x`와 `this.x`는 서로 다른 값을 참조하게 된다. `super.x`는 조상 클래스로부터 상속받은 멤버변수 `x`를 뜻하며, `this.x`는 자손 클래스에 선언된 멤버변수를 뜻한다.

이처럼 조상 클래스에 선언된 멤버변수와 같은 이름의 멤버변수를 자손 클래스에서 중복해서 정의하는 것이 가능하며 참조변수 `super`를 이용해서 서로 구별할 수 있다.

변수만이 아니라 메소드 역시 `super`를 써서 호출할 수 있다. 특히 조상 클래스의 메소드를 자손 클래스에서 오버라이딩한 경우에 `super`를 사용한다.

``` java
class Point {
    int x;
    int y;

    String getLocation() {
        return "x = " + x + ", y = " + y;
    }
}

class Point3D extends Point {
    int z;
    String getLocation() {  // 오버라이딩
//      return "x = " + x + ", y = " + y + ", z = " + z;
        return super.getLocation() + ", z = " + z;  // 조상의 메소드 호출
    }
}
```

`getLocation()`을 오버라이딩할 때 조상 클래스의 `getLocation()`을 호출하는 코드를 포함시켰다. 조상클래스의 메소드의 내용에 추가적으로 작업을 덧붙이는 경우라면 이처럼 `super`를 사용해서 조상 클래스의 메소드를 포함시키는 것이 좋다. 후에 조상 클래스의 메소드가 변경되더라도 변경된 내용이 자손 클래스의 메소드에 자동적으로 반영되기 때문이다.

</br>

## 2.5 super() - 조상 클래스의 생성자

`this()`와 마찬가지로 `super()` 역시 생성자이다. `this()`는 같은 클래스의 다른 생성자를 호출하는 데 사용되지만, `super()`는 조상 클래스이 생성자를 호출하는데 사용된다.

자손 클래스의 인스턴스를 생성하면, 자손의 멤버와 조상의 멤버가 모두 합쳐진 하나의 인스턴스가 생성된다. 그래서 자손 클래스의 인스턴스가 조상 클래스이 멤버들을 사용할 수 있는 것이다. 이 때 조상 클래스 멤버의 초기화 작업이 수행되어야 하기 때문에 자손 클래스의 생성자에서 조상 클래스의 생성자가 호출되어야 한다.

생성자의 첫 줄에서 조상클래스의 생성자를 호출해야하는 이유는 자손 클래스의 멤버가 조상 클래스의 멤버를 사용할 수도 있으므로 조상의 멤버들이 먼저 초기화되어 있어야 하기 때문이다.

이와 같은 조상 클래스 생성자의 호출은 클래스의 상속관계를 거슬러 올라가면서 계속 반복된다. 마지막으로 모든 클래스의 최고 조상인 `Object`클래스의 생성자인 `Obeject()`까지 가서야 끝이 난다.

그래서 `Object`클래스를 제외한 모든 클래스의 생성자는 첫 줄에 반드시 자신의 다른 생성자 또는 조상의 생성자를 호출해야 한다. 그렇지 않으면 컴파일러는 생성자의 첫 줄에 `super();`를 자동적으로 추가한다.

> Object클래스를 제외한 모든 클래스의 생성자 첫 줄에 생성자, this(), super()를 호출해야 한다. 그렇지 않으면 컴파일러가 자동적으로 'super();'를 생성자의 첫 줄에 삽입한다.

인스턴스를 생성할 때는 클래스를 선택하는 것만큼 생성자를 선택하는 것도 중요하다.

> 1. **클래스** - 어떤 클래스의 인스턴스를 생성할 것인가?
> 2. **생성자** - 선택한 클래스의 어떤 생성자를 이용해서 인스턴스를 생성할 것인가?

예제 7-7 / ch7 / PointTest.java

``` java
class Point2 {
	int x, y;
	
	Point2(int x, int y) {
		this.x = x;
		this.y = y;
	}
	
	String getLocation() {
		return "x = " + x + ", y = " + y;
	}
}

class Point3D extends Point2 {
	int z;
	
	Point3D(int x, int y, int z) {
		// 생성자 첫 줄에 다른 생성자를 호출하지 않기 때문에 컴퍼일러가 'super();'를 여기에 삽입한다. super()는 Point3D의 조상인 Point2클래스의 기본 생성자인 Point2()를 의미한다.
		this.x = x;
		this.y = y;
		this.z = z;
	}
	
	String getLocation() {
		return "x = " + x + ", y = " + y + ", z = "+ z;
	}
}

public class PointTest {
	public static void main(String[] args) {
		Point3D p3 = new Point3D(1, 2, 3);
	}
}
```

```
Exception in thread "main" java.lang.Error: Unresolved compilation problem: 
	Implicit super constructor Point2() is undefined. Must explicitly invoke another constructor

	at Point3D.<init>(PointTest.java:17)
	at PointTest.main(PointTest.java:31)
```

이 예제를 컴파일하면 위와 같은 컴파일에러가 발생한다. `Point3D`클래스의 생성자에서 조상 클래스의 생성자인 `Point2()`를 찾을 수 없다는 내용이다.

`Point3D`클래스의 생성자의 첫 줄이 생성자(조상의 것이든 자신의 것이든)를 호출하는 문장이 아니기 때문에 컴파일러는 다음과 같이 자동적으로 `super();`를 `Point3D`클래스의 생성자의 첫 줄에 넣어준다.

``` java
Point3D(int x, int y, int z) {
    super();
    this.x = x;
    this.y = y;
    this.z = z;
}
```

그래서 `Point3D`클래스의 인스턴스를 생성하면, 생성자 `Point3D(int x, int y, int z)`가 호출되면서 첫 문장인 `super();`를 수행하게 된다. `super()`는 `Point3D`클래스의 조상인 `Point2`클래스의 기본 생성자인 `Point2()`를 뜻하므로 `Point2()`가 호출된다.

그러나 `Point2`클래스에 생성자 `Point2()`가 정의되어 있지 않기 때문에 위와 같은 컴파일에러가 발생한 것이다. 이 에러를 수정하려면, `Point2`클래스에 생성자 `Point2()`를 추가해주던가, 생성자 `Point3D(int x, int y, int z)`의 첫 줄에서 `Point2(int x, int y)`를 호출하도록 변경하면 된다.

> 생성자가 정의되어 있는 클래스에는 컴파일러가 기본 생성자를 자동적으로 추가하지 않는다.

``` java
Point3D(int x, int y, int z) {
    super(int x, int y);    // 조상 클래스의 생성자 Point2(int x, int y)를 호출한다.
    this.z = z;
}
```

위와 같이 변경하면 문제없이 컴파일이 된다. **조상 클래스의 멤버변수는 이처럼 조상의 생성자에 의해 초기화되도록 해야 한다.**

예제 7-8 / ch 7 / PointTest2.java

``` java
class Point3 {
	int x = 10;
	int y = 20;
	
	Point3(int x, int y) {
//		생성자 첫 줄에서 다른 생성자를 호출하지 않기 때문에 컴파일러가 'super();'를 여기에 삽입한다. super()는 Point3의 조상인 Object클래스의 기본 생성자인 Object()를 의미한다.
		this.x = x;
		this.y = y;
	}
}

class Point3D2 extends Point3 {
	int z = 30;
	
	Point3D2() {
		this(100, 200, 300);	// Point3D2(int x, int y, int z)를 호출한다.
	}
	
	Point3D2(int x, int y, int z) {
		super(x, y);	// Point3(int x, int y)를 호출한다.
		this.z = z;
	}
}

public class PointTest2 {
	public static void main(String[] args) {
		Point3D2 p3 = new Point3D2();
		System.out.println("p3.x = " + p3.x);
		System.out.println("p3.y = " + p3.y);
		System.out.println("p3.z = " + p3.z);
	}
}
```

```
p3.x = 100
p3.y = 200
p3.z = 300
```

`Point3D2`클래스의 인스턴스를 생성할 때 이떤 순서로 인스턴스의 초기화가 진행되는지 보여주기 위한 예제이다. `Point3`클래스의 생성자 `Point3(in x, int y)`는 어떠한 생성자도 호출하지 않기 때문에 컴파일 후에 다음과 같은 코드로 변경된다.

``` java	
Point3(int x, int y) {
    super();    // 조상인 Object클래스의 생성자 Object()를 호출한다.
    this.x = x;
    this.y = y;
}
```

그래서 `Point3D2 p3 = new Point3D2();`와 같이 인스턴스를 생성하면, 아래와 같은 순서로 생성자가 호출된다.

```
Point3D2() → Point3D2(int x, int y, int z) → Point3(int x, int y) → Object()
```

어떤 클래스의 인스턴스를 생성하면, 클래스 상속관계의 최고 조상인 `Object`클래스까지 거슬러 올라가면서 모든 조상 클래스의 생성자가 순서대로 호출된다는 것을 알 수 있다.