Chapter 7. 객체지향 프로그래밍2

# 8. 내부 클래스(inner class)

내부 클래스는 클래스 내에 선언된다는 점을 제외하고는 일반적인 클래스와 다르지 않다.

</br>

## 8.1 내부 클래스란?

내부 클래스는 클래스 내에 선언된 클래스이다. 클래스에 다른 클래스를 선언하는 이유는 두 클래스가 서로 긴밀한 관계에 있기 때문이다.

한 클래스를 다른 클래스의 내부 클래스로 선언하면 두 클래스의 멤버들 간에 서로 쉽게 접근할 수 있다는 장점과 외부에는 불필요한 클래스를 감춤으로써 코드의 복잡성을 줄일 수 있다는 장점을 얻을 수 있다.

> 내부 클래스의 장점
> - 내부 클래스에서 외부 클래스의 멤버들을 쉽게 접근할 수 있다.
> - 코드의 복잡성을 줄일 수 있다(캡슐화).

아래 왼쪽의 `A`와 `B` 두 개의 독립적인 클래스를 오른쪽과 같이 바꾸면 `B`는 `A`의 내부 클래스(inner class)가 되고 `A`는 `B`를 감싸고 있는 외부 클래스(outer class)가 된다.

![image](https://ifh.cc/g/9Ph4oS.png)

이 때 내부 클래스인 `B`는 외부 클래스인 `A`를 제외하고는 다른 클래스에서 잘 사용되지 않는 것이어야 한다.

</br>

## 8.2 내부 클래스의 종류와 특징

내부 클래스의 종류는 변수의 선언위치에 따른 종류와 같다. 내부 클래스는 마치 변수를 선언하는 것과 같은 위치에 선언할 수 있으며, 변수의 선언위치에 따라 인스턴스변수, 클래스변수(static변수), 지역변수로 구분되는 것과 같이 내부 클래스도 선언위치에 따라 다음과 같이 구분되어 진다. 내부 클래스의 유효범위와 성질이 변수와 유사하다.

![image](https://ifh.cc/g/aGsmKv.png)

</br>

## 8.3 내부 클래스의 선언

아래의 오른쪽 코드에는 외부 클래스(Outer)에 3개의 서로 다른 종류의 내부 클래스를 선언했다. 양쪽의 코드를 비교해 보면 내부 클래스의 선언위치가 변수의 선언위치와 동일하다.

변수가 선언된 위치에 따라 인스턴스변수, 클래스변수(static변수), 지역변수로 나뉘듯이 내부 클래스도 이와 마찬가지로 선언된 위치에 따라 나뉜다. 그리고, 각 내부 클래스의 선언위치에 따라 같은 선언위치의 변수와 동일한 유효범위(scope)와 접근성(accessibility)을 갖는다.

![image](https://ifh.cc/g/A4RRLA.png)

</br>

## 8.4 내부 클래스의 제어자와 접근성

아래 코드에서 인스턴스클래스(`InstanceInner`)와 스태틱 클래스(`StaticInner`)는 외부 클래스(`Outer`)의 멤버변수(인스턴스변수와 클래스변수)와 같은 위치에 선언되며, 또한 멤버변수와 같은 성질을 갖는다. 따라서 내부 클래스가 외부 클래스의 멤버와 같이 간주되고, 인스턴스멤버와 static멤버 간의 규칙이 내부 클래스에도 똑같이 적용된다.

![image](https://ifh.cc/g/TcqPQL.png)

그리고 내부 클래스도 클래스이기 때문에 `abstract`나 `final`과 같은 제어자를 사용할 수 있을 뿐만 아니라, 멤버변수들처럼 `private`, `protected`과 같은 접근제어자도 사용이 가능하다.

예제 7-31 / ch7 / InnerEx1.java

``` java
public class InnerEx1 {
	class InstanceInner {
		int iv = 100;
//		static int cv = 100;	// 에러. static변수를 선언할 수 없다.
		final static int CONST = 100;	// final static은 상수이므로 허용
	}
	
	static class StaticInner {
		int iv = 200;
		static int cv = 200;	// static클래스만 static멤버를 정의할 수 있다.
	}
	
	void method() {
		class LocalInner {
			int iv = 300;
//			static int cv = 300;	// 에러. static변수를 선언할 수 없다.
			final static int CONST = 300;	// final static은 상수이므로 허용
		}
	}
	
	public static void main(String[] args) {
		System.out.println(InstanceInner.CONST);
		System.out.println(StaticInner.cv);
	}
}
```

```
100
200
```

내부 클래스 중에서 스태틱 클래스(`StaticInner`)만 static멤버를 가질 수 있다. 드문 경우지만 내부 클래스에 static변수를 선언해야한다면 스태틱 클래스로 선언해야한다.

다만 `final`과 `static`이 동시에 붙은 변수는 상수(constant)이므로 모든 내부 클래스에서 정의가 가능하다.

예제 7-32 / ch7 / InnerEx2.java

``` java
public class InnerEx2 {
	class InstanceInner {}
	static class StaticInner {}
	
	// 인스턴스멤버 간에는 서로 직접 접근이 가능하다.
	InstanceInner iv = new InstanceInner();
	// static멤버 간에는 서로 직접 접근이 가능하다.
	static StaticInner cv = new StaticInner();
	
	static void staticMethod() {
		// static멤버는 인스턴스멤버에 직접 접근할 수 없다.
//		InstanceInner obj1 = new InstanceInner();
		StaticInner obj2 = new StaticInner();
		
		// 굳이 접근하려면 아래와 같이 객체를 생성해야 한다.
		// 인스턴스클래스는 외부 클래스를 먼저 생성해야만 생성할 수 있다.
		InnerEx2 outer = new InnerEx2();
		InstanceInner obj1 = outer.new InstanceInner();
	}
	
	void instanceMethod() {
		// 인스턴스메소드에서는 인스턴스멤버와 static멤버 모두 접근 가능하다.
		InstanceInner obj1 = new InstanceInner();
		StaticInner obj2 = new StaticInner();
		// 메소드 내에 지역적으로 선언된 내부 클래스는 외부에서 접근할 수 없다.
//		LocalInner lv = new LocalInner();
	}
	
	void myMethod() {
		class LocalInner {}
		LocalInner lv = new LocalInner();
	}
}
```

인스턴스멤버는 같은 클래스에 있는 인스턴스멤버와 static멤버 모두 직접 호출이 가능하지만, static멤버는 인스턴스멤버를 직접 호출할 수 없는 것처럼, 인스턴스클래스는 외부 클래스의 인스턴스멤버를 객체생성 없이 바로 사용할 수 있지만, 스태틱 클래스는 외부 클래스의 인스턴스멤버를 객체생성 없이 사용할 수 없다.

마찬가지로 인스턴스클래스는 스태틱 클래스의 멤버들을 객체생성 없이 사용할 수 있지만, 스태틱 클래스에서는 인스턴스클래스의 멤버들을 객체생성 없이 사용할 수 없다.

예제 7-33 / ch7 / InnerEx3.java

``` java
public class InnerEx3 {
	private int outerIv = 0;
	static int outerCv = 0;
	
	class InstanceInner {
		int iiv = outerIv;	// 외부클래스의 private멤버도 접근이 가능하다.
		int iiv2 = outerCv;
	}
	
	static class StaticInner {
		// 스태틱 클래스는 외부 클래스의 인스턴스멤버에 접근할 수 없다.
//		int siv = outerIv;
		static int scv = outerCv;
	}
	
	void myMethod() {
		int lv = 0;
		final int LV = 0;	// JDK1.8부터 final 생략 가능
		
		class LocalInner {
			int liv = outerIv;
			int liv2 = outerCv;
			// 외부 클래스의 지역변수는 final이 붙은 변수(상수)만 접근가능하다.
			int liv3 = lv;	// 에러.(JDK1.8부터 에러 아님)
			int liv4 = LV;	// OK.
		}
	}
}
```

내부 클래스에서 외부 클래스의 변수들에 대한 접근성을 보여주는 예제이다. 인스턴스클래스(`InstanceInner`)는 외부 클래스(`InnerEx3`)의 인스턴스멤버이기 때문에 인스턴스변수 `outerIv`와 statc변수 `outerCv`를 모두 사용할 수 있다. 심지어는 `outerIv`의 접근 제어자가 `private`일지라도 사용가능하다.

스태틱 클래스(`StaticInner`)는 외부 클래스(`InnerEx3`)의 static멤버이기 때문에 외부 클래스의 인스턴스멤버인 `outerIv`와 `InstanceInner`를 사용할 수 없다. 단지 static멤버인 `outerCv`만을 사용할 수 있다.

지역 클래스(`LocalInner`)는 외부 클래스의 인스턴스멤버와 static멤버를 모두 사용할 수 있으며, 지역 클래스가 포함된 메소드에 정의된 지역변수도 사용할 수 있다. 단, `final`이 붙은 지역변수만 접근가능한데 그 이유는 메소드가 수행을 마쳐서 지역변수가 소멸된 시점에도, 지역 클래스의 인스턴스가 소멸된 지역변수를 참조하려는 경우가 발생할 수 있기 때문이다.

JDK1.8부터 지역 클래스에서 접근하는 지역 변수 앞에 `final`을 생략할 수 있게 바뀌었다. 대신 컴파일러가 자동으로 붙여준다. 즉, 편의상 `final`을 생략할 수 있게 한 것일 뿐 해당 변수의 값이 바뀌는 문장이 있으면 컴파일 에러가 발생한다.

예제 7-34 / ch7 / InnerEx4.java

``` java
class Outer {
	class InstanceInner {
		int iv = 100;
	}
	
	static class StaticInner {
		int iv = 200;
		static int cv = 300;
	}
	
	void myMethod() {
		class LocalInner {
			int iv = 400;
		}
	}
}

public class InnerEx4 {
	public static void main(String[] args) {
		// 인스턴스클래스의 인스턴스를 생성하려면
		// 외부 클래스의 인스턴스를 먼저 생성해야 한다.
		Outer oc = new Outer();
		Outer.InstanceInner ii = oc.new InstanceInner();
		
		System.out.println("ii.iv : " + ii.iv);
		System.out.println("Outer.StaticInner.cv : " + Outer.StaticInner.cv);
		
		// 스태틱 내부 클래스의 인스턴스는 외부 클래스를 먼저 생성하지 않아도 된다.
		Outer.StaticInner si = new Outer.StaticInner();
		System.out.println("si.iv : " + si.iv);
	}
}
```

```
ii.iv : 100
Outer.StaticInner.cv : 300
si.iv : 200
```

외부 클래스가 아닌 다른 클래스에서 내부 클래스를 생성하고 내부 클래스의 멤버에 접근하는 예제이다. 실제로 이런 경우가 발생했다는 것은 내부 클래스로 선언해서는 안 되는 클래스를 내부 클래스로 선언했다는 의미이다.

참고로 컴파일 시 생성되는 클래스 파일은 다음과 같다.

InnerEx4.class   
Outer.class   
Outer$InstanceInner.class   
Outer$StaticInner.class   
Outer$LocalInner.class

컴파일 했을 때 생성되는 파일명은 **'외부 클래스명$내부 클래스명.class'**형식으로 되어 있다. 다만 서로 다른 메소드 내에서는 같은 이름의 지역변수를 사용하는 것이 가능한 것처럼, 지역내부 클래스는 다른 메소드에 같은 이름의 내부 클래스가 존재할 수 있기 때문에 내부 클래스명 앞에 숫자가 붙는다.

![image](https://ifh.cc/g/Rxf85R.png)

만일 오른쪽의 코드를 컴파일 하면 다음과 같은 클래스파일이 생성된다.

Outer.class   
Outer$1LocalInner.class   
Outer$2LocalInner.class

예제 7-35 / ch7 / InnerEx5.java

``` java
class Outer2 {
	int value = 10;	// Outer.this.value
	
	class Inner {
		int value = 20;	// this.value
		
		void method1() {
			int value = 30;
			System.out.println("value : " + value);
			System.out.println("this.value : " + this.value);
			System.out.println("Outer2.this.value : " + Outer2.this.value);
		}
	}	// Inner클래스의 끝
}	// Outer클래스의 끝

public class InnerEx5 {
	public static void main(String[] args) {
		Outer2 outer = new Outer2();
		Outer2.Inner inner = outer.new Inner();
		inner.method1();
	}
}	// InnerEx5 끝
```

```
value : 30
this.value : 20
Outer2.this.value : 10
```

위의 예제는 내부 클래스와 외부 클래스에 선언된 변수의 이름이 같을 때 변수 앞에 `this` 또는 `외부 클래스명.this`를 붙여서 서로 구별할 수 있다는 것을 보여준다.

</br>

## 8.5 익명 클래스(anonymous class)

익명 클래스는 특이하게도 다른 내부 클래스드과는 달리 이름이 없다. 클래스의 선언과 객체의 생성을 동시에 하기 때문에 단 한번만 사용될 수 있고 오직 하나의 객체만을 생성할 수 있는 일회용 클래스이다.

``` java
new 조상클래스이름() {
    // 멤버 선언
}

    또는

new 구현인터페이스이름() {
    // 멤버 선언
}
```

이름이 없기 때문에 생성자도 가질 수 없으며, 조상클래스의 이름이나 구현하고자 하는 인터페이스의 이름을 사용했기 때문에 하나의 클래스로 상속받는 동시에 인터페이스를 구현하거나 둘 이상의 인터페이스를 구현할 수 없다. 오로지 단 하나의 클래스를 상속받거나 단 하나의 인터페이스만을 구현할 수 있다.

예제 7-36 / ch7 / InnerEx6.java

``` java
public class InnerEx6 {
	Object iv = new Object() { void method() {} };	// 익명클래스
	static Object cv = new Object() { void method() {} };	// 익명 클래스
	
	void myMethod() {
		Object lv = new Object() { void method() {} };	// 익명 클래스
	}
}
```

위의 예제는 단순히 익명 클래스의 사용 예를 보여 준 것이다. 이 예제를 컴파일 하면 다음과 같이 4개의 클래스파일이 생성된다.

InnerEx6.class   
InnerEx6$1.class ← 익명 클래스   
InnerEx6$2.class ← 익명 클래스   
InnerEx6$3.class ← 익명 클래스

익명 클래스는 이름이 없기 때문에 **'외부 클래스명$숫자.class'**의 형식으로 클래스파일명이 결정된다.

예제 7-37 / ch7 / InnerEx7.java

``` java
import java.awt.*;
import java.awt.event.*;

class EventHandler implements ActionListener {
	public void actionPerformed(ActionEvent e) {
		System.out.println("ActionEvent occurred.");
	}
}

public class InnerEx7 {
	public static void main(String[] args) {
		Button b = new Button("Start");
		b.addActionListener(new EventHandler());
	}
}
```

이 예제를 실행하면 아무것도 화면에 나타나지 않는 채 종료된다. 단지 익명클래스로 변환하는 예를 보여주기 위한 것이다.

예제 7-38 / ch7 / InnerEx8.java

``` java
import java.awt.*;
import java.awt.event.*;

public class InnerEx8 {
	public static void main(String[] args) {
		Button b = new Button("Start");
		b.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				System.out.println("ActionEvent occured.");
			} // 익명 클래스의 끝
		});
	}	// main의 끝
}	// InnerEx8의 끝
```

예제 7-37을 익명클래스를 이용해서 변경한 것이 예제 7-38이다. 먼저 두 개의 독립된 클래스를 작성한 다음에, 다시 익명클래스를 이용하여 변경하면 보다 쉽게 코드를 작성할 수 있다.