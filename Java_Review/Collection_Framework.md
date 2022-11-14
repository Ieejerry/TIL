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

</br>

## 1.6 Arrays

`Arrays`클래스에는 배열을 다루는데 유용한 메소드가 정의되어 있다. 같은 기능의 메소드가 배열의 타입만 다르게 오버로딩되어 있어서 많아 보이지만, 실제로는 그리 많지 않다. 아래는 `Arrays`에 정의된 `toString()`인데, 모든 기본형 배열과 참조형 배열 별로 하나씩 정의되어 있다.

> Arrays에 정의된 메소드는 모두 static메소드이다.

``` java
static String toString(boolean[] a)
static String toString(byte[] a)
static String toString(char[] a)
static String toString(short[] a)
static String toString(int[] a)
static String toString(long[] a)
static String toString(float[] a)
static String toString(double[] a)
static String toString(Object[] a)
```

</br>

### 배열의 복사 - copyOf(), copyOfRange()

`copyOf()`는 배열 전체를, `copyOfRange()`는 배열의 일부를 복사해서 새로운 배열을 만들어 반환한다. `copyOfRange()`에 지정된 범위의 끝은 포함되지 않는다.

``` java
int[] arr = {0, 1, 2, 3, 4};
int[] arr2 = Arrays.copyOf(arr, arr.length);	// arr2 = [0, 1, 2, 3, 4]
int[] arr3 = Arrays.copyOf(arr, 3);				// arr3 = [0, 1, 2]
int[] arr4 = Arrays.copyOf(arr, 7);				// arr4 = [0, 1, 2, 3, 4, 0, 0]
int[] arr5 = Arrays.copyOfRange(arr, 2, 4);		// arr5 = [2, 3] ← 4는 불포함
int[] arr6 = Arrays.copyOfRange(arr, 0, 7);		// arr6 = [0, 1, 2, 3, 4, 0, 0]
```

</br>

### 배열 채우기 - fill(), setAll()

`fill()`은 배열의 모든 요소를 지정된 값으로 채운다. `setAll()`은 배열을 채우는데 사용할 함수형 인터페이스를 매개변수로 받는다. 이 메소드를 호출할 때는 함수형 인터페이스를 구현한 객체를 매개변수로 지정하던가 아니면 람다식을 지정해야한다.

``` java
int[] arr = new int[5];
Arrays.fill(arr, 9);	// arr = [9, 9, 9, 9, 9]
Arrays.setAll(arr, () -> (int)(Math.random() * 5) + 1);	// arr = [1, 5, 2, 1, 1]
```

위의 문장에 사용된 `i -> (int)(Math.rondom() * 5) + 1)`은 '람다식(lambda expression)'인데, 1~5의 범위에 속한 임의의 정수를 반환하는 일을 한다. 그리고 `setAll()`메소드는 이 람다식이 반환한 임의의 정수로 배열을 채운다.

</br>

### 배열의 정렬과 검색 - sort(), binarySearch()

`sort()`는 배열을 정렬할 때, 그리고 배열에 저장된 요소를 검색할 때는 `binarySearch()`를 사용한다. `binarySeartch()`는 배열에서 지정된 값이 저장된 위치(index)를 찾아서 반환하는데, 반드시 배열이 정렬된 상태이어야 올바른 결과를 얻는다. 그리고 만일 검색한 값과 일치하는 요소들이 여러 개 있다면, 이 중에서 어떤 것의 위치가 반환될지는 알 수 없다.

``` java
int[] arr = { 3, 2, 0, 1, 4 };
int idx = Arrays.binarySearch(arr, 2);	// idx = -5 ← 잘못된 결과

Arrays.sort(arr);	// 배열의 arr을 정렬한다.
System.out.println(Arrays.toString(arr));	// [ 0, 1, 2, 3, 4 ]
int idx = Arrays.binarySearch(arr, 2);	// idx = 2 ← 올바른 결과
```

배열의 첫 번째 요소부터 순서대로 하나씩 검색을 하는 것을 '순차 검색(linear search)'이라고 하는데, 이 검색 방법은 배열이 정렬되어 있을 필요는 없지만 배열의 요소를 하나씩 비교하기 때문에 시간이 많이 걸린다. 반면에 이진 검색(binary search)은 배열의 검색할 범위를 반복적으로 절반씩 줄여가면서 검색하기 때문에 검색속도가 상당히 빠르다. 배열의 길이가 10배가 늘어나도 검색 횟수는 3~4회 밖에 늘어나지 않으므로 큰 배열의 검색에 유리하다. 단, 배열이 정렬이 되어 있는 경우에만 사용할 수 있다는 단점이 있다.

</br>

### 배열의 비교와 출력 - equals(), toString()

`toString()`배열의 모든 요소를 문자열로 편하게 출력할 수 있다. `toString()`은 일차원 배열에만 사용할 수 있으므로, 다차원 배열에는 `deepToString()`을 사용해야 한다. `deepToString()`은 배열의 모든 요소를 재귀적으로 접근해서 문자열을 구성하므로 2차원뿐만 아니라 3차우너 이상의 배열에도 동작한다.

``` java
int[] arr = { 0, 1, 3, 4 };
int[][] arr2D = {{11, 22}, {21, 22}};

System.out.println(Arrays.toString(arr));	// [0, 1, 2, 3, 4]
System.out.println(Arrays.deepToString(arr2D));	// [[11, 22], [21, 22]]
```

`equals()`는 두 배열에 저장된 모든 요소를 비교해서 같으면 true, 다르면 false를 반환한다. `equals()`도 일차원 배열에만 사용가능하므로, 다차원 배열의 비교에는 `deepEquals()`를 사용해야한다.

``` java
String[][] str2D = new String[][] {{"aaa", "bbb"}, {"AAA", "BBB"}};
String[][] str2D2 = new String[][] {{"aaa", "bbb"}, {"AAA", "BBB"}};

System.out.println(Arrays.equals(str2D, str2D2));		// false
System.out.println(Arrays.deepEquals(str2D, str2D2))	// true
```

위와 같이 2차원 String배열을 `equals()`로 비교하면 배열에 저장된 내요잉 같은데도 false를 결과로 얻는다. 다차원 배열은 '배열의 배열'의 형태로 구성하기 때문에 `equals()`로 비교하면, 문자열을 비교하는 것이 아니라 '배열에 저장된 배열의 주소'를 비교하게 된다. 서로 다른 배열은 항상 주소가 다르므로 false를 결과로 얻는다.

</br>

### 배열을 List로 반환 - asList(Object... a)

`asList()`는 배열을 List에 담아서 반환한다. 매개변수의 타입이 가변인수라서 배열 생성없이 저장할 요소들만 나열하는 것도 가능하다.

``` java
List list = Arrays.asList(new Integer[] { 1, 2, 3, 4, 5 });	// list = [1, 2, 3, 4, 5]
List list = Arrays>asList(1, 2, 3, 4, 5);
list.add(6);	// UnsupportedOperationException 예외 발생
```

한 가지 주의할 점은 `asList()`가 반환한 List의 크기를 변경할 수 없다는 것이다. 즉, 추가 또는 삭제가 불가능하다. 저장된 내용은 변경가능하다. 만일 크기를 변경할 수 없는 List가 필요하다면 다음과 같이 하면 된다.

``` java
List list = new ArrayList(Arrays.asList(1, 2, 3, 4, 5));
```

</br>

### parallelXXX(), spliterator(), stream()

이 외에도, `parallel`로 시작하는 이름의 메소드들이 있는데, 이 메소드들은 보다 빠른 결과를 얻기 위해 여러 쓰레드가 작업을 나누어 처리하도록 한다. `spliterator()`는 여러 쓰레드가 처리할 수 있게 하나의 작업을 여러 작업으로 나누는 `Spliterator`를 반환하며, `stream()`은 컬렉션을 스트림으로 변환한다.

</br>

예제 11-18 / ch11 / ArraysEx.java

``` java
import java.util.*;

public class ArraysEx {
	public static void main(String[] args) {
		int[] arr = {0, 1, 2, 3, 4};
		int[][] arr2D = {{11, 12, 13}, {21, 22, 23}};
		
		System.out.println("arr = " + Arrays.toString(arr));
		System.out.println("arr2D = " + Arrays.deepToString(arr2D));
		
		int[] arr2 = Arrays.copyOf(arr, arr.length);
		int[] arr3 = Arrays.copyOf(arr, 3);
		int[] arr4 = Arrays.copyOf(arr, 7);
		int[] arr5 = Arrays.copyOfRange(arr, 2, 4);
		int[] arr6 = Arrays.copyOfRange(arr, 0, 7);
		
		System.out.println("arr2 = " + Arrays.toString(arr2));
		System.out.println("arr2 = " + Arrays.toString(arr3));
		System.out.println("arr2 = " + Arrays.toString(arr4));
		System.out.println("arr2 = " + Arrays.toString(arr5));
		System.out.println("arr2 = " + Arrays.toString(arr6));
		
		int[] arr7 = new int[5];
		Arrays.fill(arr7, 9);	// arr={9, 9, 9, 9, 9}
		System.out.println("arr7 = " + Arrays.toString(arr7));
		
		Arrays.setAll(arr7, i -> (int)(Math.random() * 6) + 1);
		System.out.println("arr7 = " + Arrays.toString(arr7));
		
		for(int i : arr7) {
			char[] graph = new char[i];
			Arrays.fill(graph, '*');
			System.out.println(new String(graph) + i);
		}
		
		String[][] str2D = new String[][] {{"aaa", "bbb"}, {"AAA","BBB"}};
		String[][] str2D2 = new String[][] {{"aaa", "bbb"}, {"AAA","BBB"}};
		
		System.out.println(Arrays.equals(str2D, str2D2));	// false
		System.out.println(Arrays.deepEquals(str2D, str2D2));	// true
		
		char[] chArr = { 'A', 'D', 'C', 'B', 'E' };
		
		System.out.println("chArr = " + Arrays.toString(chArr));
		System.out.println("index of B = " + Arrays.binarySearch(chArr, 'B'));
		System.out.println("= After sorting =");
		Arrays.sort(chArr);
		System.out.println("chArr = " + Arrays.toString(chArr));
		System.out.println("index of B = " + Arrays.binarySearch(chArr, 'B'));
	}
}
```

```
arr = [0, 1, 2, 3, 4]
arr2D = [[11, 12, 13], [21, 22, 23]]
arr2 = [0, 1, 2, 3, 4]
arr2 = [0, 1, 2]
arr2 = [0, 1, 2, 3, 4, 0, 0]
arr2 = [2, 3]
arr2 = [0, 1, 2, 3, 4, 0, 0]
arr7 = [9, 9, 9, 9, 9]
arr7 = [6, 5, 5, 2, 3]
******6
*****5
*****5
**2
***3
false
true
chArr = [A, D, C, B, E]
index of B = -2
= After sorting =
chArr = [A, B, C, D, E]
index of B = 1
```

</br>

## 1.7 Comparator와 Comparable

`Arrays.sort()`를 호출만 하면 컴퓨터가 알아서 배열을 정렬하는 것처럼 보이지만, 사실은 `Chacter`클래스의 `Comparable`의 구현에 의해 정렬된다.

`Comparator`와 `Comparable`은 모두 인터페이스로 컬렉션을 정렬하는데 필요한 메소드를 정의하고 있으며, `Comparable`을 구현하고 있는 클래스들은 같은 타입의 인스턴스끼리 서로 비교할 수 있는 클래스들, 주로 `Integer`와 같은 wrapper클래스와 `String`, `Date`, `File`과 같은 것들이며 기본적으로 오름차순, 즉 작은 값에서부터 큰 값의 순으로 정렬되도록 구현되어 있다. 그래서 `Comparable`을 구현한 클래스는 정렬이 가능하다는 것을 의미한다. `Comparator`와 `Comparable`의 실제 소스는 다음과 같다.

``` java
public interface Comparator {
	int compare(Object o1, Object o2);
	boolean equals(Object obj);
}

public interface Comparable {
	public int comparaTo(Object o);
}
```

> Comparable은 java.lang패키지에 있고, Comparator는 java.util패키지에 있다.

`compare()`와 `compareTo()`는 선언형태와 이름이 약간 다를 뿐 두 객체를 비교한다는 같은 기능을 목적으로 고안된 것이다. `compareTo()`의 반환값은 int이지만 실제로는 비교하는 두 객체가 같으면 0, 비교하는 값보다 작으면 음수, 크면 양수를 반환하도록 구현해야 한다. 이와 마찬가지로 `compare()`도 객체를 비교해서 음수, 0, 양수 중의 하나를 반환하도록 구현해야한다.

`equals`메소드는 모든 클래스가 가지고 있는 공통적인 메소드이지만, `Comparator`를 구현하는 클래스는 오버라이딩이 필요할 수도 있다는 것을 알리기 위해서 정의한 것일 뿐, 그냥 `compare(Object o1, Object o2)`만 구현하면 된다.

``` java
public final class Integer extends Number implements Comparable {
	...
	public int comparaTo(Object o) {
		return compareTo((Integer)o);
	}

	public int compareTo(Integer anotherInteger) {
		int thisVal = this.value;
		int anotherVal = anotherInteger.value;

		// 비교하는 값이 크면 -1, 같으면 0, 작으면 1을 반환한다.
		return (thisVal < anotherVal ? -1 : (thisVal == anotherVal ? 0 : 1));
	}
}
```

위의 코드는 `Integer`클래스의 일부이다. `Comparable`의 `compareTo(Object o)`를 구현해 놓은 것을 볼 수 있다. 두 `Integer`객체에 저장된 int값(value)을 비교해서 같으면 0, 크면 -1, 작으면 1을 반환하는 것을 알 수 있다.

`Comparable`을 구현한 클래스들이 기본적으로 오름차순으로 정렬되어 있지만, 내림차순으로 정렬한다던가 아니면 다른 기준에 의해서 정렬되도록 하고 싶을 때 `Comparator`를 구현해서 정렬기준을 제공할 수 있다.

> **Comparable** 기본 정렬기준을 구현하는데 사용.   
**Comparator** 기본 정렬기준 외에 다른 기준으로 정렬하고자할 때 사용

</br>

예제 11-19 / ch11 / ComparatorEx.java

``` java
import java.util.*;

public class ComparatorEx {
	public static void main(String[] args) {
		String[] strArr = {"cat", "Dog", "lion", "tiger"};
		
		Arrays.sort(strArr);	// String의 Comparable구현에 의한 정렬
		System.out.println("strArr = " + Arrays.toString(strArr));
		
		Arrays.sort(strArr, String.CASE_INSENSITIVE_ORDER);	// 대소문자 구분안함
		System.out.println("strArr = " + Arrays.toString(strArr));
		
		Arrays.sort(strArr, new Descending());	// 역순 정렬
		System.out.println("strArr = " + Arrays.toString(strArr));
	}
}

class Descending implements Comparator {
	public int compare(Object o1, Object o2) {
		if(o1 instanceof Comparable && o2 instanceof Comparable) {
			Comparable c1 = (Comparable)o1;
			Comparable c2 = (Comparable)o2;
			return c1.compareTo(o2) * -1;	// -1을 곱해서 기본 정렬방식의 역으로 변경한다.
									// 또는 c2.compareTo(c1)와 같이 순서를 바꿔도 된다.
		}
		return -1;
	}
}
```

```
strArr = [Dog, cat, lion, tiger]
strArr = [cat, Dog, lion, tiger]
strArr = [tiger, lion, cat, Dog]
```

`Arrays.sort()`는 배열을 정의할 때, `Comparator`를 지정해주지 않으면 저장하는 객체(주로 Comparable을 구현한 클래스의 객체)에 구현된 내용에 따라 정렬된다.

``` java
static void sort(Object[] a)	// 객체 배열에 저자오딘 객체가 구현한 Comparable에 의한 정렬
static void sort(Object[] a, Comparator c)	// 지정한 Comparator에 의한 정렬
```

`String`의 `Comparable`구현은 문자열이 사전 순으로 정렬되도록 작성되어 있다. 문자열의 오름차순 정렬은 공백, 숫자, 대문자, 소문자의 순으로 정렬되는 것을 의미한다. 정확히 얘기하면 문자의 유니코드의 순서가 작은 값에서부터 큰 값으로 정렬되는 것이다.

그리고 아래와 같이 대소문자를 구분하지 않고 비교하는 `Comparator`를 상수의 형태로 제공한다.

``` java
public static final Comparator CASE_INSENSITIVE_ORDER
```

이 `Comparator`를 이용하면, 문자열을 대소문자로 구분없이 정렬할 수 있다.

``` java
Arrays.sort(strArr, String.CASE_INSENSITIVE_ORDER);	// 대소문자를 구분없이 정렬
```

`String`의 기본 정렬을 반대로 하는 것, 즉 문자열을 내림차순(descending order)을 구현하는 것은 아주 간단하다. 단지 `String`에 구현된 `compareTo()`의 결과에 -1을 곱하기만 하면 된다. 또는 비교하는 객체의 위치를 바꿔서 `c2.compareTo(c1)`과 같이 해도 된다.

다만 `compare()`의 매개변수가 `Object`타입이기 때문에 `compareTo()`를 바로 호출할 수 없으므로 먼저 `Comparable`로 형변환해야 한다.

``` java
class Descending implements Comparator {
	public int compare(Object o1, Object o2) {
		if(o1 instanceof Comparable && o2 instanceof Comparable) {
			Comparable c1 = (Comparable)o1;
			Comparable c2 = (Comparable)o2;
			return c1.compareTo(c2) * -1;	// 기본 정렬방식의 역으로 변경한다.
		}
		return -1;
	}
}
```

</br>

## 1.8 HashSet

`HashSet`은 `Set`인터페이스를 구현한 가장 대표적인 컬렉션이며, `Set`인터페이스의 특징대로 `HashSet`은 중복된 요소를 저장하지 않는다.

`ArrayList`와 같이 `List`인터페이스를 구현한 컬렉션과 달리 `HashSet`은 저장순서를 유지하지 않으므로 저장순서를 유지하고자 한다면 `LinkedHashSet`을 사용해야한다.

> HashSet은 내부적으로 HashMap을 이용해서 만들어졌으며, HashSet이란 이름은 해싱(hasing)을 이용해서 구현했기 때문에 붙여진 것이다.

![image](https://ifh.cc/g/jyy3VS.png)

> load factor는 컬렉션 클래스에 저장공간이 가득 차기 전에 미리 용량을 확보하기 위한 것으로 이 값을 0.8로 지정하면, 저장공간의 80%가 채워졌을 때 용량이 두 배로 늘어난다. 기본값은 0.75, 즉 75%이다.

</br>

예제 11-20 / ch11 / hashSetEx1.java

``` java
import java.util.*;

public class HashSetEx1 {
	public static void main(String[] args) {
		Object[] objArr = {"1", new Integer(1), "2", "2", "3", "3", "4", "4", "4"};
		Set set = new HashSet();
		
		for(int i = 0; i < objArr.length; i++) {
			set.add(objArr[i]);	// HashSet에 objArr의 요소들을 저장한다.
		}
		
		// HashSet에 저장된 요소들을 출력한다.
		System.out.println(set);
	}
}
```

```
[1, 1, 2, 3, 4]
```

결과에서 알 수 있듯이 중복된 값은 저장되지 않았다. `add`메소드는 객체를 추가할 때 `HashSet`에 이미 같은 객체가 있으면 중복으로 간주하고 저장하지 않는다. 그리고는 작업이 실패했다는 의미로 false를 반환한다.

'1'이 두 번 출력되었는데, 둘 다 '1'로 보이기 때문에 구별이 안 되지만, 사실 하나는 `String`인스턴스이고 다른 하나는 `Integer`인스턴스로 서로 다른 객체이므로 중복을오 간주하지 않는다.

`Set`을 구현한 컬렉션 클래스는 `List`를 구현한 컬렉션 클래스와 달리 순서를 유지하지 않기 때문에 저장한 순서와 다를 수 있다.

만일 중복을 제거하는 동시에 저장한 순서를 유지하고자 한다면 `HashSet`대신 `LinkedHashSet`을 사용해야한다.

</br>

예제 11-21 / ch11 / HashSetLotto.java

``` java
import java.util.*;

public class HashSetLotto {
	public static void main(String[] args) {
		Set set = new HashSet();
		
		for(int i = 0; set.size() < 6; i++) {
			int num = (int)(Math.random() * 45) + 1;
			set.add(new Integer(num));
		}
		
		List list = new LinkedList(set);	// LinkedList(Collection c)
		Collections.sort(list);	// Collections.sort(List list)
		System.out.println(list);
	}
}
```

```
[12, 16, 26, 41, 44, 45]
```

번호를 크기순으로 정렬하기 위해서 `Collections`클래스의 `sort(List list)`를 사용했다. 이 메소드는 인자로 `List`인터페이스 타입을 필요로 하기 때문에 `LinkedList`클래스의 생성자 `LinkedList(Collection c)`를 이용해서 `HashSet`에 저장된 객체들을 `LinkedList`에 담아서 처리했다.

실행결과의 정렬기준은, 컬렉션에 저장된 객체가 `Integer`이기 때문에 `Integer`클래스에 정의된 기본정렬이 사용되었다.

> Collection은 인터페이스고 Collections는 클래스임에 주의해야 한다.

</br>

예제 11-22 / ch11 / Bingo.java

``` java
import java.util.*;

public class Bingo {
	public static void main(String[] args) {
		Set set = new HashSet();
//		Set set = new LinkedHashSet();
		int[][] board = new int[5][5];
		
		for(int i = 0; set.size() < 25; i++) {
			set.add((int)(Math.random() * 50) + 1 + "");
		}
		
		Iterator it = set.iterator();
		
		for(int i = 0; i < board.length; i++) {
			for(int j = 0; j < board[i].length; j++) {
				board[i][j] = Integer.parseInt((String)it.next());
				System.out.print((board[i][j] < 10 ? "  " : " ") + board[i][j]);
			}
			System.out.println();
		}
	}	// main
}
```

```
 44 23 46 24 26
 49 27 29 30 10
 35 13 36 14 39
 18  1  4  7  8
  9 41 20 42 43
```

1~50사이의 숫자 중에서 25개를 골라서 '5X5'크기의 빙고판을 만드는 예제이다. `next()`는 반환값이 `Object`타입이므로 형변환해서 원래의 타입으로 되돌려 놓아야 한다.

그런데 몇번 실행해보면 같은 숫자가 비슷한 위치에 나온다는 사실을 발견할 수 있을 것이다. 앞서 언급한 것과 같이 `HashSet`은 저장된 순서를 보장하지 않고 자체적인 저장방식에 따라 순서가 결정되기 때문이다.

</br>

예제 11-23 / ch11 / HashSetEx3.java

``` java
import java.util.*;

public class HashSetEx3 {
	public static void main(String[] args) {
		HashSet set = new HashSet();
		
		set.add("abc");
		set.add("abc");
		set.add(new Person("David", 10));
		set.add(new Person("David", 10));
		
		System.out.println(set);
	}
}

class Person {
	String name;
	int age;
	
	Person(String name, int age) {
		this.name = name;
		this.age = age;
	}
	
	public String toString() {
		return name + " : " + age;
	}
}
```

```
[abc, David : 10, David : 10]
```

`Person`클래스는 `name`과 `age`를 멤버변수로 갖는다. 이름(name)과 나이(age)가 같으면 같은 사람으로 인식하도록 하려는 의도로 작성하였다. 하지만 실행결과를 보면 두 인스턴스의 `name`과 `age`의 값이 같음에도 불구하고 서로 다른 것으로 인식하여 'David:10'이 두 번 출력되었다.

</br>

예제 11-24 / ch11 / HashSetEx4.java

``` java
import java.util.*;

public class HashSetEx4 {
	public static void main(String[] args) {
		HashSet set = new HashSet();
		
		set.add(new String("abc"));
		set.add(new String("abc"));
		set.add(new Person2("David", 10));
		set.add(new Person2("David", 10));
		
		System.out.println(set);
	}
}

class Person2 {
	String name;
	int age;
	
	Person2(String name, int age) {
		this.name = name;
		this.age = age;
	}
	
	public boolean equals(Object obj) {
		if(obj instanceof Person2) {
			Person2 tmp = (Person2)obj;
			return name.equals(tmp.name) && age == tmp.age;
		}
		return false;
	}
	
	public int hashCode() {
		return (name+age).hashCode();
	}
	
	public String toString() {
		return name + " : " + age;
	}
}
```

```
[abc, David : 10]
```

`HashSet`의 `add`메소드는 새로운 요소를 추가하기 전에 기존에 저장된 요소와 같은 것인지 판별하기 위해 추가하려는 요소의 `equals()`와 `hashCode()`를 호출하기 때문에 `equals()`와 `hashCode()`를 목적에 맞게 오버라이딩해야 한다.

그래서 `String`클래스에서 같은 내용의 문자열에 대한 `equals()`의 호출결과가 true인 것과 같이, `Person2`클래스에서도 두 인스턴스의 `name`과 `age`가 서로 같으면 true를 반환하도록 `equals()`를 오버라이딩했다. 그리고 `hashCode()`는 `String`클래스의 `hashCode()`를 이용해서 구현했다. `String`클래스의 `hashCode()`는 잘 구현되어 있기 때문에 이를 활용하면 간단히 처리할 수 있다.

``` java
public int hashCode() {
	return (name+age).hashCode()
}
```

위의 코드를 JDK1.8부터 추가된 `java.util.Objects`클래스의 `hash()`를 이용해서 작성하면 아래와 같다. 이 메소드의 괄호 안에 클래스의 인스턴스 변수들을 넣으면 된다. 이전의 코드와 별반 다르지 않지만, 가능하면 아래의 코드를 사용하는 것이 좋다.

``` java
public int hashCode() {
	return Objects.hash(name, age);	// int hash(Object... value)
}
```

오버라이딩을 통해 작성된 `hashCode()`는 다음의 세 가지 조건을 만족 시켜야 한다.

1. 실행 중인 애플리케이션 내의 동일한 객체에 대해서 여러 번 hashCode()를 호출해도 동일한 int값을 반환해야한다. 하지만, 실행시마다 동일한 int값을 반환할 필요는 없다. (단, equals메소드의 구현에 사용된 멤버변수와 값이 바뀌지 않았다고 가정한다.)

예를 들어 `Person2`클래스의 `equals`메소드에 사용된 멤버변수 `name`과 `age`의 값이 바뀌지 않는 한, 하나의 `Person2`인스턴스에 대해 `hashCode()`를 여러 번 호출했을 때 항상 같은 int값을 얻어야 한다.

``` java
Person2 p = new Person2("David", 10);

int hashCode1 = p.hashCode();
int hashCode2 = p.hashCode();

p.age = 20;
int hashCode3 = p.hashCode();
```

위의 코드에서 `hashCode1`의 값과 `hashCode2`의 값은 항상 일치해야하지만 이 두 값이 매번 실행할 때마다 반드시 같은 값일 필요는 없다. `hashCode3`은 `equals`메소드에 사용된 멤버변수 `age`를 변경한 후에 `hashCode`메소드를 호출한 결과이므로 `hashCode1`이나 `hashCode2`와 달라도 된다.

> String클래스는 문자열의 내용으로 해시코드를 만들어 내기 때문에 내용이 같은 문자열에 대한 hashCode() 호출은 항상 동일한 해시코드를 반환한다. 반면에 Object클래스는 객체의 주소로 해시코드를 만들어 내기 때문에 실행할 때마다 해시코드값이 달라질 수 있다.

2. equals메소드를 이용한 비교에 의해서 true를 얻은 두 객체에 대해 각각 hashCode()를 호출해서 얻은 결과는 반드시 같아야 한다.

인스턴스 `p1`과 `p2`에 대해서 `equals`메소드를 이용한 비교의 결과인 변수 `b`의 값이 true라면, `hashCode1`과 `hashCode2`의 값은 같아야 한다는 뜻이다.

``` java
Person2 p1 = new Person2("David", 10);
Person2 p2 = new Person2("David", 10);

boolean b = p1.equals(p2);

int hashCode1 = p1.hashCode();
int hashCode2 = p2.hashCode();
```

3. equals메소드를 호출했을 때 false를 반환하는 두 객체는 `hashCode()`호출에 대해 같은 int값을 반환하는 경우가 있어도 괜찮지만, 해싱(hashing)을 사용하는 컬렉션의 성능을 향상시키기 위해서는 다른 int값을 반환하는 것이 좋다.

위의 코드에서 변수 `b`의 값이 false일지라도 `hashCode1`과 `hashCode2`의 값이 같은 경우가 발생하는 것을 허용한다. 하지만, 해시코드를 사용하는 `Hashtable`이나 `HashMap`과 같은 컬렉션의 성능을 높이기 위해서는 가능한 한 서로 다른 값을 반환하도록 `hashCode()`를 잘 작성해야 한다는 뜻이다.

서로 다른 객체에 대해서 해시코드값(hashCode()를 호출한 결과)이 중복되는 경우가 많이질수록 해싱을 사용하는 `Hashtable`, `HashMap`과 같은 컬렉션의 검색속도가 떨어진다.

두 객체에 대해 `equals`메소드를 호출한 결과가 true이면, 두 객체의 해시코드는 반드시 같아야하지만, 두 객체의 해시코드가 같다고 해서 `equals`메소드의 호출결과가 반드시 true이어야 하는 것은 아니다.

</br>

예제 11-25 / ch11 / HashSetEx5.java

``` java
import java.util.*;

public class HashSetEx5 {
	public static void main(String[] args) {
		HashSet setA = new HashSet();
		HashSet setB = new HashSet();
		HashSet setHab = new HashSet();
		HashSet setKyo = new HashSet();
		HashSet setCha = new HashSet();
		
		setA.add("1");	setA.add("2");	setA.add("3");
		setA.add("4");	setA.add("5");
		System.out.println("A = " + setA);
		
		setB.add("4");	setB.add("5");	setB.add("6");
		setB.add("7");	setB.add("8");
		System.out.println("B = " + setB);
		
		Iterator it = setB.iterator();
		while(it.hasNext()) {
			Object tmp = it.next();
			if(setA.contains(tmp))
				setKyo.add(tmp);
		}
		
		it = setA.iterator();
		while(it.hasNext()) {
			Object tmp = it.next();
			if(!setB.contains(tmp))
				setCha.add(tmp);
		}
		
		it = setA.iterator();
		while(it.hasNext()) {
			setHab.add(it.next());
		}
		
		it = setB.iterator();
		while(it.hasNext()) {
			setHab.add(it.next());
		}
		
		System.out.println("A ∩ B = " + setKyo);	// 한글 ㄷ을 누르고 한자키
		System.out.println("A ∪ B = " + setHab);		// 한글 ㄷ을 누르고 한자키
		System.out.println("A - B = " + setCha);
	}
}
```

```
A = [1, 2, 3, 4, 5]
B = [4, 5, 6, 7, 8]
A ∩ B = [4, 5]
A ∪ B = [1, 2, 3, 4, 5, 6, 7, 8]
A - B = [1, 2, 3]
```

이 예제는 두 개의 `HashSet`에 저장된 객체들을 비교해서 합집합, 교집합, 차집합을 구하는 방법을 보여준다. 사실은 `Set`은 중복을 허용하지 않으므로 `HashSet`의 메소드를 호출하는 것만으로도 간단하게 합집합(addAll), 교집합(retainAll), 차집합(removeAll)을 구할 수 있다.

</br>

## 1.9 TreeSet

`TreeSet`은 이진 검색 트리(binary search tree)라는 자료구조의 형태로 데이터를 저장하는 컬렉션 클래스이다. 이진 검색 트리는 정렬, 검색, 범위검색(range search)에 높은 성능을 보이는 자료구조이며 `TreeSet`은 이진 검색 트리의 성능을 향상시킨 '레드-블랙 트리(Red-Black tree)'로 구현되어 있다.

그리고 `Set`인터페이스를 구현했으므로 **중복된 데이터의 저장을 허용하지 않으며 정렬된 위치에 저장하므로 저장순서를 유지하지도 않는다.**

이진 트리(binary tree)는 링크드리스트처럼 여러 개의 노드(node)가 서로 연결된 구조로, 각 노드에 최대 2개의 노드를 연결할 수 있으며 '루트(root)'라고 불리는 하나의 노드에서부터 시작해서 계속 확장해 나갈 수 있다.

위 아래로 연결된 두 노드를 '부모-자식관계'에 있다고 하며 위의 노드를 부모 노드, 아래의 노드를 자식 노드라 한다. 부모-자식관계는 상대적인 것이며 하나의 부모 노드는 최대 ㅊ두 개의 자식 노드와 연결될 수 있다.

아래의 그림에서 A는 B와 C의 부모 노드이고, B와 C는 A의 자식 노드이다.

> 트리(tree)는 각 노드간의 연결된 모양이 나무와 같다고 해서 붙여진 이름이다.

![image](https://ifh.cc/g/GCaoGM.png)

이진 트리의 노드를 코드로 표현하면 다음과 같다.

``` java
class TreeNode {
	TreeNode left;	// 왼쪽 자식노드
	Object element;	// 객체를 저장하기 위한 참조변수
	TreeNode right;	// 오른쪽 자식노드
}
```

데이터를 저장하기 위한 `Object`타입의 참조변수 하나와 두 개의 노드를 참조하기 위한 두 개의 참조변수를 선언했다.

이진 검색 트리(binary search tree)는 부모노드의 왼쪽에는 부모노드의 값보다 작은 값의 자식노드를 오른쪽에는 큰 값의 자식노드를 저장하는 이진 트리이다.

예를 들어 데이터를 5, 1, 7의 순서로 저장한 이진 트리의 구조는 아래와 같이 표현할 수 있다. 실제로는 오른쪽 그림과 같이 표현해야 한다.

![image](https://ifh.cc/g/0pFBz5.png)

예를 들어 이진검색트리에 7, 4, 9, 1, 5의 순서로 값을 저장한다고 가정하면 다음과 같은 순서로 진행된다.

![image](https://ifh.cc/g/OQrHlO.png)

첫 번째로 저장되는 값은 루트가 되고, 두 번째 값은 트리의 루트부터 시작해서 값의 크기를 비교하면서 트리를 따라 내려간다. 작은 값은 왼쪽에 큰 값은 오른쪽에 저장한다. 이렇게 트리를 구성하면, 왼쪽 마지막 레벨이 제일 작은 값이 되고 오른쪽 마지막 레벨의 값이 제일 큰 값이 된다. 컴퓨터는 알아서 값을 비교하지 못한다.

`TreeSet`에 저장되는 객체가 `Comparable`을 구현하던가 아니면, `TreeSet`에게 `Comparator`를 제공해서 두 객체를 비교할 방법을 알려줘야 한다. 그렇지 않으면, `TreeSet`에 객체를 저장할 때 예외가 발생한다.

왼쪽 마지막 값에서부터 오른쪽 값까지 값을 '왼쪽 노드 → 부모 노드 → 오른쪽 노드'순으로 읽어오면 오름차순으로 정렬된 순서를 얻을 수 있다. `TreeSet`은 이처럼 정렬된 상태를 유지하기 때문에 단일 값 검색과 범위검색(range search)이 매우 빠르다.

저장된 값의 개수에 비례해서 검색시간이 증가하긴 하지만 값의 개수가 10배 증가해도 특정 값을 찾는데 필요한 비교횟수가 3~4번만 증가할 정도로 검색효율이 뛰어난 자료구조이다.

트리는 데이터를 순차적으로 저장하는 것이 아니라 저장위치를 찾아서 저장해야하고, 삭제하는 경우 트리의 일부를 재구성해야하므로 링크드 리스트보다 데이터 추가/삭제 시간은 더 걸린다. 대신 배열이나 링크드 리스트에 비해 검색과 정렬기능이 더 뛰어나다.

> **이진 검색 트리(binary search tree)는**
> - 모든 노드는 최대 두 개의 자식노드를 가질 수 있다.
> - 왼쪽 자식노드의 값은 부모노드의 값보다 작고 오른쪽 자식노드의 값은 부모노드의 값보다 커야한다.
> - 노드의 추가 삭제에 시간이 걸린다.(순차적으로 저장하지 않으므로)
> - 검색(범위검색)과 정렬에 유리하다.
> - 중복된 값을 저장하지 못한다.

![image](https://ifh.cc/g/FPAoJf.png)

</br>

예제 11-26 / ch11 / TreeSetLotto.java

``` java
import java.util.*;

public class TreeSetLotto {
	public static void main(String[] args) {
		Set set = new TreeSet();
		
		for(int i = 0; set.size() < 6; i++) {
			int num = (int)(Math.random() * 45) + 1;
			set.add(num);	// set.add(new Integer(num));
		}
		
		System.out.println(set);
	}
}
```

```
[1, 16, 18, 36, 38, 43]
```

이전의 예제 11-21 HashSetLotto.java를 `TreeSet`을 사용해서 바꾸었다. 이전 예제와는 달리 정렬하는 코드가 빠져 있는데, `TreeSet`은 저장할 때 이미 정렬하기 때문에 읽어올 때 따로 정렬할 필요가 없기 때문이다.

</br>

예제 11-27 / ch11 / TreeSetEx1.java

``` java
import java.util.*;

public class TreeSetEx1 {
	public static void main(String[] args) {
		TreeSet set = new TreeSet();
		
		String from = "b";
		String to = "d";
		
		set.add("abc");		set.add("alien");	set.add("bat");
		set.add("car");		set.add("Car");		set.add("disc");
		set.add("dance");	set.add("dZZZZ");	set.add("dzzzz");
		set.add("elephant");set.add("elevator");set.add("fan");
		set.add("flower");
		
		System.out.println(set);
		System.out.println("range search : from " + from + " to " + to);
		System.out.println("result1 " + set.subSet(from, to));
		System.out.println("result2 " + set.subSet(from, to + "zzz"));
	}
}
```

```
[Car, abc, alien, bat, car, dZZZZ, dance, disc, dzzzz, elephant, elevator, fan, flower]
range search : from b to d
result1 [bat, car]
result2 [bat, car, dZZZZ, dance, disc]
```

`subSet()`을 이용해서 범위검색(range search)할 때 시작범위는 포함되지만 끝 범위는 포함되지 않으므로 `result1`에는 c로 시작하는 단어까지만 검색결과에 포함되어 있다.

만일 끝 범위인 d로 시작하는 단어까지 포함시키고자 한다면, 아래와 같이 끝 범위에 'zzz'와 같은 문자열을 붙이면 된다.

``` java
System.out.println("result2 " + set.subSet(from, to + "zzz"));
```

d로 시작하는 단어 중에서 'dzzz' 다음에 오는 단어는 없을 것이기 때문에 d로 시작하는 모든 단어들이 포함된다.

결과를 보면 `abc`보다 `Car`가 앞에 있고 `dZZZZ`가 `dance`보다 앞에 정렬되어 있는 것을 알 수 있다. 대문자가 소문자보다 우선하기 때문에 대소문자가 섞여 있는 경우 의되한 것과는 다른 범위검색결과를 얻을 수 있다.

그래서 가능하면 대문자 또는 소문자로 통일해서 저장하는 것이 좋다.

> 반드시 대소문자가 섞여 있어야 하거나 다른 방식으로 정렬해야하는 경우 Comparator를 이용하면 된다.

문자열의 경우 정렬순서는 문자의 코드값이 기준이 되므로, 오름차순 정렬의 경우 코드값의 크기가 작은 순서에서 큰 순서, 즉 공백, 숫자, 대문자, 소문자 순으로 정렬되고 내림차순의 경우 그 반대가 된다.

</br>

예제 11-28 / ch11 / AsciiPrint.java

``` java
import java.util.*;

public class AsciiPrint {
	public static void main(String[] args) {
		char ch = ' ';
		// 공백(' ')이후의 문자들을 출력한다.
		for(int i = 0; i < 95; i++)
			System.out.print(ch++);
	}
}
```

```
 !"#$%&'()*+,-./0123456789:;<=>?@ABCDEFGHIJKLMNOPQRSTUVWXYZ[\]^_`abcdefghijklmnopqrstuvwxyz{|}~
```

</br>

예제 11-29 / ch11 / TreeSetEx2.java

``` java
import java.util.*;

public class TreeSetEx2 {
	public static void main(String[] args) {
		TreeSet set = new TreeSet();
		int[] score = {80, 95, 50, 35, 45, 65, 10, 100};
		
		for(int i = 0; i < score.length; i++)
			set.add(new Integer(score[i]));
		
		System.out.println("50보다 작은 값 : " + set.headSet(new Integer(50)));
		System.out.println("50보다 큰 값 : " + set.tailSet(new Integer(50)));
	}
}
```

```
50보다 작은 값 : [10, 35, 45]
50보다 큰 값 : [50, 65, 80, 95, 100]
```

`headSet`메소드와 `tailSet`메소드를 이용하면, `TreeSet`에 저장된 객체 중 지정된 기준 값보다 큰 값의 객체들과 작은 값의 객체들을 얻을 수 있다.

예제에 사용된 값들로 이진 검색 트리를 구성해 보면 다음 그림과 같다.

![image](https://ifh.cc/g/MahC0z.png)

위의 그림을 보면 50이 저장된 노드의 왼쪽노드와 그 아래 연결된 모든 노드의 값은 50보다 작고, 나머지 다른 노드의 값들은 50보다 같거나 크다는 것을 알 수 있다.

</br>

## 1.10 HashMap과 Hashtable

`Hashtable`과 `HashMap`의 관계는 `Vector`와 `ArrayList`의 관계와 같아서 `Hashtable`보다는 새로운 버전인 `HashMap`을 사용하는 것이 좋다.

`HashMap`은 `Map`을 구현했으므로 앞에서 살펴본 `Map`의 특징, 키(key)와 값(value)을 묶어서 하나의 데이터(entry)로 저장한다는 특징을 갖는다. 그리고 해싱(hashing)을 사용하기 때문에 많은 양의 데이터를 검색하는데 있어서 뛰어난 성능을 보인다.

`HashMap`이 데이터를 어떻게 저장하는지 확인하기 위해 실제소스의 일부를 보겠다.

``` java
public class HashMap extends AbstractMap implements Map, Cloneable, Serializable {
	transient Entry[] table;
		...
	static class Entry implements Map.Entry {
		final Object key;
		Object value;
			...
	}
}
```

`HashMap`은 `Entry`라는 내부 클래스를 정의하고, 다시 `Entry`타입의 배열을 선언하고 있다. 키(key)와 값(value)은 별개의 값이 아니라 서로 관련된 값이기 때문에 각각의 배열로 선언하기 보다는 하나의 클래스로 정의해서 하나의 배열로 다루는 것이 데이터의 무결성(integrity)적인 측면에서 더 바림직하기 때문이다.

![image](https://ifh.cc/g/BcKOoh.png)

> Map.Entry는 Map인터페이스에 정의된 'static inner interface'이다.

`HashMap`은 키와 값을 각각 Object타입으로 저장한다. 즉 (Object, Object)의 형태로 저장하기 때문에 어떠한 객체도 저장할 수 있지만 키는 주로 String을 대문자 또는 소문자로 통일해서 사용하곤 한다.

> **키(key)** 컬렉션 내의 키(key) 중에서 유일해야 한다.   
> **값(value)** 키(key)와 달리 데이터의 중복을 허용한다.

키는 저장한 값을 찾는데 사용되는 것이기 때문에 컬렉션 내에서 유일(unique)해야 한다. 즉, `HashMap`에 저장된 데이터를 하나의 키로 검색했을 때 결과가 단 하나이어야 함을 뜻한다. 만일 하나의 키에 대해 여러 검색결과과 값을 얻는다면 원하는 값이 어떤 값인지 알 수 없기 때문이다.

예를 들어 사용자ID가 키(key)로, 비밀번호가 값(value)으로 연결되어 저장된 데이터집합이 있다고 가정한다면, 로그인 시에 비밀번호를 확인하기 위해서 입력된 사용자ID에 대한 비밀번호를 검색했을 때, 단 하나의 결과를 얻어야만 올바른 비밀번호를 입력했는지 확인이 가능하다. 만일 하나의 사용자ID에 대해서 두 개 이상의 비밀번호를 얻는다면 어떤 비밀번호가 맞는 것인지 알 수 없다.

![image](https://ifh.cc/g/axNn8S.png)

</br>

예제 11-30 / ch11 / HashMapEx1.java

``` java
import java.util.*;

public class HashMapEx1 {
	public static void main(String[] args) {
		HashMap map = new HashMap();
		map.put("myId", "1234");
		map.put("asdf", "1111");
		map.put("asdf", "1234");
		
		Scanner s = new Scanner(System.in);	// 화면으로부터 라인단위로 입력받는다.
		
		while(true) {
			System.out.println("id와 password를 입력해주세요.");
			System.out.print("id : ");
			String id = s.nextLine().trim();
			
			System.out.print("password : ");
			String password = s.nextLine().trim();
			System.out.println();
			
			if(!map.containsKey(id)) {
				System.out.println("입력하신 id는 존재하지 않습니다. 다시 입력해주세요.");
				continue;
			}
			
			if(!(map.get(id)).equals(password)) {
				System.out.println("비밀번호가 일치하지 않습니다. 다시 입력해주세요.");
			} else {
				System.out.println("id와 비밀번호가 일치합니다.");
				break;
			}
		}	// while
	}	// main
}
```

```
id와 password를 입력해주세요.
id : asdf
password : 1111

비밀번호가 일치하지 않습니다. 다시 입력해주세요.
id와 password를 입력해주세요.
id : asdf
password : 1234

id와 비밀번호가 일치합니다.
```

`HashMap`을 생성하고 사용자ID와 비밀번호를 키와 값의 쌍(pair)으로 저장한 다음, 입력된 사용자ID를 키로 `HashMap`에서 검색해서 얻은 값(비밀번호)을 입력된 비밀번호와 비교하는 예제이다.

``` java
HashMap map = new HashMap();
map.put("myId", "1234");
map.put("asdf", "1111");
map.put("asdf", "1234");
```

위의 코드는 `HashMap`을 생성하고 데이터를 저장하는 부분인데 이 코드가 실행되고 나면 `HashMap`에는 아래와 같은 형태로 데이터가 저장된다.

![image](https://ifh.cc/g/FHBclF.png)

3개의 데이터 쌍을 저장했지만 실제로는 2개 밖에 저장되지 않은 이유는 중복된 키가 있기 때문이다. 세 번째로 저장한 데이터의 키인 'asdf'는 이미 존재하기 때문에 새로 추가되는 대신 기존의 값을 덮어썼다. 그래서 키 'asdf'에 연결된 값은 '1234'가 된다.

`Map`은 값은 중복을 허용하지만 키는 중복을 허용하지 않기 때문에 저장하려는 두 데이터 중에서 어느 쪽을 키로 할 것인지를 잘 결정해야한다.

> Hashtable은 키(key)나 값(value)으로 null을 허용하지 않지만, HashMap은 허용한다. 그래서 'map.put(null, null);'이나 'map.get(null);'과 같이 할 수 있다.

</br>

예제 11-31 / ch11 / HashMapEx2.java

``` java
import java.util.*;

public class HashMapEx2 {
	public static void main(String[] args) {
		HashMap map = new HashMap();
		map.put("김자바", new Integer(90));
		map.put("김자바", new Integer(100));
		map.put("이자바", new Integer(100));
		map.put("강자바", new Integer(80));
		map.put("안자바", new Integer(90));
		
		Set set = map.entrySet();
		Iterator it = set.iterator();
		
		while(it.hasNext()) {
			Map.Entry e = (Map.Entry)it.next();
			System.out.println("이름 : " + e.getKey() + ", 점수 : " + e.getValue());
		}
		
		set = map.keySet();
		System.out.println("참가자 명단 : " + set);
		
		Collection values = map.values();
		it = values.iterator();
		
		int total = 0;
		
		while(it.hasNext()) {
			Integer i = (Integer)it.next();
			total += i.intValue();
		}
		
		System.out.println("총점 : " + total);
		System.out.println("평균 : " + (float)total / set.size());
		System.out.println("최고점수 : " + Collections.max(values));
		System.out.println("최저점수 : " + Collections.min(values));
	}
}
```

```
이름 : 안자바, 점수 : 90
이름 : 김자바, 점수 : 100
이름 : 강자바, 점수 : 80
이름 : 이자바, 점수 : 100
참가자 명단 : [안자바, 김자바, 강자바, 이자바]
총점 : 370
평균 : 92.5
최고점수 : 100
최저점수 : 80
```

`HashMap`의 기본적인 메소드를 이용해서 데이터를 저장하고 읽어오는 예제이다. `entrySet()`을 이용해서 키와 값을 함께 읽어 올 수도 있고 `keySet()`이나 `values()`를 이용해서 키와 값을 따로 읽어 올 수 있다.

</br>

예제 11-32 / ch11 / HashMapEx3.java

``` java
import java.util.*;

public class HashMapEx3 {
	static HashMap phoneBook = new HashMap();
	
	public static void main(String[] args) {
		addPhoneNo("친구", "이자바", "010-111-1111");
		addPhoneNo("친구", "김자바", "010-222-2222");
		addPhoneNo("친구", "김자바", "010-333-3333");
		addPhoneNo("회사", "김대리", "010-444-4444");
		addPhoneNo("회사", "김대리", "010-555-5555");
		addPhoneNo("회사", "박대리", "010-666-6666");
		addPhoneNo("회사", "이과장", "010-777-7777");
		addPhoneNo("세탁", "010-888-8888");
		
		printList();
	}	// main
	
	//그룹에 전화번호를 추가하는 메소드
	static void addPhoneNo(String groupName, String name, String tel) {
		addGroup(groupName);
		HashMap group = (HashMap)phoneBook.get(groupName);
		group.put(tel, name);	// 이름은 중복될 수 있으니 전화번호를 key로 저장한다.
	}
	
	// 그룹을 추가하는 메소드
	static void addGroup(String groupName) {
		if(!phoneBook.containsKey(groupName))
			phoneBook.put(groupName, new HashMap());
	}
	
	static void addPhoneNo(String name, String tel) {
		addPhoneNo("기타", name, tel);
	}
	
	// 전화번호부 전체를 출력하는 메소드
	static void printList() {
		Set set = phoneBook.entrySet();
		Iterator it = set.iterator();
		
		while(it.hasNext()) {
			Map.Entry e = (Map.Entry)it.next();
			
			Set subSet = ((HashMap)e.getValue()).entrySet();
			Iterator subIt = subSet.iterator();
			
			System.out.println(" * " + e.getKey() + "[" + subSet.size() + "]");
			
			while(subIt.hasNext()) {
				Map.Entry subE = (Map.Entry)subIt.next();
				String telNo = (String)subE.getKey();
				String name = (String)subE.getValue();
				System.out.println(name + " " + telNo);
			}
			System.out.println();
		}
	}	// printList()
}	// class
```

```
 * 기타[1]
세탁 010-888-8888

 * 친구[3]
이자바 010-111-1111
김자바 010-222-2222
김자바 010-333-3333

 * 회사[4]
이과장 010-777-7777
김대리 010-444-4444
김대리 010-555-5555
박대리 010-666-6666
```

`HashMap`은 데이터를 키와 값을 모두 Object타입으로 저장히기 때문에 `HashMap`의 값(value)으로 `HashMap`을 다시 저장할 수 있다. 이렇게 함으로써 하나의 키에 다시 복수의 데이터를 저장할 수 있다.

먼저 전화번호를 저장할 그룹을 만들고 그룹 안에 다시 이름과 전화번호를 저장하도록 했다. 이때 이름대신 전화번호를 키로 사용했다. 이름은 동명이인이 있을 수 있지만 전화번호는 유일하기 때문이다.

</br>

예제 11-33 / ch11 / HashMapEx4.java

``` java
import java.util.*;

public class HashMapEx4 {
	public static void main(String[] args) {
		String[] data = { "A", "K", "A", "K", "D", "K", "A", "K", "K", "K", "Z", "D" };
		
		HashMap map = new HashMap();
		
		for(int i = 0; i < data.length; i++) {
			if(map.containsKey(data[i])) {
				int value = (int)map.get(data[i]);
				map.put(data[i], value + 1);
			} else {
				map.put(data[i], 1);
			}
		}
		
		Iterator it = map.entrySet().iterator();
		
		while(it.hasNext()) {
			Map.Entry entry = (Map.Entry)it.next();
			int value = (int)entry.getValue();
			System.out.println(entry.getKey() + " : " + printBar('#', value) + " " + value);
		}
	}	// main
	
	public static String printBar(char ch, int value) {
		char[] bar = new char[value];
		
		for(int i = 0; i < bar.length; i++) {
			bar[i] = ch;
		}
		
		return new String(bar);	// String(char[] chArr)
	}
}
```

```
A : ### 3
D : ## 2
Z : # 1
K : ###### 6
```

문자열 배열에 담긴 문자열을 하나씩 읽어서 `HashMap`에 키로 저장하고 값으로 1을 저장한다. `HashMap`에 같은 문자열이 키로 저장되어 있는지 `containsKey()`로 확인하여 이미 저장되어 있는 문자열이면 값을 1증가시킨다.

그리고 그 결과를 `printBar()`를 이용해서 그래프로 표현했다. 이렇게 하면 문자열 배열에 담긴 문자열들의 빈도수를 구할 수 있다.

한정된 범위 내에 있는 순차적인 값들의 빈도수는 배열을 이용하지만, 이처럼 한정되지 않은 범위의 비순차적인 값들의 빈도수는 `HashMap`을 이용해서 구할 수 있다.

> 결과를 통해 HashMap과 같이 해싱을 구현한 컬렉션 클래스들은 저장순서를 유지하지 않는다.

</br>

### 해싱과 해시함수

해싱이란 해시함수(hash function)를 이용해서 데이터를 해시테이블(hash table)에 저장하고 검색하는 기법을 말한다. 해시함수는 데이터가 저장되어 있는 곳을 알려 주기 때문에 다량의 데이터 중에서도 원하는 데이터를 빠르게 찾을 수 있다.

해싱은 구현한 컬렉션 클래스로는 `HashSet`, `HashMap`, `Hashtable` 등이 있다. `Hashtable`은 컬렉션 프레임워크이 도입되면서 `HashMap`으로 대체되었으나 이전 소스와의 호환성 문제로 남겨 두고 있다. 가능하면 `Hashtable`대신 `HashMap`을 사용하는 것이 좋다.

해싱에서 사용하는 자료구조는 다음과 같이 배열과 링크드 리스트의 조합으로 되어 있다.

![image](https://ifh.cc/g/KgSg8s.png)

저장할 데이터의 키를 해시함수에 넣으면 배열의 한 요소를 얻게 되고, 다시 그 곳에 연결되어 있는 링크드 리스트에 저장하게 된다.

이해를 돕기 위해서 실생활에 비유한 예를 하나 들어보겠다. 한 간호사가 많은 환자들의 데이터 중에서, 원하는 환자의 데이터를 쉽게 찾을 수 있는 방법이 없을까를 고민하다가 주민등록번호의 맨 앞자리인 생년을 기준으로 데이터를 분류해서 10개의 서랍(배열)에 나눠 담는 방법을 생객해냈다. 예를 들면 71년생, 72년생과 같은 70년대생 환자들의 데이터는 같은 서랍에 저장된다.

이렇게 분류해서 저장해두면 환자의 주민번호로 태어난 년대를 계산해서 어느 서랍에서 찾아야 할지를 쉽게 알 수 있다.

> 동명이인이 있을 수 있기 때문에 이름보다는 주민등록번호를 키로 사용한다.

![image](https://ifh.cc/g/vPWbzZ.png)

여기서 서랍은 해싱에 사용되는 자료구조 중 배열의 각 요소를 의미하며, 배열의 각 요소에는 링크드 리스트가 저장되어 있어서 실제 데이터는 링크드 리스트에 담겨지게 된다.

아래 그림은 79년생 환자의 주민번호를 키로 해시함수를 통해 7이라는 해시코드를 얻은 다음, 배열의 7번째 요소에 저장된 링크드 리스트에서 원하는 데이터를 검색하는 과정을 표현한 것이다.

![image](https://ifh.cc/g/bhH3LS.png)

① 검색하고자 하는 값의 키로 해시함수를 호출한다.   
② 해시함수의 계산결과(해시코드)로 해당 값이 저장되어 있는 링크드 리스트를 찾는다.   
③ 링크드 리스트에서 검색한 키와 일치하는 데이터를 찾는다.

이미 배운 바와 같이 링크드 리스트는 검색에 불리한 자료구조이기 때문에 링크드 리스트의 크기가 커질수록 검색속도가 떨어지게 된다. 이는 하나의 서랍에 데이터의 수가 많을 수록 검색에 시간이 더 걸리는 것과 같다.

반면에 배열은 배열의 크기가 커져도, 원하는 요소가 몇 번째에 있는지만 알면 아래의 공식에 의해서 빠르게 원하는 값을 찾을 수 있다.

> **배열의 인덱스가 n인 요소의 주소 = 배열의 시작주소 + type의 size * n**

그래서 하나의 서랍에 많은 데이터가 저장되어 있는 형태보다는 많은 서랍에 하나의 데이터만 저장되어 있는 형태가 더 빠른 검색결과를 얻을 수 있다.

![image](https://ifh.cc/g/XCdh4v.png)

하나의 링크드 리스트(서랍)에 최소한의 데이터만 저장되려면, 저장된 데이터의 크기를 고려해서 `HashMap`의 크기를 적절하게 지정해주어야 하고, 해시함수가 서로 다른 키(주민번호)에 대해서 중복된 해시코드(서랍위치)의 반환을 최소화해야 한다. 그래야 `HashMap`에서 빠른 검색시간을 얻을 수 있다.

그래서 해싱을 구현하는 과정에서 제일 중요한 것은 해시함수의 알고리즘이며, 이 예에서 사용된 해시함수의 알고리즘은 주어진 키(주민번호)의 첫 번째 문자를 뽑아서 정수로 반환하기만 하면 되므로 아래와 같이 코드로 표현할 수 있다.

``` java
int hashFunction(String key) {
	return Integer.parseInt(key.substring(0, 1));
}
```

알고리즘이 간단한 만큼 성능이 좋지 않아서 서로 다른 키에 대해서 중복된 해시코드를 반환하는 경우가 많다.

실제로는 `HashMap`과 같이 해싱을 구현한 컬렉션 클래스에서는 `Object`클래스에 정의된 `hashCode()`를 해시함수로 사용한다. `Object`클래스에 정의된 `hashCode()`는 객체의 주소를 이용하는 알고리즘으로 해시코드를 만들어 내기 때문에 모든 객체에 대해 `hashCode()`를 호출한 결과가 서로 유일한 훌륭한 방법이다.

`String`클래스의 경우 `Object`클래스로부터 상속받은 `hashCode()`를 오버라이딩해서 문자열의 내용으로 해시코드를 만들어 낸다. 그래서 서로 다른 `String`인스턴스일지라도 같은 내용의 문자열을 가졌다면 `hashCode()`를 호출하면 같은 해시코드를 얻는다.

`HashSet`에서 설명했던 것과 같이 서로 다른 두 객체에 대해 `equals()`로 비교한 결과가 true인 동시에 `hashCode()`의 반환값이 같아야 같은 객체로 인식한다. `HashMap`에서도 같은 방법으로 객체를 구별하며, 이미 존재하는 키에 대한 값을 저장하면 기존의 값을 새로운 값으로 덮어쓴다.

그래서 새로운 클래스를 정의할 때 `equals()`를 재정의오버라이딩해야 한다면 `hashCode()`도 같이 재정의해서 `equals()`의 결과가 true인 두 객체의 해시코드 `hashCode()`의 결과 값이 항상 같도록 해주어야 한다.

그렇지 않으면 `HashMap`과 같이 해싱을 구현한 컬렉션 클래스에서는 `equals()`의 호출결과가 true지만 해시코드가 다른 두 객체를 서로 다른 것으로 인식하고 따로 저장할 것이다.

> equals()로 비교한 결과가 false이고, 해시코드가 같은 경우는 같은 링크드 리스트(서랍)에 서로 다른 두 데이터가 된다.

</br>

## 1.11 TreeMap

`TreeMap`은 이름에서 알 수 있듯이 이진검색트리의 형태로 키와 값의 쌍으로 이루어진 데이터를 저장한다. 그래서 검색과 정렬에 적합한 컬력션 클래스이다.

검색에 관한 대부분의 경우에서 `HashMap`이 `TreeMap`보다 더 뛰어나므로 `HashMap`을 사용하는 것이 좋다. 다만 범위검색이나 정렬이 필요한 경우에는 `TreeMap`을 사용하는 것이 좋다.

![image](https://ifh.cc/g/DygTsr.png)

</br>

예제 11-34 / ch11 / TreeMapEx1.java

``` java
import java.util.*;

public class TreeMapEx1 {
	public static void main(String[] args) {
		String[] data = { "A", "K", "A", "K", "D", "K", "A", "K", "K", "K", "Z", "D" };
		
		TreeMap map = new TreeMap();
		
		for(int i = 0; i < data.length; i++) {
			if(map.containsKey(data[i])) {
				Integer value = (Integer)map.get(data[i]);
				map.put(data[i], new Integer(value.intValue() + 1));
			} else {
				map.put(data[i], new Integer(1));
			}
		}
		
		Iterator it = map.entrySet().iterator();
		
		System.out.println("= 기본정렬 =");
		while(it.hasNext()) {
			Map.Entry entry = (Map.Entry)it.next();
			int value = ((Integer)entry.getValue()).intValue();
			System.out.println(entry.getKey() + " : " + printBar('#', value) + " " + value);
		}
		System.out.println();
		
		// map을 ArrayList로 변환한 다음에 Collections.sort()로 정렬
		Set set = map.entrySet();
		List list = new ArrayList(set);	// ArrayList(Collection c)
		
		// static void sort(List list, Comparator c)
		Collections.sort(list, new ValueComparator());
		
		it = list.iterator();
		
		System.out.println("= 값의 크기가 큰 순서로 정렬 =");
		while(it.hasNext()) {
			Map.Entry entry = (Map.Entry)it.next();
			int value = ((Integer)entry.getValue()).intValue();
			System.out.println(entry.getKey() + " : " + printBar('#', value) + " " + value);
		}
	}	// public static void main(String[] args)
	
	static class ValueComparator implements Comparator {
		public int compare(Object o1, Object o2) {
			if(o1 instanceof Map.Entry && o2 instanceof Map.Entry) {
				Map.Entry e1 = (Map.Entry)o1;
				Map.Entry e2 = (Map.Entry)o2;
				
				int v1 = ((Integer)e1.getValue()).intValue();
				int v2 = ((Integer)e2.getValue()).intValue();
				
				return v2 - v1;
			}
			return -1;
		}
	}	// static class ValueComparator implements Comparator {
	
	public static String printBar(char ch, int value) {
		char[] bar = new char[value];
		
		for(int i = 0; i < bar.length; i++) {
			bar[i] = ch;
		}
		return new String(bar);
	}
}
```

```
= 기본정렬 =
A : ### 3
D : ## 2
K : ###### 6
Z : # 1

= 값의 크기가 큰 순서로 정렬 =
K : ###### 6
A : ### 3
D : ## 2
Z : # 1
```

이 예제는 예제 11-33 HashMapEx4.java를 `TreeMap`을 이용해서 변형한 것인데 `TreeMap`을 사용했기 때문에 HashMapEx4.java의 결과와는 달리 키가 오름차순으로 정렬되어 있는 것을 알 수 있다. 키가 `String`인스턴스이기 때문에 `String`클래스에 정의된 정렬기준에 의해서 정렬된 것이다.

그리고 `Comparator`를 구현한 클래스와 `Collections.sort(List list, Comparator c)`를 이용해서 값에 대한 내림차순으로 정렬하는 방법을 보여준다.