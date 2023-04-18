# 두개의 Stack으로 Queue만들기

</br>

## 두 개의 Stack으로 하나의 Queue를 구현하시오.

</br>

[![2023-04-17-9-19-28.png](https://i.postimg.cc/PqbjJvfL/2023-04-17-9-19-28.png)](https://postimg.cc/wtBPbvmH)

</br>

그림의 왼쪽처럼 Queue는 처음 입력된 데이터가 먼저 출력되는 FIFO(First In First Out)구조이다. 반대로 Stack은 마지막에 입력된 데이터가 먼저 출력되는 LIFO(Last In First Out)구조인데, 두 개의 Stack을 가지고 Queue를 구현하는 방법은 간단하다.

새로운 데이터를 받는 Stack과 오래된 데이터를 저장할 Stack 두 개로 나눈다.

</br>

[![2023-04-17-9-24-23.png](https://i.postimg.cc/8kRtYdKf/2023-04-17-9-24-23.png)](https://postimg.cc/Wt4GFZPs)

</br>

`add()`를 할 때는, 새로운 데이터를 받는 new Stack에 입력되는 데이터를 받는다.

</br>

[![2023-04-17-9-27-14.png](https://i.postimg.cc/0yR5NsGB/2023-04-17-9-27-14.png)](https://postimg.cc/LnDFyGbt)

</br>

`peek()`이나 `remove()`가 호출되었을 때는, new Stack의 데이터를 old Stack에 붓는다. 그러면 new Stack에 마지막에 입력된 데이터가 먼저 `pop()`이 되고, old Stack에 `push()`가 되고, 마지막 전에 입력된 데이터가 `pop()`이 되고, old Stack에 `push()`가 되고, 이렇게 반복이 된다. 

</br>

[![2023-04-17-9-33-59.png](https://i.postimg.cc/2SDw71FF/2023-04-17-9-33-59.png)](https://postimg.cc/zVxKJXQV)

</br>

그런 다음, old Stack에서 `pop()`을 해주면, Queue의 `remove()`나 `peek()`와 같은 역할을 수행하게 된다.

</br>

## 전체 코드

</br>

``` java
package DataStructure;

import java.util.Stack;

class MyQueue<T> {
	Stack<T> stackNewest, stackOldest;
	
	MyQueue() {
		stackNewest = new Stack<T>();
		stackOldest = new Stack<T>();
	}
	
	public int size() {
		return stackNewest.size() + stackOldest.size();
	}
	
	public void add(T value) {
		stackNewest.push(value);
	}
	
	private void shiftStacks() {
		if(stackOldest.isEmpty()) {
			while(!stackNewest.isEmpty()) {
				stackOldest.push(stackNewest.pop());
			}
		}
	}
	
	public T peek() {
		shiftStacks();
		return stackOldest.peek();
	}
	
	public T remove() {
		shiftStacks();
		return stackOldest.pop();
	}
}

public class QueueTest2 {
	public static void main(String[] args) {
		MyQueue<Integer> q = new MyQueue<>();
		q.add(1);
		q.add(2);
		q.add(3);
		System.out.println(q.remove());
		System.out.println(q.remove());
		System.out.println(q.remove());
	}
}
```