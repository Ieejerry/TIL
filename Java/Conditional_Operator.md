# 논리 연산자
> 생활코딩 Java 입문 강의를 들으면서 강의의 내용 정리

</br>

## 논리 연산자
[조건문 수업](https://opentutorials.org/module/516/5335)에서 Boolean에 따라서 프로그램이 다르게 동작하도록 하는 방법을 배웠다. 이번 시간에는 Boolean의 값을 결합해서 코드를 좀 더 간결하게 만들 수 있는 논리 연산자(Conditional Operator)에 대해서 알아보자. 뒤에서는 조건문 수업의 예제에 논리 연산자를 결합해 볼 것이다.

</br>

### &&
&&는 좌항과 우항의 값이 모두 참(true)일 때 참이 된다. And라고 읽는다. 다음 예제를 보자. 결과는 1이다. and의 좌우항이 모두 true인 것은 첫 번째 조건문 밖에 없기 때문이다.
``` java
package org.opentutorials.javatutorials.conditionaloperator;
 
public class AndDemo {
 
    public static void main(String[] args) {
        if (true && true) {
            System.out.println(1);
        }
 
        if (true && false) {
            System.out.println(2);
        }
 
        if (false && true) {
            System.out.println(3);
        }
 
        if (false && false) {
            System.out.println(4);
        }
 
    }
 
}
```
논리 연산자를 이용한 사례를 살펴보자. 다음 예제는 논리 연산자를 이용해서 이전 예제를 개선한 것이다.
``` java
package org.opentutorials.javatutorials.conditionaloperator;
 
public class LoginDemo3 {
    public static void main(String[] args) {
        String id = args[0];
        String password = args[1];
        if (id.equals("egoing") && password.equals("111111")) {
            System.out.println("right");
        } else {
            System.out.println("wrong");
        }
    }
}
```
중첩된 if 문을 하나로 줄였다. 덕분에 코드의 복잡성도 낮아졌다. 위의 코드에서 &&는 아래와 같은 의미가 된다.

"id의 값이 egoing이고 password의 값이 111111이면 참이다"

즉 and 연산자의 좌항과 우항이 모두 참일 때 전체가 참이 되는 것이다.

</br>

### ||
||(or)는 좌우항 중에 하나라도 true라면 전체가 true가 되는 논리 연산자다. 다음 예를 보자. 결과는 1,2,3이 출력된다. 마지막 조건문의 or는 좌항과 우항이 모두 false이기 때문에 false가 된다.
``` java
package org.opentutorials.javatutorials.conditionaloperator;
 
public class OrDemo {
 
    public static void main(String[] args) {
        if (true || true) {
            System.out.println(1);
        }
        if (true || false) {
            System.out.println(2);
        }
        if (false || true) {
            System.out.println(3);
        }
        if (false || false) {
            System.out.println(4);
        }
 
    }
 
}
```
다음 예제는 id 값으로 egoing, k8805, sorialgi 중의 하나를 사용하고 비밀번호는 111111을 입력하면 right 외의 경우에는 wrong를 출력하는 예다.
``` java
package org.opentutorials.javatutorials.conditionaloperator;
 
public class LoginDemo4 {
    public static void main(String[] args) {
        String id = args[0];
        String password = args[1];
        if ((id.equals("egoing") || id.equals("k8805") || id.equals("sorialgi"))
                && password.equals("111111")) {
            System.out.println("right");
        } else {
            System.out.println("wrong");
        }
    }
}
```
위의 예제에서는 or와 and를 혼합해서 사용하는 방법을 보여준다. id 값을 테스트하는 구간을 괄호()로 묶었다. 사용자가 id의 값으로 egoing 비밀번호를 111111을 입력했다면 연산의 순서는 아래와 같이 된다.

(id=="egoing" or id=="k8805" or id=="sorialgi") : true가 된다.
password=='111111' : true가 된다.
true(1항) and true(2항) : true가 된다.
사칙 연산을 할 때 괄호부터 계산하는 것과 같은 원리다.

</br>

### !
!는 부정의 의미로 not이라고 읽는다. Boolean의 값을 역전시키는 역할을 한다. true에 !를 붙으면 false가 되고 false에 !을 붙이면 true가 된다. 아래의 결과는 2다.
``` java
package org.opentutorials.javatutorials.conditionaloperator;
 
public class NotDemo {
 
    public static void main(String[] args) {
        if (!true) {
            System.out.println(1);
        }
        if (!false) {
            System.out.println(2);
        }
 
    }
 
}
```