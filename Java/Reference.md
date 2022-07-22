# 참조

</br>

## 복제

전자화된 시스템의 가장 중요한 특징은 복제다. 현실의 사물과 다르게 전자화된 시스템 위의 데이터를 복제 하는데는 비용이 거의 들지 않는다. 바로 이러한 특징이 소프트웨어를 기존의 산업과 구분하는 가장 큰 특징이다. 프로그래밍에서 복제가 무엇인가를 살펴보겠다.

``` java
package reference;
 
public class ReferenceDemo1 {
 
    public static void runValue(){
        int a = 1;	// a 라는 변수에 1을 할당
        int b = a;	// a 라는 변수에 할당된 1를 복제하여 변수 b에 할당
        b = 2;	// b 라는 변수에 2를 새롭게 할당
        System.out.println("runValue, "+a);	// 변수 b에는 변수 a에 담긴 1를 복제하여 할당하였기 때문에 변수 a에 담긴 1은 변하지 않는다.
    }
 
    public static void main(String[] args) {
        runValue();
    }
 
}
```

결과

``` java
runValue, 1
```

결과를 보면, 값을 변경한 것은 변수 `b`이기 때문에 변수 `a`에 담겨있는 값은 그대로이다. 변수 `b`의 값에 변수 `a`의 값이 복제된 것이다. 이를 그림으로 표시하면 아래와 같다.

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/516/2131.png)

</br>

## 참조

그런데 자연의 산물이 아니라 거대한 약속의 집합인 소프트웨어의 세계에서 당연한 것은 없다. 이것이 당연하지 않은 이유는 다음 예제를 통해서 좀 더 분명하게 드러난다.

``` java
package reference;
class A{
    public int id;	// 인스턴스 변수 int형 id 선언
    A(int id){	// 매개변수를 가진 생성자 정의
        this.id = id;	// 매개변수로 들어온 인자를 전역변수 id에 할당
    }
}
public class ReferenceDemo1 {
 
	public static void runValue(){
        int a = 1;	// a 라는 변수에 1을 할당
        int b = a;	// a 라는 변수에 할당된 1를 복제하여 변수 b에 할당
        b = 2;	// b 라는 변수에 2를 새롭게 할당
        System.out.println("runValue, "+a);	// 변수 b에는 변수 a에 담긴 1를 복제하여 할당하였기 때문에 변수 a에 담긴 1은 변하지 않는다.
    }
     
    public static void runReference(){
        A a = new A(1);	// a라는 변수에 클래스 A를 인스턴스하고 인자로 1를 전달, 그리하여 인스턴스 a의 id는 1이 할당
        A b = a;	// A라는 참조형 데이터 타입을 똑같이 가진 b라는 변수에 인스턴스 a 할당
        b.id = 2;	// 변수 b에는 클래스 A의 인스턴스가 할당되어 있고, id를 2로 할당
        System.out.println("runReference, "+a.id);	// 원시 데이터 타입과 다르게 참조형 데이터 타입은 다른 변수에 할당을 할 때, 변수에 담긴 인스턴스를 복제하는 것이 아니라 참조 시킨다. 즉, 클래스 A 인스턴스를 변수 a와 b가 같이 사용한다고 생각하면 된다.
    }
 
    public static void main(String[] args) {
        runValue();
        runReference();
    }
 
}
```

결과

``` java
runValue, 1
runReference, 2
```

이 코드의 주인공은 아래와 같다.

``` java
b.id = 2;
System.out.println("runReference, "+a.id);  
```

놀라운 차이점이 있다. 변수 `b`에 담긴 인스턴스의 `id` 값을 `2`로 변경했을 뿐인데 `a.id`의 값도 `2`가 된 것이다. 이것은 변수 `b`와 변수 `a`에 담긴 인스턴스가 서로 같다는 것을 의미한다.

전자화된 세계에서 복제는 가장 중요한 특징이다. 그런데 복제만으로 전자화된 시스템을 설명하는 것은 조금 부족하다. 비유하자면 복제는 파일을 복사하는 것이고 참조는 심볼릭 링크(symbolic link) 혹은 바로가기(윈도우)를 만드는 것과 비슷하다. 원본 파일에 대해서 심볼릭 링크를 만들면 원본이 수정되면 심볼릭 링크에도 그 내용이 실시간으로 반영되는 것과 같은 효과다. 심볼릭 링크를 통해서 만든 파일은 원본 파일에 대한 주소 값이 담겨 있다. 누군가 심볼릭 링크에 접근하면 컴퓨터는 심볼릭 링크에 저장된 원본의 주소를 참조해서 원본의 위치를 알아내고 원본에 대한 작업을 하게 된다. 다시 말해서 원본을 복제한 것이 아니라 원본 파일을 참조(reference)하고 있는 것이다. 덕분에 저장 장치의 용량을 절약할 수 있고, 원본 파일을 사용하고 있는 모든 복제본이 동일한 내용을 유지할 수 있게 된다. 참조는 전자화된 세계의 극치라고 할 수 있다.

프로그래밍에서 광범위하게 사용하는 라이브러리라는 개념도 일종의 참조라고 할 수 있다. 공용 라이브러리를 사용하게 되면 하나의 라이브러리를 여러 애플리케이션에서 공유해서 사용하게 된다. 라이브러리의 내용이 변경되면 이를 참조하고 있는 애플리케이션에도 내용이 반영되게 된다. 또 우리가 변수를 사용하는 이유도 말하자면 참조를 위해서라고 할 수 있다.

아래 두 개의 구문의 차이점을 알아보겠다.

``` java
int a = 1;
```

``` java
A a = new A(1);
```

전자는 데이터형이 `int`이고 후자는 `A`이다. `int`는 기본 데이터형(원시 데이터형, Primitive Data Types)이다. 자바에서는 기본 데이터형을 제외한 모든 데이터 타입은 참조 데이터형(참조 자료형)이라고 부른다. 기본 데이터형은 위와 같이 복제 되지만 참조 데이터형은 참조된다. `new`를 사용해서 객체를 만드는 모든 데이터 타입이 참조 데이터형이라고 생각해도 된다. (단 `String`은 제외다) 이를 그림으로 나타내면 아래와 같다.

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/516/2133.png)

정리하면 변수에 담겨있는 데이터가 기본형이면 그 안에는 실제 데이터가 들어있고, 기본형이 아니면 변수 안에는 데이터에 대한 참조 방법이 들어있다고 할 수 있다.

</br>

## 참조 데이터 형과 매개 변수

그럼 일종의 변수할당이라고 할 수 있는 메소드의 매개변수는 어떻게 동작하는가를 살펴보겠다.

``` java
package reference;
 
public class ReferenceParameterDemo {
     
    static void _value(int b){	// 인자 변수 a를 매개변수 b에 할당
        b = 2;	// 매개변수로 받은 인자에 2를 할당
    }
     
    public static void runValue(){
        int a = 1;	// 변수 a에 1를 할당
        _value(a);	// 메소드 _value에 변수 a를 인자로 전달
        System.out.println("runValue, "+a);	// 변수 a 호출 시 1 출력
    }
     
    static void _reference1(A b){	// 인자 인스턴스 a를 매개변수 b에 할당
        b = new A(2);	// 매개변수로 받은 인자에 새로운 인스턴스 할당
    }
     
    public static void runReference1(){
        A a = new A(1);	// 변수 a에 인스턴스 할당
        _reference1(a);	// 메소드 _reference1에 인스턴스 a를 인자로 전달
        System.out.println("runReference1, "+a.id);	// b는 새로운 인스턴스를 할당 받았기 때문에 각 변수는 서로 다른 인스턴스를 참조하기 때문에 인스턴스 a의 id값은 변하지 않고 1이 출력된다.  
    }
     
    static void _reference2(A b){	// 인자 인스턴스 a를 매개변수 b에 할당
        b.id = 2;	// 인스턴스 a를 인자로 받은 매개변수 b의 id를 2로 할당
    }
 
    public static void runReference2(){
        A a = new A(1);	// 변수 a에 클래스 A 인스턴스를 할당
        _reference2(a);	// _reference2 메소드에 인스턴스 a 인자로 전달
        System.out.println("runReference2, "+a.id);	// 인스턴스 b는 인스턴스 a를 할당 받았기 때문에 인스턴스 b는 인스턴스 a를 참조하고 있다. 인스턴스 b에서 id 값을 바꿨기 때문에 인스턴스 a의 id 값도 바뀌게 된다.
    }
     
    public static void main(String[] args) {
        runValue(); // runValue, 1
        runReference1(); // runReference1, 1
        runReference2(); // runReference2, 2
    }
 
}
```

결과는 아래와 같다.

``` java
runValue, 1
runReference1, 1
runReference2, 2
```

위의 예제는 3가지 경우를 설명하고 있다. 하나씩 살펴보겠다. 

아래 코드는 `_value`의 매개변수로 기본 데이터형(`int`)를 전달했다.

``` java
runValue();
```

메소드 `_value`의 인자로 `a`를 전달했다. 인자 `a`는 매개변수 `b`가 되어서 `_value` 안으로 전달되고 있다. `_value` 안에서 `b`의 값을 변경했다. `_value`가 실행된 후에 `runValue`에서 `a`값을 출력해본 결과 값이 변경되지 않았다. 호출된 메소드의 작업이 호출한 메소드에 영향을 미치지 않고 있다.

두번째 코드를 보겠다. 아래 코드는 `_reference1`의 매개변수로 참조 데이터 타입을 전달하고 있다. 

``` java
runReference1();
```

메소드 `_reference1` 안에서 매개변수 `b`의 값을 다른 객체로 변경하고 있다. 이것은 지역변수인 `b`의 데이터를 교체한 것일 뿐이기 때문에 `runReference1`의 결과에는 영향을 미치지 않는다. 

그런데 다음의 코드는 호출된 메소드의 작업이 호출한 메소드의 변수에 영향을 미친다.

``` java
runReference2();
```

매개변수 `b`의 값을 다른 객체로 교체한 것이 아니라 매개변수 `b`의 인스턴스 변수 `id` 값을 `2`로 변경하고 있다. 이러한 맥락에서 `_reference2`의 변수 `b`는 `runReference2`의 변수 `a`와 참조 관계로 연결되어 있는 것이기 때문에 `a`와 `b`는 모두 같은 객체를 참조하고 있는 변수다.

매개변수를 다른 객체로 변경하는 것과 참조 데이터 타입의 매개변수에 담겨 있는 객체에 접근하는 것은 완전히 다른 의미를 가진다.

</br>

## 참조

- [코드와 오픈소스](https://opentutorials.org/course/1189/6340)