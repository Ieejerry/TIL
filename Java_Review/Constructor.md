Chapter 6. 객체지향 프로그래밍1

# 5. 생성자(Constructor)

</br>

## 5.1 생성자란?

생성자는 인스턴스가 생성될 때 호출되는 '인스턴스 초기화 메소드
이다. 따라서 인스턴스변수의 초기화 작업에 주로 사용되며, 인스턴스 생성 시에 실행되어야 할 작업을 위해서도 사용된다.

> 인스턴스 초기화란, 인스턴스변수들을 초기화하는 것을 뜻한다.

생성자 역시 메소드처럼 클래스 내에 선언되며, 구조도 메소드와 유사하지만 리턴값이 없다는 점이 다르다. 그렇다고 해서 생성자 앞에 리턴값이 없음을 뜻하는 키워드 `void`를 사용하지는 않고, 단지 아무 것도 적지 않는다. 생성자의 조건은 다음과 같다.

> 1. 생성자의 이름은 클래스의 이름과 같아야 한다.
> 2. 생성자는 리턴 값이 없다.

> 생성자도 메소드이기 때문에 리턴값이 없다는 의미의 void를 붙여야 하지만, 모든 생성자가 리턴값이 없으므로 void를 생략할 수 있게 한 것이다.

생성자는 다음과 같이 정의한다. 생성자도 오버로딩이 가능하므로 하나의 클래스에 여러 개의 생성자가 존재할 수 있다.

``` java
클래스이름(타입 변수명, 타입 변수명, ... ) {
    // 인스턴스 생성 시 수행될 코드,
    // 주로 인스턴스 변수의 초기화 코드를 적는다.
}

class Card {
    Card() {    // 매개변수가 없는 생성자.
        ...
    }

    Card(String k, int num) {   // 매개변수가 있는 생성자.
        ...
    }
    ...
}
```

**연산자 `new`가 인스턴스를 생성하는 것이지 생성자가 인스턴스를 생성하는 것이 아니다.** 생성자는 단순히 인스턴스변수들의 초기화에 사용되는 조금 특별한 메소드일 뿐이다.

`Card`클래스의 인스턴스를 생성하는 코드를 예로 들어, 수행되는 과정을 단계별로 나누어 보면 다음과 같다.

``` java
Card c = new Card();

// 1. 연산자 new에 의해서 메모리(heap)에 Card클래스의 인스턴스가 생성된다.
// 2. 생성자 Card()가 호출되어 수행된다.
// 3. 연산자 new의 결과로, 생성된 Card인스턴스의 주소가 반환되어 참조변수 c에 저장된다.
```

인스턴스를 생성하기 위해 사용해왔던 '클래스이름()'이 바로 생성자이다. 인스턴스를 생성할 때는 반드시 클래스 내에 정의된 생성자 중의 하나를 선택하여 지정해주어야 한다.

</br>

## 5.2 기본 생성자(default constructor)

모든 클래스에는 반드시 하나 이상의 생성자가 정의되어 있어야 한다.

컴파일러가 제공하는 '기본 생성자(default constructor)' 덕분에 클래스에 생성자를 정의하지 않고도 인스턴스를 생성할 수 있다.

컴파일 할 때, 소스파일(*.java)의 클래스에 생성자가 하나도 정의되지 않은 경우 컴파일러는 자동적으로 아래와 같은 내용의 기본 생성자를 추가하여 컴파일 한다.

``` java
클래스이름() { }

Card() { }
```

컴파일러가 자동적으로 추가해주는 기본 생성자는 이와 같이 매개변수도 없고 아무런 내용도 없는 아주 간단한 것이다.

> 클래스의 '접근 제어자(Access Modifier)'가 public인 경우에는 기본 생성자로 'public 클래스이름() {}'이 추가된다.

예제 6-23 / ch6 / ConstructorTest.java

``` java
class Data1 {
	int value;
}

class Data2 {
	int value;
	
	Data2(int x) {	// 매개변수가 있는 생성자
		value = x;
	}
}

public class ConstructorTest {

	public static void main(String[] args) {
		Data1 d1 = new Data1();
		Data2 d2 = new Data2();	// compile error 발생
	}

}
```

```
Exception in thread "main" java.lang.Error: Unresolved compilation problem: 
	The constructor Data2() is undefined

	at ConstructorTest.main(ConstructorTest.java:17)
```

이 예제를 컴파일 하면 위와 같은 에러메세지가 나타난다. 이것은 `Data2`에서 `Data2()`라는 생성자를 찾을 수 없다는 내용의 내용의 에러메세지인데, `Data2`에 생성자 `Data2()`가 정의되어 있지 않기 때문에 에러가 발생한 것이다.

`Data1`에는 정의되어 있는 생성자가 하나도 없으므로 컴파일러가 기본 생성자를 추가해주었지만, `Data2`에는 이미 생성자 `Data2(int x)`가 정의되어 있으므로 기본 생성자가 추가되지 않았기 때문이다.

컴파일러가 자동적으로 기본 생성자를 추가해주는 경우는 '클래스 내에 생성자가 하나도 없을 때'뿐이다.

![image](https://ifh.cc/g/gfWGYQ.png)

이 예제에서 컴파일 에러가 발생하지 않도록 하기 위해서는 위의 오른쪽 코드와 같이 `Data2`의 인스턴스를 생성할 때 생성자 `Data2(int x)`를 사용하던가, 아니면 클래스 `Data2`에 생성자 `Data2()`를 추가로 정의해주면 된다.

> **기본 생성자가 컴파일러에 의해서 추가되는 경우는 클래스에 정의된 생성자가 하나도 없을 때 뿐이다.**

</br>

## 5.3 매개변수가 있는 생성자

생성자도 메소드처럼 매개변수를 선언하여 호출 시 값을 넘겨받아서 인스턴스의 초기화 작업에 사용할 수 있다. 인스턴스마다 각기 다른 값으로 초기화되어야하는 경우가 많기 때문에 매개변수를 사용한 초기화는 매우 유용하다.

아래의 코드는 자동차를 클래스로 정의한 것인데, 단순히 `color`, `gearType`, `door` 세 개의 인스턴스변수와 두 개의 생성자만을 가지고 있다.

``` java
class Car {
    String color;       // 색상
    String gearType;    // 변속기 종류 - auto(자동), manual(수동)
    int door;           // 문의 개수

    Car() {}            // 생성자
    Car(String c, String g, int d) {    // 생성자
        color = c;
        gearType = g;
        door = d;
    }
}
```

`Car`인스턴스를 생성할 때, 생성자 `Car()`를 사용한다면, 인스턴스를 생성한 다음에 인스턴스변수들을 따로 초기화해주어야 하지만, 매개변수가 있는 생성자 `Car(String color, String gearType, int door)`를 사용한다면 인스턴스를 생성하는 동시에 원하는 값으로 초기화를 할 수 있게 된다.

인스턴스를 생성한 다음에 인스턴스변수의 값을 변경하는 것보다 매개변수를 갖는 생성자를 사용하는 것이 코드를 보다 간결하고 직관적으로 만든다.

![image](https://ifh.cc/g/tx8a4h.png)

위의 양쪽 코드 모두 같은 내용이지만, 오른쪽 코드가 더 간결하고 직관적이다. 이처럼 클래스를 작성할 때 다양한 생성자를 제공함으로써 인스턴스 생성 후에 별도로 초기화를 하지 않아도 되도록 하는 것이 바람직하다.

예제 6-24 / ch6 / CarTest.java

``` java
class Car {
	String color;	// 색상
	String gearType;	// 변속기 종류 - auto(자동), manual(수동)
	int door;	// 문의 개수
	
	Car() {}
	
	Car(String c, String g, int d) {
		color = c;
		gearType = g;
		door = d;
	}
}


public class CarTest {

	public static void main(String[] args) {
		Car c1 = new Car();
		c1.color = "white";
		c1.gearType = "auto";
		c1.door = 4;
		
		Car c2 = new Car("white", "auto", 4);
		
		System.out.println("c1의 color = " + c1.color + ", gearType = " + c1.gearType + ", door = " + c1.door);
		System.out.println("c2의 color = " + c1.color + ", gearType = " + c1.gearType + ", door = " + c1.door);
	}

}
```

```
c1의 color = white, gearType = auto, door = 4
c2의 color = white, gearType = auto, door = 4
```

## 5.4 생성자에서 다른 생성자 호출하기 - this(), this

같은 클래스의 멤버들 간에 서로 호출할 수 있는 것처럼 생성자 간에도 서로 호출이 가능하다. 단 다음의 두 조건을 만족시켜야 한다.

> - 생성자의 이름으로 클래스이름 대신 this를 사용한다.
> - 한 생성자에서 다른 생성자를 호출할 때는 반드시 첫 줄에서만 호출이 가능하다.

다음의 코드는 생성자를 작성할 때 지켜야하는 두 조건을 모두 만족시키지 못했기 때문에 에러가 발생한다.

``` java
Car(String color) {
	door = 5;	// 첫번째 줄
	Car(color, "auto", 4);	// 에러1. 생성자의 두 번째 줄에서 다른 생성자 호출
							// 에러2. this(color, "auto" 4);로 해야함
}
```

생성자 내에서 다른 생성자를 호출할 때는 클래스이름인 `Car`대신 `this`를 사용해야하는데 그러지 않아서 에러이고, 또 다른 에러는 생성자 호출이 첫 번째 줄이 아닌 두 번째 줄이기 때문에 에러이다.

생성자에서 다른 생성자를 첫 줄에서만 호출이 가능하도록 한 이유는 생성자 내에서 초기화 작업도중에 다른 생성자를 호출하게 되면, 호출된 다른 생성자 내에서도 멤버변수들의 값을 초기화를 할 것이므로 다른 생성자를 호출하기 이전의 초기화 작업이 무의미해질 수 있기 때문이다.

예제 6-25 / ch6 / CarTest2.java

``` java
class Car2 {
	String color;	// 색상
	String gearType;	// 변속기 종류 - auto(자동), manual(수동)
	int door;	// 문의 개수
	
	Car2() {
		this("white", "auto", 4);
	}
	
	Car2(String color) {
		this(color, "auto", 4);
	}
	
	Car2(String color, String gearType, int door) {
		this.color = color;
		this.gearType = gearType;
		this.door = door;
	}
}

public class CarTest2 {

	public static void main(String[] args) {
		Car2 c1 = new Car2();
		Car2 c2 = new Car2("blue");
		
		System.out.println("c1의 color = " + c1.color + ", gearType = " + c1.gearType + ", door = " + c1.door);
		System.out.println("c2의 color = " + c2.color + ", gearType = " + c2.gearType + ", door = " + c2.door);
	}

}
```

```
c1의 color = white, gearType = auto, door = 4
c2의 color = blue, gearType = auto, door = 4
```

생성자 `Car2()`에서 또 다른 생성자 `Car2(String color, String gearType, int door)`를 호출하였다. 이처럼 생성자간의 호출에는 생성자의 이름 대신 `this`를 사용해야만 하므로 `Car2` 대신 `this`를 사용했다. 그리고 생성자 `Car2()`의 첫째 줄에서 호출하였다.

![image](https://ifh.cc/g/ROo2mz.png)

위 코드는 양쪽 모두 같은 일을 하지만 오른쪽의 코드는 생성자 `Car2(String color, String gearType, int door)`를 활용해서 더 간략히 한 것이다. `Car2 c1 = new Car2();`와 같이 생생자 `Car2()`를 사용해서 `Car2`인스턴스를 생성한 경우에, 인스턴스변수 `color`는 "white", `gearType`은 "auto", `door`은 4로 초기화 되도록 하였다.

이것은 마치 실생활에서 자동차(`Car2`인스턴스)를 생성할 때, 아무런 옵션도 주지 않으면, 기본적으로 흰색(white)에 자동변속기(auto) 그리고 문의 개수가 4개인 자동차가 생산되도록 하는 것에 비유할 수 있다.

같은 클래스 내의 생성자들은 일반적으로 서로 관계가 깊은 경우가 많아서 이처럼 서로 호출하도록 하여 유기적으로 연결해주면 더 좋은 코드를 얻을 수 있다. 그리고 수정이 필요한 경우에도 보다 적은 코드만을 변경하면 되므로 유지보수가 쉬워진다.

![image](https://ifh.cc/g/RFpzsp.png)

왼쪽 코드의 `color = c;`는 생성자의 매개변수로 선언된 지역변수 `c`의 값을 인스턴스 변수 `color`에 저장한다. 이 때 변수 `color`와 `c`는 이름만으로도 서로 구별되므로 아무런 문제가 없다.

하지만, 오른쪽 코드에서처럼 생성자의 매개변수로 선언된 변수의 이름이 `color`로 인스턴스변수 `color`와 같을 경우에는 이름만으로는 두 변수가 서로 구별이 안 된다. 이런 경우에는 인스턴스변수 앞에 `this`를 사용하면 된다.

이렇게 하면 `this.color`는 인스턴스변수이고, `color`는 생성자의 매개변수로 정의된 지역변수로 서로 구별이 가능하다. 만일 오른쪽 코드에서 `this.color = color;`대신 `color = color;`와 같이하면 둘 다 지역변수로 간주된다.

이처럼 생성자의 매개변수로 인스턴스변수들의 초기값을 제공받는 경우가 많기 때문에 매개변수와 인스턴스변수의 이름이 일치하는 경우가 자주 있다. 이 때는 왼쪽코드와 같이 매개변수이름을 다르게 하는 것 보다 `this`를 사용해서 구별되도록 하는 것이 의미가 더 명확하고 이해하기 쉽다.

`this`는 참조변수로 인스턴스 자신을 가르킨다. 참조변수를 통해 인스턴스의 멤버에 접근할 수 있는 것처럼, `this`로 인스턴스변수에 접근할 수 있는 것이다.

하지만, `this`를 사용할 수 있는 것은 인스턴스멤버뿐이다. static메소드(클래스메소드)에서는 인스턴스 멤버들을 사용할 수 없는 것처럼, `this` 역시 사용할 수 없다. 왜냐하면, static메소드는 인스턴스를 생성하지 않고도 호출될 수 있으므로 static메소드가 호출된 시점에 인스턴스가 존재하지 않을 수도 있기 때문이다.

사실 생성자를 포함한 모든 인스턴스메소드에는 자신이 관련된 인스턴스를 가리키는 참조변수 `this`가 지역변수로 숨겨진 채로 존재한다.

일반적으로 인스턴스메소드는 특정 인스턴스와 관련된 작업을 하기 때문에 자신과 관련된 인스턴스의 정보가 필요하지만, static메소드는 인스턴스와 관련 없는 작업을 하므로 인스턴스에 대한 정보가 필요 없기 때문이다.

> **this** 인스턴스 자신을 가리키는 참조변수, 인스턴스의 주소가 저장되어 있다. 모든 인스턴스메소드에 지역변수로 숨겨진 채로 존재한다.
> **this(),this(매개변수)** 생성자, 같은 클래스의 다른 생성자를 호출할 때 사용한다.

> this와 this()는 비슷하게 생겼을 뿐 완전히 다른 것이다. this는 '참조 변수'이고, this()는 '생성자'이다.

</br>

## 5.5 생성자를 이용한 인스턴스의 복사

현재 사용하고 있는 인스턴스와 같은 상태를 갖는 인스턴스를 하나 더 만들고자 할 때 생성자를 이용할 수 있다. 두 인스턴스가 같은 상태를 갖는다는 것은 두 인스턴스의 모든 인스턴스 변수(상태)가 동일한 값을 갖고 있다는 것을 뜻한다.

하나의 클래스로부터 생성된 모든 인스턴스의 메소드와 클래스변수는 서로 동일하게 때문에 인스턴스간의 차이는, 인스턴스마다 각기 다른 값을 가질 수 있는 인스턴스변수 뿐이다.

``` java
Car2(Car c) {
	color = c.color;
	gearType = c.gearType;
	door = c.door;
}
```

위의 코드는 `Car2`클래스의 참조변수를 매개변수로 선언한 생성자이다. 매개변수로 넘겨진 참조변수가 가리키는 `Car2`인스턴스의 인스턴스변수인 `color`, `gearType`, `door`의 값을 인스턴스 자신으로 복사하는 것이다.

어떤 인스턴스의 상태를 전혀 알지 못해도 똑같은 상태의 인스턴스를 추가로 생성할 수 있다. Java API의 많은 클래스들이 인스턴스의 복사를 위한 생성자를 정의해놓고 있다.

> Object클래스에 정의된 clone메소드를 이용하면 간단히 인스턴스를 복사할 수 있다.

예제 6-26 / ch6 / CarTest3.java

``` java
class Car3 {
	String color;	// 색상
	String gearType;	// 변속기 종류 - auto(자동), manual(수동)
	int door;	// 문의 개수
	
	Car3() {
		this("white", "auto", 4);
	}
	
	Car3(Car3 c) {	// 인스턴스 복사를 위한 생성자
		color = c.color;
		gearType = c.gearType;
		door = c.door;
	}
	
	Car3(String color, String gearType, int door) {
		this.color = color;
		this.gearType = gearType;
		this.door = door;
	}
}

public class CarTest3 {

	public static void main(String[] args) {
		Car3 c1 = new Car3();
		Car3 c2 = new Car3(c1);	// c1의 복사본 c2를 생성한다.
		System.out.println("c1의 color = " + c1.color + ", gearType = " + c1.gearType + ", door = " + c1.door);
		System.out.println("c2의 color = " + c2.color + ", gearType = " + c2.gearType + ", door = " + c2.door);
		c1.door = 100;	// c1의 인스턴스변수 door의 값을 변경한다.
		System.out.println("c1.door = 100; 수행 후");
		System.out.println("c1의 color = " + c1.color + ", gearType = " + c1.gearType + ", door = " + c1.door);
		System.out.println("c2의 color = " + c2.color + ", gearType = " + c2.gearType + ", door = " + c2.door);
	}

}
```

```
c1의 color = white, gearType = auto, door = 4
c2의 color = white, gearType = auto, door = 4
c1.door = 100; 수행 후
c1의 color = white, gearType = auto, door = 100
c2의 color = white, gearType = auto, door = 4
```

인스턴스 `c2`는 `c1`을 복사하여 생성된 것으므로 서로 같은 상태를 갖지만, 서로 독립적으로 메모리공간에 존재하는 별도의 인스턴스이므로 `c1`의 값들이 변경되어도 `c2`는 영향을 받지 않는다.

생성자 `Car3(Car3 c)`는 아래와 같이 다른 생성자인 `Car3(String color, String gearType, int door)`를 호출하는 것이 바람직하다. 무작정 새로 코드를 작성하는 것보다 기존의 코드를 활용할 수 없는지 고민해야 한다.

![image](https://ifh.cc/g/moPprh.png)

> **인스턴스를 생설할 때는 다음의 2가지 사항을 결정해야 한다.**
> 1. 클래스 - 어떤 클래스의 인스턴스를 생성할 것인가?
> 2. 생성자 - 선택한 클래스의 어떤 생성자로 인스턴스를 생성할 것인가?