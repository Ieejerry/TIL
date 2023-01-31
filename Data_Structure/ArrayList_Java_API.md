# ArrayList - Java API

Java에서 `ArrayList`는 가장 많이 사용되는 데이터 스트럭쳐이다. 특히 자바의 배열은 동일한 데이터 타입의 엘리먼트만 담을 수 있고 크기가 고정 되어 있기 때문에 사용하기가 까다롭다.

</br>

## 내장된 ArrayList의 사용법

`ArrayList`를 직접 구현하기 전에 자바에서 기본적으로 제공하는 `ArrayList`의 사용법을 먼저 알아야 한다.

</br>

### 생성

`ArrayList`를 사용하기 위해서는 우선 `ArrayList` 객체를 만들어야 한다.

</br>

``` java
ArrayList<Integer> numbers = new ArrayList<>();
```

</br>

`ArrayList`는 `java.util.ArrayList`에 포함되어 있기 때문에 `import`를 해주어야 한다.

</br>

``` java
import java.util.ArrayList;
```

</br>


### 추가

엘리먼트를 추가 할 때는 `add` 메소드를 사용한다. `add`는 배열에 단순히 더해지는 것이기 때문에 빠르게 동작한다.

</br>

``` java
numbers.add(10);
numbers.add(20);
numbers.add(30);
numbers.add(40);
```

```
[10, 20, 30, 40]
```

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2888.png)

</br>

특정 위치에 추가하고 싶다면 메소드 `add`의 첫번째 인자로 인덱스를 지정한다.

</br>

``` java
numbers.add(1, 50);
```

```
[10, 50, 20, 30, 40]
```

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2889.png)

</br>

자바의 배열은 크기가 고정되어 있다. 데이터를 추가하는 과정에서 내부적으로 사용하는 배열이 꽉차면 기존의 배열 대비 크기가 2배 큰 새로운 배열을 만들고 기존의 데이터를 새로운 배열로 복제한다. 덕분에 프로그래머는 `ArrayList`의 크기에 신경쓰지 않고 편리하게 프로그램을 만들 수 있다. 하지만 배열의 크기를 키우는 과정에서 많은 부하가 발생한다. 이런 기능은 `List` 데이터 스트럭쳐의 본질적인 기능이라고 할 수는 없다.

</br>

### 삭제

특정 인덱스에 위치하는 엘리먼트를 삭제할 때는 `remove`를 사용한다.

</br>

``` java
numbers.remove(2);
```

```
[10, 50, 30, 40]
```

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2890.png)

</br>

### 가져오기

엘리먼트를 가져올 때는 `get`을 사용한다. 이때 내부적으로 배열을 이용하기 때문에 매우 빠르게 엘리먼트를 가져올 수 있다.

</br>

``` java
numbers.get(2);
```

```
30
```

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2891.png)

</br>

### Size(크기)

`ArrayList`에 몇 개의 엘리먼트가 저장되었는지 사이즈를 가져오고 싶을 때는 메소드 `size`를 사용한다.

</br>

``` java
numbers.size();
```

```
4
```

</br>

### 반복

자바에서는 `ArrayList`를 탐색하기 위한 방법으로 `iterator`을 제공한다. 이것은 주로 객체지향 프로그래밍에서 사용하는 반복기법이다. 우선 `Iterator` 객체를 만들어야 한다.

</br>

``` java
Iterator it<Integer> = numbers.iterator();
```

</br>

`Iterator` 객체는 `numbers` 객체 내부에 저장된 값을 하나씩 순회하면서 탐색할 수 있도록 돕는 객체이다.

</br>

``` java
while(it.hasNext()){
    System.out.println(it.next());          
}
```

```
10
50
30
40
```

</br>

`it.next()` 메소드를 호출할 때마다 엘리먼트를 순서대로 리턴한다. 만약 더 이상 순회할 엘리먼트가 없다면 `it.hasNext()`의 값은 false가 되면서 while문이 종료된다.

순회 과정에서 필요에 따라서는 엘리먼트를 삭제/추가하는 작업을 해야 할 것이다. 그런 경우 아래와 같이 처리할 수 있다.

</br>

``` java
while(it.hasNext()){
    int value = it.next();
    if(value == 30){
        it.remove();
    }                       
}
```

</br>

`it.remove()`는 `it.next()`를 통해서 반환된 `numbers`의 엘리먼트를 삭제하는 명령이다.

조금 더 편리한 방법도 있다.

</br>

``` java
for(int value : numbers){
    System.out.println(value);
}
```

```
10
50
40
```

</br>

## 전체 코드

</br>

``` java
package list.arraylist.api;
 
import java.util.ArrayList;
import java.util.Iterator;
 
public class Main {
 
    public static void main(String[] args) {
 
        ArrayList<Integer> numbers = new ArrayList<>();
 
        numbers.add(10);
        numbers.add(20);
        numbers.add(30);
        numbers.add(40);
        System.out.println("add(값)");
        System.out.println(numbers);
 
        numbers.add(1, 50);
        System.out.println("\nadd(인덱스, 값)");
        System.out.println(numbers);
 
        numbers.remove(2);
        System.out.println("\nremove(인덱스)");
        System.out.println(numbers);
 
        System.out.println("\nget(인덱스)");
        System.out.println(numbers.get(2));
 
        System.out.println("\nsize()");
        System.out.println(numbers.size());
 
        System.out.println("\nindexOf()");
        System.out.println(numbers.indexOf(30));
 
        Iterator it = numbers.iterator();
        System.out.println("\niterator");
        while (it.hasNext()) {
            int value = (int) it.next();
            if (value == 30) {
                it.remove();
            }
            System.out.println(value);
        }
        System.out.println(numbers);
 
        System.out.println("\nfor each");
        for (int value : numbers) {
            System.out.println(value);
        }
        System.out.println("\nfor");
        for (int i = 0; i < numbers.size(); i++) {
            System.out.println(numbers.get(i));
        }
 
    }
 
}
```

```
add(값)
[10, 20, 30, 40]

add(인덱스, 값)
[10, 50, 20, 30, 40]

remove(인덱스)
[10, 50, 30, 40]

get(인덱스)
30

size()
4

indexOf()
2

iterator
10
50
30
40
[10, 50, 40]

for each
10
50
40

for
10
50
40
```

</br>