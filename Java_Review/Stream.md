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

</br>

## 2.2 스트림 만들기

스트림의 소스가 될 수 있는 대상은 배열, 컬렉션, 임의의 수 등 다양하다.

</br>

### 컬렉션

컬렉션의 최고 조상인 `Collection`에 `stream()`이 정의되어 있다. 그래서 `Collection`의 자손인 `List`와 `Set`을 구현한 컬렉션 클래스들은 모두 이 메소드로 스트림을 생성할 수 있다. `stream()`은 해당 컬렉션을 소스(source)로 하는 스트림을 반환한다.

``` java
Stream<T> Collection.stream()
```

예를 들어 List로부터 스트림을 생성하는 코드는 다음과 같다.

``` java
List<Integer> list = Arrays.asList(1, 2, 3, 4, 5);  // 가변인자
Stream<Integer> IntStream = list.stream();  // list를 소스로 하는 컬렉션 생성
```

`forEach()`는 지정된 작업을 스트림의 모든 요소에 대해 수행한다. 아래의 문장은 스트림의 모든 요소를 화면에 출력한다.

``` java
intStream.forEach(System.out::println); // 스트림의 모든 요소를 출력한다.
intStream.forEach(System.out::println); // 에러. 스트림이 이미 닫혔다.
```

한 가지 주의할 점은 `forEach()`가 스트림의 요소를 소모하면서 작업을 수행하므로 같은 스트림에 `forEach()`를 두 번 호출할 수 없다. 그래서 스트림의 요소를 한번 더 출력하려면 스트림을 새로 생성해야 한다. `forEach()`에 의해 스트림의 요소가 소모되는 것이지, 소스의 요소가 소모되는 것은 아니기 때문에 같은 소스로부터 다시 스트림을 생성할 수 있다.

</br>

### 배열

배열을 소스로 하는 스트림을 생성하는 메소드는 다음과 같이 `Stream`과 `Arrays`에 static메소드로 정의되어 있다.

``` java
Stream<T> Stream.of(T... value) // 가변 인자
Stream<T> Stream.of(T[])
Stream<T> Arrays.stream(T[])
Stream<T> Arrays.stream(T[] array, int startInclusive, int endExclusive)
```

예를 드렁 문자열 스트림은 다음과 같이 생성한다.

``` java
Stream<String> strStream = Stream.of("a", "b", "c");    // 가변 인자
Stream<String> strStream = Stream.of(new String[] {"a", "b", "c"});
Stream<String> strStream = Arrays.stream(new String[] {"a", "b", "c"});
Stream<String> strStream = Arrays.stream(new String[] {"a", "b", "c"}, 0, 3);
```

그리고 int, long, double과 같은 기본형 배열을 소스로 하는 스트림을 생성하는 메소드도 있다.

``` java
IntStream IntStream.of(int... values)    // Stream이 아니라 IntStream
IntStream IntStream.of(int[])
IntStream Arrays.stream(int[])
IntStream Arrays.stream(int[] array, int startInclusive, int endExclusive)
```

이 외에도 long과 double타입의 배열로부터 `LongStream`과 `DoubleStream`을 반환하는 메소드들이 있다.

</br>

### 특정 범위의 정수

`IntStream`과 `LongStream`은 다음과 같이 지정된 범위의 연속된 정수를 스트림으로 생성해서 반환하는 `range()`와 `rangeClosed()`를 가지고 있다.

``` java
IntStream IntStream.range(int begin, int end)
IntStream IntStream.rangeClosed(int begin, int end)
```

`range()`의 경우 경계의 끝인 `end`가 범위에 포함되지 않고, `rangeClosed()`의 경우는 포함된다.

``` java
IntStream intStream = IntStream.range(1, 5); // 1, 2, 3, 4
IntStream intStream = IntStream.rangeClosed(1, 5);  // 1, 2, 3, 4, 5
```

int보다 큰 범위의 스트림을 생성하려면 `LongStream`에 있는 동일한 읾의 메소드를 사용하면 된다.

</br>

### 임의의 수

난수를 생성하는데 사용하는 `Random`클래스에는 아래와 같은 인스턴스 메소드들이 포함되어 있다. 이 메소드들은 해당 타입의 난수들로 이루어진 스트림을 반환한다.

``` java
IntStream ints()
LongStream longs()
DoubleStream doubles()
```

이 메소드들이 반환하는 스트림은 크기가 정해지지 않은 '무한 스트림(infinite stream)'이므로 `limit()`도 같이 사용해서 스트림의 크기를 제한해 주어야 한다. `limit()`은 스트림의 개수를 지정하는데 사용되며, 무한 스트림을 유한 스트림으로 만들어 준다.

``` java
IntStream intStream = new Random().ints();  // 무한 스트림
intStream.limit(5).forEach(System.out::println);    // 5개의 요소만 출력한다.
```

아래의 메소드들은 매개변수로 스트림의 크기를 지정해서 '유한 스트림'을 생성해서 반환하므로 `limit()`을 사용하지 않아도 된다.

``` java
IntStream ints(long streamSize)
LongStream longs(long streamSize)
DoubleStream doubles(long streamSize)

IntStream intStream = new Random().ints(5); // 크기가 5인 난수 스트림을 반환
```

위 메소드들에 의해 생성된 스트림의 난수는 아래의 범위를 갖는다.

``` java
Integer.MIN_VALUE <= ints() <= Integer.MAX_VALUE
Long.MIN_VALUE <= longs() <= Long.MAX_VALUE
0.0 <= doubles() <= 1.0
```

지정된 범위(begin~end)의 난수를 발생시키는 스트림을 얻는 메소드는 아래와 같다. 단, `end`는 범위에 포함되지 않는다.

``` java
IntStream ints(int begin, int end)
LongStream longs(long begin, long end)
DoubleStrem doubles(double begin, double end)

IntStream ints(long streamSize, int begin, int end)
LongStream longs(long streamSize, long begin, long end)
DoubleStream doubles(long streamSize, double begin, double end)
```

</br>

### 람다식 - iterate(), generate()

`Stream`클래스의 `iterate()`와 `generate()`는 람다식을 매개변수로 받아서, 이 람다식에 의해 계산되는 값들을 요소로 하는 무한 스트림을 생성한다.

``` java
static <T> Stream<T> iterate(T seed, UnaryOperator<T> f)
static <T> STream<T> generate(Supplier<T> s)
```

`iterate()`는 씨앗값(seed)으로 지정된 값부터 시작해서, 람다식 `f`에 의해 계산된 결과를 다시 `seed`값으로 해서 계산을 반복한다. 아래의 `evenStream`은 0부터 시작해서 값이 2씩 계속 증가한다.

``` java
Stream<Integer> evenStream = Stream.iterate(0, n -> n + 2); // 0, 2, 4, 6, ...
```

`generate()`도 `iterate()`처럼, 람다식에 의해 계산되는 값을 요소로 하는 무한 스트림을 생성해서 반환하지만, `iterate()`와 달리, 이전 결과를 이용해서 다음 요소를 계산하지 않는다.

``` java
Stream<Double> randomStream = Stream.generate(Math::random);
Stream<Integer> oneStream = Stream.generate(() -> 1);
```

그리고 `generate()`에 정의된 매개변수의 타입은 `Supplier<T>`이므로 매개변수가 없는 람다식만 허용된다. 한 가지 주의할 점은 `iterate()`와 `generate()`에 의해 생성된 스트림을 아래와 같이 기본형 스트림 타입의 참조변수로 다룰 수 없다.

``` java
IntStream evenStream = Stream.iterate(0, n -> n + 2);       // 에러.
DoubleStream randomStream = Stream.generate(Math::random);  // 에러.
```

굳이 필요하다면, 아래와 같이 `mapToInt()`와 같은 메소드로 변환을 해야 한다.

``` java
IntStream evenStream = Stream.iterate(0, n -> n + 2).mapToInt(Integer::valueOf);
Stream<Integer> stream = evenStream.boxed();    // IntStream → Stream<Integer>
```

반대로 `IntStream`타입의 스트림을 `Stream<Integer>`타입으로 변환하려면, `boxed()`를 사용하면 된다.

</br>

### 파일

`java.nio.file.Files`는 파일을 다루는데 필요한 유용한 메소드들을 제공하는데, `list()`는 지정된 디렉토리(dir)에 있는 파일의 목록을 소스로 하는 스트림을 생성해서 반환한다.

> Path는 하나의 파일 또는 경로를 의미한다.

``` java
Stream<Path> Files.list(Path dir)
```

그리고 파일의 한 행(line)을 요소로 하는 스트림을 생성하는 메소드도 있다. 아래의 세 번째 메소드는 `BufferedReader`클래스에 속한 것인데, 파일 뿐만 아니라 다른 입력대상으로부터도 데이터를 행단위로 읽어올 수 있다.

``` java
Stream<String> Files.lines(Path path)
Stream<String> Files.lines(Path path, Charset cs)
Stream<String> lines()  // BufferedReader클래스의 메소드
```

</br>

### 빈 스트림

요소가 하나도 없는 비어있는 스트림을 생성할 수도 있다. 스트림에 연산을 수행한 결과가 하나도 없을 때, null보다 빈 스트림을 반환하는 것이 낫다.

``` java
Stream emptyStream = Stream.empty();    // empty()는 빈 스트림을 생성해서 반환한다.
long count = emptyStream.count();   // count의 값은 0
```

`count()`는 스트림 요소의 개수를 반환하며, 위의 문장에서 변수 `count`의 값은 0이 된다.

</br>

### 두 스트림의 연결

`Stream`의 static메소드인 `concat()`을 사용하면, 두 스트림을 하나로 연결할 수 있다. 물론 연결하려는 두 스트림의 요소는 같은 타입이어야 한다.

``` java
String[] str1 = {"123", "456", "789"};
String[] str2 = {"ABC", "abc", "DEF"};

Stream<String> strs1 = Stream.of(str1);
Stream<String> strs2 = Stream.of(str2);
Stream<String> strs3 = Stream.concat(strs1, strs2); // 두 스트림을 하나로 연결
```