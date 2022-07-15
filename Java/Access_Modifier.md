# 접근 제어자

</br>

## 자유와 규제

프로그래밍 도구의 기본적인 목표는 생각하는 것을 자유롭게 표현할 수 있도록 하는 것이다. 하지만 자유만으로는 부족하다. 프로그래밍은 작은 것에서 거대한 것, 단순한 것에서 복잡한 것, 단독 작업에서 협업으로 나아가게 된다. 이러한 변화를 수용하기 위해서는 다양한 규제가 필요해지게 된다. 대표적인 규제 중의 하나는 데이터 타입 있다. 어떤 변수가 있을 때 그 변수에 어떤 데이터 타입이 들어있는지, 또 어떤 메소드가 어떤 데이터 타입의 데이터를 리턴하는지를 명시함으로써 사용하는 입장에서는 안심하고 변수와 메소드를 사용할 수 있게 된다. 물론 도구 설계자의 취향이나, 도구의 목적에 따라서 이러한 규제는 채택 되기도 하고, 배제 되기도 한다.

추상 클래스, final, 접근 제어자, 인터페이스 등은 바로 이 규제에 해당한다. 사려 깊은 규제라면 그것이 목적해야 하는 바는 분명해야 한다. 자유에 질서를 부여함으로서 자유를 촉진하는 것이다.

</br>

## 접근 제어자

접근 제어자는 클래스의 맴버(변수와 메소드)들의 접근 권한을 지정한다. 이게 무엇을 의미하는지는 아래의 코드를 보겠다.

``` java
package accessmodifier;
class A {
    public String y(){  // 접근 제어자가 public이면 어디서든 접근을 할 수가 있다.
        return "public void y()";
    }
    private String z(){ // 접근 제어자가 private이면 그 메소드가 속한 내부 클래스를 제외한 외부에서는 접근이 불가능하다.
        return "public void z()";
    }
    public String x(){
        return z();
    }
}
public class AccessDemo1 {
    public static void main(String[] args) {
        A a = new A();
        System.out.println(a.y());
        // 아래 코드는 오류가 발생한다.
        //System.out.println(a.z());
        System.out.println(a.x());  // 접근 제어자가 public인 메소드 x()에 외부 클래스인 AccessDemo1이 접근하여 호출하였고, 메소드 x()는 접근 제어자가 private인 메소드 z()와 같은 내부 클래스에 있어서 접근할 수가 있는 상황이고, 메소드 x()는 메소드 z()를 호출하고 있다. 그래서 결과적으로 외부 클래스인 AccessDemo1에서 메소드 x()를 통해 private인 메소드 z()를 호출하게된다.
    }
}
```

아래 코드는 실행된다.

``` java
System.out.println(a.y());
```

하지만 아래의 코드는 오류를 발생시킨다.

``` java
System.out.println(a.z());
```

오류의 내용은 아래와 같다.

``` java
Exception in thread "main" java.lang.Error: Unresolved compilation problem: 
    The method z() from the type A is not visible
    at org.opentutorials.javatutorials.accessmodifier.AccessDemo1.main(AccessDemo1.java:15)

```

즉 메소드 `z`에 접근 할 수 없다는 의미다. 메소드 `z`의 본체를 보겠다.

``` java
private String z(){
    return "public void z()";
}
```

메소드가 키워드 `private`으로 시작되고 있다. `private`은 클래스(`A`) 밖에서는 접근 할 수 없다는 의미다. 바로 이 private의 자리에 오는 것들을 접근 제어자(access modifier)라고 한다. 밖에서 접근할 수 없는 메소드는 내부적으로 사용하기 위해서 정의한다. 다음 코드를 보겠다.

``` java
System.out.println(a.x());
```

메소드 x의 본체는 아래와 같다.

``` java
public String x(){
    return z();
}
```

접근 제어자가 `public`이기 때문에 호출 할 수 있다. 그리고 메소드의 내용을 보면 내부적으로 메소드 `z`를 호출하고 있다. 메소드 `z`는 정상적으로 호출된다. 왜냐하면 메소드 `x`와 메소드 `z`는 같은 클래스의 소속이기 때문이다. 따라서 메소드 `x`에서 `z`를 호출 할 수 있는 것이다.

</br>

## 접근 제어자를 사용하는 이유

접근 제어자는 매우 중요한 개념이다. 하지만 그 중요함은 기본적으로는 이해의 영역이지만 근본적으로는 공감의 영역이다. 규모있는 에플리케이션을 만드는 과정에서 경험하게 되는 수 많은 막장들로 인한 깊은 절망감을 경험해보지 않았다면 접근 제어자와 같은 개념들은 관념적인 것으로 치부되기 쉽다. 에플리케이션이 커진다는 것은 다른 말로 망가질 확률이 커진다는 의미와 같다. 특히 로직이 망가지는 첫번째 용의자는 사용자다. 즉 객체를 사용하는 입장에서 객체 내부적으로 사용하는 변수나 메소드에 접근함으로서 개발자가 의도하지 못한 오동작을 일으키게 되는 것이다.

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/516/1979.jpg)

이런 문제로부터 객체의 로직을 보호하기 위해서는 맴버에 따라서 외부의 접근을 허용하거나 차단해야 할 필요가 생긴다. 마치 은행이 누구나 접근 할 수 있는 창구와 관계자외에는 출입이 엄격하게 통제되는 금고를 구분하고 있는 이유와 같다.

접근 제어자를 사용하는 또 다른 이유는 사용자에게 객체를 조작 할 수 있는 수단만을 제공함으로서 결과적으로 객체의 사용에 집중 할 수 있도록 돕기 위함이다.

[계산기](https://opentutorials.org/module/516/5400#Calculator.java)를 좀 더 견고하고 사용하기 좋은 에플리케이션으로 만들어보겠다.

``` java
package accessmodifier;
 
class Calculator{
    private int left, right;    // 전역변수를 private으로 설정하여, 외부에서 전역변수에 할당을 못하도록 함.
     
    public void setOprands(int left, int right){
        this.left = left;
        this.right = right;
    }
    private int _sum(){ // 민감한 계산 로직을 private로 설정하여, 외부에서 접근하지 못하게 함.
        return this.left+this.right;
    }
    public void sumDecoPlus(){
        System.out.println("++++"+_sum()+"++++");
    }
    public void sumDecoMinus(){
        System.out.println("----"+_sum()+"----");
    }
}
  
public class CalculatorDemo {
    public static void main(String[] args) {        
        Calculator c1 = new Calculator();   // private을 통해 사용자가 Calculator라는 클래스의 사용법을 제한할 수 있고, 간결하게 만들어줄 수 있다.
        c1.setOprands(10, 20);
        c1.sumDecoPlus();
        c1.sumDecoMinus();
    }
}
```

실행 결과는 아래와 같다.

``` java
++++30++++
----30----
```

우선 인스턴스 필드인 `left`와 `right`가 `private`으로 지정되었다.

``` java
int left, right;
```

이 두개의 변수는 객체 외부에서 호출될 필요가 없다. 따라서 외부로부터 이 변수를 숨기기 위해서 접근 제어자로 `private`을 지정했다.

또한 메소드 `_sum`이 추가 되었는데 실제 계산은 이 메소드가 내부적으로 처리하고, 계산된 결과를 외부에 출력해주는 메소드는 `sumDecoPlus`, `sumDecoMinus`에서 처리한다.

이상과 같은 조치를 통해서 사용자가 접근하면 안되거나 접근 할 필요가 없는 맴버에 대한 접근을 규제할 수 있게 되었다. 어떤 맴버에 대한 접근을 허용할 것인가를 작업자의 판단에 달렸다.

</br>

## 세밀한 제어

접근 제어자는 `public`과 `private`외에도 두가지가 더 있다. `protected`과 `default`가 그것이다. `protected`는 상속 관계에 있다면 서로 다른 패키지에 있는 클래스의 접근도 허용한다. `default`는 접근 제어 지시자가 없는 경우를 의미하는데, 접근 제어자가 없는 메소드는 같은 패키지에 있고 상속 관계에 있는 메소드에 대해서만 접근을 허용한다. 아래 그림은 접근 제어자 별로 접근의 허용범위를 그림으로 나타낸 것이다. 안쪽에 있을수록 접근 통제가 삼엄하고, 밖에 있을수록 접근이 허용된다.

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/516/1996.jpg)

| | public | protected | default | private |
| --- | --- | --- | --- | --- |
| 같은 패키지, 같은 클래스 | 허용 | 허용 | 허용 | 허용 |
| 같은 패키지, 상속 관계 | 허용 | 허용 | 허용 | 불용 |
| 같은 패키지, 상속 관계 아님 | 허용 | 허용 | 허용 | 불용 |
| 다른 패키지, 상속 관계 | 허용 | 허용 | 불용 | 불용 |
| 다른 패키지, 상속 관계 아님 | 허용 | 불용 | 불용 | 불용 |

위의 표는 매우 중요하다. 하지만 이걸 억지로 외우려하면 뇌를 혹사시키는 것이 된다. 직접 코드를 작성해서 경우의 수를 완성해보는 것이 좋은 방법이라고 생각한다. 그리고 그 결과에 따라서 표를 작성해보면 좋을 것 같다. 무엇보다 애매한 것들에 대해서 직접 확인해보는 습관을 정착시키는 것도 좋은 일이다.

위의 관계는 필드(변수)에도 적용된다. 또한 클래스 맴버(static)에게도 적용된다.

</br>

## 클래스의 접근 제어자

클래스 맴버에 대한 접근 제어자를 알아보았다. 이제 살펴볼 것은 클래스의 접근 제어자다. 클래스도 접근 제어자가 있다. 클래스의 접근 제어자는 총 2개로 `public`과 `default`이다. `default`는 접근 제어자를 붙이지 않은 경우 `default`가 된다. 클래스의 접근 제어자는 패키지와 관련된 개념이다. <U>즉 접근 제어자가 `public`인 클래스는 다른 패키지의 클래스에서도 사용할 수 있고, `default`인 경우는 같은 패키지에서만 사용 가능하다.</U>

각각의 두 클래스의 접근 제어자는 이름에 이미 암시되어 있다.

``` java
package accessmodifier.inner;
public class PublicClass {}
```

``` java
package accessmodifier.inner;
class DefaultClass {}
```

위의 클래스들과 같은 패키지에서 이 클래스들을 사용해보면, 아무 문제도 발생하지 않는다.

``` java
package accessmodifier.inner;
public class ClassAccessModifierInnerPackage {
    PublicClass publicClass = new PublicClass();
    DefaultClass defaultClass = new DefaultClass();
}
```

이번에는 다른 패키지에 있는 클래스에서 사용해겠다.

``` java
package accessmodifier.outter;
import accessmodifier.inner.*;
public class ClassAccessModifierOuterPackage {
    PublicClass publicClass = new PublicClass();
    //DefaultClass defaultClass = new DefaultClass();
}
```

주석으로 처리한 부분은 오류가 발생한다. `DefaultClass`의 접근 제어자가 `default`이기 때문이다.

한가지 중요한 제약 사항이 있다. `public` 클래스가 포함된 소소코드는 `public` 클래스의 클래스 명과 소스코드의 파일명이 같아야 한다. 아래 코드의 이름은 `PublicNameDemo.java`이다.

``` java
package accessmodifier.inner;
//public class PublicName {}
public class PublicNameDemo {}
```

주석처리된 부분은 오류가 발생한다. 퍼블릭 클래스의 이름과 소스코드의 이름이 일치하지 않기 때문이다. 그 말은 하나의 소스 코드에는 하나의 public 클래스가 존재 할 수 있다는 의미다.