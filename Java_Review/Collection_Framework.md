Chapter 11. 컬렉션 프레임워크 Collection Framework

# 1. 컬렉션 프레임워크(Collection Framework)

컬렉션 프레임워크란, '데이터 군을 저장하는 클래스들을 표준화한 설계'를 뜻한다. 컬렉션(Collection)은 다수의 데이터, 즉 데이터 그룹을, 프레임워크은 표준화된 프로그래밍 방식을 의미한다.

</br>

## 1.1 컬렉션 프레임워크의 핵심 인터페이스

컬렉션 프레임워크에서는 컬렉션데이터 그룹을 크게 3가지 타입이 존재한다고 인식하고 각 컬렉션을 다루는데 필요한 기능을 가진 3개의 인터페이스를 정의하였다. 그리고 인터페이스 `List`와 `Set`의 공통된 부분을 다시 뽑아서 새로운 인터페이스인 `Collection`을 추가로 정의하였다.

![image](https://ifh.cc/g/9plRtw.png)

인터페이스 `List`와 `Set`을 구현한 컬렉션 클래스들을 서로 많은 공통부분이 있어서, 공통된 부분을 다시 뽑아 `Collection`인터페이스를 정의할 수 있었지만 `Map`인터페이스는 이들과는 전혀 다른 형태로 컬렉션을 다루기 때문에 같은 상속계층도에 포함되지 못했다.

> JDK1.5부터 Iterable인터페이스가 추가되고 이를 Collection인터페이스가 상속받도록 변경되었으나 이것은 단지 인터페이스들의 공통적인 메소드인 iterator()를 뽑아서 중복을 제거하기 위한 것에 불과하므로 상속계층도에서 별 의미가 없다.

![image](https://ifh.cc/g/yOhazt.png)

> 키(key)란, 데이터 집합 중에서 어떤 값(value)을 찾는데 열쇠(key)가 된다는 의미에서 붙여진 이름이다. 그래서 키(key)는 중복을 허용하지 않는다.

컬렉션 프레임워크의 모든 컬렉션 클래스들은 `List`, `Set`, `Map`중의 하나를 구현하고 있으며, 구현한 인터페이스의 이름이 클래스의 이름에 포함되어있어서 이름만으로도 클래스의 특징을 쉽게 알 수 있도록 되어있다.

`Vector`나 `HashTable`과 같은 기존의 컬렉션 클래스들은 호환을 위해, 설계를 변경해서 남겨두었지만 가능하면 사용하지 않는 것이 좋다. 그 대신 새로 추가된 `ArrayList`와 `HashMap`을 사용하는 것이 좋다.

![image](https://ifh.cc/g/H1bAAT.png)

</br>

### Collection인터페이스

`List`와 `Set`의 조상인 `Collection`인터페이스에는 다음과 같은 메소드들이 정의되어 있다.

![image](https://ifh.cc/g/PKnm9R.png)

`Collection`인터페이스는 컬렉션 클래스에 저장된 데이터를 읽고, 추가하고 삭제하는 등 컬렉션을 다루는데 가장 기본적인 메소드들을 정의하고 있다.

위의 표에서 반환 타입이 boolean인 메소드들은 작업을 성공하거나 사실이면 true를, 그렇지 않으면 false를 반환한다.

예를 들어 `boolean add(Object o)`를 사용해서 객체를 컬렉션을 추가할 때, 성공하면 true를, 실패하면 false를 반환한다. `boolean isEmpty()`를 사용해서 컬렉션에 포함된 객체가 없으면, 즉 컬렉션이 비어있으면 true를, 그렇지 않으면 false를 반환한다.

</br>

### List인터페이스

`List`인터페이스는 **중복을 허용**하면서 **저장순서가 유지**되는 컬렉션을 구현하는데 사용된다.

![image](https://ifh.cc/g/zWC3Jw.png)

`List`인터페이스에 정의된 메소드는 다음과 같다. `Collection`인터페이스로부터 상속받은 것들은 제외하였다.

![image](https://ifh.cc/g/vPmcF0.png)

</br>

### Set인터페이스

`Set`인터페이스는 중복을 허용하지 않고 저장순서가 유지되지 않는 컬렉션 클래스를 구현하는데 사용된다. `Set`인터페이스를 구현한 클래스로는 `HashSet`, `TreeSet` 등이 있다.

![image](https://ifh.cc/g/8szmks.png)

</br>

### Map인터페이스

`Map`인터페이스는 키(key)와 값(value)을 하나의 쌍으로 묶어서 저장하는 컬렉션 클래스를 구현하는 데 사용된다. 키는 중복될 수 없지만 값은 중복을 허용한다. 기존에 저장된 데이터와 중복된 키와 값을 저장하면 기존의 값은 없어지고 마지막에 저장된 값이 남게된다. `Map`인터페이스를 구현한 클래스로는 `Hashtable`, `HashMap`, `LinkedHashMap`, `SortedMap`, `TreeMap` 등이 있다.

> Map이란 개념은 어떤 두 값을 연결한다는 의미에서 붙여진 이름이다.

![image](https://ifh.cc/g/gtX5cY.png)

![image](https://ifh.cc/g/3fr96N.png)

`value()`에서는 반환타입이 `Colleciton`이고, `keySet()`에서는 반환타입이 `Set`이다. `Map`인터페이스에서 값(value)은 중복을 허용하기 때문에 `Collection`타입으로 반환하고, 키(key)는 중복을 허용하지 않기 때문에 `Set`타입으로 반환한다.

</br>

### Map.Entry인터페이스

`Map.Entry`인터페이스는 `Map`인터페이스의 내부 인터페이스이다. 내부 클래스와 같이 인터페이스도 인터페이스 안에 인터페이스를 정의하는 내부 인터페이스(inner interface)를 정의하는 것이 가능하다.

`Map`에 저장되는 key-value쌍을 다루기 위해 내부적으로 `Entry`인터페이스를 정의해 놓았다. 이것은 보다 객체지향적으로 설계하도록 유도하기 위한 것으로 `Map`인터페이스를 구현하는 클래스에서는 `Map.Entry`인터페이스도 함께 구현해야한다.

다음은 `Map`인터페이스의 소스코드의 일부이다.

``` java
public interface Map {
    ...
    public static interface Entry {
        Object getKey();
        Object getValue();
        Object setValue(Object value);
        boolean equals(Object o);
        int hashCode();
        ...                     // JDK1.8부터 추가된 메소드는 생략
    }
}
```

</br>

![image](https://ifh.cc/g/tg4dO2.png)