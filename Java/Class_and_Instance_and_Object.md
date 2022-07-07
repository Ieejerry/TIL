# 클래스와 인스턴스 그리고 객체

## 클래스와 인스턴스 이전의 프로그래밍

아래 예제는 간단한 더하기 프로그램이이다. 아주 간단한 예제지만 상당히 복잡한 작업을 실행하고 있는 로직이라고 가정해 보겠다.

``` java
package object;
 
public class CalculatorDemo {
 
    public static void main(String[] args) {
        // 아래의 로직이 1000줄 짜리의 복잡한 로직이라고 가정하자.
        System.out.println(10 + 20);
        System.out.println(20 + 40);
    }
    // 메소드를 사용하여 중복을 제거하자.
}
```

</br>

## 메소드화

실행 결과는 30과 60이다. 프로그래밍의 기본은 중복을 제거하는 것이다. 위의 로직은 두개의 값을 더한다는 중복이 존재한다. 이 중복을 제거하기 위한 방법으로 고려해볼 수 있는 기능이 메소드다. 로직을 메소드로 만들면 코드의 양을 줄일 수 있고, 문제가 생겼을 때 원인을 더 쉽게 찾을 수 있다. 아래의 코드는 위의 코드를 메소드화시킨 예제다.

``` java
package object;
 
public class CalculatorDemo2 {
 
    public static void sum(int left, int right) {   // 메솓를 사용하여 중복의 제거를 함.
        System.out.println(left + right);
    }
 
    public static void main(String[] args) {
        sum(10, 20);
        sum(20, 40);
    }
    // 기존의 코드랑 동일하게 동작하지만, 내용을 보다 효율적으로 만드는 행위이며,
    // 예를 들어 로직은 동일하지만, 중복의 제거하는 것을 리팩토링(refactoring)이라고 한다.
}
```

> 프로그램이라는 것은 한 번에 만들어지는게 아니라 여러가지 다양한 과정을 거쳐서 만들어지기 때문에 자주 리팩토링하는 코드가 결국엔 건강한 코드가 되고, 코드가 건강해야지 변화가 있을 때, 변화에 유연하게 대응할 수가 있고, 또 그 코드가 버그를 만들 확률이 낮아지게 된다. 이러한 이유 때문에 리팩토링을 하는 것이다.

> 프로그래밍에서 리팩토링은 상당히 중요한 주제이다.

그런데 똑같은 수를 이용해서 더하기 뿐 아니라 평균도 구해야 한다면 아래와 같이 할 수 있을 것이다. 입력값(left, right)을 변수화시키고 메소드들(sum, avg)가 이 값을 사용하면 코드의 양을 줄일 수 있게 된다.

``` java
package object;
 
public class ClaculatorDemo3 {
 
    public static void avg(int left, int right) {
        System.out.println((left + right) / 2);
    }
 
    public static void sum(int left, int right) {
        System.out.println(left + right);
    }
 
    public static void main(String[] args) {
        int left, right;
 
        left = 10;
        right = 20;
 
        sum(left, right);
        avg(left, right);
 
        left = 20;
        right = 40;
 
        sum(left, right);
        avg(left, right);
    }
 
}
```

</br>

## 객체화

평균을 계산하는 메소드 avg를 추가했고, 두개의 메소드(sum, avg)에서 동일한 입력값(10, 20)을 사용하고 있기 때문에 변수를 이용해서 좌항(left)과 우항(right)에 값을 담았다. 코드가 복잡해지기 시작한다.

실행 메소드인 main 에는 계산과 관련된 로직 밖에 없지만, 만약에 위의 코드에 직원 정보를 데이터베이스에서 가져오는 로직이나, 계산된 결과를 그래프로 표시하는 로직과 같은 것이 함께 위치한다면 코드는 점점 복잡해 질 것이다. 그러다 누군가 변수 left, right의 의미를 계산을 위한 좌항과 우항이 아니라 그래프의 디자인을 변경하는 코드로 사용했거나, 메소드 sum을 더하기가 아니라 요약(summary) 정보를 그래프로 표시하는 의미로 사용하게 되면 하나의 프로그램 안에서 메소드나 변수의 의미가 달라지게 되는 것이다.

코드가 복잡해짐에 따라서 버그는 많아지고, 팀웍은 서서히 깨지기 시작할 것이다. 언어의 설계자는 이런 상황을 완화하기 위한 고민을 했고, 이런 맥락에서 객체 지향이라는 개념이 등장하기 시작하는 것이다. 

객체 지향은 많은 선배 프로그래머들에 의해서 만들어졌기 때문에 다양한 의도가 반영된 프로그래밍 패러다임이다. 그래서 객체 지향이 만들어진 동기를 하나의 케이스로 설명하는 것은 어려운 일이다.
객체 지향의 핵심은 연관되어 있는 변수와 메소드를 하나의 그룹으로 묶어서 그룹핑하는 것이다. 위의 예제를 분석해보면, 연관되어 있는 부분과 반복적인 부분을 찾아 볼 수 있다.

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/516/1863.gif)

메소드 sum과 avg는 변수 left와 right와 서로 연관 되어 있다. 또한 합계와 평균을 구하는 작업은 다른 에플리케이션에서도 사용할 수 있는 기능이다. 이것들을 그룹핑해서 하나의 부품으로 만들면 필요할 때마다 반복적으로 사용할 수 있을 것이다. 객체를 만들 때가 된 것이다.

아래의 예제는 의미적으로 연관된 로직들을 물리적으로 응집된 하나의 객체로 만드는 법을 설명하는 예제다.

``` java
package object;
 
class Calculator{	// 객체의 설계도 = 클래스
    int left, right;	// 변수 선언
      
    public void setOprands(int left, int right){
        this.left = left; // 매개변수로 받은 인자는 left에 들어가게된다.
        this.right = right;	// this는 인스턴스 자기 자신을 의미하고, 앞에 this. 붙은 변수는 class 초입에 선언한 변수이다.
    }
    // 결과적으로 초입에 선언한 변수에 매개변수로 받은 인자가 들어가게 된다.

    public void sum(){
        System.out.println(this.left+this.right);
    }
      
    public void avg(){
        System.out.println((this.left+this.right)/2);
    }
}
  
public class CalculatorDemo4 {
      
    public static void main(String[] args) {
          
        Calculator c1 = new Calculator();	// Calculator라는 객체를 new을 사용해 호출해주고, c1이라는 변수에 담아준다. 그리고 변수 c1은 Calculator라는 데이터 타입을 가진다.
        c1.setOprands(10, 20);	// c1이라는 변수에 담긴 Calculator라는 객체의 setOprands라는 메소드를 호출해준다.
        c1.sum();	// c1이라는 변수에 담긴 Calculator라는 객체의 sum이라는 메소드를 호출해준다.       
        c1.avg();	// c1이라는 변수에 담긴 Calculator라는 객체의 avg라는 메소드를 호출해준다.       
 
        // 변수 c1에 담은 실제 객체의 내용(구체적인 객체)을 인스턴스라고 한다.
        
        Calculator c2 = new Calculator();
        c2.setOprands(20, 40);
        c2.sum();       
        c2.avg();
    }
  
}
```

## 클래스

4행을 보면

``` java
class Calculator {
```

위의 예에서 변수 left와 right, 메소드 sum과 avg는 연관되어 있는 로직이다. 이 로직들의 연관성은 계산을 하기 위한 것이다. 그래서 이 로직들을 대표하는 이름을 계산기라는 의미의 Calculator라고 정하고 이것들을 Calculator이라는 이름으로 그룹핑하고 싶다. 이럴 때 사용하는 키워드가 class이다. class 키워드 뒤에는 클래스 이름이 오고 그 뒤의 중괄호는 클래스의 시작과 끝의 경계를 의미한다. 이렇게 해서 더하기(sum)와 평균(avg)를 계산 할 수 있는 클래스가 만들어졌다. 클래스는 아래와 같이 정의 할 수 있다.

**클래스는 연관되어 있는 변수와 메소드의 집합이다.**

## 인스턴스

클래스는 일종의 설계도다. 클래스를 정의하는 것 자체로는 할 수 있는 일이 많지 않다. 설계도를 구체적인 제품으로 만들어야 한다. 그 때 사용하는 키워드가 new이다. 25번 라인을 보면

``` java
Calculator c1 = new Calculator();
```

new Calculator()은 클래스 Calculator를 구체적인 제품으로 만드는 명령이다. 이렇게 만들어진 구체적인 제품을 인스턴스(instance)라고 부른다.

- 클래스 : 설계도
- 인스턴스 : 제품

위의 코드는 new를 이용해서 만든 인스턴스를 변수 c1에 담고 있다. 변수 c1에 인스턴스를 담은 이유는 c1을 통해서 인스턴스를 제어해야 하기 때문이다. 그런데 c1 앞에 Caculator가 위치하고 있다. 예를 들어서 변수 a는 변수가 담을 수 있는 데이터 타입에 따라서 아래와 같이 다양한 형태로 선언된다.

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/516/1864.gif)

그럼 아래와 같은 구문은 변수명 c1의 어떤 데이터 타입을 뜻하는 것인지 알아보자면

``` java
Calculator c1
```

Calculator라는 의미다. 즉 클래스를 만든다는 것은 사용자 정의 데이터 타입을 만드는 것과 같은 의미다. 일단은 클래스를 인스턴스화 할 때는 변수에 담아야 한다는 것과 이 때 사용하는 변수의 데이터 타입은 그 클래스가 된다는 점을 기억해야 된다.

> 클래스와 인스턴스는 설계도와 제품이라고 설명했다. 그래서 객체는 클래스인가 인스턴스인가에 대해서 일반적으로 설계도인 클래스가 구체적인 실체인 인스턴스가 되었을 때 객체라고 부른다. 보통은 구체적인 코드 상에서 나타나는 객체를 인스턴스라고 부르고, 로직을 설계 할 때 나타나는 인스턴스를 객체라고 부른다. 또는 클래스, 인스턴스의 구분없이 포괄적으로 객체라는 말을 쓰기도 한다.

클래스를 단순히 변수와 메소드의 묶음으로 보면 부족하다. 우리가 객체를 만들어서 사용하는 이유는 재활용성을 높이기 위해서다.

``` java
Calculator c1 = new Calculator();
c1.setOprands(10, 20);
c1.sum();       
c1.avg();       
 
Calculator c2 = new Calculator();
c2.setOprands(20, 40);
c2.sum();       
c2.avg();
```

위의 코드를 보면 두개의 인스턴스를 각각 c1과 c2에 담았다. 그리고 각각의 인스턴스에 소속된 메소드를 호출하고 있다. 각각의 인스턴스는 메소드 setOprands를 통해서 변수 left, right의 값을 설정하고 있다. 그 결과 인스턴스 C1과 C2는 아래와 같이 서로 다른 변수의 값을 내부적으로 가지고 있게 된다.

``` java
public void setOprands(int left, int right){
    this.left = left;
    this.right = right;
}
```

이 때 메소드 setOprands 내에 this.이라는 것이 있다. this는 클래스를 통해서 만들어진 인스턴스 자신을 가리킨다. 위의 코드에서 left는 매개변수이고 이 변수는 setOprands 밖에서는 접근 할 수 없다. 반면에 this.left는 4행에서 선언한 변수에 값을 설정하는 것이고 메소드 밖에서 선언한 변수는 인스턴스 내의 모든 메소드에서 접근이 가능하다.

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/516/1878.gif)

변수를 다른 말로는 상태(state)라고도 표현한다. c1.sum의 결과는 30, c2.sum의 결과는 60인 것을 통해서 알 수 있듯이 상태가 다른 객체를 대상으로 메소스를 실행시키면 다른 결과를 나타내게 된다. 메소드를 다른 말로는 행동(behave)라고도 표현한다.

- 변수 : 상태
- 메소드 : 행동

<u>즉 하나의 클래스를 바탕으로 서로 다른 상태를 가진 인스턴스를 만들면 서로 다른 행동을 하게 된다는 것을 알 수 있다.</u> 하나의 클래스가 여러개의 인스턴스가 될 수 있다는 점이 객체 지향이 제공하는 가장 기본적인 재활용성이라고 할 수 있다.

객체 지향의 객체를 하나의 작은 프로그램처럼 생각해보면, 프로그램 안에 객체라는 작은 프로그램을 만드는 것이다. 이것들을 레고 블럭처럼 쌓아서 웅장한 프로그램을 만드는 것이 객체 지향이 추구하는 바라고 할 수 있다.

> 객체를 만듦으로써 메모리에 객체를 위한 용량을 확보하고, 객체를 통해 그 메모리 용량을 사용하게 된다. 즉, 객체를 만든다는 것은 사용자 정의 데이터 타입을 만든다는 것과 시스템 적 입장으로 같은 의미이다.

> 또한 객체를 만든다는 것은 프로그래밍을 하는 입장으로는 코드를 더 경제적이고 효율적으로 작성할 수 있는 어떠한 도구(수단)를 제공한다는 측면도 가지고 있다.