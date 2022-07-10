# 상속

</br>

## 상속이란?

객체지향을 통해서 달성하고자 하는 목표 중에서 가장 중요한 것은 재활용성일 것이다. 상속은 객체지향의 재활용성을 극대화시킨 프로그래밍 기법이라고 할 수 있다. 동시에 객체지향을 복잡하게 하는 주요 원인이라고도 할 수 있다.

상속(Inheritance)이란 물려준다는 의미다. 어떤 객체가 있을 때 그 객체의 필드(변수)와 메소드를 다른 객체가 물려 받을 수 있는 기능을 상속이라고 한다.

객체지향 수업의 [첫 번째 예제인 `CalculatorDemo`](https://opentutorials.org/module/516/5400#Calculator.java) 이 예제에서 등장하는 객체 `Calculator`는 더하기와 평균에 해당하는 `sum`과 `avg` 메소드를 가지고 있다. 그런데 이 객체가 가지고 있는 기능에 빼기를 추가하고 싶다. 가장 쉬운 방법은 이 객체에 빼기를 의미하는 `substract`를 추가해서 아래와 같이 사용하면 되는데

``` java
Calculator c1 = new Calculator();
c1.setOprands(10, 20);
c1.sum();
c1.avg(); 
c1.substract();
```

만약 아래와 같은 경우에 속한다면 객체에 메소드를 추가하는 것이 어렵다.

1. 객체를 자신이 만들지 않았다. 그래서 소스를 변경할 수 없다. 변경 할 수 있다고 해도 원 소스를 업데이트 하면 메소드 substarct이 사라진다. 이러한 문제가 일어나지 않게 하기 위해서는 지속적으로 코드를 관리해야 한다.

2. 객체가 다양한 곳에서 활용되고 있는데 메소드를 추가하면 다른 곳에서는 불필요한 기능이 포함될 수 있다. 이것은 자연스럽게 객체를 사용하는 입장에서 몰라도 되는 것까지 알아야 하는 문제가 된다.

기존의 객체를 그대로 유지하면서 어떤 기능을 추가하는 방법이 상속이다. 즉 기존의 객체를 수정하지 않으면서 새로운 객체가 기존의 객체를 기반으로 만들어지게 되는 것이다. 이때 기존의 객체는 기능을 물려준다는 의미에서 부모 객체가 되고 새로운 객체는 기존 객체의 기능을 물려받는다는 의미에서 자식 객체가 된다.

> 부모 클래스와 자식 클래스의 관계를 상위(super) 클래스와 하위(sub) 클래스라고 표현하기도 한다. 또한 기초 클래스(base class), 유도 클래스(derived class)라고도 부른다. 

``` java
package Inheritance.example1;
 
class Calculator {
    int left, right;
 
    public void setOprands(int left, int right) {
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
 
class SubstractionableCalculator extends Calculator {	// Calculator 부모 클래스로부터 상속 받은 SubstractionableCalculator 자식 클래스는 부모 클래스의 변수 및 메소드를 사용할 수 있다.
    public void substract() {
        System.out.println(this.left - this.right);	// this.left와 this.right 변수는 SubstractionableCalculator 클래스에 선언이 안되어 있기 때문에 부모 클래스의 변수를 사용한다.
    }
}
 
public class CalculatorDemo1 {
 
    public static void main(String[] args) {
 
        SubstractionableCalculator c1 = new SubstractionableCalculator();
        c1.setOprands(10, 20);	// Calculator 클래스의 기존 메소드
        c1.sum();	// Calculator 클래스의 기존 메소드
        c1.avg();	// Calculator 클래스의 기존 메소드
        c1.substract();	// SubstractionableCalculator 클래스에서 추가로 생성한 메소드
    }
 
}
```

실행결과는 아래와 같다.

``` java
30
15
-10
```

위의 코드를 하나씩 분해해서 본다면,

``` java
class SubstractionableCalculator extends Calculator {
    public void substract() {
        System.out.println(this.left - this.right);
    }
}
```

우선 새로운 클래스인 `SubstractionableCalculator`을 정의했다. 이 클래스의 본체에는 `sbstract`라는 메소드만이 존재한다. 하지만 이 클래스를 인스턴스화한 `c1`은 아래와 같이 정의하지 않은 메소드들을 호출하고 있고, 잘 동작한다.

``` java
SubstractionableCalculator c1 = new SubstractionableCalculator();
c1.setOprands(10, 20);
c1.sum();
c1.avg();
c1.substract();
```

이것이 가능한 이유는 `extends Calculator` 때문이다. 이것은 클래스 `Calculator`를 상속 받는다는 의미다. 따라서 `SubstaractableCalculator`는 `Calculator`에서 정의한 메소드 `setOprands`, `sub`, `avg`를 사용할 수 있게 된다. 이것이 프로그래밍의 역사에서 대단한 진전으로 평가받는 상속의 기본적인 의미다. 상속을 통해서 코드의 중복을 제거할 수 있었고, 또 부모 클래스을 개선하면 이를 상속받고 있는 모든 자식 클래스들에게 그 혜택이 자동으로 돌아간다. 다시 말해서 유지보수가 편리해진다는 것이다.  재활용성과 중복의 제거, 그리고 유지보수의 편의는 서로 다른 목적으로 가지고 있지만, 하나가 좋아지면 자연스럽게 다른 쪽도 좋아지는 관계에 있다는 것을 다시 한 번 환기해주는 대목이다.

생각을 조금 더 말랑말랑하게 하기 위해서 Calculator을 상속 받는 클래스를 하나 더 만들어보면, 이 클래스는 곱하기를 할 수 있는 클래스다.

``` java
package Inheritance.example1;
 
class MultiplicationableCalculator extends Calculator {	// MultiplicationableCalculator 자식 클래스는 Calculator 부모 클래스로부터 상속을 받아 부모 클래스의 필드, 메소드를 호출할 수 있다.
    public void multiplication() {
        System.out.println(this.left * this.right);	// 부모 클래스의 인스턴스 변수인 this.left, this.right를 호출하여 사용함.
    }
}
 
public class CalculatorDemo2 {
 
    public static void main(String[] args) {
 
        MultiplicationableCalculator c1 = new MultiplicationableCalculator();
        c1.setOprands(10, 20);	// 부모 클래스의 메소드 사용
        c1.sum();	// 부모 클래스의 메소드 사용
        c1.avg();	// 부모 클래스의 메소드 사용
        c1.multiplication();	// 자식 클래스의 메소드 사용
    }
 
}
```

결과는 아래와 같다.

``` java
30
15
200
```

그리고 상속한 클래스를 다시 상속할 수 있다. 아래의 예제는 곱하기가 가능한 클래스인 `MultiplicationableCalculator`을 상속받고 있다.

``` java
package Inheritance.example1;
 
class DivisionableCalculator extends MultiplicationableCalculator {	// DivisionableCalculator 자식 클래스는 MultiplicationableCalculator 부모 클래스로부터 상속을 받아 부모 클래스의 필드, 메소드를 호출할 수 있다. 
    public void division() {
        System.out.println(this.left / this.right);	// DivisionableCalculators 클래스는 자신의 메소드 division()를 생성하였고, 이 메소드는 자신의 부모 클래스의 부모 클래스인 Calculator 클래스의 인스턴스 변수를 호출하여 사용한다.
    }
    // 하나의 부모 클래스로부터 여러 개의 자식 클래스는 상속을 받을 수 있고, 상속 받은 자식 클래스는 자신이 부모 클래스가 되어 자신의 자식 클래스에게 상속할 수 있다. 이렇게 상속은 무궁무진하게 사용이 가능하다.
}
 
public class CalculatorDemo3 {
 
    public static void main(String[] args) {
 
        DivisionableCalculator c1 = new DivisionableCalculator();
        c1.setOprands(10, 20);
        c1.sum();
        c1.avg();
        c1.multiplication();
        c1.division();
    }
 
}
```

이것이 상속의 기본적인 개념이다. 하지만 장점이 있으면 단점도 있는 법이다. 프로그래밍의 세계에서는 이 상속의 효용을 수용하기 위해서 꽤나 많은 대가를 치러야 했다. 그 대가를 한마디로 표현하자면 복잡도의 증가라고 이야기할 수 있다.