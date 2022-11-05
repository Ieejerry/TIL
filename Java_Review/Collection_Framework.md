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

</br>

## 1.3 LinkedList

배열은 가장 기본적인 형태의 자료구조로 구조가 간단하며 사용하기 쉽고 데이터를 읽어오는데 걸리는 시간(접근시간, access time)이 가장 빠르다는 장점을 가지고 있지만 다음과 같은 단점도 가지고 있다.

> 1. 크기를 변경할 수 없다.   
> - 크기를 변경할 수 없으므로 새로운 배열을 생성해서 데이터를 복사해야한다.
> - 실행속도를 향상시키기 위해서는 충분히 큰 크기의 배열을 생성해야 하므로 메모리가 낭비된다.
>   
> 2. 비순차적인 데이터의 추가 또는 삭제에 시간이 많이 걸린다.
> - 차례대로 데이터를 추가하고 마지막에서부터 데이터를 삭제하는 것은 빠르지만.
> - 배열이 중간에 데이터를 추가하려면, 빈자리를 만들기 위해 다른 데이터들을 복사해서 이동해야 한다.

이러한 배열의 단점을 보완하기 위해서 링크드 리스트(Linked list)라는 자료구조가 고안되었다. 배열은 모든 데이터가 연속적으로 존재하지만 링크드 리스트는 불연속적으로 존재하는 데이터를 서로 연결(link)한 형태로 구성되어 있다.

![image](https://ifh.cc/g/BB8qoO.png)

위의 그림에서 알 수 있듯이 링크드 리스트의 각 요소(node)들은 자신과 연결된 다음 요소에 대한 참조(주소값)와 데이터로 구성되어 있다.

``` java
class Node {
	Node next;	// 다음 요소의 주소를 저장
	Object obj;	// 데이터를 저장
}
```

링크드 리스트에서의 데이터 삭제는 간단하다. 삭제하고자 하는 요소의 이전요소가 삭제하고자 하는 요소의 다음 요소를 참조하도록 변경하기만 하면 된다. 단 하나의 참조만 변경하면 삭제가 이루어지는 것이다. 배열처럼 데이터를 이동하기 위해 복사하는 과정이 없기 때문에 처리속도가 매우 빠르다.

![image](https://ifh.cc/g/vTQQyK.png)

새로운 데이터를 추가할 때는 새로운 요소를 생성한 다음 추가하고자 하는 위치의 이전 요소의 참조를 새로운 요소에 대한 참조로 변경해주고, 새로운 요소가 그 다음 요소를 참조하도록 변경하기만 하면 되므로 처리속도가 매우 빠르다.

![image](https://ifh.cc/g/QJMHod.png)

링크드 리스트는 이동방향이 단방향이기 떄문에 다음 요소에 대한 접근이 쉽지만 이전 요소에 대한 접근은 어렵다. 이 점을 보완한 것이 더블 링크드 리스트(이중 연결리스트, doubly linked list)이다.

더블 링크드 리스트는 단순히 링크드 리스트에 참조변수를 하나 더 추가하여 다음 요소에 대한 참조뿐 아니라 이전 요소에 대한 참조가 가능하도록 했을 뿐, 그 외에는 링크드 리스트와 같다.

더블 링크드 리스트는 링크드 리스트보다 각 요소에 대한 접근과 이동이 쉽기 때문에 링크드 리스트보다 더 많이 사용된다.

``` java
class Node {
	Node next;	// 다음 요소의 주소를 저장
	Node previous;	// 이전 요소의 주소를 저장
	Object obj;	// 데이터를 저장
}
```

![image](https://ifh.cc/g/Lmb6zw.png)

더블 링크드 리스트의 접근성을 보다 향상시킨 것이 '더블 써큘러 링크드 리스트(이중 원형 연결리스트, doubly circular linked list)'인데, 단순히 더블 링크드 리스트의 첫 번째 요소와 마지막 요소를 서로 연결시킨 것이다. 이렇게 하면, 마지막 요소의 다음 요소가 첫 번째가 되고, 첫 번째의 이전 요소가 마지막 요소가 된다.

![image](https://ifh.cc/g/bFTBrQ.png)

실제로 `LinkedList`클래스는 이름과 달리 '링크드 리스트'가 아닌 '더블 링크드 리스트'로 구현되어 있는데, 이는 링크드 리스트의 단점인 낮은 접근성(accessability)을 높이기 위한 것이다. `LinkedList`클래스에 대해 알아보도록 하겠다.

![image](https://ifh.cc/g/flN47X.png)

> LinkedList는 Queue인터페이스(JDK1.5)와 Deque인터페이스(JDK1.6)를 구현하도록 변경되었는데, 표의 마지막 22개의 메소드는 Queue인터페이스(회색바탕)와 Deque인터페이스(흰색바탕)를 구현하면서 추가된 것이다.

`LinkedList` 역시 `List`인터페이스를 구현했기 때문에 `ArrayList`와 내부구현방법만 다를 뿐 제공하는 메소드의 종류와 기능은 거의 같다.

`ArrayList`와 `LinkedList`의 장단점을 이해하고 필요한 상황에 적절한 것을 선택해서 사용하는 것이 좋다.

</br>

예제 11-5 / ch11 / ArrayListLinkedListTest.java

``` java
import java.util.*;

public class ArrayListLinkedListTest {
	public static void main(String[] args) {
		// 추가할 데이터의 개수를 고려하여 충분히 잡아야한다.
		ArrayList al = new ArrayList(2000000);
		LinkedList ll = new LinkedList();
		
		System.out.println("= 순차적으로 추가하기 =");
		System.out.println("ArrayList : " + add1(al));
		System.out.println("LinkedList : " + add1(ll));
		System.out.println();
		System.out.println("= 중간에 추가하기 =");
		System.out.println("ArrayList : " + add2(al));
		System.out.println("LinkedList : " + add2(ll));
		System.out.println();
		System.out.println("= 중간에서 삭제하기 =");
		System.out.println("ArrayList : " + remove2(al));
		System.out.println("LinkedList : " + remove2(ll));
		System.out.println();
		System.out.println("= 순차적으로 삭제하기 =");
		System.out.println("ArrayList : " + remove1(al));
		System.out.println("LinkedList : " + remove1(ll));
	}
	
	public static long add1(List list) {
		long start = System.currentTimeMillis();
		for(int i = 0; i < 1000000; i++) list.add(i + "");
		long end = System.currentTimeMillis();
		return end - start;
	}
	
	public static long add2(List list) {
		long start = System.currentTimeMillis();
		for(int i = 0; i < 10000; i++) list.add(500, "X");
		long end = System.currentTimeMillis();
		return end - start;
	}
	
	public static long remove1(List list) {
		long start = System.currentTimeMillis();
		for(int i = list.size()-1; i >= 0; i--) list.remove(i);
		long end = System.currentTimeMillis();
		return end - start;
	}
	
	public static long remove2(List list) {
		long start = System.currentTimeMillis();
		for(int i = 0; i < 10000; i++) list.remove(i);
		long end = System.currentTimeMillis();
		return end - start;
	}
}
```

```
= 순차적으로 추가하기 =
ArrayList : 222
LinkedList : 426

= 중간에 추가하기 =
ArrayList : 2722
LinkedList : 17

= 중간에서 삭제하기 =
ArrayList : 1978
LinkedList : 321

= 순차적으로 삭제하기 =
ArrayList : 12
LinkedList : 38
```

[결론 1] 순차적으로 추가/삭제하는 경우에는 ArrayList가 LinkedList보다 빠르다.

단순히 저장하는 시간만을 비교할 수 있도록 하기 위해서 `ArrayList`를 생성할 때는 저장할 데이터의 개수만큼 충분한 초기용량을 확보해서, 저장공간이 부족해서 새로운 `ArrayList`를 생성해야하는 상황이 일어나지 않도록 했다. 만일 `ArrayList`의 크기가 충분하지 않으면, 새로운 크기의 `ArrayList`를 생성하고 데이터를 복사하는 일이 발생하게 되므로 순차적으로 데이터를 추가해도 `ArrayList`보다 `LinkedList`가 더 빠를 수 있다.

순차적으로 삭제한다는 것은 마지막 데이터부터 역순으로 삭제해나간다는 것을 의미하며, `ArrayList`는 마지막 데이터부터 삭제할 경우 각 요소들의 재배치가 필요하지 않기 때문에 상당히 빠르다. 단지 마지막 요소의 값을 null로만 바꾸면 된다.

[결론 2] 중간 데이터를 추가/삭제하는 경우에는 LinkedList가 ArrayList보다 빠르다.

중간 요소를 추가 또는 삭제하는 경우, `LiekedList`는 각 요소간의 연결만 변경해주면 되기 때문에 처리속도가 상당히 빠르다. 반면에 `ArrayList`는 각 요소들을 재배치하여 추가할 공간을 확보하거나 빈 공간을 채워야하기 때문에 처리속도가 늦다.

예제에서는 `ArrayList`와 `LinkedList`의 차이를 비교하기 위해 데이터의 개수를 크게 잡았는데, 사실 데이터의 개수가 그리 크지 않다면 어느 것을 사용해도 큰 차이가 나지는 않는다. 그래도 `ArrayList`와 `LinkedList`의 장단점을 잘 이해하고 상황에 따라 적합한 것을 선택해서 사용하는 것이 좋다.

</br>

예제 11-6 / ch11 / ArrayListLinkedListTest2.java

``` java
import java.util.*;

public class ArrayListLinkedListTest2 {
	public static void main(String[] args) {
		ArrayList al = new ArrayList(1000000);
		LinkedList ll = new LinkedList();
		add(al);
		add(ll);
		
		System.out.println("= 접근시간테스트 =");
		System.out.println("ArrayList : " + access(al));
		System.out.println("ArrayList : " + access(ll));
	}
	
	public static void add(List list) {
		for(int i = 0; i < 100000; i++) list.add(i + "");
	}
	
	public static long access(List list) {
		long start = System.currentTimeMillis();
		for(int i = 0; i < 10000; i++) list.get(i);
		long end = System.currentTimeMillis();
		return end - start;
	}
}
```

```
= 접근시간테스트 =
ArrayList : 1
ArrayList : 458
```

배열의 경우 만일 인덱스가 n인 요소의 값을 얻어 오고자 한다면 단순히 아래와 같이 수식을 계산함으로써 해결된다.

> **인덱스가 n인 데이터이 주소 = 배열의 주소 + n * 데이터 타입의 크기**

아래와 같이 Object배열이 선언되었을 때 `arr[2]`에 저장된 값을 읽으려 한다면 `n`은 2, 모든 참조형 변수의 크기는 4byte이고 생성된 배열의 주소는 0x100이므로 3번째 데이터가 저장되어 있는 주소는 0x100 + 2 * 4 = 0x108이 된다.

![image](https://ifh.cc/g/wpQx7m.png)

배열은 각 요소들이 연속적으로 메모리상에 존재하기 때문에 이처럼 간단한 계산만으로 원하는 요소의 주소를 얻어서 저장된 데이터를 곧바로 읽어올 수 있지만, `LinkedList`는 불연속적으로 위치한 각 요소들이 서로 연결된 것이라 처음부터 n번째 데이터부터 차례대로 따라가야만 원하는 값을 얻을 수 있다.

그래서 `LinkedList`는 저장해야하는 데이터의 개수가 많아질수록 데이터를 읽어 오는 시간, 즉 접근시간(access time)이 길어진다는 단점이 있다.

![image](https://ifh.cc/g/ydRCD5.png)

다루고자 하는 데이터의 개수가 변하지 않는 경우라면, `ArrayList`가 최상의 선택이 되겠지만, 데이터 개수의 변경이 잦다면 `LinkedList`를 사용하는 것이 더 나은 선택이 될 것이다.

두 클래스의 장점을 이용해서 두 클래스를 조합해서 사용하는 방법도 생각해 볼 수 있다. 처음에 작업하기 전에 데이터를 저장할 때는 `ArrayList`를 사용한 다음, 작업할 때는 `LinkedList`로 데이터를 옮겨서 작업하면 좋은 효율을 얻을 수 있다.

``` java
ArrayList al = new ArrayList(1000000);
for(int i = 0; i < 100000; i++) al.add(i + "");

LinkedList ll = new LinkedList(al);
for(int i = 0; i < 1000; i++) ll.add(500, "X");
```

컬렉션 프레임워크에 속한 대부분의 컬렉션 클래스들은 이처럼 서로 변환이 가능한 생성자를 제공하므로 이를 이용하면 간단히 다른 컬렉션 클래스로 데이터를 옮길 수 있다.

</br>

## 1.4 Stack와 Queue

스택은 마지막에 저장한 데이터를 가장 먼저 꺼내게 되는 LIFO(Last In First Out)구조로 되어 있고, 큐는 처음에 저장한 데이터를 가장 먼저 꺼내게 되는 FIFO(First In First Out)구조로 되어 있다.

![image](https://ifh.cc/g/6O2cr1.png)

예를 들어 스택에 0, 1, 2의 순서로 데이터를 넣었다면 꺼낼 때는 2, 1, 0의 순서로 꺼내게 된다. 즉, 넣은 순서와 꺼낸 순서가 뒤집어지게 되는 것이다. 이와 반대로 큐에 0, 1, 2의 순서로 데이터를 넣었다면 꺼낼 때 역시 0, 1, 2의 순서로 꺼내게 된다. 순서의 변경 없이 먼저 넣은 것을 먼저 꺼내게 되는 것이다.

순차적으로 데이터를 추가하고 삭제하는 스택에는 `ArrayList`와 같은 배열기반의 컬렉션 클래스가 적합하지만, 큐는 데이터를 꺼낼 때 항상 첫 번째 저장된 데이터를 삭제하므로, `ArrayList`와 같은 배열기반의 컬렉션 클래스를 사용한다면 데이터를 꺼낼 때마다 빈 공간을 채우기 위해 데이터의 복사가 발생하므로 비효율적이다. 그래서 큐는 `ArrayList`보다 데이터의 추가/삭제가 쉬운 `LinkedList`로 구현하는 것이 더 적합하다.

![image](https://ifh.cc/g/30tmQ4.png)

</br>

예제 11-7 / ch11 / StackQueueEx.java

``` java
import java.util.*;

public class StackQueueEx {
	public static void main(String[] args) {
		Stack st = new Stack();
		Queue q = new LinkedList();	// Queue인터페이스의 구현체인 LinkedList를 사용
		
		st.push("0");
		st.push("1");
		st.push("2");
		
		q.offer("0");
		q.offer("1");
		q.offer("2");
		
		System.out.println("= Stack =");
		while(!st.empty()) {
			System.out.println(st.pop());
		}
		
		System.out.println("= Queue =");
		while(!q.isEmpty()) {
			System.out.println(q.poll());
		}
	}
}
```

```
= Stack =
2
1
0
= Queue =
0
1
2
```

스택과 큐에 각각 "0", "1", "2"를 같은 순서로 넣고 꺼내었을 때의 결과가 다른 것을 알 수 있다. 큐는 먼저 넣은 것이 먼저 꺼내지는 구조(FIFO)이기 때문에 넣을 떄와 같은 순서이고, 스택은 먼저 넣은 것이 나중에 꺼내지는 구조(LIFO)이기 떄문에 넣을 때의 순서와 반대로 꺼내진 것을 알 수 있다.

자바에서는 스택을 `Stack`클래스로 구현하여 제공하고 있지만 큐는 `Queue`인터페이스만 정의해 놓았을 뿐 별도의 클래스를 제공하고 있지 않다. 대신 `Queue`인터페이스를 구현한 클래스들이 있어서 이 들 중의 하나를 선택해서 사용하면 된다.

</br>

### Stack 직접 구현하기

`Stack`은 컬렉션 프레임워크 이전부터 존재하던 것이기 때문에 `ArrayList`가 아닌 `Vector`부터 상속받아 구현하였다. `Stack`의 실제코드를 이해하기 쉽게 약간 수정해서 `MyStack`을 만들어 보았다.

</br>

예제 11-8 / ch11 / MyStack.java

``` java
import java.util.*;

public class MyStack extends Vector{
	public static void main(String[] args) {
		
	}
	
	public Object pop() {
		Object obj = peek();	// Stack에 저장된 마지막 요소를 읽어온다.
		// 만일 Stack이 비어있으면 peek()메소드가 EmptyStackException을 발생시킨다.
		// 마지막 요소를 삭제한다. 배열의 index가 0 부터 시작하므로 1을 빼준다.
		removeElementAt(size() - 1);
		return obj;
	}
	
	public Object peek() {
		int len = size();
		
		if(len == 0)
			throw new EmptyStackException();
		// 마지막 요소를 반환한다. 배열의 index가 0 부터 시작하므로 1을 빼준다.
		return elementAt(len - 1);
	}
	
	public boolean empty() {
		return size() == 0;
	}
	
	public int search(Object o) {
		int i = lastIndexOf(o);	// 끝에서부터 객체를 찾는다.
								// 반환값은 저장된 위치(배열의 index)이다.
		if(i >= 0) {	// 객체를 찾은 경우
			return size() - i;	// Stack은 맨 위에 저장된 객체의 index를 1로 정의하기 때문에
								// 계산을 통해서 구한다.
		}
		return -1;	// 해당 객체를 찾지 못하면 -1를 반환한다.
	}
}
```

> EmptyStackException은 RuntimeException이므로 따로 예외처리를 해주지 않아도 된다.

</br>

### 스택과 큐의 활용

쉽게 찾아볼 수 있는 스택과 큐의 활용 예는 다음과 같다.

> **스택의 활용 예** - 수식계산, 수식괄호검사, 워드프로세서의 undo/redo, 웹브라우저의 뒤로/앞으로   
**큐의 활용 예** - 최근사용문서, 인쇄작업 대기목록, 버퍼(buffer)

</br>

예제 11-9 / ch11 / StackEx1.java

``` java
import java.util.*;

public class StackEx1 {
	public static Stack back = new Stack();
	public static Stack forward = new Stack();
	
	public static void main(String[] args) {
		goURL("1.네이트");
		goURL("2.야후");
		goURL("3.네이버");
		goURL("4.다음");
		
		printStatus();
		
		goBack();
		System.out.println("= '뒤로' 버튼을 누른 후 =");
		printStatus();
		
		goBack();
		System.out.println("= '뒤로' 버튼을 누른 후 =");
		printStatus();
		
		goForward();
		System.out.println("= '앞으로' 버튼을 누른 후 =");
		printStatus();
		
		goURL("codechobo.com");
		System.out.println("= 새로운 주소로 이동 후 =");
		printStatus();
		
	}
	
	public static void printStatus() {
		System.out.println("back : " + back);
		System.out.println("forward : " + forward);
		System.out.println("현재화면은 '" + back.peek() + "' 입니다.");
		System.out.println();
	}
	
	public static void goURL(String url) {
		back.push(url);
		if(!forward.empty())
			forward.clear();
	}
	
	public static void goForward() {
		if(!forward.empty())
			back.push(forward.pop());
	}
	
	public static void goBack() {
		if(!back.empty())
			forward.push(back.pop());
	}
}
```

```
back : [1.네이트, 2.야후, 3.네이버, 4.다음]
forward : []
현재화면은 '4.다음' 입니다.

= '뒤로' 버튼을 누른 후 =
back : [1.네이트, 2.야후, 3.네이버]
forward : [4.다음]
현재화면은 '3.네이버' 입니다.

= '뒤로' 버튼을 누른 후 =
back : [1.네이트, 2.야후]
forward : [4.다음, 3.네이버]
현재화면은 '2.야후' 입니다.

= '앞으로' 버튼을 누른 후 =
back : [1.네이트, 2.야후, 3.네이버]
forward : [4.다음]
현재화면은 '3.네이버' 입니다.

= 새로운 주소로 이동 후 =
back : [1.네이트, 2.야후, 3.네이버, codechobo.com]
forward : []
현재화면은 'codechobo.com' 입니다.
```

이 예제는 웹브라우저의 '뒤로', '앞으로'버튼의 기능을 구현한 것이다. 이 기능을 구현하기 위해서는 2개의 스택을 사용해야한다.

> 워드프로세서의 되돌리기 기능(undo/redo) 역시 이와 같은 방식으로 되어있다.

</br>

예제 11-10 / ch11 / ExpValidCheck.java

``` java
import java.util.*;

public class ExpValidCheck {
	public static void main(String[] args) {
		if(args.length != 1) {
			System.out.println("Usage:java Ex11_3 \"EXPRESSION\"");
			System.out.println("Example:java Ex11_3 \"((2+3)*1)+3\"");
			System.exit(0);
		}
		
		Stack st = new Stack();
		String expression = args[0];
		
		System.out.println("expression:" + expression);
		
		try {
			for(int i = 0; i < expression.length(); i++) {
				char ch = expression.charAt(i);
				
				if(ch == '(') {
					st.push(ch + "");
				} else if(ch == ')') {
					st.pop();
				}
			}
			
			if(st.isEmpty()) {
				System.out.println("괄호가 일치합니다.");
			} else {
				System.out.println("괄호가 일치하지 않습니다.");
			}
		} catch (EmptyStackException e) {
			System.out.println("괄호가 일치하지 않습니다.");
		}	// try
	}
}
```

```
c:\jdk1.8\work\ch11>java ExpValidCheck
Usage	: java ExpValidCheck "EXPRESSION"
Example : java ExpValidCheck "((2+3)*1)+3"

c:\jdk.19\work\ch11>java ExpValidCheck (2+3)*1
expression: (2+3)*1
괄호가 일치합니다.
```

입력한 수식의 괄호가 올바른지를 체크하는 예제이다. '('를 만나면 스택에 넣고 ')'를 만나면 스택에서 '('를 꺼낸다. ')'를 만나서 '('를 꺼내려 할 때 스택이 비어있거나 수식을 검사하고 난 후에도 스택이 비어있지 않으면 괄호가 잘못된 것이다.

')'를 만나서 '('를 꺼내려 할 때 스택이 비어있으면 EmptyStackException이 발생하므로 try-catch문을 이용해서 EmptyStackException이 발생하면 괄호가 일치하지 않는다는 메세지를 출력하도록 했다.

</br>

예제 11-11 / ch11 / QueueEx1.java

``` java
import java.util.*;

public class QueueEx1 {
	static Queue q = new LinkedList();
	static final int MAX_SIZE = 5;	// Queue에 최대 5개까지만 저장되도록 한다.
	
	public static void main(String[] args) {
		System.out.println("help를 입력하면 도움말을 볼 수 있습니다.");
		
		while(true) {
			System.out.println(">>");
			try {
				// 화면으로부터 라인단위로 입력받는다.
				Scanner s = new Scanner(System.in);
				String input = s.nextLine().trim();
				
				if("".equals(input)) continue;
				
				if(input.equalsIgnoreCase("q")) {
					System.exit(0);
				} else if(input.equalsIgnoreCase("help")) {
					System.out.println(" help - 도움말을 보여줍니다.");
					System.out.println(" q 또는 Q - 프로그램을 종료합니다.");
					System.out.println(" history - 최근에 입력한 명령어를 " + MAX_SIZE + "개 보여줍니다.");
				} else if (input.equalsIgnoreCase("history")) {
					save(input);	// 입력받은 명령어를 저장하고,
					
					// LinkedList의 내용을 보여준다.
					LinkedList list = (LinkedList)q;
					
					final int SIZE = list.size();
					for(int i = 0; i < SIZE; i++) {
						System.out.println((i+1)+"."+list.get(i));
					}
				} else {
					save(input);
					System.out.println(input);
				}	// if(input.equalsIgnoreCase("q")) {
			} catch (Exception e) {
				System.out.println("입력 오류입니다.");
			}
		}
	}
	
	public static void save(String input) {
		// queue에 저장한다.
		if(!"".equals(input))	// if(!input.equals(""))
			q.offer(input);	// 큐에 명령어를 저장
		
		// queue의 최대크기를 넘으면 제일 처음 입력된 것을 삭제한다.
		if(q.size() > MAX_SIZE)	// size()는 Collection인터페이스에 정의
			q.remove();
	}
}	// end of class
```

```
c:\jdk1.8\work\ch11>java QueueEx1
help를 입력하면 도움말을 볼 수 있습니다.
>>
help
 help - 도움말을 보여줍니다.
 q 또는 Q - 프로그램을 종료합니다.
 history - 최근에 입력한 명령어를 5개 보여줍니다.
>>
dir
dir
>>
cd
cd
>>
mkdir
mkdir
>>
dir
dir
>>
history
1.dir
2.cd
3.mkdir
4.dir
5.history
>>
q

c:\jdk1.8\work\ch11>java QueueEx1
```

이 예제는 유닉스 history명령러를 `Queue`를 이용해서 구현한 것이다. history명령어는 사용자가 입력한 명령어의 이력을 순서대로 보여 준다. 여기서는 최근 5개의 명령어만을 보여주는데 `MAX_SIZE`의 값을 변경함으로써 더 많은 명령어 입력기록을 남길 수 있다.

</br>

### PriorityQueue

`Queue`인터페이스의 구현체 중의 하나로, 저장한 순서에 관계없이 우선순위(priority)가 높은 것부터 꺼내게 된다는 특징이 있다. 그리고 null은 저장할 수 없다. null을 저장하면 NullPointerException이 발생한다.

`PriorityQueue`는 저장공간으로 배열을 사용하며, 각 요소를 '힙(heap)'이라는 자료구조의 형태로 저장한다. 힙은 이진 트리의 한 종류로 가장 큰 값이나 가장 작은 값을 빠르게 찾을 수 있다는 특징이 있다.

> 자료구조 힙(heap)은 JVM의 힙(heap)과 이름만 같을 뿐 다른 것이다.

</br>

예제 11-12 / ch11 / PriorityQueueEx.java

``` java
import java.util.*;

public class PriorityQueueEx {
	public static void main(String[] args) {
		Queue pq = new PriorityQueue();
		pq.offer(3);	// pq.offer(new Integer(3)); 오토박싱
		pq.offer(1);
		pq.offer(5);
		pq.offer(2);
		pq.offer(4);
		System.out.println(pq);	// pq의 내부 배열을 출력
		
		Object obj = null;
		
		// PriorityQueue에 저장된 요소를 하나씩 꺼낸다.
		while((obj = pq.poll()) != null)
			System.out.println(obj);
	}
}
```

```
[1, 2, 5, 3, 4]
1
2
3
4
5
```

저장순서가 3, 1, 5, 2, 4인데도 출력결과는 1, 2, 3, 4, 5이다. 우선순위는 숫자가 작을수록 높은 것이므로 1이 가장 먼저 출력된 것이다. 물론 숫자뿐만 아니라 객체를 저장할 수도 있는데 그럴 경우 각 객체의 크기를 비교할 수 있는 방법을 제공해야 한다. 예제에서는 정수를 사용했는데, 컴파일러가 `Integer`로 오토박싱 해준다. `Integer`와 같은 `Number`의 자손들은 자체적으로 숫자를 비교하는 방법을 정의하고 있기 때문에 비교 방법을 지정해 주지 않아도 된다.

참조변수 `pq`를 출력하면, `PriorityQueue`가 내부적으로 가지고 있는 배열의 내용이 출력되는데, 저장한 순서와 다르게 저장되었다. 앞서 설명한 것과 같이 힙이라는 자료구조의 형태로 저장된 것이라서 그렇다.

</br>

### Deque(Double-Ended Queue)

`Queue`의 변형으로, 한 쪽 끝으로만 추가/삭제할 수 있는 `Queue`와 달리, `Deque`(덱, 또는 디큐라고 읽음)은 양쪽 끝에 추가/삭제가 가능하다. `Deque`의 조상은 `Queue`이며, 구현체로는 `ArrayDeque`과 `LinkedList`등이 있다.

![image](https://ifh.cc/g/YH19tS.png)

덱은 스택과 큐를 하나로 합쳐놓은 것과 같으며 스택으로 사용할 수도 있고, 큐로 사용할 수도 있다.

![image](https://ifh.cc/g/h2DTK7.png)

</br>

## 1.5 Iterator, ListIterater, Enumeration

`Iterator`, `ListIterator`, `Enumeration`은 모두 컬렉션에 저장된 요소를 접근하는데 사용되는 인터페이스이다. `Eumeration`은 `Iterator`의 구버전이며, `ListIterator`는 `Iterator`의 기능을 향상 시킨 것이다.

### Iterator

컬렉션 프레임워크에서는 컬렉션에 저장된 요소들을 읽어오는 방법을 표준화하였다. 컬렉션에 저장된 각 요소에 접근하는 기능을 가진 `Iterator`인터페이스를 정의하고, `Colloection`인터페이스에는 'Iterator(Iterator를 구현한 클래스의 인스턴스)'를 반환하는 `iterator()`를 정의하고 있다.

``` java
public interface Iterator {
	boolean hasNext();
	Object next();
	void remove();
}

public interface Collection {
	...
	public Iterator iterator();
	...
}
```

`iterator()`는 `Collection`인터페이스에 정의된 메소드이므로 `Collection`인터페이스의 자손인 `List`와 `Set`에도 포함되어 있다. 그래서 `List`와 `Set`인터페이스를 구현하는 컬렉션은 `iterator()`가 각 컬렉션의 특징에 알맞게 작성되어 있다. 컬렉션 클래스에 대해 `iterator()`를 호출하여 `Iterator`를 얻은 다음 반복문, 주로 while문을 사용해서 컬렉션 클래스의 요소들을 읽어 올 수 있다.

![image](https://ifh.cc/g/xw965O.png)

`ArrayList`에 저장된 요소들을 출력하기 위한 코드는 다음과 같이 작성할 수 있다.

``` java
Collection c = new ArrayList();	// 다른 컬렉션으로 변경시 이 부분만 고치면 된다.
Iterator it = c.iterator();

while(it.hasNext()) {
	System.out.println(it.next());
}
```

`ArrayList`대신 `Collection`인터페이스를 구현한 다른 컬렉션 클래스에 대해서도 이와 동일한 코드를 사용할 수 있다. 첫 줄에서 `ArrayList`대신 `Collection`인터페이스를 구현한 다른 컬렉션 클래스의 객체를 생성하도록 변경하기만 하면 된다.

`Iterator`를 이용해서 컬렉션의 요소를 읽어오는 방법을 표준화했기 때문에 이처럼 코드의 재사용성을 높이는 것이 가능한 것이다. 이처럼 공통 인터페이스를 정의해서 표준을 정의하고 구현하여 표준을 따르도록 함으로써 코드의 일관성을 유지하여 재사용성을 극대화하는 것이 객체지향 프로그래밍의 중요한 목적 중의 하나이다.

`Map`인터페이스를 구현한 클래스는 키(key)와 값(value)을 쌍(pair)으로 저장하고 있기 때문에 `iterator()`를 직접 호출할 수 없고, 그 대신 `keySet()`이나 `entrySet()`과 같은 메소드를 통해서 키와 값을 각각 따로 Set의 형태로 얻어 온 후에 다시 `iterator()`를 호출해야 `Iterator`를 얻을 수 있다.

``` java
Map map = new HashMap();
	...
Iterator it = map.entrySet().iterator();
```

`iterator it = map.entrySet().iterator();`는 아래의 두 문장을 하나로 합친 것이라고 이해하면 된다.

``` java
Set eSet = map.entrySet();
Iterator it = eSet.iterator();
```

이 문장들의 실행순서를 그림으로 그려보면 다음과 같다.

![image](https://ifh.cc/g/kfvwYo.png)

① map.entrySet()의 실행결과가 Set이므로   
Iterator it = map.entrySet().iterator(); → Iterator it = Set인스턴스.iterator();

② map.entrySet()를 통해 얻은 set인스턴스의 iterator()를 호출해서 iterator인스턴스를 얻는다.   
Iterator it = Set인스턴스.iterator(); → Iterator it = Iterator인스턴스;

③ 마지막으로 Iterator인스턴스의 참조가 it에 저장된다.

`StringBuffer`를 사용할 때 이와 유사한 코드를 많이 보았다.

``` java
StringBuffer sb = new StringBuffer();
sb.append("A");
sb.append("B");
sb.append("C");
```

위와 같은 코드를 아래와 같이 간단히 쓸 수 있는데 그 이유는 바로 `append`메소드가 수행 결과로 `StringBuffer`를 리턴하기 떄문이다. 만일 `void append(String str)`과 같이 void를 리턴하도록 선언되어 있다면 위의 코드를 아래와 같이 쓸 수 없다. `append`메소드의 호출결과가 void이기 때문에 또 다시 void에 `append`메소드를 호출할 수 없기 때문이다.

``` java
StringBuffer sb = new StringBuffer();
sb.append("A").append("B").append("C");	// StringBuffer append(String str)
```

</br>

예제 11-13 / ch11 / IteratorEx1.java

``` java
import java.util.*;

public class IteratorEx1 {
	public static void main(String[] args) {
		ArrayList list = new ArrayList();
		list.add("1");
		list.add("2");
		list.add("3");
		list.add("4");
		list.add("5");
		
		Iterator it = list.iterator();
		
		while(it.hasNext()) {
			Object obj = it.next();
			System.out.println(obj);
		}
	}	// main
}
```

```
1
2
3
4
5
```

`List`클래스들은 저장순서를 유지하기 때문에 `Iterator`를 이용해서 읽어 온 결과 역시 저장순서와 동일하지만 `Set`클래스들은 각 요소간의 순서가 유지 되지 않기 때문에 `Iterator`를 이용해서 저장된 요소들을 읽어 와도 처음에 저장된 순서와 같지 않다.

</br>

### ListIterator와 Enumeration

`Enumeration`은 컬렉션 프레임워크이 만들어지기 이전에 사용하던 것으로 `Iterator`의 구버전이라고 생각하면 된다. 이전 버전으로 작성된 소스와의 호환을 위해서 남겨 두고 있을 뿐이므로 가능하면 `Enumeration`대신 `Iterator`를 사용하는 것이 좋다.

`ListIterator`는 `Iterator`를 상속받아서 기능을 추가한 것으로, 컬렉션의 요소에 접근할 때 `Iterator`는 단반향으로만 이동할 수 있는 데 반해 `ListIterator`는 양방향으로의 이동이 가능하다. 다만 `ArrayList`나 `LinkedList`와 같이 `List`인터페이스를 구현한 컬렉션에서만 사용할 수 있다.

> **Enumeration** Iterator의 구버전   
**ListIterator** Iterator에 양방향 조회기능추가(List를 구현한 경우만 사용가능)

다음은 `Enumeration`, `Iterator`, `ListIterator`의 메소드에 대한 설명이다. `Enumeration`과 `iterator`는 메소드이름만 다를 뿐 기능은 같고, `ListIterator`는 `Iterator`에 이전방향으로의 접근기능을 추가한 것일 뿐이다.

![image](https://ifh.cc/g/DSh9Dm.png)

</br>

![image](https://ifh.cc/g/6FRA8R.png)

</br>

예제 11-14 / ch11 / ListIteratorEx1.java

``` java
import java.util.*;

public class ListIteratorEx1 {
	public static void main(String[] args) {
		ArrayList list = new ArrayList();
		list.add("1");
		list.add("2");
		list.add("3");
		list.add("4");
		list.add("5");
		
		ListIterator it = list.listIterator();
		
		while(it.hasNext()) {
			System.out.print(it.next());	// 순방향으로 진행하면서 읽어온다.
		}
		System.out.println();
		
		while(it.hasPrevious()) {
			System.out.print(it.previous());	// 역방향으로 진행하면서 읽어온다.
		}
		System.out.println();
	}
}
```

```
12345
54321
```

`ListIterator`의 사용방법을 보여주는 간단한 예제이다. `Iterator`는 단방향으로만 이동하기 때문에 컬렉션의 마지막 요소에 다다르면 더 이상 사용할 수 없지만, `ListIterator`는 양방향으로 이동하기 때문에 각 요소간의 이동이 자유롭다. 다만 이동하기 전에 반드시 `hasNext()`나 `hasPrevious()`를 호출해서 이동할 수 있는지 확인해야 한다.

위의 표에 있는 메소드 중에서 '선택적 기능(optional operation)'이라고 표시된 것들은 반드시 구현하지 않아도 된다. 예를 들어 `Iterator`인터페이스를 구현하는 클래스에서 `remove()`는 선태적인 기능이므로 구현하지 않도록 괜찮다. 그렇다하더라고 인터페이스로부터 상속받은 메소드는 추상메소드라 메소드의 몸통(body)을 반드시 만들어 주어야하므로 다음과 같이 처리한다.

``` java
public void remove() {
	throw new UnsupportedOperationException();
}
```

단순히 `public void remove() {};`와 같이 구현하는 것보다 이처럼 예외를 던져서 구현되지 않은 기능이라는 것을 메소드를 호출하는 쪽에 알리는 것이 좋다. 그렇지 않으면 호출하는 쪽에서는 소스를 구해보기 전까지는 이 기능이 바르게 동작하지 않는 이유를 알 방법이 없다.

Java API문서에서 `remove()`메소드의 상세내용을 보면 `remove`메소드를 지원하지 않는 `Iterator`는 `UnsupportedOperationException`을 발생시킨다고 쓰여 있다. 즉, `remove`메소드를 구현하지 않은 경우에는 `UnsupportedOperationException`을 발생시키도록 구현하라는 뜻이다.

위의 코드에서 `remove`메소드의 선언부에 예외처리를 하지 않은 이유는 `UnsupportedOpertionException`이 `RuntimeException`의 자손이기 때문이다.

`Iterator`의 `remove()`는 단독으로 쓰일 수 없고, `next()`와 같이 써야한다. 특정위치의 요소를 삭제하는 것이 아니라 읽어 온 것을 삭제한다. `next()`의 호출없이 `remove()` 호출하면, `IllegalStateException`이 발생한다.

</br>

예제 11-15 / ch11 / IteratorEx2.java

``` java
import java.util.*;

public class IteratorEx2 {
	public static void main(String[] args) {
		ArrayList original = new ArrayList();
		ArrayList copy1 = new ArrayList();
		ArrayList copy2 = new ArrayList();
		
		for(int i = 0; i < 10; i++) {
			original.add(i + "");
		}
		
		Iterator it = original.iterator();
		
		while(it.hasNext())
			copy1.add(it.next());
		
		System.out.println("= Original에서 copy1로 복사(copy) =");
		System.out.println("original : " + original);
		System.out.println("copy1 : " + copy1);
		System.out.println();
		
		it = original.iterator();	// Iterator는 재사용이 안되므로, 다시 얻어와야 한다.
		
		while(it.hasNext()) {
			copy2.add(it.next());
			it.remove();
		}
		
		System.out.println("= Original에서 copy2로 이동(move) =");
		System.out.println("original : " + original);
		System.out.println("copy2 : " + copy2);
	}	// main
}	// class
```

```
= Original에서 copy1로 복사(copy) =
original : [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
copy1 : [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

= Original에서 copy2로 이동(move) =
original : []
copy2 : [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

다음 예제는 전에 만들었던 예제의 `MyVector`클래스를 상속받는 새로운 클래스가 `Iterator`를 구현하도록 한 것이다.

</br>

예제 11-16 / ch11 / MyVector2.java

``` java
import java.util.*;

public class MyVector2 extends MyVector implements Iterator {
	int cursor = 0;
	int lastRet = -1;
	
	public MyVector2(int capacity) {
		super(capacity);
	}
	
	public MyVector2() {
		this(10);
	}
	
	public String toString() {
		String tmp = "";
		Iterator it = iterator();
		
		for(int i = 0; it.hasNext(); i++) {
			if(i != 0) tmp += ", ";
			tmp += it.next();	// tmp += next().toString();
		}
		return "[" + tmp + "]";
	}
	
	public Iterator iterator() {
		cursor = 0;	// cursor와 lastRet를 초기화 한다.
		lastRet = -1;
		return this;
	}
	
	public boolean hasNext() {
		return cursor != size();
	}
	
	public Object next() {
		Object next = get(cursor);
		lastRet = cursor++;
		return next;
	}
	
	public void remove() {
		// 더 이상 삭제할 것이 없으면 IllegalStateException를 발생시킨다.
		if(lastRet == -1) {
			throw new IllegalStateException();
		} else {
			remove(lastRet);
			cursor--;	// 삭제 후에 cursor의 위치를 감소시킨다.
			lastRet = -1;	// lastRet의 값을 초기화 한다.
		}
	}
}	// class
```

`cursor`는 앞으로 읽어 올 요소의 위치를 저장하는데 사용되고, `lastRet`는 마지막으로 읽어 온 요소의 위치(index)를 저장하는데 사용된다.

그래서 `lastRet`는 `cursor`보다 항상 1이 작은 값이 저장되고 `remove()`를 호출하면 이미 `next()`를 통해서 읽은 위치의 요소, 즉 `lastRet`에 저장된 값의 위치에 있는 요소를 삭제하고 `lastRet`의 값을 -1로 초기화 한다.

만일 `next()`를 호출하지 않고 `remove()`를 호출하면 `lastRet`의 값은 -1이 되어 `IllegalStateException`이 발생한다. `remove()`는 `next()`로 읽어 온 객체를 삭제하는 것이기 때문에 `remove()`를 호출하기 전에는 반드시 `next()`가 호출된 상태이어야 한다.

``` java
public void remove() {
	// 더 이상 삭제할 것이 없으면 IllegalStateException를 발생시킨다.
	if(lastRet == -1) {
		throw new IllegalStateException();
	} else {
		remove(lastRet);	// 최근에 읽어온 요소를 삭제한다.
		cursor--;			// cursor의 위치를 1감소시킨다.
		lastRet = -1;		// 읽어온 요소가 삭제되었으므로 초기화 한다.
	}
}
```

위의 코드에서 보면 `remove(lastRet)`를 호출하여 `lastRet`의 위치에 있는 객체를 삭제한 다음에 `cursor`의 값을 감소시킨다. 그리고 `lastRet`의 값을 초기화(-1)한다.

그 이유는 `remove`메소드를 호출해서 객체를 삭제하고 나면, 삭제된 위치 이후의 객체들이 빈 공간을 채우기 위해 자동적으로 이동되기 때문에 `cursor`의 위치도 같이 이동시켜주어야 한다. 그리고 읽어온 요소가 삭제되었으므로 읽어온 요소의 위치를 저장하는 `lastRet`의 값은 -1로 초기화해야 한다. `lastRet`의 값이 -1이라는 것은 읽어온 값이 없다는 것을 의미한다.

``` java
MyVector2 v = new MyVector2(5);
v.add("0"); v.add("1"); v.add("2"); v.add("3"); v.add("4");
Iterator it = v.iterator();
```

1. 만일 위의 코드와 같이 0~4의 값이 저장되어 있는 MyVector2의 iterator를 얻어왔다면 다음과 같은 그림의 상태일 것이다.

![image](https://ifh.cc/g/hHYFHM.png)

2. 그리고 next()를 두 번 호출하면 다음과 같은 그림이 될 것이다. 첫 번째 요소인 0을 읽고 두 번째 요소인 1까지 읽어 온 상태이다.

![image](https://ifh.cc/g/1Z5zRO.png)

3. remove()를 호출하면, 마지막으로 읽어 온 요소인 1이 삭제된다. 이 때 lastRet의 값은 -1로 초기화 되고 cursor의 값은 1감소된다. 데이터가 삭제되어 다른 데이터들이 한자리씩 이동하였기 때문에 cursor의 위치도 한자리 이동되어야 하는 것이다.

![image](https://ifh.cc/g/bFNAmZ.png)

> lastRet의 값이 -1이라는 것은 읽어 온 값이 없다는 의미이다. remove()는 읽어온 값이 있어야 호출될 수 있다.

</br>

예제 11-17 / ch11 / MyVector2Test.java

``` java
import java.util.*;

public class MyVector2Test {
	public static void main(String[] args) {
		MyVector2 v = new MyVector2();
		v.add("0");
		v.add("1");
		v.add("2");
		v.add("3");
		v.add("4");
		
		System.out.println("삭제 전 : " + v);
		Iterator it = v.iterator();
		it.next();
		it.remove();
		it.next();
		it.remove();
		
		System.out.println("삭제 후 : " + v);
	}
}
```

```
삭제 전 : [0, 1, 2, 3, 4]
삭제 후 : [2, 3, 4]
```

`MyVector2`클래스를 테스트하는 간단한 예제이다. `MyVector2`객체를 생성하고 데이터를 저장한 다음 `Iterator`를 통해서 첫 번째와 두 번째에 저장된 데이터를 삭제한다.

``` java
if(lastRet == -1) {
	throw new IllegalStateException();
} else {
	remove(lastRet);
//	cursor--;	// 주석처리한다.
	lastRet = -1;
}
```

예제 MyVector2.java의 `remove()`에서 위와 같이 주석처리하면, MyVector2Test.java의 실행결과는 다으모가 같이 될 것이다. 0과 1, 첫 번째와 두 번째 요소가 순서대로 삭제되지 않고, 첫 번째와 세 번째 요소인 0과 2가 삭제된 것을 알 수 있다.

삭제 전 : [0, 1, 2, 3, 4]    
삭제 후 : [1, 3, 4]