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

</br>

## 1.2 ArrayList

`ArrayList`는 컬렉션 프레임워크에서 가장 많이 사용되는 컬렉션 클래스이다. 이 `ArrayList`는 `List`인터페이스를 구현하기 때문에 데이터의 저장순서가 유지되고 중복을 허용한다는 특징을 갖는다.

`ArrayList`는 기존의 `Vector`를 개선한 것으로 `Vector`와 구현원리와 기능적인 측면에서 동일하다고 할 수 있다. `Vector`는 기존에 작성된 소스와의 호환성을 위해서 계속 남겨두고 있을 뿐이기 때문에 가능하면 `Vector`보다 `ArrayList`를 사용하는 것이 좋다.

`ArrayList`는 `Object`배열을 이용해서 데이터를 순차적으로 저장한다. 예를 들면, 첫 번째로 저장한 객체는 `Object`배열의 0번째 위치에 저장되고 그 다음에 저장하는 개체는 1번째 위치에 저장된다. 이런 식으로 계속 배열에 순서대로 저장되며, 배열에 더 이상 저장할 공간이 없으면 보다 큰 새로운 배열을 생성해서 기존의 배열에 저장된 내용을 새로운 배열로 복사한 다음에 저장된다.

``` java
public class ArrayList extends AbstractList implements List, RandomAccess, Clonable, java.io.Serializable {
        ...
    transient Object[] elementData; // Object배열
        ...
}
```

> transient는 직렬화(serialization)와 관련된 제어자이다.

위의 코드는 `ArrayList`의 소스코드 일부인데 `ArrayList`는 `elementData`라는 이름의 `Object`배열을 멤버변수로 선언하고 있다는 것을 알 수 있다. 선언된 배열의 타입이 모든 객체의 최고조상인 `Object`이기 때문에 모든 종류의 객체를 담을 수 있다.

![image](https://ifh.cc/g/JST7Df.png)

</br>

예제 11-1 / ch11 / ArrayListEx1.java

``` java
import java.util.*;

public class ArrayListEx1 {
	public static void main(String[] args) {
		ArrayList list1 = new ArrayList(10);
		list1.add(new Integer(5));
		list1.add(new Integer(4));
		list1.add(new Integer(2));
		list1.add(new Integer(0));
		list1.add(new Integer(1));
		list1.add(new Integer(3));
	
		ArrayList list2 = new ArrayList(list1.subList(1, 4));
		print(list1, list2);
		
		Collections.sort(list1);	// list1과 list2를 정렬한다.
		Collections.sort(list2);	// Collections.sort(list 1)
		print(list1, list2);
		
		System.out.println("list1.containsAll(list2) : " + list1.containsAll(list2));
		
		list2.add("B");
		list2.add("c");
		list2.add(3, "A");
		print(list1, list2);
		
		list2.set(3, "AA");
		print(list1, list2);
		
		// list1에서 list2와 겹치는 부분만 남기고 나머지는 삭제한다.
		System.out.println("list1.retainAll(list2) : " + list1.retainAll(list2));
		print(list1, list2);
		
		// list2에서 list1에 포함된 객체를 삭제한다.
		for(int i = list2.size() - 1; i >= 0; i--) {
			if(list1.contains(list2.get(i)))
				list2.remove(i);
		}
		print(list1, list2);
	}	// main의 끝
	
	static void print(ArrayList list1, ArrayList list2) {
		System.out.println("list1 : " + list1);
		System.out.println("list2 : " + list2);
		System.out.println();
	}
}
```

```
list1 : [5, 4, 2, 0, 1, 3]
list2 : [4, 2, 0]

list1 : [0, 1, 2, 3, 4, 5] ← Collections.sort(List l)를 이용해서 정렬하였다.
list2 : [0, 2, 4]

list1.containsAll(list2) : true ← list1이 list2의 모든 요소를 포함하고 있을 때만 true
list1 : [0, 1, 2, 3, 4, 5]
list2 : [0, 2, 4, A, B, c] ← add(Object obj)를 이용해서 새로운 객체를 저장하였다.

list1 : [0, 1, 2, 3, 4, 5]
list2 : [0, 2, 4, AA, B, c] ← set(int index, Object obj)를 이용해서 다른 객체로 변경

list1.retainAll(list2) : true ← retainAll에 의해 list1에 변화가 있었으므로 true를 반환
list1 : [0, 2, 4] ← list2와의 공통요소 이외에는 모두 삭제되었다.(변화가 있었다)
list2 : [0, 2, 4, AA, B, c]

list1 : [0, 2, 4]
list2 : [AA, B, c]
```

위의 예제는 `ArrayList`의 기본적인 메소드를 이용해서 객체를 다루는 방법을 보여 준다. `ArrayList`는 `List`인터페이스를 구현했기 때문에 저장된 순서를 유지한다는 것을 알 수 있다. 그리고 `Collections`클래스의 `sort`메소드를 이용해서 `ArrayList`에 저장된 객체들을 정렬했다.

``` java
for(int i = list2.size(); i >= 0; i--) {
    if(list1.contains(list2.get(i)))
        list2.remove();
}
```

이 예제에서 한 가지 설명할 것은 위의 코드인데, `list2`에서 `list1`과 공통되는 요소들을 찾아서 삭제하는 부분이다.

여기에서는 `list2`의 각 요소를 접근하기 위해 `get(int index)`메소드와 for문을 사용하였는데, for문의 변수 `i`를 0 부터 증가시킨 것이 아니라, `list2.size()-1`부터 감소시키면서 거꾸로 반복시켰다.

만일 변수 `i`를 증가시켜가면서 삭제하면, 한 요소가 삭제될 때마다 빈 공간을 채우기 위해 나머지 요소들이 자리이동을 하기 때문에 올바른 결과를 얻을 수 없다. 그래서 제어변수를 감소시켜가면서 삭제를 해야 자리이동이 발생해도 영향을 받지 않고 작업이 가능하다.

</br>

예제 11-2 / ch11 / ArrayListEx2.java

``` java
import java.util.*;

public class ArrayListEx2 {
	public static void main(String[] args) {
		final int LIMIT = 10;	// 자르고자 하는 글자의 개수를 저장한다.
		String source = "0123456789abcdefghijABCDEFGHIJ!@#$%^&*()ZZZ";
		int length = source.length();
		
		List list = new ArrayList(length/LIMIT + 10);	// 크기를 약간 여유 있게 잡는다.
		
		for(int i = 0; i < length; i+=LIMIT) {
			if(i+LIMIT < length)
				list.add(source.substring(i, i+LIMIT));
			else
				list.add(source.substring(i));
		}
		
		for(int i = 0; i < list.size(); i++) {
			System.out.println(list.get(i));
		}
	}	// main
}
```

```
0123456789
abcdefghij
ABCDEFGHIJ
!@#$%^&*()
ZZZ
```

긴 문자열 데이터를 원하는 길이로 잘라서 `ArrayList`에 담은 다음 출력하는 예제이다. 단순히 문자열을 특정크기로 잘라서 출력할 것이라면, `charAt(int i)`와 for문을 이용하면 되겠지만 `ArrayList`에 잘라서 담아놓음으로써 `ArrayList`의 기능을 이용해서 다양한 작업을 간단하게 처리할 수 있다.

``` java
List list = new ArrayList(length/LIMIT+10); // 크기를 약간 여유 있게 잡는다.
```

`ArrayList`를 생성할 때, 저장할 요소의 개수를 고려해서 실제 저장할 개수보다 약간 여유있는 크기로 하는 것이 좋다. 생성할 때 지정한 크기보다 더 많은 객체를 저장하면 자동적으로 늘어나기는 하지만 이 과정에서 처리시간이 많이 소요되기 때문이다.

</br>

예제 11-3 / ch10 / VectorEx1.java

``` java
import java.util.*;

public class VectorEx1 {
	public static void main(String[] args) {
		Vector v = new Vector(5);	// 용량(capacity)이 5인 Vector를 생성한다.
		v.add("1");
		v.add("2");
		v.add("3");
		print(v);
		
		v.trimToSize();	// 빈 공간을 없앤다.(용량과 크기가 같아진다.)
		System.out.println("=== After trimToSize() ===");
		print(v);
		
		v.ensureCapacity(6);
		System.out.println("=== After ensureCapacity(6) ===");
		print(v);
		
		v.setSize(7);
		System.out.println("=== After setSize(7) ===");
		print(v);
		
		v.clear();
		System.out.println("=== After clear() ===");
		print(v);
	}
	
	public static void print(Vector v) {
		System.out.println(v);
		System.out.println("size : " + v.size());
		System.out.println("capacity : " + v.capacity());
	}
}
```

```
[1, 2, 3]
size : 3
capacity : 5
=== After trimToSize() ===
[1, 2, 3]
size : 3
capacity : 3
=== After ensureCapacity(6) ===
[1, 2, 3]
size : 3
capacity : 6
=== After setSize(7) ===
[1, 2, 3, null, null, null, null]
size : 7
capacity : 12
=== After clear() ===
[]
size : 0
capacity : 12
```

이 예젠ㄴ `Vector`의 용량(capacity)과 크기(size)에 관한 것인데, 각 실행과정을 그림과 같이 함께 단계별로 살펴보겠다.

1. 다음 capacity가 5인 Vector인스턴스 v를 생성하고, 3개의 객체를 저장한 후의 상태를 그림으로 나타낸 것이다.

![image](https://ifh.cc/g/dcpl9V.png)

2. v.trimToSize()를 호출하면 v의 빈 공간을 없애서 size와 capacity를 같게 한다. 배열은 크기를 변경할 수 없기 때문에 새로운 배열을 생성해서 그 주소값을 변수 v에 할당한다. 기존의 Vector인스턴스는 더 이상 사용할 수 없으며, 후에 가비지컬렉터(garbage collector)에 의해서 메모리에서 제거된다.

![image](https://ifh.cc/g/0vdsOQ.png)

3. v.ensureCapacity(6)는 v의 capacity가 최소한 6이 되도록 한다. 만일 v의 capacity가 6이상이라면 아무 일도 일어나지 않는다. 현재는 v의 capacity가 3이므로 크기가 6인 배열을 생성해서 v의 내용을 복사했다. 기존의 인스턴스를 다시 사용하는 것이 아니라 새로운 인스턴스를 생성한다.

![image](https://ifh.cc/g/fnyxD6.png)

4. v.setSize(7)는 v의 size가 7이 되도록 한다. 만일 v의 capacity가 충분하면 새로 인스턴스를 생성하지 않아도 되지만 지금은 capacity가 6이므로 새로운 인스턴스를 생성해야한다. Vector는 capacity가 부족할 경우 자동적으로 기존의 크기보다 2배의 크기로 증가된다. 그래서 v의 capacity는 12가 된다.

> 생성자 Vector(int initialCapacity, int capacityIncrement)를 사용해서 인스턴스를 생성한 경우에는 지정해준 capacityIncrement만큼 증가하게 된다.

![image](https://ifh.cc/g/LmN0xS.png)

5. v.clear();는 v의 모든 요소를 삭제한다. 아래의 왼쪽그림의 상태에서 오른쪽 그림과 같은 상태가 되는 것이다.

![image](https://ifh.cc/g/WX3raH.png)

`ArrayList`나 `Vector` 같이 배열을 이용한 자료구조는 데이터를 읽어오고 저장하는 데는 효율이 좋지만, 용량을 변경해야할 때는 새로운 배열을 생성한 후 기존의 배열로부터 새로 생성된 배열로 데이터를 복사해야하기 때문에 상당히 효율이 떨어진다는 단점을 가지고 있다. 그래서 처음에 인스턴스를 생성할 때, 저장할 데이터의 개수를 잘 고려하여 충분한 용량의 인스턴스를 생성하는 것이 좋다.

다음의 예제는 `Vector`클래스의 실제코드를 바탕으로 이해하기 쉽게 재구성한 것이다.

</br>

예제 11-4 / ch11 / MyVector.java

``` java
import java.util.*;
import java.util.function.UnaryOperator;

public class MyVector implements List {
	Object[] data = null;	// 객체를 담기 위한 객체배열을 선언한다.
	int capacity = 0;		// 용량
	int size = 0;			// 크기
	
	public MyVector(int capacity) {
		if(capacity < 0) {
			throw new IllegalArgumentException("유효하지 않은 값입니다. : " + capacity);
		}
		this.capacity = capacity;
		data = new Object[capacity];
	}
	
	public MyVector() {
		this(10);	// 크기를 지정하지 않으면 크기를 10으로 한다.
	}
	
	// 최소한의 저장공간(capacity)를 확보한ㄴ 메소드
	public void ensureCapacity(int minCapacity) {
		if(minCapacity - data.length > 0)
			setCapacity(minCapacity);
	}
	
	public boolean add(Object obj) {
		// 새로운 객체를 저장하기 전에 저장할 공간을 확보한다.
		ensureCapacity(size+1);
		data[size++] = obj;
		return true;
	}
	
	public Object get(int index) {
		if(index < 0 || index >= size)
			throw new IndexOutOfBoundsException("범위를 벗어났습니다.");
		return data[index];
	}
	
	public Object remove(int index) {
		Object oldObj = null;
		
		if(index < 0 || index >= size)
			throw new IndexOutOfBoundsException("범위를 벗어났습니다.");
		oldObj = data[index];
		
		// 삭제하고자 하는 객체가 마지막 객체가 아니라면, 배열복사를 통해 빈자리를 채워줘야 한다.
		if(index != size-1) {
			System.arraycopy(data, index+1, data, index, size-index-1);
		}
		// 마지막 데이터를 null로 한다. 배열은 0 부터 시작하므로 마지막 요소는 index가 size-1이다.
		data[size-1] = null;
		size--;
		return oldObj;
	}
	
	public boolean remove(Object obj) {
		for(int i = 0; i < size; i++) {
			if(obj.equals(data[i])) {
				remove(i);
				return true;
			}
		}
		return false;
	}
	
	public void trimToSize() {
		setCapacity(size);
	}
	
	private void setCapacity(int capacity) {
		if(this.capacity == capacity) return;	// 크기가 같으면 변경하지 않는다.
		
		Object[] tmp = new Object[capacity];
		System.arraycopy(data, 0, tmp, 0, size);
		data = tmp;
		this.capacity = capacity;
	}
	
	public void clear() {
		for(int i = 0; i < size; i++) {
			data[i] = null;
		}
		size = 0;
	}
	
	public Object[] toArray() {
		Object[] result = new Object[size];
		System.arraycopy(data, 0, result, 0, size);
		
		return result;
	}
	
	public boolean isEmpty() { return size == 0; }
	public int capacity() { return capacity; }
	public int size() { return size; }
/******************************************/
/*		List인터페이스로부터 상속받은 메소드들	  */
/******************************************/
//	public int size();
//	public boolean isEmpty();
	public boolean contains(Object o) { return false; }
	public Iterator iterator() { return null; }
//	public Object[] toArray();
	public Object[] toArray(Object a[]) { return null; }
//	public boolean add(Object o);
//	public boolean remove(Object o);
	public boolean containsAll(Collection c) { return false; }
	public boolean addAll(Collection c) { return false; }
	public boolean addAll(int index, Collection c) { return false; }
	public boolean removeAll(Collection c) { return false; }
	public boolean retainAll(Collection c) { return false; }
//	public void clear();
	public boolean equals(Object o) { return false; }
//	public int hashCode();
//	public Object get(int index);
	public Object set(int index, Object element) { return null; }
	public void add(int index, Object element) {}
//	public Object remove(int index);
	public int indexOf(Object o) { return -1; }
	public int lastIndexOf(Object o) { return -1; }
	public ListIterator listIterator() { return null; }
	public ListIterator listIterator(int index) { return null; }
	public List subList(int fromIndex, int toIndex) { return null; }
	
//	default void sort(Comparator c) { /* 내용 생략 */ }					// JDK1.8부터
//	default Spliterator spliterator() { /* 내용 생략 */ }					// JDK1.8부터
//	default void replaceAll(UnaryOperator operator) { /* 내용 생략 */ }		// JDK1.8부터
}
```

`List`인터페이스의 메소드 중 주석처리한 것은 코드를 정상적으로 동작하도록 구현한 것이고, 주석처리하지 않은 것은 컴파일만 가능하도록 최소한으로 구현한 것이다.

> 인터페이스를 구현할 때 인터페이스에 정의된 모든 메소드를 구현해야 한다. 일부 메소드만 구현했다면 추상클래스로 선언해야한다. 그러나 JDK1.8부터 List인터페이스에 3개의 디폴트 메소드가 추가되었으며, 이 들은 구현하지 않아도 된다.

`remove`메소드는 단계별로 자세히 설명해보겠다.

``` java
public Object remove(int index) {
		Object oldObj = null;
		
		if(index < 0 || index >= size)
			throw new IndexOutOfBoundsException("범위를 벗어났습니다.");
		oldObj = data[index];
		
		if(index != size-1) {
			System.arraycopy(data, index+1, data, index, size-index-1);
		}

		data[size-1] = null;
		size--;

		return oldObj;
	}
```

`Object remove(int index)`메소드는 지정된 위치(index)에 있는 객체를 삭제하고 삭제한 객체를 반환하도록 작성하였다. 삭제할 객체의 바로 아래에 있는 데이터를 한 칸씩 위로 복사해서 삭제할 객체를 덮어쓰는 방식으로 처리한다. 만일 삭제할 객체가 마지막 데이터라면, 복사할 필요없이 단순히 null로 변경해주기만 하면 된다.

아래의 그림은 `MyVector`클래스에 0\~4이 값이 저장되어 있는 상태에서 세 번째 데이터를 삭제하기 위해 `remove(2)`를 호출했다고 가정하고, 그 수행과정의 일부를 단계별로 나타낸 것이다.

![image](https://ifh.cc/g/ZgAWft.png)

1. 삭제할 데이터의 아래에 있는 데이터를 한 칸씩 위로 복사해서 삭제할 데이터를 덮어쓴다.   
현재 5개의 데이터가 저장되어있으므로 `size`는 5이고 삭제할 객체의 `index`는 2이므로 `System.arraycopy(data, index+1, data, index, size-index-1)`는 `System.arraycopy(data, 3, data, 2, 2)`가 된다.

![image](https://ifh.cc/g/xgWACp.png)

2. 데이터가 모두 한 칸씩 위로 이동하였으므로 마지막 데이터는 null로 변경해야한다.   

``` java
data[size-1] = null;
```

3. 데이터가 삭제되어 데이터의 개수가 줄었으므로 size의 값을 1 감소시킨다.

``` java
size--;
```

배열에 객체를 순차적으로 저장할 때와 객체를 마지막에 저장된 것부터 삭제하면 `System.arraycopy()`를 호출하지 않기 때문에 작업시간이 짧지만, 배열의 중간에 위치한 객체를 추가하거나 삭제하는 경우 `System.arraycopy()`를 호출해서 다른 데이터의 위치를 이동시켜 줘야 하기 때문에 다루는 데이터의 개수가 많을수록 작업시간이 오래 걸린다는 것이다.