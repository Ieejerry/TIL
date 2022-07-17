# 예외 1 - 문법

</br>

## 성공과 실패

객체 지향 이전까지가 프로그램을 동작하게 하는 법이라면 객체 지향은 웅장한 소프트웨어를 만들기 위한 방법이라고 할 수 있다. 그 중 예외는 실패하지 않는 법에 대한 내용이다. 아무리 좋은 기획, 좋은 구조 그리고 높은 성능을 가진 소프트웨어라도 심각한 오류나 보안 약점으로 인해서 모든 것을 잃어버릴 수 있다.

모든 것의 기초는 덜 실패하는 법을 배우는게 좋다. 덜 실패하는 법은 실패의 크기를 줄여주는 효과 뿐 아니라 실패에 대한 두려움을 억제해서 성공하는 법을 보다 적극적으로 시도할 수 있게 촉진한다는 점에서 중요하다.

</br>

## 예외란?

프로그래밍을 하면 많은 오류 상황에 직면하게 된다. 기능이 많아질수록 오류가 발생할 확률은 기하급수적으로 증가한다. 자연스럽게 오류를 잘 처리하기 위한 방법들이 필요해지게 된다. 예외(`Exception`)란 프로그램을 만든 프로그래머가 상정한 정상적인 처리에서 벗어나는 경우에 이를 처리하기 위한 방법이다. 자바는 예기치 못한 오류를 어떻게 처리하는가를 알아보겠다.

[계산기 예제](https://opentutorials.org/module/516/5400#Calculator.java)를 보면, 아래는 기존의 더하기(`sum`), 평균(`avg`) 메소드를 제거하고 나누기 메소드를 추가한 예제다.

``` java
package exception;
class Calculator{
    int left, right;
    public void setOprands(int left, int right){
        this.left = left;
        this.right = right;
    }
    public void divide(){
        System.out.print("계산결과는 ");
        System.out.print(this.left/this.right);	// 10을 0으로 나누려고 하기 때문에 에러가 발생하게 된다.
        System.out.print(" 입니다.");
    }
} 
public class CalculatorDemo {
    public static void main(String[] args) {
        Calculator c1 = new Calculator();
        c1.setOprands(10, 0);
        c1.divide();
    }
}
```

위의 코드를 실행시키면 아래와 같은 오류가 발생한다.

``` java
계산결과는 Exception in thread "main" java.lang.ArithmeticException: / by zero
    at org.opentutorials.javatutorials.exception.Calculator.divide(CalculatorDemo.java:10)
    at org.opentutorials.javatutorials.exception.CalculatorDemo.main(CalculatorDemo.java:18)
```

'계산결과'가 출력되었다는 의미는 9행은 실행이 되었다는 의미다. 10행에서 오류가 발생한 이유는 10을 0으로 나누려고 했기 때문이다.

``` java
계산결과는 Exception in thread "main" java.lang.ArithmeticException: / by zero
```

아래의 내용은 오류가 발생한 순서를 추적하고 있는데 제일 아래쪽이 문제의 로직을 호출한 부분이고 가장 위쪽이 문제의 원인이다.

``` java
at org.opentutorials.javatutorials.exception.Calculator.divide(CalculatorDemo.java:12)
at org.opentutorials.javatutorials.exception.CalculatorDemo.main(CalculatorDemo.java:22)
```

에러 메시지는 시스템에서 어떤 오류가 발생했을 때 그 오류를 이해하고 파악하는데 큰 도움이 된다.

다시 코드로 돌아와서 이 문제를 어떻게 해결할까 생각해보겠다. 아래와 같이 코드를 변경해보자.

``` java
package exception;
class Calculator{
    int left, right;
    public void setOprands(int left, int right){
        this.left = left;
        this.right = right;
    }
    public void divide(){
        try {	// try 안에 구문이 실행되다가 오류가 생기게 되면 try 구문은 멈추게 되고, catch 구문으로 넘어가게 된다.
            System.out.print("계산결과는 ");
            System.out.print(this.left/this.right);
            System.out.print(" 입니다.");
        } catch(Exception e){	// JVM은 try 구문에서 오류가 발생하게 되면 자동으로 catch를 호출하게 되고, 에러의 정보를 담고 있는 객체를 catch의 매개변수 인자로 전달을 한다. 그 객체의 데이터 타입은 Exception이라는 클래스이다.
            System.out.println("오류가 발생했습니다 : "+e.getMessage());	// Exception이라는 클래스 안에는 getMessage()라는 메소드가 포함되어 있다.
        }
    }
} 
public class CalculatorDemo {
    public static void main(String[] args) {
        Calculator c1 = new Calculator();
        c1.setOprands(10, 0);
        c1.divide();
         
        Calculator c2 = new Calculator();
        c2.setOprands(10, 5);
        c2.divide();
    }
}
```

결과는 다음과 같다.

``` java
계산결과는 오류가 발생했습니다 : / by zero
계산결과는 2 입니다.
```

즉 10행은 실행이 되었지만 11행은 실행되지 않았다. 그런데 이전 예제와 다른 점이 있다. 오류가 발생하지 않았다는 점이다. 마치 정상적인 에플리케이션인 것처럼 동작하고 있다. 그 이유는 `try`...`catch` 때문이다.

</br>

## try...catch

`try`...`catch`는 예외에서 핵심적인 역할을 담당하는 문법적인 요소다. 형식을 살펴보자.

### try

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/516/2050.png)

`try` 안에는 예외 상황이 발생할 것으로 예상되는 로직을 위치시킨다. 예제에서는 사용자가 `setOprands`의 두 번째 인자로 숫자 0을 입력했을 때 문제가 발생할 수 있음을 예측할 수 있다. 그래서 이 로직을 `try` 구문으로 감싼 것이다.

### catch

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/516/2051.png)

`catch` 안에는 예외가 발생했을 때 뒷수습을 하기 위한 로직이 위치한다. 예제의 실행결과를 다시 살펴보겠다. 아래와 같다.

``` java
계산결과는 오류가 발생했습니다
```

이것은 아래 구문에서 오류가 발생하면서 `try` 내의 실행이 중단되고 `catch` 구문 안의 내용이 실행되었음을 의미한다.

``` java
System.out.print(this.left/this.right);	// 10을 0으로 나누려고 하기 때문에 에러가 발생하게 된다.
```

</br>

## 예외 클래스와 인스턴스

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/516/2052.png)

아래 예제를 보자.

``` java
} catch(Exception e){	// JVM은 try 구문에서 오류가 발생하게 되면 자동으로 catch를 호출하게 되고, 에러의 정보를 담고 있는 객체를 catch의 매개변수 인자로 전달을 한다. 그 객체의 데이터 타입은 Exception이라는 클래스이다.
    System.out.println("오류가 발생했습니다 : "+e.getMessage());	// Exception이라는 클래스 안에는 getMessage()라는 메소드가 포함되어 있다.
}
```

`e`는 변수다. 이 변수 앞의 `Exception`은 변수의 데이터 타입이 `Exception`이라는 의미다. `Exception`은 자바에서 기본적으로 제공하는 클래스로 `java.lang`에 소속되어 있다. 예외가 발생하면 자바는 마치 메소드를 호출하듯이 `catch`를 호출하면서 그 인자로 `Exception` 클래스의 인스턴스를 전달하는 것이다.

`e.getMessage()`는 자바가 전달한 인스턴스의 메소드 중 `getMessage`를 호출하는 코드인데, `getMessage`는 오류의 원인을 사람이 이해하기 쉬운 형태로 리턴하도록 약속되어 있다.

</br>

## 뒷수습의 방법

예외의 핵심은 뒷수습이다. 하지만 제대로 된 수습은 대단히 어려운 문제이다. 여기서는 자바에서 기본적으로 제공하는 뒷수습의 방법만 알아보겠다.

코드를 조금 바꿔보겠다.

``` java
package exception;
class Calculator{
    int left, right;
    public void setOprands(int left, int right){
        this.left = left;
        this.right = right;
    }
    public void divide(){
        try {
            System.out.print("계산결과는 ");
            System.out.print(this.left/this.right);
            System.out.print(" 입니다.");
        } catch(Exception e){
            System.out.println("\n\ne.getMessage()\n"+e.getMessage());	// 에러가 뜬 이유만 간략하게 나온다.
            System.out.println("\n\ne.toString()\n"+e.toString());	// 어떠한 에러의 종류인지와 이유가 나온다.
            System.out.println("\n\ne.printStackTrace()");
            e.printStackTrace();	// 어떠한 에러의 종류와 이유, 그리고 에러가 뜬 코드까지 나온다.
        }
    }
} 
public class CalculatorDemo {
    public static void main(String[] args) {
        Calculator c1 = new Calculator();
        c1.setOprands(10, 0);
        c1.divide();
    }
}
```

결과는 아래와 같다.

``` java
계산결과는 
 
e.getMessage()
/ by zero
 
 
e.toString()
java.lang.ArithmeticException: / by zero
 
 
e.printStackTrace()
java.lang.ArithmeticException: / by zero
    at org.opentutorials.javatutorials.exception.Calculator.divide(CalculatorDemo.java:11)
    at org.opentutorials.javatutorials.exception.CalculatorDemo.main(CalculatorDemo.java:25)
```

### e.getMessage();

오류에 대한 기본적인 내용을 출력해준다. 상세하지 않다.

### e.toString()

`e.toString()`을 호출한 결과는 `java.lang.ArithmeticException: / by zero` 이다. `e.toString()`은 `e.getMessage()`보다 더 자세한 예외 정보를 제공한다. `java.lang.ArithmeticException`은 발생한 예외가 어떤 예외에 해당하는지에 대한 정보라고 지금을 생각하자. `ArithmeticException` 수학적인 계산의 과정에서 발생하는 예외상황을 의미한다.

### e.printStackTrace()

메소드 `getMessage`, `toString`과는 다르게 `printStackTrace`는 리턴값이 없다. 이 메소드를 호출하면 메소드가 내부적으로 예외 결과를 화면에 출력한다. `printStackTrace`는 가장 자세한 예외 정보를 제공한다.

</br>

## 다양한 예외들

좀 더 다양한 예외 상황을 처리하는 방법을 알아보겠다.

``` java
package exception;
 
class A{
    private int[] arr = new int[3];	// arr이라는 변수에 3개의 값을 갖는 정수형 배열을 선언
    A(){	// 클래스 A 기본 생성자
        arr[0]=0;
        arr[1]=10;
        arr[2]=20;
    }	// arr 정수형 배열에 값을 할당
    public void z(int first, int second){
        System.out.println(arr[first] / arr[second]);	// arr은 3개의 값만 가지는 배열인데 first에서 10번째 값을 호출하기 때문에 에러가 발생.
    }
}
 
public class ExceptionDemo1 {
    public static void main(String[] args) {
        A a = new A();
        a.z(10, 1);
    }
}
```

위의 결과는 아래와 같다.

``` java
Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: 10
    at org.opentutorials.javatutorials.exception.A.z(ExceptionDemo1.java:11)
    at org.opentutorials.javatutorials.exception.ExceptionDemo1.main(ExceptionDemo1.java:18)
```

이유를 보자면, 배열 arr은 3개의 값을 담을 수 있다.

``` java
private int[] arr = new int[3];
```

하지만 10번째 인덱스를 호출하고 있다.

``` java
a.z(10, 1);
```

``` java
System.out.println(arr[first] / arr[second]);
```

따라서 존재하지 않는 값을 가져오려고 시도하고 있기 때문에 자바에서는 `ArrayIndexOutOfBoundsException`을 발생시킨 것이다.

위의 코드를 조금 변경해보겠다.

``` java
package exception;
 
class A{
    private int[] arr = new int[3];
    A(){
        arr[0]=0;
        arr[1]=10;
        arr[2]=20;
    }
    public void z(int first, int second){
        System.out.println(arr[first] / arr[second]);	// 10을 0으로 나누려고 하기 때문에 ArithmeticException 에러가 발생하게 된다.
    }
}
 
public class ExceptionDemo1 {
    public static void main(String[] args) {
        A a = new A();
        a.z(1, 0);
    }
}
```

결과는 아래와 같다.

``` java
Exception in thread "main" java.lang.ArithmeticException: / by zero
    at org.opentutorials.javatutorials.exception.A.z(ExceptionDemo1.java:11)
    at org.opentutorials.javatutorials.exception.ExceptionDemo1.main(ExceptionDemo1.java:18)
```

위의 코드는 메소드 `z` 내부적으로 10/0을 실행하게 된다. 0으로 나누는 것은 불가능하기 때문에 자바는 `ArithmeticException`을 발생시킨다.

위의 예제를 통해서 보여주고 싶은 것은 같은 로직이지만 상황에 따라서 다른 예외가 발생할 수 있다는 것이다. 이런 경우는 어떻게 예외를 처리해야 되는지 알아보겠다.

``` java
package exception;
 
class A{
    private int[] arr = new int[3];
    A(){
        arr[0]=0;
        arr[1]=10;
        arr[2]=20;
    }
    public void z(int first, int second){
        try {
            System.out.println(arr[first] / arr[second]);
        } catch(ArrayIndexOutOfBoundsException e){	// else if 처럼 ArrayIndexOutOfBoundsException이 뜰 경우 이 catch 구문을 실행.
            System.out.println("ArrayIndexOutOfBoundsException");
        } catch(ArithmeticException e){	// else if 처럼 ArithmeticException이 뜰 경우 이 catch 구문을 실행.
            System.out.println("ArithmeticException");
        } catch(Exception e){	// else 처럼 그 외 예외가 발생할 경우 실행.
            System.out.println("Exception");
        }	// 하지만 catch(Exception e)을 가장 위에 정의할 경우, Exception은 모든 에외를 담고 있기 때문에 하위 예외까지 가지 않고 처리가 된다.
        	// 그래서 Java에서는 하위 예외들이 처리가 되지 않을 것을 알기 때문에 컴파일 조차 되지 않는다.
         
    }
}
 
public class ExceptionDemo1 {
    public static void main(String[] args) {
        A a = new A();
        a.z(10, 0);
        a.z(1, 0);
        a.z(2, 1);
    }
}
```

결과는 다음과 같다.

``` java
ArrayIndexOutOfBoundsException
ArithmeticException
2
```

예제는 다중 `catch`를 보여준다. 조건문의 `else if`처럼 여러 개의 `catch`를 하나의 `try` 구문에서 사용할 수 있다. 이를 통해서 보다 간편하게 다양한 상황에 대응할 수 있다. 위의 코드는 `try` 구문에서 예외가 발생했을 때 그 예외의 종류가 `ArrayIndexOutOfBoundsException`이라면 14행이 실행되고, `ArithemeticException`이라면 16행이 실행되고 그 외의 것이라면 18행이 실행된다는 의미다.

만약 아래와 같이 메소드 `z`의 코드를 변경한다면 어떻게 되는지 알아보겠다.

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/516/2057.png)

아래와 같은 메시지가 출력되면서 컴파일 조차 되지 않는다.

``` java
Exception in thread "main" java.lang.Error: Unresolved compilation problems: 
    Unreachable catch block for ArrayIndexOutOfBoundsException. It is already handled by the catch block for Exception
    Unreachable catch block for ArithmeticException. It is already handled by the catch block for Exception
 
    at org.opentutorials.javatutorials.exception.A.z(ExceptionDemo1.java:15)
    at org.opentutorials.javatutorials.exception.ExceptionDemo1.main(ExceptionDemo1.java:27)
```

그것은 `Exception`이 `ArrayIndexOutOfBoundsException`, `ArithemeticException` 보다 포괄적인 예외를 의미하기 때문에 `Exception` 이후에 등장하는 `catch` 문은 실행될 수 없는 구문이기 때문이다. 자바 컴파일러가 불필요한 로직을 감지하고 이를 개발자에게 알려주는 것이다.

</br>

## finally

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/516/2058.png)

`finally`는 `try` 구문에서 예외가 발생하는 것과 상관없이 언제나 실행되는 로직이다.

``` java
package exception;
 
class A{
    private int[] arr = new int[3];
    A(){
        arr[0]=0;
        arr[1]=10;
        arr[2]=20;
    }
    public void z(int first, int second){
        try {
            System.out.println(arr[first] / arr[second]);
        } catch(ArrayIndexOutOfBoundsException e){
            System.out.println("ArrayIndexOutOfBoundsException");
        } catch(ArithmeticException e){
            System.out.println("ArithmeticException");
        } catch(Exception e){
            System.out.println("Exception");
        } finally {
            System.out.println("finally");
        }
    }
}
 
public class ExceptionDemo1 {
    public static void main(String[] args) {
        A a = new A();
        a.z(10, 0);
        a.z(1, 0);
        a.z(2, 1);
    }
}
```

실행결과는 다음과 같다.

``` java
ArrayIndexOutOfBoundsException
finally
ArithmeticException
finally
2
finally
```

예외와 상관없이 `try` 내의 구문이 실행되면 `finally`가 실행되고 있다.

`finally`는  예외와는 상관없이 반드시 끝내줘야 하는 상황에서 사용할 수 있다.

예를 들어 데이터베이스를 사용한다면 데이터베이스 서버에 접속해야 한다. 이때 데이터베이스 서버와 에플리케이션은 서로 접속상태를 유지하게 되는데 데이터베이스를 제어하는 과정에서 예외가 발생해서 더 이상 후속 작업을 수행하는 것이 불가능한 경우가 있을 수 있다. 예외가 발생했다고 데이터베이스 접속을 끊지 않으면 데이터베이스와 연결 상태를 유지하게 되고 급기야 데이터베이스는 더 이상 접속을 수용할 수 없는 상태에 빠질 수 있다. 접속을 끊는 작업은 예외 발생여부와 상관없기 때문에 `finally`에서 처리하기에 좋은 작업이라고 할 수 있다. 말하자면 `finally`는 작업의 뒷정리를 담당한다고 볼 수 있다.