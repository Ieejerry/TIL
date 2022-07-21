# 상수와 enum

</br>

## 상수

상수는 변하지 않는 값이다. 아래에서 좌항이 변수이고 우항이 상수이다.

``` java
int x = 1;
```

아래와 같은 구문은 있을 수 없다. `1`은 `2`가 될 수 없다.

``` java
1 = 2;
```

상수의 이런 특성을 이용해서 아래와 같은 로직을 작성할 수 있다.

``` java
package constant2;
 
public class ConstantDemo {
    public static void main(String[] args) {
        /*
         * 1. 사과
         * 2. 복숭아
         * 3. 바나나
         */
        int type = 1;
        switch(type){
            case 1:
                System.out.println(57);
                break;
            case 2:
                System.out.println(34);
                break;
            case 3:
                System.out.println(93);
                break;
        }
    }
 
}
```

위와 같은 로직에서 숫자 `1`에 해당하는 과일은 언제나 사과여야 한다. 그러므로 변하지 않는 값인 상수값에 따라서 그 값에 해당하는 과일의 의미를 고정하고 있다. 그런데 주석으로 상수의 의미를 전달하고 있지만 주석이 없어졌거나, 주석이 상수를 사용하는 코드와 멀어진다면 각 숫자에 해당하는 과일이 무엇을 나타내는지 알아보기거 어렵거나 불가능해질 수 있다.

이런 때는 이름이 있다면 더 좋을 것이다. 변수도 상수가 될 수 있다. 변수를 지정하고 그 변수를 `final`로 처리하면 한번 설정된 변수의 값은 더 이상 바뀌지 않는다. 또한 바뀌지 않는 값이라면 인스턴스 변수가 아니라 클래스 변수(`static`)로 지정하는 것이 더 좋다.

``` java
package constant2;
 
public class ConstantDemo {
    private final static int APPLE = 1;
    private final static int PEACH = 2;
    private final static int BANANA = 3;	// 더 이상 변하지 않을 값이기 때문에 final로 선언 및 할당을 해주고, 인스턴스마다 값이 달라질 이유도 없기 때문에 클래스 변수로 선언함.
    public static void main(String[] args) {
        int type = APPLE;	// 각각의 이름만 보고도 구별을 할 수가 있게 됐다.
        switch(type){
            case APPLE:
                System.out.println(57+" kcal");
                break;
            case PEACH:
                System.out.println(34+" kcal");
                break;
            case BANANA:
                System.out.println(93+" kcal");
                break;
        }
    }
}
```

그런데 프로그램이 커지면서 누군가 기업에 대한 상수가 필요해졌다. 해서 아래와 같이 코드를 변경했다.

``` java
package constant2;
 
public class ConstantDemo {
    // fruit
    private final static int APPLE = 1;
    private final static int PEACH = 2;
    private final static int BANANA = 3;
     
    // company
    private final static int GOOGLE = 1;
    //private final static int APPLE = 2;	// 위에서 final로 고정된 APPLE의 값을 변경하려고 하기 때문에 에러가 발생한다.
    private final static int ORACLE = 3;
     
    public static void main(String[] args) {
        int type = APPLE;
        switch(type){
            case APPLE:
                System.out.println(57+" kcal");
                break;
            case PEACH:
                System.out.println(34+" kcal");
                break;
            case BANANA:
                System.out.println(93+" kcal");
                break;
        }
    }
}
```

과일 `APPLE`과 기업 `APPLE`이 서로 같은 이름을 가진다. 이렇게 되면 `APPLE`의 값이 `2`에서 `1`로 바뀐다. 프로그램은 오동작 할 것이다. 다행인 것은 `final`로 선언했기 때문에 컴파일이 되지 않고 이름이 중복되는 문제를 방지 할 수 있다. 그런데 이미 기업에 대한 상수를 작성했고 이것이 이미 다양한 영역에서 사용되고 있는 상태에서 `APPLE`을 추가하려면 낭패가 될 것이다. 이러한 문제를 회피하기 위해서 접두사를 붙여보겠다.

``` java
package constant2;
 
public class ConstantDemo {
    // fruit
    private final static int FRUIT_APPLE = 1;
    private final static int FRUIT_PEACH = 2;
    private final static int FRUIT_BANANA = 3;
     
    // company
    private final static int COMPANY_GOOGLE = 1;
    private final static int COMPANY_APPLE = 2;
    private final static int COMPANY_ORACLE = 3;	// 변수 이름앞에 접두사를 붙여주어 이름의 충돌을 없애고, 접두사를 보고 그 상수들이 어떠한 취지에 속해 있는지 알 수가 있다.
     
    public static void main(String[] args) {
        int type = FRUIT_APPLE;
        switch(type){
            case FRUIT_APPLE:
                System.out.println(57+" kcal");
                break;
            case FRUIT_PEACH:
                System.out.println(34+" kcal");
                break;
            case FRUIT_BANANA:
                System.out.println(93+" kcal");
                break;
        }
    }
}
```

이름이 중복될 확률을 낮출 수 있다. 이러한 기법을 네임스페이스라고 한다. 그런데 상수가 너무 지저분하여 깔끔하게 변경하고 싶을 떄에는 인터페이스를 사용하면 된다.

``` java
package constant2;
 
interface FRUIT{
    int APPLE=1, PEACH=2, BANANA=3;
}
interface COMPANY{
    int GOOGLE=1, APPLE=2, ORACLE=3;
}
 
public class ConstantDemo {
     
    public static void main(String[] args) {
        int type = FRUIT.APPLE;
        switch(type){
            case FRUIT.APPLE:
                System.out.println(57+" kcal");
                break;
            case FRUIT.PEACH:
                System.out.println(34+" kcal");
                break;
            case FRUIT.BANANA:
                System.out.println(93+" kcal");
                break;
        }
    }
}
```

훨씬 깔끔하졌다. 접미사(`FRUIT_`, `COMPANY_`)로 이름을 구분했던 부분이 인터페이스로 구분되기 때문에 언어의 특성을 보다 잘 살린 구조가 되었다. 인터페이스를 이렇게 사용할 수 있는 것은 인터페이스에서 선언된 변수는 무조건 `public static final`의 속성을 갖기 때문이다.

그런데 type의 값으로 누군가 `COMPANY_GOOGLE`을 사용했다면 어떻게 되는지 알아보겠다.

``` java
int type = COMPANY.GOOGLE;
```

결과는 57 Kcal가 나온다. 구글이 57 Kcal가 되는 것이다.

우리 코드는 과일과 기업이라는 두 개의 상수 그룹이 존재한다. 위의 코드는 서로 다른 상수그룹의 비교를 시도했고 양쪽 모두 값이 정수 1이기 때문에 오류를 사전에 찾아주지 못하고 있다. 컴파일러가 이런 실수를 사전에 찾아줄 수 있게 해보겠다.

``` java
package constant2;
 
class Fruit{
    public static final Fruit APPLE  = new Fruit();	// 앞에 public static final은 변수를 고정하기 위해(상수로 만들기 위해) 선언
    public static final Fruit PEACH  = new Fruit();	// 데이터 타입을 클래스 자기 자신의 데이터 타입으로 선언
    public static final Fruit BANANA = new Fruit();	// 자기 자신을 인스턴스화 한 값을 앞에 상수에 할당
}
class Company{
    public static final Company GOOGLE = new Company();
    public static final Company APPLE = new Company();
    public static final Company ORACLE = new Company();
}
 
public class ConstantDemo {
     
    public static void main(String[] args) {
//        if(Fruit.APPLE == Company.APPLE){	// Fruit.APPLE과 Company.APPLE은 데이터 타입이 서로 다르기 때문에 에러가 발생한다.
//            System.out.println("과일 애플과 회사 애플이 같다.");
//        }
    }
}
```

`Fruit`와 `Company` 클래스를 만들고 클래스 변수로 해당 클래스의 인스턴스를 사용하고 있다. 각각의 변수가 `final`이기 때문에 불변이고, `Static`이므로 인스턴스로 만들지 않아도 된다. 결과는 17행에서 에러가 발생한다. 서로 다른 카테고리의 상수에 대해서는 비교조차 금지하게 된 것이다. 언제나 오류는 컴파일 시에 나타나도록 하는 것이 바람직하다. 실행 중에 발생하는 오류는 찾아내기가 더욱 어렵다.

그런데 위의 코드는 두 가지 문제점이 있는데 하나는 `switch` 문에서 사용할 수 없고 또 하나는 선언이 너무 복잡하다는 것이다.

</br>

## enum

`enum`은 열거형(enumerated type)이라고 부른다. 열거형은 서로 연관된 상수들의 집합이라고 할 수 있다. 위의 예제에서는 `Fruit`와 `Company`가 말하자면 열거인 셈이다. 이러한 패턴을 자바 1.5부터 문법적으로 지원하기 시작했는데 그것이 열거형이다. 이전 코드를 `enum`으로 바꿔보겠다.

``` java
package constant2;

/*class Fruit{
    public static final Fruit APPLE  = new Fruit();
    public static final Fruit PEACH  = new Fruit();
    public static final Fruit BANANA = new Fruit();
}*/
enum Fruit{	// enum도 클래스이다.
    APPLE, PEACH, BANANA;	// enum 안에서 상수만 입력을 해주면, 위의 주석처리 된 것과 같은 것이며, 나머지 부분을 암시해준 것이다.
}
enum Company{
    GOOGLE, APPLE, ORACLE;
}
 
public class ConstantDemo {
     
    public static void main(String[] args) {
        /*
        if(Fruit.APPLE == Company.APPLE){
            System.out.println("과일 애플과 회사 애플이 같다.");
        }
        */
        Fruit type = Fruit.APPLE;
        switch(type){	// switch문은 type의 데이터 타입이 Fruit이라는 것을 알고 있기 때문에
            case APPLE:	// 레이블에 상수만 입력해주면 된다.
                System.out.println(57+" kcal");
                break;
            case PEACH:
                System.out.println(34+" kcal");
                break;
            case BANANA:
                System.out.println(93+" kcal");
                break;
        }
    }
}
```

위의 코드를 하나씩 살펴보겠다.

``` java
enum Fruit{
    APPLE, PEACH, BANANA;
}
```

`enum`은 `class`, `interface`와 동급의 형식을 가지는 단위다. 하지만 `enum`은 사실상 `class`이다. 편의를 위해서 `enum`만을 위한 문법적 형식을 가지고 있기 때문에 구분하기 위해서 `enum`이라는 키워드를 사용하는 것이다. 위의 코드는 아래 코드와 사실상 같다.

``` java
class Fruit{
    public static final Fruit APPLE  = new Fruit();
    public static final Fruit PEACH  = new Fruit();
    public static final Fruit BANANA = new Fruit();
    private Fruit(){}
}
```

생성자의 접근 제어자가 `private`이다. 그것이 클래스 `Fruit`를 인스턴스로 만들 수 없다는 것을 의미한다. 다른 용도로 사용하는 것을 금지하고 있는 것이다. `enum`은 많은 곳에서 사용하던 디자인 패턴을 언어가 채택해서 문법적인 요소로 단순화시킨 것이라고 할 수 있다.

아래 코드는 컴파일 에러가 발생한다.

``` java
/*
if(Fruit.APPLE == Company.APPLE){
    System.out.println("과일 애플과 회사 애플이 같다.");
}
*/
```

`enum`이 서로 다른 상수 그룹에 대한 비교를 컴파일 시점에서 차단할 수 있다는 것을 의미한다. 상수 그룹 별로 클래스를 만든 것의 효과를 `enum`도 갖는다는 것을 알 수 있다.

`enum`을 사용하는 이유를 정리하면 아래와 같다.

- 코드가 단순해진다.
- 인스턴스 생성과 상속을 방지한다.
- 키워드 `enum`을 사용하기 때문에 구현의 의도가 열거임을 분명하게 나타낼 수 있다.

</br>

## enum과 생성자

`enum`은 사실 클래스다. 그렇기 때문에 생성자를 가질 수 있다. 아래와 같이 코드를 수정해보겠다.

``` java
package constant2;
 
enum Fruit{	// enum은 클래스이기 때문에 생성자가 존재한다.
    APPLE, PEACH, BANANA;	// enum 안에 상수들은 자기 자신의 클래스를 인스턴스하고 있다.
    Fruit(){
        System.out.println("Call Constructor "+this);	// 기본 생성자를 호출하면, 각 상수들은 자기 자신의 클래스를 인스턴스 했기 때문에 "Call Constructor"가 호출되고, this는 인스턴스를 대표하는 각 상수들이 호출된다.
    }
}
 
enum Company{
    GOOGLE, APPLE, ORACLE;
}
 
public class ConstantDemo {
     
    public static void main(String[] args) {
     
        /*
        if(Fruit.APPLE == Company.APPLE){
            System.out.println("과일 애플과 회사 애플이 같다.");
        }
        */
        Fruit type = Fruit.APPLE;
        switch(type){
            case APPLE:
                System.out.println(57+" kcal");
                break;
            case PEACH:
                System.out.println(34+" kcal");
                break;
            case BANANA:
                System.out.println(93+" kcal");
                break;
        }
    }
}
```

결과는 아래와 같다.

``` java
Call Constructor APPLE
Call Constructor PEACH
Call Constructor BANANA
57 kcal
```

`Call Constructor`가 출력된 것은 생성자 `Fruit`가 호출되었음을 의미한다. 이것이 3번 호출되었다는 것은 필드의 숫자만큼 호출되었다는 뜻이다. 즉 `enum`은 생성자를 가질 수 있다.

하지만 코드를 아래와 같이 바꾸면 컴파일 에러가 발생한다.

``` java
enum Fruit{
    APPLE, PEACH, BANANA;
    public Fruit(){
        System.out.println("Call Constructor "+this);
    }
}
```

이것은 `enum`의 생성자가 접근 제어자 `private`만을 허용하기 때문이다. 덕분에 `Fruit`를 직접 생성할 수 없다. 그렇다면 이 생성자의 매개변수를 통해서 필드(APPLE..)의 인스턴스 변수 값을 부여 할 수 있다. 그런데 방식이 좀 생경하다.

``` java
package constant2;
 
enum Fruit{
    APPLE("red"), PEACH("pink"), BANANA("yellow");	// 상수 뒤 괄호안에 색을 넣어주면 그 색은 생성자의 매개변수 인자가 되고, 그 인자를 전역변수에 할당을 함.
    public String color;
    Fruit(String color){
        System.out.println("Call Constructor "+this);
        this.color = color;
    }
}
 
enum Company{
    GOOGLE, APPLE, ORACLE;
}
 
public class ConstantDemo {
     
    public static void main(String[] args) {
        /*
        if(Fruit.APPLE == Company.APPLE){
            System.out.println("과일 애플과 회사 애플이 같다.");
        }
        */
        Fruit type = Fruit.APPLE;
        switch(type){
            case APPLE:
                System.out.println(57+" kcal, "+Fruit.APPLE.color);	// Fruit 클래스의 APPLE이라는 필드 안에 color 변수 호출
                break;
            case PEACH:
                System.out.println(34+" kcal"+Fruit.PEACH.color);
                break;
            case BANANA:
                System.out.println(93+" kcal"+Fruit.BANANA.color);
                break;
        }
    }
}
```

실행결과는 아래와 같다.

``` java
Call Constructor APPLE
Call Constructor PEACH
Call Constructor BANANA
57 kcal, red
```

아래 코드는 `Fruit`의 상수를 선언하면서 동시에 생성자를 호출하고 있다.

``` java
APPLE("red"), PEACH("pink"), BANANA("yellow");
```

아래 코드는 생성자다. 생성자의 매개변수로 전달된 값은 `this.color`를 통해서 5행의 인스턴스 변수의 값으로 할당된다.

``` java
Fruit(String color){
    System.out.println("Call Constructor "+this);
    this.color = color;
}
```

아래처럼 호출하면 `APPLE`에 할당된 `Fruit` 인스턴스의 `color` 필드를 반환하게 된다.

``` java
System.out.println(57+" kcal, "+Fruit.APPLE.color);
```

열거형은 메소드를 가질수도 있다. 아래 코드는 이전 예제와 동일한 결과를 출력한다.

``` java
package constant2;
 
enum Fruit{
    APPLE("red"), PEACH("pink"), BANANA("yellow");
    private String color;	// 외부에서 color의 값을 바꿀 수 없게 private으로 정의
    Fruit(String color){
        System.out.println("Call Constructor "+this);
        this.color = color;
    }
    String getColor(){	// enum은 클래스이기 때문에 메소드도 가질 수 있다.
        return this.color;	// color를 return
    }
}
 
enum Company{
    GOOGLE, APPLE, ORACLE;
}
 
public class ConstantDemo {
     
    public static void main(String[] args) {
        Fruit type = Fruit.APPLE;
        switch(type){
            case APPLE:
                System.out.println(57+" kcal, "+Fruit.APPLE.getColor());	// enum 메소드 getColor() 호출
                break;
            case PEACH:
                System.out.println(34+" kcal"+Fruit.PEACH.getColor());
                break;
            case BANANA:
                System.out.println(93+" kcal"+Fruit.BANANA.getColor());
                break;
        }
    }
}
```

`enum`은 맴버 전체를 열거 할 수 있는 기능도 제공한다.

``` java
package constant2;
 
enum Fruit{
    APPLE("red"), PEACH("pink"), BANANA("yellow");
    private String color;
    Fruit(String color){
        System.out.println("Call Constructor "+this);
        this.color = color;
    }
    String getColor(){
        return this.color;
    }
}
 
enum Company{
    GOOGLE, APPLE, ORACLE;
}
 
public class ConstantDemo {
     
    public static void main(String[] args) {	// 클래스에는 어떠한 필드가 있는지 확인할 수가 없다. 하지만 enum은 values()라는 메소드를 통해 enum 안에 있는 필드를 확인할 수 있다.
        for(Fruit f : Fruit.values()){	// for-each문을 통해 Fruit enum안에 필드들을 f라는 변수에 하나씩 담는다.
            System.out.println(f+", "+f.getColor());
        }
    }
}
```

열거형의 특성을 정리해보겠다. 열거형은 연관된 값들을 저장한다. 또 그 값들이 변경되지 않도록 보장한다. 뿐만 아니라 열거형 자체가 클래스이기 때문에 열거형 내부에 생성자, 필드, 메소드를 가질 수 있어서 단순히 상수가 아니라 더 많은 역할을 할 수 있다.