Chapter 7. 객체지향 프로그래밍2

# 4. 제어자(modifier)

</br>

## 4.1 제어자란?

제어자(modifier)는 클래스, 변수 또는 메소드의 선언부에 함께 사용되어 부가적인 의미를 부여한다. 제어자의 종류는 크게 접근 제어자와 그 외의 제어자로 나눌 수 있다.

> **접근 제어자** public, protected, default, private   
> **그 외** static, abstract, native, transient, synchronized, volatile, strictfp

제어자는 클래스나 멤버변수와 메소드에 주로 사용되며, 하나의 대상에 대해서 여러 제어자를 조합하여 사용하는 것이 가능하다.

단, 접근 제어자는 한 번에 네 가지 중 하나만 선택해서 사용할 수 있다.

> 제어자들 간의 순서는 관계없지만 주로 접근 제어자를 제일 왼쪽에 놓는 경향이 있다.

</br>

## 4.2 static - 클래스의, 공통적인

`static`은 '클래스의' 또는 '공통적인'의 의미를 가지고 있다. 인스턴스변수는 하나의 클래스로부터 생성되었더라도 각기 다른 값을 유지하지만, 클래스변수(static멤버변수)는 인스턴스에 관계없이 같은 값을 갖는다. 그 이유는 하나의 변수를 모든 인스턴스가 공유하기 때문이다.

`static`이 붙은 멤버변수와 메소드, 그리고 초기화 블럭은 인스턴스가 아닌 클래스에 관계된 것이기 때문에 인스턴스를 생성하지 않고도 사용할 수 있다.

> static이 사용될 수 있는 곳 - 멤버변수, 메소드, 초기화 블럭

![image](https://ifh.cc/g/Z1BJbW.png)

인스턴스 멤버를 사용하지 않는 메소드는 `static`을 붙여서 static메소드로 선언하는 것을 고려해야 한다. 가능하다면 static메소드로 하는 것이 인스턴스를 생성하지 않고도 호출이 가능해서 더 편리하고 속도도 더 빠르다.

> static초기화 블럭은 클래스가 메모리에 로드될 때 단 한 번만 수행되며, 주로 클래스변수(static변수)를 초기화하는 데 주로 사용된다.

``` java
class StaticTest {
    static int width = 200; // 클래스 변수(static변수)
    static int height = 120;    // 클래스 변수(static변수)

    static {    // 클래스 초기화 블럭
        // static변수의 복잡한 초기화 수행
    }

    static int max(int a, int b) {  // 클래스 메소드(static메소드)
        return a > b ? a : b;
    }
}
```

</br>

## 4.3 final - 마지막의, 변경될 수 없는

`final`은 '마지막의' 또는 '변경될 수 없는'의 의미를 가지고 있으며 거의 모든 대상에 사용될 수 있다.

변수에 사용되면 값을 변경할 수 없는 상수가 되며, 메소드에 사용되면 오버라이딩을 할 수 없게 되고 클래스에 사용되면 자신을 확장하는 자손클래스를 정의하지 못하게 된다.

> final이 사용될 수 있는 곳 - 클래스, 메소드, 멤버변수, 지역변수

![image](https://ifh.cc/g/7oSGkp.png)

> 대표적인 final클래스로는 String과 Math가 있다.

``` java
final class FinalTest { // 조상이 될 수 없는 클래스
    final int MAx_SIZE = 10;    // 값을 변경할 수 없는 멤버변수(상수)

    final void getMaxSize() {   // 오버라이딩을 할 수 없는 메소드(변경불가)
        final int LV = MAX_SIZE;    // 값을 변경할 수 없는 지역변수(상수)
        return MAX_SIZE;
    }
}
```

### 생성자를 이용한 final멤버 변수의 초기화

`final`이 붙은 변수는 상수이므로 일반적으로 선언과 초기화를 동시에 하지만, 인스턴스변수의 경우 생성자에서 초기화 되도록 할 수 있다.

클래스 내에 매개변수를 갖는 생성자를 선언하여, 인스턴스를 생성할 때 `final`이 붙은 멤버변수를 초기화하는데 필요한 값을 생성자의 매개변수로부터 제공받는 것이다.

이 기능을 활용하면 각 인스턴스마다 `final`이 붙은 멤버변수가 다른 값을 갖도록 하는 것이 가능하다.

예를 들어 카드이 경우, 각 카드마다 다른 종류와 숫자를 갖지만, 일단 카드가 생성되면 카드의 값이 변경되어서는 안된다. 52장의 카드 중에서 하나만 잘못 바꿔도 같은 카드가 2장이 되는 일이 생기기 때문이다. 그래서 카드의 값을 바꾸기 보다는 카드의 순서를 바꾸는 쪽이 더 안전한 방법이다.

예제 7-12 / ch7 / FinalCardTest.java

``` java
class Card2 {
	final int NUMBER;	// 상수지만 선언과 함께 초기화하지 않고
	final String KIND;	// 생성자에서 단 한 번만 초기화 할 수 있다.
	static int width = 100;
	static int height = 250;
	
	Card2(String kind, int num) {	// 매개변수로 넘겨받은 값으로 KIND와 NUMBER을 초기화한다
		KIND = kind;
		NUMBER = num;
	}
	
	Card2() {
		this("HEART", 1);
	}
	
	public String toString() {
		return KIND + " " + NUMBER;
	}
}

public class FinalCardTest {
	public static void main(String[] args) {
		Card2 c = new Card2("HEART", 10);
//		c.NUMBER = 5;	// 에러. cannot assign a value to fianl variable NUMBER
		System.out.println(c.KIND);
		System.out.println(c.NUMBER);
		System.out.println(c);	// System.out.println(c.toString());
	}
}
```

```
HEART
10
HEART 10
```

</br>

## 4.4 abstract - 추상의, 미완성의

`abstract`는 '미완성'의 의미를 가지고 있다. 메소드의 선언부만 작성하고 실제 수행내용은 구현하지 않은 추상 메소드를 선언하는데 사용된다.

그리고 클래스에 사용되어 클래스 내에 추상메소드가 존재한다는 것을 쉽게 알 수 있게 한다.

> abstract가 사용될 수 있는 곳 - 클래스, 메소드

![image](https://ifh.cc/g/CrN9C3.png)

추상 클래스는 아직 완성되지 않은 메소드가 존재하는 '미완성 설계도'이므로 인스턴스를 생성할 수 없다.

``` java
abstract class AbstractTest {   // 추상 클래스(추상 메소드를 포함한 클래스)
    abstract void move();   // 추상 메소드(구현부가 없는 메소드)
}
```

꽤 드물지만 추상 메소드가 없는 클래스, 즉 완성된 클래스도 `abstract`를 붙여서 추상 클래스로 만드는 경우도 있다. 예를 들어, `java.awt.event.WindowAdapter`는 아래와 같이 아무런 내용이 없는 메소드들만 정의되어 있다. 이런 클래스는 인스턴스를 생성해봐야 할 수 있는 것이 아무것도 없다. 그래서 인스턴스를 생성하지 못하게 클래스 앞에 제어자 `abastract`를 붙여 놓은 것이다.

``` java
public abstracrt class WindowAdapter implements WindowListener, WindowStateListener, WindowFocusListener {
    public void windowOpened(WindowEvent e) {}
    public void windowClosing(WindowEvent e) {}
    public void windowClosed(WindowEvent e) {}
    public void windowIconified(WindowEvent e) {}
        ...
}
```

이 클래스 자체로는 쓸모가 없지만, 다른 클래스가 이 클래스를 상속받아서 일부의 원하는 메소드만 오버라이딩해도 된다는 장점이 있다. 만일 이 클래스가 없다면 아무런 내용도 없는 메소드를 잔뜩 오버라이딩해야 한다.

</br>

## 4.5 접근 제어자(access modifier)

접근 제어자는 멤버 또는 클래스에 사용되어, 해당하는 멤버 또는 클래스를 외부에서 접근하지 못하도록 제한하는 역할을 한다.

접근 제어자가 `default`임을 알리기 위해 실제로 `default`를 붙이지 않는다. 클래스나 멤버변수, 메소드, 생성자에 접근 제어자가 지정되어 있지 않다면, 접근 제어자가 `default`임을 뜻한다.

> **접근 제어자가 사용될 수 있는 곳 - 클래스, 멤버변수, 메소드, 생성자**   
> **private** 같은 클래스 내에서만 접근이 가능하다.   
> **default** 같은 패키지 내에서만 접근이 가능하다.   
> **protected** 같은 패키지 내에서, 그리고 다른 패키지의 자손클래스에서 접근이 가능하다.   
> **public** 접근 제한이 전혀 없다.

![image](https://ifh.cc/g/PzvFA2.png)

접근 범위가 넓은 쪽에서 좁은 쪽의 순으로 왼쪽부터 나열하면 다음과 같다.

> public > protected > (default) > private

`public`은 접근 제한이 전혀 없는 것익, `private`은 같은 클래스 내에서만 사용하도록 제한하는 가장 높은 제한이다. 그리고 `default`는 같은 패키지내의 클래스에서만 접근이 가능하도록 하는 것이다.

마지막으로 `protected`는 패키지에 관계없이 상속관계에 있는 자손 클래스에서 접근할 수 있도록 하는 것이 제한목적이지만, 같은 패키지 내에서도 접근이 가능하다. 그래서 `protected`가 `default`보다 접근범위가 더 넓다.

> 접근 제어자가 default라는 것은 아무런 접근 제어자도 붙이지 않는 것을 의미한다.

![image](https://ifh.cc/g/Fo2cJ0.png)

### 접근 제어자를 이용한 캡슐화

클래스나 멤버, 주로 멤버에 접근 제어자를 사용하는 이유는 클래스의 내부에 선언된 데이터를 보호하기 위해서이다.

데이터가 유효한 값을 유지하도록, 또는 비밀번호와 같은 데이터를 외부에서 함부로 변경하지 못하도록 하기 위해서는 외부로부터의 접근을 제한하는 것이 필요하다.

이것을 데이터 감추기(data hiding)라고 하며, 객체지향개념의 캡슐화(encapsulation)에 해당하는 내용이다.

또 다른 이유는 클래스 내에서만 사용되는, 내부 작업을 위해 임시로 사용되는 멤버변수나 부분작업을 처리하기 위한 메소드 등의 멤버들을 클래스 내부에 감추기 위해서이다.

외부에서 접근할 필요가 없는 멤버들을 `private`으로 지정하여 외부에 노출시키지 않음으로써 복잡성을 줄일 수 있다. 이것 역시 캡슐화에 해당한다.

> 접근 제어자를 사용하는 이유
> - 외부로부터 데이터를 보호하기 위해서
> - 외부에는 불필요한, 내부적으로만 사용되는, 부분을 감추기 위해서

만일 메소드 하나를 변경해야 한다고 가정했을 때, 이 메소드의 접근 제어자가 `public`이라면, 메소드를 변경한 후에 오류가 없는지 테스트해야 하는 범위가 넓다. 그러나 접근 제어자가 `default`라면 패키지 내부만 확인해 보면 되고, `private`이라면 클래스 하나만 살펴보면 된다.

시간을 표시하기 위한 클래스 `Time`이 다음과 같이 정의되어 있을 때,

``` java
public class Time {
    public int hour;
    public int minute;
    public int second;
}
```

이 클래스의 인스턴스를 생성한 다음, 멤버변수에 직접 접근하여 값을 변경할 수 있다.

``` java
Time t = new Time();
t.hour = 25;
```

멤버변수 `hour`은 0보다는 같거나 크고 24보다는 작은 범위의 값을 가져야 하지만 위의 코드에서처럼 잘못된 값을 지정한다고 해도 이것을 막을 방법이 없다.

이런 경우 멤버변수를 `private`이나 `protected`로 제한하고 멤버변수의 값을 읽고 변경할 수 있는 `public`메소드를 제공함으로써 간접적으로 멤버변수의 값을 다룰 수 있도록 하는 것이 바람직하다.

``` java
public class Time {
    // 접근 제어자를 private으로 하여 외부에서 직접 접근하지 못하도록 한다.
    private int hour;
    private int minute;
    private int second;

    public int getHour() { return hour; }
    public void setHour(int hour) {
        if(hour < 0 || hour > 23) return;
        this.hour = hour;
    }
    public int getMinute() { return minute; }
    public void setMinute(int minute) {
        if(minute < 0 || minute > 59) return;
        this.minute = minute;
    }
    public int getSecond() { return second; }
    public void setSecond(int second) {
        if(second < 0 || second > 59) return;
        this.second = second;
    }
}
```

`get`으로 시작하는 메소드는 단순히 멤버변수의 값을 반환하는 일을 하고, `set`으로 시작하는 메소드는 매개변수에 지정된 값을 검사하여 조건에 맞는 값일 때만 멤버변수의 값을 변경하도록 작성되어 있다.

만일 상속을 통해 확장될 것이 예상되는 클래스라면 멤버에 접근 제한을 주되 자손클래스에서 접근하는 것이 가능하도록 하기 위해 `private`대신 `protected`를 사용한다. `private`이 붙은 멤버는 자손 클래스에서도 접근이 불가능하기 때문이다.

보통 멤버변수의 값을 읽는 메소드의 이름을 'get멤버변수이름'으로 하고, 멤버변수의 값을 변경하는 메소드의 이름을 'set멤버변수이름'으로 한다. 그리고 `get`으로 시작하는 메소드를 '겟터(getter)', `set`으로 시작하는 메소드를 '셋터(setter)'라고 부른다.

예제 7-13 / ch7 / TimeTest.java

``` java
class Time {
    private int hour, minute, second;
    
    Time(int hour, int minute, int second) {
    	setHour(hour);
    	setMinute(minute);
    	setSecond(second);
    }

    public int getHour() { return hour; }
    public void setHour(int hour) {
        if(hour < 0 || hour > 23) return;
        this.hour = hour;
    }
    public int getMinute() { return minute; }
    public void setMinute(int minute) {
        if(minute < 0 || minute > 59) return;
        this.minute = minute;
    }
    public int getSecond() { return second; }
    public void setSecond(int second) {
        if(second < 0 || second > 59) return;
        this.second = second;
    }
    public String toString() {
    	return hour + ":" + minute + ":" + second;
    }
}

public class TimeTest {
	public static void main(String[] args) {
		Time t = new Time(12, 35, 30);
		System.out.println(t);
//		t.hour = 13;
		t.setHour(t.getHour() + 1);	// 현재시간보다 1시간 후로 변경한다.
		System.out.println(t);	// System.out.println(t.toString());과 같다.
	}
}
```

```
12:35:30
13:35:30
```

`Time`클래스의 모든 멤버변수의 접근 제어자를 `private`로 하고, 이 들을 다루기 위한 public메소드를 추가했다. 그래서 't.hour = 13;'과 같이 멤버변수로의 직접적인 접근은 허가되지 않는다. 메소드를 통한 접근만이 허용될 뿐이다.

> 하나의 소스파일(*.java)에는 public클래스가 단 하나만 존재할 수 있으며, 소스파일의 이름은 반드시 public클래스의 이름과 같아야 한다.

### 생성자의 접근 제어자

생성자의 접근 제어자를 사용함으로써 인스턴스의 생성을 제한할 수 있다. 보통 생성자의 접근 제어자는 클래스의 접근 제어자와 같지만, 다르게 지정할 수도 있다.

생성자의 접근 제어자를 `private`으로 지정하면, 외부에서 생성자에 접근할 수 없으므로 인스턴스를 생성할 수 없게 된다. 그래도 클래스 내부에서는 인스턴스를 생성할 수 있다.

``` java
class Singleton {
    private Singleton() {
        ...
    }
    ...
}
```

대신 인스턴스를 생성해서 반환해주는 `public`메소드를 제공함으로써 외부에서 이 클래스의 인스턴스를 사용하도록 할 수 있다. 이 메소드는 `public`인 동시에 `static`이어야 한다.

``` java
class Singleton {
        ...
    private static Singleton s = new Singleton();   // getInstance()에서 사용될 수 있도록 인스턴스가 미리 생성되어야 하므로 static이어야 한다.
    private Singleton() {
        ...
    }

    // 인스턴스를 생성하지 않고도 호출할 수 있어야 하므로 static이어야 한다.
    public static Singleton getInstance() {
        return s;
    }
        ...
}
```

이처럼 생성자를 통해 직접 인스턴스를 생성하지 못하게 하고 `public`메소드를 통해 인스턴스에 접근하게 함으로써 사용할 수 있는 인스턴스의 개수를 제한할 수 있다.

또 한 가지, 생성자가 `private`인 클래스는 다른 클래스의 조상이 될 수 없다. 왜냐하면, 자손 클래스의 인스턴스를 생성할 때 조상 클래스의 생성자를 호출해야만 하는데, 생성자의 접근 제어자가 `private`이므로 자손 클래스에서 호출하는 것이 불가능하기 때문이다.

그래서 클래스 앞에 `final`을 더 추가하여 상속할 수 없는 클래스라는 것을 알리는 것이 좋다.

예제 7-14 / ch7 / SingletonTest.java

``` java
final class Singleton {
	private static Singleton s = new Singleton();
    private Singleton() {
        //...
    }

    public static Singleton getInstance() {
    	if(s == null) s = new Singleton();
    	
        return s;
    }
}

public class SingletonTest {
	public static void main(String[] args) {
//		Singleton s = new SingletonTest();	// 에러. Singleton() has private access in Singleton
		Singleton s = Singleton.getInstance();
	}
}
```

</br>

## 4.6 제어자(modifier)의 조합

제어자가 사용될 수 있는 대상을 중심으로 제어자를 정리하였다.

![image](https://ifh.cc/g/Jv8oqp.png)

마지막으로 제어자를 조합해서 사용할 때 주의해야 할 사항에 대해 정리하였다.

> 1. **메소드에 static과 abstract를 함께 사용할 수 없다.**   
> static메소드는 몸통이 있는 메소드에만 사용할 수 있기 때문이다.
> 2. **클래스에 abstract와 final을 동시에 사용할 수 없다.**   
> 클래스에 사용되는 final은 클래스를 확장할 수 없다는 의미이고 abstract는 상속을 통해서 완성되어야 한다는 의미이므로 서로 모순되기 때문이다.
> 3. **abstract메소드의 접근 제어자가 private일 수 없다.**   
> abstract메소드는 자손 클래스에서 구현해주어야 하는데 접근 제어자가 private이면, 자손 클래스에서 접근할 수 없기 때문이다.
> 4. **메소드에 private과 final을 같이 사용할 필요는 없다.**   
> 접근 제어자가 private인 메소드는 오버라이딩될 수 없기 때문이다. 이 둘 중 하나만 사용해도 의미가 충분하다.