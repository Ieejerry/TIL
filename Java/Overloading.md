# Overloading

[계산기 예제](https://opentutorials.org/module/516/5400#Calculator.java)를 보면, 이 예제는 2개의 값(`left`, `right`)에 대한 연산(`sum`, `avg`) 만을 수행 할 수 있다. 그런데 만약 3개의 값을 대상으로 연산을 해야 한다면 아래와 같이 입력값을 3개 받아야한다. 

``` java
c1.setOprands(10, 20, 30);
```

이를 위해서 기존의 `setOprands` 메소드를 아래와 같은 모습을 수정한다면 2개의 입력값을 받을 수 없게 된다.

``` java
public void setOprands(int left, int right, int third){
    this.left = left;
    this.right = right;
    this.third = third;
}
```

이런 경우 아래와 같이 메소드의 이름을 변경하면 될 것이다.

``` java
c1.setOprands2(10, 20);
c1.setOprands3(10, 20, 30);
```

이것도 좋은 방법이지만 매개변수의 수에 따라서 메소드의 이름이 달라지는 것은 깔끔한 방법이 아니다.

``` java
package overloading.example1;
 
class Calculator{
    int left, right;
    int third = 0;	// 전역변수 third 선언 및 할당
      
    public void setOprands(int left, int right){
        System.out.println("setOprands(int left, int right)");
        this.left = left;
        this.right = right;
    }
     
    public void setOprands(int left, int right, int third){	// 메소드의 이름이 같더라도, 매개변수가 다르면, 다른 메소드로 인식하는 것을 오버로딩이라고 한다.
        System.out.println("setOprands(int left, int right, int third)");
        this.left = left;
        this.right = right;
        this.third = third;
    }
     
    public void sum(){
        System.out.println(this.left+this.right+this.third);
    }
      
    public void avg(){
        System.out.println((this.left+this.right+this.third)/3);
    }
}
  
public class CalculatorDemo {
      
    public static void main(String[] args) {
          
        Calculator c1 = new Calculator();
        c1.setOprands(10, 20);
        c1.sum();       
        c1.avg();
        c1.setOprands(10, 20, 30);
        c1.sum();       
        c1.avg();
         
    }
  
}
```

실행 결과는 아래와 같다.

``` java
setOprands(int left, int right)
30
15
setOprands(int left, int right, int third)
60
30
```

아래 코드를 보자.

``` java
c1.setOprands(10,20);
```

이 코드의 실행 결과는 화면에 아래와 같은 메시지를 출력한다.

``` java
setOprands(int left, int right)
```

다음 코드를 보자.

``` java
c1.setOprands(10, 20, 30);
```

실행 결과는 아래와 같다.

``` java
setOprands(int left, int right, int third)
```

이를 통해서 알 수 있는 것은 매개변수의 숫자에 따라서 같은 이름의, 서로 다른 메소드를 호출하고 있다는 것을 알 수 있다.

이름은 같지만 시그니처는 다른 메소드를 중복으로 선언 할 수 있는 방법을 메소드 오버로딩(overloading)이라고 한다.

</br>

## 오버로딩의 규칙

결론적으로 말하면 메소드 오버로딩은 매개변수를 사용한다. 즉 매개변수가 다르면 이름이 같아도 서로 다른 메소드가 되는 것이다. 반면에 매개변수는 같지만 리턴타입이 다르면 오류가 발생한다.

``` java
package overloading.example1;
public class OverloadingDemo {
    void A (){System.out.println("void A()");}
    void A (int arg1){System.out.println("void A (int arg1)");}
//  void A (int param1){System.out.println("void A (int arg1)");}
    // 위의 처럼 매개변수의 이름이 다르다고 해서 오버로딩이 되지 않고, 에러를 발생한다. 오버로딩은 매개변수의 갯수, 타입, 순서가 달라야지 사용이 된다.
    void A (String arg1){System.out.println("void A (String arg1)");}
    //int A (){System.out.println("void A()");}	// 다른 반환 타입을 가져서 에러가 발생함.
    public static void main(String[] args) {
        OverloadingDemo od = new OverloadingDemo();
        od.A();
        od.A(1);
        od.A("coding everybody");
    }
}
```

3행과 4행의 메소드 A는 매개변수의 숫자가 다르다. 4행과 5행의 메소드 A는 인자의 숫자는 같지만 매개변수의 데이터 타입이 다르다. 이런 경우는 오버로딩이 가능하다. 메소드를 호출 할 때 전달되는 인자의 데이터 타입에 따라서 어떤 메소드를 호출할지를 자바가 판단 할 수 있기 때문이다. 하지만 메소드의 반환값은 메소드를 호출하는 시점에서 전달되지 않는 정보이기 때문에 오버로딩의 대상이 될 수 없다.

그리고 매개변수의 이름만 다르다고 해서 오버로딩이 되지 않고, 에러를 발생한다. 오버로딩은 매개변수의 갯수, 타입, 순서가 달라야지 사용이 가능하다.

</br>

## 상속과 오버로딩

상속의 관계에서도 오버로딩을 사용할 수 있다.

``` java
package overloading.example1;
public class OverloadingDemo2 extends OverloadingDemo{	// OverloadingDemo 클래스로부터 상속받고 있다.
    void A (String arg1, String arg2){System.out.println("sub class : void A (String arg1, String arg2)");}	// 부모 클래스중에 string 매개변수 2개를 가진 동일한 이름의 메소드가 없기 때문에 오버로딩이 된다.
    void A (){System.out.println("sub class : void A ()");}	// 부모 클래스에 매개변수가 없는 동일한 이름의 메소드가 존재하기 때문에 이 부분은 오버라이딩이 된다.
    public static void main(String[] args) {
        OverloadingDemo2 od = new OverloadingDemo2();
        od.A();
        od.A(1);
        od.A("coding everybody");
        od.A("coding everybody", "coding everybody");
         
    }
}
```

실행 결과는 아래와 같다.

``` java
sub class : void A ()
void A (int arg1)
void A (String arg1)
sub class : void A (String arg1, String arg2)
```

클래스 `OverloadingDemo2`는 `OverloadingDemo`을 상속 받고 있다. `OverloadingDemo2`의 3행에서 정의된 메소드 `A`는 문자열을 데이터타입으로 하는 두개의 매개변수를 가지고 있다. 이러한 형태의 변수는 부모 클래스에서는 정의되어 있지 않기 때문에 메소드 오버로딩이 되는 것이다. 반면에 4행에서 정의된 메소드 A는 매개변수가 없다. 그리고 부모 클래스에는 이미 매개변수가 없는 메소드 `A`가 존재한다. 이 둘은 매개변수의 형태가 같기 때문에 오버로딩이 아니라 오버라이딩에 해당한다.

</br>

## overriding VS overloading

오버라이딩과 오버로딩은 용어가 참으로 헷갈린다. 하지만 중요한 것은 오버라이딩이 무엇이고 오버로딩이 무엇인가를 구분하는 것은 아니다. riding(올라탄다)을 이용해서 부모 클래스의 메소드의 동작방법을 변경하고, loading을 이용해서 같은 이름, 다른 매개변수의 메소드들을 여러개 만들 수 있다는 사실을 아는 것이 중요하다. 다만 학습이나 협업의 과정에서 개념을 주고 받을 때는 용어가 중요해진다. 이 개념들이 헷갈리는 이유는 over라는 공통분모 때문이다. over를 제외하고 알아두면 덜 헷갈리지 않을까 싶다. (참고로 overriding는 재정의라는 사전적인 의미가 있습니다.)

</br>

## 현실적인 오버로딩

위의 예제는 overloading을 설명하기 위한 예제일뿐 현실적이지 않다. 더 많은 값을 대상으로 연산을 해야 한다면 아래 코드처럼 사용하면 된다.

``` java
package overloading.example1;
 
class Calculator2{
    int[] oprands;	// 정수형 배열 전역변수 oprands 선언
     
    public void setOprands(int[] oprands){	// 정수형 배열을 매개변수로 받는 메소드 생성
        this.oprands = oprands;	// 매개변수를 통해 받은 정수형 배열 인자를 전역변수 oprands에 넣어줌.
    }
     
    public void sum(){
        int total = 0;	// 정수형 지역변수 total 선언 및 0으로 할당
        for(int value : this.oprands){	// 배열의 데이터들을 value라는 변수에 하나씩 반복하며 담아준다.
            total += value;	// for문을 통해 배열의 데이터들을 total에 반복하며 하나씩 더해준다.
        }
        System.out.println(total);	// 배열의 데이터들을 다 total에 더해줬으면 출력한다.
    }
      
    public void avg(){
        int total = 0;	// 정수형 지역변수 total 선언 및 0으로 할당
        for(int value : this.oprands){	// oprands 배열에 담긴 데이터들을 반복하며 하나씩 value 변수에 담아준다.
            total += value;	// 배열 oprands의 데이터들을 하나씩 total 변수에 더해준다.
        }
        System.out.println(total/this.oprands.length);	// 배열 oprands의 모든 데이터를 total 변수에 다 더해줬으면, total 값에 배열의 데이터 갯수만큼 나눠준다.
    }
}
public class CalculatorDemo2 {
    public static void main(String[] args) {
        Calculator2 c1 = new Calculator2();	// c1 인스턴스 선언 및 Calculator 기본 생성자 호출
        c1.setOprands(new int[]{10,20});	// c1 인스턴스 setOprands 메소드에 정수형 배열 선언 후, 2개의 인자 넣어줌.
        c1.sum();	// 2개의 인자로 sum() 메소드 호출
        c1.avg();	// 2개의 인자로 avg() 메소드 호출
        c1.setOprands(new int[]{10,20,30});	// c1 인스턴스 setOprands 메소드에 정수형 배열 선언 후, 3개의 인자 넣어줌.
        c1.sum();	// 3개의 인자로 sum() 메소드 호출
        c1.avg();   // 3개의 인자로 avg() 메소드 호출
    }
}
```

위의 코드는 인자로 배열을 사용하고 있다. 이렇게하면 하나의 매개변수로 여러개의 값을 받을 수 있다.