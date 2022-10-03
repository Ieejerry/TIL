Chapter 7. 객체지향 프로그래밍2

# 7. 인터페이스(interface)

</br>

## 7.1 인터페이스란?

인터페이스는 일종의 추상클래스이다. 인터페이스는 추상클래스처럼 추상메소드를 갖지만 추상클래스보다 추상화 정도가 높아서 추상클래스와 달리 몸통을 갖춘 일반 메소드 또는 멤버변수를 구성원으로 가질 수 없다. 오직 추상메소드와 상수만을 멤버로 가질 수 있으며, 그 외의 다른 어떠한 요소도 허용하지 않는다.

인터페이스도 추상클래스처럼 완성되지 않은 불완전한 것이기 때문에 그 자체만으로 사용되기 보다는 다른 클래스를 작성하는데 도움 줄 목적으로 작성된다.

</br>

## 7.2 인터페이스의 작성

인터페이스를 작성하는 것은 클래스를 작성하는 것과 같다. 다만 키워드로 `class` 대신 `interface`를 사용한다는 것만 다르다. 그리고 `interface`에도 클래스와 같이 접근제어자로 `public` 또는 `default`를 사용할 수 있다.

``` java
interface 인터페이스이름 {
    public static final 타입 상수이름 = 값;
    public abstract 메소드이름(매개변수목록);
}
```

일반적인 클래스의 멤버들과 달리 인터페이스의 멤버들은 다음과 같은 제약사항이 있다.

> - 모든 멤버변수는 public static final 이어야 하며, 이를 생략할 수 있다.
> - 모든 메소드는 public abstract 이어야 하며, 이를 생략할 수 있다. 단, static메소드와 디폴트 메소드는 예외(JDK1.8부터)

인터페이스에 정의된 모든 멤버에 예외없이 적용되는 사항이기 때문에 제어자를 생략할 수 있는 것이며, 편의상 생략하는 경우가 많다. 생략된 제어자는 컴파일 시에 컴파일러가 자동적으로 추가해준다.

``` java
interface PlayingCard {
    public static final int SPADE = 4;
    final int DIAMOND = 3;  // public static final int DIAMOND = 3;
    static int HEART = 2;   // public static final int DIHEART = 2;
    int CLOVER = 1; // public static final int CLOVER = 1;

    public abstract String getCardNumber();
    String getCardKind();   // public abstract String getCardKind();
}
```

원래는 인터페이스의 모든 메소드는 추상메소드이어야 하는데, JDK1.8부터 인터페이스에 static메소드와 디폴트 메소드(defalut method)의 추가를 허용하는 방향으로 변경되었다.

</br>

## 7.3 인터페이스의 상속

인터페이스는 인터페이스로부터만 상속받을 수 있으며, 클래스와는 달리 다중상속, 즉 여러 개의 인터페이스로부터 상속을 받는 것이 가능하다.

> 인터페이스는 클래스와 달리 Object클래스와 같은 최고 조상이 없다.

``` java
interface Movable {
    /* 지정된 위치(x, y)로 이동하는 기능의 메소드 */
    void move(int x, int y);
}

interface Attackable {
    /* 지정된 대상(u)을 공격하는 기능의 메소드 */
    void attack(Unit u);
}

interface Fightable extends Movable, Attackable { }
```

클래스의 상속과 마찬가지로 자손 인터페이스(Fightable)는 조상 인터페이스(Movable, Attackble)에 정의된 멤버를 모두 상속받는다.

</br>

## 7.4 인터페이스의 구현

인터페이스도 추상클래스처럼 그 자체로는 인스턴스를 생성할 수 없으며, 추상클래스가 상속을 통해 추상메소드를 완성하는 것처럼, 인터페이스도 자신에 정의된 추상메소드의 몸통을 만들어주는 클래스를 작성해야 하는데, 그 방법은 추상클래스가 자신을 상속받는 클래스를 정의하는 것과 다르지 않다. 다만 클래스는 확장한다는 의미의 키워드 `extends`를 사용하지만 인터페이스는 구현한다는 의미의 키워드 `implements`를 사용한다.

``` java
class 클래스이름 implements 인터페이스이름 {
    // 인터페이스에 정의된 추상메소드를 구현해야 한다.
}

class Fighter implements Fightable {
    public void move(int x, int y) { /* 내용 생략 */ }
    public void attack(Unit u) { /* 내용 생략 */ }
}
```

만일 구현하는 인터페이스의 메소드 중 일부만 구현한다면, `abstract`를 붙여서 추상클래스로 선언해야 한다.

``` java
abstract class Fighter implements Fightable {
    public void move(int x, int y) { /* 내용 생략 */ }
}
```

그리고 다음과 같이 상속과 구현을 동시에 할 수도 없다.

``` java
class Fighter extends Unit implements Fightable {
    public void move(int x, int y) { /* 내용 생략 */ }
    public void attack(Unit u) { /* 내용 생략 */ }
}
```

> 인터페이스의 이름에는 주로 Fightable과 같이 '~을 할 수 있는'의 의미인 'able'로 끝나는 것들이 많은데, 그 이유는 어떠한 기능 또는 행위를 하는데 필요한 메소드를 제공한다는 의미를 강조하기 위해서이다. 또한 그 인터페이스를 구현한 클래스는 '~를 할 수 있는'능력을 갖추었다는 의미이기도 하다. 이름이 'able'로 끝나는 것은 인터페이스라고 추측할 수 있지만, 모든 인터페이스의 이름이 반드시 'able'로 끝나야 하는 것은 아니다.

예제 7-24 / ch7 / FighterTest.java

``` java
interface Movable {
	/* 지정된 위치(x, y)로 이동하는 기능의 메소드 */
	void move(int x, int y);
}

interface Attackable {
	/* 지정된 대상(u)을 공격하는 기능의 메소드 */
	void attack(Unit u);
}

interface Fightable extends Movable, Attackable { }

class Unit {
	int currentHP;	// 유닛의 체력
	int x;	// 유닛의 위치(x좌표)
	int y;	// 유닛의 위치(y좌표)
}

class Fighter extends Unit implements Fightable {
	public void move(int x, int y) { /* 내용 생략 */ }
	public void attack(Unit u) { /* 내용 생략 */ }
}

public class FighterTest {
	public static void main(String[] args) {
		Fighter f = new Fighter();
		
		if(f instanceof Unit) {
			System.out.println("f는 Unit클래스의 자손입니다.");
		}
		
		if(f instanceof Fightable) {
			System.out.println("f는 Fightable인터페이스를 구현했습니다.");
		}
		
		if(f instanceof Movable) {
			System.out.println("f는 Movable인터페이스를 구현했습니다.");
		}
		
		if(f instanceof Object) {
			System.out.println("f는 Object클래스의 자손입니다.");
		}
		
		if(f instanceof Attackable) {
			System.out.println("f는 Attackable인터페이스를 구현했습니다.");
		}
	}
}
```

```
f는 Unit클래스의 자손입니다.
f는 Fightable인터페이스를 구현했습니다.
f는 Movable인터페이스를 구현했습니다.
f는 Object클래스의 자손입니다.
f는 Attackable인터페이스를 구현했습니다.
```

예제에 사용된 클래스와 인터페이스간의 관계를 그림으로 보면 다음과 같다.

![image](https://ifh.cc/g/qvysA8.png)

실제로 `Fighter`클래스는 `Unit`클래스로부터 상속받고 `Fightable`인터페이스만을 구현했지만, `Unit`클래스는 `Object`클래스의 자손이고, `Fightable`인터페이스는 `Attackable`과 `Movable`인터페이스의 자손이므로 `Fighter`클래스는 이 모든 클래스와 인터페이스의 자손이 되는 셈이다.

인터페이스는 상속 대신 구현이라는 용어를 사용하지만, 인터페이스로부터 상속받은 추상메소드를 구현하는 것이기 때문에 인터페이스도 조금은 다른 의미의 조상이라고 할 수 있다. 여기서 주의 깊게 봐두어야 할 것은 `Movable`인터페이스에 정의된 `void move(int x, int y)`를 `Fighter`클래스에서 구현할 때 접근 제어자를 `public`으로 했다는 것이다.

``` java
interface Movable {
    void move(int x, int y);
}

class Fighter extends Unit implements Fightable {
    public void move(int x, int y)  { /* 실제구현내용 생략 */}
    public void attack(Unit u) { /* 실제구현내용 생략 */ }
}
```

오버라이딩 할 때는 조상의 메소드보다 넓은 범위의 접근 제어자를 지정해야 한다. `Movavle`인터페이스에 `void move(int x, int y)`와 같이 정의되어 있지만 사실 `public abstrac`가 생략된 것이기 때문에 실제로 `public abstract void move(int x, int y)`이다. 그래서, 이를 구현하는 `Fighter`클래스에는 `void move(int x, int y)`의 접근 제어자를 반드시 `public`으로 해야 하는 것이다.

</br>

## 7.5 인터페이스를 이용한 다중상속

두 조상으로부터 상속받는 멤버 중에서 멤버변수의 이름이 같거나 메소드의 선언부가 일치하고 구현 내용이 다르다면 이 두 조상으로부터 상속받은 자손클래스는 어느 조상의 것을 상속받게 되는 것인지 알 수 없다. 어느 한 쪽으로부터의 상속을 포기하던가, 이름이 충돌하지 않도록 조상클래스를 변경하는 수밖에 없다.

그래서 다중상속은 장점도 있지만 단점이 더 크다고 판단하였기 때문에 자바에서는 다중상속을 허용하지 않는다.

인터페이스는 static상수만 정의할 수 있으므로 조상클래스의 멤버변수와 충돌하는 경우는 거의 없고 충돌된다 하더라도 클래스 이름을 붙여서 구분이 가능하다. 그리고 추상메소드는 구현내용이 전혀 없으므로 조상클래스의 메소드와 선언부가 일치하는 경우에는 당연히 조상 클래스 쪽의 메소드를 상속받으면 되므로 문제되지 않는다.

그러나, 이렇게 하면 상속받는 멤버의 충돌은 피할 수 있지만, 다중상속의 장점을 잃게 된다. 만일 두 개의 클래스로부터 상속을 받아야 할 상황이라면, 두 조상클래스 중에서 비중이 높은 쪽을 선택하고 다른 한쪽은 클래스 내부에 멤버로 포함시키는 방식으로 처리하거나 어느 한쪽의 필요한 부분을 뽑아서 인터페이스로 만든 다음 구현하도록 한다.

예를 들어, 다음과 같이 `Tv`클래스와 `VCR`클래스가 있을 때, `TCVR`클래스를 작성하기 위해 두 클래스로부터 상속을 받을 수만 있으면 좋겠지만, 다중상속을 허용하지 않으므로, 한 쪽만 선택하여 상속받고 나머지 한 쪽은 클래스 내에 포함시켜서 내부적으로 인스턴스를 생성해서 사용하도록 한다.

``` java
public class Tv {
    protected boolean power;
    protected int channel;
    protected int volume;

    public void power() { power = !power; }
    public void channelUp() { channel++; }
    public void channelDown() { channel--; }
    public void volumeUp() { volume++; }
    public void volumeDown() { volume--; }
}

public class VCR {
    protected int counter;  // VCR의 카운터

    public void play() {
        // Tape를 재상ㅎ나다.
    }

    public void stop() {
        // 재생을 멈춘다.
    }

    public void reset() {
        counter = 0;
    }

    public int getCounter() {
        return counter;
    }

    public int setCounter(int c) {
        counter = c;
    }
}
```

`VCR`클래스에 정의된 메소드와 일치하는 추상메소드를 갖는 인터페이스를 작성한다.

``` java
public interface IVCR {
    public void play();
    public void stop();
    public void reset();
    public int getCounter();
    public void setCounter(int c);
}
```

이제 `IVCR`인터페이스를 구현하고 `Tv`클래스로부터 상속받는 `TVCR`클래스를 작성한다.

이때 `VCR`클래스 타입의 참조변수를 멤버변수로 선언하여 `IVCR`인터페이스의 추상메소드를 구현하는데 사용한다.

``` java
public class TVCR extends Tv implements IVCR {
    VCR vcr = new VCR();

    public void play() {
        vcr.play(); // 코드를 작성하는 대신 VCR인스턴스의 메소드를 호출한다.
    }

    public void stop() {
        vcr.stop();
    }

    public void reset() {
        vcr.reset();
    }

    public int getCounter() {
        return vcr.getCounter();
    }

    public void setCounter(int c) {
        vcr.setCounter(c);
    }
}
```

`IVCR`인터페이스를 구현하기 위해서는 새로 메소드를 작성해야하는 부담이 있지만 이처럼 `VCR`클래스의 인스턴스를 사용하면 손쉽게 다중상속을 구현할 수 있다.

또한 `VCR`클래스의 내용이 변경되어도 변경된 내용이 `TVCR`클래스에도 자동적으로 반영되는 효과도 얻을 수 있다.

사실 인터페이스를 새로 작성하지 않고도 `VCR`클래스를 `TVCR`클래스에 포함시키는 것만으로도 충분하지만, 인터페이스를 이용하면 다형적 특성을 이용할 수 있다는 장점이 있다.

</br>

## 7.6 인터페이스를 이용한 다형성

자손클래스의 인스턴스를 조상타입의 참조변수로 참조하는 것이 가능하다.

인터페이스 역시 이를 구현한 클래스의 조상이라 할 수 있으므로 해당 인터페이스 타입의 참조변수로 이를 구현한 클래스의 인스턴스를 참조할 수 있으며, 인터페이스 타입으로의 형변환도 가능하다.

인터페이스 `Fightable`을 클래스 `Fighter`가 구현했을 때, 다음과 같이 `Fighter`인스턴스를 `Fightable`타입의 참조변수로 참조하는 것이 가능하다.

``` java
Fightable f = (Fightable)new Fighter();
또는
Fightable f = new Fighter();
```

> Fightable타입의 참조변수로는 인터페이스 Fightable에 정의된 멤버들만 호출이 가능하다.

따라서 인터페이스는 다음과 같이 메소드의 매개변수의 타입으로 사용될 수 있다.

``` java
void attack(Fightable f) {
    // ...
}
```

인터페이스 타입의 매개변수가 갖는 의미는 메소드 호출 시 해당 인터페이스르 구현한 클래스의 인스턴스를 매겨변수로 제공해야한다는 것이다.

그래서 `attack`메소드를 호출할 때는 매개변수로 `Fightable`인터페이스를 구현한 클래스의 인스턴스를 남겨주어야 한다.

``` java
class Fighter extends Unit implements Fightable {
    public void move(int x, int y) { /* 내용 생략 */ }
    public void attack(Fightable f) { /* 내용 생략 */ }
}
```

위와 같이 `Fightable`인터페이스를 구현한 `Fighter`클래스가 있을 때, `attack`메소드의 매개변수로 `Fighter`인스턴스를 넘겨 줄 수 있다. 즉, `attack(new Fighter())`와 같이 할 수 있다.

그리고 다음과 같이 메소드의 리턴타입으로 인터페이스의 타입을 저장하는 것 역시 가능하다.

``` java
Fightable method() {
    ...
    Fighter f = new Fighter();
    return f;
}
```

**리턴타입이 인터페이스라는 것은 메소드가 해당 인터페이스를 구현한 클래스의 인스턴스를 반환한다는 것을 의미한다.**

위의 코드에서는 `method()`의 리턴타입이 `Fightable`인터페이스이기 때문에 메소드의 return문에서 `Fightabla`인터페이스를 구현한 `Fighter`클래스의 인스턴스를 반환한다.

예제 7-25 / ch7 / ParserTest.java

``` java
interface Parseable {
    // 구문 분석작업을 수행한다.
    public abstract void parse(String fileName);
}

class ParserManager {
    // 리턴타입이 Parseable인터페이스이다.
    public static Parseable getParser(String type) {
        if(type.equals("XML")) {
            return new XMLParser();
        } else {
            Parseable p = new HTMLParser();
            return p;
            // return new HTMLParser();
        }
    }
}

class XMLParser implements Parseable {
    public void parse(String fileName) {
        /* 구문 분석작업을 수행하는 코드를 적는다. */
    	System.out.println(fileName + " - XML parsing completed.");
    }
}

class HTMLParser implements Parseable {
	public void parse(String fileName) {
		/* 구문 분석작업을 수행하는 코드를 적는다. */
		System.out.println(fileName + " - HTML parsing completed.");
	}
}

public class ParserTest {
	public static void main(String[] args) {
		Parseable parser = ParserManager.getParser("XML");
		parser.parse("document.xml");
		parser = ParserManager.getParser("HTML");
		parser.parse("document2.html");
	}
}
```

```
document.xml - XML parsing completed.
document2.html - HTML parsing completed.
```

`Parseable`인터페이스는 구문분석(parsing)을 수행하는 기능을 구현할 목적으로 추상메소드 `parse(String fileName)`을 정의했다. 그리고 `XMLParser`클래스와 `HTMLParser`클래스는 `Parseable`인터페이스를 구현하였다.

`ParserManager`클래스의 `getParser`메소드는 매개변수로 넘겨받는 `type`의 값에 따라 `XMLParser`인스턴스 또는 `HTMLParser`인스턴스를 반환한다.

``` java
Parseable parser = ParserManager.getParser("XML");

public static Parseable getParser(String type) {
    if(type.equals("XML")) {
        return new XMLParser();
    } else {
        Parseable p = new HTMLParser();
        return p;
        // return new HTMLParser();
    }
}
```

`getParser`메소드의 수행결과로 참조변수 `parser`는 `XMLParser`인스턴스의 주소값을 갖게 된다. 마치 `Parseable parser = new XMLParser();`이 수행된 것과 같다.

``` java
parser.parse("document.xml");   // parser는 XMLParser인스턴스를 가리킨다.
```

참조변수 `parser`를 통해 `parse()`를 호출하면, `parser`가 참조하고 있는 `XMLParser`인스턴스의 `parse`메소드가 호출된다.

만일 나중에 새로운 종류의 XML구문분석기 `NewXMLParser`클래스가 나와도 `ParserTest`클래스는 변경할 필요 없이 `ParserManager`클래스의 `getParser`메소드에서 `return new XMLParser();`대신 `return new NewXMLParser();`로 변경하기만 하면 된다.

이러한 장점은 특히 분산환경 프로그래밍에서 그 위력을 발휘한다. 사용자 컴퓨터에 설치된 프로그램을 변경하지 않고 서버측의 변경만으로도 사용자가 새로 개정된 프로그램을 사용하는 것이 가능하다.

</br>

## 7.7 인터페이스의 장점

인터페이스를 사용하는 이유와 그 장점을 정리해 보면 다음과 같다.

> - 개발시간을 단축시킬 수 있다.
> - 표준화가 가능하다.
> - 서로 관계없는 클래스들에게 관게를 맺어줄 수 있다.
> - 독립적인 프로그래밍이 가능하다.

1. 개발시간을 단축시킬 수 있다.   
   
    일단 인터페이스가 작성되면, 이를 사용해서 프로그램을 작성하는 것이 가능하다. 메소드를 호출하는 쪽에서는 메소드의 내용에 관계없이 선언부만 알면 되기 때문이다.   
    그리고 동시에 다른 한 쪽에서는 인터페이스를 구현하는 클래스를 작성하게 되면, 인터페이스를 구현하는 클래스가 작성될 때까지 기다리지 않고도 양쪽에서 동시에 개발을 진행할 수 있다.

2. 표준화가 가능하다.   
   
   프로젝트에 사용되는 기본 틀을 인터페이스로 작성한 다음, 개발자들에게 인터페이스를 구현하여 프로그램을 작성하도록 함으로써 보다 일관되고 정형화된 프로그램의 개발이 가능하다.

3. 서로 관계없는 클래스들에게 관계를 맺어 줄 수 있다.  
   
   서로 상속관계에 있지도 않고, 같은 조상클래스를 가지고 있지 않은 서로 아무런 관계도 없는 클래스들에게 하나의 인터페이스를 공통적으로 구현하도록 함으로써 관계를 맺어줄 수 있다.

4. 독립적인 프로그래밍이 가능하다.   
   
   인터페이스를 이용하면 클래스의 선언과 구현을 분리시킬 수 있기 때문에 실제구현에 독립적인 프로그램을 작성하는 것이 가능하다. 클래스와 클래스간의 직접적인 관계를 인터페이스를 이용해서 간접적인 관계로 변경하면, 한 클래스의 변경이 관련된 다른 클래스에 영향을 미치지 않는 독립적인 프로그래밍이 가능하다.

예를 들어 한 데이터베이스 회사가 제공하는 특정 데이터베이스를 사용하는데 필요한 클래스를 사용해서 프로그램을 작성했다면 이 프로그램은 다른 종류의 데이터베이스를 사용하기 위해서는 전체 프로그램 중에서 데이터베이스 관련된 부분은 모두 변경해야할 것이다.

그러나 데이터베이스 관련 인터페이스를 정의하고 이를 이용해서 프로그램을 작성하면, 데이터베이스의 종류가 변경되더라도 프로그램을 변경하지 않도록 할 수 있다.

단, 데이터베이스 회사에서 제공하는 클래스도 인터페이스를 구현하도록 요구해야 한다. 데이터베이스를 이요한 응용프로그램을 작성하는 쪽에서는 인터페이스를 이용해서 프로그램을 작성하고, 데이터베이스 회사에서는 인터페이스를 구현한 클래스를 작성해서 제공해야한다.

실제로 자바에서는 다수의 데이터베이스와 관련된 다수의 인터페이스를 제공하고 있으며, 프로그래머는 이 인터페이스를 이용해서 프로그래밍하면 특정 데이터베이스에 종속되지 않는 프로그램을 작성할 수 있다.

게임에 나오는 유닛을 클래스로 표현하고 이들의 관계를 상속계층도로 표현해보겠다.

![image](https://ifh.cc/g/2VRqsG.png)

게임에 나오는 모든 유닛들의 최고 조상은 `Unit`클래스이고 유닛의 종류는 지상유닛(`GroundUnit`)과 공중유닛(`AirUnit`)으로 나누어진다.

그리고 지상유닛에는 `Marine`, `SCV(건설인부)`, `Tank`가 있고, 공중유닛으로는 `DropShip(수송선)`이 있다. `SCV`에게 `Tank`와 `DropShip`과 같은 기계화 유닛을 수리할 수 있는 기능을 제공하기 위해 `repair`메소드를 정의한다면 다음과 같다.

``` java
void repair(Tank t) {
    // Tank를 수리한다.
}

void repair(DropShip d) {
    // DropShip을 수리한다.
}
```

이런 식으로 수리가 가능한 유닛의 개수만틈 다른 버전의 오버로딩된 메소드를 정의해야 할 것이다.

이것을 피하기 위해 매개변수의 타입을 이 들의 공통 조상으로 하면 좋겠지만 `DropShip`은 공통조상이 다르기 때문에 공통조상의 타입으로 메소드를 정의한다고 해도 최소한 2개의 메소드가 필요할 것이다.

``` java
void repair(GroundUnit gu) {
    // 매개변수로 넘겨진 지상유닛(GroundUnit)을 수리한다.
}

void repair(AirUnit au) {
    // DropShip을 수리한다.
}
```

그리고 `GroundUnit`의 자손 중에는 `Marine`과 같이 기계화 유닛이 아닌 클래스도 포함될 수 있기 때문에 `repair`메소드의 매개변수 타입으로 `GroundUnit`은 부적합하다.

현재의 상속관계에서는 이들의 공통점은 없다. 이 때 인터페이스를 이용하면 기존의 상속체계를 유지하면서 이들 기계화 유닛에 공통점을 부여할 수 있다.

다음과 같이 `Repairable`이라는 인터페이스를 정의하고 수리가 가능한 기계화 유닛에게 이 인터페이스를 구현하도록 하면 된다.

``` java
interface Repairable {}

class SCV extends GroundUnit implements Repairable {
    // ...
}

class Tank extends GroundUnit implements Repairable {
    // ...
}

class DropShip extends AirUnit implements Repairable {
    // ...
}
```

이제 이 3개의 클래스에느 같은 인터페이스를 구현했다는 공통점이 생겼다. 인터페이스 `Repairable`에 정의된 것은 아무것도 없고, 다닞 인스턴스의 타입체크에만 사용될 뿐이다. `Repairable`인터페이스를 중심으로 상속계층도를 그려보겠다.

![image](https://ifh.cc/g/crKTzR.png)

그리고 `repair`메소드의 매개변수의 타입을 `Repairable`로 선언하면, 이 메소드의 매개변수로 `Repairable`인터페이스를 구현한 클래스의 인스턴스만 받아들여진다.

``` java
void repair(Repairable r) {
    // 매개변수로 넘겨받은 유닛을 수리한다.
}
```

앞으로 새로운 클래스가 추가될 때, `SCV`의 `repair`메소드에 의해서 수리가 가능하도록 하려면 `Repairable`인터페이스를 구현하도록 하면 된다.

예제 7-26 / ch7 / RepairableTest.java

``` java
interface Repairable {}

class Unit2 {
	int hitPoint;
	final int MAX_HP;
	
	Unit2(int hp) {
		MAX_HP = hp;
	}
	// ...
}

class GroundUnit extends Unit2 {
	GroundUnit(int hp) {
		super(hp);
	}
}

class AirUnit extends Unit2 {
	AirUnit(int hp) {
		super(hp);
	}
}

class Tank extends GroundUnit implements Repairable {
	Tank() {
		super(150);	// Tank의 HP는 150이다.
		hitPoint = MAX_HP;
	}
	
	public String toString() {
		return "Tank";
	}
	// ...
}

class DropShip extends AirUnit implements Repairable {
	DropShip() {
		super(125);	// DropShip의 HP는 125이다.
		hitPoint = MAX_HP;
	}
	
	public String toString() {
		return "DropShip";
	}
	// ...
}

class Marine extends GroundUnit {
	Marine() {
		super(40);
		hitPoint = MAX_HP;
	}
	// ...
}

class SCV extends GroundUnit implements Repairable {
	SCV() {
		super(60);	// Tank의 HP는 150이다.
		hitPoint = MAX_HP;
	}
	
	void repair(Repairable r) {
		if(r instanceof Unit2) {
			Unit2 u = (Unit2)r;
			while(u.hitPoint != u.MAX_HP) {
				/* Unit의 HP를 증가시킨다. */
				u.hitPoint++;
			}
			System.out.println(u.toString() + "의 수리가 끝났습니다.");
		}
	}
	// ...
}

public class RepairableTest {
	public static void main(String[] args) {
		Tank tank = new Tank();
		DropShip dropShip = new DropShip();
		
		Marine marine = new Marine();
		SCV scv = new SCV();
		
		scv.repair(tank);	// SCV가 Tank를 수리하도록 한다.
		scv.repair(dropShip);
//		scv.repair(marine);	// 에러. repair(Repairable) in SCV cannot be applied to (Marine) 
	}
}
```

```
Tank의 수리가 끝났습니다.
DropShip의 수리가 끝났습니다.
```

`repair`메소드의 매개변수 `r`은 `Repairable`타입이기 때문에 인터페이스 `Repairable`에 정의된 멤버만 사용할 수 있다. 그러나 `Repairable`에는 정의된 멤버가 없으므로 이 타입의 참조변수로는 할 수 있는 일은 아무 것도 없다.

그래서 `instanceof`연산자로 타입을 체크한 뒤 캐스팅하여 `Unit2`클래스에 정의된 `hipPoint`와 `MAX_HP`를 사용할 수 있도록 하였다.

그 다음엔 유닛의 현재 체력(`hipPoint`)이 유닛이 가질 수 있는 최고 체력(`MAX_HP`)이 될 때까지 체력을 증가시키는 작업을 수행한다.

`Marine`은 `Repairable`인터페이스를 구현하지 않았으므로 `SCV`클래스의 `repair`메소드의 매개벼누솔 `Marine`을 사용하면 컴파일 시에 에러가 발생한다.

이와 유사한 예를 한 가지 더 들어보겠다. 게임에 나오는 건물들을 클래스로 표현하고 이들의 관계를 상속계층도로 표현하였다.

![image](https://ifh.cc/g/QVYkM6.png)

건물을 표현하는 클래스 `Academy`, `Bunker`, `Barrack`, `Factory`가 있고 이들의 조상인 `Building`클래스가 있다고 하겠다. 이 때 `Barrack`클래스와 `Factory`클래스에 건물을 이동시킬 수 있는 새로운 메소드를 추가하겠다.

``` java
void liftOff() { /* 내용 생략 */ }
void move(int x, int y) { /* 내용 생략 */ }
void stop() { /* 내용 생략 */ }
void land() { /* 내용 생략 */ }
```

`Barrack`클래스와 `Factory`클래스 모두 위의 코드를 적어주면 되긴 하지만, 코드가 중복된다는 단점이 있다. 그렇다고 해서 조상클래스인 `Building`클래스에 코드를 추가해주면, `Building`클래스의 다른 자손인 `Academy`와 `Bunker`클래스도 추가된 코드를 상속받으므로 안 된다.

이런 경우에도 인터페이스를 이용해서 해결할 수 있다. 우선 새로 추가하고자하는 메소드를 정의하는 인터페이스를 정의하고 이를 구현하는 클래스를 작성한다.

``` java
interface Liftable {
    /* 건물을 들어 올린다. */
    void liftOff(); // public abstract가 생략되었음.
    /* 건물을 이동한다. */
    void move(int x, int y);
    /* 건물을 정지시킨다. */
    void stop();
    /* 건물을 착륙시킨다. */
    void land();
}

class LiftableImp1 implements Liftable {
    public void liftOff() { /* 내용 생략 */ }
    public void move(int x, int y) { /* 내용 생략 */ }
    public void stop() { /* 내용 생략 */ }
    public void land() { /* 내용 생략 */ }
}
```

마지막으로 새로 작성된 인터페이스와 이를 구현한 클래스를 `Barrack`과 `Factory`클래스에 적용하면 된다.

![image](https://ifh.cc/g/7Tr4NJ.png)

`Barrack`클래스가 `Liftable`인터페이스를 구현하도록 하고, 인터페이스를 구현한 `LiftableImpl`클래스를 `Barrack`클래스에 포함시켜서 내부적으로 호출해서 사용하도록 한다.

이렇게 함으로써 같은 내용의 코드를 `Barrack`클래스와 `Factory`클래스에서 각각 작성하지 않고 `LiftableImpl`클래스 한 곳에서 관리할 수 있다. 그리고 작성된 `Liftable`인터페이스와 이를 구현한 `LiftableImpl`클래스는 후에 다시 재사용될 수 있다.

``` java
class Barrack extends Buidling implements Liftable {
    LiftableImpl l  = new LiftableImpl();
    void liftOff() { l.liftOff(); }
    void move(int x, int y) { l.move(x, y); }
    void stop() { l.stop(); }
    void land() { l.land(); }
    void trainMarine() { /* 내용 생략 */ }
        ...
}

class Factory extends Building implements Liftable {
    LiftableImpl l = new LiftableImpl();
    void liftOff() { l.liftOff(); }
    void move(int x, int y) { l.stop(); }
    void stop() { l.stop(); }
    void land() { l.land(); }
    void makeTank() { /* 내용 생략 */ }
        ...
}
```

</br>

## 7.8 인터페이스의 이해

인터페이스를 이해하기 위해서는 다음의 두 가지 사항을 반드시 염두에 두고 있어야 한다.

> - 클래스를 사용하는 쪽(User)과 클래스를 제공하는 쪽(Provider)이 있다.
> - 메소드를 사용(호출)하는 쪽(User)에서는 사용하려는 메소드(Provider)의 선언부만 알면 된다.(내용은 몰라도 된다.)

예제 7-27 / ch7 / InterfaceTest.java

``` java
class A {
	public void methodA(B b) {
		b.methodB();
	}
}

class B {
	public void methodB() {
		System.out.println("methodB()");
	}
}

public class InterfaceTest {
	public static void main(String[] args) {
		A a = new A();
		a.methodA(new B());
	}
}
```

```
methodB()
```

예제 7-27과 같이 클래스 `A`와 클래스 `B`가 있다고 하겠다. 클래스 `A(User)`는 클래스 `B(Provider)`의 인스턴스를 생성하고 메소드를 호출한다. 이 두 클래스는 서로 직접적인 관계에 있다. 이것을 간단히 'A-B'라고 표현하겠다.

![image](https://ifh.cc/g/4OSNYR.png)

이 경우 클래스 `A`를 작성하려면 클래스 `B`가 이미 작성되어 있어야 한다. 그리고 클래스 `B`의 `methodB()`의 선언부가 변경되면, 이를 사용하는 클래스 `A`도 변경되어야 한다.

이와 같이 직접적인 관계의 두 클래스는 한 쪽(Provider)이 변경되면 다른 한 쪽(User)도 변경되어야 한다는 단점이 있다.

그러나 클래스 `A`가 클래스 `B`를 직접 호출하지 않고 인터페이스를 매개체로 해서 클래스 `A`가 인터페이스를 통해서 클래스 `B`의 메소드에 접근하도록 하면, 클래스 `B`에 변경사항이 생기거나 클래스 `B`와 같은 기능의 다른 클래스로 대체 되어도 클래스 `A`는 전혀 영향을 받지 않도록 하는 것이 가능하다.

두 클래스간의 관계를 간접적으로 변경하기 위해서는 먼저 인터페이스를 이용해서 클래스`B(Provider)`의 선언과 구현을 분리해야한다.

먼저 다음과 같이 클래스 `B`에 정의된 메소드를 추상메소드로 정의하는 인터페이스 `I`를 정의한다.

``` java
interface I {
    public abstract void methodB();
}
```

그 다음에는 클래스 `B`가 인터페이스 `I`를 구현하도록 하였다.

``` java
class B implements I {
    public void methodB() {
        System.out.println("methodB in B class");
    }
}
```

이제 클래스 `A`는 클래스 `B` 대신 인터페이스 `I`를 사용해서 작성할 수 있다.

![image](https://ifh.cc/g/OSapqf.png)

> methodA가 호출될 때 인터페이스 I를 구현한 클래스의 인스턴스(클래스 B의 인스턴스)를 제공받아야 한다.

클래스 `A`를 작성하는데 있어서 클래스 `B`가 사용되지 않았다느 점에 주목해야한다. 이제 클래스 `A`와 클래스 `B`는 'A-B'의 직접적인 관계에서 'A-I-B'의 간접적인 관계로 바뀐 것이다.

![image](https://ifh.cc/g/wkjR82.png)

결국 클래스 `A`는 여전히 클래스 `B`의 메소드를 호출하지만, 클래스 A는 인터페이스 `I`하고만 직접적인 관계에 있기 때문에 클래스 `B`의 변경에 영향을 받지 않는다.

클래스 `A`는 인터페이스를 통해 실제로 사용하는 클래스의 이름을 몰라도 되고 심지어는 실제로 구현된 클래스가 존재하지 않아도 문제되지 않는다. 클래스 `A`는 오직 직접적인 관계에 있는 인터페이스 `I`의 영향만 받는다.

![image](https://ifh.cc/g/6PqtJo.png)

예제 7-28 / ch7 / InterfaceTest2.java

``` java
class A2 {
	void autoPlay(I i) {
		i.play();
	}
}

interface I {
	public void play();
}

class B2 implements I {
	public void play() {
		System.out.println("play in B2 class");
	}
}

class C2 implements I {
	public void play() {
		System.out.println("play in C2 class");
	}
}

public class InterfaceTest2 {
	public static void main(String[] args) {
		A2 a = new A2();
		a.autoPlay(new B2());	// void autoPlay(I i)호출
		a.autoPlay(new C2());	// void autoPlay(I i)호출
	}
}
```

```
play in B2 class
play in C2 class
```

클래스 `A`가 인터페이스 `I`를 사용해서 작성되긴 하였지만, 이처럼 매개변수를 통해서 인터페이스 `I`를 구현한 클래스의 인스턴스를 동적으로 제공받아야 한다.

이처럼 매개변수를 통해 동적으로 제공받을 수도 있지만 다음과 같이 제3의 클래스를 통해서 제공받을 수도 있다.

예제 7-29 / ch7 / InterfaceTest3.java

``` java
class A3 {
	void methodA() {
		I3 i = InstanceManager.getInstance();	// 제3의 클래스의 메소드를 통해서 인터페이스 I를 구현한 클래스의 인스턴스를 얻어온다.
		i.methodB();
		System.out.println(i.toString());	// i로 Object클래스의 메소드 호출가능
	}
}

interface I3 {
	public abstract void methodB();
}

class B3 implements I3 {
	public void methodB() {
		System.out.println("methodB in B3 class");
	}
	
	public String toString() { return "class B3"; }
}

class InstanceManager {
	public static I3 getInstance() {
		return new B3();
	}
}

public class InterfaceTest3 {
	public static void main(String[] args) {
		A3 a3 = new A3();
		a3.methodA();
	}
}
```

```
methodB in B class
class B3
```

인스턴스를 직접 생성하지 않고, `getInstance()`라는 메소드를 통해 제공받는다. 이렇게 하면, 나중에 다른 클래스의 인스턴스로 변경되어도 `A`클래스의 변경없이 `getInstance()`만 변경하면 된다는 장점이 생긴다.

``` java
class InstanceManager {
    public static I3 getInstance() {
        return new B3();    // 다른 인스턴스로 바꾸려면 여기만 변경하면 됨.
    }
}
```

그리고 인터페이스 `I3` 타입의 참조변수 `i`로도 `Object`클래스에 정의된 메소드들을 호출할 수 있다는 것도 알아둬야 한다. `i`에 `toString()`이 정의되어 있지 않지만, 모든 객체는 `Object`클래스에 정의된 메소드를 가지고 있을 것이기 때문에 허용하는 것이다.

``` java
class A3 {
	void methodA() {
		I3 i = InstanceManager.getInstance();
		i.methodB();
		System.out.println(i.toString());	// i로 Object클래스의 메소드 호출가능
	}
}
```

</br>

## 7.9 디폴트 메소드와 static메소드

원래는 인터페이스에 추상메소드만 선언할 수 있는데, JDK1.8부터 디폴트 메소드와 static메소드도 추가할 수 있게 되었다.

그리고 인터페이스의 static메소드 역시 접근 제어자가 항상 public이며, 생략할 수 있다.

### 디폴트 메소드

조상 클래스에 새로운 메소드를 추가하는 것은 별 일이 아니지만, 인터페이스의 경우에는 보통 큰 일이 아니다. 인터페이스에 메소드를 추가한다는 것은, 추상 메소드를 추가한다는 것이고, 이 인터페이스를 구현한 기존의 모든 클래스들이 새로 추가된 메소드를 구현해야하기 때문이다.

인터페이스가 변경되지 않으면 제일 좋겠지만, 아무리 설계를 잘해도 언젠가 변경은 발생하기 마련이다. JDK의 설계자들은 고심 끝에 **디폴트 메소드(default method)**라는 것을 고안해 내었다. 디폴트 메소드는 추상 메소드의 기본적인 구현을 제공하는 메소드로, 추상 메소드가 아니기 때문에 디폴트 메소드가 새로 추가되어도 해당 인터페이스를 구현한 클래스를 변경하지 않아도 된다.

디폴트 메소드는 앞에 키워드 `default`를 붙이며, 추상 메소드와 달리 일반 메소드처럼 몸통{}이 있어야 힌다. 디폴트 메소드 역시 접근 제어자가 public이며, 생략가능하다.

![image](https://ifh.cc/g/C1Dyww.png)

위의 왼쪽과 같이 `newMethod()`라는 추상 메소드를 추가하는 대신, 오른쪽과 같이 디폴트 메소드를 추가하면, 기존의 `MyInterface`를 구현한 클래스를 변경하지 않아도 된다. 즉, 조상 클래스에 새로운 메소드를 추가한 것과 동일해 지는 것이다.

대신, 새로 추가된 디폴트 메소드가 기존의 메소드와 이름이 중복되어 충돌하는 경우가 발생한다. 이 충돌을 해결하는 규칙은 다음과 같다.

> 1. **여러 인터페이스의 디폴트 메소드 간의 충돌**   
> - 인터페이스를 구현한 클래스에서 디폴트 메소드를 오버라이딩해야 한다.
> 2. **디폴트 메소드와 조상 클래스의 메소드 간의 충돌**
> - 조상 클래스의 메소드가 상속되고, 디폴트 메소드는 무시된다.

필요한 쪽의 메소드와 같은 내용으로 오버라이딩하면 된다.

예제 7-30 / ch7 / DefaultMethodTest.java

``` java
class Child6 extends Parent6 implements MyInterface, MyInterface2 {
	public void method1() {
		System.out.println("method1() in Child6");	// 오버라이딩
	}
}

class Parent6 {
	public void method2() {
		System.out.println("method2() in Parent6");
	}
}

interface MyInterface {
	default void method1() {
		System.out.println("method1() in MyInterface");
	}
	
	default void method2() {
		System.out.println("method2() in MyInterface");
	}
	
	static void staticMethod() {
		System.out.println("staticMethod() in MyInterface");
	}
}

interface MyInterface2 {
	default void method1() {
		System.out.println("method1() in MyInterface2");
	}
	
	static void staticMethod() {
		System.out.println("staticMethod() in Myinterface2");
	}
}

public class DefaultMethodTest {
	public static void main(String[] args) {
		Child6 c = new Child6();
		c.method1();
		c.method2();
		MyInterface.staticMethod();
		MyInterface2.staticMethod();
	}
}
```

```
method1() in Child
method2() in Parent
staticMethod() in MyInterface
staticMethod() in Myinterface2
```