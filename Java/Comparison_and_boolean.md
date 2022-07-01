# 비교와 Boolean
> 생활코딩 Java 입문 강의를 들으면서 강의의 내용 정리

> 프로그래밍의 비교나 불린은 이것만으로는 효용이 크지 않다. 후속 수업인 반복문과 조건문에서 그 효용이 드러나기 때문에 조금 지루하더라도 조건문까지만 인내하자.

## boolean
불린(Boolean)은 참과 거짓을 의미하는 데이터 타입으로 bool이라고도 부른다. 불린은 정수나 문자와 같이 하나의 데이터 타입인데, 참을 의미하는 true와 거짓을 의미하는 false 두 가지의 값을 가지고 있다. 아래는 비교 연산자들에 대한 설명이다.

</br>

## 비교 연산자 (관계 연산자)
프로그래밍에서 비교란 주어진 값들이 같은지, 다른지, 큰지, 작은지를 구분하는 것을 의미한다. 이때 비교 연산자를 사용하는데 비교 연산자의 결과는 true나 false 중의 하나다. true는 비교 결과가 참이라는 의미이고, false는 거짓이라는 뜻이다.

</br>

### ==
좌항과 우항을 비교해서 서로 값이 같다면 true 다르다면 false가 된다. '='이 두 개인 것을 주의하자. '='이 하나인 것은 대입 연산자로 우항의 값을 좌항의 변수에 대입할 때 사용하는 것으로 의미가 완전히 다르다.
``` java
package org.opentutorials.javatutorials.compare;
 
public class EqualDemo {
 
    public static void main(String[] args) {
        System.out.println(1==2);           //false
        System.out.println(1==1);           //true
        System.out.println("one"=="two");   //false
        System.out.println("one"=="one");   //true
    }
 
}
```

</br>

### !=
'!'는 부정을 의미한다. '같다'의 부정은 '같지 않다'이다. 이것을 기호로는 '!='로 표시한다. 아래의 결과는 !=의 결과인데 ==와 정반대의 결과를 보여준다.
``` java
package org.opentutorials.javatutorials.compare;
 
public class NotDemo {
 
    public static void main(String[] args) {
        System.out.println(1!=2);           //true
        System.out.println(1!=1);           //false
        System.out.println("one"!="two");   //true  
        System.out.println("one"!="one");   //false
    }
}
```

</br>

### >
좌항이 우항보다 크다면 참, 그렇지 않다면 거짓임을 알려주는 연산자다. '<'는 반대의 의미로 언급은 생략하겠다. 
``` java
package org.opentutorials.javatutorials.compare;
 
public class GreaterThanDemo {
 
    public static void main(String[] args) {
        System.out.println(10>20);       //false
        System.out.println(10>2);            //true
        System.out.println(10>10);           //false
    }
}
```

</br>

### >=
좌항이 우항보다 크거나 같다. '<='는 반대의 의미로 언급은 생략하겠다.
``` java
package org.opentutorials.javatutorials.compare;
 
public class GreaterThanOrEqualDemo {
 
    public static void main(String[] args) {
 
        System.out.println(10 >= 20); // false
        System.out.println(10 >= 2); // true
        System.out.println(10 >= 10); // true
    }
}
```

</br>

### .equals
.equals는 문자열을 비교할 때 사용하는 메소드다. 우리는 아직 메소드를 배우지 않았기 때문에 지금은 그냥 이것을 연산자로 이해해도 무방하다. 아래는 문자와 문자를 비교하는 방법이다.
``` java
package org.opentutorials.javatutorials.compare;
 
public class EqualStringDemo {
 
    public static void main(String[] args) {
        String a = "Hello world";
        String b = new String("Hello world");
        System.out.println(a == b);
        System.out.println(a.equals(b));
    }
}
```
변수 a와 b에 각각 문자열을 생성해서 저장했다. 변수 b에 문자열을 만드는 방법은 생성자를 이용하고 있는데 이 방법은 후에 객체 지향 시간에 배우게 된다. 지금은 new String의 괄호 안에 문자열을 넣으면 문자열을 생성할 수 있다고만 알아두자. 결과는 false와 true이다. ==은 두개의 데이터 타입이 동일한 객체인지를 알아내기 위해서 사용하는 연산자이기 때문에 b에 담긴 객체와 일치하지 않는 것이다. 이를 보안하는 비교 방법이 equals이고 이를 이용해서 서로 다른 객체들간에 값이 같은지를 비교할 수 있다. 이 이야기는 지금 단계에서는 이해하기 다소 어려움이 있다. 문자와 문자를 비교할 때는 '=='를 사용하지 않고 .equals를 사용한다고 일단은 알아두자.