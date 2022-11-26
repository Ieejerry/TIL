# 1. 제네릭스(Generics)

</br>

## 1.1 제네릭스란?

제네릭스는 다양한 타입의 객체들을 다루는 메소드나 컬렉션 클래스에 컴파일 시의 타입 체크(compile-time type check)를 해주는 기능이다. 객체의 타입을 컴파일 시에 체크하기 때문에 객체의 타입 안전성을 높이고 형변환의 번거러움이 줄어든다.

타입 안정성을 높인다는 것은 의도하지 않은 타입의 객체가 저장되는 것을 막고, 저장된 객체를 꺼내올 때 원래의 타입과 다른 타입으로 잘못 형변환되어 발생할 수 있는 오류를 줄어준다.

예를 들어, ArrayList와 같은 컬렉션 클래스는 다양한 종류의 객체를 담을 수 있긴 하지만 보통 한 종류의 객체를 담는 경우가 더 많다. 그런데도 꺼낼 때 마다 타입체크를 하고 형변환을 하는 것은 아무래도 불편할 수밖에 없다. 게다가 원하지 않는 종류의 객체가 포함되는 것을 막을 방법이 없다는 것도 문제다. 이러한 문제들을 제네릭스가 해결해 준다.

> **제네릭스의 장점**   
> 1. 타입 안정성을 제공한다.   
> 2. 타입체크의 형변환을 생략할 수 있으므로 코드가 간결해 진다.

간단하게 얘기하면 다룰 객체의 타입을 미리 명시해줌으로써 번거로운 형변환을 줄여준다.

</br>

## 1.2 제네릭 클래스의 선언

제네릭 타입은 클래스와 메소드에 선언할 수 있는데, 먼저 클래스에 선언하는 지네릭 타입에 대해 알아보겠다. 예를 들어 클래스 `Box`가 다음과 같이 정의되어 있다고 가정하겠다.

``` java
class Box {
    Object item;

    void setItem(Object item) { this.item = item; }
    Object getItem() { return item; }
}
```

이 클래스를 제네릭 클래스로 변경하면 다음과 같이 클래스 옆에 `<T>`를 붙이면 된다. 그리고 `Object`를 모두 `T`로 바꾼다.

``` java
class Box<T> {  // 제네릭 타입 T를 선언
    T item;

    void setItem(T item) { this.item = item; }
    T getItem() { return item; }
}
```

`Box<T>`에서 `T`를 '타입 변수(type variable)'라고 하며, `Type`의 첫 글자에서 따온 것이다 .타입 변수는 `T`가 아닌 다른 것을 사용해도 된다. `ArrayList<E>`의 경우, 타입 변수 `E`는 'Element(요소)'의 첫 글자를 따서 사용했다. 타입 변수가 여러 개인 경우에는 `Map<K, V>`와 같이 콤마 ','를 구분자로 나열하면 된다. `K`는 Key(키)를 의미하고, `V`는 Value(값)을 의미한다. 무조건 `T`를 사용하기보다 가능하면, 이처럼 상황에 맞게 의미있는 문자를 선택해서 사용하는 것이 좋다.

이들은 **기호의 종류만 다를 뿐 '임의의 참조형 타입'을 의미한다는 것은 모두 같다.**

기존에는 다양한 종류의 타입을 다루는 메소드의 매개변수나 리턴타입으로 Object타입의 참조변수를 많이 사용했고, 그로 인해 형변환이 불가피했지만, 이젠 Object타입 대신 원하는 타입을 지정하기만 하면 되는 것이다.

이제 제네릭 클래스가 된 `Box`클래스의 객체를 생성할 때는 다음과 같이 참조변수와 생성자에 타입 `T`대신에 사용될 실제 타입을 지정해주어야 한다.

``` java
Box<String> b = new Box<String>();  // 타입 T 대신, 실제 타입을 지정
b.setItem(new Object());    // 에러. String이외의 타입은 지정불가
b.setItem("ABC");   // OK. String타입이므로 가능
String item = b.getItem(); // 형변환이 필요없음
```

위의 코드에서 타입 `T`대신에 `String`타입을 지정해줬으므로, 제네릭 클래스 `Box<T>`는 다음과 같이 정의된 것과 같다.

``` java
class Box { // 제네릭 타입을 String으로 지정
    String item;

    void setItem(String item) { this.item = item; }
    String getItem() { return item; }
}
```

제네릭이 도입되기 이전의 코드와 호환을 위해, 제네릭 클래스인데도 예전의 방식으로 객체를 생성하는 것이 허용된다. 다만 제네릭 타입을 지정하지 않아서 안전하지 않다는 경고가 발생한다.

``` java
Box b = new Box();  // OK. T는 Object로 간주된다.
b.setItem("ABC");  // 경고. unchecked or unsafe operation
b.setItem(new Object());    // 경고. unchecked or unsafe operation
```

아래와 같이 타입 변수 `T`에 `Object`타입을 지정하면, 타입을 지정하지 않은 것이 아니라 알고 적은 것이므로 경고는 발생하지 않는다.

``` java
Box<Object> b = new Box<Object>();
b.setItem("ABC");   // 경고발생 안함
b.setItem(new Object());    // 경고발생 안함
```

</br>

### 제네릭스 용어

다음과 같이 제네릭 클래스 `Box`가 선언되어 있을 때,

![image](https://ifh.cc/g/fm23Af.png)

> **Box\<T\>** 제네릭 클래스. 'T의 Box' 또는 'T Box'라고 읽는다.   
> **T** 타입 변수 또는 타입 매개변수.(T는 타입 문자)   
> **Box** 원시 타입(raw type)

타입 문자 `T`는 제네릭 클래스 `Box<T>`의 타입 변수 또는 타입 매개변수라고 하는데, 메소드의 매개변수와 유사한 면이 있기 때문이다. 그래서 아래와 같이 타입 매개변수에 타입을 지정하는 것을 '제네릭 타입 호출'이라고 하고, 지정된 타입 `String`을 '매개변수화된 타입(parameterized type)'이라고 한다. 매개변수화된 타입이라는 용어가 좀 길어서, 앞으로 이 용어 대신 '대입된 타입'이라는 용어를 사용하겠다.

![image](https://ifh.cc/g/kcwQhm.png)

예를 들어, `Box<String>`과 `Box<Integer>`는 제네릭 클래스 `Box<T>`에 서로 다른 타입을 대입하여 호출한 것일 뿐, 이 둘이 별개의 클래스를 의미하는 것은 아니다. 이는 마치 매개변수의 값이 다른 메소드 호출, 즉 `add(3,5)`와 `add(2,4)`가 서로 다른 메소드를 호출하는 것이 아닌 것과 같다.

컴파일 후에 `Box<String>`과 `Box<Integer>`는 이들의 '원시 타입'인 `Box`로 바뀐다. 즉, 제네릭 타입이 제거된다.

</br>

### 제네릭스의 제한

제네릭 클래스 `Box`의 객체를 생성할 때, 객체별로 다른 타입을 지정하는 것은 적절하다. 제네릭스는 이처럼 인스턴스별로 다르게 동작하도록 하려고 만든 기능이다.

``` java
Box<Apple> appleBox = new Box<Apple>(); // OK. Apple객체만 저장가능
Box<Grape> grapeBox = new Box<Grape>(); // OK. Grape객체만 저장가능
```

그러나 모든 객체에 대해 동일하게 동작해야하는 static멤버에 타입 변수 `T`를 사용할 수 없다. `T`는 인스턴스변수로 간주되기 때문이다.

``` java
class Box<T> {
    static T item;  // 에러
    static int compare(T t1, T t2) { ... }  // 에러
        ...
}
```

static멤버는 타입 변수에 지정된 타입, 즉 대입된 타입의 종류에 관계없이 동일한 것이어야 하기 때문이다. 즉, `Box<Apple>.item`과 `Box<Grape>.item`이 다른 것이어서는 안된다는 뜻이다. 그리고 제네릭 타입의 배열을 생성하는 것도 허용되지 않는다. 제네릭 배열 타입의 참조변수를 선언하는 것은 가능하지만, `new T[10]`과 같이 배열을 생성하는 것은 안 된다는 뜻이다.

``` java
class Box<T> {
    T[] itemArr;    // OK. T타입의 배열을 위한 참조변수
        ...
    T[] toArray() {
        T[] tmpArr = new T[itemArr.length]; // 에러. 제네릭 배열 생성불가
        ...
        return tmpArr;
    }
        ...
}
```

제네릭 배열을 생성할 수 없는 것은 `new`연산자 때문인데, 이 연산자는 컴파일 시점에 타입 `T`가 뭔지 정확히 알아야 한다. 그런데 위의 코드에 정의된 `Box<T>`클래스를 컴파일하는 시점에서는 `T`가 어떤 타입이 될지 전혀 알 수 없다. `instanceof`연산자도 `new`연산자와 같은 이유로 `T`를 피연산자로 사용할 수 없다.

꼭 제네릭 배열을 생성해야할 필요가 있을 때는, `new`연산자 대신 'Reflection API'의 `newInstance()`와 같이 동적으로 객체를 생성하는 메소드로 배열을 생성하거나, `Object`배열을 생성해서 복사한 다음에 `T[]`로 형변환하는 방법 등을 사용한다.

</br>

## 1.3 제네릭 클래스의 객체 생성과 사용

제네릭 클래스 `Box<T>`가 다음과 같이 정의되어 있다고 가정하겠다. 이 `Box<T>`의 객체는 한 가지 종류, 즉 `T`타입의 객체만 저장할 수 있다. 전과 달리 `ArrayList`를 이용해서 여러 객체를 저장할 수 있도록 하였다.

``` java
class Box<T> {
    ArrayList<T> list = new ArrayList<T>();

    void add(T item) { list.add(item); }
    T get(int i) { return list.get(i); }
    ArrayList<T> getList() { return list; }
    int size() { return list.size(); }
    public String toString() { return list.toString(); }
}
```

`Box<T>`의 객체를 생성할 때는 다음과 같이 한다. 참조변수와 생성자에 대입된 타입(매개변수화된 타입)이 일치해야 한다. 일치하지 않으면 에러가 발생한다.

``` java
Box<Apple> appleBox = new Box<Apple>(); // OK.
Box<Apple> appleBox = new Box<Grape>(); // 에러
```

두 타입이 상속관계에 있어도 마찬가지이다. `Apple`이 `Fruit`의 자손이라고 가정하겠다.

``` java
Box<Fruit> appleBox = new Box<Apple>(); // 에러. 대입된 타입이 다르다.
```

단, 두 제네릭 클래스의 타입이 상속관계에 있고, 대입돈 타입이 같은 것은 괜찮다. `FruitBox`는 `Box`의 자손이라고 가정하겠다.

``` java
Box<Apple> appleBox = new FruitBox<Apple>();    // OK. 다형성
```

JDK1.7부터는 추정이 가능한 경우 타입을 생략할 수 있게 되었다. 참조변수의 타입으로부터 `Box`가 `Apple`타입의 객체만 저장한다는 것을 알 수 있기 때문에, 생성자에 반복해서 타입을 지정하지 않아도 되는 것이다. 따라서 아래의 두 문장은 동일하다.

``` java
Box<Apple> appleBox = new Box<Apple>();
Box<Apple> appleBox = new Box<>();  // OK. JDK1.7부터 생략가능
```

생성된 `Box<T>`의 객체에 `void add(T item)`으로 객체를 추가할 때, 대입된 타입과 다른 타입의 객체는 추가할 수 없다.

``` java
Box<Apple> appleBox = new Box<Apple>();
appleBox.add(new Apple());  // OK.
appleBox.add(new Grape());  // 에러. Box<Apple>에는 Apple객체만 추가가능
```

그러나 타입 `T`가 `Fruit`인 경우, `void add(Fruit item)`가 되므로 `Fruit`의 자손들은 이 메소드의 매개변수가 될 수 있다. `Apple`이 `Fruit`의 자손이라고 가정하겠다.

``` java
Box<Fruit> fruitBox = new Box<Fruit>();
fruitBox.add(new Fruit());  // OK.
fruitBox.add(new Apple());  // OK. void add(Fruit item)
```

</br>

예제 12-1 / ch12 / FruitBoxEx1.java

``` java
import java.util.ArrayList;

class Fruit { public String toString() { return "Fruit"; }}
class Apple extends Fruit { public String toString() { return "Apple"; }}
class Grape extends Fruit { public String toString() { return "Grape"; }}
class Toy { public String toString() { return "Toy"; }}

public class FruitBoxEx1 {
	public static void main(String[] args) {
		Box<Fruit> fruitBox = new Box<Fruit>();
		Box<Apple> appleBox = new Box<Apple>();
		Box<Toy> toyBox = new Box<Toy>();
//		Box<Grape> grapeBox = new Box<Apple>();	// 에러. 타입 불일치
		
		fruitBox.add(new Fruit());
		fruitBox.add(new Apple());	// OK. void add(Fruit item)
		
		appleBox.add(new Apple());
		appleBox.add(new Apple());
//		appleBox.add(new Toy());	// 에러. Box<Apple>에는 Apple만 담을 수 있음.
		
		toyBox.add(new Toy());
//		toyBox.add(new Apple());	// 에러. Box<Toy>에는 Apple을 담을 수 없음.
		
		System.out.println(fruitBox);
		System.out.println(appleBox);
		System.out.println(toyBox);
	}   // main
}

class Box<T> {
	ArrayList<T> list = new ArrayList<T>();
	void add(T item) { list.add(item); }
	T get(int i) { return list.get(i); }
	int size() { return list.size(); }
	public String toString() { return list.toString(); }
}
```

```
[Fruit, Apple]
[Apple, Apple]
[Toy]
```

</br>

## 1.4 제한된 제네릭 클래스

타입 문자로 사용할 타입을 명시하면 한 종류의 타입만 저장할 수 있도록 제한할 수 있지만, 그래도 여전히 모든 종류의 타입을 저장할 수 있다는 것에는 변함이 없다.

``` java
FruitBox<Toy> fruitBox = new FruitBox<Toy>();
fruitBox.add(new Toy());    // OK. 과일상자에 장난감을 담을 수 있다.
```

다음과 같이 제네릭 타입에 `extends`를 사용하면, 특정 타입의 자손들만 대입할 수 있게 제한할 수 있다.

``` java
class FruitBox<T extends Fruit> {   // Fruit의 자손만 타입으로 지정가능
    ArrayList<T> list = new ArrayList<T>();
    ...
}
```

여전히 한 종류의 타입만 담을 수 있지만, `Fruit`클래스의 자손들만 담을 수 있다는 제한이  더 추가된 것이다.

``` java
FruitBox<Apple> appleBox = new FruitBox<Apple>();   // OK
FruitBox<Toy> toyBox = new FruitBox<Toy>(); // 에러. Toy는 Fruit의 자손이 아님
```

게다가 `add()`의 매개변수의 타입 `T`도 `Fruit`와 그 자손 타입이 될 수 있으므로, 아래와 같이 여러 과일을 담을 수 있는 상자가 가능하게 된다.

``` java
FruitBox<Fruit> fruitBox = new FruitBox<Fruit>();
fruitBox.add(new Apple());  // OK. Apple이 Fruit의 자손
fruitBox.add(new Grape());  // OK. Grape가 Fruit의 자손
```

다형성에서 조상타입의 참조변수로 자손타입의 객체를 가리킬 수 있는 것처럼, 매개변수화된 타입의 자손 타입도 가능한 것이다. 타입 매개변수 `T`에 `Object`를 대입하면, 모든 종류의 객체를 저장할 수 있게 된다.

만일 클래스가 아니라 인터페이스를 구현해야 한다는 제약이 필요하다면, 이 때도 `extends`를 사용한다. `implements`를 사용하지 않는다.

``` java
interface Eatable {}
class FruitBox<T extends Eatable> { ... }
```

클래스 `Fruit`의 자손이면서 `Eatable`인터페이스도 구현해야한다면 아래와 같이 `&`기호로 연결한다.

``` java
class FruitBox<T extends Fruit & Eatable> { ... }
```

이제 `FruitBox`에는 `Fruit`의 자손이면서 `Eatable`을 구현한 클래스만 타입 매개변수 `T`에 대입될 수 있다.

</br>

예제 12-2 / ch12 / FruitBoxEx2.java

``` java
import java.util.ArrayList;

class Fruit implements Eatable {
	public String toString() { return "Fruit"; }
}

class Apple extends Fruit { public String toString() { return "Apple"; }}
class Grape extends Fruit { public String toString() { return "Grape"; }}
class Toy { public String toString() { return "Toy"; }}

interface Eatable {}

public class FruitBoxEx2 {
	public static void main(String[] args) {
		FruitBox<Fruit> fruitBox = new FruitBox<Fruit>();
		FruitBox<Apple> appleBox = new FruitBox<Apple>();
		FruitBox<Grape> grapeBox = new FruitBox<Grape>();
//		FruitBox<Grape> grapeBox = new FruitBox<Apple>();	// 에러. 타입 불일치
//		FruitBox<Toy> toyBox = new FruitBox<Toy>();	// 에러.
		
		fruitBox.add(new Fruit());
		fruitBox.add(new Apple());
		fruitBox.add(new Grape());
		appleBox.add(new Apple());
//		appleBox.add(new Grape());	// 에러. Grape는 Apple의 자손이 아님
		grapeBox.add(new Grape());
		
		System.out.println("fruitbox - " + fruitBox);
		System.out.println("applebox - " + appleBox);
		System.out.println("grapebox - " + grapeBox);
	}	// main
}

class FruitBox<T extends Fruit & Eatable> extends Box<T> {}

class Box<T> {
	ArrayList<T> list = new ArrayList<T>();	// item을 저장할 list
	void add(T item) { list.add(item); }	// 박스에 item을 추가
	T get(int i) { return list.get(i); }	// 박스에 item을 꺼낼 때
	int size() { return list.size(); }
	public String toString() { return list.toString(); }
}
```

```
fruitbox - [Fruit, Apple, Grape]
applebox - [Apple]
grapebox - [Grape]
```

</br>

## 1.5 와일드 카드

매개변수에 과일박스를 대입하면 주스를 만들어서 반환하는 `Juicer`라는 클래스가 있고 이 클래스에는 과일을 주스로 만들어서 반환하는 `makeJuice()`라는 static메소드가 다음과 같이 정의되어 있다고 가정하겠다.

``` java
class Juiceer {
    static Juice makeJuice(FruitBox<Fruit> box) {   // <Fruit>으로 저장
        String tmp = "";
        for(Fruit f : box.getList()) tmp += f + " ";
        return new Juice(tmp);
    }
}
```

`Juicer`클래스는 제네릭 클래스가 아닌데다, 제네릭 클래스라고 해도 static메소드에는 타입 매개변수 `T`를 매개변수에 사용할 수 없으므로 아예 제네릭스를 적용하지 않던가, 위와 같이 타입 매개변수 대신, 특정 타입을 지정해줘야 한다.

``` java
FruitBox<Fruit> fruitBox = new FruitBox<Fruit>();
FruitBox<Apple> appleBox = new FruitBox<Apple>();
        ...
System.out.println(Juicer.makeJuice(fruitBox)); // OK. FruitBox<Fruit>
System.out.println(Juicer.makeJuice(appleBox)); // 에러. FruitBox<Apple>
```

이렇게 제네릭 타입을 `FruitBox<Fruit>`로 고정해 놓으면, 위의 코드에서 알 수 있듯이 `FruitBox<Apple>`타입의 객체는 `makeJuice()`의 매개변수가 될 수 없으므로, 다음과 같이 여러 가지 타입의 매개변수를 갖는 `makeJuice()`를 만들 수밖에 없다.

``` java
static Juice makeJuice(FruitBox<Fruit> box) {
    String tmp = "";
    for(Fruit f : box.getList()) tmp += f + " ";
    return new Juice(tmp);
}

static Juice makeJuice(FruitBox<Apple> box) {
    String tmp = "";
    for(Fruit f : box.getList()) tmp += f + " ";
    return new Juice(tmp);
}
```

그러나 위와 같이 오버로딩하면, 컴파일 에러가 발생한다. **지네릭 타입이 다른 것만으로는 오버로딩이 성립되지 않기 때문이다.** 제네릭 타입은 컴파일러가 컴파일할 때만 사용히거 제거해버린다. 그래서 위의 두 메소드는 오버로딩이 아니라 '메소드 중복 정의'이다.

이럴 때 사용하기 위해 고안된 것이 바로 '와일드 카드'이다. 와일드 카드는 기호 `?`로 표현하는데, 와일드 카드는 어떠한 타입도 될 수 있다.

`?`만으로는 Object타입과 다를 게 없으므로, 다음과 같이 `extends`와 `super`로 상한(upper bound)과 하한(lower bound)을 제한할 수 있다.

> **\<? extends T\>** 와일드 카드의 상한 제한. T와 그 자손들만 가능  
> **\<? super T\>** 와일드 카드의 하한 제한. T와 그 조상들만 가능   
> **\<?\>** 제한 없음. 모든 타입이 가능. <? extends Object>와 동일

> 제네릭 클래스와 달리 와일드 카드에는 '&'를 사용할 수 없다. 즉, \<? extends T & E\>와 같이 할 수 없다.

와일드 카드를 사용해서 `makeJuice()`의 매개변수 타입을 `FruitBox<Fruit>`에서 `FruitBox<? extends Fruit>`으로 바꾸면 다음과 같이 된다.

``` java
static Juice makeJuice(FruitBox<? extends Fruit> box) {
    String tmp = "";
    for(Fruit f : box.getList()) tmp += f + " ";
    return new Juice(tmp);
}
```

이제 이 메소드의 매개변수로 `FruitBox<Fruit>`뿐만 아니라, `FruitBox<Apple>`와 `FruitBox<Grape>`도 가능하게 된다.

> 매개변수의 타입을 'FruitBox\<? extends Object\>로 하면, 모든 종류의 FruitBox가 매개변수로 가능하다.

``` java
FruitBox<Fruit> fruitBox = new FruitBox<Fruit>();
FruitBox<Apple> appleBox = new FruitBox<Apple>();
    ...
System.out.println(Juicer.makeJuice(fruitBox)); // OK. FruitBox<Fruit>
System.out.println(Juicer.makeJuice(appleBox)); // OK. FruitBox<Apple>
```

매개변수의 타입을 `FruitBox<? extends Object>`로 하면, 모든 종류의 `FruitBox`가 이 메소드의 매개변수로 가능해진다. 대신, 전과 달리 `box`의 요소가 `Fruit`의 자손이라는 보장이 없으므로 아래의 for문에서 `box`에 저장된 요소를 `Fruit`타입의 참조변수로 못받는다.

``` java
static Juice makeJuice(FruitBox<? extends Object> box) {
    String tmp = "";

    for(Fruit f : box.getList()) tmp += f + " ";    // 에러. Fruit이 아닐 수 있음
    return new Juice(tmp);
}
```

그러나 실제로 테스트 해보면 문제없이 컴파일되는데 그 이유는 바로 제네릭 클래스 `FruitBox`를 제한했기 때문이다.

``` java
class FruitBox<T extends Fruit> extends Box<T> {}
```

컴파일러는 위 문장으로부터 모든 `FruitBox`의 요소들이 `Fruit`의 자손이라는 것을 알고 있으므로 문제 삼지 않는 것이다.

</br>

예제 12-3 / ch12 / FruitBoxEx3.java

``` java
import java.util.ArrayList;

class Fruit2 { public String toString() { return "Fruit"; }}
class Apple2 extends Fruit2 { public String toString() { return "Apple"; }}
class Grape2 extends Fruit2 { public String toString() { return "Grape"; }}

class Juice {
	String name;
	
	Juice(String name) { this.name = name + "Juice"; }
	public String toString() { return name; }
}

class Juicer {
	static Juice makeJuice(FruitBox2 <? extends Fruit2> box) {
		String tmp = "";
		
		for(Fruit2 f : box.getList()) {
			tmp += f + " ";
		}
		return new Juice(tmp);
	}
}

public class FruitBoxEx3 {

	public static void main(String[] args) {
		FruitBox2<Fruit2> fruitBox = new FruitBox2<Fruit2>();
		FruitBox2<Apple2> appleBox = new FruitBox2<Apple2>();
		
		fruitBox.add(new Apple2());
		fruitBox.add(new Grape2());
		appleBox.add(new Apple2());
		appleBox.add(new Apple2());
		
		System.out.println(Juicer.makeJuice(fruitBox));
		System.out.println(Juicer.makeJuice(appleBox));
	}	// main

}

class FruitBox2<T extends Fruit2> extends Box2<T> {}

class Box2<T> {
	ArrayList<T> list = new ArrayList<T>();
	void add(T item) { list.add(item); }
	T get(int i) { return list.get(i); }
	ArrayList<T> getList() { return list; }
	int size() { return list.size(); }
	public String toString() { return list.toString(); }
}
```

```
Apple Grape Juice
Apple Apple Juice
```

다음 예제는 `super`로 와일드 카드의 하한을 제한하는 경우에 대한 예를 보여준다.

</br>

예제 12-4 / ch12 / FruitBoxEx4.java

``` java
import java.lang.annotation.Retention;
import java.util.*;

class Fruit3 {
	String name;
	int weight;
	
	Fruit3(String name, int weight) {
		this.name = name;
		this.weight = weight;
	}
	
	public String toString() { return name + "(" + weight + ")"; }
}

class Apple3 extends Fruit3 {
	Apple3(String name, int weight) {
		super(name, weight);
	}
}

class Grape3 extends Fruit3 {
	Grape3(String name, int weight) {
		super(name, weight);
	}
}

class AppleComp implements Comparator<Apple3> {
	public int compare(Apple3 t1, Apple3 t2) {
		return t2.weight - t1.weight;
	}
}

class GrapeComp implements Comparator<Grape3> {
	public int compare(Grape3 t1, Grape3 t2) {
		return t2.weight - t1.weight;
	}
}

class FruitComp implements Comparator<Fruit3> {
	public int compare(Fruit3 t1, Fruit3 t2) {
		return t1.weight - t2.weight;
	}
}

public class FruitBoxEx4 {
	public static void main(String[] args) {
		FruitBox3<Apple3> appleBox = new FruitBox3<Apple3>();
		FruitBox3<Grape3> grapeBox = new FruitBox3<Grape3>();
		
		appleBox.add(new Apple3("GreenApple", 300));
		appleBox.add(new Apple3("GreenApple", 100));
		appleBox.add(new Apple3("GreenApple", 200));
			
		grapeBox.add(new Grape3("GreenGrape", 400));
		grapeBox.add(new Grape3("GreenGrape", 300));
		grapeBox.add(new Grape3("GreenGrape", 200));
		
		Collections.sort(appleBox.getList(), new AppleComp());
		Collections.sort(grapeBox.getList(), new GrapeComp());
		System.out.println(appleBox);
		System.out.println(grapeBox);
		System.out.println();
		Collections.sort(appleBox.getList(), new FruitComp());
		Collections.sort(grapeBox.getList(), new FruitComp());
		System.out.println(appleBox);
		System.out.println(grapeBox);
	}	// main
}

class FruitBox3<T extends Fruit3> extends Box3<T> {}

class Box3<T> {
	ArrayList<T> list = new ArrayList<T>();
	
	void add(T item) {
		list.add(item);
	}
	
	T get(int i) {
		return list.get(i);
	}
	
	ArrayList<T> getList() { return list; }
	
	int size() {
		return list.size();
	}
	
	public String toString() {
		return list.toString();
	}
}
```

```
[GreenApple(300), GreenApple(200), GreenApple(100)]
[GreenGrape(400), GreenGrape(300), GreenGrape(200)]

[GreenApple(100), GreenApple(200), GreenApple(300)]
[GreenGrape(200), GreenGrape(300), GreenGrape(400)]
```

이 예제는 `Collections.sort()`를 이용해서 `appleBox`와 `grapeBox`에 담긴 과일을 무게별로 정렬한다. 이 메소드의 선언부는 다음과 같다.

``` java
static <T> void sort(List<T> list, Comparator<? super T> c)
```

`static` 옆에 있는 `<T>`는 메소드에 선언된 제네릭 타입이다. 이런 메소드를 제네릭 메소드라고 한다. 첫 번째 매개변수는 정렬한 대상이고, 두 번째 매개변수는 정렬할 방법이 정의된 `Comparator`이다. `Comparator`의 제네릭 타입에 하한 제한이 걸려있는 와일드 카드가 사용되었다. 먼저 다음과 같이 와일드 카드를 사용하지 않았다고 가정하겠다.

``` java
static <T> void sort(List<T> list, Comparator<T> c)
```

만일 타입 매개변수 `T`에 `Apple3`이 대입되면, 위의 정의는 아래와 같이 바뀐다.

``` java
static void sort(List<Apple3> list, Comparator<Apple3> c)
```

이것은 `List<Apple3>`을 정렬하기 위해서는 `Comparator<Apple3>`이 필요하다는 것을 의미한다. 그래서 `Comparator<Apple3>`을 구현한 `AppleComp`클래스를 아래처럼 정의하였다.

``` java
class AppleComp implements Comparator<Apple> {
    public int compare(Apple3 t1, Apple3 t2) {
        return t2.weight - t1.weight;
    }
}
```

`Apple3`대신 `Grape3`가 대입되어 `List<Grape3>`를 정렬하려면, `Comparator<Grape3>`가 필요하다. `Comparator<Apple3>`로는 `List<Grape3>`를 정렬할 수 없기 때문이다.

``` java
class GrapeComp implements Comparator<Grape3> {
	public int compare(Grape3 t1, Grape3 t2) {
		return t2.weight - t1.weight;
	}
}
```

`AppleComp`와 `GrapeComp`는 타입만 다를 뿐 완전히 같은 코드이다. 코드의 중복도 문제지만, 새로운 `Fruit`의 자손이 생길 때마다 위와 같은 코드를 반복해서 만들어야 한다는 것이 더 문제이다. 이 문제를 해결하기 위해서는 타입 매개변수에 하한 제한의 와일드 카드를 적용해야 한다. 앞서 살펴본 것과 같이 `sort()`는 원래 그렇게 정의되어 있다.

``` java
static <T> void sort(List<T> list, Comparator<? super T> c)
```

위의 문장에서 타입 매개변수 `T`에 `Apple3`이 대입되면 다음과 같이 된다.

``` java
static void sort(List<Apple3> list, Comparator<? super Apple3> c)
```

매개변수의 타입이 `Comparator<? extends Apple3>`이라는 의미는 `Comparator`의 타입 매개변수로 `Apple3`와 그 조상이 가능하다는 뜻이다. 즉, `Comparator<Apple3>`, `Comparator<Fruit>`, `Comparator<Object>` 중의 하나가 두 번째 매개변수로 올 수 있다는 뜻이다.

> **Comparator\<? super Apple3\>** : Comparator\<Apple3\>, Comparator\<Fruit3\>, Comparator\<Object\>   
> **Comparator\<? super Grape3\>** : Comparator\<Grape3\>, Comparator\<Fruit3\>,
Comparator\<Object\>

그래서 아래와 같이 `FruitComp`를 만들면, `List<Apple3>`과 `List<Grape3>`를 모두 정렬할 수 있다. 비교의 대상이 되는 `weight`는 `Apple3`과 `Grape3`의 조상인 `Fruit3`에 정의되어 있기 때문에 가능한 것이기도 하다.

``` java
class FruitComp implements Comparator<Fruit3> {
	public int compare(Fruit3 t1, Fruit3 t2) {
		return t1.weight - t2.weight;
	}
}
    ...
// List<Apple3>과 List<Grape3>를 모두 Comparator<Fruit3>으로 정렬
Collections.sort(appleBox.getList(), new FruitComp());
Collections.sort(grapeBox.getList(), new FruitComp());
```

이러한 장점 때문에 `Comparator`에는 항상 `<? super T>`가 습관적으로 따라 붙는다.

</br>

## 1.6 제네릭 메소드

메소드의 선언부에 제네릭 타입이 선언된 메소드를 제네릭 메소드라 한다. `Collections.sort()`가 제네릭 메소드이며, 제네릭 타입의 선언 위치는 반환타입 바로 앞이다.

``` java
static <T> void sort(List<T> list, Comparator<? super T> c)
```

제네릭 클래스에 정의된 타입 매개변수와 제네릭 메소드에 정의된 타입 매개변수는 전혀 별개의 것이다. 같은 타입 문자 `T`를 사용해도 같은 것이 아니라는 것에 주의해야 한다.

> 제네릭 메소드는 제네릭 클래스가 아닌 클래스에도 정의될 수 있다.

``` java
class FruitBox<T> {
        ...
    static <T> void sort(List<T> list, Comparator<? super T> c) {
        ...
    }
}
```

위의 코드에서 제네릭 클래스 `FruitBox`에 선언된 타입 매개변수 `T`와 제네릭 메소드 `sort()`에 선언된 타입 매개변수 `T`는 타입 문자만 같을 뿐 서로 다른 것이다. 그리고 `sort()`가 static메소드라는 것에 주목해야 한다. 앞서 설명한 것처럼, static멤버에는 타입 매개변수를 사용할 수 없지만, 이처럼 메소드에 제네릭 타입을 선언하고 사용하는 것은 가능하다.

메소드에 선언된 제네릭 타입은 지역 변수를 선언한 것과 같다고 생각하면 된다. 이 타입 매개변수는 메소드 내에서만 지역적으로 사용될 것이므로 메소드가 static이건 아니건 상관이 없다.

> 같은 이유로 내부 클래스에 선언된 타입 문자가 외부 클래스의 타입 문자와 같아도 구별될 수 있다.

앞서 나왔던 `makeJuice()`를 제네릭 메소드로 바꾸면 다음과 같다.

![image](https://ifh.cc/g/qN8fB0.png)

이제 이 메소드를 호출할 때는 아래와 같이 타입 변수에 타입을 대입해야 한다.

``` java
FruitBox<Fruit> fruitBox = new FruitBox<Fruit>();
FruitBox<Apple> fruitBox = new FruitBox<Apple>();
    ...
Syetem.out.println(Juicer.<Fruit>makeJuice(fruitBox));
Syetem.out.println(Juicer.<Apple>makeJuice(appleBox));
```

그러나 대부분의 경우 컴파일러가 타입을 추정할 수 있기 때문에 생략해도 된다. 위의 코드에서도 `fruitBox`와 `appleBox`의 선언부를 통해 대입된 타입을 컴파일러가 추정할 수 있다.

``` java
System.out.println(Juicer.makeJuice(fruitBox)); // 대입된 타입을 생략할 수 있다.
Syetem.out.println(Juicer.makeJuice(appleBox));
```

한 가지 주의할 점은 제네릭 메소드를 호출할 때, 대입된 타입을 생략할 수 없는 경우에는 참조변수나 클래스 이름을 생략할 수 없다는 것이다.

``` java
System.out.println(<Fruit>makeJuice(fruitBox)); // 에러. 클래스 이름 생략불가
System.out.println(this.<Fruit>makeJuice(fruitBox));    // OK
System.out.println(Juicer.<Fruit>makeJuice(fruitBox));  // OK
```

같은 클래스 내에 있는 멤버들끼리는 참조변수나 클래스이름, 즉 `this.`이나 `클래스이름.`을 생략하고 메소드 이름만으로 호출이 가능하지만, 대입된 타입이 있을 때는 반드시 써줘야 한다. 이것은 단지 기술적인 이유에 의한 규칙이다.

제네릭 메소드는 매개변수의 타입이 복잘할 때도 유용하다. 만일 아래와 같은 코드가 있다면 타입을 별도로 선언함으로써 코드를 간략히 할 수 있다.

![image](https://ifh.cc/g/9LNaTR.png)

이번엔 좀 복잡하게 선언된 제네릭 메소드 하나를 예를 들어보겠다. 아래의 메소드는 `Collections`클래스의 `sort()`인데, 이전의 `sort()`와 달리 매개변수가 하나짜리이다.

``` java
public static <T extends Comparable<? super T>> void sort(List<T> list)
```

매개변수로 지정한 `List<T>`를 정렬한다는 것은 알겠는데, 메소드에 선언된 제네릭 타입이 좀 복잡하다. 이럴 때는 일단 와일드 카드를 걷어내야 한다.

``` java
public static <T extends Comparable<T>> void sort(List<T> list)
```

`List<T>`의 요소가 `Comparable`인터페이스를 구현한 것이어야 한다는 뜻이다. 인터페이스락 해서 `implements`라고 쓰지 않는다.

이제 다시 와일드 카드를 넣어보겠다.

``` java
public static <T extends Comparable<? super T>> void sort(List<T> list)
```

![image](https://ifh.cc/g/TLzWHC.png)

① 타입 T를 요소로 하는 List를 매개변수로 허용한다.   
② 'T'는 Comparable을 구현한 클래스이어야 하며(\<T extends Comparable\>), 'T' 또는 그 조상의 타입을 비교하는 Comparable이어야 한다는 것(Comparable\<? super T\>)을 의미한다. 만일 T가 Student이고, Person의 자손이라면, \<? super T\>는 Student, Person, Object가 모두 가능하다.

</br>

## 1.7 제네릭 타입의 형변환

아래의 코드를 보겠다.

``` java
Box box = null;
Box<Object> objBox = null;

box = (Box)objBox;  // OK. 제네릭 타입 → 원시 타입. 경고 발생
objBox = (Box<Object>)box;  // OK. 원시 타입 → 제네릭 타입. 경고 발생
```

제네릭 타입과 넌제네릭(non-generic)타입간의 형변환은 항상 가능하다.

``` java
Box<Object> objBox = null;
Box<String> strBox = null;

objBox = (Box<Object>)strBox;   // 에러. Box<String> → Box<Object>
strBox = (Box<String>)objBox;   // 에러. Box<Object> → Box<String>
```

대입된 타입이 다른 제네릭 타입 간에는 형변환이 불가능하다. 대입된 타입이 `Object`일지라도 말이다. 아래의 문장이 안된단ㄴ 얘기는 `Box<String>`이 `Box<Object>`로 형변환될 수 없다는 사실을 간접적으로 알려준다.

``` java
// Box<Object> objBox = (Box<Object>)new Box<String>();
Box<Object> objBox = new Box<String>(); // 에러. 형변환 불가능
```

``` java
Box<? extends Object> wBox = new Box<String>();
```

`Box<String>`이 `Box<? extends Object>`로 형변환이 된다. 그래서 전에 배운 `makeJuice`메소드의 매개변수에 다형성이 적용될 수 있었던 것이다.

``` java
// 매개변수로 FruitBox<Fruit>, FruitBox<Apple>, FruitBox<Grape> 등이 가능
static Juice makeJuice(FruitBox<? extends Fruit> box) { ... }

FruitBox<? extends Fruit> box = new FruitBox<Fruit>();  // OK
FruitBox<? extends Fruit> box = new FruitBox<Apple>();  // OK
FruitBox<? extends Fruit> box = new FruitBox<Grape>();  // OK
```

반대로의 형변환도 성립되지만, 확인되지 않은 형변환이라는 경고가 발생한다. `FruitBox<? extends Fruit>`에 대입될 수 있는 타입이 여러 개인데다, `FruitBox<Apple>`를 제외한 다른 타입은 `FruitBox<Apple>`로 형변환될 수 없기 때문이다.

``` java
FruitBox<? extends Fruit> box = null;
// OK. 미확인 타입으로 형변환 경고
FruitBox<Apple> appleBox = (FruitBox<Apple>)box;
```

다음은 `java.util.Optional클래스의 실제 소스의 일부이다.

``` java
public final class Optional<T> {
    private static final Optional<?> EMPTY = new Optional<>();
    private final T value;
        ...
    public static <T> Optional<T> empty() {
        Optional<T> t = (Optional<T>)EMPTY;
        return t;
    }
        ...
}
```

static상수 `EMPTY`에 비어있는 `Optional`객체를 생성해서 저장했다가 `empty()`를 호출하면 `EMPTY`를 형변환해서 반환한다. 먼저 상수를 선언하는 문장을 단계별로 분석해보면 다음과 같다. 편의상 제어자는 생략하였다.

``` java
    Optional<?> EMPTY = new Optional<>();
→   Optional<? extends Object> EMPTY = new Optional<>();
→   Optional<? extends Object> EMPTY = new Optional<Object>();
```

`<?>`는 `<? extends Object>`를 줄여 쓴 것이며, \<\>안에 생략된 타입은 `?`가 아니라 `Object`이다.

``` java
Optional<?> EMPTY = new Optional<?>();  // 에러. 미확인 타입의 객체는 생성불가
Optional<?> EMPTY = new Optional<Object>(); // OK.
Optional<?> EMPTY = new Optional<>();   // OK. 위의 문장과 동일
```

> class Box\<T extends Fruit\>의 경우 Box\<?\> b = new Box\<\>;는 Box\<?\> b = new Box\<Fruit\>;이다.

위의 문장에서 `EMPTY`의 타입을 `Optional<Object>`가 아닌 `Optional<?>`로 한 이유는 `Optional<T>`로 형변환이 가능하기 때문이다.

``` java
Optional<?> wopt = new Optional<Object>();
Optional<Object> oopt = new Optional<Object>();

Optional<String> sopt = (Optional<String>)wopt; // OK. 형변환 가능
Optional<String> sopt = (Optional<String>)oopt; // 에러. 형변환 불가
```

`empty()`의 반환 타입이 `Optional<T>`이므로 `EMPTY`를 `Optional<T>`로 형변환해야 하는데, 위의 코드에서 알 수 있는 것처럼 `Optional<Object>`는 `Optional<T>`로 형변환이 불가능하다.

``` java
public static<T> Optional<T> empty() {
    Optional<T> t = (Optional<T>) EMPTY;    // Optional<?> → Optional<T>
    return t;
}
```

정리하면, `Optional<Object>`를 `Optional<String>`으로 직접 형변환하는 것은 불가능하지만, 와일드 카드가 포함된 제네릭 타입으로 형변환하면 가능하다. 대신 확인되지 않은 타입으로의 형변환이라는 경고가 발생한다.

``` java
Optional<Object> → Optional<T>  // 형변환 불가능.
Optional<Object> → Optional<?> → Optional<T>    // 형변환 가능. 경고발생
```

다음과 같이 와일드 카드가 사용된 제네릭 타입끼리도 다음과 같은 경우에는 형변환이 가능하다.

``` java
FruitBox<? extends Object> objBox = null;
FruitBox<? extends String> strBox = null;

strBox = (FruitBox<? extends String>)objBox;    // OK. 미확정 타입으로 형변환 경고
objBox = (FruitBox<? extends Objcet>)strBox;    // OK. 미확정 타입으로 형변환 경고
```

형변환이 가능하긴 하지만, 와일드 카드는 타입이 확정된 타입이 아니므로 컴파일러는 미확정 타입으로 형변환하는 것이라고 경고한다.

</br>

## 1.8 제네릭 타입의 제거

컴파일러는 제네릭 타입을 이용해서 소스파일을 체크하고, 필요한 곳에 형변환을 넣어준다. 그리고 제네릭 타입을 제거한다. 즉, 컴파일된 파일(*.class)에는 제네릭 타입에 대한 정보가 없는 것이다.

이렇게 하는 주된 이유는 제네릭이 도입되기 이전의 소스 코드와의 호환성을 유지하기 위해서이다. JDK1.5부터 제네릭스가 도입되었지만, 아직도 원시 타입을 사용해서 코드를 작성하는 것을 허용한다.

기본적인 제거과정에 대해서만 살펴보겠다.

**1. 제네릭 타입의 경계(bound)를 제거한다.**   

제네릭 타입 `<T extends Fruit>`라면 `T`는 `Fruit`로 치환된다. `<T>`인 경우는 `T`는 `Object`로 치환된다. 그리고 클래스 옆의 선언은 제거된다.

![image](https://ifh.cc/g/ksBtzZ.png)

**2. 제네릭 타입을 제거한 후에 타입이 일치하지 않으면, 형변환을 추가한다.**

`List`의 `get()`은 `Object`타입을 반환하므로 형변환이 필요하다.

![image](https://ifh.cc/g/tpZ4oq.png)

와일드 카드가 포함되어 있는 경우에는 다음과 같이 적절한 타입으로의 형변환이 추가된다.

![image](https://ifh.cc/g/9RM5hD.png)