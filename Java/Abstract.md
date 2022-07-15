# Abstract

</br>

## abstract

`abstract`란 한국어로는 추상으로 번역된다. 이에 대한 정의는 뒤에서 내리도록 하고 지금 단계에서는 `abstract`라는 것이 상속을 강제하는 일종의 규제라고 생각하자. 즉 `abstract` 클래스나 메소드를 사용하기 위해서는 반드시 상속해서 사용하도록 강제하는 것이 `abstract`다. 

</br>

## 추상 메소드

추상 메소드란 메소드의 시그니처만이 정의된 비어있는 메소드를 의미한다.

``` java
package abstractclass.example1;

abstract class A{	// abstract 클래스는 상속을 강제한다.
    public abstract int b();	// abstract 메소드는 오버라이딩을 강제한다.
    //본체가 있는 메소드는 abstract 키워드를 가질 수 없다.
    //public abstract int c(){System.out.println("Hello")}
    //추상 클래스 내에는 추상 메소드가 아닌 메소드가 존재 할 수 있다. 
    public void d(){
        System.out.println("world");
    }
}
public class AbstractDemo {
    public static void main(String[] args) {
//        A obj = new A();	// 상속과 오버라이딩이 되지 않아 에러가 발생한다.
    }
}
```

위 코드의 실행 결과는 아래와 같다.

``` java
Exception in thread "main" java.lang.Error: Unresolved compilation problem: 
    Cannot instantiate the type A
 
    at org.opentutorials.javatutorials.abstractclass.example1.AbstractDemo.main(AbstractDemo.java:7)
```

 메소드 `b`의 선언 부분에는 `abstract`라는 키워드가 등장하고 있다. 이 키워드는 메소드 `b`는 메소드의 시그니처만 정의 되어 있고 이 메소드의 구체적인 구현은 하위 클래스에서 오버라이딩 해야 한다는 의미다. 이렇게 내용이 비어있는 메소드를 추상 메소드라고 부른다. 추상 메소드를 하나라도 포함하고 있는 클래스는 추상 클래스가 되고, 자연스럽게 클래스의 이름 앞에 `abstract`가 붙는다. 

``` java
 abstract class A{
    public abstract int b();
}
```

아래 코드는 오류를 발생시키는데 본체인 `{System.out.println("Hello")}`가 존재하는데 추상 메소드를 의미하는 `abstract`를 사용하고 있기 때문이다.

``` java
public abstract int c(){System.out.println("Hello")}
```

추상 클래스에는 추상 메소드가 아닌 메소드가 존재할 수 있다.

``` java
public int d(){
    System.out.println("world");
}
```

아래와 같이 추상 클래스 `A`를 인스턴스화하면 오류가 발생한다. 그것은 추상 클래스는 구체적인 메소드의 내용이 존재하지 않기 때문에 인스턴스화시켜서 사용할 수 없기 때문이다. 그럼 어떻게 해야 클래스 `A`를 사용할 수 있을까? 또 이렇게 불편한 추상 클래스는 왜 사용하는 것일까?

``` java
A obj = new A();
```

</br>

## 추상 클래스의 상속

위의 문제를 해결하기 위해서는 클래스 `A`를 상속한 하위 클래스를 만들고 추상 메소드를 오버라이드해서 내용있는 메소드를 만들어야 한다.

``` java
package abstractclass.example2;
abstract class A{
    public abstract int b();
    public void d(){
        System.out.println("world");
    }
}
class B extends A{	// abstract 클래스인 A를 상속하는 B 자식 클래스를 생성해야 한다.
    public int b(){return 1;}	// abstract 메소드인 b()를 오버라이딩해야 한다.
}
public class AbstractDemo {
    public static void main(String[] args) {
        B obj = new B();	// 상속받은 자식 클래스를 obj로 인스턴스함.
        System.out.println(obj.b());	// B 클래스의 메소드 b() 호출
    }
}
```

클래스 `B`는 클래스 `A`를 상속했다. 그리고 클래스 `A`의 추상 메소드인 메소드 `b`를 오버라이딩하고 있다. 그 결과 클래스 `A`를 사용할 수 있었다.

</br>

## 추상 클래스를 사용하는 이유

추상 클래스는 상속을 강제하기 위한 것이다. 즉 부모 클래스에는 메소드의 시그니처만 정의해놓고 그 메소드의 실제 동작 방법은 이 메소드를 상속 받은 하위 클래스의 책임으로 위임하고 있다. 사실 코드를 이런 식으로 작성하는 경우는 작은 규모의 프로젝트에서는 거의 없다.

아래 코드는 [계산기 예제](https://opentutorials.org/module/516/5400#Calculator.java)에 추상 클래스의 개념을 도입한 것이다.

``` java
package abstractclass.example3;

abstract class Calculator{
    int left, right;
    public void setOprands(int left, int right){
        this.left = left;
        this.right = right;
    } 
    public abstract void sum();  
    public abstract void avg();
    public void run(){
        sum();	// 추상 메소드 sum을 호출
        avg();	// 추상 메소드 avg를 호출
    }
}
class CalculatorDecoPlus extends Calculator {
    public void sum(){	// sum() 메소드를 오버라이딩
        System.out.println("+ sum :"+(this.left+this.right));
    }
    public void avg(){	// avg() 메소드를 오버라이딩
        System.out.println("+ avg :"+(this.left+this.right)/2);
    }
} 
class CalculatorDecoMinus extends Calculator {
    public void sum(){	// sum() 메소드를 오버라이딩
        System.out.println("- sum :"+(this.left+this.right));
    }
    public void avg(){	// avg() 메소드를 오버라이딩
        System.out.println("- avg :"+(this.left+this.right)/2);
    }
} 
public class CalculatorDemo {
    public static void main(String[] args) { 
        CalculatorDecoPlus c1 = new CalculatorDecoPlus();
        c1.setOprands(10, 20);	// CalculatorDecoPlus 클래스에는 setOprands 메소드가 없기 때문에 부모 클래스의 setOprands 메소드를 호출한다.
        c1.run();	// CalculatorDecoPlus 클래스에는 run 메소드가 없기 때문에 부모 클래스의 run 메소드를 호출한다.
        // 자식 클래스에는 run 메소드가 호출하는 sum(), avg() 메소드가 오버라이딩 되어있어서 자식 클래스의 sum(),avg() 메소드를 호출한다.
         
        CalculatorDecoMinus c2 = new CalculatorDecoMinus();
        c2.setOprands(10, 20);
        c2.run();
    }
   
}
```

결과는 다음과 같다.

``` java
+ sum :30
+ avg :15
- sum :30
- avg :15
```

위의 예제는 합계(`sum`)를 실행하고 평균(`avg`)을 실행하는 절차를 메소드 `run`을 통해서 한 번에 실행되도록 한 코드이다. 그런데 경우에 따라서 합계와 평균을 화면에 출력하는 모습을 달리해야 하는 경우가 있다고 치자. 그런 경우에 상황에 따라서 동작 방법이 달라지는 메소드(`sum`, `avg`)는 추상 메소드로 만들어서 하위 클래스에서 구현하도록 하고 모든 클래스의 공통분모(`setOprands`, `run`)의 경우에는 상위 클래스에 두어서 코드의 중복, 유지보수의 편의성 등을 꾀할 수 있다.

</br>

## 디자인 패턴

이러한 개발 방법을 template method pattern이라고도 한다. 아래는 추억의 템플릿이다.

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/516/1972.png)

위의 그림에 등장하는 템플릿은 자주 사용하는 모양을 모아둔 것이라고 할 수 있다. 템플릿은 모양을 결정하지만 템플릿을 통해서 그려질 도형은 팬의 종류나 색상에 따라서 달라진다. 즉 공통분모인 메소드 `run`은 메소드 `sum`과 `avg`가 어떻게 동작할지 알 수 없지만 `sum`이 실행되고 `avg`을 실행시킨다. 반면에 실행결과를 어떤 기호(+,-)로 시작할지는 하위 클래스에서 결정하고 있다.

즉, 위의 예제를 통해서도 알 수 있지만 프로그래밍이라는 것은 반복되는 패턴이 있다. 이런 패턴들을 모아서 정리한 것이 디자인 패턴(design pattern)이다. 물론 시각 디자이너들의 디자인이 아니라 좋은 소프트웨어를 만들기 위한 설계로서 디자인이라는 표현을 쓰고 있는 것이다. 디자인 패턴의 장점은 크게 두가지이다. 하나는 좋은 설계를 단기간에 학습할 수 있다는 점이다. 물론 비교적 단기간이라는 뜻이다. 다른 하나는 소통에 도움이 된다는 점이다. 설계 방법을 토의하거나 전달할 때 설계 방법에 따라 적절한 이름이 있다면 상호간에 생각을 일치시키는 데 큰 도움이 된다.