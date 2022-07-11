# 상속과 생성자

편리함을 위해서 어떠한 기능을 수용하면 그 기능이 기존의 체계와 관계하면서 다양한 문제를 발생시킨다. 그 문제를 한마디로 줄여서 말하면 복잡도의 증가라고 할 수 있다. 예를 들면 생성자가 상속을 만나면서 발생한 복잡성이 있다. 그래서 super라는 키워드의 의미도 중요하다. 

기본 생성자의 성질에 대한 이해를 돕기 위해 아래의 예제를 보겠다.

``` java
package Inheritance.example2;
public class ConstructorDemo {	// 어떠한 생성자도 존재하지 않으면, java는 자동으로 기본 생성자를 생성해준다.
	// 매개변수가 없이 클래스 이름과 동일한 메소드가 기본 생성자이다. 기본 생성자는 내용이 비어있다.
    public static void main(String[] args) {
        ConstructorDemo  c = new ConstructorDemo();
    }
}
```

위의 예제는 에러를 발생시키지 않는다. `ConstructorDemo` 객체를 생성할 때 자동으로 생성자를 만들어주기 때문이다. 하지만 아래의 예제는 에러가 발생한다.

``` java
package Inheritance.example2;
public class ConstructorDemo2 {
    public ConstructorDemo2(int param1) {}	// 기본 생성자가 아닌 생성자, 즉 매개변수가 있는 생성자를 생성했다.
    // 어떠한 생성자가 명시적으로 만들어지면, java는 기본 생성자를 자동으로 생성해주지 않는다.
    public static void main(String[] args) {
//        ConstructorDemo2  c = new ConstructorDemo2();	// 기본 생성자를 생성해주지 않는데, 기본 생성자를 호출하여 에러가 발생하게 된다.
    }
}
```

매개변수가 있는 생성자가 있을 때는 자동으로 기본 생성자를 만들어주지 않는다. 따라서 위의 예제는 존재하지 않는 생성자를 호출하고 있다. 이 문제를 해결하기 위해서는 아래와 같이 기본 생성자를 추가해줘야 한다.

``` java
package Inheritance.example2;
public class ConstructorDemo3 {
    public ConstructorDemo3(){}	// 기본 생성자가 아닌 다른 생성자가 존재할 시에는 명시적으로 기본 생성저라를 생성해줘야한다.
    public ConstructorDemo3(int param1) {}
    public static void main(String[] args) {
        ConstructorDemo3  c = new ConstructorDemo3();
    }
}
```

[상속 토픽의 첫 번째 예제](https://opentutorials.org/module/516/6060#CalculatorDemo1)를 조금 수정해서 생성자를 통해서 left, right의 값을 설정한다.

``` java
package Inheritance.example2;
 
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
 
class SubstractionableCalculator extends Calculator {
    public SubstractionableCalculator(int left, int right) {	// SubstractionableCalculator 클래스에 매개변수가 있는 생성자를 생성.
        this.left = left;
        this.right = right;
    }
 
    public void substract() {
        System.out.println(this.left - this.right);
    }
}
 
public class CalculatorConstructorDemo {
    public static void main(String[] args) {
        SubstractionableCalculator c1 = new SubstractionableCalculator(10, 20);	// 인자를 넣어주어, 생성자 호출
        c1.sum();
        c1.avg();
        c1.substract();
    }
}
```

실행결과는 아래와 같다.

``` java
30
15
-10
```

`SubstractionableCalculator`의 생성자로 `left`와 `right`의 값을 받아서 초기화시키고 있다. 만약 클래스 `Calculator`가 메소드 `setOprands`가 아니라 생성자를 통해서 `left`, `right` 값을 설정하도록 하고 싶다면 아래와 같이 코드를 변경해야 할 것이다.

``` java
package Inheritance.example2;

class Calculator2 {	// 기본 생성자가 존재하지 않는다. java는 어떠한 생성자가 명시되어 있는 경우, 자동으로 기본 생성자를 생성해주지 않는다.
    int left, right;
    // 자식 클래스가 부모 클래스의 기본 생성자를 호출하는데, 기본 생성자가 존재하지 않아 에러가 발생한다.
    
    public Calculator2(int left, int right){
        this.left = left;
        this.right = right;
    }
     
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
 
class SubstractionableCalculator2 extends Calculator2 {	// 자식 클래스의 생성자가 호출되면, 자식 클래스는 부모 클래스의 생성자를 자동으로 호출하도록 되어있다.
    public SubstractionableCalculator2(int left, int right) {
        this.left = left;
        this.right = right;
    }
 
    public void substract() {
        System.out.println(this.left - this.right);
    }
}
 
public class CalculatorConstructorDemo2 {
    public static void main(String[] args) {
        SubstractionableCalculator2 c1 = new SubstractionableCalculator2(10, 20);	// 자식 클래스의 생성자를 호출.
        c1.sum();
        c1.avg();
        c1.substract();
    }
}
```

위의 코드를 실행하면 오류가 발생한다. 오류의 내용은 아래와 같다.

``` java
Exception in thread "main" java.lang.Error: Unresolved compilation problem: 
    Implicit super constructor Calculator() is undefined. Must explicitly invoke another constructor
 
    at org.opentutorials.javatutorials.Inheritance.example3.SubstractionableCalculator.<init>(CalculatorConstructorDemo5.java:26)
    at org.opentutorials.javatutorials.Inheritance.example3.CalculatorConstructorDemo5.main(CalculatorConstructorDemo5.java:38)
```

즉 상위 클래스인 `Calculator`의 기본 생성자가 존재하지 않는다는 의미다. 하위 클래스가 호출될 때 자동으로 상위 클래스의 기본 생성자를 호출하게 된다. 그런데 상위 클래스에 매개변수가 있는 생성자가 있다면 자바는 자동으로 상위 클래스의 기본 생성자를 만들어주지 않는다. 따라서 존재하지 않는 생성자를 호출하게 되기 때문에 에러가 발생했다. 이 문제를 해결하기 위해서는 아래와 같이 상위 클래스에 기본 생성자를 추가하면 된다.

``` java
package Inheritance.example2;

class Calculator2 {	// 기본 생성자가 존재하지 않는다. java는 어떠한 생성자가 명시되어 있는 경우, 자동으로 기본 생성자를 생성해주지 않는다.
    int left, right;
    // 자식 클래스가 부모 클래스의 기본 생성자를 호출하는데, 기본 생성자가 존재하지 않아 에러가 발생한다.
    
    public Calculator2(){    // 기본 생성자를 명시적으로 생성해주면 된다. (수정 코드)
        
    }
    
    public Calculator2(int left, int right){
        this.left = left;
        this.right = right;
    }
     
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
 
class SubstractionableCalculator2 extends Calculator2 {	// 자식 클래스의 생성자가 호출되면, 자식 클래스는 부모 클래스의 생성자를 자동으로 호출하도록 되어있다.
    public SubstractionableCalculator2(int left, int right) {
        this.left = left;
        this.right = right;
    }
 
    public void substract() {
        System.out.println(this.left - this.right);
    }
}
 
public class CalculatorConstructorDemo2 {
    public static void main(String[] args) {
        SubstractionableCalculator2 c1 = new SubstractionableCalculator2(10, 20);	// 자식 클래스의 생성자를 호출.
        c1.sum();
        c1.avg();
        c1.substract();
    }
}
```

그런데 상위 클래스인 `Calculator`에는 `left`와 `right` 값을 초기화할 수 있는 좋은 생성자가 이미 존재한다. 이것을 사용한다면 하위 클래스에서 `left`와 `right`의 값을 직접 설정하는 불필요한 절차를 생략할 수 있을 것이다.

</br>

## super

super는 상위 클래스를 가리키는 키워드다. 예제를 통해서 super의 사용법을 알아보자.

``` java
package Inheritance.example2;

class Calculator3 {
    int left, right;
     
    public Calculator3(){}
     
    public Calculator3(int left, int right){
        this.left = left;
        this.right = right;
    }
     
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
class SubstractionableCalculator3 extends Calculator3 {
    public SubstractionableCalculator3(int left, int right) {
        super(left, right);	// super는 부모클래스를 뜻하고, super 옆에 ()가 붙으면 생성자라는 뜻함.
    }	// 부모 클래스의 매개변수가 있는 생성자는 left, right에 자식 클래스 생성자 매개변수를 인자로 받는다.
    	// 자식 클래스의 초기화 코드는 무조건 super 밑으로 코딩되어야 한다. 안그러면 에러가 발생한다.
    
    public void substract() {
        System.out.println(this.left - this.right);
    }
}
 
public class CalculatorConstructorDemo3 {
    public static void main(String[] args) {
        SubstractionableCalculator3 c1 = new SubstractionableCalculator3(10, 20);
        c1.sum();
        c1.avg();
        c1.substract();
    }
}
```

`super` 키워드는 부모 클래스를 의미한다. 여기에 ()붙이면 부모 클래스의 생성자를 의미하게 된다. 이렇게 하면 부모 클래스의 기본 생성자가 없어져도 오류가 발생하지 않는다.

하위 클래스의 생성자에서 `super`를 사용할 때 주의할 점은 `super`가 가장 먼저 나타나야 한다는 점이다. 즉 부모가 초기화되기 전에 자식이 초기화되는 일을 방지하기 위한 정책이다.