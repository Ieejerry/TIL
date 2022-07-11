# Overriding

오버라이딩(Overridng)은 한국어로 재정의라는 말로 새롭게 정의한다는 뜻을 가지고 있다. 상속과 아주 밀접한 관계에 있는 개념이다.

</br>

## 창의적인 상속

상속은 상위 클래스의 기능을 하위 클래스에게 물려주는 기능이다. 그렇다면 하위 클래스는 상위 클래스의 메소드를 주어진 그대로 사용해야 한다면 제약이 상당할 것이다. 이런 제약을 벗어나려면 하위 클래스가 부모 클래스의 기본적인 동작방법을 변경할 수 있어야 한다. 이런 맥락에서 도입된 기능이 메소드 오버라이딩(overriding)이다.

[상속 시간의 예제](https://opentutorials.org/module/516/6060#SubstaractionableCalculator)를 살펴보면, 이 예제는 클래스 `Calculator`의 기본적인 동작 방법을 상속 받은 `SubstractionableCalculator`에 빼기 기능을 추가하고 있다. 이것은 상위 클래스의 기능에 새로운 기능을 추가한 것이다. 만약 상위 클래스에서 물려 받은 메소드 `sum`을 호출했을 때 아래와 같이 그 결과를 좀 더 친절하게 알려줘야 한다면 상황이라면 이럴 때 오버라이딩을 하면 된다.

``` java
실행 결과는 30입니다.
```

상속 토픽의 예제를 조금 변경해보자.

``` java
package overriding.example1;
 
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
     
    public void sum() {	// 부모 클래스 메소드를 오버라이딩한 자식 클래스를 인스턴스한 상황에서 해당 메소드를 호출하면 오버라이딩한 메소드가 호출된다.
        System.out.println("실행 결과는 " +(this.left + this.right)+"입니다.");
    }
     
    public void substract() {
        System.out.println(this.left - this.right);
    }
}
 
public class CalculatorDemo {
    public static void main(String[] args) {
        SubstractionableCalculator c1 = new SubstractionableCalculator();
        c1.setOprands(10, 20);
        c1.sum();
        c1.avg();
        c1.substract();
    }
}
```

실행결과는 아래와 같다.

``` java
실행 결과는 30입니다.
15
-10
```

메소드 `sum`이  `SubstractionableCalculator`에 추가 되었다. 실행결과는 `c1.sum`이 상위 클래스의 메소드가 아니라 하위 클래스의 메소드 `sum`을 실행하고 있다는 것을 보여준다. 하위 클래스 입장에서 부모 클래스란 말하자면 기본적인 동작 방법을 정의한 것이라고 생각할 수 있다. 하위 클래스에서 상의 클래스와 동일한 메소드를 정의하면 부모 클래스로부터 물려 받은 기본 동작 방법을 변경하는 효과를 갖게 된다. 기본동작은 폭넓게 적용되고, 예외적인 동작은 더 높은 우선순위를 갖게하고 있다. 이것은 공학에서 일반적으로 발견되는 규칙이다. 이것을 메소드 오버라이딩(overriding)이라고 한다.

</br>

## 오버라이딩의 조건

상위 클래스에서 정의하고 있는 메소드 `avg`는 계산 결과를 화면에 출력하고 있다. 그런데 계산 결과를 좀 더 다양하게 사용하기 위해서 메소드 `avg`가 화면에 결과를 출력하는 대신 계산 결과를 리턴해주면 좋겠다. 그래서 아래와 같이 코드를 고쳐봤다.

``` java
package overriding.example1;
 
class Calculator2 {
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
 
class SubstractionableCalculator2 extends Calculator2 {
     
    public void sum() {
        System.out.println("실행 결과는 " +(this.left + this.right)+"입니다.");
    }
     
//    public int avg() {	// 오버라이딩을 하려면 부모 클래스의 해당 메소드와 메소드 이름, 반환 타입, 매개변수 수와 타입이 순서가 같아야하는데, 이 경우 반환 타입이 다르기 때문에 에러가 발생하게 된다.
//        return (this.left + this.right)/2;
//    }
     
    public void substract() {
        System.out.println(this.left - this.right);
    }
}
 
public class CalculatorDemo2 {
    public static void main(String[] args) {
        SubstractionableCalculator2 c1 = new SubstractionableCalculator2();
        c1.setOprands(10, 20);
        c1.sum();
        c1.avg();
        c1.substract();
    }
}
```

이것은 아래와 같은 에러를 발생한다.

``` java
Exception in thread "main" java.lang.Error: Unresolved compilation problem: 
    The return type is incompatible with Calculator.avg()
 
    at org.opentutorials.javatutorials.overriding.example1.SubstractionableCalculator.avg(CalculatorDemo.java:26)
    at org.opentutorials.javatutorials.overriding.example1.CalculatorDemo.main(CalculatorDemo.java:40)
```

overriding을 하기 위해서는 메소드의 리턴 형식이 같아야 한다. 즉 클래스 `Calculator`의 메소드 `avg`는 리턴 타입이 `void`이다. 그런데 이것을 상속한 클래스 `SubstractionableCalculator`의 리턴 타입은 `int`이다. 오버라이딩을 하기 위해서는 아래의 조건을 충족시켜야 한다.

- 메소드의 이름
- 메소드 매개변수의 숫자와 데이터 타입 그리고 순서
- 메소드의 리턴 타입

위와 같이 메소드의 형태를 정의하는 사항들을 통털어서 메소드의 서명(signature)라고 한다. 즉 위의 에러는 메소드들 간의 서명이 달라서 발생한 문제다. 그래서 아래와 같이 상위 클래스의 코드를 변경해보겠다.

``` java
package overriding.example1;
 
class Calculator3 {
    int left, right;
 
    public void setOprands(int left, int right) {
        this.left = left;
        this.right = right;
    }
 
    public void sum() {
        System.out.println(this.left + this.right);
    }
 
    public int avg() {	// 에러를 해결하기 위해서 부모 클래스의 메소드 signature를 자식 클래스의 메소드와 동일하게 수정을 해주면 된다. 하지만 이 방법은 바람직한 방법이 아니다.
        return ((this.left + this.right) / 2);
    }
}
 
class SubstractionableCalculator3 extends Calculator3 {
     
    public void sum() {
        System.out.println("실행 결과는 " +(this.left + this.right)+"입니다.");
    }
     
    public int avg() {
        return ((this.left + this.right) / 2);	// 부모 클래스의 메소드 signature를 변경하니 자식 클래스와 동일한 메소드가 되었다. 이럴 경우 코드의 중복이 발생하게 된다.
    }
     
    public void substract() {
        System.out.println(this.left - this.right);
    }
}
 
public class CalculatorDemo3 {
    public static void main(String[] args) {
        SubstractionableCalculator3 c1 = new SubstractionableCalculator3();
        c1.setOprands(10, 20);
        c1.sum();
        c1.avg();
        c1.substract();
    }
}
```

상위 클래스와 하위 클래스의 서명이 같기 때문에 메소드 오버라이딩을 할 수 있었다. 그런데 위의 코드를 보면 중복이 발생했다. 메소드 `avg`의 부모와 자식 클래스가 같은 로직을 가지고 있다. 중복은 제거 되어야 한다. 생성자와 마찬가지로 `super`를 사용하면 이 문제를 해결 할 수 있다.

``` java
package overriding.example1;
 
class Calculator4 {
    int left, right;
 
    public void setOprands(int left, int right) {
        this.left = left;
        this.right = right;
    }
 
    public void sum() {
        System.out.println(this.left + this.right);
    }
 
    public int avg() {
        return ((this.left + this.right) / 2);
    }
}
 
class SubstractionableCalculator4 extends Calculator4 {
     
    public void sum() {
        System.out.println("실행 결과는 " +(this.left + this.right)+"입니다.");
    }
     
    public int avg() {
        return super.avg();	// 코드 중복의 제거를 위해 부모 클래스 avg()의 내용을 입력하지 않고, 부모 클래스를 뜻하는 super 뒤에 .avg()를 호출하면 된다.
    }
     
    public void substract() {
        System.out.println(this.left - this.right);
    }
}
 
public class CalculatorDemo4 {
    public static void main(String[] args) {
        SubstractionableCalculator4 c1 = new SubstractionableCalculator4();
        c1.setOprands(10, 20);
        c1.sum();
        System.out.println("실행 결과는 " + c1.avg());	// 부모 클래스와 자식 클래스의 sum() 메소드는 동일한 코드이기 때문에, 자식 클래스에서 sum() 메소드를 정의하지 않고, 객체에서 sum()을 호출하면 부모 클래스의 메소드를 호출하기 때문에 불필요한 코드를 줄일 수 있겠다.
        // 하지만 super.(부모 클래스 메소드)를 한 후, 추가적으로 코드를 더한다면 다른 코드가 되기 때문에 부모 클래스 메소드를 추가 수정할 시에는 중복의 제거를 할 수 있다.
        c1.substract();
    }
}
```

하위 클래스의 메소드 `avg`에서 상위 클래스의 메소드를 호출하기 위해서 `super`를 사용하고 있다. 덕분에 코드의 중복을 제거 할 수 있었다.

이렇게해서 부모 클래스의 기능을 변경 할 수 있는 방법인 메소드 오버라이딩에 대해서 알아봤다.