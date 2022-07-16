# Final

추상이 상속을 강제하는 것이라면 `final`은 상속/변경을 금지하는 규제다.

</br>

## final 필드

필드와 변수는 같은 의미라는 것 기억할 것이다. 실행되는 과정에서 한번 값이 정해진 이후에는 변수 내의 값이 바뀌지 않도록하는 규제다.

[클래스 맴버와 인스턴스 맴버 토픽의 첫번째 예제](https://opentutorials.org/module/516/5440#example1)를 기반으로 내용을 조금 바꾸었다.

``` java
package finals;
 
class Calculator {
    static final double PI = 3.14;	// final을 통해 변수 PI는 3.14로 고정함.
    int left, right;
 
    public void setOprands(int left, int right) {
        this.left = left;
        this.right = right;
        //Calculator.PI = 6;	// 변수 PI는 final로 고정되어 있기 때문에 다른 상수로 할당하려고 한다면 에러가 발생하게 된다.
    }
 
    public void sum() {
        System.out.println(this.left + this.right);
    }
 
    public void avg() {
        System.out.println((this.left + this.right) / 2);
    }
}
 
public class CalculatorDemo1 {
 
    public static void main(String[] args) {
 
        Calculator c1 = new Calculator();
        System.out.println(c1.PI);
        //Calculator.PI = 10;	// 변수 PI는 final로 고정되어 있기 때문에 다른 상수로 할당하려고 한다면 에러가 발생하게 된다.
 
 
    }
 
}
```

위의 코드에서 주목할 점은 변수 앞에 `final`이 붙어있다는 점이다. 그리고 10행과 28행에 `Calculator.PI`를 통해서 클래스 변수 `PI`의 값을 변경하려고 하고 있지만 자바는 이것을 허용하지 않는다. `final`로 지정된 변수에는 한번 값이 할당되면 그 값을 바꿀 수 없기 때문이다.

상수가 변하지 않는 값이다. 그리고 위의 `PI` 예제는 변하지 않을 값이다. 이런 값은 변수 앞에 `final`을 붙여서 이 값이 변경되는 것을 규제할 수 있다. 이러한 특징은 클래스 변수의 예를 들었지만 인스턴스 변수에도 적용된다.

</br>

## final 메소드

`final` 메소드는 `final` 변수 만큼 사용 빈도가 높지는 않다. 아래의 코드는 `final`로 확정(고정)된 메소드 `b`를 오버라이딩하려하기 때문에 오류가 발생한다. 즉, `final`로 고정된 메소드는 오버라이딩, 오버로딩을 할 수 없다.

``` java
package finals;
 
class A{
    final void b(){}
}
class B extends A{
    void b(){}
}
```

</br>

## final 클래스

아래 코드는 `final`로 클래스를 확정(고정)하였는데, 상속하려하고 있다. 따라서 오류가 발생한다. 즉, `final`로 확정된 클래스는 상속할 수 없다.

``` java
package finals;
 
final class C{
    final void b(){}
}
class D extends C{}
```