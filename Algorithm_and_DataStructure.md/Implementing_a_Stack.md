# Stack 구현하기 in Java

</br>

[![2023-04-16-6-36-30.png](https://i.postimg.cc/PJ90fGgg/2023-04-16-6-36-30.png)](https://postimg.cc/CnCcJ2L7)

</br>

Stack의 '쌓다'라는 뜻을 가지고 있다. 무언가를 쌓으면 맨 위에 올린 것부터 꺼낼 수 있다. 그래서 Stack이라고 부른다.

</br>

[![2023-04-16-6-39-00.png](https://i.postimg.cc/qvbDpH2j/2023-04-16-6-39-00.png)](https://postimg.cc/TKbJcS7D)

</br>

다시 말하면, 나중에 저장된 데이터가 먼저 나오는 구조이다. 이런 구조를 LIFO(Last In First Out)구조라고 한다.

</br>

## Stack 기능

</br>

### pop()

맨 마지막에 있는 데이터를 가져오면서 지우는 기능

</br>

### push()

새로운 데이터를 맨 마지막에 하나 더 쌓아올리는 기능

</br>

### peek()

맨 마지막 데이터를 보는 기능

</br>

### isEmpty()

Stack에 데이터가 있는지 없는지 확인하는 기능

</br>

## 전체 코드

``` java
package DataStructure;

import java.util.EmptyStackException;

class Stack<T> {
	class Node<T> {
		private T data;
		private Node<T> next;
		
		public Node(T data) {
			this.data = data;
		}
	}
	
	private Node<T> top;
	
	public T pop() {
		if(top == null) {
			throw new EmptyStackException();
		}
		
		T item = top.data;
		top = top.next;
		return item;
	}
	
	public void push(T item) {
		Node<T> t = new Node<T>(item);
		t.next = top;
		top = t;
	}
	
	public T peek() {
		if(top == null) {
			throw new EmptyStackException();
		}
		return top.data;
	}
	
	public boolean isEmpty() {
		return top == null;
	}
}

public class StackTest {
	public static void main(String[] args) {
		Stack<Integer> s = new Stack<>();
		s.push(1);
		s.push(2);
		s.push(3);
		s.push(4);
		System.out.println(s.pop());
		System.out.println(s.pop());
		System.out.println(s.peek());
		System.out.println(s.pop());
		System.out.println(s.isEmpty());
		System.out.println(s.pop());
		System.out.println(s.isEmpty());
	}
}
```

```
4
3
2
2
false
1
true
```