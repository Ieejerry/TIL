# Collections Framework

</br>

## 배열과 컬렉션즈 프레임워크

배열은 연관된 데이터를 관리하기 위한 수단이다. 그런데 배열에는 몇가지 불편한 점이 있었는데 그 중의 하나가 한번 정해진 배열의 크기를 변경할 수 없다는 점이다. 이러한 불편함을 컬렉션즈 프래임워크를 사용하면 줄어든다.

아래의 예를 보겠다.

``` java
package collection;
 
import java.util.ArrayList;	// ArrayList를 사용하기 위해선, java.util,ArrayList 패키지를 import 해야된다.
 
public class ArrayListDemo {
 
    public static void main(String[] args) {
        String[] arrayObj = new String[2];
        arrayObj[0] = "one";
        arrayObj[1] = "two";
        // arrayObj[2] = "three"; 오류가 발생한다.
        for(int i=0; i<arrayObj.length; i++){	// 배열은 배열 인스턴스의 length라는 속성값을 이용해서 배열의 길이를 알 수 있다.
            System.out.println(arrayObj[i]);	// 배열 같은 경우 배열 안의 값을 출력할 때, 배열 인스턴스뒤에 []안에 인덱스 값을 넣어 해당 인덱스의 값을 호출할 수 있다.
        }
         
        ArrayList al = new ArrayList();	// 배열과 다르게 ArrayList는 생성할 때, 길이를 지정할 필요가 없다. 
        al.add("one");	// ArrayList는 add()라는 인스턴스 메소드를 통해 ArrayList에 값을 추가할 수 있다.
        al.add("two");	// ArrayList의 add()라는 메소드는 어떠한 데이터 타입도 수용한다.
        al.add("three");    // add() 메소드에 인자들은 ArrayList에 저장될 때 Object 타입으로 저장이 된다.
        for(int i=0; i<al.size(); i++){	// ArrayList는 배열고 다르게 length가 아니라 size()라는 메소드를 사용해서 ArrayList의 길이를 알 수 있다.
            System.out.println(al.get(i));	// ArrayList 같은 경우 인스턴스 변수 뒤에 get()이라는 메소드에 인덱스를 인자로 전달해 해당 인덱스의 값을 호출할 수 있다.
        }
    }
 
}
```

아래 코드처럼 배열은 그 크기를 한번 지정하면 크기보다 많은 수의 값을 저장할 수 없다.

``` java
String[] arrayObj = new String[2];
arrayObj[0] = "one";
arrayObj[1] = "two";
// arrayObj[2] = "three"; 오류가 발생한다.
```

하지만 `ArrayList`는 크기를 미리 지정하지 않기 때문에 얼마든지 많은 수의 값을 저장할 수 있다.

``` java
ArrayList al = new ArrayList();	// 배열과 다르게 ArrayList는 생성할 때, 길이를 지정할 필요가 없다. 
    al.add("one");	// ArrayList는 add()라는 인스턴스 메소드를 통해 ArrayList에 값을 추가할 수 있다.
    al.add("two");  // ArrayList의 add()라는 메소드는 어떠한 데이터 타입도 수용한다.
    al.add("three");    // add() 메소드에 인자들은 ArrayList에 저장될 때 Object 타입으로 저장이 된다.
```

`ArrayList`는 배열과는 사용방법이 조금 다르다. 배열의 경우 값의 개수를 구할 때 `.length`를 사용했지만 `ArrayList`는 메소드 `size`를 사용한다. 또한, 특정한 값을 가져올 때 배열은 `[인덱스 번호]`를 사용했지만 컬렉션은 `.get(인덱스 번호)`를 사용한다.

``` java
for(int i=0; i<al.size(); i++){	// ArrayList는 배열고 다르게 length가 아니라 size()라는 메소드를 사용해서 ArrayList의 길이를 알 수 있다.
    System.out.println(al.get(i));	// ArrayList 같은 경우 인스턴스 변수 뒤에 get()이라는 메소드에 인덱스를 인자로 전달해 해당 인덱스의 값을 호출할 수 있다.
}
```

그런데 `ArrayList`를 사용할 때 주의할 점이 있다. 위의 반복문을 아래처럼 바꿔보겠다.

``` java
for(int i=0; i<al.size(); i++){
    String val = al.get(i); // ArrayList에 담긴 값들은 Object 타입으로 저장되기 때문에 String 타입의 val 변수에 담으려고 하니, 에러가 발생하게 된다.
    System.out.println(val);
}
```

위의 코드는 컴파일 오류가 발생한다. `ArrayList`의 메소드 `add`의 입장에서는 인자로 어떤 형태의 값이 올지 알 수 없다. 그렇기 때문에 모든 데이터 타입의 조상인 `Object` 형식으로 데이터를 받고 있다. 예를들면 아래와 같은 모습일 것이다. (실제와는 다르다)

``` java
public boolean add(Object e) {
```

따라서 `ArrayList` 내에서 `add`를 통해서 입력된 값은 `Object`의 데이터 타입을 가지고 있고, `get`을 이용해서 이를 꺼내도 `Object`의 데이터 타입을 가지고 있게 된다. 그래서 위의 코드는 아래와 같이 바꿔야 한다.

``` java
for(int i=0; i<al.size(); i++){
    String val = (String)al.get(i); // al.get(i)잎에 (String)을 넣어줘서 Object 타입을 String으로 형변환 해주면 에러가 사라지게 된다.
    System.out.println(val);
}
```

`get`의 리턴값을 문자열로 형변환하고 있다. 원래의 데이터 타입이 된 것이다.

그런데 위의 방식은 예전의 방식이다. 이제는 아래와 같이 제네릭을 사용해야 한다.

``` java
ArrayList<String> al = new ArrayList<String>(); // al이라는 ArrayList에 제네릭을 통해 ArrayList에 들어오는 값을 String 데이터타입이 되도록 지정을 함
al.add("one");
al.add("two");
al.add("three");
for(int i=0; i<al.size(); i++){
    String val = al.get(i); // get() 메소드를 통해 호출한 값을 String으로 형변환 하지 않아도 된다. 제네릭을 통해 String 데이터 타입으로 저장이 되기 때문에 String 데이터 타입으로 호출이 된다.
    System.out.println(val);
}
```

제네릭을 사용하면 `ArrayList` 내에서 사용할 데이터 타입을 인스턴스를 생성할 때 지정할 수 있기 때문에 데이터를 꺼낼 때 `(String val = al.get(i);)` 형변환을 하지 않아도 된다.

</br>

## 컬렉션즈 프래임워크란?

컬렉션즈 프래임워크가 무엇인가 본격적으로 알아보겠다. 컬렉션즈 프래임워크라는 것은 다른 말로는 컨테이너라고도 부른다. 즉 값을 담는 그릇이라는 의미이다. 그런데 그 값의 성격에 따라서 컨테이너의 성격이 조금씩 달라진다. 자바에서는 다양한 상황에서 사용할 수 있는 다양한 컨테이너를 제공하는데 이것을 컬렉션즈 프래임워크라고 부른다. `ArrayList`는 그중의 하나다.

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/516/2154.png)

위의 그림은 컬렉션즈 프래임워크의 구성을 보여준다. `Collection`과 `Map`이라는 최상위 카테고리가 있고, 그 아래에 다양한 컬렉션들이 존재한다. 그럼 구체적인 컬렉션즈 프래임워크 클래스들을 살펴보겠다.

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/516/2160.png)

`ArrayList`는 `Collection-List`에 속해있다. `ArrayList`는 `LIst`라는 성격으로 분류되고 있는 것이다. `List`는 인터페이스이다. 그리고 `List` 하위의 클래스들은 모두 `List` 인터페이스를 구현하기 때문에 모두 같은 API를 가지고 있다. 클래스의 취지에 따라서 구현방법과 동작방법은 다르지만 공통의 조작방법을 가지고 있는 것이다. 익숙한 `ArrayList`를 바탕으로 나머지 컬렉션들의 성격을 파악해보겠다.

`List`와 `Set`의 차이점은 `List`는 중복을 허용하고, `Set`은 허용하지 않는다.

``` java
package collection;
 
import java.util.ArrayList;	// ArrayList 컨테이너를 사용하기 위해 java.util.ArrayList 패키지 import
import java.util.HashSet;	// HashSet 컨테이너를 사용하기 위해 java.util.HashSet 패키지 import
 
import java.util.Iterator;
 
public class ListSetDemo {
 
    public static void main(String[] args) {
        ArrayList<String> al = new ArrayList<String>();	// ArrayList 컨테이너를 al 변수에 인스턴스하고, al ArrayList에는 제네릭을 통해 String 데이터 타입의 값을 담을 것이란 것을 지정
        al.add("one");	// Array은 add()라는 메소드 인자에 값을 할당해 추가할 수 있다.
        al.add("two");
        al.add("two");
        al.add("three");
        al.add("three");
        al.add("five");
        System.out.println("array");
        // iterator는 반복자라는 뜻을 가진다.
        Iterator ai = al.iterator();	// iterator() 메소드를 호출하게 되면, Iterator라는 데이터 타입을 가진 인스턴스를 반환하고, 그 인스턴스를 변수 al에 할당
        while(ai.hasNext()){	// ai 인스턴스는 메소드를 호출한 al 인스턴스의 원소들을 갖게 되고, hasNext() 메소드는 ai 인스턴스에 원소가 존재하는지 확인
            System.out.println(ai.next());	// next() 메소드는 ai 인스턴스 안의 원소중에 하나를 반환하고 없앤다. (이 때, ai 인스턴스의 원소를 없애는 것이지, 오리지널 al 인스턴스의 원소를 없애는 것이 아니다.)
        }
        // List는 값의 중복을 허용한다.
        // List는 순서가 보장된다.
         
        HashSet<String> hs = new HashSet<String>();	// HashSet 컨테이너를 hs 변수에 인스턴스하고, hs HashSet에는 제네릭을 통해 String 데이터 타입의 값을 담을 것이란 것을 지정
        hs.add("one");	// HashSet은 add()라는 메소드 인자에 값을 할당해 추가할 수 있다.
        hs.add("two");
        hs.add("two");
        hs.add("three");
        hs.add("three");
        hs.add("five");
        Iterator hi = hs.iterator();
        System.out.println("\nhashset");
        while(hi.hasNext()){
            System.out.println(hi.next());
        }
        // Set은 값의 중복을 허용하지 않는다.
        // 순서가 보장되지 않는다.
    }
 
}
```

결과는 아래와 같다.

``` java
array
one
two
two
three
three
five
 
hashset
two
five
one
three
```

우선 값을 가져오는 방법이 조금 달라졌다. (`ArrayList`에서도 이 방법을 사용할 수 있다)

``` java
// iterator는 반복자라는 뜻을 가진다.
Iterator ai = al.iterator();	// iterator() 메소드를 호출하게 되면, Iterator라는 데이터 타입을 가진 인스턴스를 반환하고, 그 인스턴스를 변수 al에 할당
while(ai.hasNext()){	// ai 인스턴스는 메소드를 호출한 al 인스턴스의 원소들을 갖게 되고, hasNext() 메소드는 ai 인스턴스에 원소가 존재하는지 확인
    System.out.println(ai.next());	// next() 메소드는 ai 인스턴스 안의 원소중에 하나를 반환하고 없앤다. (이 때, ai 인스턴스의 원소를 없애는 것이지, 오리지널 al 인스턴스의 원소를 없애는 것이 아니다.)
}
```

메소드 `iterator`는 인터페이스 `Collection`에 정의되어 있다. 따라서 `Collection`을 구현하고 있는 모든 컬렉션즈 프레임웍크는 이 메소드를 구현하고 있음을 보증한다. 메소드 `iterator`의 호출 결과는 인터페이스 `iterator`를 구현한 객체를 리턴한다. 인터페이스 `iterator`는 아래 3개의 메소드를 구현하도록 강제하고 있는데 각각의 역할은 아래와 같다.

- hasNext   
반복할 데이터가 더 있으면 true, 더 이상 반복할 데이터가 없다면 false를 리턴한다.
- next   
hasNext가 true라는 것은 next가 리턴할 데이터가 존재한다는 의미다. 

이러한 기능을 조합하면 `for` 문을 이용하는 것과 동일하게 데이터를 순차적으로 처리할 수 있다.

`Set`과 `List`의 차이를 짚어보겠다. 위의 결과를 통해서 알 수 있는 것처럼 `Set`는 중복을 허용하지 않고 순서가 없지만, `List`는 중복을 허용하고 저장되는 순서가 유지된다는 것을 알 수 있다. 이러한 특징을 고려해서 컬렉션을 선택해야 한다. 그럼 `Set`에 대해서 조금 더 알아보겠다.

</br>

## Set

`Set`은 한국어로 집합이라는 뜻이다. 여기서의 집합이란 수학의 집합과 같은 의미다. 수학에서의 집합도 순서가 없고 중복되지 않는 특성이 있다. 수학에서 집합은 교집합(intersect), 차집합(difference), 합집합(union)과 같은 연산을 할 수 있다. `Set`도 마찬가지다.

아래와 같이 3개의 집합 `hs1`, `hs2`, `hs3`이 있다. `h1`은 숫자 1,2,3으로 이루어진 집합이고, `h2`는 3,4,5 `h3`는 1,2로 구성되어 있다. `set`의 API를 이용해서 집합 연산을 해보겠다.

``` java
package collection;
 
import java.util.HashSet;
 
import java.util.Iterator;
 
public class SetDemo {
 
    public static void main(String[] args) {
        HashSet<Integer> A = new HashSet<Integer>();
        A.add(1);
        A.add(2);
        A.add(3);
         
        HashSet<Integer> B = new HashSet<Integer>();
        B.add(3);
        B.add(4);
        B.add(5);
         
        HashSet<Integer> C = new HashSet<Integer>();
        C.add(1);
        C.add(2);
         
        System.out.println(A.containsAll(B)); // false
        // containsAll() 메소드는 인자 Set이 인스턴스 Set의 부분집합인지를 boolean형으로 반환한다.
        System.out.println(A.containsAll(C)); // true
         
        //A.addAll(B);	// 인스턴스 Set과 인자 Set의 합집합
        //A.retainAll(B);	// 인스턴스 Set과 인자 Set의 교집합
        //A.removeAll(B);	// 인스턴스 Set에 인자 Set의 차집합
         
        Iterator hi = A.iterator();
        while(hi.hasNext()){
            System.out.println(hi.next());
        }
    }
 
}
```

### 부분집합 (subset)

``` java
System.out.println(A.containsAll(B)); // false
// containsAll() 메소드는 인자 Set이 인스턴스 Set의 부분집합인지를 boolean형으로 반환한다.
System.out.println(A.containsAll(C)); // true
```

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/516/2155.png)

### 합집합(union)

``` java
A.addAll(B);	// 인스턴스 Set과 인자 Set의 합집합
```

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/516/2156.png)

### 교집합(intersect)

``` java
A.retainAll(B);	// 인스턴스 Set과 인자 Set의 교집합
```

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/516/2157.png)

### 차집합(difference)

``` java
A.removeAll(B);	// 인스턴스 Set에 인자 Set의 차집합
```

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/516/2158.png)

</br>

## Map

이번에는 `Map` 컬렉션에 대해서 알아보겠다. `Map` 컬렉션은 `key`와 `value`의 쌍으로 값을 저장하는 컬렉션이다. 아래 코드를 보겠다.

``` java
package collection;
 
import java.util.*;
 
public class MapDemo {
 
    public static void main(String[] args) {
        HashMap<String, Integer> a = new HashMap<String, Integer>();	// Map 같은 경우에는 key와 value 두 개의 값을 가지기 때문에 제네릭으로 두 개의 데이터 타입을 지정해주어야 된다.
        a.put("one", 1);	// put() 메소드는 Collection 인터페이스에는 존재하지 않고, Map 인터페이스에만 존재하는 메소드이다.
        a.put("two", 2);	// put() 메소드는 두 개의 인자를 받는데, 첫번째 인자로는 key값을 두번째 인자로는 value값을 받는다.
        a.put("three", 3);
        a.put("four", 4);
        System.out.println(a.get("one"));	// Map에서 get() 메소드를 사용할 떄에는 인자로 key값을 주면, 그 key값에 해당하는 value값을 반환하게 된다.
        System.out.println(a.get("two"));
        System.out.println(a.get("three"));
         
        iteratorUsingForEach(a);
        iteratorUsingIterator(a);
    }
     
    static void iteratorUsingForEach(HashMap map){
        Set<Map.Entry<String, Integer>> entries = map.entrySet();	// Map 인터페이스에 있는 entrySet() 메소드를 호출하면 Set 데이터 타입을 가진 객체가 반환되고, 그 객체를 entries라는 변수에 담는다.
        // Set 객체 안에는 Map 안에 있는 값들이 Map.Entry라는 객체로 담긴다. 첫번째 제네릭 데이터 타입은 getKey() 메소드가 가지는 데이터 타입이고, 두번째 제네릭 데이터 타입은 getValue() 메소드가 가지는 데이터 타입이다.
        for (Map.Entry<String, Integer> entry : entries) {	// for-each문을 통해서 entries라는 변수에 담긴 Set 객체안에 Map.Entry 객체들을 하니씩 꺼내 entry라는 변수에 담는다.
            System.out.println(entry.getKey() + " : " + entry.getValue());	// entry 변수에 담긴 Map.Entry 객체를 getKey() 메소드를 통해 key값을 호출하고, getValue() 통해 value값을 호출한다.
        }
    }
     
    static void iteratorUsingIterator(HashMap map){
        Set<Map.Entry<String, Integer>> entries = map.entrySet();	// Map 인터페이스에 있는 entrySet() 메소드를 호출하면 Set 데이터 타입을 가진 객체가 반환되고, 그 객체를 entries라는 변수에 담는다.
        Iterator<Map.Entry<String, Integer>> i = entries.iterator();	// Map.Entry가 담긴 Set 객체를 iterator() 메소드를 활용하여 얻은 반복자를 i 변수에 할당
        while(i.hasNext()){	// hasNext()를 통해 i 객체에 호출할 데이터가 있는지 조회
            Map.Entry<String, Integer> entry = i.next();	// next()를 통해 Set 객체에 있는 Map.Entry 객체를 하나씩 entry라는 변수 담고 없앤다.
            System.out.println(entry.getKey()+" : "+entry.getValue());	// entry 변수에 담긴 Map.Entry 객체를 getKey() 메소드를 통해 Key값을 호출하고, getValue()라는 메소드를 통해 value값을 호출한다.
        }
    }
 
}
```

`Map`에서 데이터를 추가할 때 사용하는 API는 `put`이다. `put`의 첫번째 인자는 값의 `key`이고, 두번째 인자는 `key`에대한 값이다. `key`를 이용해서 값을 가져올 수 있다.

`Map`에서 `key`의 값은 중복이 되지 않지만, `value`의 값은 중복이 가능하다. 만약 이미 등록되어 있는 `key`와 같은 값을 가진 `key`와 새로운 `value`를 추가해주게 되면 이미 등록되어 있던 `key`의 `value`값이 새로운 `value`값으로 바뀌게 된다.

``` java
a.put("one", 1);	// put() 메소드는 Collection 인터페이스에는 존재하지 않고, Map 인터페이스에만 존재하는 메소드이다.
a.put("two", 2);	// put() 메소드는 두 개의 인자를 받는데, 첫번째 인자로는 key값을 두번째 인자로는 value값을 받는다.
```

이것이 `Map`의 가장 기본적인 사용법이다. 그럼 `Map`에 저장된 데이터를 열거할 때는 어떻게 해야되는지 알아보겠다.

``` java
Set<Map.Entry<String, Integer>> entries = map.entrySet();	// Map 인터페이스에 있는 entrySet() 메소드를 호출하면 Set 데이터 타입을 가진 객체가 반환되고, 그 객체를 entries라는 변수에 담는다.
// Set 객체 안에는 Map 안에 있는 값들이 Map.Entry라는 객체로 담긴다. 첫번째 제네릭 데이터 타입은 getKey() 메소드가 가지는 데이터 타입이고, 두번째 제네릭 데이터 타입은 getValue() 메소드가 가지는 데이터 타입이다.
for (Map.Entry<String, Integer> entry : entries) {	// for-each문을 통해서 entries라는 변수에 담긴 Set 객체안에 Map.Entry 객체들을 하니씩 꺼내 entry라는 변수에 담는다.
    System.out.println(entry.getKey() + " : " + entry.getValue());	// entry 변수에 담긴 Map.Entry 객체를 getKey() 메소드를 통해 key값을 호출하고, getValue() 통해 value값을 호출한다.
}
```

메소드 `entrySet`은 `Map`의 데이터를 담고 있는 `Set`을 반환한다. 반환한 `Set`의 값이 사용할 데이터 타입은 `Map.Entry`이다. `Map.Entry`는 [인터페이스](https://docs.oracle.com/javase/7/docs/api/java/util/Map.Entry.html)인데 아래와 같은 API를 가지고 있다.

- getKey
- getValue

위의 API를 이용해서 `Map`의 `key`, `value`를 조회할 수 있다.

`Set`은 수학의 집합을 프로그래밍적으로 구현한 것이다. `map`은 수학의 함수를 프로그래밍화한 것이다. 수학의 함수가 "정의역과 공역 원소들 사이의 단가 대응의 관계"라는 의미를 이해하고 있는 사람이라면 `Map`의 `key`와 `value`의 관계가 함수의 정의역과 공역의 관계와 같다는 것을 이해할 수 있다.

</br>

## 데이터 타입의 교체

컬렉션을 사용할 때는 데이터 타입은 가급적 해당 컬렉션을 대표하는 인터페이스를 사용하는 것이 좋다. 이전 예제의 12행의 내용은 아래와 같다.

``` java
HashMap<String, Integer> a = new HashMap<String, Integer>();
```

이것을 아래와 같이 수정하겠다. `HashMap`은 `Map` 인터페이스를 구현하기 때문에 변수 `a`의 데이터 타입으로 `Map`을 사용할 수 있다.

``` java
Map<String, Integer> a = new HashMap<String, Integer>();
```

어떤 필요에 의해서 컬렉션을 `HashMap`에서 `HashTable`로 바꾸고 싶다면 아래와 같이 수정하면 된다.

``` java
Map<String, Integer> a = new Hashtable<String, Integer>();
```

</br>

## 정렬

컬렉션을 사용하는 이유 중의 하나는 정렬과 같은 데이터와 관련된 작업을 하기 위해서다. 정렬하는 법을 알아보겠다. 패키지 [java.util 내에는 Collections](http://docs.oracle.com/javase/7/docs/api/java/util/Collections.html)라는 클래스가 있다. 이 클래스를 사용하는 법을 알아보겠다.

``` java
package collection;
 
import java.util.*;
 
class Computer implements Comparable{	// Collections 클래스의 sort() 메소드를 사용하려면 List안에 그 객체들은 Comparable 인터페이스를 구현하고 있어야 한다.
    int serial;	// 전역변수 int형의 serial 선언
    String owner;	// 전역변수 String형의 owner 선언
    Computer(int serial, String owner){	// 첫번째 매개변수로 int형을 두번째 매개변수로 String형을 받는 생성자 정의
        this.serial = serial;	// 생성자를 통해 전달된 첫번째 인자를 serial 전역변수에 할당
        this.owner = owner;	// 생성자를 통해 전달된 두번째 인자를 owner 전역변수에 할당
    }
    public int compareTo(Object o) {	// Comparable 인터페이스는 compareTo(Object o)를 구현하게 강제 되어있다.
        return this.serial - ((Computer)o).serial;	// 각 객체의 serial값을 비교하여, 선후 관계를 판별하여 정렬한다.
    }
    public String toString(){	// String형을 반환하는 toString() 메소드 정의
        return serial+" "+owner;	// 메소드 호출시 serial값과 owner값 반환
    }
}
 
public class CollectionsDemo {
     
    public static void main(String[] args) {
        List<Computer> computers = new ArrayList<Computer>();	// Computer 데이터 타입의 값을 받는 List 데이터 타입의 ArrayList를 인스턴스 
        computers.add(new Computer(500, "egoing"));	// add() 메소드 안에서 Computer 인스턴스 생성 serial = 500, owner = egoing
        computers.add(new Computer(200, "leezche"));	// 생성된 객체들을 ArrayList에 담음
        computers.add(new Computer(3233, "graphittie"));
        Iterator i = computers.iterator();
        System.out.println("before");
        while(i.hasNext()){	// while문을 통해 computers에 담긴 객체 출력
            System.out.println(i.next());
        }
        Collections.sort(computers);	// Collections 클래스의 sort()라는 메소드에 List를 인자로 전달하면 List를 정렬해준다.
        System.out.println("\nafter");
        i = computers.iterator();
        while(i.hasNext()){	// while문을 통해 정렬한 computers에 담긴 객체 출력
            System.out.println(i.next());
        }
    }
 
}
```

결과

``` java
before
500 egoing
200 leezche
3233 graphittie
 
after
200 leezche
500 egoing
3233 graphittie
```

클래스 `Collectors`는 [다양한 클래스 메소드](https://docs.oracle.com/javase/7/docs/api/java/util/Collections.html#sort%28java.util.List%29)를 가지고 있다. 메소드 `sort`는 그 중의 하나로 `List`의 정렬을 수행한다. 다음은 `sort`의 시그니처다.

_public static <T extends [Comparable](https://docs.oracle.com/javase/7/docs/api/java/lang/Comparable.html)<? super T>> void sort([List](https://docs.oracle.com/javase/7/docs/api/java/util/List.html)<T> list)_

`sort`의 인자인 `list`는 데이터 타입이 `List`이다. 즉 메소드 `sort`는 `List` 형식의 컬렉션을 지원한다는 것을 알 수 있다. 인자 `list`의 제네릭 `<T>`는 `coparable`을 `extends` 하고 있어야 한다. `Comparable`은 인터페이스인데 이를 구현하고 있는 클래스는 아래 메소드를 가지고 있어야 한다.

- [compareTo(T o)](https://docs.oracle.com/javase/7/docs/api/java/lang/Comparable.html)

아래의 메소드는 이러한 제약 조건을 준수하기 위해서 구현한 메소드다.

``` java
public int compareTo(Object o) {	// Comparable 인터페이스는 compareTo(Object o)를 구현하게 강제 되어있다.
    return this.serial - ((Computer)o).serial;	// 각 객체의 serial값을 비교하여, 선후 관계를 판별하여 정렬한다.
}
```

메소드 `sort`를 실행하면 내부적으로 `compareTo`를 실행하고 그 결과에 따라서 객체의 선후 관계를 판별하게 된다.

컬렉션즈 프레임워크는 효율적인 에플리케이션을 구축하기 위해서 매우 중요한 내용이다. 그런데 컬렉션은 단순히 사용법을 이해하는 것으로는 부족하고, 소위 알고리즘이나 자료구조(data structure)라고 불리는 분야에 대한 충분한 이해가 필요하다. 컬렉션즈 프레임워크는 이러한 분야의 성취를 누구나 쉽게 사용할 수 있도록 제공되는 일종의 라이브러리라고 할 수 있기 때문이다.

</br>

## 참조

- [Collections Framework Class diagram (backup)](https://prashantgaurav1.files.wordpress.com/2013/12/java-util-collection.gif)