Chapter 7. 객체지향 프로그래밍2

# 5. 다형성(polymorphism)

</br>

## 5.1 다형성이란?

객체지향개념에서 다형성이란 '여러 가지 형태를 가질 수 있는 능력'을 의미하며, 자바에서는 한 타입의 참조변수로 여러 타입의 객체를 참조할 수 있도록 함으로써 다형성을 프로그램적으로 구현하였다.

이를 좀 더 구체적으로 말하자면, **조상클래스 타입의 참조변수로 자손클래스의 인스턴스를 참조할 수 있도록 하였다.** 예제를 통해서 보다 자세히 알아보도록 하겠다.

``` java
class Tv {
    boolean power;  // 전원상태(on/off)
    int channel;    // 채널

    void power() { power = !power; }
    void channelUp() { ++channel; }
    void channelDown() { --channel; }
}

class CaptionTv extends Tv {
    String text;    // 캡션을 보여 주기 위한 문자열
    void caption() { /* 내용 생략 */ }
}
```

`Tv`클래스와 `CaptionTv`클래스가 이와 같이 정의되어 있을 때, 두 클래스간의 관계를 그림을 나타내면 아래와 같다.

![image](https://ifh.cc/g/rK7Cjs.png)

클래스 `Tv`와 `CaptionTv`는 서로 상속관계에 있으며, 이 두 클래스의 인스턴스를 생성하고 사용하기 위해서는 다음과 같이 할 수 있다.

``` java
Tv t = new Tv();
CaptionTv c = new CaptionTv();
```

지금까지 생성된 인스턴스를 다루기 위해서, 인스턴스의 타입과 일치하는 타입의 참조변수만을 사용했다. 즉, `Tv`인스턴스를 다루기 위해서는 `Tv`타입의 참조변수를 사용하고, `CaptionTv`인스턴스를 다루기 우해서는 `CaptionTv`타입의 참조변수를 사용했다.

이처럼 인스턴스의 타입과 참조변수의 타입이 일치하는 것이 보통이지만, `Tv`와 `CaptionTv`클래스가 서로 상속관계에 있을 경우, 다음과 같이 조상 클래스 타입의 참조변수로 자손 클래스의 인스턴스를 참조하도록 하는 것도 가능하다.

``` java
Tv t = new CaptionTv(); // 조상 타입의 참조변수로 자손 인스턴스를 참조
```

``` java
CaptionTv c = new CaptionTv();
Tv t = new CaptionTv();
```

위의 코드에서 `CaptionTv`인스턴스 2개를 생성하고, 참조변수 `c`와 `t`가 생성된 인스턴스를 하나씩 참조하도록 하였다. 이 경우 실제 인스턴스가 `CaptionTv`타입이라 할지라도, 참조변수 `t`로는 `CaptionTv`인스턴스의 모든 멤버를 사용할 수 없다.

`Tv`타입의 참조변수로는 `CaptionTv`인스턴스 중에서 `Tv`클래스의 멤버들(상속받은 멤버포함)만 사용할 수 있다. 따라서, 생성된 `CaptionTv`인스턴스의 멤버 중에서 `Tv`클래스에 정의 되지 않은 멤버, `text`와 `caption()`은 참조변수 `t`로 사용이 불가능하다. 즉, `t.text` 또는 `t.caption()`와 같이 할 수 없다는 것이다. **둘 다 같은 타입의 인스턴스지만 참조변수의 타입에 따라 사용할 수 있는 멤버이 개수가 달라진다.**

![image](https://ifh.cc/g/TyRwcF.png)

> 실제로는 모든 클래스의 최고조상인 Object클래스로부터 상속받은 부분도 포함되어야 하지만 간단히 하기위해 생략했다.

반대로 아래와 같이 자손타입의 참조변수로 조상타입의 인스턴스를 참조하는 것은 가능하지 않다.

``` java
CaptionTv c = new Tv();
```

위의 코드를 컴파일 하면 에러가 발생한다. 그 이유는 실제 인스턴스인 `Tv`의 멤버 개수보다 참조변수 `c`가 사용할 수 있는 멤버 개수가 더 많기 때문이다. 그래서 이를 허용하지 않는다.

`CaptionTv`클래스에는 `text`와 `caption()`이 정의되어 있으므로 참조변수 `c`로는 `c.text`, `c.caption()`과 같은 방식으로 `c`가 참조하고 있는 인스턴스에서 `text`와 `caption()`을 사용하려 할 수 있다.

하지만 `c`가 참조하고 있는 인스턴스는 `Tv`타입이고, `Tv`타입의 인스턴스에는 `text`와 `caption()`이 존재하지 않기 때문에 이들을 사용하려 하면 문제가 발생한다.

그래서, 자손타입의 참조변수로 조상타입의 인스턴스를 참조하는 것은 존재하지 않는 멤버를 사용하고자 할 가능성이 있으므로 허용하지 않는 것이다. **참조변수가 사용할 수 있는 멤버의 개수는 인스턴스의 멤버 개수보다 같거나 적어야 한다.**

> 클래스는 상속을 통해서 확장될 수는 있어도 축소될 수는 없어서, 조상 인스턴스의 멤버 개수는 자손 인스턴스의 멤버 개수보다 항상 적거나 같다.

> 모든 참조변수는 null 또는 4 byte의 주소값이 저장되며, 참조변수의 타입은 참조할 수 있는 객체의 종류와 사용할 수 있는 멤버의 수를 결정한다

> 조상타입의 참조변수로 자손타입의 인스턴스를 참조할 수 있다.   
> 반대로 자손타입의 참조변수로 조상타입의 인스턴스를 참조할 수 없다.

</br>

## 5.2 참조변수의 형변환

기본형 변수와 같이 참조변수도 형변환이 가능하다. 단, 서로 상속관계에 있는 클래스사이에서만 가능하기 때문에 자손타입의 참조변수를 조상타입의 참조변수로, 조상타입의 참조변수를 자손타입의 참조변수로의 형변환만 가능하다.

> 바로 윗 조상이나 자손이 아닌, 조상의 조상으로도 형변환이 가능하다. 따라서 모든 참조변수는 모든 클래스의 조상인 Object클래스 타입으로 형변환이 가능하다.

기본형 변수의 형변환에서 작은 자료형에서 큰 자료형의 형변환은 생략이 가능하듯이, 참조형 변수의 형변환에서는 자손타입의 참조변수를 조상타입으로 형변환하는 경우에는 형변환을 생략할 수 있다.

> 자손타입 → 조상타입(Up-casting) : 형변환 생략가능   
> 자손타입 ← 조상타입(Down-casting) : 형변환 생략불가

조상타입의 참조변수를 자손타입의 참조변수로 변환하는 것을 다운캐스팅(down-casting)이라고 하며, 자손타입의 참조변수를 조상타입의 참조변수로 변환하는 것을 업캐스팅(up-casting)이라고 한다.

참조변수간의 형변환 역시 캐스트연산자를 사용하며, 괄호()안에 변환하고자 하는 타입의 이름(클래스명)을 적어주면 된다.

``` java
class Car {
    String color;
    int door;
    void drive() {  // 운전하는 기능
        System.out.println("drive, Brrr~");
    }
    void stop() {   // 멈추는 기능
        System.out.println("stop!!!");
    }
}

class FireEngine extends Car {  // 소방차
    void water() {  // 물 뿌리는 기능
        System.out.println("water!!!");
    }
}

class Ambulance extends Car {   // 엠뷸런스
    void siren() {  // 사이렌을 울리는 기능
        System.out.println("siren~~~");
    }
}
```

이와 같이 세 클래스, `Car`, `FireEngine`, `Ambulance`가 정의되어 있을 때, 이 세 클래스간의 관계를 그림으로 표현하면 다음과 같다.

![image](https://ifh.cc/g/2lzNQV.png)

`Car`클래스는 `FireEngine`클래스와 `Ambulance`클래스의 조상이다. 그렇다고 해서 `FireEngine`클래스와 `Ambulance`클래스가 형제관계는 아니다. 자바에서는 조상과 자식관계만 존재하기 때문에 `FireEngine`클래스와 `Ambulance`클래스는 서로 아무런 관계가 없다.

따라서 `Car`타입의 참조변수와 `FireEngine`타입의 참조변수 그리고 `Car`타입의 참조변수와 `Ambulance`타입의 참조변수 간에는 서로 형변환이 가능하지만, `FireEngine`타입의 참조변수와 `Ambulance`타입의 참조변수 간에는 서로 형변환이 가능하지 않다.

``` java
FireEngine f;
Ambulance a;
a = (Ambulance)f;   // 에러. 상속관계가 아닌 클래스간의 형변환 불가
f = (FireEngine)a;  // 에러. 상속관계가 아닌 클래스간의 형변환 불가
```

먼저 `Car`타입 참조변수와 `FireEngine`타입 참조변수 간의 형변환을 예로 들어보겠다.

``` java
Car car = null;
FireEngine fe = new FireEngine();
FireEngine fe2 = null;

car = fe;   // car = (Car)fe;에서 형변환 생략됨. 업캐스팅
fe2 = (FireEngine)car;  // 형변환 생략불가. 다운캐스팅
```

참조변수 `car`와 `fe`의 타입이 서로 다르기 때문에, 대입연산(=)이 수행되기 전에 형변환을 수행하여 두 변수간의 타입을 맞춰주어야 한다.

그러나, 자손타입의 참조변수를 조상타입의 참조변수에 할당할 경우 형변환을 생략할 수 있어서 `car = fe;`와 같이 하였다. 원칙적으로는 `car = (Car)fe;`와 같이 해야 한다

반대로 조상타입의 참조변수를 자손타입의 참조변수에 저장할 경우 형변환을 생략할 수 없으므로, `fe2 = (FireEngine)car;`와 같이 명시적으로 형변환을 해주어야 한다.

참고로 형변환을 생략할 수 있는 경우와 생략할 수 없는 경우에 대한 이유를 설명하자면 다음과 같다.

`Car`타입의 참조변수 `c`가 있다고 가정하겠다. 참조변수 `c`가 참조하고 있는 인스턴스는 아마도 `Car`인스턴스이거나 자손인 `FireEngine`인스턴스일 것이다.

**`Car`타입의 참조변수 `c`를 `Car`타입의 조상인 `Object`타입의 참조변수로 형변환하는 것은 참조변수가 다룰 수 있는 멤버의 개수가 실제 인스턴스가 갖고 있는 멤버의 개수보다 적을 것이 분명하므로 문제가 되지 않는다. 그래서 형변환을 생략할 수 있도록 한 것이다.**

하지만, `Car`타입의 참조변수 `c`를 자손인 `FireEngine`타입으로 변환하는 것은 참조변수가 다룰 수 있는 멤버이 개수를 늘리는 것이므로, 실제 인스턴스의 멤버 개수보다 참조변수가 사용할 수 있는 멤버의 개수가 더 많아지므로 문제가 발생할 가능성이 있다.

그래서 자손타입으로의 형변환은 생략할 수 없으며, 형변환을 수행하기 전에 `instanceof`연산자를 사용해서 참조변수가 참조하고 있는 실제 인스턴스의 타입을 확인하는 것이 안전하다

**형변환은 참조변수의 타입을 변환하는 것이지 인스턴스를 변환하는 것은 아니기 때문에 참조변수의 형변환은 인스턴스에 아무런 영향을 미치지 않는다.

단지 참조 변수의 형변환을 통해서, 참조하고 있는 인스턴스에서 사용할 수 있는 멤버의 범위(개수)를 조절하는 것뿐이다.

예제 7-15 / ch7 / CastingTest.java

``` java
class Car {
    String color;
    int door;
    void drive() {  // 운전하는 기능
        System.out.println("drive, Brrr~");
    }
    void stop() {   // 멈추는 기능
        System.out.println("stop!!!");
    }
}

class FireEngine extends Car {  // 소방차
    void water() {  // 물 뿌리는 기능
        System.out.println("water!!!");
    }
}

class Ambulance extends Car {   // 엠뷸런스
    void siren() {  // 사이렌을 울리는 기능
        System.out.println("siren~~~");
    }
}

public class CastingTest1 {
	public static void main(String[] args) {
		Car car = null;
		FireEngine fe = new FireEngine();
		FireEngine fe2 = null;
		
		fe.water();
		car = fe;	// car = (Car)fe;에서 형변환이 생략된 형태다.
//		car.water();	// 컴파일 에러. Car타입의 참조변수로는 water()를 호출할 수 없다.
		fe2 = (FireEngine)car;	// 자손타입 ← 조상타입
		fe2.water();
	}
}
```

```
water!!!
water!!!
```

1. Car car = null;

`Car`타입의 참조변수 `car`를 선언하고 `null`로 초기화한다.

![image](https://ifh.cc/g/ON9AZc.png)

2. FireEngine fe = new FireEngine();

`FireEngine`인스턴스를 생성하고 `FireEngine`타입의 참조변수가 참조하도록 한다.

![image](https://ifh.cc/g/BgZDGK.png)

3. car = fe;    // 조상 타입 ← 자손 타입

참조변수 `fe`가 참조하고 있는 인스턴스를 참조변수 `car`가 참조하도록 한다. `fe`의 값(fe가 참조하고 있는 인스턴스의 주소)이 `car`에 저장된다. 이 때 두 참조변수의 타입이 다르므로 참조변수 `fe`가 형변환되어야 하지만 생략되었다.

이제는 참조변수 `car`를 통해서도 `FireEngine`인스턴스를 사용할 수 있지만, `fe`와는 달리 `car`는 `Car`타입이므로 `Car`클래스의 멤버가 아닌 `water()`는 사용할 수 없다.

![image](https://ifh.cc/g/NgAWW1.png)

4. fe2 = (FireEngine)car;   // 자손 타입 ← 조상 타입

참조변수 `car`가 참조하고 있는 인스턴스를 참조변수 `fe2`가 참조하도록 한다. 이 때 두 참조변수의 타입이 다르므로 참조변수 `car`를 형변환하였다. `car`에는 `FireEngine`인스턴스의 주소가 저장되어 있으므로 `fe2`에도 `FireEngine`인스턴스의 주소가 저장된다.

이제는 참조변수 `fe2`를 통해서도 `FireEngine`인스턴스를 사용할 수 있지만, `car`와는 달리, `fe2`는 `FireEngine`타입이므로 `FireEngine`인스턴스의 모든 멤버들을 사용할 수 있다.

![image](https://ifh.cc/g/BhaqWN.png)

예제 7-16 / ch7 / CastingTest2.java

``` java
public class CastingTest2 {
	public static void main(String[] args) {
		Car car = new Car();
		Car car2 = null;
		FireEngine fe = null;
		
		car.drive();
		fe = (FireEngine)car;	// 8번째 줄, 컴파일은 OK. 실행 시 에러가 발생
		fe.drive();
		car2 = fe;
		car2.drive();
	}
}
```

```
drive, Brrr~
Exception in thread "main" java.lang.ClassCastException: class Car cannot be cast to class FireEngine (Car and FireEngine are in unnamed module of loader 'app')
	at CastingTest2.main(CastingTest2.java:8)
```

이 예제는 컴파일은 성공하지만, 실행 시 에러(ClassCastException)가 발생한다. 에러가 발생한 문장은 'CastingTest2.java'의 8번째 라인인 `fe = (FireEngine)car;`이며, 발생이유는 형변환에 오류가 있기 때문이다. 캐스트 연산자를 이용해서 조상타입의 참조변수를 자손타입의 참조변수로 형변환한 것이기 때문에 문제가 없어 보이지만, 문제는 참조변수 `car`가 참조하고 있는 인스턴스가 `Car`타입의 인스턴스라는데 있다. 전에 배운 것처럼 조상타입의 인스턴스를 자손타입의 참조변수로 참조하는 것은 허용되지 않는다.

위의 예제에서 `Car car = new Car();`를 `Car car = new FireEngine();`와 같이 변경하면, 컴파일할 때 뿐만 아니라 실행할 때도 에러가 발생하지 않을 것이다.

컴파일 시에는 참조변수간의 타입만 체크하기 때문에 실행 시 생성될 인스턴스의 타입에 대해서는 전혀 알지 못한다. 그래서 컴파일 시에는 문제가 없었지만, 실행 시에는 에러가 발생하여 실행이 비정상적으로 종료된 것이다.

> 서로 상속관계에 있는 타입간의 형변환은 양방향으로 자유롭게 수행될 수 있으나, **참조변수가 가리키는 인스턴스의 자손타입으로 형변환은 허용되지 않는다.   그래서 참조변수가 가리키는 인스턴스 타입이 무언인지 확인하는 것이 중요하다.**

</br>

## 5.3 instanceof연산자

참조변수가 참조하고 있는 인스턴스의 실제 타입을 알아보기 위해 `instanceof`연산자를 사용한다. 주로 조건문에 사용되며, `instanceof`의 왼쪽에는 참조변수를 오른쪽에는 타입(클래스명)이 피연산자로 위치한다. 그리고 연산의 결과로 boolean값인 `true`와 `false` 중의 하나를 반환한다.

`instanceof`를 이용한 연산결과로 `true`를 얻었다는 것은 참조변수가 검사한 타입으로 형변환이 가능하다는 것을 뜻한다.

> 값이 null인 참조변수에 대해 instanceof연산을 수행하면 false를 결과로 얻는다.

``` java
void dowork(Car c) {
    if (c instanceof FireEngine) {
        FireEngine fe = (FireEngine)c;
        fe.water();
            ...
    } else if (c instanceof Ambulance) {
        Ambulance a = (Ambulance)c;
        a.siren();
            ...
    }
        ...
}
```

위의 코드는 `Car`타입의 참조변수 `c`를 매개변수로 하는 메소드이다. 이 메소드가 호출될 때, 매개변수로 `Car`클래스 또는 그 자손 클래스의 인스턴스를 넘겨받겠지만 메소드 내에서는 정확히 어떤 인스턴스인지 알 길이 없다. 그래서 `instanceof`연산자를 이용해서 참조변수 `c`가 가리키고 있는 인스턴스의 타입을 체크하고, 적절히 형변환한 다음에 작업을 해야 한다.

조상타입의 참조변수로 자손타입의 인스턴스를 참조할 수 있기 때문에, 참조변수의 타입과 인스턴스의 타입이 항상 일치하지는 않는다. 조상타입의 참조변수로는 실제 인스턴스의 멤버들을 모두 사용할 수 없기 때문에, 실제 인스턴스와 같은 타입의 참조변수로 형변환을 해야만 인스턴스의 모든 멤버들을 사용할 수 있다.

예제 7-17 / ch7 / InstanceofTest.java

``` java
class Car2 {}

class FireEngine2 extends Car2 {}

public class InstanceofTest {
	public static void main(String[] args) {
		FireEngine2 fe = new FireEngine2();
		
		if(fe instanceof FireEngine2) {
			System.out.println("This is a FireEngine instance.");
		}
		
		if(fe instanceof Car2) {
			System.out.println("This is a Car instance.");
		}
		
		if(fe instanceof Object) {
			System.out.println("This is an Object instance.");
		}
		
		System.out.println(fe.getClass().getName());	// 클래스의 이름을 출력
	}
}	// class
```

```
This is a FireEngine instance.
This is a Car instance.
This is an Object instance.
FireEngine2
```

생성된 인스턴스는 `FireEngine`타입인데도, `Object`타입과 `Car`타입의 `instanceof`연산에서도 `true`를 결과로 얻었다. 그 이유는 `FireEngine`클래스는 `Object`클래스와 `Car`클래스의 자손 클래스이므로 조상의 멤버들을 상속받았기 때문에, `FireEngine`인스턴스는 `Object`인스턴스와 `Car`인스턴스를 포함하고 있는 셈이기 때문이다.

요약하면, 실제 인스턴스와 같은 타입의 `instanceof`연산 이외에 조상타입의 `instanceof`연산에도 `true`를 결과로 얻으며, `instanceof`연산의 결과가 `true`라는 것은 검사한 타입으로의 형변환을 해도 아무런 문제가 없다는 뜻이다.

`참조변수.getClass().getName()`은 참조변수가 가리키고 있는 인스턴스의 클래스 이름을 문자열(String)로 반환한다.

> 어떤 타입에 대한 instanceof연산의 결과가 true라는 것은 검사한 타입으로 형변환이 가능하다는 것을 뜻한다.

</br>

## 5.4 참조변수와 인스턴스의 연결

조상 타입의 참조변수와 자손 타입의 참조변수의 차이점이 사용할 수 있는 멤버의 개수이다.

조상 클래스에 선언된 멤버변수와 같은 이름의 인스턴스변수를 자손 클래스에 중복으로 정의했을 때, 조상타입의 참조변수로 자손 인스턴스를 참조하는 경우와 자손타입의 참조변수로 자손 인스턴스를 참조하는 경우는 서로 다른 결과를 얻는다.

메소드의 경우 조상 클래스의 메소드를 자손의 클래스에서 오버라이딩한 경우에도 참조변수의 타입에 관계없이 항상 실제 인스턴스의 메소드(오버라이딩된 메소드)가 호출되지만, **멤버변수의 경우 참조변수의 타입에 따라 달라진다.**

> static메소드는 static변수처럼 참조변수의 타입에 영향을 받는다. 참조변수의 타입에 영향을 받지 않는 것은 인스턴스메소드뿐이다. 그래서 static메소드는 반드시 참조변수가 아닌 '클래스이름.메소드()'로 호출해야 한다.

결론부터 말하자면, 멤버변수가 조상 클래스와 자손 클래스에 중복으로 정의된 경우, 조상타입의 참조변수를 사용했을 때는 조상 클래스에 선언된 멤버변수가 사용되고, 자손타입의 참조변수를 사용했을 때는 자손 클래스에 선언된 멤버변수가 사용된다.

하지만 중복 정의되지 않은 경우, 조상타입의 참조변수를 사용했을 때와 자손타입의 참조변수를 사용했을 때의 차이는 없다. 중복된 경우는 참조변수의 타입에 따라 달라지지만, 중복되지 않은 경우 하나뿐이므로 선택의 여지가 없기 때문이다.

예제 7-18 / ch7 / BindingTest.java

``` java
class Parent3 {
	int x = 100;
	
	void method() {
		System.out.println("Parent Method");
	}
}

class Child3 extends Parent3 {
	int x = 200;
	
	void method() {
		System.out.println("Child Method");
	}
}

public class BindingTest {
	public static void main(String[] args) {
		Parent3 p = new Child3();
		Child3 c = new Child3();
		
		System.out.println("p.x = " + p.x);
		p.method();
		System.out.println("c.x = " + c.x);
		c.method();
	}
}
```

```
p.x = 100
Child Method
c.x = 200
Child Method
```

타입은 다르지만, 참조변수 `p`와 `c` 모두 `Child3`인스턴스를 참조하고 있다. 그리고 `Parent3`클래스와 `Child3`클래스는 서로 같은 멤버들을 정의하고 있다.

이 때 조상타입의 참조변수 `p`로 `Child3`인스턴스의 멤버들을 사용하는 것과 자손타입의 참조변수 `c`로 `Child3`인스턴스의 멤버들을 사용하는 것의 차이를 알 수 있다.

메소드인 `method()`의 경우 참조변수의 타입에 관계없이 항상 실제 인스턴스의 타입인 `Child3`클래스에 정의된 메소드가 호출되지만, 인스턴스변수인 `x`는 참조변수의 타입에 따라서 달라진다.

예제 7-19 / ch7 / BindingTest2.java

``` java
class Parent4 {
	int x = 100;
	
	void method() {
		System.out.println("Parent Method");
	}
}

class Child4 extends Parent4 { }

public class BindingTest2 {
	public static void main(String[] args) {
		Parent4 p = new Child4();
		Child4 c = new Child4();
		
		System.out.println("p.x = " + p.x);
		p.method();
		System.out.println("c.x = " + c.x);
		c.method();
	}
}
```

```
p.x = 100
Parent Method
c.x = 100
Parent Method
```

이전의 예제와는 달리 `Child4`클래스에는 아무런 멤버도 정의되어 있지 않고 단순히 조상으로부터 멤버들을 상속받는다. 그렇기 때문에 참조변수의 타입에 관계없이 조상의 멤버들을 사용하게 된다.

이처럼 자손 클래스에서 조상 클래스의 멤버를 중복으로 정의하지 않았을 때는 참조변수의 타입에 따른 변화는 없다. 어느 클래스의 멤버가 호출되어야 할지, 즉 조상의 멤버가 호출되어야할 지, 자손의 멤버가 호출되어야 할지에 대해 선택의 여지가 없기 때문이다. 참조변수의 타입에 따라 결과가 달라지는 경우는 조상 클래스의 멤버변수의 같은 이름의 멤버변수를 자손 클래스에 중복해서 정의한 경우뿐이다.

예제 7-20 / ch7 / BindingTest3.java

``` java
class Parent5 {
	int x = 100;
	
	void method() {
		System.out.println("Parent Method");
	}
}

class Child5 extends Parent5 {
	int x = 200;
	
	void method() {
		System.out.println("x = " + x);	// this.x와 같다.
		System.out.println("super.x = " + super.x);
		System.out.println("this.x = " + this.x);
	}
}

public class BindingTest3 {
	public static void main(String[] args) {
		Parent5 p = new Child5();
		Child5 c = new Child5();
		
		System.out.println("p.x = " + p.x);
		p.method();
		System.out.println();
		System.out.println("c.x = " + c.x);
		c.method();
	}
}
```

```
p.x = 100
x = 200
super.x = 100
this.x = 200

c.x = 200
x = 200
super.x = 100
this.x = 200
```

자손 클래스의 `Child5`에 선언되 인스턴스변수 `x`와 조상 클래스 `Parent5`로부터 상속받은 인스턴스변수 `x`를 구분하는데 참조변수 `super`와 `this`가 사용된다. 자손인 `Child5`클래스에서의 `super.x`는 조상 클래스인 `Parent5`에 선언된 인스턴스변수 `x`를 뜻하며, `this.x` 또는 `x`는 `Child5`클래스의 인스턴스변수 `x`를 뜻한다. 그래서 위 결과에서 `x`와 `this.x`의 값은 같다.

</br>

## 5.5 매개변수의 다형성

참조변수와 다형적인 특성은 메소드의 매개변수에도 적용된다. 아래와 같이 `Product`, `Tv`, `Computer`, `Audio`, `Buyer`클래스가 정의되어 있다.

``` java
class Product {
	int price;	// 제품의 가격
	int bounsPoint;	// 제품구매 시 제공하는 보너스
}
class Tv extends Product {}
class Computer extends Product {}
class Audio extends Product {}

class Buyer {   // 고객, 물건을 사는 사람
    int money;  // 소유금액
    int bonusPoint; // 보너스점수
}
```

`Product`클래스는 `Tv`, `Audio`, `Computer`클래스의 조상이며, `Buyer`클래스는 제품(Product)을 구입하는 사람을 클래스로 표현한 것이다.

`Buyer`클래스에 물건을 구입하는 기능의 메소드를 추가해보겠다. 구입할 대상이 필요하므로 매개변수로 구입할 제품을 넘겨받아야 한다. `Tv`를 살 수 있도록 매개변수를 `Tv`타입으로 하였다.

``` java
void buy(Tv t) {
    // Buyer가 가진 돈(money)에서 제품의 가격(t.price)만큼 뺀다.
    money = money - t.price;

    // Buyer의 보너스점수 (bonusPoint)에 제품의 보너스점수(t.bonusPoint)를 더한다.
    bonusPoint = bonusPoint + t.bonousPoint;
}
```

buy(Tv t)는 제품을 구입하면 제품을 구입한 사람이 가진 돈에서 제품의 가격을 빼고, 보너스점수는 추가하는 작업을 하도록 작성되었다. 그런데 `buy(Tv t)`로는 `Tv`밖에 살 수 없기 때문에 아래와 같이 다른 제품들도 구입할 수 있는 메소드가 추가로 필요하다.

``` java
void buy(Computer c) {
    money = money - c.price;
    bounusPoint = bonusPoint + c.bonusPoint;
}

void buy(Audio a) {
    money = money - a.price;
    bonusPoint = bonusPoint + a.bonusPoint;
}
```

이렇게 되면, 제품의 종류가 늘어날 때마다 `Buyer`클래스에는 새로운 `buy`메소드를 추가해주어야 할 것이다.

그러나 메소드의 매개변수에 다형성을 적용하면 아래와 같이 하나의 메소드로 간단히 처리할 수 있다.

``` java
void buy(Product p) {
    money = money - p.price;
    bounusPoint = bonusPoint + p.bonusPoint;
}
```

매개변수가 `Product`타입의 참조변수라는 것은, 메소드의 매개변수로 `Product`클래스의 자손타입의 참조변수면 어느 것이나 매개변수로 받아들일 수 있다는 뜻이다.

그리고 `Product`클래스에 `price`와 `bonusPoint`가 선언되어 있기 때문에 참조변수 `p`로 인스턴스의 `price`와 `bonusPoint`를 사용할 수 있게에 이와 같이 할 수 있다.

앞으로 다른 제품 클래스를 추가할 때 `Product`클래스를 상속받기만 하면, `buy(Product p)`메소드의 매개변수로 받아들여질 수 있다.

``` java
Buyer b = new Buyer();
Tv t = new Tv();
Computer c = new Computer();
b.buy(t);
b.buy(c);
```

`Tv`클래스와 `Computer`클래스는 `Product`클래스의 자손이므로 위의 코드와 같이 `buy(Product p)`메소드에 매개변수로 `Tv`인스터스와 `Computer`인스턴스를 제공하는 것이 가능하다.

예제 7-21 / ch7 / PolyArgumentTest.java

``` java
class Product {
	int price;	// 제품의 가격
	int bounsPoint;	// 제품구매 시 제공하는 보너스
	
	Product(int price) {
		this.price = price;
		bounsPoint = (int)(price/10.0);	// 보너스점수는 제품가격의 10%
	}
}

class Tv1 extends Product {
	Tv1() {
		// 조상클래스의 생성자 Product(int price)를 호출한다.
		super(100);	// Tv의 가격을 100만원으로 한다.
	}
	
	// Object클래스의 toString()을 오버라이딩한다.
	public String toString() { return "Tv"; }
}

class Computer extends Product {
	Computer() { super(200); }
	
	public String toString() { return "Computer"; }
}

class Buyer {	// 고객, 물건을 사는 사람
	int money = 1000;	// 소유금액
	int bonusPoint = 0;	// 보너스 점수
	
	void buy(Product p) {
		if(money < p.price) {
			System.out.println("잔액이 부족하여 물건을 살 수 없습니다.");
			return;
		}
		
		money -= p.price;	// 가진 돈에서 구입한 제품의 가격을 뺀다.
		bonusPoint += p.bounsPoint;	// 제품 보너스 점수를 추가한다.
		System.out.println(p + "을/를 구입하셨습니다.");
	}
}

public class Ex7_8 {
	public static void main(String[] args) {
		Buyer b = new Buyer();
		
		b.buy(new Tv1());	// buy(Product p)
		b.buy(new Computer());	// buy(Product p)
		
		System.out.println("현재 남은 돈은 " + b.money + "만원입니다.");
		System.out.println("현재 보너스 점수는 " + b.bonusPoint + "점입니다.");
	}
}
```

```
Tv을/를 구입하셨습니다.
Computer을/를 구입하셨습니다.
현재 남은 돈은 700만원입니다.
현재 보너스 점수는 30점입니다.
```

고객(Buyer)이 `buy(Product p)`메소드를 이용해서 `Tv`와 `Computer`를 구입하고, 고객의 잔고와 보너스점수를 출력하는 예제이다.

매개변수의 다형성의 또 다른 예로 `PrintStream`클래스에 정의되어있는 `print(Object obj)`메소드를 살펴보겠다. `print(Object obj)`는 매개변수로 `Object`타입의 변수가 선언되어 있는데 `Object`는 모든 클래스의 조상이므로 이 메소드의 매개변수로 어떤 타입의 인스턴스도 가능하므로, 이 하나의 메소드로 모든 타입의 인스턴스를 처리할 수 있는 것이다.

이 메소드는 매개변수에 `toString()`을 호출하여 문자열을 얻어서 출력한다. 실제 코드는 아래와 같다.

``` java
public void print(Object obj) {
    write(String.valueOf(obj)); // valueof()가 반환한 문자열을 출력한다.
}

public static String valueOf(Object obj) {
    return (obj == null) ? "null" : obj.toString(); // 문자열을 반환한다.
}
```

</br>

## 5.6 여러 종류의 객체를 배열로 다루기

``` java
Product p1 = new Tv();
Product p2 = new new Computer();
Product p3 = new Audio();
```

위의 코드를 `Product`타입의 참조변수 배열로 처리하면 아래와 같다.

``` java
Product p[] = new Product[3];
p[0] = new Tv();
p[1] = new Computer();
p[2] = new Audio();
```

이처럼 조상타입의 참조변수 배열을 사용하면, 공통의 조상을 가진 서로 다른 종류의 객체를 배열로 묶어서 다룰 수 있다. 또는 묶어서 다루고싶은 객체들의 상속관계를 따져서 가장 가까운 공통조상 클래스 타입의 참조변수 배열을 생성해서 객체들을 저장하면 된다.

이러한 특징을 이용해서 예제 7-21의 `Buyer`클래스에 구입한 제품을 저장하기 위한 `Product`배열을 추가해보도록 하겠다.

``` java
class Buyer {
    int money = 1000;
    int bounusPoint = 0;
    Product[] item = new Product[10];   // 구입한 제품을 저장하기 위한 배열
    int i = 0;  // Product배열 item에 사용될 index

    void buy(Product p) {
        if(money < p.price) {
            System.out.println("잔액이 부족하여 물건을 살수 없습니다.");
            return;
        }

        money -= p.price;   // 가진 돈에서 제품가격을 뺀다.
        bounsPoint += p.bonusPoint; // 제품의 보너스포인트를 더한다.
        item[i++] = p;  // 제품을 Product[] item에 저장한다
        System.out.println(p + "을/를 구입하셨습니다.");
    }
}
```

구입한 제품을 담기 위해 `Buyer`클래스에 `Product`배열인 `item`을 추가해주었다. 그리고 `buy`메소드에 `item[i++] = p;`문장을 추가함으로써 물건을 구입하면, 배열 `item`에 저장되도록 했다.

이렇게 함으로써, 모든 제품클래스의 조상인 `Product`클래스 타입의 배열을 사용함으로써 구입한 제품을 하나의 배열로 간단하게 다룰 수 있게 된다.

예제 7-22 / ch7 / PolyArgumentTest2.java

``` java
class Product2 {
    int price;  // 제품의 가격
    int bonusPoint; // 제품구매 시 제공하는 보너스점수

    Product2(int price) {
        this.price = price;
        bonusPoint = (int)(price / 10.0);
    }

    Product2() { }   // 기본 생성자
}

class Tv2 extends Product2 {
    Tv2() { super(100); }    // 조상 클래스의 생성자 Product(int price)를 호출한다.

    public String toString() { return "Tv"; }
}

class Computer2 extends Product2 {
    Computer2() { super(200); }
    public String toString() { return "Computer"; }
}

class Audio2 extends Product2 {
    Audio2() { super(50); }
    public String toString() { return "Audio"; }
}

class Buyer2 {   // 고객, 물건을 사는 사람
    int money = 1000;   // 소유금액
    int bonusPoint = 0; // 보너스점수
    Product2[] item = new Product2[10];   // 구입한 제품을 저장하기 위한 배열
    int i = 0;  // Product배열에 사용될 카운터

    void buy(Product2 p) {
        if(money < p.price) {
            System.out.println("잔액이 부족하여 물건을 살 수 없습니다.");
            return;
        }

        money -= p.price;   // 가진 돈에서 구입한 제품의 가격을 뺀다.
        bonusPoint += p.bonusPoint; // 제품의 보너스 점수를 추가한다.
        item[i++] = p;  // 제품을 Product[] item에 저장한다.
        System.out.println(p + "을/를 구입하셨습니다.");
    }

    void summary() {    // 구입한 물품에 대한 정보를 요약해서 보여 준다
        int sum = 0;    // 구입한 물품의 가격합계
        String itemList = "";   // 구입한 물품목록

        // 반복문을 이용해서 구입한 물품의 총 가격과 목록을 만든다.
        for(int i = 0; i < item.length; i++) {
            if(item[i] == null) break;
            sum += item[i].price;
            itemList += item[i] + ", ";
        }
        System.out.println("구입하신 물품의 총금액은 " + sum + "만원입니다.");
        System.out.println("구입하신 제품은 " + itemList + "입니다.");
    }
}

public class PolyArgumentTest2 {
	public static void main(String[] args) {
		Buyer2 b = new Buyer2();
		
		b.buy(new Tv2());
		b.buy(new Computer2());
		b.buy(new Audio2());
		b.summary();
	}
}
```

```
Tv을/를 구입하셨습니다.
Computer을/를 구입하셨습니다.
Audio을/를 구입하셨습니다.
구입하신 물품의 총금액은 350만원입니다.
구입하신 제품은 Tv, Computer, Audio, 입니다.
```

위 예제에서 `Product`배열로 구입한 제품들을 저장할 수 있도록 했지만, 배열의 크기를 10으로 했기 때문에 11개 이상의 제품을 구입할 수 없는 것이 문제다. 그렇다고 해서 배열의 크기를 무조건 크게 설정할 수만도 없는 일이다.

이런 경우, `Vector`클래스를 사용하면 된다. `Vector`클래스는 내부적으로 `Object`타입의 배열을 가지고 있어서, 이 배열에 객체를 추가하거나 제거할 수 있게 작성되어 있다.

그리고 배열의 크기를 알아서 관리해주기 때문에 저장할 인스턴스의 개수에 신경 쓰지 않아도 된다.

``` java
public class Vector extends AbstractList implements List, Cloneable, java.io.Serializable {
    protected Object elementData[];
        ...
}
```

`Vector`클래스는 이름 때문에 클래스의 기능을 오해할 수 있는데, 단지 동적으로 크기가 관리되는 객체배열일 뿐이다.

![image](https://ifh.cc/g/PJGjR0.png)

예제 7-23 / ch7 / PolyArgumentTest3.java

``` java
import java.util.*;	// Vector클래스를 사용하기 위해서 추가

class Product3 {
	int price;	// 제품의 가격
	int bonusPoint;	// 제품구매 시 제공하는 보너스점수
	
	Product3(int price) {
		this.price = price;
		bonusPoint = (int)(price / 10.0);
	}
	
	Product3() {
		price = 0;
		bonusPoint = 0;
	}
}

class Tv3 extends Product3 {
	Tv3() { super(100); }
	public String toString() { return "Tv"; }
}

class Computer3 extends Product3 {
	Computer3() { super(200); }
	public String toString() { return "Computer"; }
}

class Audio3 extends Product3 {
	Audio3() { super(50); }
	public String toString() { return "Audio"; }
}

class Buyer3 {	// 고객, 물건을 사는 사람
	int money = 1000;	// 소유금액
	int bonusPoint = 0;	// 보너스점수
	Vector item = new Vector();	// 구입한 제품을 저장하는데 사용할 Vector객체
	
	void buy(Product3 p) {
		if(money < p.price) {
			System.out.println("잔액이 부족하여 물건을 살수 없습니다.");
			return;
		}
		money -= p.price;	// 가진 돈에서 구입한 제품의 가격을 뺀다.
		bonusPoint += p.bonusPoint;	// 제품의 보너스 점수를 추가한다.
		item.add(p);	// 구입한 제품을 Vector에 저장한다.
		System.out.println(p + "을/를 구입하셨습니다.");
	}
	
	void refund(Product3 p) {	// 구입한 제품을 환불한다.
		if(item.remove(p) ) {	// 제품을 Vector에서 제거한다.
			money += p.price;
			bonusPoint -= p.bonusPoint;
			System.out.println(p + "을/를 반품하셨습니다.");
		} else {	// 제거에 실패한 경우
			System.out.println("구입하신 제품 중 해당 제품이 없습니다.");
		}
	}
	
	void summary() {	// 구매한 물품에 대한 정보를 요약해서 보여준다.
		int sum = 0;	// 구입한 물품의 가격합계
		String itemList = "";	// 구입한 물품목록
		
		if(item.isEmpty()) {	// Vector가 비어있는지 확인한다.
			System.out.println("구입하신 제품이 없습니다.");
			return;
		}
		
		// 반복문을 이용해서 구입한 물품의 총 가격과 목록을 만든다.
		for(int i = 0; i < item.size(); i++) {
			Product3 p = (Product3)item.get(i);	// Vector의 i번째에 있는 객체를 얻어온다.
			sum += p.price;
			itemList += (i == 0) ? "" + p : ", " + p;
		}
		System.out.println("구입하신 물품의 총금액은 " + sum + "만원입니다.");
		System.out.println("구입하신 제품은 " + itemList + "입니다.");
	}
}
public class PolyArgumentTest3 {
	public static void main(String[] args) {
		Buyer3 b = new Buyer3();
		Tv3 tv = new Tv3();
		Computer3 com = new Computer3();
		Audio3 audio = new Audio3();
		
		b.buy(tv);
		b.buy(com);
		b.buy(audio);
		b.summary();
		System.out.println();
		b.refund(com);
		b.summary();
	}
}
```

```
Tv을/를 구입하셨습니다.
Computer을/를 구입하셨습니다.
Audio을/를 구입하셨습니다.
구입하신 물품의 총금액은 350만원입니다.
구입하신 제품은 Tv, Computer, Audio입니다.

Computer을/를 반품하셨습니다.
구입하신 물품의 총금액은 150만원입니다.
구입하신 제품은 Tv, Audio입니다.
```

구입한 물건을 다시 반환할 수 있도록 `refund(Product3 p)`를 추가하였다. 이 메소드가 호출되면, 구입물품이 저장되어 있는 `item`에서 해당제품을 제거한다.

> 문자열과 참조변수의 덧셈(결합연산)은 참조변수에 toString()을 호출해서 문자열을 얻어 결합한다. 그래서 위 예제에 나오는 "" +p는 "" + p.toString()이 되고, 만일 p.toString()의 결과가 "Audio"라면 ""+"Audio"가 되어 결국 "Audio"가 된다.