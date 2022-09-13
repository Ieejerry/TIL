Chapter 6. 객체지향 프로그래밍1

# 3. 변수와 메소드

</br>

## 3.1 선언위치에 따른 변수의 종류

변수는 클래스변수, 인스턴스변수, 지역변수 모두 세 종류가 있다. 변수의 종류를 결정짓는 중요한 요소는 '변수의 선언된 위치'이므로 변수의 종류를 파악하기 위해서는 변수가 어느 영역에 선언되었는지를 확인하는 것이 중요하다. 멤버변수를 제외한 나머지 변수들은 모두 지역변수이며, 멤버변수 중 `static`이 붙은 것은 클래스변수, 붙지 않은 것은 인스턴스변수이다.

아래 그림에는 모두 3개의 int형 변수가 선언되어 있는데, `iv`와 `cv`는 클래스 영역에 선언되어있으므로 멤버변수이다. 그 중 `cv`는 키워드 `static`과 함께 선언되어 있으므로 클래스 변수이며, `iv`는 인스턴스변수이다. 그리고 `lv`는 메소드인 `method()`의 내부, 즉 '메소드 영역'에 선언되어 있으므로 지역변수이다.

![image](https://ifh.cc/g/pDJr9H.png)

![image](https://ifh.cc/g/G9stOj.png)

1. 인스턴스변수(instance variable)

클래스 영역에 선언되며, 클래스의 인스턴스를 생성할 때 만들어진다. 그렇기 때문에 인스턴스 변수의 값을 읽어 오거나 저장하기 위해서는 먼저 인스턴스를 생성해야한다.

인스턴스는 독립적인 저장공간을 가지므로 서로 다른 값을 가질 수 있다. 인스턴스마다 고유한 상태를 유지해야하는 속성의 경우, 인스턴스변수로 선언한다.

2. 클래스변수(class variable)

클래스 변수를 선언하는 방법은 인스턴스변수 앞에 `static`을 붙이기만 하면 된다. 인스턴스마다 독립적인 저장공간을 갖는 인스턴스변수와는 달리, 클래스변수는 모든 인스턴스가 공통된 저장공간(변수)를 공유하게 된다. 한 클래스의 모든 인스턴스들이 공통적인 값을 유지해야하는 속성의 경우, 클래스변수로 선언해야 한다.

클래스 변수는 인스턴스변수와 달리 인스턴스를 생성하지 않고도 언제라도 바로 사용할 수 있다는 특징이 있으며, '클래스이름.클래스변수'와 같은 형식으로 사용한다.

클래스가 메모리에 '로딩(loading)'될 때 생성되어 프로그램이 종료될 때 까지 유지되며, `public`을 앞에 붙이면 같은 프로그램 내에서 어디서나 접근할 수 있는 '전역변수(global variable)'의 성격을 갖는다.

> 참조변수의 선언이나 객체의 생성과 같이 클래스의 정보가 필요할 때, 클래스는 메모리에 로딩된다.

3. 지역변수(local variable)

메소드 내에 선언되어 메소드 내에서만 사용 가능하며, 메소드가 종료되면 소멸되어 사용할 수 없게 된다. for문 또는 while문의 블럭 내에 선언된 지역변수는, 지역변수가 선언된 블럭{} 내에서만 사용 가능하며, 블럭{}을 벗어나면 소멸되어 사용할 수 없게 된다.

</br>

## 3.2 클래스변수와 인스턴스변수

클래스변수와 인스턴스변수의 차이를 이해하기 위한 예로 카드 게임에 사용되는 카드를 클래스로 정의해보겠다.

카드 클래스를 작성하기 위해서는 먼저 카드를 분석해서 속성과 기능을 알아내야 한다. 속성으로는 카드의 무늬, 숫자, 폭, 높이 정도를 생각할 수 있다.

``` java
class Card {
    String kind;    // 무늬
    int number;     // 숫자

    static int width = 100;     // 폭
    static int height = 250;    // 높이
}
```

각 `Card`인스턴스는 자신만의 무늬(kind)와 숫자(number)를 유지하고 있어야 하므로 이들을 인스턴스변수로 선언하였고, 각 카드의 폭(width)과 높이(height)는 모든 인스턴스가 공통적으로 같은 값을 유지해야하므로 클래스변수로 선언하였다.

카드의 폭을 변경해야할 필요가 있을 경우, 모든 카드의 `width`값을 변경하지 않고 한 카드의 `width`값만 변경해도 모든 카드의 `width`값이 변경된다.

예제 6-5 / ch6 / CardTest.java
``` java
public class CardTest {

	public static void main(String[] args) {
		System.out.println("Card.width = " + Card.width);
		System.out.println("Card.height = " + Card.height);
		
		Card c1 = new Card();
		c1.kind = "Heart";
		c1.number = 7;
		
		Card c2 = new Card();
		c2.kind = "Spade";
		c2.number = 4;
		
		System.out.println("c1은 " + c1.kind + ", " + c1.number + "이며, 크기는 (" + c1.width + ", " + c1.height + ")");
		System.out.println("c2은 " + c2.kind + ", " + c2.number + "이며, 크기는 (" + c2.width + ", " + c2.height + ")");
		System.out.println("c1의 width와 height를 각각 50, 80으로 변경합니다.");
		c1.width = 50;
		c1.height = 80;
		
		System.out.println("c1은 " + c1.kind + ", " + c1.number + "이며, 크기는 (" + c1.width + ", " + c1.height + ")");
		System.out.println("c2은 " + c2.kind + ", " + c2.number + "이며, 크기는 (" + c2.width + ", " + c2.height + ")");
	}

}

class Card {
	String kind;
	int number;
	static int width = 100;
	static int height = 250;
}
```

```
Card.width = 100
Card.height = 250
c1은 Heart, 7이며, 크기는 (100, 250)
c2은 Spade, 4이며, 크기는 (100, 250)
c1의 width와 height를 각각 50, 80으로 변경합니다.
c1은 Heart, 7이며, 크기는 (50, 80)
c2은 Spade, 4이며, 크기는 (50, 80)
```

`Card`클래스의 클래스변수(static변수)인 `width`, `height`는 `Card`클래스의 인스턴스를 생성하지 않고도 '클래스이름.클래스변수'와 같은 방식으로 사용할 수 있다.

`Card`인스턴스인 `c1`과 `c2`는 클래스변수인 `width`와 `height`를 공유하기 때문에, `c1`의 `width`와 `height`를 변경하면 `c2`의 `width`와 `height`값도 바뀐 것과 같은 결과를 얻는다.

`Card.width`, `c1.width`, `c2.width`는 모두 같은 저장공간을 참조하므로 항상 같은 값을 갖게 된다.

클래스변수를 사용할 때는 `Card.width`와 같이 '클래스이름.클래스변수'의 형태로 하는 것이 좋다. 참조변수 `c1`, `c2`를 통해서도 클래스변수를 사용할 수 있지만 이렇게 하면 클래스변수를 인스턴스변수로 오해하기 쉽기 때문이다.

> **인스턴스변수는 인스턴스가 생성될 때마다 생성되므로 인스턴스마다 각기 다른 값을 유지할 수 있지만, 클래스 변수는 모든 인스턴스가 하나의 저장공간을 공유하므로, 항상 공통된 값을 갖는다.**

</br>

## 3.3 메소드

'메소드(method)'는 특정 작업을 수행하는 일련의 문장들을 하나로 묶은 것이다. 기본적으로 수학의 함수와 유사하며, 어떤 값을 입력하면 이 값으로 작업을 수행해서 결과를 반환한다.

> 수학의 함수와 달리 메소드는 입력값 또는 출력값(결과값)이 없을 수도 있으며, 심지어는 입력값과 출력값이 모두 없을 수도 있다.

그저 메소드가 작업을 수행하는데 필요한 값만 넣고 원하는 결과를 얻으면 될 뿐, 이 메소드가 내부적으로 어떤 과정을 거쳐 결과를 만들어내는지 전혀 몰라도 된다. 즉, 메소드에 넣을 값(입력)과 반환하는 결과(출력)만 알면 되는 것이다. 그래서 메소드를 내부가 보이지 않는 '블랙박스(black box)'라고도 한다.

### 메소드를 사용하는 이유

1. 높은 재사용성(reusability)

한 번 만들어 놓은 메소드는 몇 번이고 호출할 수 있으며, 다른 프로글매에서도 사용이 가능하다.

2. 중복된 코드의 제거

반복되는 문장들 대신 메소드를 호출하는 한 문장으로 대체할 수 있다. 그러면, 전체 소스 코드의 길이도 짧아지고, 변경사항이 발생했을 때 수정해야할 코드의 양이 줄어들어 오류가 발생할 가능성도 함께 줄어든다.

3. 프로그램의 구조화

큰 규모의 프로그램에서는 문장들을 작업단위로 나눠서 여러 개의 메소드에 담아 프로그램의 구조를 단순화시키는 것이 필수적이다. 예를 들어 예제 5-10을 작업단위로 나누어서 메소드로 만들면, `main`메소드가 아래와 같이 간단해 진다.

``` java
public static void main(String[] args) {
    int[] numArr = new int[10];

    initArr(numArr);    // 1. 배열을 초기화
    printArr(numArr);   // 2. 배열을 출력
    sortArr(numArr);    // 3. 배열을 정렬
    printArr(numArr);   // 4. 배열을 출력
}
```

이처럼 `main`메소드는 프로그램의 전체 흐름이 한눈에 들어올 정도로 단순하게 구조화하는 것이 좋다. 그래야 나주에 프로글매에 문제가 발생해도 해당 부분을 쉽게 찾아서 해결할 수 있다.

처음에 프로그램을 설계할 때 내용이 없는 메소드를 작업단위로 만들어 놓고, 하나씩 완성해가는 것도 프로그램을 구조화하는 좋은 방법이다.

</br>

## 3.4 메소드의 선언과 구현

메소드는 크게 두 부분, '선언부(header, 머리)'와 '구현부(body, 몸통)'로 이루어져 있다. 메소드를 정의한다는 것은 선언부와 구현부를 작성하는 것을 뜻하며 다름과 같은 형식으로 메소드를 정의한다.

![image](https://ifh.cc/g/RH5QoJ.png)

### 메소드 선언부(method declaration, method header)

메소드 선언부는 '메소드의 이름'과 '매개변수 선언', 그리고 '반환타입'으로 구성되어 있으며, 메소드가 작업을 수행하기 위해 어떤 값들을 필요로 하고 작업의 결과로 어떤 타입의 값을 반환하는지에 대한 정보를 제공한다.

예를 들어 아래의 정의된 메소드 `add`는 두 개의 정수를 입력받아서, 두 값을 더한 결과(int타입의 값)를 반환한다.

![image](https://ifh.cc/g/9zCFJS.png)

메소드의 선언부는 후에 변경사항이 발생하지 않도록 신중히 작성해야한다. 메소드의 선언부를 변경하게 되면, 그 메소드가 호출되는 모든 곳도 같이 변경해야 하기 때문이다.

### 매개변수 선언(parameter declaration)

매개변수는 메소드가 작업을 수행하는데 필요한 값들(입력)을 제공받기 위한 것이며, 필요한 값의 개수만큼 변수를 선언하며 각 변수 간의 구분은 쉼표','를 사용한다. 한 가지 주의할 점은 일반적인 변수선언과 달리 두 변수의 타입이 같아도 변수의 타입을 생략할 수 없다.

``` java
int add(int x, int y) { ... }   // OK.
int add(int x, y) { ... }       // 에러. 매개변수 y의 타입이 없다.
```

선언할 수 있는 매개변수의 개수는 거의 제한이 없지만, 만일 입력해야 할 값의 개수가 많은 경우에는 배열이나 참조변수를 사용하면 된다. 만일 값을 전혀 입력받을 필요가 없다면 괄호()안에 아무 것도 적지 않는다.

> 매겨변수도 메소드 내에 선언된 것으로 간주되므로 '지역변수(local variable)'이다.

### 메소드의 이름(method name)

메소드의 이름도 변수의 명명규칙대로 작성하면 된다. 메소드는 특정 작업을 수행하므로 메소드의 이름은 'add'처럼 동사인 경우가 많으며, 이름만으로도 메소드의 기능을 쉽게 알 수 있도록 함축적이면서도 의미있는 이름을 짓도록해야 한다.

### 반환타입(retrun type)

메소드의 작업수행 결과(출력)인 '반환값(return value)'의 타입을 적는다. 반환값이 없는 경우 반환타입으로 `void`를 적어야 한다.

### 메소드의 구현부(method body, 메소드 몸통)

메소드의 선언부 다음에 오는 괄호{}를 '메소드의 구현부'라고 하는데, 여기에 메소드를 호출했을 때 수행될 문장들을 넣는다.

### return문

메소드의 반환타입이 `void`가 아닌 경우, 구현부 {}안에 'retrun 반환값;'이 반드시 포함되어 있어야 한다. 이 문장은 작업을 수행한 결과인 반환값을 호출한 메소드로 전달하는데, 이 값의 타입은 반환타입과 **일치하거나 적어도 자동 형변환이 가능한 것**이어야 한다.

여러 개의 변수를 선언할 수 있는 매개변수와 달리 `return`문은 단 하나의 값만 반환할 수 있는데, 메소드로의 입력(매개변수)은 여러 개일 수도 있어도 출력(반환값)은 최대 하나만 허용한다.

![image](https://ifh.cc/g/G5fnH9.png)

위의 코드에서 `return result;`는 변수 `result`에 저장된 값을 호출한 메소드로 반환한다. 변수 `result`의 타입이 int이므로 메소드 `add`의 반환타입이 일치하는 것을 알 수 있다.

### 지역변수(local variable)

메소드 내에 선언된 변수들은 그 메소드 내에서만 사용할 수 있으므로 서로 다른 메소드라면 같은 이름의 변수를 선언해도 된다. 이처럼 메소드 내에 선언되 변수를 '지역변수(local variable)'라고 한다.

> 매개변수도 메소드 내에 선언된 것으로 간주되므로 지역변수이다.

</br>

## 3.5 메소드 호출

메소드를 정의했어도 호출되지 않으면 아무 일도 일어나지 않는다. 메소드를 호출해야만 구현부{}의 문장들이 수행된다. 메소드를 호출하는 방법은 다음과 같다.

> main메소드는 프로그램 실행 시 OS에 의해 자동적으로 호출된다.

``` java
메소드이름(값1, 값2, ...);  // 메소드를 호출하는 방법

print99danAll();        // void print99danAll()을 호출
int result = add(3, 5); // int add(int x, int y)를 호출하고, 결과를 result에 저장
```

### 인자(argument)와 매개변수(parameter)

메소드를 호출할 때 괄호()안에 지정해준 값들을 '인자(argument)' 또는 '인수'라고 하는데, 인자의 개수와 순서는 호출된 메소드에 선언된 매개변수와 일치해야 한다. 그리고 인자는 메소드가 호출되면서 매개변수에 대입되므로, 인자의 타입은 매개변수의 타입과 일치하거나 자동 형변환이 가능한 것이어야 한다.

![image](https://ifh.cc/g/XVzblq.png)

만일 아래와 같이 메소드에 선언된 매개변수의 개수보다 많은 값을 괄호()에 넣거나 타입이 다른 값을 넣으면 컴파일러가 에러를 발생시킨다.

``` java
int result = add(1, 3, 3);      // 에러. 메소드에 선언된 매개변수의 개수가 다름
int result = add(1.0, 2.0);     // 에러. 메소드에 선언된 매개변수의 타입이 다름
```

반환타입이 `void`가 아닌 경우, 메소드가 작업을 수행하고 반환한 값을 대입연산자로 변수에 저장하는 것이 보통이지만, 저장하지 않아도 문제가 되지 않는다.

``` java
int result = add(3, 5); // int add(int x, int y)의 호출결과를 result에 저장
add(3, 5);              // OK. 메소드 add가 반환한 결과를 사용하지 않아도 된다.
```

### 메소드의 실행흐름

같은 클래스 내의 메소드끼리는 참조변수를 사용하지 않고도 서로 호출이 가능하지만 `static`메소드는 같은 클래스 내의 인스턴스 메소드를 호출할 수 없다.

다음은 두 개의 값을 매개변수로 받아서 사칙연산을 수행하는 4개의 메소드를 가진 `MyMath`클래스를 정의한 것이다.

``` java
class MyMath {
    long add(long a, long b) {
        long result = a + b;
        return result;
    //  return a + b;   // 위의 두 줄을 이와 같이 한 줄로 간단히 할 수 있다.    
    }
    long subtract(long a, long b) { return a - b; }
    long multiply(long a, long b) { return a * b; }
    double divide(double a, double b) { return a / b; }
}
```

`MyMath`클래스의 `add(long a, long b)`를 호출하기 위해서는 먼저 `MyMath mm = new MyMath();`와 같이 해서, `MyMath`클래스의 인스턴스를 생성한 다음 참조변수 `mm`을 통해야한다.

![image](https://ifh.cc/g/tGg4hx.png)

① `main`메소드에서 메소드 `add`를 호출한다. 호출시 지정한 1L과 2L이 메소드 `add`의 매개변수 `a`, `b`에 각각 복사(대입)된다.   
② 메소드 `add`의 괄호{}안에 있는 문장들이 순서대로 수행된다.   
③ 메소드 `add`의 모든 문장이 실행되거나 `return`문을 만나면, 호출한 메소드(main메소드)로 되돌아와서 이후의 문장들을 실행한다.

메소드가 호출되면 지금까지 실행 중이던 메소드는 실행을 잠시 멈추고 호출된 메소드의 문장들이 실행된다. 호출된 메소드의 작업이 모두 끝나면, 다시 호출한 메소드로 돌아와 이후의 문장들을 실행한다.

위의 그림에서 편의상 메소드 `add`의 호출결과가 바로 `value`에 저장되는 것처럼 그렸지만, 사실은 호출한 자리를 반환값이 대신하고 대입연산자에 의해 이 값이 변수 `value`에 저장된다.

``` java
    long value = add(1L, 2L);
→   long value = 3L;
```

`add`메소드의 매개변수의 타입이 long이므로 long으로 자동 형변환이 가능한 값을 지정해야 한다. 호출시 매개변수로 지정된 값은 메소드의 매개변수로 복사된다. 위의 코드에서는 1L과 2L의 값이 long타입의 매개변수 `a`와 `b`에 각각 복사된다.

메소드는 호출시 넘겨받은 값으로 연산을 수행하고 그 결과를 반환하면서 종료된다. 반환된 값은 대입연산자에 의해서 변수 `vaule`에 저장된다. 메소드의 결과를 저장하기 위한 변수 `value` 역시 반환값과 같은 타입이거나 반환값이 자동 형변환되어 저장될 수 있는 타입이어야 한다.

예제 6-6 / ch6 / MyMathTest.java
``` java
public class MyMathTest {

	public static void main(String[] args) {
		MyMath mm = new MyMath();
		long result1 = mm.add(5L, 3L);
		long result2 = mm.subtract(5L, 3L);
		long result3 = mm.multiply(5L, 3L);
		double result4 = mm.divide(5L, 3L);
		
		System.out.println("add(5L, 3L) = " + result1);
		System.out.println("subtract(5L, 3L) = " + result2);
		System.out.println("multiply(5L, 3L) = " + result3);
		System.out.println("divide(5L, 3L) = " + result4);
	}

}

class MyMath {
	long add(long a, long b) {
		long result = a + b;
		return result;
//		return a + b;	// 위의 두 줄을 이와 같이 한 줄로 간단히 할 수 있다.
	}
	
	long subtract(long a, long b) { return a - b; }
	long multiply(long a, long b) { return a * b; }
	double divide(double a, double b) {
		return a / b;
	}
}
```

```
add(5L, 3L) = 8
subtract(5L, 3L) = 2
multiply(5L, 3L) = 15
divide(5L, 3L) = 1.6666666666666667
```

사칙연산을 위한 4개의 메소드가 정의되어 있는 `MyMath`클래스를 이용한 예제이다. 이 예제를 통해서 클래스에 선언된 메소드를 어떻게 호출하는지 알 수 있다.

여기서 눈여겨봐야 할 곳은 `divide(double a, double b)`를 호출하는 부분이다. `divide`메소드에 선언된 매개변수 타입은 double형인데, 이와 다른 long형의 값인 5L과 3L을 사용해서 호출하는 것이 가능하다.

``` java
double result4 = mm.divide(5L, 3L);

double divide(double a, double b) {
    return a / b;
}
```

호출 시에 입력된 값은 메소드의 매개변수에 대입되는 것이므로, long형의 값을 double형 변수에 저장하는 것과 같이서 `double a = 5L;`을 수행 했을 때와 같이 long형의 값인 5L은 double형 값인 5.0으로 자동형변환되어 `divide`의 매개변수 `a`에 저장된다.

그래서, `divide`메소드에 두 개의 정수값(5L, 3L)을 입력하여 호출하였음에도 불구하고 연산결과가 double형의 값이 된다.

</br>

## 3.6 return문

return문은 현재 실행중인 메소드를 종료하고 호출한 메소드로 되돌아간다. 지금까지 반환값이 있을 때만 return문을 썼지만, 원래는 반환값의 유무에 관계없이 모든 메소드에는 적어도 하나의 return문이 있어야 한다. 그런데도 반환타입이 `void`인 경우, return문 없이도 아무런 문제가 없었던 이유는 컴파일러가 메소드의 마지막에 `return;`을 자동적으로 추가해주었기 때문이다.

``` java
void printGugudan(int dan) {
    for(int i = 0; i <= 9; i++) {
        System.out.printf("%d * %d = %d%n", dan, i, dan * i);
    }
//    return; // 반환 타입이 void이므로 생략가능. 컴파일러가 자동추가
}
```

그러나 반환타입이 `void`가 아닌 경우, 즉 반환값이 있는 경우, 반드시 return문이 있어야 한다. return문이 없으면 컴파일 에러(error: missing return statement)가 발생한다.

``` java
int multiply(int x, int y) {
    int result = x * y;

    return result;  // 반환 타입이 void가 아니므로 생략불가
}
```

아래의 코드는 두 값 중에서 큰 값을 반환하는 메소드이다. 이 메소드의 리턴타입이 int이고 int타입의 값을 반환하는 return문이 있지만, return문이 없다는 에러가 발생한다.

왜냐하면 if문 조건식의 결과에 따라 return문이 실행되지 않을 수도 있기 때문이다.

``` java
int max(int a, int b) {
    if(a > b) return a; // 조건식이 참일 때만 실행된다.
}
```

그래서 이런 경우에 다름과 같이 if문의 else블럭에 return문을 추가해서, 항상 결과값이 반환되도록 해야 한다.

``` java
int max(int a, int b) {
    if(a > b) return a; // 조건식이 참일 때 실행된다.
    else return b;      // 조건식이 거짓일 때 실행된다.
}
```

### 반환값(return value)

return문의 반환값으로 주로 변수가 오긴 하지만 항상 그런 것은 아니다. 아래 왼쪽의 코드는 오른쪽과 같이 간략히 할 수 있는데, 오른 쪽의 코드는 return문의 반환값으로 `x + y`라는 수식이 적혀있다. 그렇다고 해서 수식이 반환되는 것은 아니고, 이 수식을 계산한 결과가 반환된다.

![image](https://ifh.cc/g/nqCw4a.png)

### 매개변수의 유효성 검사

메소드의 구현부{}를 작성할 때, 제일 먼저 해야 하는 일이 매개변수의 값이 적절한 것인지 확인하는 것이다. 타입만 맞으면 어떤 값도 매개변수를 통해 넘어올 수 있기 때문에, 가능한 모든 경우의 수에 대해 고민하고 그에 대비한 코드를 작성해야한다.

아래에 정의된 메소드 `divide`는 매개변수 `x`를 `y`로 나눈 결과를 실수(flaot타입)로 반환하는데, 0으로 나눈 것은 금지되어 있기 때문에 계산 전에 `y`의 값이 0인지 확인해야 한다. 그래서 `y`의 값이 0이면, 나누기를 계산할 수 없으므로 return문을 이용해서 작업을 중단하고 메소드를 빠져나와야 한다. 그렇지 않으면, 나누기를 하는 문장에서 프로그램이 비정상적으로 종료된다.

``` java
float divide(int x, int y) {
    // 작업을 하기 전에 나누는 수(y)가 0인지 확인한다.
    if(y == 0) {
        System.out.println("0으로 나눌 수 없습니다.");
        return 0;   // 매개변수가 유효하지 않으므로 메소드를 종료한다.
    }

    return x / (float)y;
}
```

적절하지 않은 값이 매개변수를 통해 넘어온다면 매개변수의 값을 보정하던가, 보정하는 것이 불가능하다면 return문을 사용해서 작업을 중단하고 호출한 메소드로 되돌아가야한다.

</br>

## 3.7 JVM의 메모리 구조

응용프로그램이 실행되면, JVM은 시스템으로부터 프로그램을 수행하는데 필욯나 메모리를 할당받고, JVM은 이 메모리를 용도에 따라 여러 영역으로 나누어 관리한다.

1. 메소드 영역(method area)
- 프로그램 실행 중 어떤 클래스가 사용되면, JVM은 해당 클래스의 클래스파일(*.class)을 읽어서 분석하여 클래스에 대한 정보(클래스 데이터)를 이곳에 저장한다. 이 때, 그 클래스의 클래스변수(class variable)도 이 영역에 함께 생성된다.

2. 힙(heap)
- 인스턴스가 생성되는 공간, 프로그램 실행 중 생성되는 인스턴스는 모두 이곳에 생성된다. 즉, 인스턴스변수(instance variable)들이 생성되는 공간이다.

3. 호출스택(call stack 또는 execution stack)
- 호출스택은 메소드의 작업에 필요한 메모리 공간을 제공한다. 메소드가 호출되면, 호출스택에 호출된 메소드를 위한 메모리가 할당되며, 이 메모리는 메소드가 작업을 수행하는 동안 지역변수(매개변수 포함)들과 연산의 중간결과 등을 저장하는데 사용된다. 그리고 메소드가 작업을 마치면 할당되었던 메모리공간은 반환되어 비워진다.

각 메소드를 위한 메모리상의 작업공간은 서로 구별되며, 첫 번째로 호출된 메소드를 위한 작업공간이 호출스택의 맨 밑에 마련되고, 첫 번째 메소드 수행 중에 다른 메소드를 호출하면, 첫 번째 메소드의 바로 위에 두 번째로 호출된 메소드를 위한 공간이 마련된다.

이 때 첫 번째 메소드는 수행을 멈추고, 두 번째 메소드가 수행되기 시작한다. 두 번째로 호출된 메소드가 수행을 마치게 되면, 두 번째 메소드를 위해 제공되었던 호출스택의 메모리공간이 반환되며, 첫 번째 메소드는 다시 수행을 계속하게 된다. 첫 번째 메소드가 수행을 마치면, 역시 제공되었떤 메모리 공간이 호출스택에서 제거되며 호출스택은 완전히 비워지게 된다. 호출스택의 제일 상위에 위치하는 메소드가 현재 실행 중인 메소드이며, 나머지는 대기상태에 있게 된다.

따라서, 호출스택을 조사해 보면 메소드 간의 호출관계와 현재 수행중인 메소드가 어느 것인지 알 수 있다. 호출스택의 특징을 정리해보면 다음과 같다.

> - 메소드가 호출되면 수행에 필요한 만큼의 메모리를 스택에 할당받는다.
> - 메소드가 수행을 마치고나면 사용했던 메모리를 반환하고 스택에서 제거된다.
> - 호출스택의 제일 위에 있는 메소드가 현재 실행 중인 메소드이다.
> - 아래에 있는 메소드가 바로 위의 메소드를 호출한 메소드이다.

반환타입(return type)이 있는 메소드는 종료되면서 결과값을 자신을 호출한 메소드(caller)에게 반환한다. 대기상태에 있던 호출한 메소드(caller)는 넘겨받은 반환값으로 수행을 계속 진행하게 된다.

예제 6-7 / ch6 / CallStackTest.java
``` java
public class CallStackTest {

	public static void main(String[] args) {
		firstMethod();	// static메소드는 객체 생성없이 호출가능하다.
	}
	
	static void firstMethod() {
		secondMethod();
	}
	
	static void secondMethod() {
		System.out.println("secondMethod");
	}

}
```

```
secondMethod
```

`main()`이 `firstMethod()`를 호출하고 `firstMethod()`는 `secondMethod()`를 호출한다. 객체를 생성하지 않고도 메소들르 호출할 수 있으려면, 메소드 앞에 `static`을 붙여야 한다.

위의 예제를 실행시켰을 때, 프로그램이 수행되는 동안 호출스택의 변화를 그림과 함께 살펴보겠다.

![image](https://ifh.cc/g/kfyKFJ.png)

①~② 위의 예제를 실행시키면, JVM에 의해서 `main`메소드가 호출됨으로써 프로그램이 시작된다. 이 때, 호출스택에는 `main`메소드를 위한 메모리공간이 할당되고 `main`메소드의 코드가 수행되기 시작한다.   
③ `main`메소드에서 `firstMethod()`를 호출한 상태이다. 아직 `main`메소드가 끝난 것은 아니므로 `main`메소드는 호출스택에 대기상태로 남아있고 `firstMethod()`의 수행이 시작된다.   
④ `firstMethod()`에서 다시 `secondMehod()`를 호출했다. `firstMethod()`는 `secondMethod()`가 수행을 마칠 때까지 대기상태에 있게 된다. `secondMethod()`가 수행을 마쳐야 `firstMethod()`의 나머지 문장들을 수행할 수 있기 때문이다.   
⑤ `secondMethod()`에서 `println()`을 호출했다. `println`메소드에 의해 `secondMethod()`가 화면에 출력된다.   
⑥ `println`메소드의 수행이 완료되어 호출스택에서 사라지고 자신을 호출한 `secondMethod()`로 되돌아간다. 대기 중이던 `secondMethod()`는 `println()`을 호출한 이후부터 수행을 재개한다.   
⑦ `secondMethod()`에 더 이상 수행할 코드가 없으므로 중료되고, 자신을 호출한 `firstMethod()`로 돌아간다.   
⑧ `firstMethod()`에도 더 이상 수행할 코드가 없으므로 종료되고, 자신을 호출한 `main`메소드로 돌아간다.   
⑨ `main`메소드에도 더 이상 수행할 코드가 없으므로 종료되어, 호출스택은 완전히 비워지게 되고 프로그램은 종료된다.

예제 6-8 / ch6 / CallStackTest2.java
``` java
public class CallStackTest2 {

	public static void main(String[] args) {
		System.out.println("main(String[] args)이 시작되었음.");
		firstMethod();
		System.out.println("main(String[] args)이 끝났음.");
	}
	
	static void firstMethod() {		
		System.out.println("firstMethod()이 시작되었음.");
		secondMethod();
		System.out.println("firstMethod()이 끝났음.");
	}
	
	static void secondMethod() {
		System.out.println("secondMethod()이 시작되었음.");
		System.out.println("secondMethod()이 끝났음.");
	}

}
```

```
main(String[] args)이 시작되었음.
firstMethod()이 시작되었음.
secondMethod()이 시작되었음.
secondMethod()이 끝났음.
firstMethod()이 끝났음.
main(String[] args)이 끝났음.
```

</br>

## 3.8 기본형 매개변수와 참조형 매개변수

자바에서는 메소드를 호출할 때 매개변수로 지정한 값을 메소드의 매개변수에 복사해서 넘겨준다. 매개변수의 타입이 기본형(primitive type)일 때는 기본형 값이 복사되겠지만, 참조형(reference type)이면 인스턴스의 주소가 복사된다.

메소드의 매개변수를 기본형으로 선언하면 단순히 저장된 값만 얻지만, 참조형으로 선언하면 값이 저장된 곳의 주소를 알 수 있기 때문에 값을 읽어 오는 것은 물론 값을 변경하는 것도 가능하다.

> **기본형 매개변수** 변수의 값을 읽기만 할 수 있다.(read only)
> **참조형 매개변수** 변수의 값을 읽고 변경할 수 있다.(read & write)

예제 6-9 / ch6 / PrimitiveParamEx.java
``` java
class Data { int x; }

public class PrimitiveParamEx {

	public static void main(String[] args) {
		Data d = new Data();
		d.x = 10;
		System.out.println("main() : x = " + d.x);
		
		change(d.x);
		System.out.println("After change(d.x)");
		System.out.println("main() : x = " + d.x);
	}
	
	static void change(int x) {	// 기본형 매개변수
		x = 1000;
		System.out.println("change() : x = " + x);
	}

}
```

```
main() : x = 10
change() : x = 1000
After change(d.x)
main() : x = 10
```

`change`메소드에서 `main`메소드로부터 넘겨받은 `d.x`의 값을 1000으로 변경했는데도 `main`메소드에서는 `d.x`의 값이 그대로이다. 왜 이런 결과가 나오는지 단계별로 그림을 보겠다.

![image](https://ifh.cc/g/w9HJ55.png)

① `change`메소드가 호출되면서 `d.x`가 `change`메소드의 매개변수 `x`에 복사됨   
② `change`메소드에서 `x`의 값을 1000으로 변경   
③ `change`메소드가 종료되면서 매개변수 `x`는 스택에서 제거됨

`d.x`의 값이 변경된 것이 아니라, `change`메소드의 매개변수 `x`의 값이 변경된 것이다. 즉, 원본이 아닌 복사본이 변경된 것이라 원본에는 아무런 영향을 미치지 못한다. 이처럼 기본형 매개변수는 변수에 저장된 값만 읽을 수만 있을 뿐 변경할 수는 없다.

예제 6-10 / ch6 / ReferenceParamEx.java
``` java
class Data { int x; }

public class ReferenceParamEx {

	public static void main(String[] args) {
		Data d = new Data();
		d.x = 10;
		System.out.println("main() : x = " + d.x);
		
		change(d);
		System.out.println("After change(d)");
		System.out.println("main() : x = " + d.x);
	}
	
	static void change(Data d) {	// 참조형 매개변수
		d.x = 1000;
		System.out.println("change() : x = " + d.x);
	}
}
```

```
main() : x = 10
change() : x = 1000
After change(d)
main() : x = 1000
```

이전 예제와 달리 `change`메소드를 호출한 후에 `d.x`의 값이 변경되었다. `change`메소드의 매개변수가 참조형이라서 값이 아니라 '값이 저장된 주소'를 `change`메소드에게 넘겨주었기 때문에 값을 읽어오는 것뿐만 아니라 변경하는 것도 가능하다.

![image](https://ifh.cc/g/bYMnLH.png)

① `change`메소드가 호출되면서 참조변수 `d`의 값(주소)이 매개변수 `d`에 복사됨.   
이제 매개변수 `d`에 저장된 주소값으로 `x`에 접근이 가능   
② `change`메소드에서 매개변수 `d`로 `x`의 값을 1000으로 변경   
③ `change`메소드가 종료되면서 매개변수 `d`는 스택에서 제거됨

이전 예제와 달리, `change`메소드의 매개변수를 참조형으로 선언했기 때문에, `x`의 값이 아닌 주소가 매개변수 `d`에 복사되었다. 이제 `main`메소드의 참조변수 `d`와 `change`메소드의 참조변수 `d`는 같은 객체를 가리키게 된다. 그래서 매개변수 `d`로 `x`의 값을 읽는 것과 변경하는 것이 모두 가능한 것이다.

예제 6-11 / ch6 / ReferenceParamEx2.java
``` java
public class ReferenceParamEx2 {

	public static void main(String[] args) {
		int[] x = { 10 }; // 크기가 1인 배열. x[0] = 10;
		System.out.println("main() : x = " + x[0]);
		
		change(x);
		System.out.println("After change(x)");
		System.out.println("main() : x = " + x[0]);
	}
	
	static void change(int[] x) {	// 참조형 매개변수
		x[0] = 1000;
		System.out.println("change() : x = " + x[0]);
	}
}
```

```
main() : x = 10
change() : x = 1000
After change(x)
main() : x = 1000
```

이전의 참조형 매개변수 예제를 `Data`클래스의 인스턴스 대신 길이가 1인 배열 `x`를 사용하도록 변경한 것이다. 배열도 객체와 같이 참조변수를 통해 데이터가 저장된 공간에 접근한다. 이전 예제 `Data`클래스 타입의 참조변수 `d`와 같이 변수 `x`도 int배열타입의 참조변수이기 때문에 같은 결과를 얻는다.

예제 6-12 / ch6 / ReferenceParamEx3.java
``` java
public class ReferenceParamEx3 {

	public static void main(String[] args) {
		int[] arr = new int[] { 3, 2, 1, 6, 5, 4 };
		
		printArr(arr);	// 배열의 모든 요소를 출력
		sortArr(arr);	// 배열의 정렬
		printArr(arr);	// 정렬 후 결과를 출력
		System.out.println("sum = " + sumArr(arr));	// 배열의 총합을 출력
	}
	
	static void printArr(int[] arr) {	// 배열의 모든 요소를 출력
		System.out.print("[");
		
		for(int i : arr) System.out.print(i + ",");
		System.out.println("]");
	}

	static int sumArr(int[] arr) {	// 배열의 모든 요소의 합을 반환
		int sum = 0;
		
		for(int i = 0; i < arr.length; i++) sum += arr[i];
		return sum;
	}
	
	static void sortArr(int[] arr) {	// 배열을 오름차순으로 정렬
		for(int i = 0; i < arr.length; i++)
			for(int j = 0; j < arr.length - 1 - i; j++)
				if(arr[j] > arr[j + 1]) {
					int tmp = arr[j];
					arr[j] = arr[j + 1];
					arr[j + 1] = tmp;
				}
	}	// sortArr(int[] arr)
}
```

```
[3,2,1,6,5,4,]
[1,2,3,4,5,6,]
sum = 21
```

메소드로 배열을 다루는 여러 가지 방법을 보여주는 예제이다. 매개변수의 타입이 배열이니까. 참조형 매개변수이다. 그래서 `sortArr`메소드에서 정렬한 것이 원래의 배열에 영향을 미친다.

예제 6-13 / ch6 / ReturnTest.java
``` java
public class ReturnTest {

	public static void main(String[] args) {
		ReturnTest r = new ReturnTest();
		
		int result = r.add(3, 5);
		System.out.println(result);
		
		int[] result2 = {0};	// 배열을 생성하고 result2[0]의 값을 0으로 초기화
		r.add(3, 5, result2);	// 배열을 add메소드의 매개변수로 전달
		System.out.println(result2[0]);
	}
	
	int add(int a, int b) {
		return a + b;
	}
	
	void add(int a, int b, int[] result) {
		result[0] = a + b;	// 매개변수로 넘겨받은 배열에 연산결과를 저장
	}

}
```

```
8
8
```

이 예제는 반환값이 있는 메소드를 반환값이 없는 메소드로 바꾸는 방법을 보여준다.

![image](https://ifh.cc/g/1k1hB4.png)

메소드는 단 하나의 값만을 반환할 수 있지만 이것을 응용하면 여러 개의 값을 반환받는 것과 같은 효과를 얻을 수 있다.

</br>

## 3.9 참조형 반환타입

매개변수뿐만 아니라 반환타입도 참조형이 될 수 있다. 반환타입이 참조형이라는 것은 반환하는 값의 타입이 참조형이라는 얘긴데, 모든 참조형 타입의 값은 '객체의 주소'이므로 그저 정수의 값이 반환되는 것이다.

예제 6-14 / ch6 / ReferenceReturnEx.java
``` java
public class ReferenceReturnEx {

	public static void main(String[] args) {
		Data d = new Data();
		d.x = 10;
		
		Data d2 = copy(d);
		System.out.println("d.x = " + d.x);
		System.out.println("d2.x = " + d2.x);
	}
	
	static Data copy(Data d) {
		Data tmp = new Data();
		tmp.x = d.x;
		
		return tmp;
	}
}
```

```
d.x = 10
d2.x = 10
```

`copy`메소드는 새로운 객체를 생성한 다음에, 매개변수로 넘겨받은 객체에 저장된 값을 복사해서 반환한다. 반환하는 값이 `Data`객체의 주소이므로 반환 타입이 `Data`인 것이다.

``` java
static Data copy(Data d) {
    Data tmp = new Data();  // 새로운 객체 tmp를 생성한다.
    tmp.x = d.x;            // d.x의 값을 tmp.x에 복사한다.

    return tmp;             // 복사한 객체의 주소를 반환한다.
}
```

이 메소드의 반환타입이 `Data`이므로, 호출결과를 저장하는 변수의 타입 역시 `Data`타입의 참조변수이어야 한다.

``` java
Data d2 = copy(d);  // static Data copy(Data d)
```

`copy`메소드 내에서 생성한 객체를 `main`메소드에서 사용할 수 있으려면, 이렇게 새로운 객체의 주소를 반환해줘야 한다. 그렇지 않으면, `copy`메소드가 종료되면서 새로운 객체의 참조가 사라지기 때문에 더 이상 이 객체를 사용할 방법이 없다.

`copy`메소드가 호출된 직후부터 종료까지의 과정을 단계별로 살펴보면 다음과 같다.

![image](https://ifh.cc/g/z770gz.png)

① `copy`메소드를 호출하면서 참조변수 `d`의 값이 매개변수 `d`에 복사된다.   
② 새로운 객체를 생성한 다음, `d.x`에 저장된 값을 `tmp.x`에 복사한다.   
③ `copy`메소드가 종료되면서 반환한 `tmp`의 값은 참조변수 `d2`에 저장된다.   
④ `copy`메소드가 종료되어 `tmp`가 사라졌지만, `d2`로 새로운 객체를 다룰 수 있다.

> **"반환타입이 '참조형'이라는 것은 메소드가 '객체의 주소'를 반환한다는 것을 의미한다."**

</br>

## 3.10 재귀호출(recursive call)

메소드의 내부에서 메소드 자신을 다시 호출하는 것을 '재귀호출(recursive call)'이라 하고, 재귀호출을 하는 메소드를 '재귀 메소드'라 한다.

``` java
void method() {
    method();   // 재귀호출. 메소드 자신을 호출한다.
}
```

'메소드 호출'이라는 것이 그저 특정 위치에 저장되어 있는 명령들을 수행하는 것일 뿐이다.

호출된 메소드는 '값에 의한 호출(call by value)'을 통해, 원래의 값이 아닌 복사된 값으로 작업하기 때문에 호출한 메소드와 관계없이 독립적인 작업수행이 가능하다.

그런데 위의 코드처럼 오로지 재귀호출뿐이면, 무한히 자기 자신을 호출하기 때문에 무한반복에 빠지게 된다. 무한반복문이 조건문과 함께 사용되어야 하는 것처럼, 재귀호출도 조건문이 필수적으로 따라다닌다.

``` java
void method(int n) {
    if(n == 0) return;  // n의 값이 0일 때, 메소드를 종료한다.
    System.out.println(n);

    method(--n);    // 재귀호출. method(int n)을 호출
}
```

이 코드는 매개변수 `n`을 1씩 감소시켜가면서 재귀호출을 하다가 `n`의 값이 0이 되면 재귀호출을 중단하게 된다. 재귀호출은 반복문과 유사한 점이 많으며, 대부분의 재귀호출은 반복문으로 작성하는 것이 가능하다. 위의 코드를 반복문으로 작성하면 다음의 오른쪽 코드와 같다.

![image](https://ifh.cc/g/ga82Dx.png)

반복문은 그저 같은 문장을 반복해서 수행하는 것이지만, 메소드를 호출하는 것은 반복문보다 몇 가지 과정, 예를 들면 매개변수 복사와 종료 후 복귀할 주소저장 등, 이 추가로 필요하기 때문에 반복문보다 재귀호출의 수행시간이 더 오래 걸린다.

재귀호출을 굳이 반복문대신 사용하는 이유는 바로 재귀호출이 주는 논리적 간결함 때문이다. 몇 겹의 반복문과 조건문으로 복잡하게 작성된 코드가 재귀호출로 작성하면 보다 단순한 구조로 바뀔 수도 있다. 아무리 효율적이라도 알아보기 힘들게 작성하는 것보다 다소 비효율적이더라도 알아보기 쉽게 작성하는 것이 논리적 오류가 발생할 확률도 줄어들고 나중에 수정하기도 좋다.

어떤 작업을 반복적으로 처리해야한다면, 먼저 반복문으로 작성해보고 너무 복잡하면 재귀호출로 간단히 할 수 없는지 고민해볼 필요가 있다. 재귀호출은 비효율적이므로 재귀호출에 드는 비용보다 재귀호출의 간결함이 주는 이득이 추분히 큰 경우에만 사용해야 한다.

대표적인 재귀호출의 예는 팩토리얼(factorial)을 구하는 것이다. 팩토리얼은 한 숫자가 1일 될 때까지 1씩 감소시켜가면서 계속해서 곱해 나가는 것인데, n!(n은 양의 정수)과 같이 표현한다. 예를 들면, '5! = 5 * 4 * 3 * 2 * 1 = 120'이다.

팩토리얼을 수학적 메소드로 표현하면 아래와 같이 표현할 수 있다.

```
f(n) = n * f(n - 1), 단 f(1) = 1
```

예제 6-15 / ch6 / FactorialTest.java
``` java
public class FactorialTest {

	public static void main(String[] args) {
		int result = factorial(4);
		
		System.out.println(result);
	}

	static int factorial(int n) {
		int result = 0;
		
		if(n == 1) result = 1;
		else result = n * factorial(n - 1);	// 다시 메소드 자신을 호출한다.
		return result;
	}
}
```

```
24
```

위 예제는 팩토리얼을 계산하는 메소드를 구현하고 테스트하는 것이다. `factorial`메소드가 `static`메소드이므로 인스턴스를 생성하지 않고 직접 호출할 수 있다. 그리고 `main`메소드와 같은 클래스에 있기 때문에 `static`메소드를 호출할 때 클래스이름을 생략하는 것이 가능하다. 그래서 `FactorialTest.factorial(4)`대신 `factorial(4)`와 같이 하였다.

``` java
static int factorial(int n) {
    if(n == 1) return 1;
    return n * factorial(n - 1);
}
```

만일 매개변수 `n`의 값이 3이라면, `n`대신 3을 직접 대입해보자. 오른쪽의 코드처럼 된다.

![image](https://ifh.cc/g/JBKL1V.png)

이 방법을 이용해서 `main`메소드에서 `factorial(1)`을 호출했을 때의 실행과정을 살표보겠다. 아래의 그림은 매개변수 `n` 대신 1을 대입한 것이다.

![image](https://ifh.cc/g/aPkH5v.png)

if문의 조건식이 참이 되어 1을 반환하기 때문에, 재귀호출이 일어나기도 전에 `factorial`메소드는 종료된다. 그리고 `result`에는 `factorial(1)`의 반환값인 1이 저장된다.

이번엔 `factorial(2)`를 호출했을 때의 실행과정을 살펴보겠다. 매개변수의 값이 1이 아니므로 조건식이 거짓이 되어 그 다음 문장인 `return 2 * factorial(1);`이 수행되고, 이 식을 계산하는 과정에서 다시 `factorial(1)`이 호출된다.

① `fatorial(2)`를 호출하면서 매개변수 `n`에 2가 복사된다.   
② `return 2 * factorial(1);`을 계산하려면 `factorial(1)`을 호출한 결과가 필요하다. 그래서 `factorial(1)`이 호출되고 매개변수 `n`에 1이 복사된다.   
③ if문의 조건식이 참이므로 1을 반환하면서 메소드는 종료된다. 그리고 `factorial(1)`을 호출한 곳으로 되돌아간다.   
④ 이제 `factorial(1)`의 결과값인 1을 얻었으므로, return문이 다음의 과정으로 계산된다.

``` java
    return 2 * factorial(1);
→   return 2 * 1;
→   return 2;
```

![image](https://ifh.cc/g/2xTWL2.png)

`factorial(2)`는 종료되면서 결과값 2를 반환하고, 이 값은 변수 `result`에 저장된다.

``` java
    int result = factorial(2);
→   int result = 2;
```

그런데 만일 `factorial`메소드의 매개변수 `n`의 값이 0이면 if문의 조건식이 절대 참이 될 수 업식 때문에 계속해서 재귀호출만 일어날 뿐 메소드가 종료되지 않으므로 스택에 계속 데이터가 쌓여만 간다.

어느 시점에 이르러서는 결국 스택의 저장한계를 넘게 되고, '스택오버플로우 에러(StackOverflow Error)'가 발생한다. 매개변수 `n`의 값이 100,000과 같이 큰 경우에도 마찬가지다.

이처럼 어떤 값이 들어와도 에러없이 처리되는 견고한 코드를 작성해야 한다. 그래서 '매개변수의 유효성검사'가 중요하다.

``` java
static int factorial(int n) {
    if(n <= 0 || n > 12) return -1; // 매개변수 n의 유효성 검사를 추가
    if(n == 1) return 1;

    return n * factorial(n - 1);
}
```

매개변수 `n`의 상한값을 12로 정한 이유는 13!의 값이 메소드 `factorial`의 반환타입인 int의 최대값(약20억)보다 크기 때문이다. 만일 그 이상의 값을 구하고 싶으면 반환타입을 int보다 큰 타입으로 변경하면 된다.

참고로 재귀메소드 `factorial`을 반복문으로 작성하면 다음과 같다.

![image](https://ifh.cc/g/LtjRm7.png)

while문으로 작성한 오른쪽의 코드는 왼쪽의 재귀호추과 달리 많은 수의 반복에도 '스택오버플로우 에러'와 같은 메모리 부족문제를 겪지 않을 뿐만 아니라 속도도 빠르다.

예제 6-16 / ch6 / FactorialTest2.java
``` java
public class FactorialTest2 {
	static long factorial(int n) {
		if(n <= 0 || n > 20) return -1;	// 매개변수의 유효성 검사.
		if(n <= 1) return 1;
		
		return n * factorial(n - 1);
	}
	
	public static void main(String[] args) {
		int n = 21;
		long result = 0;
		
		for(int i = 1ㅌ; i <= n; i++) {
			result = factorial(i);
			
			if(result == -1) {
				System.out.printf("유효하지 않은 값입니다.(0<n<=20):%d%n", n);
				break;
			}
			
			System.out.printf("%2d != %20d%n", i, result);
		}
	}	// main의 끝
}
```

```
 1 !=                    1
 2 !=                    2
 3 !=                    6
 4 !=                   24
 5 !=                  120
 6 !=                  720
 7 !=                 5040
 8 !=                40320
 9 !=               362880
10 !=              3628800
11 !=             39916800
12 !=            479001600
13 !=           6227020800
14 !=          87178291200
15 !=        1307674368000
16 !=       20922789888000
17 !=      355687428096000
18 !=     6402373705728000
19 !=   121645100408832000
20 !=  2432902008176640000
유효하지 않은 값입니다.(0<n<=20):21
```

이전 예제 6-15에 매개변수의 유효성을 검사하는 코드를 추가해서 메소드 `factorial`의 매개변수 `n`이 음수거나 20보다 크면 -1을 반환하도록 하였다.

예제 6-17 / ch6 / MainTest.java
``` java
public class MainTest {

	public static void main(String[] args) {
		main(null);		// 재귀호출. 자기 자신을 다시 호출한다.
	}

}
```

```
Exception in thread "main" java.lang.StackOverflowError
	at MainTest.main(MainTest.java:5)
	at MainTest.main(MainTest.java:5)
    ...
	at MainTest.main(MainTest.java:5)
	at MainTest.main(MainTest.java:5)
```

`main`메소드 역시 자기 자신을 호출하는 것이 가능하며 아무런 조건도 없이 계속해서 자기 자신을 다시 호출하기 때문에 무한호출에 빠지게 된다.

`main`메소드가 종료되지 않고 호출스택에 계속해서 쌓이게 되므로 결국 호출스택의 메모리 한계를 넘게 되고 `StackOverflowError`가 발생하여 프로그램은 비정상적으로 종료된다.

예제 6-18 / ch6 / PowerTest.java
``` java
public class PowerTest {
	public static void main(String[] args) {
		int x = 2;
		int n = 5;
		long result = 0;
		
		for(int i = 1; i <= n; i++) {
			result += power(x, i);
		}
		
		System.out.println(result);
	}
	
	static long power(int x, int n) {
		if(n == 1) return x;
		return x * power(x, n-1);
	}
}
```

```
62
```

x<sup>1</sup>부터 x<sup>n</sup>까지의 합을 구하는 예제이다. 재귀호출을 사용하여 x<sup>n</sup>을 구하는 `power()`를 작성하였다. `x`는 2, `n`은 5로 계산했기 때문에 2<sup>1</sup>+2<sup>2</sup>+2<sup>3</sup>+2<sup>4</sup>+2<sup>5</sup>의 결과인 62가 출력되었다.

`x`의 `n`제곱을 계산하는  메소드는 다음과 같이 정의할 수 있는데, 이 메소드 역시 메소드의 정의에 자신을 포함하는 재귀 메소드이다.

``` java
f(x, n) = x * f(x, n - 1), 단 f(x, 1) = x
```

예를 들어 2의 4제곱을 구해보겠다. `x`는 2이고, `n`은 4이므로 각각을 메소드에 대입하면 다음과 같이 된다.

``` java
f(2, 4) = 2 * f(2, 3)
```

`f(2, 3)`은 `2 * f(2, 2)`이므로, 위의 식에 `f(2, 3)`대신 `2 * f(2, 2)`를 대입하면 다음과 같다.

``` java
f(2, 4) = 2 * f(2, 3)
f(2, 4) = 2 * 2 * f(2, 2)
```

같은 방식으로 반복해서 계산하면 다음과 같다. `f(2, 1)`은 2라는 것에 주의해야 한다.

``` java
    f(2, 4) = 2 * f(2, 3)
→   f(2, 4) = 2 * 2 * f(2, 2)
→   f(2, 4) = 2 * 2 * 2 * f(2, 1)
→   f(2, 4) = 2 * 2 * 2 * 2
```

</br>

## 3.12 클래스 메소드(static메소드)와 인스턴스 메소드

변수에서 그랬던 것과 같이, 메소드 앞에 `static`이 붙어 있으면 클래스 메소드이고 붙어있지 않으면 인스턴스 메소드이다.

클래스 메소드도 클래스변수처럼, 객체를 생성하지 않고도 '클래스이름.메소드이름(매개변수)'와 같은 식으로 호출이 가능하다. 반면에 인스턴스 메소드는 반드시 객체를 생성해야만 호출할 수 있다.

클래스는 '데이터(변수)와 데이터에 관련된 메소드의 집합'이므로, 같은 클래스 내에 있는 메소드와 멤버변수는 아주 밀접한 관계가 있다.

**인스턴스 메소드는 인스턴스 변수와 관련된 작업을 하는, 즉 메소드의 작업을 수행하는데 인스턴스 변수를 필요로 하는 메소드이다.** 그런데 인스턴스 변수는 인스턴스(객체)를 생성해야만 만들어지므로 인스턴스 메소드 역시 인스턴스를 생성해야만 호출할 수 있는 것이다.

반면에 메소드 중에서 **인스턴스와 관계없는(인스턴스 변수나 인스턴스 메소드를 사용하지 않는) 메소드를 클래스 메소드(static메소드)로 정의한다.**

물론 인스턴스 변수를 사용하지 않는다고 해서 반드시 클래스 메소드로 정의해야하는 것은 아니지만 특별한 이유가 없는 한 그렇게 하는 것이 일반적이다.

> 클래스 영역에 선언된 변수는 멤버변수라 한다. 멤버변수 중에 static이 붙은 것은 클래스변수(static변수), static이 붙지 않은 것은 인스턴스변수라 한다. 멤버변수는 인스턴스변수와 static변수를 모두 통칭하는 말이다.

1. 클래스를 설계할 때, 멤버변수 중 모든 인스턴스에 공통으로 사용하는 것에 static을 붙인다.
- 생성된 각 인스턴스는 서로 독립적이기 때문에 각 인스턴스의 변수(iv)는 서로 다른 값을 유지한다. 그러나 모든 인스턴스에서 같은 값이 유지되어야 하는 변수는 static을 붙여서 클래스변수로 정의해야 한다.

2. 클래스 변수(static변수)는 인스턴스를 생성하지 않아도 사용할 수 있다.
- static이 붙은 변수(클래스변수)는 클래스가 메모리에 올라갈 때 이미 자동적으로 생성되기 때문이다.

3. 클래스 메소드(static메소드)는 인스턴스 변수를 사용할 수 없다.
- 인스턴스변수는 인스턴스가 반드시 존재해야만 사용할 수 있는데, 클래스메소드(static이 붙은 메소드)는 인스턴스 생성 없이 호출가능하므로 클래스 메소드가 호출되었을 때 인스턴스가 존재하지 않을 수도 있다. 그래서 클래스 메소드에서 인스턴스변수의 사용을 금지한다.   
반면에 인스턴스변수나 인스턴스메소드에서는 static이 붙은 멤버들을 사용하는 것이 언제나 가능하다. 인스턴스 변수가 존재한다는 것은 static변수가 이미 메모리에 존재한다는 것을 의미하기 때문이다.

4. 메소드 내에서 인스턴스 변수를 사용하지 않는다면, static을 붙이는 것을 고려한다.
- 메소드의 작업내용 중에서 인스턴스변수를 필요로 한다면, static을 붙일 수 없다. 반대로 인스턴스변수를 필요로 하지 않는다면 static을 붙이는 것이 좋다. 메소드 호출시간이 짧아지므로 성능이 향상된다. static을 안 붙인 메소드(인스턴스메소드)는 실행 시 호출되어야할 메소드를 찾는 과정이 추가적으로 필요하기 때문에 시간이 더 걸린다.

> - 클래스의 멤버변수 중 모든 인스턴스에 공통된 값을 유지해야하는 것이 있는지 살펴보고 있으면 static을 붙여준다.
> - 작성한 메소드 중에서 인스턴스변수나 인스턴스 메소드를 사용하지 않는 메소드에 static을 붙일 것을 고려한다.

예제 6-19 / ch6 / MyMathTest2.java
``` java
class MyMath2 {
	long a, b;
	
	// 인스턴스변수 a, b만을 이용해서 작업하므로 매개변수가 필요없다.
	long add() { return a + b; }	// a, b는 인스턴스변수
	long subtract() { return a - b; }
	long multiply() { return a * b; }
	double divide() { return a / b; }
	
	static long add(long a, long b) { return a + b; }	// a, b는 지역변수
	static long subtract(long a, long b) { return a - b; }
	static long multiply(long a, long b) { return a * b; }
	static double divide(double a, double b) { return a / b; }
}

public class MyMathTest2 {

	public static void main(String[] args) {
		// 클래스메소드 호출, 인스턴스 생성없이 호출가능
		System.out.println(MyMath2.add(200L, 100L));
		System.out.println(MyMath2.subtract(200L, 100L));
		System.out.println(MyMath2.multiply(200L, 100L));
		System.out.println(MyMath2.divide(200.0, 100.0));
		
		MyMath2 mm = new MyMath2();	// 인스턴스를 생성
		mm.a = 200L;
		mm.b = 100L;
		// 인스턴스메소드는 객체생성 후에만 호출이 가능함.
		System.out.println(mm.add());
		System.out.println(mm.subtract());
		System.out.println(mm.multiply());
		System.out.println(mm.divide());
	}

}
```

```
300
100
20000
2.0
300
100
20000
2.0
```

인스턴스메소드인 `add()`, `subtract()`, `multiply()`, `divide()`는 인스턴스변수인 `a`와 `b`만으로도 충분히 작업이 가능하기 때문에, 매개변수를 필요로 하지 않으므로 괄호()에 매개변수를 선언하지 않았다.

반면에 `add(long a, long b)`, `subtract(long a, long b)` 등은 인스턴스변수 없이 매개변수만으로 작업을 수행하기 때문에 `static`을 붙여서 클래스메소드로 선언하였다.

그래서 `MyMathTest2`의 `main`메소드에서 보면, 클래스메소드는 객체생성없이 바로 호출이 가능했고, 인스턴스메소드는 `MyMath2`클래스의 인스턴스를 생성한 후에야 호출이 가능했다.

</br>

## 3.12 클래스 멤버와 인스턴스 멤버간의 참조와 호출

같은 클래스에 속한 멤버들 간에는 별도의 인스턴스를 생성하지 않고도 서로 참조 또는 호출이 가능하다. 단, 클래스멤버가 인스턴스 멤버를 참조 또는 호출하고자 하는 경우에는 인스턴스를 생성해야 한다.

그 이유는 **인스턴스 멤버가 존재하는 시점에 클래스 멤버는 항상 존재하지만, 클래스멤버가 존재하는 시점에 인스턴스 멤버가 존재하지 않을 수도 있기 때문이다.**

> 인스턴스 멤버란 인스턴스 변수와 인스턴스 메소드를 의미한다.

``` java
class TestClass {
    void instanceMethod() {}        // 인스턴스메소드
    static void staticMethod() {}   // static메소드

    void instanceMethod2() {        // 인스턴스 메소드
        instanceMethod();           // 다른 인스턴스 메소드를 호출한다.
        staticMethod();             // static메소드를 호출한다.
    }

    static void staticMethod2() {
        instanceMethod();           // 에러. 인스턴스메소드를 호출할 수 없다.
        staticMethod();             // static메소드는 호출 할 수 있다.
    }
}   // end of class
```

위의 코드는 같은 클래스 내의 인스턴스 메소드와 static메소드 간의 호출에 대해서 설명하고 있다. 같은 클래스 내의 메소드는 서로 객체의 생성이나 참조변수 없이 직접 호출이 가능하지만 static메소드는 인스턴스 메소드를 호출할 수 없다.

``` java
class TestClass2 {
    int iv;         // 인스턴스 변수
    static int cv;  // 클래스 변수

    void instanceMethod() {         // 인스턴스메소드
        System.out.println(iv);     // 인스턴스 변수를 사용할 수 있다.
        System.out.println(cv);     // 클래스 변수를 사용할 수 있다.
    }

    static void staticMethod() {    // static메소드
        System.out.println(iv);     // 에러. 인스턴스 변수를 사용할 수 없다.
        System.out.println(cv);     // 클래스 변수는 사용할 수 있다.
    }
}   // end of class
```

이번에 변수와 메소드간의 호출에 대해서 살펴보겠다. 메소드간의 호추과 마찬가지로 인스턴스메소드는 인스턴스변수를 사용할 수 있지만, static메소드는 인스턴스변수를 사용할 수 없다.

예제 6-20 / ch6 / MemberCall.java
``` java
public class MemberCall {
	int iv = 10;
	static int cv = 20;
	
	int iv2 = cv;
//	static int cv2 = iv;		// 에러. 클래스변수는 인스턴스 변수를 사용할 수 없음
	static int cv2 = new MemberCall().iv;	// 이처럼 객체를 생성해야 사용가능
			
	static void staticMethod() {
		System.out.println(cv);
//		System.out.println(iv);		// 에러. 클래스메소드에서 인스턴스변수를 사용불가.
		MemberCall c = new MemberCall();
		System.out.println(c.iv);	// 객체를 생성한 후에야 인스턴스변수의 참조가능
	}
	
	void instanceMethod() {
		System.out.println(cv);
		System.out.println(iv);		// 인스턴스메소드에서는 인스턴스변수를 바로 사용가능
	}
	
	static void staticMethod2() {
		staticMethod();
//		instanceMethod();		// 에러. 클래스메소드에서는 인스턴스메소드를 호출할 수 없음
		MemberCall c = new MemberCall();
		c.instanceMethod();		// 인스턴스를 생성한 후에야 호출할 수 있음
	}
	
	void instanceMethod2() {	// 인스턴스메소드에서는 인스턴스메소드와 클래스메소드
		staticMethod();			// 모두 인스턴스 생성없이 바로 호출이 가능하다.
		instanceMethod();
	}
}
```

클래스멤버(클래스변수와 클래스메소드)는 언제나 참조 또는 호출이 가능하기 때문에 인스턴스멤버가 클래스멤버를 사용하는 것은 아무런 문제가 안 된다. 클래스멤버간의 참조 또는 호출 역시 아무런 문제가 없다.

그러나, 인스턴스멤버(인스턴스변수와 인스턴스메소드)는 반드시 객체를 생성한 후에만 참조 또는 호출이 가능하기 때문에 클래스멤버가 인스턴스멤버를 참조, 호출하기 위해서는 객체를 생성하여야 한다.

하지만, **인스턴스멤버간의 호출에는 아무런 문제가 없다. 하나의 인스턴스멤버가 존재한다는 것은 인스턴스가 이미 생성되어있다는 것을 의미하며, 즉 다른 인스턴스멤버들도 모두 존재하기 때문이다.**

수학에서의 대입법처럼, `c = new MemberCall()`이므로 `c.instanceMethod();`에서 `c`대신 `new MemberCall()`을 대입하여 사용할 수 있다.

``` java
MemberCall c = new MemberCall();
int result = c.instanceMethod1();
```

그래서 위의 두 줄을 다음과 같이 한 줄로 할 수 있다.

``` java
int result = new MemberCall().instanceMethod();
```

대신 참조변수를 선언하지 않았기 때문에 생성된 `MemberCall`인스턴스는 더 이상 사용할 수 없다.