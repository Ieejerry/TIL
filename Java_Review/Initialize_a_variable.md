Chapter 6. 객체지향 프로그래밍1

# 6. 변수의 초기화

</br>

## 6.1 변수의 초기화

변수를 선언하고 처음으로 값을 저장하는 것을 '변수의 초기화'라고 한다. 변수의 초기화는 경우에 따라서 필수적이기도 하고 선택적이기도 하지만, 가능하면 선언과 동시에 적절한 값으로 초기화 하는 것이 바람직하다.

멤버변수는 초기화를 하지 않아도 자동적으로 변수의 자료형에 맞는 기본값으로 초기화가 이루어지므로 초기화하지 않고 사용해도 되지만, **지역변수는 사용하기 전에 반드시 초기화해야 한다.**

``` java
class InitTest {
    int x;  // 인스턴스변수
    int y = x;  // 인스턴스변수

    void method1() {
        int i;  // 지역변수
        int j = i;  // 에러. 지역변수를 초기화하지 않고 사용
    }
}
```

위의 코드에서 `x`, `y`는 인스턴스 변수이고, `i`, `j`는 지역변수이다. 그 중 `x`와 `i`는 선언만 하고 초기화를 하지 않았다. 그리고 `y`를 초기화 하는데 `x`를 사용하였고, `j`를 초기화 하는데 `i`를 사용하였다.

인스턴스 변수 `x`는 초기화를 해주지 않아도 자동적으로 int형의 기본값인 0으로 초기화되므로, `int y = x;`와 같이 할 수 있다. `x`의 값이 0이므로 `y` 역시 0이 저장된다.

하지만, `method()`의 지역변수 `i`는 자동적으로 초기화되지 않으므로, 초기화 되지 않은 상태에서 변수 `j`를 초기화 하는데 사용될 수 없다. 컴파일하면, 에러가 발생한다.

> **멤버변수(클래스변수와 인스턴스변수)와 배열의 초기화는 선택적이지만, 지역변수의 초기화는 필수적이다.**

참고로 각 타입의 기본값(default value)은 다음과 같다.

![image](https://ifh.cc/g/B2Fz6w.png)

변수의 초기화에 대한 예를 몇 가지 더 살펴보겠다.

![image](https://ifh.cc/g/Q7ynfx.png)

> - 멤버변수의 초기화 방법
> 1. 명시적 초기화(explicit initialization)
> 2. 생성자(constructor)
> 3. 초기화 블럭(initialization block)
>    - 인스턴스 초기화 블럭: 인스턴스변수를 초기화 하는데 사용
>    - 클래스 초기화 블럭: 클래스변수를 초기화 하는데 사용

</br>

## 6.2 명시적 초기회(explicit initialization)

변수를 선언과 동시에 초기화하는 것을 명시적 초기화라고 한다. 가장 기본적이면서도 간단한 초기화 방법이므로 여러 초기화 방법 중에서 가장 우선적으로 고려되어야 한다.

``` java
class Car {
    int door = 4;   // 기본형(primitive type) 변수의 초기화
    Engine e = new Engine();    // 참조형(reference type)변수의 초기화

    // ...
}
```

명서적 초기화가 간단하고 명료하긴 하지만, 보다 복잡한 초기화 작업이 필요할 때는 '초기화 블럭(initialization block)' 또는 생성자를 사용해야 한다.

</br>

## 6.3 초기화 블럭(initialization block)

초기화 블럭에는 '클래스 초기화 블럭'과 '인스턴스 초기화 블럭' 두 가지 종류가 있다. 클래스 초기화 블럭은 클래스변수의 초기화에 사용되고, 인스턴스 초기화 블럭은 인스턴스변수의 초기화에 사용된다.

> **클래스 초기화 블럭** 클래스변수의 복잡한 초기화에 사용된다.   
> **인스턴스 초기화 블럭** 인스턴스변수의 복잡한 초기화에 사용된다.

초기화 블럭을 작성하려면, 인스턴스 초기화 블럭은 단순히 클래스 내에 블럭{}을 만들고 그 안에 코드를 작성하기만 하면 된다. 그리고 클래스 초기화 블럭은 인스턴스 초기화 블럭 앞에 단순히 `static`을 덧붙이기만 하면 된다.

초기화 블럭 내에는 메소드 내에서와 같이 조건문, 반복문, 예외처리구문 등을 자유롭게 사용할 수 있으므로, 초기화 작업이 복잡하여 명시적 초기화만으로는 부족한 경우 초기화 블럭을 사용한다.

``` java
class InitBlock {
    static { /* 클래스 초기화블럭 입니다. */ }

    { /* 인스턴스 초기화블럭 입니다. */ }

    // ...
}
```

클래스 초기화 블럭은 클래스가 메모리에 처음 로딩될 때 한번만 수행되며, 인스턴스 초기화 블럭은 생성자와 같이 인스턴스를 생성할 때 마다 수행된다.

그리고 생성자 보다 인스턴스 초기화 블럭이 먼저 수행된다

> 클래스가 처음 로딩될 때 클래스변수들이 자동적으로 메모리에 만들어지고, 곧바로 클래스 초기화블럭이 클래스변수들을 초기화하게 되는 것이다.

인스턴스 변수의 초기화는 주로 생성자를 사용하고, 인스턴스 초기화 블럭은 모든 생성자에서 공통으로 수행되야 하는 코드를 넣는데 사용한다.

``` java
Car() {
    count++;            // 중복되는 코드
    serialNo = count;   // 중복되는 코드
    color = "White";
    gearType = "Auto";
}

Car(String color, String gearType) {
    count++;            // 중복되는 코드
    serialNo = count;   // 중복되는 코드
    this.color = color;
    this.gearType = gearType;
}
```

예를 들면, 위와 같이 클래스의 모든 생성자에 공통으로 수행되어야 하는 문장들이 있을 때, 이 문장들을 각 생성자마다 써주기 보다는 아래와 같이 인스턴스 블럭에 넣어주면 코드가 보다 간결해진다.

``` java
{
    count++;
    serialNo = count;
}

Car() {
    color = "White";
    gearType = "Auto";
}

Car(String color, String gearType) {
    this.color = color;
    this.gearType = gearType;
}
```

이처럼 코드의 중복을 제거하는 것은 코드의 신뢰성을 높여 주고, 오류의 발생가능성을 줄여 준다는 장점이 있다. 즉, 재사용성을 높이고 중복을 제거하는 것, 이것이 바로 객체지향프로그래밍이 추구하는 궁극적인 목표이다.

예제 6-27 / ch6 / BlockTest.java

``` java
public class BlockTest {
	static {
		System.out.println("static { }");
	}
	
	{
		System.out.println("{ }");
	}
	
	public BlockTest() {
		System.out.println("생성자");
	}
	
	public static void main(String[] args) {
		System.out.println("BlockTest bt = new BlockTest(); ");
		BlockTest bt = new BlockTest();
		
		System.out.println("BlockTest bt2 = new BlockTest(); ");
		BlockTest bt2 = new BlockTest();
	}

}
```

```
static { }
BlockTest bt = new BlockTest(); 
{ }
생성자
BlockTest bt2 = new BlockTest(); 
{ }
생성자
```

예제가 실행되면서 `BlockTest`가 메모리에 로딩될 때, 클래스 초기화 블럭이 가장 먼저 수행되어 `static {}`이 화면에 출력된다. 그 다음에 `main`메소드가 수행되어 `BlockTest`인스턴스가 생성되면서 인스턴스 초기화 블럭이 먼저 수행되고, 끝으로 새엉자가 수행된다.
위의 실행결과에서도 알 수 있듯이 클래스 초기화 블럭은 처음 메모리에 로딩될 때 한번만 수행되었지만, 인스턴스 초기화 블럭은 인스턴스가 생성될 때 마다 수행되었다.

예제 6-28 / ch6 / StaticBlockTest.java

``` java
public class StaticBlockTest {
	static int[] arr = new int[10];
	
	static {
		for(int i = 0; i < arr.length; i++) {
			// 1과 10사이의 임의의 값을 배열 arr에 저장한다.
			arr[i] = (int)(Math.random() * 10) + 1;
		}
	}
	
	public static void main(String[] args) {
		for(int i = 0; i < arr.length; i++)
			System.out.println("arr[" + i + "] :" + arr[i]);
	}

}
```

```
arr[0] :4
arr[1] :1
arr[2] :1
arr[3] :2
arr[4] :9
arr[5] :8
arr[6] :10
arr[7] :8
arr[8] :10
arr[9] :7
```

명시적 초기화를 통해 배열 `arr`을 생성하고, 클래스 초기화 블럭을 이요해서 배열의 각 요소들을 `random()`을 사용해서 임의의 값으로 채우도록 했다.

이처럼 배열이나 예외처리가 필요한 초기화에서는 명시적 초기화만으로는 복잡한 초기화 작업을 할 수 없다. 이런 경우에 추가적으로 클래스 초기화 블럭을 사용하도록 한다.

> 인스턴스변수의 복잡한 초기화는 생성자 또는 인스턴스 초기화 블럭을 사용한다.

</br>

## 6.4 멤버변수의 초기화 시기와 순서

> **클래변수의 초기화시점** 클래스가 처음 로딩될 때 단 한번 초기화 된다.   
> **인스턴스변수의 초기화시점** 인스턴스가 생성될 때마다 각 인스턴스별로 초기화가 이루어진다.
> **클래스변수의 초기화순서** 기본값 → 명시적초기화 → 클래스 초기화 블럭   
> **인스턴스변수의 초기화순서** 기본값 → 명시적초기화 → 인스턴스 초기화 블럭 → 생성자

프로그램 실행도중 클래스에 대한 정보가 요구될 때, 클래스는 메모리에 로딩된다. 예를 들면, 클래스 멤버를 사용했을 때, 인스턴스를 생성할 때 등이 이에 해당한다.

하지만, 해당 클래스가 이미 메모리에 로딩되어 있다면, 또다시 로딩하지 않는다. 물론 초기화도 다시 수행되지 않는다.

> 클래스의 로딩 시기는 JVM의 종류에 따라 좀 다를 수 있는데, 클래스가 필요할 때 바로 메모리에 로딩하도록 설계가 되어있는 것도 있고, 실행효율을 높이기 위해서 사용될 클래스들을 프로그램이 시작될 때 미리 로딩하도록 되어있는 것도 있다.

``` java
class InitTest {
    static int cv = 1;  // 명시적 초기화
    int iv = 1; // 명시적 초기화

    static { cv = 2; }  // 클래스 초기화 블럭

    { iv = 2;}  // 인스턴스 초기화 블럭

    InitTest() {    // 생성자
        iv = 3;
    }
}
```

위의 `InitTest`클래스는 클래스변수(`cv`)와 인스턴스변수(`iv`)를 각각 하나씩 가지고 있다. `new InitTest();`와 같이 하여 인스턴스를 생성했을 때, `cv`와 `iv`가 초기화되어가는 과정을 단계별로 자세히 살펴보도록 하겠다.

![image](https://ifh.cc/g/VHqBkT.png)

▶ 클래스변수 초기화(1~3) : 클래스가 처음 메모리에 로딩될 때 차례대로 수행됨.
▶ 인스턴스변수 초기화(4~7) : 인스턴스를 생성할 때 차례대로 수행됨.

> 클래스변수는 항상 인스턴스변수보다 항상 먼저 생성되고 초기화 된다.

1. cv가 메모리(method area)에 생성되고, cv에는 int형의 기본값인 0이 cv에 저장된다.
2. 그 다음에는 명시적 초기화(int cv = 1)에 의해서 cv에 1이 저장된다.
3. 마지막으로 클래스 초기화 블럭(cv = 2)이 수행되어 cv에는 2가 저장된다.
4. InitTest클래스의 인스턴스가 생성되면서 iv가 메모리(heap)에 존재하게 된다. iv 역시 int형 변수이므로 기본값 0이 저장된다.
5. 명시적 초기화에 의해서 iv에 1이 저장되고
6. 인스턴스 초기화 블럭이 수행되어 iv에 2가 저장된다.
7. 마지막으로 생성자가 수행되어 iv에는 3이 저장된다.

예제 6-29 / ch6 / ProductTest.java

``` java
class Product {
	static int count = 0;	// 생성된 인스턴스의 수를 저장하기 위한 변수
	int serialNo;	// 인스턴스 고유의 번호
	
	{
		++count;
		serialNo = count;
	}
	
	public Product() {}	// 기본생성자, 생략가능
}

public class ProductTest {

	public static void main(String[] args) {
		Product p1 = new Product();
		Product p2 = new Product();
		Product p3 = new Product();
		
		System.out.println("p1의 제품번호(serial no)는 " + p1.serialNo);
		System.out.println("p2의 제품번호(serial no)는 " + p2.serialNo);
		System.out.println("p3의 제품번호(serial no)는 " + p3.serialNo);
		System.out.println("생성된 제품의 수는 모두 " + Product.count + "개 입니다.");
	}

}
```

```
p1의 제품번호(serial no)는 1
p2의 제품번호(serial no)는 2
p3의 제품번호(serial no)는 3
생성된 제품의 수는 모두 3개 입니다.
```

공장에서 제품을 생산할 때 제품마다 생산일련번호(serial no)를 부여하는 것과 같이 `Product`클래스의 인스턴스가 고유의 일련번호(serialNo)를 갖도록 하였다.

`Product`클래스의 인스턴스를 생성할 때마다 인스턴스 블럭이 수행되어, 클래스변수 `count`의 값을 1증가시킨 다음, 그 값을 인스턴스변수 `serialNo`에 저장한다.

이렇게 함으로써 새로 생성되는 인스턴스는 이전에 생성된 인스턴스보다 1이 증가된 `serialNo`값을 갖게 된다.

생성자가 하나 밖에 없기 때문에 인스턴스 블럭 대신, `Product`클래스의 생성자를 사용해도 결과는 같지만, 코드의 의미상 모든 생성자에서 공통으로 수행되어야하는 내용이기 때문에 인스턴스 블럭을 사용하였다.

만일 `count`를 인스턴스 변수로 선언했다면, 인스턴스가 생성될 때마다 0으로 초기화 될 것이므로 모든 `Product`인스턴스의 `serialNo`값은 항상 1이 될 것이다.

예제 6-20 / ch6 / DocumentTest.java

``` java
class Document {
	static int count = 0;
	String name;	// 문서명(Document name)
	
	Document() {	// 문서 생성 시 문서명을 지정하지 않았을 때
		this("제목없음" + ++count);
	}
	
	Document(String name) {
		this.name = name;
		System.out.println("문서 " + this.name + "가 생성되었습니다.");
	}
}

public class DocumentTest {

	public static void main(String[] args) {
		Document d1 = new Document();
		Document d2 = new Document("자바.txt");
		Document d3 = new Document();
		Document d4 = new Document();
	}

}
```

```
문서 제목없음1가 생성되었습니다.
문서 자바.txt가 생성되었습니다.
문서 제목없음2가 생성되었습니다.
문서 제목없음3가 생성되었습니다.
```

바로 이전의 일련번호 예제를 응용한 것으로, 워드프로세서나 문서편집기에 이와 유사한 코드가 사용된다. 문서(Document)를 생성할 때, 문서의 이름을 지정하면 그 이름의 문서가 생성되지만, 문서의 이름을 지정하지 않으면 프로그램이 일정한 규칙을 적용해서 자동으로 이름을 결정한다.