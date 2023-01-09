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

</br>

## 2.3 스트림의 중간연산

</br>

### 스트림 자르기 - skip(), limit()

`skip()`과 `limit()`은 스트림의 일부를 잘라낼 때 사용하며, `skip(3)`은 처음 3개의 요소를 건너뛰고, `limit(5)`는 스트림의 요소를 5개로 제한한다.

``` java
Stream<T> skip(long n)
Stream<T> limit(long maxSize)
```

예를 들어 10개의 요소를 가진 스트림에 `skip(3)`과 `limit(5)`을 순서대로 적용하면 4번째 요소부터 5개의 요소를 가진 스트림이 반환된다.

``` java
IntStream intStream - IntStream.rangeClosed(1, 10); // 1~10의 요소를 가진 스트림
intStream.skip(3).limit(5).forEach(System.out::println);    // 45678
```

기본형 스트림에도 `skip()`과 `limit()`이 정의되어 있는데, 반환 타입이 기본형 스트림이라는 점만 다르다.

``` java
IntStream skip(long n)
IntStream limit(long maxSize)
```

</br>

### 스트림의 요소 걸러내기 - filter(), distinct()

`distinct()`는 스트림에서 중복된 요소들을 제거하고, `filter()`는 주어진 조건(Predicate)에 맞지 않는 요소를 걸러낸다.

``` java
Stream<T> filter(Predicate<? super T> predicate)
Stream<T> distinct()
```

`distinct()`의 사용 방법은 간단하다.

``` java
IntStream intStream = IntStream.of(1, 2, 2, 3, 3, 3, 4, 5, 5, 6);
intStream.distinct().forEach(System.out::println);  //12345
```

`filter()`는 매개변수로 `Predicate`를 필요로 하는데, 아래와 같이 연산결과가 boolean이니 람다식을 사용해도 된다.

``` java
IntStream intStream = IntStream.rangeClosed(1, 10); // 1~10
intStream.filter(i -> i % 2 == 0).forEach(System.out::print);   // 246810
```

필요하다면 `filter()`를 다른 조건으로 여러 번 사용할 수도 있다.

``` java
// 아래의 두 문장은 동일한 결과를 얻는다.
intStream.filter(i -> i % 2 != 0 && i % 3 != 0).forEach(System.out::print); // 157
intStream.filter(i -> i % 2 != 0).filter(i -> i % 3 == 0).forEach(System.out::print);
```

</br>

### 정렬 - sorted()

스트림에 정렬할 때는 `sorted()`를 사용하면 된다.

``` java
Stream<T> sorted()
Stream<T> sorted(Comparator<? super T> comparator)
```

`sorted()`는 지정된 `Comparator`로 스트림을 정렬하는데, `Comparator` 대신 int값을 반환하는 람다식을 사용하는 것도 가능하다. `Comparator`를 지정하지 않으면 스트림 요소의 기본 정렬 기준(Comparable)으로 정렬한다. 단, 스트림의 요소가 `Comparable`을 구현한 클래스가 아니면 예외가 발생한다.

``` java
Stream<String> strStream = Stream.of("dd", "aaa", "CC", "cc", "b");
strStream.sorted().forEach(System.out::print);  // CCaaabccdd
```

위의 코드는 문자열 스트림에 String에 정의된 기본 정렬(사전순 정렬)로 정렬해서 출력한다. 아래의 표는 위의 문자열 스트림(strStream)을 다양한 방법으로 정렬한 후에 `forEach(System.out::print)`로 출력한 결과를 보여준다.

> String.CASE_INSENSITIVE_ORDER는 String클래스에 정의된 Comparator이다.

![image](https://ifh.cc/g/ph59Ln.png)

JDK1.8부터 `Comparator`인터페이스에 static메소드와 디폴트 메소드가 많이 추가되었는데, 이 메소드들을 이용하면 정렬이 쉬워진다. 이 메소드들은 모두 `Comparator<T>`를 반환하며, 아래의 메소드 목록은 제네릭에서 와일드 카드를 제거하여 간단히 한 것이다.

Comparator의 default메소드

``` java
reversed()
thenComparing(Comparator<T> other)
thenComparing(Function<T, U> keyExtractor)
thenComparing(Function<T, U> keyExtractor, Comparator<U> keyComp)
thenComparingInt(ToIntFunction<T> keyExtractor)
thenComparingLong(ToLongFunction<T> keyExtractor)
thenComparingDouble(ToDoubleFunction<T> keyExtractor)
```

Comparator의 static메소드

``` java
naturalOrder()
reverseOrder()
comparing(Function<T, U> keyExtractor)
comparing(Function<T, U> keyExtractor, Comparator<U> keyComparator)
comparingInt(ToIntFunction<T> keyExtractor)
comparingLong(ToLongFunction<T> keyExtractor)
comparingDouble(ToDoubleFunction<T> keyExtractor)
nullsFirst(Comparator<T> comparator)
nullsLast(Comparator<T> comparator)
```

정렬에 사용되는 메소드의 개수가 많지만, 가장 기본적인 메소드는 `comparing()`이다.

``` java
comparing(Function<T, U> keyExtractor)
comparing(Function<T, U> keyExtractor, Comparator<U> keyComparator)
```

스트림의 요소가 `Comparable`을 구현한 경우, 매개변수 하나짜리를 사용하면 되고, 그렇지 않은 경우, 추가적인 매개변수로 정렬기준(Comparator)을 따로 지정해 줘야한다.

``` java
comparingInt(ToIntFunction<T> keyExtractor)
comparingLong(ToLongFunction<T> keyExtractor)
comparingDouble(ToDoubleFunction<T> keyExtractor)
```

비교대상이 기본형인 경우, `comparing()`대신 위의 메소드를 사용하면 오토박싱과 언박싱과정이 없어서 더 효율적이다. 그리고 정렬 조건을 추가할 때는 `thenComparing()`을 사용한다.

``` java
thenComparing(Comparator<T> other)
thenComparing(Function<T, U> keyExtractor)
thenComparing(Function<T, U> keyExtractor, Comparator<U> keyComp)
```

예를 들어 학생 스트림(studentStream)을 반(ban)별, 성적(totalScore)순, 그리고 이름(name)순으로 정렬하여 출력하려면 다음과 같이 한다.

``` java
studentStream.sorted(Comparator.comparing(Student::getBan)
                            .thenComparing(Student::getTotalScore)
                            .thenComparing(Student::getName))
                            .forEach(System.out::println);
```

다음 예제는 학생의 성적을 반별 오름차순, 총점별 내림차순으로 정렬하여 출력한다.

</br>

예제 14-8 / ch14 / StreamEx1.java

``` java
import java.util.*;
import java.util.stream.*;

public class StreamEx1 {
	public static void main(String[] args) {
		Stream<Student> studentStream = Stream.of(
					new Student("이자바", 3, 300),
					new Student("김자바", 1, 200),
					new Student("안자바", 2, 100),
					new Student("박자바", 2, 150),
					new Student("소자바", 1, 200),
					new Student("나자바", 3, 290),
					new Student("감자바", 3, 180)
				);
		
		studentStream.sorted(Comparator.comparing(Student::getBan)	// 반별 정렬
				.thenComparing(Comparator.naturalOrder()))	// 기본 정렬
				.forEach(System.out::println);
	}
}

class Student implements Comparable<Student> {
	String name;
	int ban;
	int totalScore;
	Student(String name, int ban, int totalScore) {
		this.name = name;
		this.ban = ban;
		this.totalScore = totalScore;
	}
	
	public String toString() {
		return String.format("[%s, %d, %d]", name, ban, totalScore);
	}
	
	String getName() { return name; }
	int getBan() { return ban; }
	int getTotalScore() { return totalScore; }
	
	// 총점 내림차순을 기본 정렬로 한다.
	public int compareTo(Student s) {
		return s.totalScore - this.totalScore;
	}
}
```

```
[김자바, 1, 200]
[소자바, 1, 200]
[박자바, 2, 150]
[안자바, 2, 100]
[이자바, 3, 300]
[나자바, 3, 290]
[감자바, 3, 180]
```

학생 성적 정보를 요소로 하는 `Stream<Student>`을 반별로 정렬한 다음에, 총점별 내림차순으로 정렬한다. 정렬하는 코드를 짧게 하려고, `Comparable`을 구현해서 총점별 내림차순 정렬이 `Student`클래스의 기본 정렬이 되도록 했다.

``` java
studentStream.sorted(Comparator.comparing(Student::getBan)  // 반별 정렬
                .thenComparing(Comparator.naturalOrder()))  // 기본 정렬
                .forEach(System.out::println);
```

</br>

### 변환 - map()

스트림의 요소에 저장된 값 중에서 원하는 필드만 뽑아내거나 특정 형태로 변환해야 할 때 사용하는 것이 바로 `map()`이다. 이 메소드의 선언부는 아래와 같으며, 매개변수로 T타입을 R타입으로 변환해서 반호나하는 함수를 지정해야한다.

``` java
Stream<R> map(Function<? super T, ? extends R> mapper)
```

예를 들어 `File`의 스트림에서 파일의 이름만 뽑아서 출력하고 싶을 때, 아래와 같이 `map()`을 이용하면 `File`객체에서 파일의 이름(String)만 간단히 뽑아낼 수 있다.

``` java
Stream<File> fileStream = Stream.of(new File("Ex1.java"), new File("Ex1"),
        new File("Ex1.bak"), new File("Ex2.java"), new File("Ex1.txt"));

// map()으로 Stream<File>을 Stream<String>으로 변환
Stream<String> filenameStream = fileStream.map(File::getName);
filenameStream.forEach(System.out::println);    // 스트림의 모든 파일이름을 출력
```

`map()` 역시 중간 연산이므로, 연산결과는 String을 요소로 하는 스트림이다. `map()`으로 `Stream<File>`을 `Stream<String>`으로 변환했다고 볼 수 있다.

그리고, `map()`도 `filter()`처럼 하나의 스트림에 여러 번 적용할 수 있다. 다음의 문장은 `File`의 스트림에서 파일의 확장자만을 뽑은 다음 중복을 제거해서 출력한다.

``` java
fileStream.map(File::getName)   // Stream<File> → Stream<String>
    .filter(s -> s.indexOf(',') != -1)  // 확장자가 없는 것은 제외
    .map(s -> s.substring(s.indexOf(',') + 1))  // Stream<String> → Stream<String>
    .map(String::toUpperCase)   // 모두 대문자로 변환
    .distinct() // 중복 제거
    .forEach(System.out::print);    // JAVABAKTXT
```

</br>

### 조회 - peek()

연산과 연산 사이에 올바르게 처리되었는지 확인하고 싶다면, `peek()`를 사용하자. `forEach()`와 달리 스트림의 요소를 소모하지 않으므로 연산 사이에 여러 번 끼워 넣어도 문제가 되지 않는다.

``` java
fileStream.map(File::getName)   // Stream<File> → Stream<String>
    .filter(s -> s.indexOf(',') != -1)  // 확장자가 없는 것은 제외
    .peek(s -> System.out.printf("filename = %s%n", s)) // 파일명을 출력한다.
    .map(s -> s.substring(s.indexOf(',') + 1))  // 확장자만 추출
    .peek(s -> System.out.printf("extension = %s%n", s))    // 확장자를 출력한다.
    .forEach(System.out::println);
```

`filter()`나 `map()`의 결과를 확인할 때 유용하게 사용될 수 있다.

</br>

예제 14-9 / ch14 / StreamEx2.java

``` java
import java.io.*;
import java.util.stream.Stream;

public class StreamEx2 {
	public static void main(String[] args) {
		File[] fileArr = { new File("Ex1.java"), new File("Ex1.bak"),
				new File("Ex2.java"), new File("Ex1"), new File("Ex1.txt")
		};
		
		Stream<File> fileStream = Stream.of(fileArr);
		
		// map()으로 Stream<File>을 Stream<String>으로 변환
		Stream<String> filenameStream = fileStream.map(File::getName);
		filenameStream.forEach(System.out::println);	// 모든 파일의 이름을 출력
		
		fileStream = Stream.of(fileArr);	// 스트림을 다시 생성
		
		fileStream.map(File::getName)	// Stream<File> → Stream<String>
			.filter(s -> s.indexOf('.') != -1) // 확장자가 없는 것은 제외
			.peek(s -> System.out.printf("filename = %s%n", s))
			.map(s -> s.substring(s.indexOf('.') + 1))	// 확장자만 추출
			.peek(s -> System.out.printf("extension = %s%n", s))
			.map(String::toUpperCase)	// 모두 대문자로 변환
			.distinct()	// 중복 제거
			.forEach(System.out::print);	// JAVABAKTXT
		
		System.out.println();
	}
}
```

```
Ex1.java
Ex1.bak
Ex2.java
Ex1
Ex1.txt
filename = Ex1.java
extension = java
JAVA
filename = Ex1.bak
extension = bak
BAK
filename = Ex2.java
extension = java
filename = Ex1.txt
extension = txt
TXT
```

</br>

### mapToInt(), mapToLong(), mapToDouble()

`map()`은 연산의 결과로 `Stream<T>`타입의 스트림을 반환하는데, 스트림의 요소를 숫자로 변환하는 경우 `IntStream`과 같은 기본형 스트림으로 변환하는 것이 더 유용할 수 있다. `Stream<T>`타입의 스트림을 기본형 스트림으로 변환할 때 사용하는 것이 아래의 메소드들이다.

``` java
DoubleStream mapToDouble(ToDoubleFunction<? super T> mapper)
IntStream mapToInt(ToIntFunction<? super T> mapper)
LongStream mapToLong(ToLongFunction<? super T> mapper)
```

앞서 사용했던 `studentStream`에서, 스트림에 포함된 모든 학생의 성적을 합산해야 한다면, `map()`으로 학생의 총점을 뽑아서 새로운 스트림을 만들어 낼 수 있다.

``` java
Stream<Integer> studentScoreStream = studentStream.map(Student::getTotalScore);
```

그러나 이럴 때는 애초부터 `mapToInt()`를 사용해서 `Stream<Integer>`가 아닌 `IntStream`타입의 스트림을 생성해서 사용하는 것이 더 효율적이다. 성적을 더할 때, Integer를 int로 변환할 필요가 없기 때문이다.

``` java
IntStream studentScoreStream = studentStream.mapToInt(Student::getTotalScore);
int allTotalScore = studentScoreStream.sum();   // int sum();
```

`count()`만 지원하는 `Stream<T>`와 달리 `IntStream`과 같은 기본형 스트림은 아래와 같이 숫자를 다루는데 편리한 메소드들을 제공한다.

> max()와 min()은 Stream에도 정의되어 있지만, 매개변수로 Comparator를 지정해야 한다는 차이가 있다.

![image](https://ifh.cc/g/d3kOgy.png)

스트림의 요소가 하나도 없을 때, `sum()`은 0을 반환하면 그만이지만 다른 메소드들은 단순히 0을 반환할 수 없다. 여러 요소들을 합한 평균이 0일수 도 있기 때문이다. 이를 구분하기 위해 단순히 double값을 반환하는 대신, double타입의 값을 내부적으로 가지고 있는 `OptionalDouble`을 반환하는 것이다. `OptionalDouble` 등은 일종의 래퍼클래스로 각각 int값과 Double값을 내부적으로 가지고 있다.

그리고 이 메소드들은 최종연산이기 때문에 호출 후에 스트림이 닫힌다. 아래의 코드에서처럼 하나의 스트림에 `sum()`과 `average()`를 연속해서 호출할 수 없다.

``` java
IntStream scoreStream = studentStream.mapToInt(Student::getTotalScore);

long totalScore = scoreStream.sum();    // sum()은 최종연산이라 호출 후 스트림이 닫힘
OptionalDouble average = scoreStream.average(); // 에러. 스트림이 이미 닫혔음.

double d = average.getAsDouble();   // OptionalDouble에 저장된 값을 꺼내서 d에 저장
```

`sum()`과 `average()`를 모두 호출해야할 때, 스트림을 또 생성해야하므로 불편하다. 그래서 `summaryStatistics()`라는 메소드가 따로 제공된다.

``` java
IntSummaryStatistics stat = scoreStream.summaryStatistics();

long totalCount = stat.getCount();
long totalScore = stat.getSum();
double avgScore = stat.getAverage();
int minScore = stat.getMin();
int maxScore = stat.getMax();
```

`IntSummaryStatistics`는 위와 같이 다양한 종류의 메소드를 제공하며, 이 중에서 필요한 것만 골라서 사용하면 된다.

기본형 스트림 `LongStream`과 `DoubleStream`도 `IntStream`과 같은 연산(반환타입은 다름)을 지원한다. 반대로 `IntStream`을 `Stream<T>`로 변환할 때는 `mapToObj()`를, `Stream<Integer>`로 반환할 때는 `boxed()`를 사용한다.

``` java
Stream<T> mapToObj(IntFunction<? extends U> mapper)
Stream<Integer> boxed()
```

아래는 로또번호를 생성해서 출력하는 코드인데, `mapToObj()`를 이용해서 `IntStream`을 `Stream<String>`으로 변환하였다.

``` java
IntStream intStream = new Random().ints(1, 46); // 1~45사이의 정수(46은 포함안됨)
Stream<String> lottoStream = intStream.distinct().limit(6).sorted()
                                .mapToObj(i -> i + ",");    // 정수를 문자열로 반환
lottoStream.forEach(System.out::print); // 12, 14, 20, 23, 26, 29
```

참고로 `CharSequence`에 정의된 `chars()`는 String이나 StringBuffer에 저장된 문자들을 `IntStream`으로 다룰 수 있게 해준다.

``` java
IntStream charStream = "12345".chars(); // default IntStream chars()
int charSum = charStream.map(ch -> ch - '0').sum(); // charSum = 15
```

위의 코드에서 사용된 `map()`은 `IntStream`에 정의된 것으로 `IntStream`을 결과로 반환한다. 그리고 `mapToInt()`와 함께 자주 사용되는 메소드로는 Integer의 `parseInt()`나 `valueOf()`가 있다.

``` java
Stream<String> → IntStream 변환할 때, mapToInt(Integer::parseInt)
Stream<Integer> → IntStream 변활할 때, mapToInt(Integer::intValue)
```

</br>

예제 14-10 / ch14 / StreamEx3.java

``` java
import java.util.*;
import java.util.stream.*;

public class StreamEx3 {
	public static void main(String[] args) {
		Student[] stuArr = {
			new Student("이자바", 3, 300),
			new Student("김자바", 1, 200),
			new Student("안자바", 2, 100),
			new Student("박자바", 2, 150),
			new Student("소자바", 1, 200),
			new Student("나자바", 3, 290),
			new Student("감자바", 3, 180)
		};
		
		Stream<Student> stuStream = Stream.of(stuArr);
		
		stuStream.sorted(Comparator.comparing(Student::getBan)
						.thenComparing(Comparator.naturalOrder()))
						.forEach(System.out::println);
		
		stuStream = Stream.of(stuArr);	// 스트림을 다시 생성한다.
		IntStream stuScoreStream = stuStream.mapToInt(Student::getTotalScore);
		
		IntSummaryStatistics stat = stuScoreStream.summaryStatistics();
		System.out.println("count = " + stat.getCount());
		System.out.println("sum = " + stat.getSum());
		System.out.printf("average = %.2f%n", stat.getAverage());
		System.out.println("min = " + stat.getMin());
		System.out.println("max = " + stat.getMax());
	}
}

class Student implements Comparable<Student> {
	String name;
	int ban;
	int totalScore;
	Student(String name, int ban, int totalScore) {
		this.name = name;
		this.ban = ban;
		this.totalScore = totalScore;
	}
	
	public String toString() {
		return String.format("[%s, %d, %d]", name, ban, totalScore);
	}
	
	String getName() { return name; }
	int getBan() { return ban; }
	int getTotalScore() { return totalScore; }
	
	// 총점 내림차순을 기본 정렬로 한다.
	public int compareTo(Student s) {
		return s.totalScore - this.totalScore;
	}
}
```

```
[김자바, 1, 200]
[소자바, 1, 200]
[박자바, 2, 150]
[안자바, 2, 100]
[이자바, 3, 300]
[나자바, 3, 290]
[감자바, 3, 180]
count = 7
sum = 1420
average = 202.86
min = 100
max = 300
```

</br>

### flatMap() - Stream<T[]>를 Stream<T>로 변환

스트림의 요소가 배열이거나 `map()`의 연산결과가 배열인 경우, 즉 스트림의 타입이 `Stream<T[]>`인 경우 `map()`대신 `flatMap()`을 사용하면 된다.

예를 들어 아래와 같이 요소가 문자열 배열(String[])인 스트림이 있을 때,

``` java
Stream<String[]> stuArrStrm = Stream.of(
        new String[] {"abc", "def", "ghi"},
        new String[] {"ABC", "GHI", "JKLMN"}
);
```

각 요소의 문자열들을 합쳐서 문자열이 요소인 스트림, 즉 `Stream<String>`으로 만들려면 먼저 스트림의 요소를 변환해야하니까 일단 `map()`을 써야할 것이고 여기에 배열을 스트림으로 만들어주는 `Arrays.stream<T[]>`를 함께 사용해야 한다.

``` java
Stream<Stream<String>> strStrStrm = strArrStrm.map(Arrays::stream);
```

예상한 것과 달리, `Stream<String[]>`을 `map(Arrays::stream)`으로 변환한 결과는 `Stream<Stirng>`이 아닌, `Stream<Stream<String>>`이다. 즉, 스트림의 스트림인 것이다.

각 요소의 문자열들이 합쳐지지 않고, 스트림의 스트림 형태로 되었다. 이 때, 간단히 `map()`을 아래와 같이 `flatMap()`으로 바꾸기만 하면 된다.

``` java
Stream<Stream<String>> strStrStrm = strArrStrm.map(Arrays::stream);

    Stream<String> strStrm = strArrStrm.flatMap(Arrays::stream);
```

`flatMap()`은 `map()`과 달리 스트림의 스트림이 아닌 스트림으로 만들어 준다.

아래와 같이 여러 문장을 요소로 하는 스트림이 있을 때, 이 문장들을 `split()`으로 나눠서 요소가 단어인 스트림을 만들고 싶다면

``` java
String[] lineArr = {
    "Belive or not It is ture",
    "Do or do not There is no try",
};

Stream<String> lineStream = Arrays.stream(lineArr);
Stream<Stream<String>> strArrStream = lineStream.map(line -> Stream.of(line.split(" +")));
```

`map()`은 `Stream<String>`이 아니라 `Stream<Stream<String>>`을 결과로 돌려준다. 이럴 때도 `map()`대신 `flatMap()`으로 원하는 결과를 얻을 수 있다.

``` java
Stream<String> strStream = lineStream.flatMap(line -> Stream.of(line.split(" +")));
```

`strStream`의 단어들을 모두 소문자로 변환하고, 중복된 단어들을 제거한 다음에 정렬해서 출력하는 문장은 다음과 같다.

``` java
strStream.map(String::toLowerCase)  // 모든 단어를 소문자로 변경
         .distinct()    // 중복된 단어를 제거
         .sorted()  // 사전 순으로 정렬
         .forEach(System.out::println); // 화면에 출력
```

스트림을 요소로 하는 스트림, 즉 스트림의 스트림을 하나의 스트림으로 합칠 때도 `flatMap()`을 사용한다.

``` java
Stream<String> strStrm = Stream.of("abc", "def", "jklmn");
Stream<String> strStrm2 = Stream.of("ABC", "GHI", "JKLMN");

Stream<Stream<String>> strmStrm = Stream.of(strStrm, strStrm2)
```

위와 같이 요소의 타입이 `Stream<String>`인 스트림(`Stream<Stream<String>>`)이 있을 때, 이 스트림을 `Stream<String>`으로 변환하려면 다음과 같이 `map()`과 `flatMap()`을 함께 사용해야 한다.

``` java
Stream<String> strStream = strmStrm
    .map(s -> s.toArray(String[]::new)) // Stream<Stream<String>> → Stream<String[]>
    .flatMap(Arrays::stream);   // Stream<String[]> → Stream<String>
```

`toArray()`는 스트림을 배열로 변환해서 반환한다. 매개변수를 지정하지 않으면 `Object[]`을 반환하므로 위와 같이 특정 타입의 생성자를 지정해줘야 한다. 여기서는 String배열의 생성자(`String[]::new`)를 지정하였다. 그 다음엔 `flatMap()`으로 `Stream<String[]>`을 `Stream<String>`으로 변환한다.

</br>

예제 14-11 / ch14 / StreamEx4.java

``` java
import java.util.*;
import java.util.stream.Stream;

public class StreamEx4 {
	public static void main(String[] args) {
		Stream<String[]> strArrStrm = Stream.of(
			new String[] { "abc", "def", "jkl" },
			new String[] { "ABC", "GHI", "JKL" }
		);
		
//		Stream<Stream<String>> strStrmStrm = strArrStrm.map(Arrays::stream);
		Stream<String> strStrm = strArrStrm.flatMap(Arrays::stream);
		
		strStrm.map(String::toLowerCase)
			   .distinct()
			   .sorted()
			   .forEach(System.out::println);
		System.out.println();
		
		String[] lineArr = {
			"Believe or not It is true",
			"Do or do not There is no try",
		};
		
		Stream<String> lineStream = Arrays.stream(lineArr);
		lineStream.flatMap(line -> Stream.of(line.split(" +")))	// " +" 하나 이상의 공백(정규식)
			.map(String::toLowerCase)
			.distinct()
			.sorted()
			.forEach(System.out::println);
		System.out.println();
		
		Stream<String> strStrm1 = Stream.of("AAA", "ABC", "bBb", "Dd");
		Stream<String> strStrm2 = Stream.of("bbb", "aaa", "ccc", "dd");
		
		Stream<Stream<String>> strStrmStrm = Stream.of(strStrm1, strStrm2);
		Stream<String> strStream = strStrmStrm
									.map(s -> s.toArray(String[]::new))
									.flatMap(Arrays::stream);
		strStream.map(String::toLowerCase)
				 .distinct()
				 .forEach(System.out::println);
	}
}
```

```
abc
def
ghi
jkl

believe
do
is
it
no
not
or
there
true
try

aaa
abc
bbb
dd
ccc
```

</br>

## 2.4 Optional<T>와 OptionalInt

`Optional<T>`은 제네릭 클래스로 "T타입의 객체"를 감싸는 래퍼 클래스이다. 그래서 `Optional`타입의 객체에는 모든 타입의 참조변수를 담을 수 있다.

> java.util.Optional은 JDK1.8부터 추가되었다.

``` java
public final class Optional<T> {
	private final T value;	// T타입의 참조변수
		...
}
```

최종 연산의 결과를 그냥 반환하는 게 아니라 `Optional`객체에 담아서 반환하는 것이다. 이처럼 객체에 담아서 반환을 하면, 반환된 결과가 null인지 매번 if문으로 체크하는 대신 `Optional`에 정의된 메소드를 통해서 간단히 처리할 수 있다.

널 체크를 위한 if문 없이도 `NullPointerException`이 발생하지 않는 보다 간결하고 안전한 코드를 작성하는 것이 가능해진 것이다.

> Objects클래스에 isNull(), nonNull(), requireNonNull()과 같은 메소드가 있는 것도 널 체크를 위한 if문을 메소드 안으로 넣어서 코드의 복잡도를 낮추기 위한 것이다

</br>

### Optional객체 생성하기

`Optional`객체를 생성할 때는 `of()` 또는 `ofNullable()`을 사용한다.

``` java
String str = "abc";
Optional<String> optVal = Optional.of(str);
Optional<String> optVal = Optional.of("abc");
Optional<String> optVal = Optional.of(new String("abc"));
```

만일 참조변수의 값이 null일 가능성이 있으면, `of()`대신 `ofNullable()`을 사용해야한다. `of()`는 매개변수의 값이 null이면 `NullPointerException`이 발생하기 때문이다.

``` java
Optional<String> optVal = Optional.of(null);	// NullPointerException발생
Optional<String> optVal = Optional.ofNullalbe(null);	// OK
```

`Optional<T>`타입의 참조변수를 기본값으로 초기화할 때는 `empty()`를 사용한다. null로 초기화하는 것이 가능하지만, `empty()`로 초기화하는 것이 바람직하다.

> empty()는 제네릭 메소드라서 앞에 <T>를 붙였다. 추정 가능하므로 생략할 수 있다.

``` java
Optional<String> optVal = null;	// 널로 초기화
Optional<String> optVal = Optional.<String>empty();	// 빈 객체로 초기화
```

</br>

### Optional객체의 값 가져오기

`Optional`객체에 저장된 값을 가져올 때는 `get()`을 사용한다. 값이 null일 때는 `NoSuchElementException`이 발생하며, 이를 대비해서 `orElse()`로 대체할 값을 지정할 수 있다.

``` java
Optional<String> optVal = Optional.of("abc");
String str1 = optVal.get();	// optVal에 저장된 값을 반환. null이면 예외발생
String str2 = optVal.orElse("");	// optVal에 저장된 값이 null일 때는, ""를 반환
```

`orElse()`의 변형으로는 null을 대체할 값을 반환하는 람다식을 지정할 수 있는 `orElseGet()`과 null일 때 지정된 예외를 발생시키는 `orElseThrow()`가 있다.

``` java
T orElseGet(Supplier<? extends T> other)
T orElseThrow(Supplier<? extends T> exceptionSupplier)
```

사용하는 방법은 아래와 같다.

``` java
String str3 = optVal2.orElseGet(String::new);	// () -> new String()와 동일
STring str4 = optVal2.orElseThrow(NullPointerException::new);	// 널이면 예외발생
```

`Stream`처럼 `Optional`객체에도 `filter()`, `map()`, `flatMap()`을 사용할 수 있다. `map()`의 연산결과가 `Optional<Optional<T>>`일 때, `flatMap()`을 사용하면 `Optional<T>`를 결과로 얻는다. 만일 `Optional`객체의 값이 null이면, 이 메소드들은 아무 일도 하지 않는다.

``` java
int result = Optional.of("123");
				.filter(x -> x.length() > 0)
				.map(Integer::parseInt).orElse(-1);	// result = 123
result = Optional.of("")
			.filter(x -> x.length() > 0)
			.map(Integer::parseInt).orElse(-1);	// result = -1
```

`parseInt()`는 예외가 발생하기 쉬운 메소드이다. 만일 예외처리된 메소드를 만든다면 다음과 같을 것이다.

``` java
static int optStrToInt(Optional<String> optStr, int defaultValue) {
	try {
		return optStr.map(Integer::parseInt).get();
	} catch (Exception e) {
		return defaultValue;
	}
}
```

`isPresent()`는 `Optional`객체의 값이 null이면 false를, 아니면 true를 반환한다. `ifPresent(Consumer<T> block)`은 값이 있으면 주어진 람다식을 실행하고, 없으면 아무 일도 하지 않는다.

``` java
if(str != null) {
	System.out.println(str);
}
```

만일 위와 같은 조건문이 있다면, `isPresent()`를 이용해서 다음과 같이 쓸 수 있다.

``` java
if(Optional.ofNullable(str).isPresent()) {
	System.out.println(str);
}
```

이 코드를 `ifPresent()`를 이용해서 바꾸면 더 간단히 할 수 있다. 아래의 문장은 참조변수 `str`이 null이 아닐 때만 값을 출력하고, null이면 아무 일도 일어나지 않는다.

``` java
Optional.ofNullable(str).ifPresent(System.out::println);
```

`ifPresent()`는 `Optional<T>`를 반환하는 `findAny()`나 `findFirst()`와 같은 최종 연산과 잘 어울린다. `Stream`클래스에 정의된 메소드 중에서 `Optional<T>`를 반환하는 것들은 다음과 같다.

``` java
Optional<T> findAny()
Optional<T> findFirst()
Optional<T> max(Comparator<? super T> comparator)
Optional<T> min(Comparator<? super T> comparator)
Optional<T> reduce(BinaryOperator<T> accumulator)
```

이처럼 `Optional<T>`를 결과로 반환하는 최종 연산 메소드들은 몇 개 없다. 심지어 `max()`와 `min()`같은 메소드들은 `reduce()`를 이용해서 작성된 것이다.

</br>

### OptionalInt, OptionalLong, OptionalDouble

`IntStream`과 같은 기본형 스트림에는 `Optional`도 기본형을 값으로 하는 `OptionalInt`, `OptionalLong`, `OptionalDouble`을 반환한다. 아래의 목록은 `IntStream`에 정의된 메소드들이다.

``` java
OptionalInt findAny()
OptionalInt findFirest()
OptionalInt reduce(IntBinaryOperator op)
OptionalInt max()
OptionalInt min()
OptionalInt average()
```

반환 타입이 `Optional<T>`가 아니라는 것을 제외하고는 `Stream`에 정의된 것과 비슷하다 그리고 기본형 `Optional`에 저장된 값을 꺼낼 때 사용하는 메소드의 이름이 조금씩 다르다.

![image](https://ifh.cc/g/hl6PX9.png)

`OptionalInt`는 다음과 같이 정의되어 있다.

``` java
pulbic final class OptionalInt {
		...
	private final boolean isPresent;	// 값이 저장되어 있으면 true
	private final int value;	// int타입의 변수
```

기본형 int의 기본값은 0이므로 아무런 값도 갖지 않는 `OptionalInt`에 저장되는 값은 0일 것이다.

``` java
OptionalInt opt = OptionalInt.of(0);	// OptionalInt에 0을 저장
OptionalInt opt2 = OptionalInt.empty(0);	// OptionalInt에 0을 저장
```

저장된 값이 없는 것과 0이 저장된 것은 `isPresent`라는 인스턴스 변수로 구분이 가능하다. `isPresent()`는 이 인스턴스변수의 값은 반환한다.

``` java
System.out.println(opt.isPresent());	// true
System.out.println(opt2.isPresent());	// false

System.out.println(opt.getAsInt());	// 0
System.out.println(opt2.getAsInt());	// NoSuchElementException예외발생

System.out.println(opt.equals(opt2));	// false
```

그러나 `Optional`객체의 경우 null을 저장하면 비어있는 것과 동일하게 취급한다.

``` java
Optional<String> opt = Optional.ofNullable(null);
Optional<String> opt2 = Optional.empty();

System.out.println(opt.equals(opt2));	// true
```

</br>

예제 14-12 / ch14 / OptionalEx1.java

``` java
import java.util.*;

public class OptionalEx1 {
	public static void main(String[] args) {
		Optional<String> optStr = Optional.of("abcde");
		Optional<Integer> optInt = optStr.map(String::length);
		System.out.println("optStr = " + optStr.get());
		System.out.println("optInt = " + optInt.get());
		
		int result1 = Optional.of("123")
						.filter(x -> x.length() > 0)
						.map(Integer::parseInt).get();
		
		int result2 = Optional.of("")
						.filter(x -> x.length() > 0)
						.map(Integer::parseInt).orElse(-1);
		
		System.out.println("result1 = " + result1);
		System.out.println("result2 = " + result2);
		
		Optional.of("456").map(Integer::parseInt)
						.ifPresent(x -> System.out.printf("result3 = %d%n", x));
		
		OptionalInt optInt1 = OptionalInt.of(0);	// 0을 저장
		OptionalInt optInt2 = OptionalInt.empty();	// 빈 객체를 생성
		
		System.out.println(optInt1.isPresent());	// true
		System.out.println(optInt2.isPresent());	// false
		
		System.out.println(optInt1.getAsInt());	// 0
//		System.out.println(optInt2.getAsInt());	// NoSuchElementExcption
		System.out.println("optInt1 = " + optInt1);
		System.out.println("optInt2 = " + optInt2);
		System.out.println("optInt1.equals(optInt2) ? " + optInt1.equals(optInt2));
		
		Optional<String> opt = Optional.ofNullable(null);	// null를 저장
		Optional<String> opt2 = Optional.empty();	// 빈 객체를 생성
		System.out.println("opt = " + opt);
		System.out.println("opt2 = " + opt2);
		System.out.println("opt.equals(opt2) ? " + opt.equals(opt2));	// true
		
		int result3 = optStrToInt(Optional.of("123"), 0);
		int result4 = optStrToInt(Optional.of(""), 0);
		
		System.out.println("result3 = " + result3);
		System.out.println("result4 = " + result4);
	}
	
	static int optStrToInt(Optional<String> optStr, int defaultValue) {
		try {
			return optStr.map(Integer::parseInt).get();
		} catch (Exception e) {
			return defaultValue;
		}
	}
}
```

```
optStr = abcde
optInt = 5
result1 = 123
result2 = -1
result3 = 456
true
false
0
optInt1 = OptionalInt[0]
optInt2 = OptionalInt.empty
optInt1.equals(optInt2) ? false
opt = Optional.empty
opt2 = Optional.empty
opt.equals(opt2) ? true
result3 = 123
result4 = 0
```

</br>

## 2.5 스트림의 최종 연산

최종 연산은 스트림의 요소를 소모해서 결과를 만들어낸다. 그래서 최종 연산후에는 스트림이 닫히게 되고 더 이상 사용할 수 없다. 최종 연산의 결과는 스트림 요소의 합과 같은 단일 값이거나, 스트림의 요소가 담긴 배열 또는 컬렉션일 수 있다.

</br>

### forEach

`forEach()`는 `peek()`과 달리 스트림의 요소를 소모하는 최종연산이다. 반환 타입이 void이므로 스트림의 요소를 출력하는 용도로 많이 사용된다.

``` java
void forEach(Consumer<? super T> action)
```

</br>

### 조건 검사 - allMatch(), anyMatch(), noneMatch(), findFirst(), findAny()

스트림에 요소에 대해 지정된 조건에 모든 요소가 일치하는 지, 일부가 일치하는지 아니면 어떤 요소도 일치하지 않는지 확인하는데 사용할 수 있는 메소드들이다. 이 메소드들은 모두 매개변수로 `Predicate`를 요구하며, 연산결과로 boolean을 반환한다.

``` java
boolean allMatch (Predicate<? super T> predicate)
boolean anyMatch (Predicate<? super T> predicate)
boolean noneMatch (Predicate<? super T> predicate)
```

예를 들어 학생들의 성적 정보 스트림 `stuStream`에서 총점이 낙제점(총점 100이하)인 학생이 있는지 확인하는 방법은 다음과 같다.

``` java
boolean noFailed = stuStream.anyMatch(s -> s.getTotalScore() <= 100)
```

이외에도 스트림의 요소 중에서 조건에 일치하는 첫 번째 것을 반환하는 `findFirst()`가 있는데, 주로 `filter()`와 함께 사용되어 조건에 맞는 스트림의 요소가 있는지 확인하는데 사용된다. 병렬 스트림인 경우에는 `findFirst()`대신 `findAny()`를 사용해야 한다.

``` java
Optional<Student> stu = stuStream.filter(s -> s.getTotalScore() <= 100).findFirst();
Optional<Student> stu = parallelStream.filter(s -> s.getTotalScore() <= 100).findAny();
```

`findAny()`와 `findFirst()`의 반환 타입은 `Optional<T>`이며, 스트림의 요소가 없을 때는 비어있는 `Optional`객체를 반환한다.

> 비어있는 Operator객체는 내부적으로 null을 저장하고 있다.

</br>

### 통계 - count(), sum(), average(), max(), min()

`IntStream`과 같은 기본형 스트림에는 스트림의 요소들에 대한 통계 정보를 얻을 수 있는 메소드들이 있다. 그러나 기본형 스트림이 아닌 경우에는 통계와 관련된 메소드들이 아래의 3개뿐이다.

> 기본형 스트림의 min(), max()와 달리 매개변수로 Comparator를 필요로 한다는 차이가 있다.

``` java
long count()
Optional<T> max(Comparator<? super T> comparator)
Optional<T> min(Comparator<? super T> comparator)
```

대부분의 경우 위의 메소드를 사용하기보다 기본형 스트림으로 변환하거나, 아니면 `reduce()`와 `collect()`를 사용해서 통계 정보를 얻는다.

</br>

### 리듀싱 - reduce()

`reduce()`는 스르림의 요소를 줄여나가면서 연산을 수행하고 최종결과를 반환한다. 그래서 매개변수의 타입이 `BinaryOperator<T>`인 것이다. 처음 두 요소를 가지고 연산한 결과를 가지고 그 다음 요소와 연산한다.

이 과정에서 스트림의 요소를 하나씩 소모하게 되며, 스트림의 모든 요소를 소모하게 되면 그 결과를 반환한다.

``` java
Optional<T> reduce(BinaryOperator<T> accumulator)
```

이 외에도 연산결과의 초기값(identity)을 갖는 `reduce()`도 있는데, 이 메소드들은 초기값과 스트림의 첫 번째 요소로 연산을 시작한다. 스트림의 요소가 하나도 없는 경우, 초기값이 반환되므로, 반환 타입이 `Optional<T>`가 아니라 `T`이다.

> BinaryOperator<T>는 BiFunction의 자손이며, BiFunction<T, T, T>와 동등하다.

``` java
T reduce(T identity, BinaryOperator<T> accumulator)
U reduce(U identity, BiFunction<U, T, U> accumulator, BinaryOperator<U> combiner)
```

위의 두 번째 메소드의 마지막 매개변수인 `combiner`는 병렬 스트림에 의해 처리된 결과를 합칠 때 사용하기 위해 사용한다.

최종 연산 `count()`와 `sum()` 등은 내부적으로 모두 `reduce()`를 이용해서 아래와 같이 작성된 것이다.

``` java
int count = intStream.reduce(0, (a, b) -> a + 1);	// count()
int sum = intStream.reduce(0, (a, b) -> a + b);	// sum()
int max = intStream.reduce(Integer.MIN_VALUE, (a, b) -> a > b ? a : b);	//max()
int min = intStream.reduce(Integer.MAX_VALUE, (a, b) -> a < b ? a : b);	// min()
```

사실 `max()`와 `min()`의 경우, 초기값이 필요없으므로 `Optional<T>`를 반환하는 매개변수 하나짜리 `reduce()`를 사용하는 것이 낫다. 단, `intStream`의 타입이 `IntStream`인 경우 `OptionalInt`를 사용해야 한다. `Stream<T>`와 달리 `IntStream`에 정의된 `reduce()`의 반환 타입이 `OptionalInt`이기 때문이다.

``` java
// OptionalInt reduce(IntBinaryOperator accumulator)
OptionalInt max = intStream.reduce((a, b) -> a > b ? a : b);	// max()
OptionalInt min = intStream.reduce((a, b) -> a < b ? a : b);	// min()
```

참고로 위의 문장들에서 람다식을 `Integer`클래스의 static메소드 `max()`와 `min()`을 이용해서 메소드 참조로 바꾸면 다음과 같다.

``` java
OptionalInt max = intStream.reduce(Integer::max);	// int max(int a, int b)
OptionalInt min = intStream.reduce(Integer::min);	// int min(int a, int b)
```

그리고 `OptionalInt`에 저장된 값을 꺼내려면 아래와 같이 하면 된다.

``` java
int maxValue = max.getAsInt();	// OptionalInt에 저장된 값을 maxValue에 저장
```

`reduce()`로 스트림의 모든 요소를 다 더하는 과정을 for문으로 표현해 보았다.

``` java
int a = identity;	// 초기값을 a에 저장한다.

for(int b : stream)
	a = a + b;	// 모든 요소의 값을 a에 누적한다.
```

`reduce()`가 다음과 같이 작성되어 있다.

``` java
T reduce(T identity, BinaryOperator<T> accumulator) {
	T a = identity;

	for(T b : stream)
		a = accumulator.apply(a, b);

	return a;
}
```

`reduce()`를 사용하는 방법은 간단하다. 그저 초기값(identity)과 어떤 연산(BinaryOperator)으로 스트림의 요소를 줄여나갈 것인지만 결정하면 된다.

</br>

예제 14-13 / ch14 / StreamEx5.java

``` java
import java.util.*;
import java.util.stream.*;

public class StreamEx5 {
	public static void main(String[] args) {
		String[] strArr = {
			"Inheritance", "Java", "Lambda", "stream",
			"OptionalDouble", "IntStream", "count", "sum"
		};
		
		Stream.of(strArr).forEach(System.out::println);
		
		boolean noEmptyStr = Stream.of(strArr).noneMatch(s -> s.length() == 0);
		Optional<String> sWord = Stream.of(strArr)
								.filter(s -> s.charAt(0) == 's').findFirst();
		
		System.out.println("noEmptyStr = " + noEmptyStr);
		System.out.println("sWord = " + sWord.get());
		
		// Stream<String[]>을 IntStream으로 변환
		IntStream intStream1 = Stream.of(strArr).mapToInt(String::length);
		IntStream intStream2 = Stream.of(strArr).mapToInt(String::length);
		IntStream intStream3 = Stream.of(strArr).mapToInt(String::length);
		IntStream intStream4 = Stream.of(strArr).mapToInt(String::length);
		
		int count = intStream1.reduce(0, (a, b) -> a + 1); 
		int sum = intStream2.reduce(0, (a, b) -> a + b);
		
		OptionalInt max = intStream3.reduce(Integer::max);
		OptionalInt min = intStream4.reduce(Integer::min);
		
		System.out.println("count = " + count);
		System.out.println("sum = " + sum);
		System.out.println("max = " + max.getAsInt());
		System.out.println("min = " + min.getAsInt());
	}
}
```

```
Inheritance
Java
Lambda
stream
OptionalDouble
IntStream
count
sum
noEmptyStr = true
sWord = stream
count = 8
sum = 58
max = 14
min = 3
```

</br>

## 2.6 collect()

`collect()`는 스트림의 요소를 수집하는 최종 연산으로 리듀싱(reducing)과 유사하다. `collect()`가 스트림의 요소를 수집하려면, 어떻게 수집할 것인가에 대한 방법이 정의되어 있어야 하는데, 이 방법을 정의한 것이 바로 컬렉터(collector)이다.

컬렉터는 `Collector`인터페이스를 구현한 것으로, 직접 구현할 수도 있고 미리 작성된 것을 사용할 수도 있다. `Collectors`클래스는 미리 작성된 다양한 종류의 컬렉터를 반환하는 static메소드를 가지고 있으며, 이 클래스를 통해 제공되는 컬렉터만으로도 많은 일들을 할 수 있다.

> **collect()** 스트림의 최종연산, 매개변수로 컬렉터를 필요로 한다.   
**Collector** 인터페이스, 컬렉터는 이 인터페이스를 구현해야한다.   
**Collectors** 클래스, static메소드로 미리 작성된 컬렉터를 제공한다.

`collect()`는 매개변수의 타입이 `Collector`인데, 매개변수가 `Collector`를 구현한 클래스의 객체이어야 한다는 뜻이다. 그리고 `collect()`는 이 객체에 구현된 방법대로 스트림의 요소를 수집한다.

> sort()할 때, Comparator가 필요한 것처럼 collect()할 때는 Collector가 필요하다.

``` java
Object collect(Collector collector)	// Collector를 구현한 클래스의 객체를 매개변수로
Object collect(Supplier supplier, BiConsumer accumulator, BiConsumer combiner)
```

그리고 매개변수가 3개나 정의된 `collect()`는 잘 사용되지 않지만, `Collector`인터페이스를 구현하지 않고 간단히 람다식으로 수집할 때 사용하면 편리하다.

</br>

### 스트림을 컬렉션과 배열로 변환 - toList(), toSet(), toMap(), toCollection(), toArray()

스트림의 모든 요소를 컬렉션에 수집하려면, `Collectors`크랠스의 `toList()`와 같은 메소드를 사용하면 된다. `List`나 `Set`이 아닌 특정 컬렉션을 저장하려면, `toCollection()`에 해당 켈렉션의 생성자 참조를 매개변수로 넣어주면 된다.

``` java
List<String> names = stuStream.map(Student::getName)
								.collect(Collectors.toList());
ArrayList<String> list = names.stream()
					.collect(Collectors.toCollection(ArrayList::new));
```

`Map`은 키와 값의 쌍으로 저장해야하므로 객체의 어떤 필드를 키로 사용할 지와 값으로 사용할 지를 지정해줘야 한다.

``` java
Map<String, Person> map = personStream
					.collect(Collectors.toMap(p -> p.getRegId(), p -> p));
```

위의 문장은 요소의 타입이 `Person`인 스트림에서 사람의 주민번호(regId)를 키로 하고, 값으로 `Person`객체를 그대로 저장한다.

> 항등 함수를 의미하는 람다식 'p -> p' 대신 Function.identity()를 쓸 수도 있다.

스트림에 저장된 요소들을 `T[]`타입의 배열로 변환하려면, `toArray()`를 사용하면 된다. 단, 해당 타입의 생성자 참조를 매개변수로 지정해줘야 한다. 만일 매개변수를 지정하지 않으면 반환되는 배열의 타입이 `Object[]`이다.

``` java
Student[] stuNames = studentStream.toArray(Student[]::new);	// OK
Student[] stuNames = studentStream.toArray();	// 에러.
Object[] stuNames = studentStream.toArray();	// OK
```

</br>

### 통계 - counting(), summingInt(), averageingInt(), maxBy(), minBy()

최종 연산들이 제공하는 통계 정보를 `collect()`로 똑같이 얻을 수 있다. 보다 간결한 코드를 위해 `Collectors`의 static메소드를 호출할 때는 `Collectors.`를 생략하였다. `static import`되어 있다고 가정하겠다.

> summingInt()외에도 summingLong(), summingDouble()이 있다. averagingInt()도 마찬가지다.

``` java
long count = stuStream.count();
long count = stuStream.collect(counting());	// Collectors.counting()

long totalScore = stuStream.mapToInt(Student::getTotalScore).sum();
long totalScore = stuStream.collect(summingInt(Student::getTotalScore));

OptionalInt topScore = studentStream.mapToInt(Student::getTotalScore).max();
Optional<Student> topStudent = stuStream.max(Comparator.comparingInt(Student::getTotalScore));
Optional<Student> topStudent = stuStream.collect(MaxBy(Comparator.comparingInt(Student::getTotalScore)));

IntSummaryStatistics stat = stuStream.mapToInt(Student::getTotalScore).summaryStatistics();
IntSummaryStatistics stat = stuStream.collect(summarizingInt(Student::getTotaScore));
```

`summingInt()`와 `summarizingInt()`를 혼동하지 않도록 주의해야 한다.

</br>

### 리듀싱 - reducing()

리듀싱 역시 `collct()`로 가능하다. `IntStream`에는 매개변수 3개짜리 `collect()`만 정의되어 있으므로 `boxed()`를 통해 `IntStream`을 `Stream<Integer>`로 변환해야 매개변수 1개짜리 `collect()`를 쓸 수 있다.

``` java
IntStream intStream = new Random().ints(1, 46).distinct().limit(6);

OptionalInt max = intStream.reduce(Integer::max);
Optional<Integer> max = intStream.boxed().collect(reducing(Integer::max));

long sum = intStream.reduce(0, (a, b) -> a + b);
long sum = intStream.boxed().collect(reducing(0, (a, b) -> a + b));

int grandTotal = stuStream.map(Student::getTotalScore).reduce(0, Integer::sum);
int grandTotal = stuStream.collect(reducing(0, Student::getTotalScore, Integer::sum));
```

`Collectors.reducing()`에는 아래와 같이 3가지 종류가 있다. 세 번째 메소드만 제외하고 `reduce()`와 같다. 세 번째 것은 `map()`과 `reduce()`를 하나로 합쳐놓은 것이다.

``` java
Collector reducing(BinaryOperator<T> op)
Collector reducing(T identity, BinaryOperator<T> op)
Collector reducing(U identity, Function<T, U> mapper, BinaryOperator<u> op)
```

위의 메소드 목록 역시 와일드 카드를 제거하여 간략히 하였다.

</br>

### 문자열 결합 - joining()

문자열 스트림의 모든 요소를 하나의 문자열로 연결해서 반환한다. 구분자를 지정해줄 수도 있고, 접두사와 접미사도 지정가능하다. 스트림의 요소가 `String`이나 `StringBuffer`처럼 `CharSequence`의 자손인 경우에만 결합이 가능하므로 스트림의 요소가 문자열이 아닌 경우에는 먼저 `map()`을 이용해서 스트림의 요소를 문자열로 변환해야 한다.

``` java
String studentNames = stuStream.map(Student::getName).collect(joining());
String studentNames = stuStream.map(Student::getName).collect(joining(","));
String studentNames = stuStream.map(Student::getName).collect(joining(",", "[", "]"));
```

만일 `map()`없이 스트림에 바로 `joining()`하면, 스트림의 요소에 `toString()`을 호출한 결과를 결합한다.

``` java
// Student의 toString()으로 결합
String studentInfo = stuStream.collect(joining(","));
```

</br>

예제 14-14 / ch14 / StreamEx6.java

``` java
import java.util.*;
import java.util.stream.*;
import static java.util.stream.Collectors.*;

public class StreamEx6 {
	public static void main(String[] args) {
		Student[] stuArr = {
			new Student("이자바", 3, 300),
			new Student("김자바", 1, 200),
			new Student("안자바", 2, 100),
			new Student("박자바", 2, 150),
			new Student("소자바", 1, 200),
			new Student("나자바", 3, 290),
			new Student("감자바", 3, 180)
		};
		
		// 학생 이름만 뽑아서 List<String>에 저장
		List<String> names = Stream.of(stuArr).map(Student::getName).collect(Collectors.toList());
		System.out.println(names);
		
		// 스트림을 배열로 변환
		Student[] stuArr2 = Stream.of(stuArr).toArray(Student[]::new);
		
		for(Student s : stuArr2)
			System.out.println(s);
		
		// 스트림을 Map<String, Student>로 변환. 학생 이름이 key
		Map<String, Student> stuMap = Stream.of(stuArr).collect(Collectors.toMap(s -> s.getName(), p -> p));
		
		for(String name : stuMap.keySet())
			System.out.println(name + "-" + stuMap.get(name));
		
		long count = Stream.of(stuArr).collect(counting());
		long totalScore = Stream.of(stuArr).collect(summingInt(Student::getTotalScore));
		System.out.println("count = " + count);
		System.out.println("totalScore = " + totalScore);
		
		totalScore = Stream.of(stuArr).collect(reducing(0, Student::getTotalScore, Integer::sum));
		System.out.println("totalScore = " + totalScore);
		
		Optional<Student> topStudent = Stream.of(stuArr).collect(maxBy(Comparator.comparingInt(Student::getTotalScore)));
		System.out.println("topStudent = " + topStudent.get());
		
		IntSummaryStatistics stat = Stream.of(stuArr).collect(summarizingInt(Student::getTotalScore));
		System.out.println(stat);
		
		String stuNames = Stream.of(stuArr).map(Student::getName).collect(joining(",", "{", "}"));
		System.out.println(stuNames);
	}
}
```

```
[이자바, 김자바, 안자바, 박자바, 소자바, 나자바, 감자바]
[이자바, 3, 300]
[김자바, 1, 200]
[안자바, 2, 100]
[박자바, 2, 150]
[소자바, 1, 200]
[나자바, 3, 290]
[감자바, 3, 180]
안자바-[안자바, 2, 100]
김자바-[김자바, 1, 200]
박자바-[박자바, 2, 150]
나자바-[나자바, 3, 290]
감자바-[감자바, 3, 180]
이자바-[이자바, 3, 300]
소자바-[소자바, 1, 200]
count = 7
totalScore = 1420
totalScore = 1420
topStudent = [이자바, 3, 300]
IntSummaryStatistics{count=7, sum=1420, min=100, average=202.857143, max=300}
{이자바,김자바,안자바,박자바,소자바,나자바,감자바}
```

</br>

### 그룹화와 분할 - groupingBy(), partitioningBy()

그룹화는 스트림의 요소를 특정 기준으로 그룹화하는 것을 의미하고, 분할은 스트림의 요소를 두 가지, 지정된 조건에 일치하는 그룹과 일치하지 않는 그룹으로의 분할을 의미한다. 아래의 메소드 정의에서 알 수 있듯이, `groupingBy()`는 스트림의 요소를 `Function`으로, `partitioningBy()`는 `Predicate`로 분류한다.

``` java
Collector groupingBy(Function classifier)
Collector groupingBy(Function classifier, Collector downstream)
Collector groupingBy(Function classifier, Supplier mapFactory, Collector downstream)
Collector partitioningBy(Predicate predicate)
Collector partitioningBy(Predicate predicate, Collector downstream)
```

메소드의 정의를 보면 `groupingBy()`와 `partitioningBy()`가 분류를 `Function`으로 하느냐 `Predicate`로 하느냐의 차이만 있을 뿐 동일하다. 스트림을 두 개의 그룹으로 나눠야 한다면, 당연히 `partitioningBy()`로 분할하는 것이 더 빠르다. 그 외에는 `groupingBy()`를 쓰면 된다. 그리고 그룹화와 분할의 결과는 `Map`에 담겨 반환된다.

먼저 예시에 사용될 `Student`클래스는 다음과 같이 정의되어 있다고 가정하겠다.

``` java
class Student2 {
	String name;	// 이름
	boolean isMale;	// 성별
	int hak;	// 학년
	int ban;	// 반
	int score;	// 점수
	
	Student2(String name, boolean isMale, int hak, int ban, int score) {
		this.name = name;
		this.isMale = isMale;
		this.hak = hak;
		this.ban = ban;
		this.score = score;
	}
	
	String getName() { return name; }
	boolean isMale() { return isMale; }
	int getHak() { return hak; }
	int getBan() { return ban; }
	int getScore() { return score; }
	
	public String toString() {
		return String.format("[%s, %s, %d학년, %d반, %3d점]",
			name, isMale ? "남" : "여", hak, ban, score);
	}
	
	enum Level { HIGH, MID, LOW }	// 성적 상, 중, 하 세 단계로 분류
}	// class Student
```

그리고 스트림 `stuStream`은 아래와 같은 요소들로 이루어져 있다고 가정하겠다.

``` java
Stream<Student2> stuStream = Stream.of(
	new Student2("나자바", true, 1, 1, 300),
	new Student2("김지미", false, 1, 1, 250),
	new Student2("김자바", true, 1, 1, 200),
	new Student2("이지미", false, 1, 2, 150),
	new Student2("남자바", true, 1, 2, 100),
	new Student2("안지미", false, 1, 2, 50),
	new Student2("황지미", false, 1, 3, 100),
	new Student2("강지미", false, 1, 3, 150),
	new Student2("이자바", true, 1, 3, 200),

	new Student2("나자바", true, 2, 1, 300),
	new Student2("김지미", false, 2, 1, 250),
	new Student2("김자바", true, 2, 1, 200),
	new Student2("이지미", false, 2, 2, 150),
	new Student2("남자바", true, 2, 2, 100),
	new Student2("안지미", false, 2, 2, 50),
	new Student2("황지미", false, 2, 3, 100),
	new Student2("강지미", false, 2, 3, 150),
	new Student2("이자바", true, 2, 3, 200),
```

</br>

### partitioningBy()에 의한 분류

상대적으로 간단한 `partitioningBy()`로 가장 기본적인 분할은 학생들을 성별로 나누어 `List`에 담는 것이다.

``` java
// 1. 기본 분할
Map<Boolean, List<Student2>> stuBySex = stuStream
				.collect(partitioningBy(Student2::isMale));	// 학생들을 성별로 분할
		
List<Student2> maleStudent = stuBySex.get(true);	// Map에서 남학생 목록을 얻는다.
List<Student2> femaleStudent = stuBySex.get(false);	// Map에서 여학생 목록을 얻는다.
```

이번엔 `counting()`을 추가해서 남학생의 수와 여학생의 수를 구해보겠다.

``` java
Map<Boolean, Long> stuNumBySex = stuStream
				.collect(partitioningBy(Student2::isMale, counting()));
		
System.out.println("남학생 수 : " + stuNumBySex.get(true));	// 남학생 수 : 8
System.out.println("여학생 수 : " + stuNumBySex.get(false));	// 여학생 수 : 10
```

`counting()`대신 `summingLong()`을 사용하면, 남학생과 여학생의 총점을 구할 수 있다

``` java
Map<Boolean, Optional<Student2>> topScoreBySex = stuStream
				.collect(
					partitioningBy(Student2::isMale,
						maxBy(comparingInt(Student2::getScore))
					)
				);
System.out.println("남학생 1등 : " + topScoreBySex.get(true));
System.out.println("남학생 1등 : " + topScoreBySex.get(false));

// 남학생 1등 : Optional[[나자바, 남, 1, 1, 300]]
// 여학생 1등 : Optional[[김지미, 여, 1, 1, 250]]
```

`MaxBy()`는 반환타입이 `Optional<Student>`라서 위와 같은 겨로가가 나왔다. `Optional<Student>`가 아닌 `Student`를 반환 결과로 얻으려면, 아래와 같이 `collectingAndThen()`과 `Optional::get`을 함께 사용하면 된다.

``` java
Map<Boolean, Student2> topScoreBySex2 = stuStream
			.collect(
				partitioningBy(Student2::isMale,
					collectingAndThen(
						maxBy(comparingInt(Student2::getScore)), Optional::get
					)
				)	// 남학생 1등 : [나자바, 남, 1, 1, 300]
			);		// 여학생 1등 : [김지미, 여, 1, 1, 250]
		
System.out.println("남학생 1등 : " + topScoreBySex2.get(true));
System.out.println("여학생 1등 : " + topScoreBySex2.get(false));
```

성적 150점 아래인 학생들은 불합격처리하고 싶을 때, 불합격자를 성별로 분류하여 얻어내려면 `partitioningBy()`를 한 번 더 사용해서 이중 분할을 하면 된다.

``` java
Map<Boolean, Map<Boolean, List<Student2>>> failedStuBySex = stuStream
	.collect(
		partitioningBy(Student2::isMale,
			partitioningBy(s -> s.getScore() < 150)
		)
	);
List<Student2> failedMaleStu = failedStuBySex.get(true).get(true);
List<Student2> failedFemaleStu = failedStuBySex.get(false).get(true);
```

</br>

예제 14-15 / ch14 / StreamEx7.java

``` java
import java.util.*;
import java.util.function.*;
import java.util.stream.*;
import static java.util.stream.Collectors.*;
import static java.util.Comparator.*;

class Student2 {
	String name;
	boolean isMale;	// 성별
	int hak;	// 학년
	int ban;	// 반
	int score;
	
	Student2(String name, boolean isMale, int hak, int ban, int score) {
		this.name = name;
		this.isMale = isMale;
		this.hak = hak;
		this.ban = ban;
		this.score = score;
	}
	
	String getName() { return name; }
	boolean isMale() { return isMale; }
	int getHak() { return hak; }
	int getBan() { return ban; }
	int getScore() { return score; }
	
	public String toString() {
		return String.format("[%s, %s, %d학년, %d반, %3d점]",
			name, isMale ? "남" : "여", hak, ban, score);
	}
	
	// groupingBy()에서 사용
	enum Level { HIGH, MID, LOW }	// 성적 상, 중, 하 세 단계로 분류
}

public class StreamEx7 {
	public static void main(String[] args) {
		Student2[] stuArr = {
			new Student2("나자바", true, 1, 1, 300),
			new Student2("김지미", false, 1, 1, 250),
			new Student2("김자바", true, 1, 1, 200),
			new Student2("이지미", false, 1, 2, 150),
			new Student2("남자바", true, 1, 2, 100),
			new Student2("안지미", false, 1, 2, 50),
			new Student2("황지미", false, 1, 3, 100),
			new Student2("강지미", false, 1, 3, 150),
			new Student2("이자바", true, 1, 3, 200),
			new Student2("나자바", true, 2, 1, 300),
			new Student2("김지미", false, 2, 1, 250),
			new Student2("김자바", true, 2, 1, 200),
			new Student2("이지미", false, 2, 2, 150),
			new Student2("남자바", true, 2, 2, 100),
			new Student2("안지미", false, 2, 2, 50),
			new Student2("황지미", false, 2, 3, 100),
			new Student2("강지미", false, 2, 3, 150),
			new Student2("이자바", true, 2, 3, 200),
		};
		
		System.out.printf("1. 단순분할(성별로 분할)%n");
		Map<Boolean, List<Student2>> stuBySex = Stream.of(stuArr)
				.collect(partitioningBy(Student2::isMale));
		
		List<Student2> maleStudent = stuBySex.get(true);
		List<Student2> femaleStudent = stuBySex.get(false);
		
		for(Student2 s : maleStudent) System.out.println(s);
		for(Student2 s : femaleStudent) System.out.println(s);
		
		System.out.printf("%n2. 단순분할 + 통계(성별 학생수)%n");
		Map<Boolean, Long> stuNumBySex = Stream.of(stuArr)
				.collect(partitioningBy(Student2::isMale, counting()));
		
		System.out.println("남학생 수 : " + stuNumBySex.get(true));
		System.out.println("여학생 수 : " + stuNumBySex.get(false));
		
		System.out.printf("%n3. 단순분할 + 통계(성별 1등)%n");
		Map<Boolean, Optional<Student2>> topScoreBySex = Stream.of(stuArr)
				.collect(partitioningBy(Student2::isMale,
					maxBy(comparingInt(Student2::getScore))
				));
		System.out.println("남학생 1등 : " + topScoreBySex.get(true));
		System.out.println("남학생 1등 : " + topScoreBySex.get(false));
		
		Map<Boolean, Student2> topScoreBySex2 = Stream.of(stuArr)
			.collect(partitioningBy(Student2::isMale,
				collectingAndThen(
					maxBy(comparingInt(Student2::getScore)), Optional::get
				)
			));
		
		System.out.println("남학생 1등 : " + topScoreBySex2.get(true));
		System.out.println("여학생 1등 : " + topScoreBySex2.get(false));
		
		System.out.printf("%n4. 다중분할(성별 불합격자, 100점 이하)%n");
		
		Map<Boolean, Map<Boolean, List<Student2>>> failedStuBySex =
			Stream.of(stuArr).collect(partitioningBy(Student2::isMale,
				partitioningBy(s -> s.getScore() <= 100))
			);
		List<Student2> failedMaleStu = failedStuBySex.get(true).get(true);
		List<Student2> failedFemaleStu = failedStuBySex.get(false).get(true);
		
		for(Student2 s : failedMaleStu) System.out.println(s);
		for(Student2 s : failedFemaleStu) System.out.println(s);
	}
}
```

```
1. 단순분할(성별로 분할)
[나자바, 남, 1학년, 1반, 300점]
[김자바, 남, 1학년, 1반, 200점]
[남자바, 남, 1학년, 2반, 100점]
[이자바, 남, 1학년, 3반, 200점]
[나자바, 남, 2학년, 1반, 300점]
[김자바, 남, 2학년, 1반, 200점]
[남자바, 남, 2학년, 2반, 100점]
[이자바, 남, 2학년, 3반, 200점]
[김지미, 여, 1학년, 1반, 250점]
[이지미, 여, 1학년, 2반, 150점]
[안지미, 여, 1학년, 2반,  50점]
[황지미, 여, 1학년, 3반, 100점]
[강지미, 여, 1학년, 3반, 150점]
[김지미, 여, 2학년, 1반, 250점]
[이지미, 여, 2학년, 2반, 150점]
[안지미, 여, 2학년, 2반,  50점]
[황지미, 여, 2학년, 3반, 100점]
[강지미, 여, 2학년, 3반, 150점]

2. 단순분할 + 통계(성별 학생수)
남학생 수 : 8
여학생 수 : 10

3. 단순분할 + 통계(성별 1등)
남학생 1등 : Optional[[나자바, 남, 1학년, 1반, 300점]]
남학생 1등 : Optional[[김지미, 여, 1학년, 1반, 250점]]
남학생 1등 : [나자바, 남, 1학년, 1반, 300점]
여학생 1등 : [김지미, 여, 1학년, 1반, 250점]

4. 다중분할(성별 불합격자, 100점 이하)
[남자바, 남, 1학년, 2반, 100점]
[남자바, 남, 2학년, 2반, 100점]
[안지미, 여, 1학년, 2반,  50점]
[황지미, 여, 1학년, 3반, 100점]
[안지미, 여, 2학년, 2반,  50점]
[황지미, 여, 2학년, 3반, 100점]
```

</br>

### groupingBy()에 의한 분류

`stuStream`을 반 별로 그룹지어 `Map`에 저장하는 방법은 다음과 같다.

``` java
Map<Integer, List<Student3>> stuByBan = stuStream
		.collect(groupingBy(Student::getBan));	// toList()가 생략됨
```

`groupingBy()`로 그룹화를 하면 기본적으로 `List<T>`에 담는다. 그래서 위의 문장은 아래문자으이 생략된 형태이다. 만일 원한다면, `toList()`대신 `toSet()`이나 `toCollection(HashSet::new)`을 사용할 수도 있다. 단, `Map`의 제네릭 타입도 적절히 변경해줘야 한다.

``` java
Map<Integer, List<Student3>> stuByBan = stuStream
	.collect(groupingBy(Student::getBan, toList()));	// toList() 생략가능

Map<Integer, HashSet<Student3>> stuByHak = stuStream
	.collect(groupingBy(Student::getHak, toCollection(HashSet::new)));
```

이번엔 조금 복잡하게 `stuStream`을 성적의 등급(Student.Level)으로 그룹화 해보겠다. 아래의 문장은 모든 학생을 세 등급(HIGH, MID, LOW)으로 분류하여 집계한다.

``` java
Map<Student3.Level, Long> stuByLevel = stuStream
	.collect(groupingBy(s -> {
			if(s.getScore() >= 200) return Student3.Level.HIGH;
			else if(s.getScore() >= 100) return Student3.Level.MID;
			else return Student3.Level.LOW;
		}, counting())
	);	// [MID] - 8명, [HIGH] - 8명, [LOW] - 2명
```

`groupingBy()`를 여러 번 사용하면, 다수준 그룹화가 가능하다. 만일 학년별로 그룹화 한 후에 다시 반별로 그룹화하고 싶으면 다음과 같이 한다.

``` java
Map<Integer, Map<Integer, List<Student3>>> stuByHakAndBan = stuStream
		.collect(groupingBy(Student3::getHak,
				groupingBy(Student3::getBan)
		));
```

위의 코드를 발전시켜서 각 반이 1등을 출력하고 싶다면, `collectingAndThen()`과 `maxBy()`를 써서 다음과 같이 하면 된다.

``` java
Map<Integer, Map<Integer, Student3>> topStuByHakAndBan = stuStream
		.collect(groupingBy(Student3::getHak,
				groupingBy(Student3::getBan,
						collectingAndThen(
							maxBy(comparingInt(Student3::getScore)), Optional::get
						)
				)
		));
```

아래의 코드는 학년별로 반별로 그룹화한 다음에, 성적그룹으로 변환(mapping)하여 `Set`에 저장한다.

``` java
Map<Integer, Map<Integer, Set<Student3.Level>>> stuByHakAndBan = stuStream
	.collect(
		groupingBy(Student::getHak,
			groupingBy(Student::getBan,
				mapping(s -> {
					if(s.getScore() >= 200) return Student3.Level.HIGH;
					else if(s.getScore() >= 100) return Student3.Level.MID;
					else return Student3.Level.LOW;
				}, toSet())
			)
		)
	);
```

</br>

예제 14-16 / ch14 / StreamEx8.java

``` java
import java.util.*;
import java.util.function.*;
import java.util.stream.*;
import static java.util.stream.Collectors.*;
import static java.util.Comparator.*;

class Student3 {
	String name;
	boolean isMale;	// 성별
	int hak;	// 학년
	int ban;	// 반
	int score;
	
	Student3(String name, boolean isMale, int hak, int ban, int score) {
		this.name = name;
		this.isMale = isMale;
		this.hak = hak;
		this.ban = ban;
		this.score = score;
	}
	
	String getName() { return name; }
	boolean isMale() { return isMale; }
	int getHak() { return hak; }
	int getBan() { return ban; }
	int getScore() { return score; }
	
	public String toString() {
		return String.format("[%s, %s, %d학년, %d반, %3d점]",
			name, isMale ? "남" : "여", hak, ban, score);
	}
	
	enum Level {
		HIGH, MID, LOW
	}
}

public class StreamEx8 {
	public static void main(String[] args) {
		Student3[] stuArr = {
			new Student3("나자바", true, 1, 1, 300),
			new Student3("김지미", false, 1, 1, 250),
			new Student3("김자바", true, 1, 1, 200),
			new Student3("이지미", false, 1, 2, 150),
			new Student3("남자바", true, 1, 2, 100),
			new Student3("안지미", false, 1, 2, 50),
			new Student3("황지미", false, 1, 3, 100),
			new Student3("강지미", false, 1, 3, 150),
			new Student3("이자바", true, 1, 3, 200),
			
			new Student3("나자바", true, 2, 1, 300),
			new Student3("김지미", false, 2, 1, 250),
			new Student3("김자바", true, 2, 1, 200),
			new Student3("이지미", false, 2, 2, 150),
			new Student3("남자바", true, 2, 2, 100),
			new Student3("안지미", false, 2, 2, 50),
			new Student3("황지미", false, 2, 3, 100),
			new Student3("강지미", false, 2, 3, 150),
			new Student3("이자바", true, 2, 3, 200),
		};
		
		System.out.printf("1. 단순그룹화(반별로 분할)%n");
		Map<Integer, List<Student3>> stuByBan = Stream.of(stuArr)
				.collect(groupingBy(Student3::getBan));
		
		for(List<Student3> ban : stuByBan.values()) {
			for(Student3 s : ban) {
				System.out.println(s); 
			}
		}
		
		System.out.printf("%n2. 단순그룹화(성적별로 그룹화)%n");
		Map<Student3.Level, List<Student3>> stuByLevel = Stream.of(stuArr)
				.collect(groupingBy(s -> {
						if(s.getScore() >= 200) return Student3.Level.HIGH;
						else if(s.getScore() >= 100) return Student3.Level.MID;
						else return Student3.Level.LOW;
				}));
		
		TreeSet<Student3.Level> keySet = new TreeSet<>(stuByLevel.keySet());
		
		for(Student3.Level key : keySet) {
			System.out.println("[" + key + "]");
			
			for(Student3 s : stuByLevel.get(key))
				System.out.println(s);
			System.out.println();
		}
		
		System.out.printf("%n3. 단순그룹화 + 통계(성적별 학생수)%n");
		Map<Student3.Level, Long> stuCntByLevel = Stream.of(stuArr)
			.collect(groupingBy(s -> {
					if(s.getScore() >= 200) return Student3.Level.HIGH;
					else if(s.getScore() >= 100) return Student3.Level.MID;
					else return Student3.Level.LOW;
			}, counting()));
		
		for(Student3.Level key : stuCntByLevel.keySet())
			System.out.printf("[%s] - %d명, ", key, stuCntByLevel.get(key));
		System.out.println();
/*
		for(List<Student3> level : stuByLevel.values()) {
			System.out.println();
			for(Student3 s : level) {
				System.out.println(s);
			}
		}
*/	
		System.out.printf("%n4. 다중그룹화(학년별, 반별)");
		Map<Integer, Map<Integer, List<Student3>>> stuByHakAndBan =
			Stream.of(stuArr)
				  .collect(groupingBy(Student3::getHak,
						   groupingBy(Student3::getBan)
				   ));
		
		for(Map<Integer, List<Student3>> hak : stuByHakAndBan.values()) {
			for(List<Student3> ban : hak.values()) {
				System.out.println();
				for(Student3 s : ban)
					System.out.println(s);
			}
		}
		
		System.out.printf("%n5. 다중그룹화 + 통계(학년별, 반별 1등)%n");
		Map<Integer, Map<Integer, Student3>> topStuByHakAndBan =
			Stream.of(stuArr)
				  .collect(groupingBy(Student3::getHak,
						   groupingBy(Student3::getBan,
							   collectingAndThen(
								  maxBy(comparingInt(Student3::getScore))
								  , Optional::get
							   )
						    )
				   ));
		
		for(Map<Integer, Student3> ban : topStuByHakAndBan.values())
			for(Student3 s : ban.values())
				System.out.println(s);
		
		System.out.printf("%n6. 다중그룹화 + 통계(학년별, 반별 성적그룹)%n");
		Map<String, Set<Student3.Level>> stuBySocreGroup = Stream.of(stuArr)
			.collect(groupingBy(s -> s.getHak() + "-" + s.getBan(),
					mapping(s -> {
						if(s.getScore() >= 200) return Student3.Level.HIGH;
						else if(s.getScore() >= 100) return Student3.Level.MID;
						else return Student3.Level.LOW;
					}, toSet())
			));
		
		Set<String> keySet2 = stuBySocreGroup.keySet();
		
		for(String key : keySet2) {
			System.out.println("[" + key + "]" + stuBySocreGroup.get(key));
		}
	}	// main의 끝
}
```

```
1. 단순그룹화(반별로 분할)
[나자바, 남, 1학년, 1반, 300점]
[김지미, 여, 1학년, 1반, 250점]
[김자바, 남, 1학년, 1반, 200점]
[나자바, 남, 2학년, 1반, 300점]
[김지미, 여, 2학년, 1반, 250점]
[김자바, 남, 2학년, 1반, 200점]
[이지미, 여, 1학년, 2반, 150점]
[남자바, 남, 1학년, 2반, 100점]
[안지미, 여, 1학년, 2반,  50점]
[이지미, 여, 2학년, 2반, 150점]
[남자바, 남, 2학년, 2반, 100점]
[안지미, 여, 2학년, 2반,  50점]
[황지미, 여, 1학년, 3반, 100점]
[강지미, 여, 1학년, 3반, 150점]
[이자바, 남, 1학년, 3반, 200점]
[황지미, 여, 2학년, 3반, 100점]
[강지미, 여, 2학년, 3반, 150점]
[이자바, 남, 2학년, 3반, 200점]

2. 단순그룹화(성적별로 그룹화)
[HIGH]
[나자바, 남, 1학년, 1반, 300점]
[김지미, 여, 1학년, 1반, 250점]
[김자바, 남, 1학년, 1반, 200점]
[이자바, 남, 1학년, 3반, 200점]
[나자바, 남, 2학년, 1반, 300점]
[김지미, 여, 2학년, 1반, 250점]
[김자바, 남, 2학년, 1반, 200점]
[이자바, 남, 2학년, 3반, 200점]

[MID]
[이지미, 여, 1학년, 2반, 150점]
[남자바, 남, 1학년, 2반, 100점]
[황지미, 여, 1학년, 3반, 100점]
[강지미, 여, 1학년, 3반, 150점]
[이지미, 여, 2학년, 2반, 150점]
[남자바, 남, 2학년, 2반, 100점]
[황지미, 여, 2학년, 3반, 100점]
[강지미, 여, 2학년, 3반, 150점]

[LOW]
[안지미, 여, 1학년, 2반,  50점]
[안지미, 여, 2학년, 2반,  50점]


3. 단순그룹화 + 통계(성적별 학생수)
[HIGH] - 8명, [MID] - 8명, [LOW] - 2명, 

4. 다중그룹화(학년별, 반별)
[나자바, 남, 1학년, 1반, 300점]
[김지미, 여, 1학년, 1반, 250점]
[김자바, 남, 1학년, 1반, 200점]

[이지미, 여, 1학년, 2반, 150점]
[남자바, 남, 1학년, 2반, 100점]
[안지미, 여, 1학년, 2반,  50점]

[황지미, 여, 1학년, 3반, 100점]
[강지미, 여, 1학년, 3반, 150점]
[이자바, 남, 1학년, 3반, 200점]

[나자바, 남, 2학년, 1반, 300점]
[김지미, 여, 2학년, 1반, 250점]
[김자바, 남, 2학년, 1반, 200점]

[이지미, 여, 2학년, 2반, 150점]
[남자바, 남, 2학년, 2반, 100점]
[안지미, 여, 2학년, 2반,  50점]

[황지미, 여, 2학년, 3반, 100점]
[강지미, 여, 2학년, 3반, 150점]
[이자바, 남, 2학년, 3반, 200점]

5. 다중그룹화 + 통계(학년별, 반별 1등)
[나자바, 남, 1학년, 1반, 300점]
[이지미, 여, 1학년, 2반, 150점]
[이자바, 남, 1학년, 3반, 200점]
[나자바, 남, 2학년, 1반, 300점]
[이지미, 여, 2학년, 2반, 150점]
[이자바, 남, 2학년, 3반, 200점]

6. 다중그룹화 + 통계(학년별, 반별 성적그룹)
[1-1][HIGH]
[2-1][HIGH]
[1-2][MID, LOW]
[2-2][MID, LOW]
[1-3][HIGH, MID]
[2-3][HIGH, MID]
```