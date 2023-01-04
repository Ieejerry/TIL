Chapter 14. 람다와 스트림

# 2. 스트림(Stream)

</br>

## 2.1 스트림이란?

스트림은 데이터 소스를 추상화하고, 데이터를 다루는데 자주 사용되는 메소드들을 정의해 놓았다. 데이터 소스를 추상화하였다는 것은, 데이터 소스가 무엇이던 간에 같은 방식으로 다룰 수 있게 되었다는 것과 코드의 재사용성을 높아진다는 것을 의미한다.

스트림을 이용하면, 배열이나 컬렉션뿐만 아니라 파일에 저장된 데이터도 모두 같은 방식으로 다룰 수 있다.

예를 들어, 문자열 배열과 같은 내용의 문자열을 저장하는 List가 있을 때,

``` java
String[] strArr = { "aaa", "ddd", "ccc" };
List<String> strList = Arrays.asList(strArr);
```

이 두 데이터 소스를 기반으로 하는 스트림은 다음과 같이 생성한다.

``` java
Stream<String> strStream1 = strList.stream();   // 스트림을 생성
Stream<String> strStream2 = Arrays.stream(strArr);  // 스트림을 생성
```

이 두 스트림으로 데이터 소스의 데이터를 읽어서 정렬하고 화면에 출력하는 방법은 다음과 같다. 데이터 소스가 정렬되는 것은 아니다.

``` java
strStream1.sorted().forEach(System.out::println);
strStream2.sorted().forEach(System.out::println);
```

두 스트림의 데이터 소스는 서로 다르지만, 정렬하고 출력하는 방법은 완전히 동일하다. 예전에는 아래와 같이 코드를 작성해야 했다.

``` java
Arrays.sort(strArr);
Collections.sort(strList);

for(String str : strArr)
    System.out.println(str);

for(String str : strList)
    System.out.println(str);
```

스트림을 사용한 코드가 간결하고 이해하기 쉬우며 재사용성도 높다.

</br>

### 스트림은 데이터 소스를 변경하지 않는다.

그리고 스트림은 데이터 소스로 부터 데이터를 읽기만할 뿐, 데이터 소스를 변경하지 않는다는 차이가 있다. 필요하다면, 정렬된 결과를 컬렉션이나 배열에 담아서 반환할 수도 있다.

``` java
// 정렬된 결과를 새로운 List에 담아서 반환한다.
List<string> sortedList = strStream2.sorted().collect(Collectors.toList());
```

</br>

### 스트림은 일회용이다.

스트림은 `Iterator`처럼 일회용이다. `Iterator`로 컬렉션의 요소를 모두 읽고 나면 다시 사용할 수 없는 것처럼, 스트림도 한번 사용하면 닫혀서 다시 사용할 수 없다. 필요하다면 스트림을 다시 생성해야한다.

``` java
strStream1.sorted().forEach(System.out.println);
int numOfStr = strStream1.count();  // 에러. 스트림이 이미 닫혔음.
```

</br>

### 스트림은 작업을 내부 반복으로 처리한다.

스트림을 이요한 자겁이 간결할 수 있는 비결중의 하나가 바로 '내부 반복'이다. 내부 반복이라는 것은 반복문을 메소드의 내부에 숨길 수 있다는 것을 의미한다. `forEach()`는 스트림에 정의된 메소드 중의 하나로 매개변수에 대입된 람다식을 데이터 소스의 모든 요소에 적용한다.

![image](https://ifh.cc/g/Wf1vPX.png)

> 메소드 참조 System.out::println를 람다식으로 표현하면 (str) -> System.out.println(str)과 같다.

즉, `forEach()`는 메소드 안으로 for문을 넣은 것이다. 수행할 작업은 매개변수로 받는다.

``` java
void forEach(Consumer<? super T> action) {
    Objects.requireNonNull(action); // 매개변수의 널 체크

    for(T t : src) {    // 내부 반복
        action.accept(T);
    }
}
```

</br>

### 스트림의 연산

스트림이 제공하는 다양한 연산을 이용해서 복잡한 작업들을 간단히 처리할 수 있다. 마치 데이터베이스에 SELECT문으로 질의(쿼리, query)하는 것과 같은 느낌이다.

> 스트림에 정의된 메소드 중에서 데이터 소스를 다루는 작업을 수행하는 것을 연산(operation)이라고 한다.

스트림이 제공하는 연산은 중간 연산과 최종 연산으로 분류할 수 있는데, 중간 연산은 연산결과를  스트림으로 반환하기 때문에 중간 연산을 연속해서 연결할 수 있다. 반면에 최종 연산은 스트림이 요소를 소모하면서 연산을 수행하므로 단 한번만 연산이 가능하다.

> **중간 연산** 연산 결과가 스트림인 연산. 스트림에 연속해서 중간 연산할 수 있음   
**최종 연산** 연산 결과가 스트림 아닌 연산, 스트림의 요소를 소모하므로 단 한번만 가능

![image](https://ifh.cc/g/OWrzRn.png)

모든 중간 연산의 결과는 스트림이지만, 연산 전의 스트림과 같은 것은 아니다. 위의 문장과 달리 모든 스트림 연산을 나누어 쓰면 아래와 같다.

``` java
String[] strArr = { "dd", "aaa", "CC", "cc", "b" };
Stream<String> stream = Stream.of(strArr);  // 문자열 배열이 소스인 스트림
Stream<String> filteredStream = stream.filter();    // 걸러내기(중간 연산)
Stream<String> distinctedStream = stream.distinct();    // 중복제거(중간 연산)
Stream<String> sortedStream = stream.sort();    // 정렬(중간 연산)
Stream<String> limitedStream = stream.limit(5); // 스트림 자르기(중간 연산)
int total = stream.count(); // 요소 개수 세기(최종 연산)
```

`Stream`에ㅓ 정의된 연산을 정리하면 다음과 같다.

![image](https://ifh.cc/g/HQLjb5.png)

![image](https://ifh.cc/g/W5WV7W.png)

중간 연산은 `map()`과 `flatMap()`, 최종 연산은 `reduce()`와 `collect()`가 핵심이다.

> 표 목록은 Stream클래스에 정의된 연산들만 나열한 것이다.
> Optional은 일종의 래퍼 클래스(wrapper class)로 내부에 하나의 객체를 저장할 수 있다.

</br>

### 지연된 연산

스트림 연산에서 한 가지 중요한 점은 최종 연산이 수행되지 전까지는 중간 연산이 수행되지 않는다는 것이다. 스트림에 대해 `distinct()`나 `sort()`같은 중간 연산을 호출해도 즉각적인 연산이 수행되는 것은 아니라는 것이다. 중간 연산을 호출하는 것은 단지 어떤 작업이 수행되어야하는지를 지정해주는 것일 뿐이다. 최종 연산이 수행되어야 비로소 스트림의 요소들이 중간 연산을 거쳐 최종 연산에서 소모된다.

</br>

### Stream<Integer>와 IntStream

요소의 타입이 `T`인 스트림은 기본적으로 `Stream<T>`이지만, 오토박싱&언박싱으로 인한 비효율을 줄이기 위해 데이터 소스의 요소를 기본형으로 다루는 스트림, `IntStream`, `LongStream`, `DoubleStream`이 제공된다. 일반적으로 `Stream<Integer>`대신 `IntStream`을 사용하는 것이 더 효율적이고, `IntStream`에는 int타입의 값으로 작업하는데 유용한 메소드들이 포함되어 있다.

</br>

### 병렬 스트림

스트림으로 데이터를 다룰 때의 장점 중 하나가 바로 병렬 처리가 쉽다는 것이다. 병렬 스트림은 내부적으로 fork&join프레임워크를 이용해서 자동적으로 연산을 병렬로 수행한다. 스트림에 `parallel()`이라는 메소드를 호출해서 병렬로 연산을 수행하도록 하면 된다. 반대로 병렬로 처리되지 않게 하려면 `sequential()`을 호출하면 된다. 모든 스트림은 기본적으로 벙렬 스트림이 아니므로 `sequential()`을 호출할 필요가 없다. 이 메소드는 `parallel()`을 호출한 것을 취소할 때만 사용한다.

> parallel()과 sequential()은 새로운 스트림을 생성하는 것이 아니라, 그저 스트림의 속성을 변경할 뿐이다.

``` java
int sum = strStream.parallel()  // strStream을 병렬 스트림으로 전환
                   .mapToInt(s -> s.length())
                   .sum();
```

병렬처리가 항상 더 빠른 결과를 얻게 해주는 것은 아니다.