# Object 클래스

</br>

## 상속

자바에서 상속이란 필수적이다. 상속하건 하지 않았건 기본적인 상속을 하게 된다.

``` java
package progenitor;

class O {}
```

위의 코드는 아래와 코드가 같다.

``` java
package progenitor;
 
class O extends Object {}
```

자바에서 모든 클래스는 사실 `Object`를 암시적으로 상속받고 있다. 그런 점에서 `Object`는 모든 클래스의 조상이라고 할 수 있다. 그 이유는 모든 클래스가 공통으로 포함하고 있어야 하는 기능을 제공하기 위해서다.

API 문서를 보겠다.

http://docs.oracle.com/javase/7/docs/api/java/lang/Object.html

메소드의 목록을 살펴보겠다.

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/516/2123.png)

위의 그림은 `Object` 클래스가 가지고 있는 메소드를 보여준다. 다시 말해서 자바의 객체는 위의 메소드들을 반드시 가지고 있다고 할 수 있다. 이 중에 중요하면서 입문 단계에서 이해할 수 있는 API들을 살펴보겠다.

</br>

## toString

`toString`은 객체를 문자로 표현하는 메소드이다. 기본 예제인 계산기 코드를 보겠다.

``` java
package progenitor;
 
class Calculator{	// 암시적으로 Object라는 부모 클래스를 모든 클래스가 상속 받고 있다.
    int left, right;
      
    public void setOprands(int left, int right){
        this.left = left;
        this.right = right;
    }
    public void sum(){
        System.out.println(this.left+this.right);
    }
      
    public void avg(){
        System.out.println((this.left+this.right)/2);
    }
}
  
public class CalculatorDemo {
      
    public static void main(String[] args) {
          
        Calculator c1 = new Calculator();
        c1.setOprands(10, 20);
        System.out.println(c1);	// 객체만을 println 메소드의 인자로 넣게되면, Java는 내부적으로 .toString을 호출한다.
        // toString() 메소드는 Object의 메소드이며, 모든 클래스는 Object 클래스를 상속 받기 때문에 정의하지 않아도 사용이 가능하다.
        // toString은 어떠한 객체가 있을 때, 그 객체를 문자화 시켜주는 메소드이다.
    }
  
}
```

25라인에 아래 코드는 클래스 `Calculator`의 인스턴스 `c1`을 화면에 출력하고 있다.

``` java
System.out.println(c1);
```

결과는 아래와 같다. @ 뒤의 내용은 각자 다르다.

``` java
progenitor.Calculator@11be650f
```

이것은 인스턴스 `c1`이 클래스 `Calculator`의 인스턴스라는 의미다. @ 뒤의 내용은 인스턴스에 대한 고유한 식별 값이라고 생각하면 된다.

위의 정보도 유용한 정보이지만 클래스 설계자의 필요에 따라서 `toString`의 결과를 더욱 유용하게 만들 수 있다. 예를들어 계산기 인스턴스의 `left`, `right` 값을 알 수 있다면 개발을 좀 더 편하게 할 수 있을 것이다.

``` java
package progenitor;
 
class Calculator{	// 암시적으로 Object라는 부모 클래스를 모든 클래스가 상속 받고 있다.
    int left, right;
      
    public void setOprands(int left, int right){
        this.left = left;
        this.right = right;
    }
    public void sum(){
        System.out.println(this.left+this.right);
    }
      
    public void avg(){
        System.out.println((this.left+this.right)/2);
    }
    
    public String toString(){	// Object 클래스의 toString() 메소드 오버라이딩
        return "left : " + this.left + ", right : "+ this.right;
    }
}
  
public class CalculatorDemo {
      
    public static void main(String[] args) {
          
        Calculator c1 = new Calculator();
        c1.setOprands(10, 20);
        System.out.println(c1);	// 객체만을 println 메소드의 인자로 넣게되면, Java는 내부적으로 .toString을 호출한다.
        System.out.println(c1.toString());	// toString() 메소드를 호출하건 안하건 동일한 결과를 보여준다.
        // toString() 메소드는 Object의 메소드이며, 모든 클래스는 Object 클래스를 상속 받기 때문에 정의하지 않아도 사용이 가능하다.
        // toString은 어떠한 객체가 있을 때, 그 객체를 문자화 시켜주는 메소드이다.
    }
  
}
```

실행결과

``` java
left : 10, right : 20
left : 10, right : 20
```

클래스 `Calculator`에 `toString`을 재정의(`overiding`)했다. 그리고 인스턴스를 `System.out.println`의 인자로 전달하니까 `toString`을 명시적으로 호출하지 않았음에도 동일한 효과가 나고 있다. `toString` 메소드는 자바에서 특별히 취급하는 메소드다. `toString`을 직접 호출하지 않아도 어떤 객체를 `System.out.println`로 호출하면 자동으로 `toString`이 호출되도록 약속되어 있다.

이를 통해서 인스턴스 `c1`의 상태를 쉽게 파악할 수 있게 되었다.

</br>

## equals

`equals`는 객체와 객체가 같은 것인지를 비교하는 API이다. 객체 간에 같고 다름은 필요에 따라서 달라질 수 있기 때문이다.

``` java
package progenitor;
 
class Student{
    String name;
    Student(String name){
        this.name = name;
    }
    public boolean equals(Object obj) {	// Object 클래스의 equals() 메소드 오버라이딩
        Student _obj = (Student)obj;	// 매개변수로 받은 객체를 Student 데이터 타입으로 형변환 [부모 클래스가 자식 클래스로 형변환을 하려면 객체 앞에 (자식 클래스 이름)을 명시적으로 넣어줘야한다.]
        return name == _obj.name;	// 메소드를 호출한 객체의 name과 매개변수로 전달된 객체의 name을 비교하여 같으면 true, 다르면 false를 반환한다.
    }
}
 
class ObjectDemo {
 
    public static void main(String[] args) {
        Student s1 = new Student("egoing");
        Student s2 = new Student("egoing");
        System.out.println(s1 == s2);
        System.out.println(s1.equals(s2));
 
    }
 
}
```

결과는 아래와 같다.

``` java
false
true
```

아래 코드를 보겠다.

``` java
System.out.println(s1 == s2);
```

결과는 false다.

그 이유는 `s1`과 `s2`가 서로 다른 객체이기 때문이다. 어찌 보면 당연한 결과이지만 두 개의 객체가 논리적으로는 `egoing`이라는 값을 가지고 있기 때문에 두 개의 객체가 같은 객체로 간주 되게 하려면 클래스 `Object`의 메소드 `equals`를 `overiding`하면 된다.

``` java
    public boolean equals(Object obj) {	// Object 클래스의 equals() 메소드 오버라이딩
        Student _obj = (Student)obj;	// 매개변수로 받은 객체를 Student 데이터 타입으로 형변환 [부모 클래스가 자식 클래스로 형변환을 하려면 객체 앞에 (자식 클래스 이름)을 명시적으로 넣어줘야한다.]
        return name == _obj.name;	// 메소드를 호출한 객체의 name과 매개변수로 전달된 객체의 name을 비교하여 같으면 true, 다르면 false를 반환한다.
    }
```

위의 코드 `(Student)obj` 는 메소드 `equals`로 전달된 `obj`의 데이터 타입이 `Object`이기 때문에 이를 `Student` 타입으로 형 변환하는 코드다.  아래 코드를 통해서 현재 객체의 변수 `name`과 `equals`의 인자로 전달된 객체의 변수 `name`을 비교한 결과를 `Boolean` 값으로 리턴하고 있다. 이 값에 따라서 두 개의 객체는 같거나 다른 것이 된다. 

``` java
return name == _obj.name;	// 메소드를 호출한 객체의 name과 매개변수로 전달된 객체의 name을 비교하여 같으면 true, 다르면 false를 반환한다.
```

그런데 `eqauls`를 제대로 사용하기 위해서는 `hashCode`라는 클래스도 함께 구현해야 한다.

1. 객체 간에 동일성을 비교하고 싶을 때는 `==`를 사용하지 말고 `equals`를 이용해야 한다.

2. `equals`를 직접 구현해야 한다면 `hashCode`도 함께 구현해야 한다.

3. `equals`를 직접 구현해야 한다면 eclipse와 같은 개발도구들은 `equals`와 `hashCode`를 자동으로 생성해주는 기능을 가지고 있다.

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/516/2125.png)

4. 그 이유가 분명하지 않다면 비교 연산자 `==` 은 원시 데이터형을 비교할 때만 사용한다.

> 원시 데이터 형(Primitive Data Type)이란 자바에서 기본적으로 제공하는 데이터 타입으로 `byte`, `short`, `int`, `long`, `float`, `double`, `boolean`, `char`가 있다. 이러한 데이터 타입들은 `new` 연산자를 이용해서 생성하지 않아도 사용될 수 있다는 특징이 있다.

</br>

## finalize

`finalize`는 객체가 소멸될 때 호출되기로 약속된 메소드이다. 많은 자바의 전문가들이 이 메소드의 사용을 만류하고 있다.

이 메소드 보다는 가비지 컬렉션(garbage collection)에 대해서 알아보겠다. 인스턴스를 만드는 것은 내부적으로는 컴퓨터의 메모리를 사용하는 것이다. 여기서 말하는 메모리는 RAM을 의미한다. 램은 가장 빠른 저장 장치이기 때문에 컴퓨터 프로그램들은 이 램에 저장된 후에 동작하게 된다. 하지만 램은 가격이 비싸고 용량이 적기 때문에 램은 컴퓨터에서 가장 소중한 저장 장치라고 할 수 있다. 그러므로 램의 적게 사용하는 프로그램이 좋은 프로그램이다. 그런 이유로 많은 프로그래밍 언어들이 램을 효율적으로 사용하기 위해서 더 이상 사용하지 않는 데이터를 램에서 제거할 수 있는 방법들을 제공한다.

하지만 자바에서는 이러한 방법이 제한적으로 제공되고 있는데 그것은 자동으로 해주기 때문이다. 이 작업을 자동화한 것을 가비지 컬렉션이라고 한다. 이를테면 어떤 인스턴스를 만들었고, 그것을 변수에 담았다. 그런데 그 변수를 사용하는 곳이 더 이상 없다면 이 변수와 변수에 담겨있는 인스턴스는 더 이상 메모리에 머물고 있을 필요가 없는 것이다. 자바는 이를 감지하고 자동으로 쓰지 않은 데이터를 삭제한다. 따라서 개발자가 사용하지 않는 데이터를 직접 삭제하는 작업을 하지 않아도 되는 것이다. 이것은 어려운 메모리 관리로부터 개발자들의 부담을 경감시킨 도약이라고 할 수 있다.

그럼에도 불구하고 좋은 에플리케이션을 만들기 위해서는 가비지 컬렉션에 대한 이해는 필요하다.

[Java Garbage collection(NHN Hello world 블로그)](https://d2.naver.com/helloworld/1329)

</br>

## clone

`clone`은 복제라는 뜻이다. 어떤 객체가 있을 때 그 객체와 똑같은 객체를 복제해주는 기능이 `clone` 메소드의 역할이다.

``` java
package progenitor;
 
class Student implements Cloneable{
    String name;
    Student(String name){
        this.name = name;
    }
    protected Object clone() throws CloneNotSupportedException{	// Object 클래스 clone() 메소드 오버라이딩
        return super.clone();	// 부모 클래스(Object 클래스)의 clone() 메소드 반환
        // Object 클래스의 clone() 메소드는 CloneNotSupportedException라는 checked Exception이 throws 되어있다.
        // 예외를 이 클래스에서 처리하지 않고 다음 사용자에게 던진다.
    }
}
 
class ObjectDemo {
 
    public static void main(String[] args) {
        Student s1 = new Student("egoing");
        try {
            Student s2 = (Student)s1.clone();	// s1 객체를 clone() 메소드를 통해 Student 데이터 타입의 s2로 복제를 하는데 s1은 Object 데이터 타입으로 반환되었기 때문에 (Student)를 앞에 명시해주어 형변환을 한다.
            System.out.println(s1.name);
            System.out.println(s2.name);
        } catch (CloneNotSupportedException e) {	// Student 클래스에서 CloneNotSupportedException 예외를 다음 사용자에게 던졌기 때문에 try...catch문을 통해 처리해준다.
            e.printStackTrace();
        }
    }
 
}
```

`Student` 예를 조금 변형했다. 결과는 복사에 성공했다.

``` java
egoing
egoing
```

위의 코드에서 클래스 `Student`가 인터페이스 `Cloneable`을 구현하고 있는 것을 주의 깊게 살펴보겠다. 인터페이스 `Cloneable`의 코드는 실제 내용은 아래와 같다.

``` java
public interface Cloneable {}
```

비어있는 인터페이스다. 그럼에도 불구하고 이것을 사용한 이유는 클래스 `Student`가 복제 가능하다는 것을 표시하기 위한 것이다. 만약 이 인터페이스를 구현하지 않고 있는 클래스에 대한 복제를 시도하면 오류가 발생한다.

만약 복사를 보다 정교하게 하고 싶다면 오버라이딩 한 메소드 `clone`를 직접 구현하면 된다.

</br>

## 이해해야 하는 것과 알아야 하는 것

`Object` 클래스를 놓고 생각해보겠다. 이 클래스가 모든 클래스의 부모라는 사실은 이해의 영역이 아니라 약속의 영역이다. 즉 자바를 만든 측과 자바를 사용하는 측의 약속이다. 그리고 이 클래스가 `clone`이나 `toString`과 같은 메소드를 가지고 있다는 것 또한 이해의 영역이 아니라 숙지해야 하는 영역이다. 한편 모든 클래스가 `toString`을 사용할 수 있고 또한 이 메소드를 새롭게 재정의 할 수 있다는 점은 이해의 영역이다. 어떤 지식을 배울 때는 이해해야 하는 것과 그냥 알아야 하는 것을 잘 분별하는 것이 중요하다.