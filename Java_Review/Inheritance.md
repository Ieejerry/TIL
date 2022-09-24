Chapter 7. 객체지향 프로그래밍2

# 1. 상속(inheritance)

</br>

## 1.1 상속의 정의와 장점

상속이란, 기존의 클래스를 재사용하여 새로운 클래스를 작성하는 것이다. 상속을 통해서 클래스를 작성하면 보다 적은 양의 코드로 새로운 클래스를 작성할 수 있고 코드를 공통적으로 관리할 수 있기 때문에 코드의 추가 및 변경이 매우 용이하다.

이러한 특징은 코드의 재사용성을 높이고 코드의 중복을 제거하여 프로그램의 생산성과 유지보수에 크게 기여한다.

자바에서 상속을 구현하는 방법은 아주 간단하다. 새로 작성하고자 하는 클래스의 이름 뒤에 상속받고자 하는 클래스의 이름을 키워드 `extends`와 함께 써주기만 하면 된다.

예를 들어 새로 작성하려는 클래스의 이름이 `Child`이고 상속받고자 하는 기존 클래스의 이름이 `Parent`라면 다음과 같이 하면 된다.

``` java
class Child extends Parent {
    // ...
}
```

이 두 클래스는 서로 상속 관계에 있다고 하며, 상속해주는 클래스를 '조상 클래스'라 하고 상속 받는 클래스를 '자손 클래스'라 한다.

> 서로 상속관계에 있는 두 클래스를 아래와 같은 용어를 사용해서 표현하기도 한다.

> **조상 클래스** 부모(parent)클래스, 상위(super)클래스, 기반(base)클래스   
> **자손 클래스** 자식(child)클래스, 하위(sub)클래스, 파생된(derived)클래스

아래와 같이 서로 상속관계에 있는 두 클래스를 그림으로 표현하면 다음과 같다.

``` java
class Parent { }
class Child extends Parent { }
```

![image](https://ifh.cc/g/Vw5coP.png)

클래스는 타원으로 표현했고 클래스간의 상속 관계는 화살표로 표시했다. 이와 같이 클래스 간의 상속관계를 그림으로 표현한 것을 상속계층도(class hierarchy)라고 한다.

자손 클래스는 조상 클래스의 모든 멤버를 상속받기 때문에, `Child`클래스는 `Parent`클래스의 멤버들을 포함한다고 할 수 있다. 클래스는 멤버들의 집합이므로 클래스 `Parent`와 `Child`의 관계를 다으모가 같이 표현할 수도 있다.

![image](https://ifh.cc/g/8dz2qc.png)

만일 `Parent`클래스에 `age`라는 정수형 변수를 멤버변수로 추가하면, 자손 클래스는 조상의 멤버를 모두 상속받기 때문에, `Child`클래스는 자동적으로 `age`라는 멤버변수가 추가된 것과 같은 효과를 얻는다.

``` java
class Parent {
    int age;
}

class Child extends Parent { }
```

![image](https://ifh.cc/g/K4lodn.png)

이번엔 반대로 자손인 `Child`클래스에 새로운 멤버로 `play()`메소드를 추가해보겠다.

``` java
class Parent {
    int age;
}

class Child extends Parent {
    void play() {
        System.out.println("놀자");
    }
}
```

![image](https://ifh.cc/g/NTQ8y5.png)

`Child`클래스에 새로운 코드가 추가되어도 조상인 `Parent`클래스는 아무런 영향을 받지 않는다. 여기서 알 수 있는 것처럼, 조상 클래스가 변경되면 자손 클래스는 자동적으로 영향을 받게 되지만, 자손 클래스가 변경되는 것은 조상 클래스에 아무런 영향을 주지 못한다.

자손 클래스는 조상 클래스의 모든 멤버를 상속 받으므로 항상 조상 클래스보다 같거나 많은 멤버를 갖는다.

그래서 상속을 받는다는 것은 조상 클래스를 확장(extend)한다는 의미로 해석할 수도 있으며 이것이 상속에 사용되는 키워드가 `extends`인 이유이기도 하다.

> - 생성자와 초기화 블럭은 상속되지 않는다. 멤버만 상속된다.
> - 자손 클래스의 멤버 개수는 조상 클래스보다 항상 같거나 많다.

> 접근 제어자(access modifier)가 private 또는 default인 멤버들은 상속되지 않는다기보다 상속은 받지만 자손 클래스로부터의 접근이 제한되는 것이다.

이번엔 `Parent`클래스로부터 상속받은 `Child2`클래스를 새로 작성해보겠다. `Child2`클래스를 포함한 세 클래스간의 상속계층도는 다음과 같다.

``` java
class Parent { }
class Child extends Parent { }
class Child2 extends Parent { }
```

![image](https://ifh.cc/g/3PZFMN.png)

클래스 `Child`와 `Child2`가 모두 `Parent`클래스를 상속받고 있으므로 `Parent`클래스와 `Child`클래스, 그리고 `Parent`클래스와 `Child2`클래스는 서로 상속관계에 있지만 클래스 `Child`와 `Child2`간에는 서로 아무런 관계도 성립되지 않는다. 클래스 간의 관계에서 형제 관계와 같은 것은 없다. 부모와 자식의 관계(상속관계)만이 존재한다.

만일 `Child`와 `Child2`클래스에 공통적으로 추가되어야 하는 멤버(멤버변수나 메소드)가 있다면, 이 두 클래스에 각각 따로 추가해주는 것보다는 이들의 공통조상인 `Parent`클래스에 추가하는 것이 좋다.

`Parent`클래스의 자손인 `Child`클래스와 `Child2`클래스는 조사으이 멤버를 상속받기 때문에, `Parent`클래스에 새로운 멤버를 추가해주는 것은 `Child`클래스와 `Child2`클래스에 새로운 멤버를 추가해주는 것과 같은 효과를 얻는다.

`Parent`클래스 하나만 변경하면 되므로 작업이 간단해진다. 이보다 더 중요한 사실은 같은 내용의 코드를 한 곳에서 관리함으로써 코드의 중복이 줄어든다는 것이다. 코드의 중복이 많아지면 유지보수가 어려워지고 일관성을 유지하기 어렵다.

이처럼 같은 내용의 코드를 하나 이상이 클래스에 중복적으로 추가해야하는 경우에는 상속관계를 이용해서 코드의 중복을 최소화해야 한다. 프로그램이 어떤 때는 잘 동작하지만 어떤 때는 오동작을 하는 이유는 중복된 코드 중에서 바르게 변경되지 않은 곳이 있기 때문이다.

여기에 또다시 `Child`클래스로부터 상속받는 `GrandChild`라는 새로운 클래스를 추가한다면 상속계층도는 다음과 같다.

``` java
class Parent { }
class Child extends Parent { }
class Child2 extends Parent { }
class GrandChild extends Child { }
```

![image](https://ifh.cc/g/XW7Zg5.png)

자손 클래스는 조상 클래스의 모든 멤버를 물려받으므로 `GrandChild`클래스는 `Child`클래스의 모든 멤버, `Child`클래스의 조상인 `Parent`클래스로부터 상속받은 멤버까지 상속받게 된다. 그래서 `GrandChild`클래스는 `Child`클래스의 자손이면서 `Parent`클래스의 자손이기도 하다. 좀 더 정확히 말하자면, `Child`클래스는 `GrandChild`클래스의 직접 조상이고, `Parent`클래스는 `GrandChild`클래스의 간접 조상이 된다. 그래서 `GrandChild`클래스는 `Parent`클래스와 간접적인 상속관계에 있다고 할 수 있다.

이제 `Parent`클래스에 전과 같이 정수형 변수인 `age`를 멤버변수로 추가해보겠다.

``` java
class Parent {
    int age;
}
class Child extends Parent { }
class Child2 extends Parent { }
class GrandChild extends Child { }
```

![image](https://ifh.cc/g/gOWwfh.png)

`Parent`클래스는 클래스 `Child`, `Child2`, `GrandChild`의 조상이므로 `Parent`클래스에 추가된 멤버변수 `age`는 `Parent`클래스의 모든 자손에 추가된다. 반대로 `Parent`클래스에서 멤버변수 `age`를 제거 한다면, `Parent`의 자손클래스인 `Child`, `Child2`, `GrandChild`에서도 제거된다.

이철머 조상 클래스만 변경해도 모든 자손 클래스에, 자손의 자손 클래스에까지 영향을 미치기 때문에, 클래스간의 상속관계를 맺어 주면 자손 클래스들의 공통적인 부분은 조상클래스에서 관리하고 자손 클래스는 자신에 정의된 멤버들만 관리하면 되므로 각 클래스의 코드가 적어져서 관리가 쉬워진다.

전체 프로그램을 구성하는 클래스들을 면멸히 설계 분석하여, 클래스간의 상속관계를 적절히 맺어 주는 것이 객체지향 프로그래밍에서 가장 중요한 부분이다.

예제 7-1 / ch7 / CaptionTvTest.java

``` java
class Tv{
	boolean power;	// 전원상태(on/off)
	int channel;	// 채널
	
	void power() { power = !power; }
	void channelUp() { ++channel; }
	void channelDown() { --channel; }
}

class SmartTv extends Tv {	// SmartTv는 Tv에 캡션(자막)을 보여주는 기능을 한다.
	boolean caption;	// 캡션상태(on/off)
	void displayCaption(String text) {
		if(caption) {	// 캡션 상태가 on(ture)일 때만 text를 보여준다.
			System.out.println(text);
		}
	}
}

public class CaptionTvTest {
	public static void main(String[] args) {
		SmartTv stv = new SmartTv();
		stv.channel = 10;	// 조상 클래스로부터 상속 받은 멤버
		stv.channelUp();	// 조상 클래스로부터 상속 받은 멤버
		System.out.println(stv.channel);
		stv.displayCaption("Hello, World");
		stv.caption = true;	// 캡션(자막) 기능을 켠다.
		stv.displayCaption("Hello, World");
	}
}
```

```
11
Hello, World
```

`Tv`클래스로부터 상속받고 기능을 추가하여 `CaptionTv`클래스를 작성하였다. 멤버변수 `caption`은 캡션기능의 상태를 저장하기 위한 boolean형 변수이고, `displayCaption(String text)`은 매개변수로 넘겨받은 문자열(`text`)을 캡션이 켜져 있는 경우(caption의 값이 true인 경우)에만 화면에 출력한다.

자손 클래스의 인스턴스를 생성하면 조상 클래스의 멤버도 함께 생성되기 때문에 따로 조상 클래스의 인스턴스를 생성하지 않고도 조상 클래스의 멤버들을 사용할 수 있다.

![image](https://ifh.cc/g/0wKzfd.png)

> **자손 클래스의 인스턴스를 생성하면 조상 클래스의 멤버와 자손 클래스의 멤버가 합쳐진 하나의 인스턴스로 생성된다.**

</br>

## 1.2 클래스간의 관계 - 포함관계

상속이외에도 클래스를 재사용하는 또 다른 방법이 있는데, 그것은 클래스간에 '포함(Composite)'관계를 맺어 주는 것이다. 클래스 간의 포함관계를 맺어 주는 것은 한 클래스의 멤버변수로 다른 클래스의 타입의 참조변수를 선언하는 것을 뜻한다

원(Circle)을 표현하기 위한 `Circle`이라는 클래스를 다음과 같이 작성하였다.

``` java
class Circle {
    int x;  // 원점의 x좌표
    int y;  // 원점의 y좌표
    int r;  // 반지름(radius)
}
```

그리고 좌표상의 한 점을 다루기 위한 `Point`클래스를 다음과 같이 작성하였다.

``` java
class Point {
    int x;  // x좌표
    int y;  // y좌표
}
```

`Point`클래스를 재사용해서 `Circle`클래스를 작성한다면 다음과 같이 할 수 있다.

![image](https://ifh.cc/g/hytLhN.png)

이와 같이 한 클래스를 작성하는 데 다른 클래스를 멤버변수로 선언하여 포함시키는 것은 좋은 생각이다. 하나의 거대한 클래스를 작성하는 것보다 단위별로 여러 개의 클래스를 작성한 다음, 이 단위 클래스들을 포함관계로 재사용하면 보다 간결하고 손쉽게 클래스를 작성할 수 있다. 또한 작성된 클래스들은 다른 클래스를 작성하는데 재사용될 수 있다.

``` java
class Car {
    Engine e = new Engine();    // 엔진
    Door[] d = new Door[4]; // 문, 문의 개수를 넷으로 가정하고 배열로 처리했다.
    // ...
}
```

위와 같은 `Car`클래스를 작성할 때, `Car`클래스의 단위구성요소인 `Engine`, `Door`와 같은 클래스를 미리 작성해 놓고 이들을 `Car`클래스의 멤버변수로 선언하여 포함관계를 맺어주면, 클래스를 작성하는 것도 쉽고 코드도 간결해서 이해하기 쉽다. 그리고 단위클래스별로 코드가 작게 나뉘어 작성되어 있기 때문에 코드를 관리하는데도 수월하다.

</br>

## 1.3 클래스간의 관계 결정하기

클래스를 작성하는데 있어서 상속관계를 맺어 줄 것인지 포함관계를 맺어 줄 것인지 결정하는 것은 때때로 혼돈스러울 수 있다.

전에 예를 든 `Circle`클래스의 경우, `Point`클래스를 포함시키는 대신 상속관계를 맺어주었다면 다음과 같다.

![image](https://ifh.cc/g/c3mAdR.png)

두 경우를 비교해 보면 `Circle`클래스를 작성하는데 있어서 `Point`클래스를 포함시키거나 상속받도록 하는 것은 결과적으로 별 차이가 없어 보인다.
그럴 때는 '~은 ~이다.(is-a)'와 '~은 ~을 가지고 있다(has-a)'를 넣어서 문장을 만들어 보면 클래스 간의 관계가 보다 명확해 진다

> 원(Circle)은 점(Point)**이다.** - Circle **is a** Point.   
원(Circle)은 점(Point)을 **가지고 있다.** - Circle **has a** Point.

원은 원점(Point)과 반지름으로 구성되므로 위의 두 문장을 비교해 보면 첫 번째 문장보다 두 번째 문장이 더 옳다는 것을 알 수 있다.

이처럼 클래스를 가지고 문장을 만들었을 때 '~은 ~이다.'라는 문장이 성립된다면, 서로 상속관계를 맺어 주고, '~은 ~을 가지고 있다.'는 문장이 성립한다면 포함관계를 맺어 주면 된다. 그래서 `Circle`클래스와 `Point`클래스 간의 관계는 상속관계 보다 포함관계를 맺어 주는 것이 옳다.

몇 가지 더 예를 들면, `Car`클래스와 `SportsCar`클래스는 'SportsCar는 Car이다.'와 같이 문장을 만드는 것이 더 옳기 때문에 이 두 클래스는 `Car`클래스를 조상으로 하는 상속관계를 맺어 주어야 한다.

`Card`클래스와 `Deck`클래스는 'Deck은 Card를 가지고 있다.'와 같이 문장을 만드는 것이 더 옳기 때문에 `Deck`클래스에 `Card`클래스를 포함시켜야 한다.

> **상속관계** '~은 ~이다.(is-a)'   
**포함관계** '~은 ~을 가지고 있다.(has-a)'

> 프로그램의 모든 클래스를 분석하여 가능한 많은 관계를 맺도록 노력해서 코드의 재사용성을 높여야 한다.

예제 7-2 / ch7 / DrawShape.java

``` java
class Shape {
	String color = "black";
	void draw() {
		System.out.printf("[color = %s]%n", color);
	}
}

class Point {
	int x;
	int y;
	
	Point(int x, int y) {
		this.x = x;
		this.y = y;
	}
	
	Point() {
		this(0, 0);
	}
	
	String getXY() {
		return "(" + x + ", " + y + ")";	// x와 y의 값을 문자열로 반환
	}
}

class Circle extends Shape {
	Point center;	// 원의 원점좌표
	int r;	// 반지름
	
	Circle() {
		this(new Point(0, 0), 100);	// Circle(Point center, int r)를 호출
	}
	
	Circle(Point center, int r) {
		this.center = center;
		this.r = r;
	}
	
	void draw() {	// 원을 그리는 대신에 원의 정보를 출력하도록 함
		System.out.printf("[center = (%d, %d), r = %d, color = %s]%n", center.x, center.y, r, color);
	}
}

class Triangle extends Shape {
	Point[] p = new Point[3];	// 3개의 Point인스턴스를 담을 배열을 생성한다.
	
	Triangle(Point[] p) {
		this.p = p;
	}
	
	void draw() {
		System.out.printf("[p1 = %s, p2 = %s, p3 = %s, color = %s]%n", p[0].getXY(), p[1].getXY(), p[2].getXY(), color);
	}
}

public class DrawShape {
	public static void main(String[] args) {
		Point[] p = {	new Point(100, 100),
					    new Point(140, 50),
					    new Point(200, 100)	
					};
		
		Triangle t = new Triangle(p);
		Circle c = new Circle(new Point(150, 150), 50);
		
		t.draw();	// 삼각형을 그린다.
		c.draw();	// 원을 그린다.
	}
}
```

```
[p1 = (100, 100), p2 = (140, 50), p3 = (200, 100), color = black]
[center = (150, 150), r = 50, color = black]
```

도형을 의미하는 `Shape`클래스를 정의하고, 2차원 좌표에서의 점을 의미하는 `Point`클래스를 정의한 다음, 이 두 클래스를 재활용해서 `Circle`클래스와 `Triangle`클래스를 정의하였다. 앞서 배운 'is-a'와 'has-a'로 클래스간의 관계를 어떻게 맺어야하는지 확인해보겠다.

**A Circle is a Shape. // 1. 원은 도형이다.**   
A Circle is a Point. // 2. 원은 점이다?   
A Circle has a Shape. // 3. 원은 도형을 가지고 있다?   
**A Circle has a Point. // 4. 원은 점을 가지고 있다.**

네 문장 중에서 첫 번째와 네 번째 문장이 자연스럽다는 것을 쉽게 알 수 있다. 클래스 간의 관계를 결정하는 것이 매번 이렇게 딱 떨어지는 건 아니지만, 적어도 클래스간의 관계를 맺어주는데 필요한 가장 기본적인 원칙에 대한 감은 잡을 수 있다.

`Circle`을 `Shape`와 상속관계로, 그리고 `Point`와는 포함관계로 정의하면 다음과 같다.

``` java
class Circle extends Shape {    // Circle과 Shape는 상속관계
    Point center;   // Circle과 Point는 포함관계
    int r;
        ...
}
```

`Circle`클래스는 `Shape`클래스로부터 모든 멤버를 상속받았으므로, `Shape`클래스에 정의된 `color`이나 `draw()`를 사용할 수 있다.

``` java
class Shape {
    String color = "black";

    void draw() {
        System.out.printf("[color = %s]%n", color);
    }
}
```

그러나 `Circle`클래스에도 `draw()`가 정의되어 있다면, `Circle`클래스의 `draw()`가 호출된다.

``` java
class Circle extends Shape {
    ...	
	void draw() {	// 원을 그리는 대신에 원의 정보를 출력하도록 함
		System.out.printf("[center = (%d, %d), r = %d, color = %s]%n", center.x, center.y, r, color);
	}
}
```

이처럼 조상 클래스에 정의된 메소드와 같은 메소드를 자손 클래스에 정의하는 것을 '오버라이딩'이라고 한다.

그리고 한 가지 더 설명할 것은 `Circle`인스턴스를 생성하는 문장이다.

``` java
Circle c = new Circle(new Point(150, 150), 50);
```

위 문장이 좀 복잡해 보이지만, 아래의 두 문장을 하나로 합쳐놓은 것이다.

``` java
Point p = new Point(150, 150);
Circle c = new Circle(p, 50);
```

예제 7-3 / ch7 / DeckTest.java

``` java
class Card {
	static final int KIND_MAX = 4;	// 카드 무늬의 수
	static final int NUM_MAX = 13;	// 무늬별 카드 수
	
	static final int SPADE = 4;
	static final int DIAMOND = 3;
	static final int HEART = 2;
	static final int CLOVER = 1;
	int kind;
	int number;
	
	Card() {
		this(SPADE, 1);
	}
	
	Card(int kind, int number) {
		this.kind = kind;
		this.number = number;
	}
	
	public String toString() {
		String[] kinds = {"", "CLOVER", "HEART", "DIAMOND", "SPADE"};
		String numbers = "0123456789XJQK";	// 숫자 10은 X로 표현
		return "kind : " + kinds[this.kind] + ", number : " + numbers.charAt(this.number);
	}	// toString()의 끝
}	// Card클래스의 끝

class Deck {
	final int CARD_NUM = 52;	// 카드의 개수
	Card cardArr[] = new Card[CARD_NUM];	// Card객체 배열을 포함
	
	Deck() {	// Deck의 카드를 초기화한다.
		int i = 0;
		
		for(int k = Card.KIND_MAX; k > 0; k--) {
			for(int n = 0; n < Card.NUM_MAX; n++) {
				cardArr[i++] = new Card(k, n + 1);
			}
		}
	}
	
	Card pick(int index) {	// 지정된 위치(index)에 있는 카드 하나를 꺼내서 반환
		return cardArr[index];
	}
	
	Card pick() {	// Deck에서 카드 하나를 선택한다.
		int index = (int)(Math.random() * CARD_NUM);
		return pick(index);
	}
	
	void shuffle() {	// 카드의 순서를 섞는다.
		for(int i = 0; i < cardArr.length; i++) {
			int r = (int)(Math.random() * CARD_NUM);
			
			Card temp = cardArr[i];
			cardArr[i] = cardArr[r];
			cardArr[r]= temp; 
		}
	}
}

public class DeckTest {
	public static void main(String[] args) {
		Deck d = new Deck();	// 카드 한 벌(Deck)을 만든다.
		Card c = new Card();	// 섞기 전에 제일 위의 카드를 뽑는다.
		System.out.println(c);	// System.out.println(c.toString());과 같다.
		
		d.shuffle();	// 카드를 섞는다.
		c = d.pick(0);	// 섞은 후에 제일 위의 카드를 뽑느다.
		System.out.println(c);
	}
}
```

```
kind : SPADE, number : 1
kind : HEART, number : J
```

`Deck`클래스를 작성하는데 `Card`클래스를 재사용하여 포함관계로 작성하였다. 카드 한 벌(Deck)은 모두 52장의 카드로 이루어져 있으므로 `Card`클래스를 크기가 52인 배열로 처리하였다. `shuffle()`은 카드 한 벌의 첫 번째 카드부터 순서대로 임의로 위치에 있는 카드와 위치를 서로 바꾸는 방식으로 카드를 섞는다. `random()`을 사용했기 때문에 매 실행 시 마다 결과가 다르게 나타난다.

`pick()`은 `Card`객체 배열 `cardArr`에 저장된 `Card`객체 중에서 하나를 꺼내서 반환한다. `Card`객체 배열은 참조변수 배열이고, 이 배열에 실제로 저장된 것은 객체가 아니라 객체의 주소다.

아래의 문장에서 `pick(0)`을 호출하면, 매개변수 `index`의 값이 0이 되므로, `cardArr[0]`에 저장된 `Card`객체의 주소가 참조변수 `c`에 저장된다.

``` java
Card c = d.pick(0); // pick(int index)를 호출

Card pick(int index) {
    return cardArr[index];
}
```

예를 들어 `index`의 값이 0이고, `cardArr[0]`의 값이 0x200이라면 `pick(0)`은 다음과 같은 과정으로 계산된다.

``` java
    return cardArr[index];
→   return cardArr[0];
→   return 0x200;
```

그래서 참조변수 `c`에 0x200, 즉 `cardArr[0]`에 저장된 `Card`인스턴스의 주소가 저장된다.

한 가지 더 설명할 것은 `Card`클래스에 정의된 `toString()`인데, `toString()`은 인스턴스의 정보를 문자열로 반환할 목적으로 정의된 것이다. 아래의 코드처럼 참조변수 `c`를 출력하면, 참조변수 `c`가 가리키고 있는 인스턴스에 `toString()`을 호출하여 그 결과를 화면에 출력한다.

``` java
Deck d = new Deck();	// 카드 한 벌(Deck)을 만든다.
Card c = new Card();	// 섞기 전에 제일 위의 카드를 뽑는다.
System.out.println(c);	// System.out.println(c.toString());과 같다.

// System.out.println("Card : " + c.toString());과 같다.
System.out.println("Card : " + c);
```

결국 `System.out.println(c)`는 `System.out.println(c.toString());`와 같은 결과를 얻는다.

이처럼 참조변수의 출력이나 덧셈연산자를 이용한 참조변수와 문자열의 결합에는 `toString()`이 자동적으로 호출되어 참조변수를 문자열로 대치한 후 처리한다.

`toString()`은 모든 클래스의 조상인 `Object`클래스에 정의된 것으로, 어떤 종류의 객체에 대해서도 `toString()`을 호출하는 것이 가능하다.

</br>

## 1.4 단일 상속(single inheritance)

다른 객체지향언어인 C++에서는 여러 조상 클래스로부터 상속받는 것이 가능한 '다중상속(multiple inheritance)'을 허용하지만 자바에서는 오직 단일 상속만을 허용한다. 그래서 둘 이상의 클래스로부터 상속을 받을 수 없다. 예를 들어 `TV`클래스와 `VCR`클래스가 있을 때, 이 두 클래스로부터 상속을 받는 `TVCR`클래스를 작성할 수 없다.

그래서 `TVCR`클래스는 조상 클래스로 `TV`클래스와 `VCR`클래스 중 하나만 선택해야 한다.

``` java
class TVCR extends TV, VCR {    // 에러. 조상은 하나만 허용한다.
    // ...
}
```

다중상속을 허용하면 여러 클래스로부터 상속받을 수 있기 때문에 복합적인 기능을 가진 클래스를 쉽게 작성할 수 있다는 장점이 있지만, 클래스간의 관계가 매우 복잡해진다는 것과 서로 다른 클래스로부터 상속받은 멤버간의 이름이 같은 경우 구별할 수 있는 방법이 없다는 단점을 가지고 있다.

만일 다중상속을 허용해서 `TVCR`클래스가 `TV`클래스와 `VCR`클래스를 모두 조상으로 하여 두 클래스의 멤버들을 상속받는다고 가정해보겠다.

`TV`클래스에도 `power()`라는 메소드가 있고, `VCR`클래스에도 `power()`라는 메소드가 있을 때 둘 다 상속받게 된다면, `TVCR`클래스 내에서 선언부(이름과 매개변수)만 같고 서로 다른 내용의 두 메소드를 구별할 수 없다.

static메소드라면 메소드 이름 앞에 클래스의 이름을 붙여서 구별할 수 있다지만, 인스턴스 메소드의 경우 선언부가 같은 두 메소드를 구별할 수 있는 방법은 없다.

이것을 해결하는 방법은 조상 클래스의 메소드의 이름이나 매개변수를 바꾸는 방법 밖에 없다. 이렇게 하면 그 조상 클래스의 `power()`메소드를 사용하는 모든 클래스들도 변경을 해야 하므로 그리 간단한 문제가 아니다.

자바에서는 다중상속의 이러한 문제점을 해결하기 위해 다중상속의 장점을 포기하고 단일상속만을 허용한다.

단일 상속이 하나의 조상 클래스만을 가질 수 있기 때문에 다중상속에 비해 불편한 점도 있지만, 클래스 간의 관계가 보다 명확해지고 콛를 더욱 신뢰할 수 있게 만들어 준다는 점에서 다중상속보다 유리하다.

예제 7-4 / ch7 / TVCR.java

``` java
class VCR {
	boolean power;	// 전원상태(on/off)
	int counter = 0;
	void power() { power = !power; }
	void play() { /* 내용 생략 */ }
	void stop() { /* 내용 생략 */ }
	void rew() { /* 내용 생략 */ }
	void ff() { /* 내용 생략 */ }
}

class TVCR extends Tv {
	VCR vcr = new VCR();
	
	void play() {
		vcr.play();
	}
	
	void stop() {
		vcr.stop();
	}
	
	void rew() {
		vcr.rew();
	}
	
	void ff() {
		vcr.ff();
	}
}
```

자바는 다중상속을 허용하지 않으므로 `Tv`클래스를 조상으로 하고, `VCR`클래스는 `TVCR`클래스에 포함시켰다. 그리고 `TVCR`클래스에 `VCR`클래스의 메소드와 일치하는 선언부를 가진 메소드를 선언하고 내용은 `VCR`클래스의 것을 호출해서 사용하도록 했다. 외부적으로는 `TVCR`클래스의 인스턴스를 사용하는 것처럼 보이지만 내부적으로는 `VCR`클래스의 인스턴스를 생성해서 사용하는 것이다.

이렇게 함으로써 `VCR`클래스의 메소드의 내용이 변경되더라도 `TVCR`클래스의 메소드들 역시 변경된 내용이 적용되는 결과를 얻을 수 있다.

</br>

## 1.5 Object클래스 - 모든 클래스의 조상

`Object`클래스는 모든 클래스 상속계층도의 최상위에 있는 조상클래스이다. 다른 클래스로부터 상속 받지 않는 모든 클래스들은 자동적으로 `Object`클래스로부터 상속받게 함으로써 이것을 가능하게 힌다.

만일 다음과 같이 다름 클래스로부터 상속을 받지 않는 `Tv`클래스를 정의하였다고 가정하겠다.

``` java
class Tv {
    ...
}
```

위의 코드를 컴파일 하면 컴파일러는 위의 코드를 다음과 같이 자동적으로 `extends Object`를 추가하여 `Tv`클래스가 `Object`클래스로부터 상속받도록 한다.

``` java
class Tv extends Object {
    ...
}
```

이렇게 함으로써 `Obeject`클래스가 모든 클래스의 조상이 되도록 한다. 만일 다른 클래스로부터 상속을 받는다고 하더라도 상속계층도를 따라 조상클래스, 조상클래스의 조상클래스를 찾아 올라가다 보면 결국 마지막 최상위 조상은 `Object`클래스이다.

> 이미 어떤 클래스로부터 상속받도록 작성된 클래스에 대해서는 컴파일러가 'extends Object'를 추가하지 않는다.

``` java
class Tv {
    ...
}

class CaptionTv extends Tv {
    ...
}
```

위와 같이 `Tv`클래스가 있고, `Tv`클래스를 상속받는 `CaptionTv`가 있을 때 상속계층도는 다음과 같다.

![image](https://ifh.cc/g/mlSgYN.png)

> 상속계층도를 단순화하기 위해서 Object클래스를 생략하는 경우가 많다.

이처럼 모든 상속계층도의 최상위에는 `Object`클래스가 위치한다. 그래서 자바의 모든 클래스들은 `Object`클래스의 멤버들을 상속 받기 때문에 `Object`클래스에 정의된 멤버들을 사용할 수 있다.

그동안 `toString()`이나 `equals(Object o)`와 같은 메소드를 따로 정의하지 않고도 사용할 수 있었던 이유는 이 메소드들이 `Object`클래스에 정의된 것들이기 때문이다.

`Obeject`클래스에는 `toString()`, `equals()`와 같은 모든 인스턴스가 가져야 할 기본적인 11개의 메소드가 정의되어 있다.