Chapter 6. 객체지향 프로그래밍1

# 2. 클래스와 객체

</br>

## 2.1 클래스와 객체의 정의와 용도

클래스란 '객체를 정의해놓은 것.' 또는 클래스는 '객체의 설계도 또는 틀'이라고 정의할 수 있다. 클래스는 객체를 생성하는데 사용되며, 객체는 클래스에 정의된 대로 생성된다.

> **클래스의 정의** 클래스란 객체를 저으이해 놓은 것이다.   
**클래스의 용도** 클래스는 객체를 생성하는데 사용된다.

개게의 사전적인 정의는, '실제로 존재하는 것'이다. 주변에서 볼 수 있는 책상, 의자, 자동차와 같은 사물들이 곧 객체이다. 객체지향이론에서는 사물과 같은 유형적인 것뿐만 아니라, 개념이나 논리와 같은 무형적인 것들도 객체로 간주한다.

프로그래밍에서의 객체는 클래스에 정의된 내용대로 메모리의 생성된 것을 뜻한다.

> **객체의 정의** 실제로 존재하는 것, 사물 또는 개념   
**객체의 용도** 객체가 가지고 있는 기능과 속성에 따라 다름   
**유형의 객체** 책상, 의자, 자동차, TV와 같은 사물   
**무형의 객체** 수학공식, 프로그램 에러와 같은 논리와 개념

클래스와 객체의 관계를 실생활에서 예를 들면, 제품 설계도와 제품과의 관계라고 할 수 있다. 예를 들면, TV설계도(클래스)는 TV라는 제품(객체)를 정의한 것이며, TV(객체)를 만드는데 사용된다.

또한 클래스는 단지 객체를 생성하는데 사용될 뿐, 객체 그 자체는 아니다.

프로그래밍에서는 먼저 클래스를 작성한 다음, 클래스로부터 객체를 생성하여 사용한다.

> 객체를 사용한다는 것은 객체가 가지고 있는 속성과 기능을 사용한다는 뜻이다.

![image](https://ifh.cc/g/MNgdb9.png)

클래스를 정의하고 클래스를 통해 객체를 생성하는 이유는 설계도를 통해서 제품을 만드는 이유와 같다. 하나의 설계도만 잘 만들어 놓으면 제품을 만드는 일이 쉬워진다. 제품을 만들 때마다 매번 고민할 필요없이 설계도대로만 만들면 되기 때문이다.

이와 마찬가지로 클래스를 한 번만 잘 만들어 놓기만 하면, 매번 객체를 생성할 때마다 어떻게 객체를 만들어야 할지를 고민하지 않아도 된다. 그냥 클래스로부터 객체를 생성해서 사용하기만 하면 된다.

</br>

## 2.2 객체와 인스턴스

클래스로부터 객체를 만드는 과정을 클래스의 인스턴스화(instanceiate)라고 하며, 어떤 클래스로부터 만들어진 객체를 그 클래스의 인스턴스(instance)라고 한다.

예를 들면, `Tv`클래스로부터 만들어진 객체를 `Tv`클래스의 인스턴스라고 한다. 결국 인스턴스는 객체와 같은 의미이지만, 객체는 모든 인스턴스를 대표하는 포괄적인 의미를 갖고 있으며, 인스턴스는 어떤 클래스로부터 만들어진 것인지를 강조하는 보다 구체적인 의미를 갖고 있다.

![image](https://ifh.cc/g/RG3lfy.png)

</br>

## 2.3 객체의 구성요소 - 속성과 기능

객체는 속성과 기능, 두 종류의 구성요소로 이루어져 있으며, 일반적으로 객체는 다수의 속성과 다수의 기능을 갖는다. 즉, 객체는 속성과 기능의 집합이라고 할 수 있다. 그리고 객체가 가지고 있는 속성과 기능을 그 객체의 멤버(구성원, member)라 한다.

클래스란 객체를 정의한 것이므로 클래스에는 객체의 모든 속성과 기능이 정의되어있다. 클래스로부터 객체를 생성하면, 클래스에 정의된 속성과 기능을 가진 객체가 만들어진다.

속성과 기능은 아래와 같이 같은 뜻의 여러 가지 용어가 있으며, 이 중에서도 '속성'보다는 '멤버변수'를, '기능'보다는 '메소드'를 주로 사용한다.

> **속성(property)** 멤버변수(member variable), 특성(attribute), 필드(field), 상태(state)   
**기능(function)** 메소드(method), 함수(function), 행위(behavior)

보다 쉽게 이해할 수 있도록 TV를 예로 들어보겠다. TV의 속성으로는 전원상태, 크기, 길이, 높이, 색상, 볼륨, 채널과 같은 것들이 있으며, 기능으로는 켜기, 끄기, 불륨 높이기, 채널 변경하기 등이 있다.

![image](https://ifh.cc/g/hWZ5sL.png)

객체지향 프로그래밍에서는 속성과 기능을 각각 변수와 메소드를 표현한다.

속성(property) → 멤버변수(member variable)   
기능(function) → 메소드(method)

채널 → int channel   
채널 높이기 → channelUp() { ... }

위의 분석한 내용을 토대로 `Tv`클래스를 만들어 보면 다음과 같다.

``` java
class Tv {
    String color;   // 색깔
    boolean power;  // 전원상태
    int channel;    // 채널

    void power() { power = !power; }
    void channelUp() { channel++; }
    void channelDown() { channel--; }
}
```

> 멤버변수와 메소드를 선언하는데 있어서 순서는 관계없지만, 일바넞긍로 메소드보다는 멤버변수를 먼저 선언하고 멤버변수는 멤버변수끼리 메소드는 메소드끼리 모아 놓는 것이 일반적이다.

각 변수의 자료형은 속성의 값에 알맞은 것을 선택해야한다.

</br>

## 2.4 인스턴스의 생성과 사용

`Tv`클래스를 선언한 것은 Tv설계도를 작성한 것에 불과하므로, `Tv`인스턴스를 생성해야 제품(Tv)를 사용할 수 있다. 클래스로부터 인스턴스를 생성하는 방법은 여러 가지가 있지만 일반적으로는 다음과 같이 한다.

``` java
클래스명 변수명;           // 클래스의 객체를 참조하기 위한 참조변수를 선언
변수명 = new 클래스명();   // 클래스의 객체를 생성 후, 객체의 주소를 참조변수에 저장

Tv t;                      // Tv클래스 타입의 참조변수 t를 선언
t = new Tv();              // Tv인스턴스를 생성한 후, 생성된 Tv인스턴스의 주소를 t에 저장
```

예제 6-1 / ch6 / TvTest.java
``` java
class Tv {
	// Tv의 속성(멤버변수)
	String color;	// 색상
	boolean power;	// 전원상태(on/off)
	int channel;	// 채널
	
	// Tv의 기능(메소드)
	void power() { power = !power; }	// TV를 켜거나 끄는 기능을 하는 메소드
	void channelUp() { ++channel; }		// TV의 채널을 높이는 기능을 하는 메소드
	void channelDown() { --channel; }		// TV의 채널을 낮추는 기능을 하는 메소드
}

public class TvTest {

	public static void main(String[] args) {
		Tv t;				// Tv인스턴스를 참조하기 위한 변수 t를 선언
		t = new Tv();		// Tv인스턴스를 생성한다.
		t.channel = 7;		// Tv인스턴스의 멤버변수 channel의 값을 7로 한다.
		t.channelDown();	// Tv인스턴스의 메소드 channelDown()을 호출한다.
		System.out.println("현재 채널은 " + t.channel + " 입니다.");
	}

}
```

```
현재 채널은 6 입니다.
```

이 예제는 `Tv`클래스로부터 인스턴스를 생성하고 인스턴스의 속성(`channel`)과 메소드(`channelDown()`)를 사용하는 방법을 보여 주는 것이다.

1. `Tv t;`

`Tv`클래스 타입의 참조변수 `t`를 선언한다. 메모리에 참조변수 `t`를 위한 공간이 마련된다. 아직 인스턴스가 생성되지 않았으므로 참조변수로 아무것도 할 수 없다.

![image](https://ifh.cc/g/M7QOWC.png)

2. `t = new Tv();`

연산자 `new`에 의해 `Tv`클래스의 인스턴스가 메모리의 빈 공간에 생성된다. 주소가 0x100인 곳에 생성되었다고 가정하면, 이 때, 멤버변수는 각 자료형에 해당하는 기본값으로 초기화 된다.   
`color`는 참조형이므로 null로, `power`는 boolean이므로 false로, 그리고 `channel`은 int이므로 0으로 초기화 된다.

![image](https://ifh.cc/g/ySpP8c.png)

그 다음에는 대입연산자(=)에 의해서 생성된 객체의 주소값이 참조변수 `t`에 저장된다. 이제는 참조변수 `t`를 통해 `Tv`인스턴스에 접근할 수 있다. 인스턴스를 다루기 위해서는 참조변수가 반드시 필요하다.

![imge](https://ifh.cc/g/hQL0RT.png)

3. `t.channel = 7;`

참조변수 `t`에 저장된 주소에 있는 인스턴스의 멤버변수 `channel`에 7을 저장한다. 여기서 알 수 있는 것처럼, 인스턴스의 멤버변수(속성)을 사용하려면 '참조변수.멤버변수'와 깉이 하면 된다.

![image](https://ifh.cc/g/vdQdB8.png)

4. `t.channelDown()`

참조변수 `t`가 참조하고 있는 `Tv`인스턴스의 `channelDwon()`메소드를 호출한다. `channelDown()`메소드는 멤버변수 `channel`에 저장되어 있는 값을 1 감소시킨다.

``` java
void channelDown() { --channel; }
```

`channelDown()`에 의해서 `channel`의 값은 7에서 6이 된다.

![image](https://ifh.cc/g/5DQOlk.png)

5. `System.out.println("현재 채널은 " + t.channel + " 입니다.");`

참조변수 `t`가 참조하고 있는 `Tv`인스턴스의 멤버변수 `channel`에 저장되어 있는 값을 출력한다. 현재 `channel`의 값은 6이므로 '현재 채널은 6 입니다.'가 화면에 출력된다.

인스턴스와 참조변수의 관계는 마치 일상생활에서 사용하는 TV와 TV리모컨의 관계와 같다. TV리모컨(참조변수)을 사용하여 TV(인스턴스)를 다루기 때문이다. 다른 점이라면, 인스턴스는 오직 참조변수를 통해서만 다룰 수 있다는 것이다.

그리고 TV를 사용하려면 TV리모컨을 사용해야하고, 에어컨을 사용하려면, 에어컨 리모컨을 사용해야하는 것처럼 `Tv`인스턴스를 사용하려면, `Tv`클래스 타입의 참조변수가 필요하다.

> **인스턴스는 참조변수를 통해서만 다룰 수 있으며, 참조변수의 타입은 인스턴스의 타입과 일치해야 한다.**

예제 6-2 / ch6 / TvTest2.java
``` java
class Tv {
	// Tv의 속성(멤버변수)
	String color;	// 색상
	boolean power;	// 전원상태(on/off)
	int channel;	// 채널
	
	// Tv의 기능(메소드)
	void power() { power = !power; }	// TV를 켜거나 끄는 기능을 하는 메소드
	void channelUp() { ++channel; }		// TV의 채널을 높이는 기능을 하는 메소드
	void channelDown() { --channel; }		// TV의 채널을 낮추는 기능을 하는 메소드
}

public class TvTest2 {

	public static void main(String[] args) {
		Tv t1 = new Tv();	// Tv t1; t1 = new Tv();를 한 문장으로 가능
		Tv t2 = new Tv();
		System.out.println("t1의 channel값은 " + t1.channel + " 입니다.");
		System.out.println("t2의 channel값은 " + t2.channel + " 입니다.");
		
		t1.channel = 7;	// channel 값을 7으로 한다.
		System.out.println("t1의 channel값을 7로 변경하였습니다.");
		
		System.out.println("t1의 channel값은 " + t1.channel + " 입니다.");
		System.out.println("t2의 channel값은 " + t2.channel + " 입니다.");
	}

}
```

```
t1의 channel값은 0 입니다.
t2의 channel값은 0 입니다.
t1의 channel값을 7로 변경하였습니다.
t1의 channel값은 7 입니다.
t2의 channel값은 0 입니다.
```

위의 예제는 `Tv`클래스의 인스턴스 `t1`과 `t2`를 생성한 후에, 인스턴스 `t1`의 멤버변수의 `channel`의 값을 변경하였다.

1. `Tv t1 = new Tv();`   
`Tv t2 = new Tv();`

![image](https://ifh.cc/g/L3FTz7.png)

2. `t1.channel = 7;` // t1이 가르키고 있는 인스턴스의 멤버변수 channel의 값을 7로 변경한다.

![image](https://ifh.cc/g/4RHgYR.png)

같은 클래스로부터 생성되었을지라도 각 인스턴스의 속성(멤버변수)은 서로 다른 값을 유지할 수 있으며, 메소드의 내용은 모든 인스턴스에 대해 동일하다.

예제 6-3 / ch6 / TvTest3.java
``` java
class Tv {
	// Tv의 속성(멤버변수)
	String color;	// 색상
	boolean power;	// 전원상태(on/off)
	int channel;	// 채널
	
	// Tv의 기능(메소드)
	void power() { power = !power; }	// TV를 켜거나 끄는 기능을 하는 메소드
	void channelUp() { ++channel; }		// TV의 채널을 높이는 기능을 하는 메소드
	void channelDown() { --channel; }		// TV의 채널을 낮추는 기능을 하는 메소드
}

public class TvTest3 {

	public static void main(String[] args) {
		Tv t1 = new Tv();
		Tv t2 = new Tv();
		System.out.println("t1의 channel값은 " + t1.channel + " 입니다.");
		System.out.println("t2의 channel값은 " + t2.channel + " 입니다.");
		
		t2 = t1;	// t1이 저장하고 있는 값(주소)를 t2에 저장한다.
		t1.channel = 7;	// channel 값을 7으로 한다.
		System.out.println("t1의 channel값을 7로 변경하였습니다.");
		
		System.out.println("t1의 channel값은 " + t1.channel + " 입니다.");
		System.out.println("t2의 channel값은 " + t2.channel + " 입니다.");
	}

}
```

```
t1의 channel값은 0 입니다.
t2의 channel값은 0 입니다.
t1의 channel값을 7로 변경하였습니다.
t1의 channel값은 7 입니다.
t2의 channel값은 7 입니다.
```

1. `Tv t1 = new Tv();`   
`Tv t2 = new Tv();`

![image](https://ifh.cc/g/L3FTz7.png)

2. `t2 = t1;`   // t1이 저장하고 있는 값(주소)을 t2에 저장한다.

`t1`은 참조변수이므로, 인스턴스의 주소를 저장하고 있다. 이 문장이 수행되면, `t2`가 가지고 있던 값은 잃어버리게 되고, `t1`에 저장되어 있던 값이 `t2`에 저장되게 된다. 그렇게 되면 `t2` 역시 `t1`이 참조하고 있던 인스턴스를 같이 참조하게 되고, `t2`가 원래 참조하고 있던 인스턴스는 더 이상 사용할 수 없게 된다.

![image](https://ifh.cc/g/LyY2P0.png)

> 자신을 참조하고 있는 참조변수가 하나도 없는 인스턴스는 더 이상 사용되어질 수 없으므로 '가비지 컬렉터(Garbage Collector)'에 의해서 자동적으로 메모리에서 제거된다.

3. `t1.channel = 7;` // channel 값을 7로 한다.

![image](https://ifh.cc/g/hj1gDw.png)

4. `System.out.println("t1의 channel값은 " + t1.channel + " 입니다.");`   
`System.out.println("t2의 channel값은 " + t2.channel + " 입니다.");`

이제 `t1`, `t2` 모두 같은 `Tv`클래스의 인스턴스를 가리키고 있기 때문에 `t1.channel`과 `t2.channel`의 값은 7이며 다름과 같은 결과가 화면에 출력된다.

```
t1의 channel값은 7 입니다.
t2의 channel값은 7 입니다.
```

이 예제에서 알 수 있듯이, 참조변수에는 하나의 값(주소)만이 저장될 수 있으므로 둘 이상의 참조변수가 하나의 인스턴스를 가르키는(참조하는) 것은 가능하지만 하나의 참조변수로 여러 개의 인스턴스를 가리키는 것은 가능하지 않다.

![image](https://ifh.cc/g/2s6JPp.png)

(a) 하나의 인스턴스를 여러 개의 참조변수가 가리키는 경우(가능)   
(b) 여러 인스턴스를 하나의 참조변수가 가리키는 경우(불가능)

</br>

## 2.5 객체 배열

객체 역시 배열로 다루는 것이 가능하며, 이를 '객체 배열'이라고 한다. 그렇다고 객체 배열 안에 객체가 저장되는 것은 아니고, 객체의 주소가 저장된다. 사실 객체 배열은 참조변수들을 하나로 묶은 참조 변수 배열인 것이다.

![image](https://ifh.cc/g/G3lGBz.png)

길이가 3인 객체 배열 `tvArr`을 아래와 같이 생성하면, 각 요소는 참조변수의 기본값인 null로 자동 초기화 된다. 그리고 이 객체 배열은 3개의 객체, 정확히는 객체의 주소를 저장할 수 있다.

![image](https://ifh.cc/g/Cyz7yc.png)

위의 그림에서 알 수 있듯이, 객체 배열을 생성하는 것은, 그저 객체를 다루기 위한 참조변수들이 만들어진 것일 뿐, 아직 객체가 저장되지 않았다. 객체를 생성해서 객체 배열의 각 요소에 저장하는 것을 잊으면 안 된다.

``` java
Tv[] tvArr = new Tv[3]; // 참조변수 배열(객체 배열)을 생성

// 객체를 생성해서 배열의 각 요소에 저장
tvArr[0] = new Tv();
tvArr[1] = new Tv();
tvArr[2] = new Tv();
```

배열의 초기화 블럭을 사용하면, 다음과 같이 한 줄로 간단히 할 수 있다.

``` java
Tv[] tvArr = { new Tv(), new Tv(), new Tv() };
```

다뤄야할 객체의 수가 많을 때는 for문을 사용하면 된다.

``` java
Tv[] tvArr = new Tv[100];

for(int i = 0; i < tvArr.length; i++) {
    tvArr[i] = new Tv();
}
```

예제 6-4 / ch6 / TvTest4.java
``` java
public class TvTest4 {

	public static void main(String[] args) {
		Tv[] tvArr = new Tv[3];	// 길이가 3인 Tv객체 배열
		
		// Tv객체를 생성해서 Tv객체 배열의 각 요소에 저장
		for(int i = 0; i < tvArr.length; i++) {
			tvArr[i] = new Tv();
			tvArr[i].channel = i + 10;	// tvArr[i]의 channel에 i + 10을 저장
		}
		
		for(int i = 0; i < tvArr.length; i++) {
			tvArr[i].channelUp();	// tvArr[i]의 메소드를 호출. 채널이 1증가
			System.out.printf("tvArr[%d].channel = %d%n", i, tvArr[i].channel);
		}
	}	// main의 끝

}

class Tv {
	// Tv의 속성(멤버변수)
	String color;	// 색상
	boolean power;	// 전원상태(on/off)
	int channel;	// 채널
	
	// Tv의 기능(메소드)
	void power() { power = !power; }	// TV를 켜거나 끄는 기능을 하는 메소드
	void channelUp() { ++channel; }		// TV의 채널을 높이는 기능을 하는 메소드
	void channelDown() { --channel; }		// TV의 채널을 낮추는 기능을 하는 메소드
}
```

```
tvArr[0].channel = 11
tvArr[1].channel = 12
tvArr[2].channel = 13
```

</br>

## 2.6 클래스의 또 다른 정의

클래스는 '객체를 생성하기 위한 틀'이며, '클래스는 속성과 기능으로 정의되어있다.'고 했다. 이것은 객체지향이론의 관점에서 내린 정의이고, 이번엔 프로그래밍적인 관점에서 클래스의 정의와 의미를 살펴보겠다.

1. 클래스 - 데이터와 함수의 결합

프로그래밍언어에서 데이터 처리를 위한 데이터 저장형태의 발전과정은 다음과 같다.

![image](https://ifh.cc/g/bcClNJ.png)

> **1.변수** 하나의 데이터를 저장할 수 있는 공간   
> **2.배열** 같은 종류의 여러 데이터를 하나의 집합으로 저장할 수 있는 공간   
> **3.구조체** 서로 관련된 여러 데이터를 종류에 관계없이 하나의 집합으로 저장할 수 있는 공간   
> **4.클래스** 데이터와 함수의 결합(구조체 + 함수)

하나의 데이터를 저장하기 위해 변수를, 그리고 같은 종류의 데이터를 보다 효율적으로 다루기 위해서 배열이라는 개념을 도입했으며, 후에는 구조체(structure)가 등장하여 자료형의 종류에 상관없이 서로 관계가 싶은 변수들을 하나로 묶어서 다룰 수 있도록 했다.

그동안 데이터와 함수가 서로 관계가 없는 것처럼 데이터는 데이터끼리, 함수는 함수끼리 따로 다루어져 왔지만, 사실 함수는 주로 데이터를 가지고 작업을 하기 때문에 많은 경우에 있어서 데이터와 함수는 관계가 깊다.

그래서 자바와 같은 객체지향언어에서는 변수(데이터)와 함수를 하나의 클래스에 정의하여 서로 관계가 깊은 변수와 함수들을 함께 다룰 수 있게 했다.

서로 관련된 변수들을 정의하고 이들에 대한 작업을 수행하는 함수들을 함께 정의한 것이 바로 클래스이다.

2. 클래스 - 사용자정의 타입(user-defined type)

프로그래밍언어에서 제공하는 자료형(primitive type)외에 프로그래머가 서로 관련된 변수들을 묶어서 하나의 ㅏ입으로 새로 추가하는 것을 사용자정의 타입(user-defined type)이라고 한다.

다른 프로그래밍언어에서도 사용자정의 타입을 정의할 수 있는 방법을 제공하고 있으며, 자바와 같은 객체지향언어에서는 클래스가 곧 사용자 정의 타입이다.

시간을 표현하기 위해서 위와 같이 3개의 변수르 선언하였다. 만일 3개의 시간을 다뤄야 한다면 다음과 같이 해야 한다.

``` java
int hour1, hour2, hour3;
int minute1, minute2, minute3;
float second1, second2, second3;
```

이처럼 다뤄야 하는 시간이 개수가 늘어날 때마다 시, 분, 초를 위한 변수를 추가해줘야 하는데 데이터의 개수가 많으면 이런 식으로는 곤란하다.

``` java
int[] hour = new int[3];
int[] minute = new int[3];
float[] second = new float[3];
```

위와 같이 배열로 처리하면 다뤄야 하는 시간 데이터의 개수가 늘어나더라도 배열의 크기만 변경해주면 되므로, 변수를 매번 새로 선언해줘야 하는 불편함과 복잡함은 없어졌다. 그러나 하나의 시간을 구성하는 시, 분, 초가 서로 분리되어 있기 때문에 프로그램 수행과정에서 시, 분, 초가 따로 뒤섞여서 올바르지 않은 데이터가 될 가능성이 있다. 이런 경우 시, 분, 초를 하나로 묶는 사용자정의 타입, 즉 클래스를 정의하여 사용해야한다.

``` java
class Time {
    int hour;
    int minute;
    float second;
}
```

위의 코드는 시, 분, 초를 저정하기 위한 세 변수를 멤버변수로 갖는 `Time`클래스를 정의한 것이다. 이제 새로 작성된 사용자정의 타입인 `Time`클래스를 사용해서 코드를 변경하면 아래와 같다.

![image](https://ifh.cc/g/7VH28n.png)

이제 시, 분, 초가 하나의 단위로 묶여서 다루어지기 때문에 다른 시간 데이터와 섞이는 일은 없겠지만, 시간 데이터에는 다음과 같은 추가적인 제약조건이 있다.

> 1. 시, 분, 초는 모두 0보다 크거나 같아야 한다.
> 2. 시의 범위는 0~23, 분과 초의 범위는 0~59 이다.

이러한 조건들이 모두 프로그램 코드에 반영될 때, 보다 정확한 데이터를 유지할 수 있을 것이다. 객체지향언어가 아닌 언어에서는 이러한 추가적인 조건들을 반영하기가 어렵다.

그러나 객체지향언어에서는 제어자와 메소드를 이용해서 이러한 조건들을 코드에 쉽게 반영할 수 있다.

``` java
public class Time {
    private int hour;
    private int minute;
    private float second;

    public int getHour() { return hour; }
    public int getMinute() { return minute; }
    public float getSecond() { return second; }

    public void setHour(int h) {
        if (h < 0 || h > 23) return;
        hour = h;
    }

    public void setMinute(int m) {
        if (m < 0 || m > 59) return;
        minute = m;
    }

    public void setSecond(float s) {
        if (s < 0.0f || s > 59.99f) return;
        second = s;
    }
}
```

제어자를 이용해서 변수의 값을 직접 변경하지 못하도록 하고 대신 메소드를 통해서 값을 변경하도록 작성하였다. 값을 변경할 때 지정된 값의 유효성을 조건문으로 점검한 다음에 유효한 값일 경우에만 변경한다.