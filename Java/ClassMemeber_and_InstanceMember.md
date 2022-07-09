# 클래스 맴버와 인스턴스 맴버

</br>

## 맴버

맴버(member)는 영어로 구성원이라는 뜻이다. 객체도 구성원이 있는데 아래와 같다.
- 변수
- 메소드
객체를 만들기 위해서 우선 클래스를 정의하고, 클래스에 대한 인스턴스를 만들어야 한다. 이전 시간에 살펴봤던 예제 [CalculatorDemo.java](https://opentutorials.org/module/516/5400#Calculator.java)에서 left와 right 변수는 인스턴스의 맴버다. 인스턴스를 만들어야 사용할 수 있었고, 인스턴스마다 서로 다른 값을 가지고 있기 때문이다. 또한 클래스도 맴버를 가질 수 있다.

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/516/1888.gif)

</br>

## 클래스 변수

[CalculatorDemo.java](https://opentutorials.org/module/516/5400#Calculator.java)에서 사용한 인스턴스 변수인 left의 값은 인스턴스마다 달라질 수 있다. 인스턴스 변수 c1의 left 값은 10이고, c2의 left 값은 20이었다. 인스턴스의 상태인 변수의 값이 인스턴스마다 다른 값을 가질 수 있다는 점은 하나의 클래스를 여러개의 인스턴스로 만들어서 사용할 수 있다는 점에서 좋은 기능이라고 할 수 있다. 그런데 경우에 따라서 모든 인스턴스가 같은 값을 공유하게 하고 싶을 때가 있다.

이를테면 우리가 만든 계산기가 원주율의 값을 사용자에게 제공하도록 하고 싶다고 간주해보자면, 원주율인 3.14는 이미 알려져있는 수이다. 따라서 각각의 인스턴스 마다 원주율의 값을 별도로 가지고 있을 필요가 없다. 이런 경우 변수를 클래스의 맴버로 만들면 된다. 아래 코드는 원주율을 담고 있는 변수 PI를 클래스의 소속인 맴버로 만든 예제다.

``` java
package classninstance;
 
class Calculator {
    static double PI = 3.14;	// 모든 인스턴스가 공유하는 변수 = 클래스 변수
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
 
public class CalculatorDemo1 {
 
    public static void main(String[] args) {
 
        Calculator c1 = new Calculator();
        System.out.println(c1.PI);	// 인스턴스로 클래스 변수에 접근이 가능하다.
 
        Calculator c2 = new Calculator();
        System.out.println(c2.PI);
 
        System.out.println(Calculator.PI);	// 클래스로 클래스 변수에 직접적으로 접근이 가능하다.
 
    }
 
}
```

5행을 보자.

``` java
static double PI = 3.14;
```

변수 PI의 앞에 static이 붙었다. static을 맴버(변수,메소드) 앞에 붙이면 클래스의 맴버가 된다. 클래스 소속의 변수를 만드는 법을 알았으니까 이번에는 이것을 사용하는 법을 알아보자. 아래는 클래스 변수에 접근하는 방법 두가지를 보여준다.

``` java
// 인스턴스를 통해서 PI에 접근
System.out.println(c1.PI);
// 클래스를 통해서 PI에 접근
System.out.println(Calculator.PI);
```

두번째 방법은 객체 Calculator.java의 다른 기능(sum, avg)은 필요없고, 원주율만 필요할 때 클래스에 직접 접근하기 때문에 인스턴스를 생성할 필요가 없어진다.

클래스 변수는 변수의 변경사항을 모든 인스턴스에서 공유해야 할 때도 사용한다. 만약 계산을 할 때 특별한 값을 포함시켜야 한다면 어떻게 해야 할까? 아래 예제는 sum과 avg를 실행할 때마다 특정한 값을 연산에 포함시키고 싶을 때 시도해볼 수 있는 방법이다.

``` java
package classninstance;
 
class Calculator2 {
    static double PI = 3.14;
    // 클래스 변수인 base가 추가되었다.
    static int base = 0;
    int left, right;	// 인스턴스 변수
 
    public void setOprands(int left, int right) {
        this.left = left;
        this.right = right;
    }
 
    public void sum() {
        // 더하기에 base의 값을 포함시킨다.
        System.out.println(this.left + this.right + base);	// 인스턴스 변수와 클래스 변수를 같이 사용.
    }
 
    public void avg() {
        // 평균치에 base의 값을 포함시킨다.
        System.out.println((this.left + this.right + base) / 2);
    }
}
 
public class CalculatorDemo2 {
 
    public static void main(String[] args) {
 
        Calculator2 c1 = new Calculator2();
        c1.setOprands(10, 20);
        // 30 출력
        c1.sum();
 
        Calculator2 c2 = new Calculator2();
        c2.setOprands(20, 40);
        // 60 출력
        c2.sum();
 
        // 클래스 변수 base의 값을 10으로 지정했다.
        Calculator2.base = 10;
 
        // 40 출력
        c1.sum();
 
        // 70 출력
        c2.sum();
 
    }
 
}
```

결과는 아래와 같다.

``` java
30
60
40
70
```

41번 행에서 클래스 변수 base의 값을 변경한 결과 모든 인스턴스의 base 값이 일제히 변경되었다.

클래스 변수의 용도를 정리해보면 아래와 같다.
- 인스턴스에 따라서 변하지 않는 값이 필요한 경우 (위의 예에서는 PI)
(이런 경우 final을 이용해서 상수로 선언하는 것이 바람직하다.)
- 인스턴스를 생성할 필요가 없는 값을 클래스에 저장하고 싶은 경우
- 값의 변경 사항을 모든 인스턴스가 공유해야 하는 경우

</br>

## 클래스 메소드

예제 Calculator은 인스턴스 변수 left와 right를 이용해서 합계(sum)과 평균(avg)을 계산한다. 생각해보면 굳이 인스턴스가 left와 right의 값을 항상 유지하고 있어야 할 이유는 없다. 합계나 평균을 구할 때마다 좌항과 우항의 값을 주는 방식으로 계산을 할 수도 있다.

``` java
package classninstance;
 
class Calculator3{
  
    public static void sum(int left, int right){
        System.out.println(left+right);
    }
     
    public static void avg(int left, int right){
        System.out.println((left+right)/2);
    }
}
 
public class CalculatorDemo3 {
     
    public static void main(String[] args) {
        Calculator3.sum(10, 20);	// 클래스 메소드는 인스턴스를 따로 선언해 메모리를 사용할 필요 없이,
        Calculator3.avg(10, 20);	// 간단하게 일회용성으로 사용할 메소드를 호출하여 빠르게 사용이 가능하다.
         
        Calculator3.sum(20, 40);
        Calculator3.avg(20, 40);
    }
 
}
```

만약 메소드가 인스턴스 변수를 참조하지 않는다면 클래스 메소드를 사용해서 불필요한 인스턴스의 생성을 막을 수 있다.

아래 예제는 클래스와 인스턴스의 차이점을 보여주기 위한 예제다. 이 예제는 오류가 포함되어 있기 때문에 실행되지 않을 것이다. 예제의 내용을 살펴보기 전에 몇가지 원칙을 기억해두자.

1. 인스턴스 메소드는 클래스 맴버에 접근 할 수 있다.
2. 클래스 메소드는 인스턴스 맴버에 접근 할 수 없다.

인스턴스 변수는 인스턴스가 만들어지면서 생성되는데, 클래스 메소드는 인스턴스가 생성되기 전에 만들어지기 때문에 클래스 메소드가 인스턴스 맴버에 접근하는 것은 존재하지 않는 인스턴스 변수에 접근하는 것과 같다.

위의 내용을 바탕으로 한줄 한줄 따져보자.

``` java
package classninstance;
 
class C1{
    static int static_variable = 1;
    int instance_variable = 2;
    static void static_static(){
        System.out.println(static_variable);
    }
    static void static_instance(){
        // 클래스 메소드에서는 인스턴스 변수에 접근 할 수 없다. 
        //System.out.println(instance_variable);	// 에러 발생하기 때문에 주석처리
    }
    void instance_static(){
        // 인스턴스 메소드에서는 클래스 변수에 접근 할 수 있다.
        System.out.println(static_variable);
    }
    void instance_instance(){        
        System.out.println(instance_variable);
    }
}
public class ClassMemberDemo {  
    public static void main(String[] args) {
        C1 c = new C1();
        // 인스턴스를 이용해서 정적 메소드에 접근 -> 성공
        // 인스턴스 메소드가 정적 변수에 접근 -> 성공
        c.static_static();
        // 인스턴스를 이용해서 정적 메소드에 접근 -> 성공
        // 정적 메소드가 인스턴스 변수에 접근 -> 실패
        c.static_instance();
        // 인스턴스를 이용해서 인스턴스 메소드에 접근 -> 성공
        // 인스턴스 메소드가 클래스 변수에 접근 -> 성공
        c.instance_static();
        // 인스턴스를 이용해서 인스턴스 메소드에 접근 -> 성공 
        // 인스턴스 메소드가 인스턴스 변수에 접근 -> 성공
        c.instance_instance();
        // 클래스를 이용해서 클래스 메소드에 접근 -> 성공
        // 클래스 메소드가 클래스 변수에 접근 -> 성공
        C1.static_static();
        // 클래스를 이용해서 클래스 메소드에 접근 -> 성공
        // 클래스 메소드가 인스턴스 변수에 접근 -> 실패
        C1.static_instance();
        // 클래스를 이용해서 인스턴스 메소드에 접근 -> 실패
        //C1.instance_static();
        // 클래스를 이용해서 인스턴스 메소드에 접근 -> 실패
        //C1.instance_instance();
    }
 
}
```

</br>

## 용어
인스턴스 변수와 클래스 변수는 아래와 같이 부르기도 한다.

- 인스턴스 변수 -> Non-Static Field
- 클래스 변수 -> Static Field

필드(field)라는 것은 클래스 전역에서 접근 할 수 있는 변수를 의미한다.