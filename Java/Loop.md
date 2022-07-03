# 반복문
> 생활코딩 Java 입문 강의를 들으면서 강의의 내용 정리

</br>

## 반복문
인간은 반복적인 작업을 잘하지 못한다. 실수하고, 지루해한다. 컴퓨터는 이런 반복적인 작업을 대행하기 위해서 만들어진 기계다. 인간이 하기 싫어하는 바로 그 일을 컴퓨터가 대신하도록 하는 것이 반복문(loop, iteration)이다.

</br>

## 반복문의 문법
반복문의 문법은 몇 가지가 있다. 각각의 구문은 서로 대체 가능하기 때문에 상황과 취향에 따라서 선택해서 사용하면 된다.

</br>

### while
while문의 형식은 아래와 같다.
``` java
while(조건){
    반복 실행 영역
}
```
> 다음 예제는 무한 반복을 발생시킨다. 저장되지 않은 작업이 있다면 모두 정리한 후에 이 명령을 실행하자. 콘솔에서 실행할 경우 Ctrl+C(dnls 나 Cmd+. 단축키를 이용해서 무한 반복을 중지할 수 있다.

``` java
package org.opentutorials.javatutorials.loop;
 
public class WhileDemo {
 
    public static void main(String[] args) {
        while (true) {
            System.out.println("Coding Everybody");
        }
 
    }
 
}
```
이번에는 true를 false로 바꾼 아래의 예제를 실행해보자. 아래 코드는 아예 컴파일조차 되지 않을 것이다. 반복 조건이 false이기 때문에 반복문이 한 번도 실행되지 않을 것이기 때문에 컴파일러가 오류를 발생시키는 것이다. 
> while 조건 안에 true나 false 같이 값이 변하지 않는 고정된 값을 넣는 것을 **하드코딩(hard coding)** 이라고 한다.

``` java
while(false){
    System.out.println("Coding Everybody");
}
```
while 문은 반복조건이 참(true)이면 중괄호 구간을 반복적으로 실행한다. 조건이 false면 반복문이 실행되지 않는다. 여기서 true와 false는 반복의 종료조건이 되는데, 반복문에서 종료조건을 잘못 지정하면 무한 반복이 되거나, 반복문이 실행되지 않는다.

아래의 반복문은 i의 값을 1씩 순차적으로 증가시킴으로써 반복의 지속 여부를 결정하고 있다. 주석으로 첨부한 설명을 주의 깊게 살펴보자. 변수 i는 관습적으로 반복의 조건으로 사용하는 임의의 변수다. 변수 이름으로 다른 것을 사용해도 무방하다.
``` java
int i = 0;
// i의 값이 10보다 작다면 true, 크다면 false가 된다. 현재 i의 값은 0이기 때문에 이 반복문은 실행된다. 
while(i<10){         
    System.out.println("Coding Everybody"+i);
    // i의 값에 1을 더한다. 반복문의 중괄호의 마지막 라인에 도달하면 반복문은 반복문을 재호출한다. 이때 i<10의 값을 검사하게 된다.
    i++;
}
```

</br>

### for
while문을 보면 반복의 횟수를 지정하기 위해서 while문 외부에 변수 i의 값을 초기화하고, while문 안에서 i의 값을 증가시키고 있다. 이것은 코드를 산만하게 할 수 있다. 반복문에서 자주 사용하는 이러한 패턴을 문법적인 형태로 만든 것이 for문이다. for문은 특정한 횟수만큼 반복 실행을 하는 경우에 자주 사용된다. 하지만 for문이나 while문이나 서로 대체 가능하다. 취향에 따라서 선택하면 된다. while과 for의 관계는 조건문으로 비유해서 생각해 볼 수도 있을 것 같다. 조건문의 핵심은 if이지만 연관된 로직들의 응집성을 높이기 위해서 else if, else 등이 도입된 것과 비슷한 관점으로 볼 수 있겠다. 이러한 방향성을 자신의 코드에도 적용 할 수 있도록 노력하자.

형식은 아래와 같다.
``` java
for(초기화; 종료조건; 반복실행){
    반복적으로 실행될 구문
}
```
다음 예제를 보자.
``` java
package org.opentutorials.javatutorials.loop;
 
public class ForDemo {
 
    public static void main(String[] args) {
        for (int i = 0; i < 10; i++) {
            System.out.println("Coding Everybody " + i);
        }
 
    }
 
}
```
for문의 괄호 안에는 반복의 종료 조건이 들어온다. 종료 조건은 크게 3개의 부품으로 구성되는데 아래와 같다.
- 초기화 : 반복문이 실행될 때 1회 실행된다.
- 종료조건 : 초기화가 실행된 후에 종료조건이 실행된다. 종료조건의 값이 false일 때까지 반복문의 중괄호 구간의 코드가 반복 실행된다.
- 중괄호 구간의 실행이 끝나면 반복 실행이 실행된다. 일반적으로 이 곳에 i++와 같이 변수를 증가시키는 로직이 위치하고, 이것이 실행된 후에 종료조건이 실행된다. 종료조건이 false가 될 때까지 이 과정이 반복된다.

</br>

## 반복문이 없다면
coding everybody를 10번 반복해서 출력하고 싶다고 한다면 아래와 같이 코드를 작성하면 된다. 
``` java
System.out.println("coding everybody");
System.out.println("coding everybody");
System.out.println("coding everybody");
System.out.println("coding everybody");
System.out.println("coding everybody");
System.out.println("coding everybody");
System.out.println("coding everybody");
System.out.println("coding everybody");
System.out.println("coding everybody");
System.out.println("coding everybody");
```
이 정도의 작업은 복사&붙여넣기를 이용해서도 할만하다. 하지만 좀 더 큰 규모의 데이터를 다뤄야 한다면 반복문의 효용이 드러나기 시작한다. 예를 들어서 'coding everybody'를 1천 번 출력해야 한다면 위의 예제와 아래 예제의 코드 분량에 큰 차이가 생길 것이다.
``` java
int i = 0;
while(i<10){
    System.out.println("coding everybody");
    i++;
}
```
만약 반복문 없이 coding everybody 뒤에 숫자를 1부터 10까지 붙이고 싶다면 아래와 같이 코드를 작성해야 할 것이다. 행마다 숫자를 바꿔야 하므로 Copy & Paste도 할 수 없다.
``` java
System.out.println("coding everybody1");
System.out.println("coding everybody2");
System.out.println("coding everybody3");
System.out.println("coding everybody4");
System.out.println("coding everybody5");
System.out.println("coding everybody6");
System.out.println("coding everybody7");
System.out.println("coding everybody8");
System.out.println("coding everybody9");
System.out.println("coding everybody10");
```
반복문에서는 아래와 같이 하면 된다.
``` java
int i = 0;
while(i<10){
    System.out.println("coding everybody"+i);
    i++;
}
```
coding everybody 뒤에 붙는 숫자를 2의 배수하고 싶다면 어떻게 해야 할까? 반복문이 없다면 한줄 한줄 수정해야 할 것이다. 반복문에서는 내용을 조금만 변경하면 된다.
``` java
int i = 0;
while(i<10){
    System.out.println("coding everybody"+(i+1)*2);
    i++;
}
```

</br>

## 반복문의 제어

</br>

### break
반복작업을 중간에 중단시키고 싶다면 어떻게 해야 할까?  break를 사용하면 된다. 아래의 예제는 위에서 살펴본 예제를 일부 변형한 것이다.
``` java
package org.opentutorials.javatutorials.loop;
 
public class BreakDemo {
 
    public static void main(String[] args) {
        for (int i = 0; i < 10; i++) {
            if (i == 5)
                break;
            System.out.println("Coding Everybody " + i);
        }
 
    }
 
}
```
위 코드의 결과는 아래와 같다. 종료조건에 따르면 10행이 출력돼야 하는데 5행만 출력되었다. 2행의 if(i == 5) 에 의해서 i의 값이 5일 때 break 문이 실행되면서 반복문이 완전히 종료된 것이다. 반복문 안에서 break가 실행되면 반복문을 즉시 종료시킨다. 참고로 조건문에 의해서 실행되는 코드가 한 줄일 경우 예제와 같이 중괄호를 생략 할 수 있다. 반복문도 반복적으로 실행할 코드가 한 줄일 경우 중괄호를 생략할 수 있다.
``` java
coding everybody 0
coding everybody 1
coding everybody 2
coding everybody 3
coding everybody 4
```

</br>

### continue
그럼 실행을 즉시 중단하면서 반복은 지속해가게 하려면 어떻게 해야 할까? 설명이 어렵다면 예제를 보자. 이전 예제의 break를 continue로 변경했을 뿐이지만 결과는 전혀 다르다.
``` java
package org.opentutorials.javatutorials.loop;
 
public class ContinueDemo {
 
    public static void main(String[] args) {
        for (int i = 0; i < 10; i++) {
            if (i == 5)
                continue;
            System.out.println("Coding Everybody " + i);
        }
 
    }
 
}
```
결과는 아래와 같다. 숫자 5가 보이지 않는다. 왜 그럴까? i의 값이 5가 되었을 때 실행이 중단됐기 때문이다. continue 구문은 이 명령이 나타나는 이후의 로직을 실행하지 않도록 한다. 하지만 반복문 자체를 중단하는 것이 아니고 다시 반복문이 실행된다.
``` java 
Coding Everybody 0
Coding Everybody 1
Coding Everybody 2
Coding Everybody 3
Coding Everybody 4
Coding Everybody 6
Coding Everybody 7
Coding Everybody 8
Coding Everybody 9
```

</br>

## 반복문의 중첩
반복문 안에는 다시 반복문이 나타날 수 있다. 다음 예제를 보자. 다음 예제는 00, 01, 02....99 까지를 화면에 출력한다.
``` java
package org.opentutorials.javatutorials.loop;
 
public class LoopDepthDemo {
 
    public static void main(String[] args) {
        for (int i = 0; i < 10; i++) {
            for (int j = 0; j < 10; j++) {
                System.out.println(i + "" + j);
            }
        }
 
    }
 
}
```
> 단순히 글자를 반복적으로 출력하기 위해서 반복문을 사용한다고 생각할 수도 있다. 하지만 반복문의 진가는 배열과 결합했을 때 나타난다. 다음 토픽인 배열에서 반복문의 진가를 살펴보자.