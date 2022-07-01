# 연산자
## 연산자란
연산자(演펴다연 算계산산 子, operator)란 특정한 작업을 하기 위해서 사용하는 기호를 의미한다. 작업의 종류에 따라서 대입 연산자, 산술 연산자, 비교 연산자, 논리 연산자 등이 있다. 이번 수업에서는 가장 기초적인 연산자에 대해서 알아보고, 여기서 다루지 않는 연산자들은 각 연산자가 실제로 사용되는 맥락에서 차차 알아보겠다.

</br>

## 산술 연산자
산술(算셈산 術재주술, Arithmetic)연산자는 수학적인 계산에 사용되는 연산자다. 기초적인 수학적 소양이 있다면 어려운 연산자는 없다. 다만 수학에서 사용하는 연산자와 프로그래밍에서 사용하는 연산자는 기호의 모양이 조금 다르다.

아래 표를 보자.
| | |
|---|---|
| + | 더하기 |
| - | 빼기 |
| * | 곱하기 |
| / | 나누기 |
| % | 나머지 |

밑에 세가지 부분이 프로그래밍과 수학의 기호가 다른 연산자들이다.  연산자들의 사용법을 예제를 통해서 알아보자.
``` java
package org.opentutorials.javatutorials.operator;
 
public class ArithmeticDemo  {
    public static void main(String[] args) {
        // result 의 값은 3
        int result = 1 + 2;
        System.out.println(result);
  
        // result 의 값은 2
        result = result - 1;
        System.out.println(result);
  
        // result 의 값은 4
        result = result * 2;
        System.out.println(result);
  
        // result 의 값은 2
        result = result / 2;
        System.out.println(result);
  
        // result 의 값은 10
        result = result + 8;
        // result 의 값은 3
        result = result % 7;
        System.out.println(result);
    }
}
```
결과는 아래와 같다.
``` java
3
2
4
2
3
```
연산자 중에 다소 난이도가 있는 나머지에 대해서 알아보자.
``` java
package org.opentutorials.javatutorials.operator;
 
public class RemainerDemo {
    public static void main(String[] args) {
        int a = 3;
        System.out.println(0%a);
        System.out.println(1%a);
        System.out.println(2%a);
        System.out.println(3%a);
        System.out.println(4%a);
        System.out.println(5%a);
        System.out.println(6%a);
    }
}
```
결과는 아래와 같다.
``` java
0
1
2
0
1
2
0
```
나머지는 오른쪽의 피연산자의 값을 왼쪽의 피연산자의 값으로 나누었을 때 나머지 수를 의미한다. 나머지에 대해서 잘 모르겠다면 [중학 수학 강의](https://www.youtube.com/watch?v=TMJ3sNMMGJg)를 참고하자. 결과를 자세히 보면 재미있는 규칙성을 발견할 수 있다. 숫자가 0~2를 단위로 순환하고 있다. 나머지를 이용하면 수가 증가함에 따라서 규칙적으로 순환하는 값을 만들 수 있다. 지금 단계에서 중요한 내용은 아니다.

+ 연산자는 숫자와 숫자를 더할 때 사용되지만, 문자열과 문자열을 결합할 때도 사용된다. 아래의 예제를 보자.
``` java
package org.opentutorials.javatutorials.operator;
 
class ConcatDemo {
    public static void main(String[] args){
        String firstString = "This is";
        String secondString = " a concatenated string.";
        String thirdString = firstString+secondString;
        System.out.println(thirdString);
    }
}
```
결과는 다음과 같다.
``` java
This is a concatenated string.
```
그럼 조금 복잡한 사례를 접해보자. 자바는 데이터 타입이 있기 때문에 같은 숫자임에도 정수와 실수라는 형식이 존재한다. 그럼 타입별로 나누기한 결과는 어떻게 될까?
``` java
package org.opentutorials.javatutorials.operator;
 
public class DivisionDemo {
      
    public static void main(String[] args) {
        int a = 10;
        int b = 3;
          
        float c = 10.0F;
        float d = 3.0F;
          
        System.out.println(a/b);
        System.out.println(c/d);
        System.out.println(a/d);
          
    }
  
}
```
결과는 다음과 같다.
``` java
3
3.3333333
3.3333333
```
첫 번째 결과는 정수와 정수를 나눈 것이다. 3은 나머지의 몫이고, 나머지는 버려졌다. 정수는 소수점을 표현할 수 없으므로 정수만 표시된 것이다.

세 번째 결과는 정수에서 실수를 나눈 것이다. 이 경우 암시적으로 형 변환이 일어나기 때문에 정수가 실수가 된다.

</br>

## 단항 연산자
1+2에서 사용한 연산자 +는 이항(二두이 項항목항, infix operator) 연산자이고, 좌항인 1과 우항인 2를 더해주는 작업을 하고 있다. 단항(單홑단 項항목항, unary) 연산자는 하나의 항을 대상으로 연산이 이루어지는 연산자이다. 다음은 자바에서 제공하는 단항 연산자들이다.
| | |
|---|---|
| + | 양수를 표현한다. 실제로는 사용할 필요가 없다. |
| - | 음수를 표현한다. |
| ++ | 증가(increment) 연산자로 항의 값을 1씩 증가 시킨다. |
| -- | 감소(Decrement) 연산자 |

아래는 단항 연산자들을 사용한 예제다.
``` java
package org.opentutorials.javatutorials.operator;
 
public class PrePostDemo {
    public static void main(String[] args) {
        int i = 3;
        i++;
        System.out.println(i); // 4 출력
        ++i;
        System.out.println(i); // 5 출력
        System.out.println(++i); // 6 출력
        System.out.println(i++); // 6 출력
        System.out.println(i); // 7 출력
    }
}
```
``` java
4
5
6
6
7
```
3행을 보면 i의 값이 3이다. 4행에서 i++를 한 후에 5행에서 출력한 결과는 4가 되었다. ++는 자신과 결합되어 있는 항의 값에 1을 더하는 연산을 한다. 이것은 아래와 의미가 같다. 자주 사용되는 연산이기 때문에 축약된 형태로 지원하는 것이다.
``` java
i = i + 1;
```
6행은 4행과 다르게 ++가 i 앞에 나왔다. 결과는 5다. ++가 i의 앞에 붙은 것이나 뒤에 붙은 것이나 결과는 같은 것 같다. 하지만 8행의 결과는 6이고, 9행의 결과값도 6이다. 무언가 이상하다. ++i는 i의 값에 1이 더해진 값을 출력하는 것이고, i++는 이것이 속해있는 println에 일단 현재 i의 값을 출력하고, println의 실행이 끝난 후에 i의 값이 증가하는 특성이 있다. 중요한 내용은 아니다. 이해가 안되면 일단 넘어가자.

</br>

## 연산의 우선순위
실제로 프로그래밍을 하게 되면 다양한 연산자들을 복합적으로 사용하게 된다. 이럴 때 연산의 선후 관계가 분명하지 않으면 혼란스러울 것이다. 아래는 자바에서 제공하는 연산자들 간의 우선순위를 정리한 표이다.
| 우선순위 | 연산자 | 결합방향 |
|---|---|---|
| 1 | [ ] | → |
| | () | |
| | . | |
| 2 | ++ | ← |
| | -- | |
| | +(양수) -(음수) | |
| | ~ | |
| | ! | |
| | (type) | |
| | new | |
| 3 | * / % | → |
| 4 | +(더하기) -(빼기) | → |
| | +(문자 결합 연산자) | |
| 5 | << | → |
| | >> | | |
| | >>> | |
| 6 | < <= | → |
| | > >= | |
| | instanceof | |
| 7 | == | → |
| | != | |
| 8 | & | → |
| 9 | ^ | → |
| 10 | \| | → |
| 11 | && | → |
| 12 | \|\| | → |
| 13 | ? : | ← |
| 14 | = | ← |
| | *= /= += -= %= | |
| | <<= >>= >>>= | |
| | &= ^= \|= | |

위의 표를 보는 방법을 알아보자. 아래를 계산해보자.
``` java
int a = 4-3*6;
```
위의 구문에는 3가지의 연산자가 등장한다. =, -, * 이다. 표에 따라서 우선순위 별로 배열해보면 *, -, =가 된다. 그러므로 연산자 *가 제일 먼저 실행된다. 따라서 첫 번째 연산은 3*6이 된다. 그 값은 18이다. 그다음 우선순위는 -다. 4-18을 해야 하는데 빼기의 결합 방향은 →이다. 따라서 4에서 18을 빼야 한다. 그 결과는 -14가 된다. 그다음 우선순위는 대입 연산자인 '='이다. '='의 결합방향은 '←'이기 때문에 -14를 변수 a에 대입해서 연산이 끝나게 된다. 

위의 표를 외울 필요는 없다. 자연스럽게 이해하게 된다. 다만, 헷갈리는 경우가 있을 때 이 표의 도움을 받도록 하자.