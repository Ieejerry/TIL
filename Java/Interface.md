# 인터페이스

</br>

## 인터페이스란?

인터페이스(interface)는 다소 추상적인 개념이다. 그래서 공학적으로 자바의 기능으로서 인터페이스를 받아들이는게 좋은 방법이다.

인터페이스는 `abstract`, `final`와 함께 대표적인 규제이다. 인터페이스의 역할은 이렇다. 어떤 클래스가 있고 그 클래스가 특정한 인터페이스를 사용한다면 그 클래스는 반드시 인터페이스의  메소드들을 구현해야 한다. 만약 인터페이스에서 강제하고 있는 메소드를 구현하지 않으면 이 에플리케이션은 컴파일 조차 되지 않는다.

### 예제

우선 단순한 예를 보자.

``` java
package interfaces.example1;
 
interface I{
    public void z();
}
 
class A implements I{
    public void z(){}
}
```

클래스 `A` 뒤의 `implements` `I`는 이 클래스가 인터페이스 `I`를 구현하고 있다는 의미다. 그것은 3행의 `interface` `I`의 맴버인 `public void z()` 메소드를 클래스 `A`가 반드시 포함하고 있어야 한다는 뜻이다. 따라서 위의 코드는 문제가 없다. 인터페이스의 의미를 좀 더 분명하게 하기 위해서 8행의 `public void z(){}`를 삭제하겠다. 그러면 컴파일 에러가 발생하게 된다. 

인터페이스와 상속은 다르다. 상속이 상위 클래스의 기능을 하위 클래스가 물려 받는 것이라고 한다면, 인터페이스는 하위 클래스에 특정한 메소드가 반드시 존재하도록 강제한다.

또 사용하는 키워드도 다르다. 클래스를 선언 할 때는 `class`를 사용하지만 인터페이스는 `interface`를 사용한다.

또 상속은 `extends`를 사용하지만 인터페이스는 `implements`를 사용한다. 이를 바탕으로 위의 예제를 해설해보면 아래와 같다.

> 클래스 `A`는 인터페이스 `I`를 '구현' 한다.

</br>

## 실질적인 쓰임

[계산기 예제](https://opentutorials.org/module/516/5400#Calculator.java)에 인터페이스를 도입해보겠다. 계산기 기능이 필요한 프로젝트를 진행하는데 시간이 촉박하다. 그래서 계산기 클래스는 개발자 A가 만들고, 개발자 B는 그 클래스를 사용하는 로직을 만들다고 해보자. 이런 경우 개발자 B는 개발자 A가 계산기를 잘 만들어서 나중에 제출할 것이라고 기대하고 개발을 진행할 것이다. 그리고 아래와 같이 가짜 로직을 만들어서 코드를 작성했다고 가정해보겠다.

``` java
package interfaces.example1;
class CalculatorDummy{	// 가짜 계산기 클래스를 생성
    public void setOprands(int first, int second, int third){}
    public int sum(){
        return 60;
    }
    public int avg(){
        return 20;
    }
}
public class CalculatorConsumer {
    public static void main(String[] args){
        CalculatorDummy c = new CalculatorDummy();	// 가짜 계산기 클래스로 사용 로직 구현
        c.setOprands(10,20,30);	// 사용 로직을 세 개의 인자를 받아서
        System.out.println(c.sum()+c.avg());	// sum()과 avg()이 값이 나오도록 구현
    }
}
```

개발자 A가 `Calculator`를 만드는데 3개월이 필요하다고 한다면 그 시간을 단축하기 위해서 위와 같은 코드를 작성하는 이유가 공감 할 수 있을 것이다. 3개월이 지나고 개발자 A가 `Calculator` 클래스를 완성해서 인계해줬다 가정해보겠다. 아래는 그 코드다.

``` java
package interfaces.example1;
 
class Calculator {	// 실제 계산기 로직 클래스
    int left, right;
    public void setOprands(int left, int right) {	// 두 개의 매개변수가 받을 수 있게 구현
        this.left = left;
        this.right = right;
    }
    public void sum() {
        System.out.println(this.left + this.right);
    }
    public void avg() {
        System.out.println((this.left + this.right) / 2);
    }
}
```

개발자 A는 `setOprands`의 매개변스를 2개 받고 있지만 개발자 B는 이 메소드가 변수 3개를 받을 것이라고 생각한 것이다. 이건 마치 해저터널의 공사가 중간에서 만나지 않은 것과 같은 상황이다. 이때부터 신경전이 시작된다. 경우에 따라서는 치열하게 다투게 되고 프로젝트는 파국으로 치닫는다. 이러한 문제를 해결하기 위한 가장 좋은 방법은 협업자 상호간에 구체적인 약속을 하면 된다. 특히 그 약속을 코드 안에서 할 수 있다면 참 좋을 것이다. 이럴 경우, 인터페이스가 필요한 순간이다. 

클래스 `Calculator`를 사용할 개발자가 이 클래스가 가지고 있어야 할 메소드를 인터페이스로 만들어서 제공하는 것이다. 반대의 경우도 가능하다. 만드는 쪽에서 인터페이스를 제공하면 된다. 양쪽의 개발자는 이 인터페이스를 구현한 클래스 `Calculator`와 `CalculatorDummy`를 각각 구현하면 된다.

이렇게 해서 만들어진 코드를 보자. 아래는 약속을 정의하고 있는 인터페이스이다.

``` java
package interfaces.example2;
 
public interface Calculatable {
    public void setOprands(int first, int second, int third);	// setOprands 메소드는 int형 세 개의 매개변수를 가져야하고,
    public int sum();	// int형으로 반환하는 sum() 메소드, 
    public int avg();	// int형으로 반환하는 avg() 메소드를 가져야한다고 규제함.
}
```

다음은 인터페이스를 구현한 가짜 클래스를 임시로 사용해서 만든 에플리케이션이다.

``` java
package interfaces.example2;
class CalculatorDummy implements Calculatable{	// 가짜 계산기 클래스는 Calculatable 인터페이스를 구현함.
    public void setOprands(int first, int second, int third){
    }
    public int sum(){
        return 60;
    }
    public int avg(){
        return 20;
    }
}
// 인터페이스로 인해 규제가 되었기 때문에 규제에 맞춰서 구현이 가능함.
public class CalculatorConsumer {
    public static void main(String[] args) {	// 사용 로직을 개발하는 입장에서는 구현 규제가 잘 정해져있기 때문에 안심하고 사용 로직을 잘 구현할 수가 있다.
        CalculatorDummy c = new CalculatorDummy();
        c.setOprands(10, 20, 30);
        System.out.println(c.sum()+c.avg());
    }
}
```

다음 코드는 인터페이스에 따라서 구현된 클래스이다.

``` java
package interfaces.example2;
 
class Calculator implements Calculatable {	// 인터페이스를 구현하고 있기 때문에 계산기 로직 개발자도 규제에 맞춰 더 잘 구현할 수 있다.
    int first, second, third;
    public void setOprands(int first, int second, int third) {
        this.first = first;
        this.second = second;
        this.third = third;
    }
    public int sum() {
        return this.first + this.second + this.third;
    }
    public int avg() {
        return (this.first + this.second + this.third) / 3;
    }
}
// 인터페이스로 인해 규제가 정해져있기 때문에 계산기 로직 클래스를 사용 로직에 그대로 결합을 하여도 아무 문제가 없을 거라는 보장이 있기 때문에
// 서로 안심하고 각각의 역할을 더 잘 수행할 수 있게 된다.
```

이제 해야 할 일은 가짜 클래스인 `CalculatorDummy`를 실제 로직으로 교체하면 된다.

``` java
package interfaces.example2;
public class CalculatorConsumer {
    public static void main(String[] args) {
        Calculator c = new Calculator();    // 완성된 계산기 로직 클래스를 인스턴스해주면 문제없이 실행이 된다.
        c.setOprands(10, 20, 30);
        System.out.println(c.sum()+c.avg());
    }
}
```

이렇게해서 인터페이스를 이용한 협업에 대해서 알아봤다. 인터페이스를 이용해서 서로가 동일한 메소드를 만들도록 규약을 만들어서 공유한 결과 각자가 상대의 일정이나 구현하는 방식에 덜 영향을 받으면서 에플리케이션을 구축 할 수 있게 된다.

</br>

## 인터페이스의 규칙

인터페이스의 몇가지 규칙을 더 알아보겠다.

### 하나의 클래스가 여러개의 인터페이스를 구현 할 수 있다. 

클래스 `A`는 메소드 `x`나 `z` 중 하나라도 구현하지 않으면 오류가 발생한다.

``` java
package interfaces.example3;
 
interface I1{
    public void x();
}
 
interface I2{
    public void z();
}
 
class A implements I1, I2{	// 인터페이스는 클래스 상속과는 다르게 여러 개의 인터페이스를 구현할 수 있다.
    public void x(){}	// 인터페이스 I1에 정의된 메소드 x()를 반드시 구현해야 된다.
    public void z(){}   // 인터페이스 I2에 정의된 메소드 z()를 반드시 구현해야 한다.
}
```

### 인터페이스도 상속이 된다.

``` java
package interfaces.example3;
 
interface I3{
    public void x();
}
 
interface I4 extends I3{	// 인터페이스도 상속을 할 수 있다. 인터페이스 I4는 인터페이스 I3를 상속하고 있다.
    public void z();
}
 
class B implements I4{	// 클래스 B는 인터페이스 I4를 구현함.
    public void x(){}	// 인터페이스 I4는 인터페이스 I3를 상속하였기 때문에 인터페이스 I4를 구현할 때에는 부모 인터페이스에 정의된 메소드 x() 메소드도 구현해야 된다.
    public void z(){}   // 인터페이스 I4에 정의된 메소드 z()를 반드시 구현해야 된다.
}
```

### 인터페이스의 맴버는 반드시 public이다.

아래 코드는 오류를 발생한다. 인터페이스는 그 인터페이스를 구현한 클래스를 어떻게 조작할 것인가를 규정한다. 그렇기 때문에 외부에서 제어 할 수 있는 가장 개방적인 접근 제어자인 `public`만을 허용한다. `public`을 생략하면 접근 제어자 `default`가 되는 것이 아니라 `public`이 된다. 왜냐하면 인터페이스의 맴버는 무조건 `public`이기 때문이다.

``` java
package interfaces.example3;
 
interface I5{
    private void x();
}
// 인터페이스는 그 인터페이스를 구현한 클래스를 어떻게 조작할 것인가를 규정하기 때문에
// 모든 외부에서 제어할 수 있는 가장 개방적인 접근 제어자인 `public`만을 허용한다.
// 위의 코드는 인터페이스에 private 메소드를 정의하였기 때문에 에러가 발생하게 된다.
```

</br>

## abstract vs interface

인터페이스와 추상 클래스는 서로 비슷한 듯 다른 기능이다. 인터페이스는 클래스가 아닌 인터페이스라는 고유한 형태를 가지고 있는 반면 추상 클래스는 일반적인 클래스다. 또 인터페이스는 구체적인 로직이나 상태를 가지고 있을 수 없고, 추상 클래스는 구체적인 로직이나 상태를 가지고 있을 수 있다.