# 제네릭

</br>

## 제네릭이란?

제네릭(Generic)은 클래스 내부에서 사용할 데이터 타입을 외부에서 지정하는 기법을 의미한다.

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/516/2136.png)

위의 그림은 아래의 코드를 간략화한 것이다.

``` java
package generic;
 
class Person<T>{	// 클래스의 데이터 타입을 미리 지정하지 않고 인스턴스화 될 때 지정
    public T info;	// 클래스 필드 info 또한 데이터 타입이 인스턴스화 될 때 지정
}
 
public class GenericDemo {
 
    public static void main(String[] args) {
        Person<String> p1 = new Person<String>();	// Person 클래스를 인스턴스하고 데이터 타입을 String으로 지정
        Person<StringBuilder> p2 = new Person<StringBuilder>();
    }
 
}
```

그림을 보면, `p1.info`와 `p2.info`의 데이터 타입은 결과적으로 아래와 같다.

- p1.info : String
- p2.info : StringBuilder

그것은 각각의 인스턴스를 생성할 때 사용한 <> 사이에 어떤 데이터 타입을 사용했느냐에 달려있다. 

클래스 선언부를 보겠다.

``` java
public T info;
```

클래스 `Person`의 필드 `info`의 데이터 타입은 `T`로 되어 있다. 그런데 `T`라는 데이터 타입은 존재하지 않는다. 이 값은 아래 코드의 `T`에서 정해진다.

``` java
class Person<T>{
```

위 코드의 `T`는 아래 코드의 <> 안에 지정된 데이터 타입에 의해서 결정된다. 

``` java
Person<String> p1 = new Person<String>();
```

위의 코드를 나눠보겠다. 아래 코드는 변수 `p1`의 데이터 타입을 정의하고 있다.

``` java
Person<String> p1
```

아래 코드는 인스턴스를 생성하고 있다.

``` java
new Person<String>();
```

즉 클래스를 정의 할 때는 `info`의 데이터 타입을 확정하지 않고 인스턴스를 생성할 때 데이터 타입을 지정하는 기능이 제네릭이다. 

제네릭을 사용하는 이유를 알아보겠다. 

</br>

## 제네릭을 사용하는 이유

### 타입 안전성

``` java
package generic;
class StudentInfo{
    public int grade;
    StudentInfo(int grade){ this.grade = grade; }
}
class StudentPerson{
    public StudentInfo info;
    StudentPerson(StudentInfo info){ this.info = info; }
}
class EmployeeInfo{
    public int rank;
    EmployeeInfo(int rank){ this.rank = rank; }
}
class EmployeePerson{
    public EmployeeInfo info;
    EmployeePerson(EmployeeInfo info){ this.info = info; }
}
public class GenericDemo2 {
    public static void main(String[] args) {
        StudentInfo si = new StudentInfo(2);
        StudentPerson sp = new StudentPerson(si);
        System.out.println(sp.info.grade); // 2
        EmployeeInfo ei = new EmployeeInfo(1);
        EmployeePerson ep = new EmployeePerson(ei);
        System.out.println(ep.info.rank); // 1
        // info의 정보를 담는 클래스가 중복이 일어나게 된다. 하지만 두 인스턴스는 서로 다른 데이터 타입을 가지기 때문에 따로 정의를 해줘야한다.
    }
}
```

그리고 아래 코드를 보겠다. 위의 코드는 `StudentPerson`과 `EmployeePerson`가 사실상 같은 구조를 가지고 있다. 중복이 발생하고 있는 것이다. 중복을 제거해보겠다.

``` java
package generic;
class StudentInfo{
    public int grade;
    StudentInfo(int grade){ this.grade = grade; }
}
class EmployeeInfo{
    public int rank;
    EmployeeInfo(int rank){ this.rank = rank; }
}
class Person{
    public Object info;
    Person(Object info){ this.info = info; }
}
public class GenericDemo2 {
    public static void main(String[] args) {
        Person p1 = new Person("부장");	// 인자로 인스턴스가 들어가야되는데 다른 정보가 들어가도 컴파일도 잘 되고 출력도 잘 된다. 목적으로 했던 의도와 다르게 동작하는데 에러도 뜨지 않는다.
        EmployeeInfo ei = (EmployeeInfo)p1.info;	// String 원시 데이터 타입의 변수를 형변환하는데 컴파일까지는 되지만 실행 시 예외가 발생한다.
        System.out.println(ei.rank);	// 이러한 상황을 타입이 안전하지 않다고 한다.
    }
}
```

위의 코드는 성공적으로 컴파일된다. 하지만 실행을 하면 아래와 같은 오류가 발생한다.

``` java
Exception in thread "main" java.lang.ClassCastException: java.lang.String cannot be cast to org.opentutorials.javatutorials.generic.EmployeeInfo
    at org.opentutorials.javatutorials.generic.GenericDemo.main(GenericDemo.java:17)
```

아래 코드를 보겠다.

``` java
Person p1 = new Person("부장");
```

클래스 `Person`의 생성자는 매개변수 `info`의 데이터 타입이 `Object`이다. 따라서 모든 객체가 될 수 있다. 그렇기 때문에 위와 `EmployeeInfo`의 객체가 아니라 `String`이 와도 컴파일 에러가 발생하지 않는다. 대신 런타임 에러가 발생한다. 컴파일 언어의 기본은 모든 에러는 컴파일이 발생할 수 있도록 유도해야 한다는 것이다. 런타임은 실제로 애플리케이션이 동작하고 있는 상황이기 때문에 런타임에 발생하는 에러는 항상 심각한 문제를 초래할 수 있기 때문이다. 

위와 같은 에러는 타입에 대해서 안전하지 않다고 한다. 즉 모든 타입이 올 수 있기 때문에 타입을 엄격하게 제한 할 수 없게 되는 것이다.

### 제네릭화

이것을 제네릭으로 바꿔보겠다.

``` java
package generic;
class StudentInfo{
    public int grade;
    StudentInfo(int grade){ this.grade = grade; }
}
class EmployeeInfo{
    public int rank;
    EmployeeInfo(int rank){ this.rank = rank; }
}
class Person<T>{
    public T info;
    Person(T info){ this.info = info; }
}
public class GenericDemo {
    public static void main(String[] args) {
        Person<EmployeeInfo> p1 = new Person<EmployeeInfo>(new EmployeeInfo(1));
        EmployeeInfo ei1 = p1.info;
        System.out.println(ei1.rank); // 성공
         
        Person<String> p2 = new Person<String>("부장");
        String ei2 = p2.info;
        System.out.println(ei2.rank); // 컴파일 실패
    }
}
```

`p1`은 잘 동작할 것이다. 중요한 것은 `p2`다. `p2`는 컴파일 오류가 발생하는데 `p2.info`가 `String`이고 `String`은 `rank` 필드가 없는데 이것을 호출하고 있기 때문이다. 여기서 중요한 것은 아래와 같이 정리할 수 있다.

- 컴파일 단계에서 오류가 검출된다.
- 중복의 제거와 타입 안전성을 동시에 추구할 수 있게 되었다.

</br>

## 제네릭의 특성

### 복수의 제네릭

클래스 내에서 여러개의 제네릭을 필요로 하는 경우가 있을 수 있다. 예제를 보겠다.

``` java
package generic;
class EmployeeInfo{
    public int rank;
    EmployeeInfo(int rank){ this.rank = rank; }
}
class Person<T, S>{
    public T info;	// 변수의 데이터 타입을 인스턴스화 할 때 지정
    public S id;	// 변수의 데이터 타입을 인스턴스화 할 때 지정
    Person(T info, S id){ 
        this.info = info; 
        this.id = id;
    }
}
public class GenericDemo2 {
    public static void main(String[] args) {
        Person<EmployeeInfo, int> p1 = new Person<EmployeeInfo, int>(new EmployeeInfo(1), 1);
        // 복수의 제네릭을 사용할 경우
    }
}
```

위의 코드는 예외를 발생시키지만 문제는 다음 예제에서 처리하고 형식만 보겠다. 

즉, 복수의 제네릭을 사용할 때는 `<T, S>`와 같은 형식을 사용한다. 여기서 `T`와 `S` 대신 어떠한 문자를 사용해도 된다. 하지만 묵시적인 약속(convention)이 있다. 그럼 예제의 오류를 해결해보겠다.

### 기본 데이터 타입과 제네릭

제네릭은 참조 데이터 타입에 대해서만 사용할 수 있다. 기본 데이터 타입에서는 사용할 수 없다. 따라서 아래와 같이 코드를 변경한다.

``` java
package generic;
class EmployeeInfo{
    public int rank;
    EmployeeInfo(int rank){ this.rank = rank; }
}
class Person2<T, S>{
    public T info;
    public S id;
    Person2(T info, S id){ 
        this.info = info;
        this.id = id;
    }
}
public class GenericDemo2 {
    public static void main(String[] args) {
        EmployeeInfo e = new EmployeeInfo(1);	// 제네릭에는 참조형 데이터 타입만 들어갈 수 있다.
        Integer i = new Integer(10);	// 원시 데이터 타입 같은 경우에는 참조형 데이터처럼 바꿔줘야하는데 그런 역할을 하는게 래퍼 클래스이다. 래퍼 클래스는 인스턴스처럼 정의하면 된다.
        Person2<EmployeeInfo, Integer> p1 = new Person2<EmployeeInfo, Integer>(e, i);
        System.out.println(p1.id.intValue());	// 래퍼 클래스 Integer가 담고 있는 값을 호출하려면, Integer 래퍼 클래스가 갖고 있는 intValue()라는 메소드를 호출 해야된다.
    }
}
```

`new Integer`는 기본 데이터 타입인 `int`를 참조 데이터 타입으로 변환해주는 역할을 한다. 이러한 클래스를 래퍼(wrapper) 클래스라고 한다. 덕분에 기본 데이터 타입을 사용할 수 없는 제네릭에서 `int`를 사용할 수 있게 된다.

### 제네릭의 생략

제네릭은 생략 가능하다. 아래 두 개의 코드가 있다. 이 코드들은 정확히 동일하게 동작한다. `e`와 `i`의 데이터 타입을 알고 있기 때문이다.

``` java
EmployeeInfo e = new EmployeeInfo(1);
Integer i = new Integer(10);
Person2<EmployeeInfo, Integer> p1 = new Person2<EmployeeInfo, Integer>(e, i);
Person2 p2 = new Person2(e, i);   // 인스턴스를 할 때 변수 앞에 데이터 타입을 지정을 해주기 때문에 Java는 그 변수의 데이터 타입을 알고 있다. 그래서 제네릭을 생략해줘도 무방하다.
```

### 메소드에 적용

제네릭은 메소드에 적용할 수도 있다. 

``` java
package generic;
class EmployeeInfo{
    public int rank;
    EmployeeInfo(int rank){ this.rank = rank; }
}
class Person2<T, S>{
    public T info;
    public S id;
    Person2(T info, S id){ 
        this.info = info;
        this.id = id;
    }
    public <U> void printInfo(U info){	// 제네릭은 클래스뿐만 아니라 메소드에도 사용할 수 있다.
        System.out.println(info);
    }
}
public class GenericDemo2 {
    public static void main(String[] args) {
        EmployeeInfo e = new EmployeeInfo(1);
        Integer i = new Integer(10);
        Person2<EmployeeInfo, Integer> p1 = new Person2<EmployeeInfo, Integer>(e, i);
        p1.<EmployeeInfo>printInfo(e);
        p1.printInfo(e);
    }
}
```

### 제네릭의 제한

**extends**

제네릭으로 올 수 있는 데이터 타입을 특정 클래스의 자식으로 제한할 수 있다.

``` java
package generic;
abstract class Info{
    public abstract int getLevel();
}
class EmployeeInfo extends Info{
    public int rank;
    EmployeeInfo(int rank){ this.rank = rank; }
    public int getLevel(){
        return this.rank;
    }
}
class Person2<T extends Info>{	// 제네릭 T 뒤에 extends Info를 하면 제네릭에는 데이터 타입으로 클래스 Info 혹은 Info를 상속 받은 자식 클래스만 오게 제한한다.
    public T info;
    Person2(T info){ this.info = info; }
}
public class GenericDemo2 {
    public static void main(String[] args) {
        Person2 p1 = new Person2(new EmployeeInfo(1));
        Person2<String> p2 = new Person2<String>("부장");	// String은 Info 클래스를 상속 받지 않았기 때문에 에러가 발생한다.
    }
}
```

위의 코드에서 중요한 부분은 다음과 같다.

``` java
class Person<T extends Info>{
```

즉 `Person`의 `T`는 `Info` 클래스나 그 자식 외에는 올 수 없다.

`extends`는 상속(extends)뿐 아니라 구현(implements)의 관계에서도 사용할 수 있다.

``` java
package generic;
interface Info{
    int getLevel();
}
class EmployeeInfo implements Info{
    public int rank;
    EmployeeInfo(int rank){ this.rank = rank; }
    public int getLevel(){
        return this.rank;
    }
}
class Person2<T extends Info>{	// 제네릭은 꼭 클래스가 아니고, 인터페이스라도 제한할 수 있다. 제네릭 안에서 extends는 상속이 아니라 부모가 누구인지를 가르키는 코드이다.
    public T info;
    Person2(T info){ this.info = info; }
}
public class GenericDemo2 {
    public static void main(String[] args) {
        Person2 p1 = new Person2(new EmployeeInfo(1));
        Person2<String> p2 = new Person2<String>("부장");
    }
}
```

``` java
package generic;
interface Info{
    int getLevel();
}
class EmployeeInfo implements Info{
    public int rank;
    EmployeeInfo(int rank){ this.rank = rank; }
    public int getLevel(){
        return this.rank;
    }
}
class Person2<T extends Info>{	// 제네릭은 꼭 클래스가 아니고, 인터페이스라도 제한할 수 있다. 제네릭 안에서 extends는 상속이 아니라 부모가 누구인지를 가르키는 코드이다.
    public T info;
    Person2(T info){
    	this.info = info;
    	info.getLevel();	// extends로 제한을 건 경우, 부모 클래스 혹은 인터페이스의 필드를 호출할 수 있다.
	}
}
public class GenericDemo2 {
    public static void main(String[] args) {
        Person2 p1 = new Person2(new EmployeeInfo(1));
        Person2<String> p2 = new Person2<String>("부장");
    }
}
```