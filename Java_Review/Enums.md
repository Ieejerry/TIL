Chapter 12. 제네릭스, 열거형, 애너테이션

# 2. 열거형(enums)

</br>

## 2.1 열거형이란?

열거형은 서로 관련된 상수를 편리하게 선언하기 위한 것으로 여러 상수를 정의할 때 사용하면 유용하다. 자바의 열거형은 C언어의 열거형보다 더 향상된 것으로 열거형이 갖는 값뿐만 아니라 타입도 관리하기 떄문에 보다 논리적인 오류를 줄일 수 있다.

![image](https://ifh.cc/g/RVwmhz.png)

기존의 많은 언어들, 예를 들어 C언어에서는 타입이 달라도 값이 같으면 조건식결과가 참(true)이였으나, 자바의 열거형은 '타입에 안전한 열거형(typesafe enum)'이라서 실제 값이 같아도 타입이 다르면 컴파일 에러가 발생한다. 이처럼 값뿐만 아니라 타입까지 체크하기 때문에 타입에 안전하다고 한다.

``` java
if(Card.CLOVER == Card.TWO) // true지만 false이어야 의미상 맞음.
if(Card.Kind.CLOVER == Card.Value.TWO)  // 컴파일 에러. 값은 같지만 타입이 다름
```

그리고 더 중요한 것은 상수의 값이 바뀌면, 해당 상수를 참조하는 모든 소스를 다시 컴파일해야 한다는 것이다. 하지만 열거형 상수를 사용하면, 기존의 소스를 다시 컴파일하지 않아도 된다.

</br>

## 2.2 열거형의 정의와 사용

열거형을 정의하는 방법은 간단하다. 다음과 같이 괄호 {}안에 상수의 이름을 나열하기만 하면 된다.

> enum 열거형이름 { 상수명1, 상수명2, ... }

예를 들어 동서남북 4방향을 상수로 정의하는 열거형 `Direction`은 다음과 같다.

``` java
enum Direction { EAST, SOUTH, WEST, NORTH }
```

이 열거형에 정의된 상수를 사용하는 방법은 '열거형이름.상수명'이다. 클래스의 static변수를 참조하는 것과 동일하다.

``` java
class Unit {
    int x, y;   // 유닛의 위치
    Direction dir;  // 열거형을 인스턴스 변수로 선언

    void init() {
        dir = Direction.EAST;   // 유닛의 방향을 EAST로 초기화
    }
}
```

열거형 상수간의 비교에는 `==`를 사용할 수 있다. `equals()`가 아닌 `==`로 비교가 가능하다는 것은 그만큼 빠른 성능을 제공한다는 얘기이다. 그러나 `<`, `>`와 같은 비교연산자는 사용할 수 없고, `compareTo()`는 사용가능하다. `compareTo()`는 두 비교대상이 같으면 0, 왼쪽이 크면 양수, 오른쪽이 크면 음수를 반환한다.

``` java
if(dir == Direction.EAST) {
    x++;
} else if(dir > Direction.WEST) {   // 에러. 열거형 상수에 비교연산자 사용불가
    ...
} else if(dir.compareTo(Direction.WEST) > 0) {  // compareTo()는 가능
    ...
}
```

다음과 같이 switch문의 조건식에도 열거형을 사용할 수 있다.

``` java
void move() {
    switch(dir) {
        case EAST: x++; // Direction.EAST라고 쓰면 안된다.
            break;
        case WEST: x--;
            break;
        case SOUTH: y++;
            break;
        case NORTH: y--;
            break;
    }
}
```

이 때 주의할 점은 case문에 열거형의 이름은 적지 않고 상수의 이름만 적어야 한다는 제약이 있다. 아마도 그렇게 하는 것이 오타도 줄일 수 있고 보기에도 간결하기 때문이다.

</br>

### 모든 열거형의 조상 - java.lang.Enum

열거형 `Direction`에 정의된 모든 상수를 출력하려면, 다음과 같이 한다.

``` java
Direction[] dArr = Direction.values();

for(Direction d : dArr) // for(Direction d : Direction.values())
    System.out.printf("%s = %d%n", d.name(), d.ordinal());
```

`values()`는 열거형의 모든 상수를 배열에 담아 반환한다. 이 메소드는 모든 열거형이 가지고 있는 것으로 컴파일러가 자동으로 추가해 준다. 그리고 `ordinal()`은 모든 열거형의 조상인 `java.lang.Enum`클래스에 정의된 것으로, 열거형 상수가 정의된 순서(0부터 시작)를 정수로 반환한다.

`Enum`클래스에는 그 밖에도 다음과 같은 메소드가 정의되어 있다.

![image](https://ifh.cc/g/W4Zpz3.png)

이외에도 `values()`처럼 컴파일러가 자동적으로 추가해주는 메소드가 하나 더 있다.

``` java
static E values()
static E valueOf(String name)
```

이 메소드는 열거형 상수의 이름으로 문자열 상수에 대한 참조를 얻을 수 있게 해준다.

``` java
Direction d = Direction.valueOf("WEST");

System.out.println(d);  // WEST
System.out.println(Direction.WEST == Direction.valueOf("WEST"));    // true
```

이제 예제를 통해 열거형을 직접 정의하고 사용해보겠다.

</br>

예제 12-5 / ch12 / EnumEx1.java

``` java
enum Direction { EAST, SOUTH, WEST, NORTH }

public class EnumEx1 {
	public static void main(String[] args) {
		Direction d1 = Direction.EAST;
		Direction d2 = Direction.valueOf("WEST");
		Direction d3 = Enum.valueOf(Direction.class, "EAST");
		
		System.out.println("d1 = " + d1);
		System.out.println("d2 = " + d2);
		System.out.println("d3 = " + d3);
		
		System.out.println("d1 == d2 ? " + (d1 == d2));	// false
		System.out.println("d1 == d3 ? " + (d1 == d3));	// frue
		System.out.println("d1.equals(d3) ? " + d1.equals(d3));
//		System.out.println("d2 > d3 ? " + (d1 > d3));	// 에러
		System.out.println("d1.compareTo(d3) ? " + d1.compareTo(d3));
		System.out.println("d1.compareTo(d2) ? " + d1.compareTo(d2));
		
		switch (d1) {
		case EAST:	// Direction.EAST라고 쓸 수 없다.
			System.out.println("The direction is EAST."); break;
		case SOUTH:
			System.out.println("The direction is SOUTH."); break;
		case WEST:
			System.out.println("The direction is WEST."); break;
		case NORTH:
			System.out.println("The direction is NORTH."); break;
		default:
			System.out.println("Invalid direction."); break;
		}
		
		Direction[] dArr = Direction.values();
		
		for(Direction d : dArr)	// for(Direction d : Direction.values())
			System.out.printf("%s = %d%n", d.name(), d.ordinal());	// 순서
	}
}
```

```
d1 = EAST
d2 = WEST
d3 = EAST
d1 == d2 ? false
d1 == d3 ? true
d1.equals(d3) ? true
d1.compareTo(d3) ? 0
d1.compareTo(d2) ? -2
The direction is EAST.
EAST = 0
SOUTH = 1
WEST = 2
NORTH = 3
```

</br>

## 2.3 열거형에 멤버 추가하기

`Enum`클래스에 정의된 `ordinal()`이 열거형 상수가 정의된 순서를 반환하지만, 이 값을 열거형 상수의 값으로 사용하지 않는 것이 좋다. 이 값은 내부족인 용도로만 사용되기 위한 것이기 때문이다

열거형 상수의 값이 불연속적인 경우에는 이 때는 다음과 같이 열거형 상수의 이름 옆에 원하는 값을 괄호 ()와 함께 적어주면 된다.

> enum Direction { EAST(1), SOUTH(2), WEST(3), NORTH(4) }

그리고 지정된 값을 저장할 수 있는 인스턴스 변수와 생성자를 새로 추가해 주어야 한다. 이 때 주의할 점은, 먼저 열거형 상수를 모두 정의한 다음에 다른 멤버들을 추가해야한다는 것이다. 그리고 열거형 상수의 마지막에 `;`도 잊지 말아야 한다.

``` java
enum Direction {
    EAST(1), SOUTH(5), WEST(-1), NORTH(10); // 끝에 ';'를 추가해야 한다.

    private final int value;    // 정수를 저장할 필드 (인스턴스 변수)를 추가
    Direction(int value) { this.value = value; }    // 생성자를 추가

    public int getValue() { return value; }
}
```

열거형의 인스턴스 변수는 반드시 `final`이어야 한다는 제약은 없지만, `value`는 열거형 상수의 값을 저장하기 위한 것이므로 `final`을 붙였다. 그리고 외부에서 이 값을 얻을 수 있게 `getValue()`도 추가하였다.

``` java
Direction d = new Direction(1); // 에러. 열거형의 생성자는 외부에서 호출불가
```

열거형 `Direction`에 새로운 생성자가 추가되었지만, 위와 같이 열거형의 객체를 생성할 수 없다. 열거형의 생성자는 제어자가 묵시적으로 `private`이기 때문이다.

``` java
enum Direction {
        ...
    Direction(int value) {  // private Direction(int value)와 동일
        ...
}
```

필요하다면, 다음과 같이 하나의 열거형 상수에 여러 값을 지정할 수도 있다. 다만 그에 맞게 인스턴스 변수와 생성자 등을 새로 추가해주어야 한다.

``` java
enum Direction {
    EAST(1, ">"), SOUTH(2, "V"), WEST(3, "<"), NORTH(4, "^");

    private final int value;
    private final String symbol;

    Direction(int value, String symbol) {   // 접근 제어자 private이 생략됨
        this.value = value;
        this.symbol = symbol;
    }

    public int getValue() { return value; }
    public String getSymbol()  { return symbol; }
}
```

</br>

예제 12-6 / ch12 / EnumEx2.java

``` java
enum Direction2 {
	EAST(1, ">"), SOUTH(2, "V"), WEST(3, "<"), NORTH(4, "^");
	
	private static final Direction2[] DIR_ARR = Direction2.values();
	private final int value;
	private final String symbol;
	
	Direction2(int value, String symbol) {	// 접근 제어자 private 생략됨
		this.value = value;
		this.symbol = symbol;
	}
	
	public int getValue() { return value; }
	public String getSymbol() { return symbol; }
	
	public static Direction2 of(int dir) {
		if(dir < 1 || dir > 4)
			throw new IllegalArgumentException("Invalid value : " + dir);
		
		return DIR_ARR[dir - 1];
	}
	
	// 방향을 회전시키는 메소드. num의 값만큼 90도씩 시계방향으로 회전한다.
	public Direction2 rotate(int num) {
		num = num % 4;
		
		if(num < 0) num += 4;	// num이 음수일 때는 시계반대 방향으로 회전
		
		return DIR_ARR[(value - 1+ num) % 4];
	}
	
	public String toString() {
		return name() + getSymbol();
	}
}	// enum Direction2

public class EnumEx2 {
	public static void main(String[] args) {
		for(Direction2 d : Direction2.values())
			System.out.printf("%s = %d%n", d.name(), d.getValue());
		
		Direction2 d1 = Direction2.EAST;
		Direction2 d2 = Direction2.of(1);
		
		System.out.printf("d1 = %s, %d%n", d1.name(), d1.getValue());
		System.out.printf("d2 = %s, %d%n", d2.name(), d2.getValue());
		System.out.println(Direction2.EAST.rotate(1));
		System.out.println(Direction2.EAST.rotate(2));
		System.out.println(Direction2.EAST.rotate(-1));
		System.out.println(Direction2.EAST.rotate(-2));
	}
}
```

```
SOUTH = 2
WEST = 3
NORTH = 4
d1 = EAST, 1
d2 = EAST, 1
SOUTHV
WEST<
NORTH^
WEST<
```

</br>

### 열거형에 추상 메소드 추가하기

열거형 `Transportation`은 운송 수단의 종류 별로 상수를 정의하고 있으며, 각 운송 수단에는 기본요금(BASIC_FARE)이 책정되어 있다.

``` java
enum Transportation {
    BUS(100), TRAIN(150), SHIP(100), AIRPLANE(300);

    private final int BASIC_FARE;

    private Transportation(int basicFare) {
        BASIC_FARE = basicFare;
    }

    int fare() {    // 운송 요금을 반환
        return BASIC_FARE;
    }
}
```

그러나 이것만으로는 부족하다. 거리에 따라 요금을 계산하는 방식이 각 운송 수단마다 다를 것이기 때문이다. 이럴 때, 열거형에 추상 메소드 `fare(int distance)`를 선언하면 각 열거형 상수가 이 추상 메소드를 반드시 구현해야 한다.

``` java
enum Transportation {
    BUS(100) {
        int fare(int distance) { return distance * BASIC_FARE; }
    },
    TRAIN(150) { int fare(int distance) { return distance * BASIC_FARE; }},
    SHIP(100) { int fare(int distance) { return distance * BASIC_FARE; }},
    AIRPLANE(300) { int fare(int distance) { return distance * BASIC_FARE; }};

    abstract int fare(int distance);    // 거리에 따른 요금을 계산하는 추상 메소드

    protected final int BASIC_FARE; //protected로 해야 각 상수에서 접근가능

    Transportation(int basicFare) {
        BASIC_FARE = basicFare;
    }

    public int getBasicFare() { return BASIC_FARE; }
}
```

위의 코드는 열거형에 정의된 추상 메소드를 각 상수가 어떻게 구현하는지 보여준다. 마치 익명 클래스를 작성한 것처럼 보일 정도로 유사하다.

</br>

예제 12-7 / ch12 / EnumEx3.java

``` java
enum Transportation {
    BUS(100) { int fare(int distance) { return distance * BASIC_FARE; }},
    TRAIN(150) { int fare(int distance) { return distance * BASIC_FARE; }},
    SHIP(100) { int fare(int distance) { return distance * BASIC_FARE; }},
    AIRPLANE(300) { int fare(int distance) { return distance * BASIC_FARE; }};

    protected final int BASIC_FARE; // protected로 해야 각 상수에서 접근가능

    Transportation(int basicFare) {	// private Transportation(int basicFare) {
        BASIC_FARE = basicFare;
    }

    public int getBasicFare() { return BASIC_FARE; }
    
    abstract int fare(int distance);    // 거리에 따른 요금 계산
}

public class EnumEx3 {
	public static void main(String[] args) {
		System.out.println("bus fare = " + Transportation.BUS.fare(100));
		System.out.println("train fare = " + Transportation.TRAIN.fare(100));
		System.out.println("ship fare = " + Transportation.SHIP.fare(100));
		System.out.println("airplane fare = " + Transportation.AIRPLANE.fare(100));
	}
}
```

```
bus fare = 10000
train fare = 15000
ship fare = 10000
airplane fare = 30000
```

예제에서는 각 열거형 상수가 추상 메소드 `fare()`를 똑같은 내용으로 구현했지만, 다르게 구현될 수도 있게 하려고 추상 메소드로 선언한 것이다.

</br>

## 2.4 열거형의 이해

열거형의 이해를 돕기 위해 마지막으로 열거형이 내부적으로 어떻게 구현되었는지에 대해 알아보겠다.

만일 열거형 Direction이 다음과 같이 정의되어 있을 때,

> enum Direction { EAST, SOUTH, WEST, NORTH }

사실은 열거형 상수 하나하나가 `Direction`객체이다. 위의 문장을 클래스로 정의한다면 다음과 같다.

``` java
class Direction {
    static final Direction EAST = new Direction("EAST");
    static final Direction SOUTH = new Direction("SOUTH");
    static final Direction WEST = new Direction("WEST");
    static final Direction NORTH = new Direction("NORTH");

    private String name;

    private Direction(String name) {
        this.name = name;
    }
}
```

`Direction`클래스의 static상수 `EAST`, `SOUTH`, `WEST`, `NORTH`의 값은 객체의 주소이고, 이 값은 바뀌지 않는 값이므로 `==`로 비교가 가능한 것이다.

모든 열거형은 추상 클래스 `Enum`의 자손이므로, `Enum`을 흉내 내어 `MyEnum`을 작성하면 다음과 같다.

``` java
abstract class MyEnum<T extends MyEnum<T>> implements Comparable<T> {
    static int id = 0;  // 객체에 붙일 일련번호(0부터 시작)

    int ordinal;
    String name = "";

    public int ordinal() { return ordinal(); }

    MyEnum(String name) {
        this.name = name;
        ordinal = id++; // 객체를 생성할 때마다 id의 값을 증가시킨다.
    }

    public int compareTo(T t) {
        return ordinal - t.ordinal();
    }
}
```

객체가 생성될 때마다 번호를 붙여서 인스턴스변수 `ordinal`에 저장한다. 그리고 `Comparable`인터페이스를 구현해서 열거형 상수간의 비교가 가능하도록 되어 있다. 두 열거형 상수의 `ordinal`값을 서로 빼주기만 하면 된다. 만일 클래스를 `MyEnum<T>`와 같이 선언하였다면, `compareTo()`를 위와 같이 간단히 작성할 수 없었을 것이다. 타입 `T`에 `ordinal()`이 정의되어 있는지 확인할 수 없기 때문이다.

``` java
abstract class MyEnum<T> implements Comparable<T> {
        ...
    public int compareTo(T t) {
        return ordinal - t.ordinal();   // 에러. 타입 T에 ordinal()이 있을지 확신 X
    }
}
```

그래서 `MyEnum<T extends MyEnum<T>>`와 같이 선언한 것이며, 이것은 타입 `T`가 `MyEnum<T>`의 자손이어야 한다는 의미이다. 타입 `T`가 `MyEnum`의 자손이므로 `ordinal()`이 정의되어 있는 것은 분명하므로 형변환 없이도 에러가 나지 않는다.

그리고 추상 메소드를 새로 추가하면, 클래스 앞에도 `abstract`를 붙여줘야 하고, 각 static상수들도 추상 메소드를 구현해주어야 한다. 아래의 코드에서는 익명 클래스의 형태로 추상 메소드를 구현하였다.

``` java
abstract class Direction extends MyEnum {
    static final Direction EAST = new Direction("EAST") {   // 익명 클래스
        Point move(Point p) { /* 내용 생략 */ }
    };
    static final Direction SOUTH = new Direction("SOUTH") {   // 익명 클래스
        Point move(Point p) { /* 내용 생략 */ }
    };
    static final Direction WEST = new Direction("WEST") {   // 익명 클래스
        Point move(Point p) { /* 내용 생략 */ }
    };
    static final Direction NORTH = new Direction("NORTH") {   // 익명 클래스
        Point move(Point p) { /* 내용 생략 */ }
    };

    private String name;

    private Direction(String name) {
        this.name = name;
    }

    abstract Point move(Point p);
}
```

이제 왜 열거형에 추상 메소드를 추가하면 각 열거형 상수가 추상 메소드를 구현해야하는지 이해가 된다.

</br>

예제 12-8 / ch12 / EnumEx4.java

``` java
abstract class MyEnum<T extends MyEnum<T>> implements Comparable<T> {
    static int id = 0;
    int ordinal;
    String name = "";

    public int ordinal() { return ordinal; }

    MyEnum(String name) {
        this.name = name;
        ordinal = id++;
    }

    public int compareTo(T t) {
        return ordinal - t.ordinal();
    }
}

abstract class MyTransportation extends MyEnum {
    static final MyTransportation BUS = new MyTransportation("BUS", 100) {
        int fare(int distance) { return distance * BASIC_FARE; }
    };
    static final MyTransportation TRAIN = new MyTransportation("TRAIN", 150) {
    	int fare(int distance) { return distance * BASIC_FARE; }
    };
    static final MyTransportation SHIP = new MyTransportation("SHIP", 100) {
    	int fare(int distance) { return distance * BASIC_FARE; }
    };
    static final MyTransportation AIRPLANE = new MyTransportation("AIRPLANE", 300) {
    	int fare(int distance) { return distance * BASIC_FARE; }
    };
    
    abstract int fare(int distance);	// 추상 메소드
    
    protected final int BASIC_FARE;

    private MyTransportation(String name, int basicFare) {
    	super(name);
    	BASIC_FARE = basicFare;
    }

    public String name() { return name; }
    public String toString() { return name; }
}

public class EnumEx4 {
	public static void main(String[] args) {
		MyTransportation t1 = MyTransportation.BUS;
		MyTransportation t2 = MyTransportation.BUS;
		MyTransportation t3 = MyTransportation.TRAIN;
		MyTransportation t4 = MyTransportation.SHIP;
		MyTransportation t5 = MyTransportation.AIRPLANE;
		
		System.out.printf("t1 = %s, %d%n", t1.name, t1.ordinal());
		System.out.printf("t2 = %s, %d%n", t2.name, t2.ordinal());
		System.out.printf("t3 = %s, %d%n", t3.name, t3.ordinal());
		System.out.printf("t4 = %s, %d%n", t4.name, t4.ordinal());
		System.out.printf("t5 = %s, %d%n", t5.name, t5.ordinal());
		System.out.println("t1 == t2 ? " + (t1 == t2));
		System.out.println("t1.compareTo(t3) = " + t1.compareTo(t3));
	}
}
```

```
t1 = BUS, 0
t2 = BUS, 0
t3 = TRAIN, 1
t4 = SHIP, 2
t5 = AIRPLANE, 3
t1 == t2 ? true
t1.compareTo(t3) = -1
```