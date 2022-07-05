# 메소드
반복문, 조건문, 변수, 상수와 같은 것들은 사실상 프로그램을 만드는 가장 중요한 도구들이고, 이제부터 배우게 될 메소드나 객체지향과 같은 개념들은 웅장하고, 결함이 없고, 유지보수가 쉬운 애플리케이션을 만들기 위한 기법들이다. 이것들 없이도 프로그램을 만들 수는 있지만, 이것들 없이 규모있는 애플리케이션을 만든다는 것은 현실적으로 어려운 일이다. 지금까지 만드는 방법을 배웠다면 이제부터는 잘 만드는 방법을 익히는 것이라고 생각하며 공부를 하겠다.

</br>

## 메소드
메소드(method)는 코드를 재사용할 수 있게 해준다. 경제적으로 로직을 작성하는 방법에 대해서 공부를 했다.

</br>

## 메소드의 형식
나는 지금까지 메소드를 만들고 사용해봤다. 아래 그림을 보면,

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/516/1834.gif)

이것이 메소드다. 지금까지 수없이 만들었던 저 main이라고 하는 것이 바로 메소드이다. 위의 그림을 자세히 보면 핑크색으로 된 부분과 검은색으로 된 부분이 있다. 이 중에서 검은색으로 된 부분은 나중에 객체지향과 함께 공부해야 본질을 이해할 수 있다고 하니 객체지향을 공부하면서 더욱 자세히 알아보겠다. 메소드를 만들 때 public static이라고 단은 기계적으적어야 한다고 일로 이해하고, 주목할 것은 핑크색으로 강조한 부분이다.

</br>

## 메소드의 정의와 호출
직접 메소드를 만드는 것을 정의라고 하고, 만들어진 메소드를 실행하는 것을 호출이라고 한다.

아래의 예제를 보자.
``` java
package method;
 
public class MethodDemo1 {
    public static void numbering() {
        int i = 0;
        while (i < 10) {
            System.out.println(i);
            i++;
        }
    }
 
    public static void main(String[] args) {
        numbering();
    }
}
```
결과는 아래와 같다.
``` java
0
1
2
3
4
5
6
7
8
9
```
아래 그림을 보자.

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/516/1835.gif)

위의 예제는 numbering이라는 이름의 메소드를 정의하고 있다. 이 메소드는 main이라는 이름의 메소드 안에서 호출되고 있다. 위의 코드는 아래의 코드와 정확하게 동일한 의미를 갖는다.

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/516/1836.gif)

핑크색으로 표시한 부분의 코드를 numbering이라는 이름의 메소드로 묶어서 외부로 분리한 것이다. 그리고 메소드 numbering의 로직이 필요할 때 numbering();이라고하면 메소드 numbering의 로직이 실행된다.

### main
main 메소드는 규칙이다. 만들고 싶은 프로그램이 있다면 반드시 public static void main(String[] args)가 이끄는 중괄호 안에 실행되기를 기대하는 로직을 위치시켜야 한다. 이것은 약속이기 때문에 약속을 지켜야 한다. 그렇게 코드를 작성하면 자바를 실행할 때 자바는 작성한 main 메소드를 실행하게 되는 것이다. 내가 main 메소드를 작성하고, 자바는 main 메소드를 실행하는 관계라고 할 수 있다.

</br>

## 메소드가 없다면
0부터 9까지 출력하는 애플리케이션을 만들었다고 가정하자. 메소드를 모르는 상태에서 0부터 9까지를 5번 출력해야 한다면 아래의 코드 같이 해야된다.
``` java
package method;
 
public class MethodDemo2 {
     
    public static void main(String[] args) {
        int i = 0;
        while(i<10){
            System.out.println(i);
            i++;
        }
         
        i = 0;
        while(i<10){
            System.out.println(i);
            i++;
        }
         
        i = 0;
        while(i<10){
            System.out.println(i);
            i++;
        }
         
        i = 0;
        while(i<10){
            System.out.println(i);
            i++;
        }
         
        i = 0;
        while(i<10){
            System.out.println(i);
            i++;
        }
    }
 
}
```
이 정도는 copy&paste로 해볼 만하다. 하지만 만약 이것을 1000번 해야 한다면? 각각의 로직이 1000 줄에 육박한다면? 그리고 그 내용을 수정해야 한다면? 매우 버거운 일이 되지만, 메소드를 사용한다면 이러한 문제를 현저히 줄일 수 있다. 아래의 예제를 보자. 결과는 같지만 로직은 단 한 번만 등장한다. 이러한 것을 재활용성이라고 한다.
``` java
package method;
 
public class MethodDemo3 {
    public static void numbering() {
        int i = 0;
        while (i < 10) {
            System.out.println(i);
            i++;
        }
    }
 
    public static void main(String[] args) {
        numbering();
        numbering();
        numbering();
        numbering();
        numbering();
    }
}
```

</br>

## 입력과 출력
메소드의 첫 번째 면모인 재활용성에 대해서 알아봤다. 자주 사용하는 로직을 메소드로 만들어두면 호출하는 것을 통해서 간편하게 로직을 재활용할 수 있다. 메소드의 두 번째 면모인 입력과 출력을 알아보자.

살아있는 것들은 외부의 자극에 따라서 반응한다. 외부의 자극이 입력이라면 반응은 출력이라고 할 수 있다. 우리가 아는 쓸모있는 대부분의 프로그램이 사용자의 입력에 따라서 다른 결과를 출력한다. 메소드는 프로그램 안에서 동작하는 하나의 작은 프로그램이라고 할 수 있다. 위에서 살펴본 numbering이라는 메소드는 항상 똑같은 동작만을 반복한다. 이것도 재활용이라는 측면에서는 장점이 있지만, 입력 값에 따라서 출력 값을 달리 제공한다면 더욱 쓸모 있는 프로그램이 될 수 있다.

</br>

## 매개변수와 인자
메소드의 입력 값은 매개변수(parameter)를 통해서 이루어진다. 위의 예제를 조금 개선해보면, 이전 예제는 0부터 9까지의 숫자를 화면에 출력했다. 만약 필요에 따라서 0부터 4까지 출력하고 싶거나 0부터 8까지 출력하고 싶다면 어떻게 해야 할까? 각각에 맞는 메소드를 새로 정의해야 할까? 그렇게 해도 되지만 더 좋은 방법이 있다. 입력 값에 따라서 다른 출력 값을 갖도록 메소드를 정의하면 된다. 즉, 입력을 고민할 때가 된 것이다. 아래의 예제를 보자.
``` java
package method;
 
public class MethodDemo4 {
    public static void numbering(int limit) {
        int i = 0;
        while (i < limit) {
            System.out.println(i);
            i++;
        }
    }
 
    public static void main(String[] args) {
        numbering(5);
    }
}
```
결과는 0부터 4까지 출력한다. 메소드를 호출할 때 괄호에 값을 주고 있는데 저 값을 다른 값으로 바꿔보자. 값에 따라서 다른 결과가 출력되고 있다. 입력을 통해서 메소드의 동작을 제어하고 있다. 아래 그림을 보자.

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/516/1838.gif)

메소드 numbering의 괄호 안에 위치한 숫자 5는 이 메소드가 호출될 때 limit이라는 변수의 값이 된다. 이 값은 메소드 numbering의 중괄호 안에서만 사용할 수 있다. 위의 코드는 아래의 코드와 동일한 의미를 갖는다.

``` java
public static void numbering() {
    int limit = 5;
    int i = 0;
    while (i < limit) {
        System.out.println(i);
        i++;
    }
}
```
여기서 limit이라는 변수는 메소드 numbering의 정의 부에 있는 로직들에게 5라는 값을 전달하고 있다. 호출에서 입력한 값을 로직으로 매개 한다는 의미에서 이러한 변수를 매개변수라고 부른다. 영어로는 parameter다. 그리고 메소드를 호출할 때 전달된 값인 5를 '인자' 영어로는 argument라고 한다. 관습적으로는 매개변수와 인자를 구분하지 않고 부르는 경우도 많다.

</br>

## 복수의 인자
만약 메소드로 여러개의 입력값을 전달하고 싶다면 다음 예제처럼 위의 예제를 개선해서 출력할 숫자의 시작 값과 마지막 값을 입력값으로 전달하면 된다.
``` java
package method;
 
public class MethodDemo5 {
 
    public static void numbering(int init, int limit) {
        int i = init;
        while (i < limit) {
            System.out.println(i);
            i++;
        }
    }
 
    public static void main(String[] args) {
        numbering(1, 5);
    }
 
}
```
결과는 1부터 4까지가 출력된다. 위와 같이 입력 값을 복수로 받고 싶다면 콤마 뒤에 매개변수를 정의해주면 된다. 또 이 메소스를 호출할 때는 매개변수의 순서대로 인자를 배치하면 된다.

</br>

## return
위의 예제는 화면에 숫자를 출력한다. 물론 이것도 출력이지만 좀 더 활용도가 높은 출력 방법이 있다. 아래 예제를 보자. 
``` java
package method;
 
public class MethodDemo6 {
    public static String numbering(int init, int limit) {
        int i = init;
        // 만들어지는 숫자들을 output이라는 변수에 담기 위해서 변수에 빈 값을 주었다.
        String output = "";
        while (i < limit) {
            // 숫자를 화면에 출력하는 대신 변수 output에 담았다.
            output += i;
            i++;
        }
        // 중요!!! output에 담겨 있는 문자열을 메소드 외부로 반환하려면 아래와 같이 return 키워드 뒤에 반환하려는 값을
        // 배치하면 된다.
        return output;
    }
 
    public static void main(String[] args) {
        // 메소드 numbering이 리턴한 값이 변수 result에 담긴다.
        String result = numbering(1, 5);
        // 변수 result의 값을 화면에 출력한다.
        System.out.println(result);
    }
}
```
메소드 내에서 사용한 return은 return 뒤에 따라오는 값을 메소드의 결과로 반환한다. 동시에 메소드를 종료시킨다. 한가지 잊지 말아야 할 점은 return을 통해서 반환할 값의 데이터 형식을 메소드의 이름 옆에 명시해주어야 한다는 것이다.

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/516/1839.gif)

소드가 리턴 할 값을 명시함으로서 numbering이라는 메소드는 반드시 문자열의 값을 리턴한다는 것을 보장할 수 있는 장점이 있다. 모든 일에는 장점과 단점이 있다. 장단의 다면성을 충실하게 응시할 때 적합함을 얻을 수 있다.

만약 반환 값이 없다면 아래와 같이 void를 적어준다.

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/516/1840.gif)

굳이 이렇게 복잡하게 데이터를 리턴하는 이유는 부품으로서의 가치를 높이기 위해서라고 할 수 있다. 만약 이 메소드가 출력한 값을 화면에 출력하는 것이 아니라 파일에 기록하고 싶다면 또는 이메일로 보내고 싶다면 3개의 메소드를 만들고 용도에 따라서 코드를 재작성하는 것도 좋은 방법이다. 하지만 더 좋은 방법은 숫자를 출력하고, 숫자를 파일에 기록하고, 숫자로 이메일을 보내는 작업으로부터 숫자를 계산하는 로직을 분리하는 것이다. numbering은 자신이 어떻게 사용될지 모른다. 누구든지 numbering이라는 메소드를 호출할 때 초기값과 마지막 값을 입력하면 numbering은 숫자를 문자열의 형태로 반환하면 되는 것이다. 코드를 보자.
``` java
package method;
 
import java.io.*; // 무시
 
public class MethodDemo7 {
    public static String numbering(int init, int limit) {
        int i = init;
        String output = "";
        while (i < limit) {
            output += i;
            i++;
        }
        return output;
    }
 
    public static void main(String[] args) {
        String result = numbering(1, 5);
        System.out.println(result);
        try { // 무시
            // 다음 행은 out.txt 라는 파일에 numbering이라는 메소드가 반환한 값을 저장합니다.
            BufferedWriter out = new BufferedWriter(new FileWriter("out.txt"));
            out.write(result);
            out.close();
        } catch (IOException e) {
        } // 무시
    }
}
```
코드에서 무시라고 표시된 부분은 지금 단계에서는 이해하기 어려운 것이기 때문에 무시를 하고, 중요한 것은 numbering이라는 메소드로부터 화면에 출력이라는 구체적인 행위를 제거하고 대신에 처리 결과를 반환하고 있다는 사실이다.

return의 특성에 대해서 조금 더 알아보면, return은 값을 반환하는 동작을 한다. 그런데 이것은 return에 대한 반쪽짜리 설명이다. return은 메소드를 중단시키는 역할도 한다. 코드를 보자.
``` java
package method;
 
public class ReturnDemo {
    public static int one() {
        return 1;
        return 2;
        return 3;
    }
 
    public static void main(String[] args) {
        System.out.println(one());
    }
}
```
위의 코드는 컴파일조차 되지 않는다. 왜냐하면, return 은 메소드를 종료시키는 역할을 하므로 return이 처음 등장한 이후의 구문은 실행되지 않기 때문이다. 하지만 아래의 예제는 문제가 전혀 없다.
``` java
package method;
 
public class ReturnDemo2 {
    public static String num(int i) {
        if(i==0){
            return "zero";
        } else if(i==1){
            return "one";
        } else if(i==2){
            return "two";
        }
        return "none";
    }
 
    public static void main(String[] args) {
        System.out.println(num(1));
    }
}
```
return이 여러 번 등장하지만 return이 중복적으로 실행될 가능성이 없기 때문이다. return "none";를 제거하면 컴파일이 되지 않을 것이다. 

## 복수의 리턴
메소드는 여러 개의 입력 값을 가질 수 있다. 그렇다면 여러 개의 값을 출력하고 싶다면? 자바는 문법적으로 그런 기능을 제공하지 않는다. 하나의 변수에 여러개의 값을 담아서 출력하면 된다. 아래의 코드를 보자.
``` java
package method;
 
public class ReturnDemo3 {
    public static String getMember1() {
        return "최진혁";
    }
 
    public static String getMember2() {
        return "최유빈";
    }
 
    public static String getMember3() {
        return "한이람";
    }
 
    public static void main(String[] args) {
        System.out.println(getMember1());
        System.out.println(getMember2());
        System.out.println(getMember3());
    }
}
```
하나의 메소드는 하나의 값만을 반환할 수 있기 때문에 위와 같이 각각의 회원정보를 반환하는 메소드를 만들었다. 무언가 비정상적이다. 이번엔 배열을 이용한 아래의 코드를 보자. 맴버를 담고 있는 배열을 반환하고 있다. 메소드 getMembers가 리턴한 배열을 members 변수에 담았다. 이 변수를 이용해서 여러 개의 데이터를 처리 할 수 있게 된다.
``` java
package method;
 
public class ReturnDemo4 {
 
    public static String[] getMembers() {
        String[] members = { "최진혁", "최유빈", "한이람" };
        return members;
    }
 
    public static void main(String[] args) {
        String[] members = getMembers();
    }
 
}
```