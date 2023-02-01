# ArrayList - Java 구현

</br>

## 객체생성

우선 `ArrayList`라는 이름의 객체를 만들겠다.

</br>

ArrayList.java

``` java
package list.arraylist.implementation;

public class ArrayList {
	private int size = 0;
    private Object[] elementData = new Object[100];
}
```

</br>

Main.java

``` java
package list.arraylist.implementation;

public class Main {
	public static void main(String[] args) {
		ArrayList numbers = new ArrayList();
	}
}
```

</br>

## 데이터의 추가

</br>

### 마지막 위치에 추가

데이터를 마지막 위치에 추가하는 메소드의 구현은 아래와 같다.

</br>

``` java
public boolean addLast(Object element) {
    elementData[size] = element;
    size++;
    return true;
}
```

</br>

``` java
public static void main(String[] args) {
    ArrayList numbers = new ArrayList();
    numbers.addLast(10);
    numbers.addLast(20);
    numbers.addLast(30);
    numbers.addLast(40);
}
```

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2888.png)

</br>

## 중간에 추가

</br>

데이터를 중간에 추가하는 로직은 데이터를 추가할 빈공간을 확보해야 하기 때문에 조금 더 복잡하다. 코드를 보겠다.

</br>

``` java
public boolean add(int index, Object element) {
    // 엘리먼트 중간에 데이터를 추가하기 위해서는 끝의 엘리먼트부터 index의 노드까지 뒤로 한칸씩 이동시켜야 한다.
    for (int i = size - 1; i >= index; i--) {
        elementData[i + 1] = elementData[i];
    }
    // index에 노드를 추가한다.
    elementData[index] = element;
    // 엘리먼트의 숫자를 1 증가 시킨다.
    size++;
    return true;
}
```

</br>

엘리먼트의 이동을 코드로 표현하는 것이 처음에는 쉽지 않다. 아래 그림을 보겠다.

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2892.png)

</br>

그림에 표시된 숫자의 순서대로 엘리먼트를 왼쪽에서 오른찍으로 옮겨야 한다. 이 때 가장 중요한 것은 반복조건을 헷갈리지 않는 것이다. 반복문을 만들 때는 시작과 끝을 잘 파악하는 것이 중요하다.

- 시작 : 반복작업이 시작되는 인덱스로 이 값은 size-1로 구할 수 있다.
- 끝 : 반복작업이 끝나는 엘리먼트의 인덱스는 메소드 add의 첫번째 인자의 값을 사용하면 된다.
- 반복작업 : 감소연산 i--

이 작업을 통해서 엘리먼트를 한칸씩 뒤로 이동시킬 수 있다. 빈자리에 엘리먼트를 삽입한다.

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2871.png)

</br>

엘리먼트의 이동이 끝나면 아래와 같이 `elementData`에 `element`를 추가한다.

</br>

``` java
elementData[index] = element;
```

</br>

엘리먼트를 추가 했기 때문에 `size`의 값을 1 증가시킨다.

</br>

``` java
size++;
```

</br>

Main.java

``` java
ArrayList numbers = new ArrayList();
numbers.addLast(10);
numbers.addLast(20);
numbers.addLast(30);
numbers.addLast(40);
numbers.add(1, 15);
```

</br>

## 처음에 추가

데이터를 처음에 추가하는 메소드의 구현은 아래와 같다.

</br>

``` java
public boolean addFirst(Object element){
    return add(0, element);
}
```

</br>

Main.java

``` java
ArrayList numbers = new ArrayList();
numbers.addLast(10);
numbers.addLast(20);
numbers.addLast(30);
numbers.addLast(40);
numbers.add(1, 15);
numbers.addFirst(5);
```

</br>

## 데이터 확인

데이터를 확인하기 위해서 `toString` 객체를 상속해서 구현하겠다.

</br>

``` java
public String toString(){
    String str = "[";
    for(int i = 0; i < size; i++){
        str += elementData[i];
        if(i < size - 1){
            str += ", ";
        }
    }
    return str + "]";
}
```

</br>

이제 Main.java에서 아래와 같이 실행하면 리스트의 엘리먼트를 쉽게 파악할 수 있다.

</br>

``` java
public static void main(String[] args) {
    ArrayList numbers = new ArrayList();
    numbers.addLast(10);
    numbers.addLast(20);
    numbers.addLast(30);
    numbers.addLast(40);
    numbers.add(1, 15);
    numbers.addFirst(5);
    System.out.println(numbers);
}
```

```
[5, 10, 15, 20, 30, 40]
```

</br>

## 삭제

데이터를 삭제하는 것은 중간에 추가하는 것과 유사하다.

</br>

``` java
public Object remove(int index) {
    // 엘리먼트를 삭제하기 전에 삭제할 데이터를 removed 변수에 저장한다.
    Object removed = elementData[index];
    // 삭제된 엘리먼트 다음 엘리먼트부터 마지막 엘리먼트까지 순차적으로 이동해서 빈자리를 채운다.
    for (int i = index + 1; i <= size - 1; i++) {
        elementData[i - 1] = elementData[i];
    }
    // 크기를 줄인다.
    size--;
    // 마지막 위치의 엘리먼트를 명시적으로 삭제한다. 
    elementData[size] = null;
    return removed;
}
```

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2893.png)

</br>

그림에 나타난 것처럼 엘리먼트를 삭제할 때는 뒤에 있는 엘리먼트를 한칸씩 전진시킨다. 이 때 시작과 끝을 잘 파악하는 것이 중요하다.

엘리먼트를 옮기는 작업이 끝난 후에는 `size`의 값을 1 감소시킨다.

</br>

``` java
size--;
```

</br>

Main.java

``` java
ArrayList numbers = new ArrayList();
numbers.addLast(10);
numbers.addLast(20);
numbers.addLast(30);
numbers.addLast(40);
System.out.println(numbers.remove(1));
System.out.println(numbers);
```

```
20
[10,30,40]
```

</br>

## 처음과 끝의 엘리먼트 삭제

</br>

``` java
public Object removeFirst() {
    return remove(0);
}

public Object removeLast() {
    return remove(size - 1);
}
```

</br>

Main.java

``` java
ArrayList numbers = new ArrayList();
numbers.addLast(5);
numbers.addLast(10);
numbers.addLast(20);
numbers.addLast(30);
numbers.addLast(40);
numbers.removeFirst();
numbers.removeLast();
System.out.println(numbers);
```

```
[10, 20, 30]
```

</br>

## 데이터 가져오기

데이터를 가져오는 기능은 `get`이다. `get`은 인자로 전달된 인덱스 값을 그대로 배열로 전달한다. 배열은 메모리의 주소에 직접 접근하는 랜덤 엑세스(random access)이기 때문에 매우 빠르게 처리된다.

</br>

``` java
public Object get(int index) {
    return elementData[index];
}
```

</br>

``` java
ArrayList numbers = new ArrayList();
numbers.addLast(10);
numbers.addLast(20);
numbers.addLast(30);
numbers.addLast(40);
System.out.println(numbers.get(0));
System.out.println(numbers.get(1));
System.out.println(numbers.get(2));
System.out.println(numbers.get(3));
```

```
10
20
30
40
```

</br>

## 엘리먼트의 크기

</br>

``` java
public int size() {
    return size;
}
```

</br>

Main.java

``` java
ArrayList numbers = new ArrayList();
numbers.addLast(10);
numbers.addLast(20);
numbers.addLast(30);
numbers.addLast(40);
System.out.println(numbers.size());
```

```
4
```

</br>

## 탐색

특정한 값을 가진 엘리먼트의 인덱스 값을 알아내는 방법을 알아보겠다. 값이 있다면 그 값이 발견되는 첫번째 인덱스 값을 리턴하고 값이 없다면 -1을 리턴 한다.

</br>

``` java
public Object indexOf(Object o){
    for(int i = 0; i < size; i++){
        if(o.equals(elementData[i])){
            return i;
        }
    }
    return -1;
}
```

</br>

``` java
ArrayList numbers = new ArrayList();
numbers.addLast(10);
numbers.addLast(20);
numbers.addLast(30);
numbers.addLast(40);
System.out.println(numbers.indexOf(20));
System.out.println(numbers.indexOf(70));
```

```
1
-1
```

</br>

## 반복

`ArrayList`의 엘리먼트를 순회하는 방법은 아래와 같이 하면 된다.

</br>

``` java
for(int i = 0; i < numbers.size(); i++){
    System.out.println(numbers.get(i));
}
```

</br>

위와 같은 방법으로 반복을 사용해도 된다. 하지만 아래와 같이 사용하는 것이 더 좋은 방법이다.

</br>

``` java
ArrayList.ListIterator it = numbers.listIterator();
while (it.hasNext()) {
    int value = (int) it.next();
    System.out.println(value);
}
```

</br>

위의 코드는 `ListIterator`라는 객체를 이용한 방법이다. `ListIterator` 객체는 반복작업을 위해서 고안된 것이다. 이 객체를 만드는 방법은 `ArrayList`의 `listIterator` 메소드를 호출하면 된다. 이 메소드를 만드는 코드를 보겠다.

</br>

``` java
public ListIterator listIterator() {
    // ListIterator 인스턴스를 생성해서 리턴한다.
    return new ListIterator();
} 
```

</br>

아래는 `ListIterator` 클래스이다.

</br>

``` java
public class ListIterator {
    // 현재 탐색하고 있는 순서를 가르키는 인덱스 값
    private int nextIndex = 0;
 
    // next 메소르를 호출할 수 있는지를 체크한다.
    public boolean hasNext() {
        // nextIndex가 엘리먼트의 숫자보다 적다면 next를 이용해서 탐색할 엘리먼트가 존재하는 것이기 때문에 true를 리턴한다. 
        return nextIndex < size();
    }
     
    // 순차적으로 엘리먼트를 탐색해서 리턴한다. 
    public Object next() {
        // nextIndex에 해당하는 엘리먼트를 리턴하고 nextIndex의 값을 1 증가 시킨다.
        return elementData[nextIndex++];
    }
}
```

</br>

``` java
// previous 메소드를 호출해도 되는지를 체크한다.
public boolean hasPrevious(){
    // nextIndex가 0보다 크다면 이전 엘리먼트가 존재한다는 의미이다.
    return nextIndex > 0;
}
 
// 순차적으로 이전 노드를 리턴한다.
public Object previous(){
    // 이전 엘리먼트를 리턴하고 nextIndex의 값을 1감소한다. 
    return elementData[--nextIndex];
}
```

</br>

``` java
// 현재 엘리먼트를 추가한다. 
public void add(Object element){
    ArrayList.this.add(nextIndex++, element);
}
 
// 현재 엘리먼트를 삭제한다. 
public void remove(){
    ArrayList.this.remove(nextIndex-1);
    nextIndex--;
}
```

</br>

## 전체코드

</br>

``` java
package list.arraylist.implementation;

public class ArrayList {
	private int size = 0;
    private Object[] elementData = new Object[100];
    
    public boolean addFirst(Object element) {
    	return add(0, element);
    }
    
    public boolean addLast(Object element) {
		elementData[size] = element;
		size++;
    	return true;
	}
    
    public boolean add(int index, Object element) {
    	// 엘리먼트 중간에 데이터를 추가하기 위해서는 끝의 엘리먼트부터 index의 노드까지 뒤로 한칸씩 이동시켜야 한다.
    	for(int i = size - 1; i >= index; i--) {
    		elementData[i + 1] = elementData[i];
    	}
    	// index에 노드를 추가한다.
    	elementData[index] = element;
    	// 엘리먼트의 숫자를 1 증가 시킨다.
    	size++;
		return true;
	}
    
    public String toString() {
    	String str = "[";
    	for (int i = 0; i < size; i++) {
			str += elementData[i];
			if(i < size - 1) {
				str += ", ";
			}
		}
		return str + "]";
	}
    
    public Object remove(int index) {
        // 엘리먼트를 삭제하기 전에 삭제할 데이터를 removed 변수에 저장한다.
        Object removed = elementData[index];
        // 삭제된 엘리먼트 다음 엘리먼트부터 마지막 엘리먼트까지 순차적으로 이동해서 빈자리를 채운다.
        for (int i = index + 1; i <= size - 1; i++) {
            elementData[i - 1] = elementData[i];
        }
        // 크기를 줄인다.
        size--;
        // 마지막 위치의 엘리먼트를 명시적으로 삭제한다. 
        elementData[size] = null;
        return removed;
    }
    
    public Object removeFirst() {
		return remove(0);
	}
    
    public Object removeLast() {
		return remove(size - 1);
	}
    
    public Object get(int index) {
		return elementData[index];
	}
    
    public int size() {
		return size;
	}
    
    public int indexOf(Object o) {
		for(int i = 0; i < size; i++) {
			if(o.equals(elementData[i])) {
				return i;
			}
		}
		
		return -1;
	}
    
    public ListIterator listIterator() {
        // ListIterator 인스턴스를 생성해서 리턴한다.
        return new ListIterator();
    } 
    
    public class ListIterator {
        // 현재 탐색하고 있는 순서를 가르키는 인덱스 값
        private int nextIndex = 0;
     
        // next 메소르를 호출할 수 있는지를 체크한다.
        public boolean hasNext() {
            // nextIndex가 엘리먼트의 숫자보다 적다면 next를 이용해서 탐색할 엘리먼트가 존재하는 것이기 때문에 true를 리턴한다. 
            return nextIndex < size();
        }
         
        // 순차적으로 엘리먼트를 탐색해서 리턴한다. 
        public Object next() {
            // nextIndex에 해당하는 엘리먼트를 리턴하고 nextIndex의 값을 1 증가 시킨다.
            return elementData[nextIndex++];
        }
        
        // previous 메소드를 호출해도 되는지를 체크한다.
        public boolean hasPrevious(){
            // nextIndex가 0보다 크다면 이전 엘리먼트가 존재한다는 의미이다.
            return nextIndex > 0;
        }
         
        // 순차적으로 이전 노드를 리턴한다.
        public Object previous(){
            // 이전 엘리먼트를 리턴하고 nextIndex의 값을 1감소한다. 
            return elementData[--nextIndex];
        }
        
        // 현재 엘리먼트를 추가한다. 
        public void add(Object element){
            ArrayList.this.add(nextIndex++, element);
        }
         
        // 현재 엘리먼트를 삭제한다. 
        public void remove(){
            ArrayList.this.remove(nextIndex-1);
            nextIndex--;
        }
    }
}
```