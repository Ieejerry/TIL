# Array - Java API

</br>

## 배열의 생성

아래는 `numbers1`이라는 변수에 4개의 int 데이터 타입을 담을 수 있는 배열을 만드는 방법이다. 자바에서는 배열도 객체이기 때문에 `new`를 이용해서 배열을 생성해야 한다.

</br>

``` java
int[] numbers1 = new int[4];
```

</br>

만약 문자열 엘리먼트를 사용한다면 아래와 같이 하면 된다.

</br>

``` java
String[] strings = new String[4];
```

</br>

배열에 값을 저장할 때는 아래와 같이 한다.

</br>

``` java
numbers1[0] = 10;
numbers1[1] = 20;
numbers1[2] = 30;
```

</br>

배열 `numbers1[0]`에서 숫자 0은 배열의 인덱스를 가리킨다. 즉 `numbers1[0] = 10;`은 인덱스 0번째 엘리먼트가 10이라는 의미이다.

배열의 생성과 값을 설정하는 것을 한 번에 하고 싶다면 아래와 같이 하시면 된다.

</br>

``` java
int[] numbers2 = {10, 20, 30, 40};
int[] numbers3 = new int[] {10, 20, 30, 40};
```

</br>

## 값 가져오기

값을 가져올 때는 아래와 같이 하면 된다.

</br>

``` java
numbers1[0]
```

</br>

가져온 값을 가지고 아무것도 하지 않고 있기 때문에 위의 코드는 동작하지 않습니다. 화면에 출력을 해보겠다.

</br>

``` java
System.out.println(numbers1[0]);
```

```
10
```

</br>

결과는 10이다. 인덱스는 0부터 시작한다.

아직 값을 지정하지 않은 엘리먼트를 조회해보겠다.

</br>

``` java
System.out.println(strings[3]);
```

```
null
```

</br>

숫자 형식의 배열에는 값이 지정되지 않은 엘리먼트의 값은 0 이고, 만약 배열의 데이터 타입이 문자열과 같은 객체라면 null이 된다.

</br>

## 배열의 크기

배열의 크기를 알고 싶으면 `length` 메소드를 사용하시면 된다.

</br>

``` java
System.out.println(numbers1.length);
```

```
4
```

</br>

배열의 크기는 배열을 생성할 때 지정한 크기와 같다. 자바의 배열에서는 값이 지정된 배열의 개수를 알려주는 기능이 기본적으로 제공되지 않는다. 만약 이걸 알고 싶다면 데이터를 넣거나 제거할 때 어딘가에 기록해두어야 한다. 

바로 이런 이유에서 자바에서는 `ArrayList`나 `LinkedList`와 같은 리스트를 사용한다. 리스트는 자동으로 엘리먼트를 수용할 수 있는 크기가 조정되고 또 리스트 내의 엘리먼트의 실제 개수를 알려준다.

</br>

## 배열과 반복

모든 데이터 스트럭쳐는 반복과 밀접한 관계를 가지고 있다. 데이터 스트럭쳐는 복수의 데이터를 저장하는 일종의 저장소이고 복수의 데이터를 일괄적으로 처리하려면 반복작업이 필수적이다. 반복문을 이용해서 배열의 데이터를 처리해보겠다.

</br>

``` java
int i=0;
while(numbers1.length > i){
    System.out.println(numbers1[i]);
    i++;
}
```

```
10
20
30
40
```

</br>

변수 `i`는 몇 번 반복했는지를 적어두기 위한 용도이다. 반복 실행을 할 때마다 이 값을 1씩 증가시킨다. 이 값이 배열의 크기 보다 작은 동안 반복 실행한다.

for문을 사용하는 방법도 있다. for문은 while문의 이런 패턴을 문법적으로 지원하는 기능이라고 할 수 있다.

</br>

``` java
for(i=0; numbers1.length>i; i++) {
    System.out.println(numbers1[i]);
}
```

```
10
20
30
40
```

</br>

위의 코드는 이전의 while문과 정확하게 동일한 코드이다. 하지만 변수 `i`의 초깃값을 지정하고, 값을 증가시키고, 조건을 확인하는 코드가 문법적으로 정의되어 있다. 코드의 가독성이 좋아졌다. 반복횟수가 확정적일 때는 for문을 사용하는 것이 좋다.

</br>

## 배열의 한계

자바의 배열은 기능적으로 한계가 많다. 배열의 크기를 배열을 생성할 때 지정하는 것이나, 배열의 크기를 변경할 수 없는 것도 몹시 불편한 일이다. 또 배열에서 설정된 엘리먼트의 개수를 알아낼 수 없는 것도 불편하다. 그렇다고 배열이 쓸모가 없는 것은 아니다. 데이터의 크기가 확정적일 때 배열을 사용하는 것이 메모리나 처리속도 면에서 좋다. 또한 배열은 다른 데이터 스트럭쳐의 부품이 되기도 한다. 기능이 최소한일수록 좋은 부품이 될 수 있다. 기능이 많으면 사용하기는 좋아도 그것을 사용할 수 있는 용도가 제한되기 때문이다. 

그럼 배열의 이런 한계를 극복하기 위해 조금 더 개선된 기능의 데이터 스트럭쳐를 고안할 필요가 있다. 그런 데이터 스트럭쳐가 바로 `list`이다.

</br>

## 전체코드

</br>

``` java
package list.array.api;
 
public class Main {
 
    public static void main(String[] args) {
         
        int[] numbers1 = new int[4];
         
        String[] strings = new String[4];
         
        numbers1[0] = 10;
        numbers1[1] = 20;
        numbers1[2] = 30;
         
        int[] numbers2 = {10, 20, 30, 40};
        int[] numbers3 = new int[] {10, 20, 30, 40};
         
        System.out.println("System.out.println(numbers1[0]);");
        System.out.println(numbers1[0]);
        
        System.out.println();
         
        System.out.println("System.out.println(numbers1[3]);");
        System.out.println(numbers1[3]);
        
        System.out.println();
         
        System.out.println("System.out.println(numbers1.length);");
        System.out.println(numbers1.length);
        
        System.out.println();
         
        System.out.println("while");
        int i=0;
        while(numbers1.length > i){
            System.out.println(numbers1[i]);
            i++;
        }
        
        System.out.println();
         
        System.out.println("for");
        for(i=0; numbers1.length>i; i++){
            System.out.println(numbers1[i]);
        }
    }
 
}
```

</br>