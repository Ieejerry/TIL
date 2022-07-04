# 배열
> 생활코딩 Java 입문 강의를 들으면서 강의의 내용 정리

</br>

## 배열
배열(Array)은 연관된 정보를 그룹핑 하는데 사용한다. 이해를 돕기 위해서 아래 비유를 들어보겠다.

> 쉽게 말해 하나의 변수에 여러가지 데이터를 넣어 그룹을 지어 관리하는 것을 뜻한다.

</br>

## 상수의 사용
변수에 상수를 대입하는 것과 변수에 배열을 대입하는 것의 차이를 학급의 예를 들어서 생각해보자. 1반에는 50명의 학생이 있다. 각각의 학생들은 각자의 이름이 있다. 이것을 상수라고 치자. 반장과 부반장을 뽑았다. 그럼 아래와 같이 될 것이다. 최진혁과 최유빈이라는 상수를 반장과 부반장이라는 변수에 대입했다. 이것을 코드화해보자. 이것은 실제로는 동작하지 않는 [의사코드](https://ko.wikipedia.org/wiki/%EC%9D%98%EC%82%AC%EC%BD%94%EB%93%9C)이다.

반장 = '최진혁';   
부반장 = '최유빈';

이것의 효용은 분명하다. 교실에 들어온 선생님은 그 반의 반장이 정확하게 누군지 몰라도 반장에게 어떠한 지시를 내릴 수 있다. 반장이 전학을 가서 부반장이 반장이 되었다고 해도 아무 문제 없이 반장에게 지시할 수 있다. 이것이 변수와 상수의 관계라고 할 수 있다.

</br>

## 배열의 사용
이번에는 1반이라는 개념을 통해서 배열에 대해서 생각해보자. 학급을 나누는 이유는 학생들을 관리하기 위해서 일 것이다. 학교에 1000명의 학생이 있는데 이 학생들에게 학급을 부여하지 않는다면 큰 혼란이 올 것이다. 예를 들어서 학생 상담을 한다고 해보자. 이를 위해서 1000명의 학생들을 대상으로 한사람 한사람 호명한다면 대단히 비효율적인 일이 될 것이다. 이제 반이라는 개념을 도입해보자. 1반 학생들 상담 받으러 오세요.라고 하면 된다. 이것을 코드로는 아래와 같이 표현한다.

1반 = {'최진혁', '최유빈', ...., '이고잉'}

1반은 변수고, 최진혁, 최유빈, 이고잉 외 47명의 학생은 이 변수에 소속된 상수가 되는 것이다.

</br>

## 배열의 개념
배열에 대한 기술적인 설명을 하자면, 배열은 연관된 데이터를 모아서 관리하기 위해서 사용하는 데이터 타입이다. 변수가 하나의 데이터를 저장하기 위한 것이라면 배열은 여러 개의 데이터를 저장하기 위한 것이라고 할 수 있다.

</br>

## 배열의 생성
배열을 생성하는 방법을 알아보자.
``` java
package org.opentutorials.javatutorials.array;
 
public class DefineDemo {
 
    public static void main(String[] args) {
 
        String[] classGroup = { "최진혁", "최유빈", "한이람", "이고잉" };
 
    }
 
}
```
String[] classGroup에서 classGroup은 배열이 담길 변수의 이름이다. String[]은 classGroup에 담을 배열에 담길 데이터의 타입이 문자열의 배열이라는 의미다. 배열을 선언할 때는 데이터 타입 뒤에 []를 붙여야 한다. []가 없다면 classGroup는 배열이 아니라 문자열 데이터 타입을 갖는 변수가 된다. 배열에 소속될 데이터들은 중괄호 안에 위치한다. 그리고 각각의 데이터들은 쉼표로 구분된다.

배열의 첫 번째 역할은 연관된 데이터를 저장하는 것이다. 위의 예제는 데이터를 저장하는 컨테이너로서 배열의 면모를 잘 보여주고 있다. 저장했으면 저장한 것을 꺼내오는 이슈가 생긴다. 아래의 예제는 배열에 담겨있는 데이터를 꺼내오는 방법을 보여준다.
``` java
package org.opentutorials.javatutorials.array;
 
public class GetDemo {
 
    public static void main(String[] args) {
        String[] classGroup = { "최진혁", "최유빈", "한이람", "이고잉" };
        System.out.println(classGroup[0]);
        System.out.println(classGroup[1]);
        System.out.println(classGroup[2]);
        System.out.println(classGroup[3]);
 
    }
 
}
```
결과는 아래와 같다.
``` java
최진혁
최유빈
한이람
이고잉
```
classGroup[0] 처럼 배열이 담겨있는 변수의 이름 뒤에 대괄호를 붙이고 그 안에 0부터 시작하는 숫자를 입력하면 순차적으로 값을 가져올 수 있다.

다음 예제는 배열을 정의하는 다른 방법과 배열에 담겨 있는 값의 수를 알아내는 방법을 보여준다.
``` java
package org.opentutorials.javatutorials.array;
 
public class LengthDemo {
 
    public static void main(String[] args) {
        String[] classGroup = new String[4];
        classGroup[0] = "최진혁";
        System.out.println(classGroup.length);
        classGroup[1] = "최유빈";
        System.out.println(classGroup.length);
        classGroup[2] = "한이람";
        System.out.println(classGroup.length);
        classGroup[3] = "이고잉";
        System.out.println(classGroup.length);
 
    }
 
}
```
위의 결과는 아래와 같다.
``` java
4
4
4
4
```

.length는 배열에 실제 담긴 데이터의 숫자를 의미하는 것이 아니라 배열을 처음 생성할 때 지정한 배열의 크기를 의미한다는 점을 주의하자.

지금까지 알아본 배열의 개념을 정리해보자.

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/516/1841.gif)

위와 같이 배열에 담긴 각각의 데이터를 원소(element)라고 한다. classGroup[1]은 최유빈이다. 여기서 숫자 1은 원소 최유빈을 식별하는 식별자이다. 이러한 식별자를 인덱스라고 부른다. 이 식별자는 중복되면 안 되기 때문에 데이터를 입력할 때 자동으로 1씩 증가되면서 만들어진다. 이 배열이 담을 수 있는 원소의 개수를 length라고 한다. 위의 그림에 따르면 classGroup의 길이는 4가 된다. length는 배열에 담긴 원소의 숫자가 아니라 배열을 선언할 때 지정한 배열이 담을 수 있는 값의 크기를 의미한다.

</br>

## 배열의 사용
학교 비유를 조금만 더 활용해보면, 1반 학생들이 상담을 받는다고 했을 때 이 사건에는 다음과 같은 절차가 함축되어 있다고 할 수 있다.
1. 1반 학생들을 번호순으로 정렬해서 줄을 세운다.
2. 상담받은 학생의 숫자를 기록한다.
3. 대기중인 학생과 상담을 한다.
4. 상담받은 학생의 수를 1 증가시킨다.
5. 총원보다 상담받은 학생의 수가 작다면 3번 절차로 돌아간다.
총원과 상담받은 학생의 수가 같다면 상담을 종료하고 업무를 계속한다.

위의 과정을 프로그래밍 언어로 구현해본다면, 아래와 같다.
``` java
package org.opentutorials.javatutorials.array;
 
public class ArrayLoopDemo {
 
    public static void main(String[] args) {
 
        String[] members = { "최진혁", "최유빈", "한이람" };
        for (int i = 0; i < members.length; i++) {
            String member = members[i];
            System.out.println(member + "이 상담을 받았습니다");
        }
 
    }
 
}
```
결과는 아래와 같다.
``` java
최진혁이 상담을 받았습니다
최유빈이 상담을 받았습니다
한이람이 상담을 받았습니다
```
위의 예제에서 주목해야 할 것은 반복문과 배열을 결합한 부분이다. 반복문을 이용해서 배열 members의 내용을 하나씩 꺼낸 후에 상담 결과를 화면에 출력하고 있다. 배열이란 연관된 정보를 하나의 그룹으로 관리하기 위해서 사용하는데 그 정보를 처리 할 때는 반복문을 주로 이용한다. 반복문과 배열은 매우 밀접한 관계에 있다고 할 수 있다.

</br>

## for-each
배열의 내용을 탐색할 때 for 문을 좀 더 간편하게 사용할 수 있는 방법이 있다. 아래 코드를 보자.
``` java
package org.opentutorials.javatutorials.array;
 
public class ForeachDemo {
 
    public static void main(String[] args) {
        String[] members = { "최진혁", "최유빈", "한이람" };
        for (String e : members) {
            System.out.println(e + "이 상담을 받았습니다");
        }
    }
 
}
```
위의 예제는 이전 예제와 정확하게 동일하게 동작한다. 하지만 문법적으로는 간결해졌다. 

for(String e : members)

위의 구문은 배열 members의 값을 변수 e에 담아서 중괄호 구간 안으로 전달해준다. 반복문의 종료조건이나 종료조건을 위해서 기준값을 증가시키는 등의 반복적인 작업을 내부적으로 감춘 것이라고 할 수 있다. 자바 5.0부터 도입된 기능이다.

이클립스에서 오류가 발생한다면 아래와 같이 자바의 버전을 변경해줘야 한다. 가장 높은 버전으로 지정한다.

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/516/2256.png)

## 오류
배열을 사용할 때 흔히 발생하는 오류를 살펴보자.
``` java
String[] members = { "최진혁", "최유빈", "한이람" };
System.out.println(members[3]);     
```
``` java
Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: 3
    at ot_array.ExceptionDemo.main(ExceptionDemo.java:7)
```
> 아직 예외를 배우지는 않았기 때문에 위의 내용은 그냥 오류라고만 생각하겠다.

ArrayIndexOutOfBoundsException은 존재하지 않는 인덱스를 사용하려고 했을 때 발생한다. 배열 members는 인덱스가 2까지 존재하는데 3을 사용했기 때문에 발생한 오류이다. 비유하자면 교실에 50명의 학생이 있는데 51번 학생을 호명한 셈이다. 아래는 동일한 오류를 발생시킨다. 
``` java
String[] members = new String[3];
members[0] = "최진혁";
members[1] = "최유빈";
members[2] = "한이람";
members[3] = "이고잉";
```
배열을 선언 할 때 이 배열의 크기를 3개의 문자열을 수용할 수 있는 크기로 지정했는데 더 많은 데이터를 추가하려고 하기 때문에 발생한 에러다. 50명을 수용 할 수 있는 교실에 51명을 억지로 집어넣으려고 하면서 발생한 오류라고 할 수 있다.

</br>

## 배열의 한계
배열은 초기화할 때 그 크기가 정해진다. 그래서 정해진 크기 이상의 값을 넣을 수 없다. 비유하면, 학생의 수요를 예측하고 그에 따라서 교실을 지으면 그 이상의 학생을 수용 할 수 없는 것과 같다. 부시고 다시 짓든지 새로운 교실을 만들든지 해야 한다. 이러한 한계는 c와 같은 언어에 익숙한 사람에게는 당연한 것이지만, JavaScript나 Python, PHP와 같은 언어에 익숙한 사람에게는 의아할 것이다. 후자의 언어들은 배열의 크기를 미리 정의하고 사용하지 않는다. 물론 방법이 있다. 자바에는 컬렉션 Collection이라는 기능이 있다. Container라고도 부르는 이 기능을 이용하면 JavaScript의 배열과 같이 유연하게 배열을 사용할 수 있다. 컬렉션은 매우 중요한 주제이지만 지금 단계에서는 이것을 이해하기 위한 부품이 부족하다. 객체지향에 대해서 일정한 이해가 있을 때 컬렉션에 대해서도 온전하게 이해할 수 있기 때문이다.