# Queue 구현하기 in Java

</br>

[![2023-04-16-7-07-41.png](https://i.postimg.cc/kDP75t8F/2023-04-16-7-07-41.png)](https://postimg.cc/gLsCSjgn)

</br>

Queue는 먼저 집어넣은 데이터를 먼저 꺼내는 구조의 저장공간이다. 양쪽으로 뚫린 파이프에 한 쪽은 넣기만 하고, 한 쪽은 꺼내기만 한다고 생각하면 된다. Queue는 먼저 들어간 데이터가 먼저 나오는 구조라서 FIFO(First In First Out)이라고 부른다.

</br>

## Queue의 기능

</br>

### add()

맨 마지막에 데이터를 추가하는 기능

</br>

### remove()

맨 앞에서 데이터를 꺼내는 기능

</br>

### peek()

맨 앞에 데이터를 보는 기능

</br>

### isEmpty()

Queue가 비어있는지 확인하는 기능

</br>

## 전체 코드

``` java
package DataStructure;

import java.util.NoSuchElementException;

class Queue<T> {
	class Node<T> {
		private T data;
		private Node<T> next;
		
		public Node(T data) {
			this.data = data;
		}
	}
	
	private Node<T> first;;
	private Node<T> last;
	
	public void add(T item) {
		Node<T> t = new Node<>(item);
		
		if(last != null) {
			last.next = t;
		}
		last = t;
		
		if(first == null) {
			first = last;
		}
	}
	
	public T remove() {
		if(first == null) {
			throw new NoSuchElementException();
		}
		
		T data  = first.data;
		first = first.next;
		
		if(first == null) {
			last = null;
		}
		
		return data;
	}
	
	public T peek() {
		if(first == null) {
			throw new NoSuchElementException();
		}
		
		return first.data;
	}
	
	public boolean isEmpty() {
		return first == null;
	}
}

public class QueueTest {
	public static void main(String[] args) {
		Queue<Integer> q = new Queue<>();
		q.add(1);
		q.add(2);
		q.add(3);
		q.add(4);
		System.out.println(q.remove());
		System.out.println(q.remove());
		System.out.println(q.peek());
		System.out.println(q.remove());
		System.out.println(q.isEmpty());
		System.out.println(q.remove());
		System.out.println(q.isEmpty());		
	}
}
```