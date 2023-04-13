# Linked List Digit합산 알고리즘 in Java

</br>

[![2023-04-12-1-18-17.png](https://i.postimg.cc/k4dBjfyD/2023-04-12-1-18-17.png)](https://postimg.cc/NypsF8Sw)

</br>

[![2023-04-12-1-20-08.png](https://i.postimg.cc/mrBv89HB/2023-04-12-1-20-08.png)](https://postimg.cc/0zXXNbnB)

</br>

이 문제는 위의 그림처럼 2개의 LinkedList가 있는데, 1의 자리가 헤더에 오도록 거꾸로 담았으니, 100의 자리가 맨 끝에 10의 자리가 중간, 그래서 위에 LinkedList 같은 경우, 419, 두 번째 LinkedList 같은 경우, 346이 된다. 그리고 두 LinkedList를 합산한 값을 같은 식으로 LinkedList에 담아서 반환하라고 하니, 두 LinkedList의 합인 765를 같은 식으로 반환하면 위의 그림치럼 반환해야 되는 문제이다.

</br>

[![2023-04-12-1-26-30.png](https://i.postimg.cc/YSxhsQD3/2023-04-12-1-26-30.png)](https://postimg.cc/Typdy56L)

</br>

첫 번째 LinkedList인 `L1`과 두 번째 LinkedList인 `L2`, 캐리값인 `C`, 결과인 `R` 이렇게 4개의 인자를 두고 계산을 한다. `L1`, `L2`의 헤더들부터 차례대로 더한다. 9 + 6 = 15가 되고, 10의 자리가 생겼기 때문에 캐리값 `C`를 1 올려주고, 결과값 `R`에 5를 넣어준다. 다음 노드들의 값들을 더해준다. 1 + 4 + 1 = 6이 된다. 캐리값이 없기 때문에 0을 올려주고, `R`에 6을 넣어준다. 그 다음 노드들의 값을 더해준다. 4 + 3 + 0 = 7이 되고, 이번에도 캐리값이 없기 때문에 0을 올려주고, `R`에 7을 넣어준다. 다음 노드들의 값을 보려고 하니 두 LinkedList 모두 `null`이고, 캐리값도 0이기 때문에 합산을 멈추고, 함수를 호출했던 스택 순서대로 다시 돌아간다. 돌아갈 때 호출에서 받은 노드를 자기가 생성한 노드의 다음 노드로 저장한다.

예를 들어보면, 4 + 3 + 0 = 함수가 7를 반환했다. 그러면 이 함수를 호출한 함수는 자기가 만든 노드값 `next`에 반환 받은 노드를 할당한다. 그래서 7를 반환 받으면 6에 링크를 걸고, 6을 반환 받으면 5에 링크를 걸어서 새롭게 생성된 노드들이 LinkedList로 서로 연결이 되도록 한다. 그리고 최종적으로 헤더 노드를 반환하면 사용자가 결과값을 출력할 수 있게 된다.

</br>

### 전체 코드

</br>

``` java
package DataStructure;

import static DataStructure.LinkedList5.Node;

public class TEST4 {
	public static void main(String[] args) {
		LinkedList5 l1 = new LinkedList5();
		l1.append(9);
		l1.append(1);
		l1.append(4);
		l1.retrieve();
		
		LinkedList5 l2 = new LinkedList5();
		l2.append(6);
		l2.append(4);
		l2.append(3);
		l2.retrieve();
		
		Node n = sumLists(l1.get(1), l2.get(1), 0);
		while(n.next != null) {
			System.out.print(n.data + " -> ");
			n = n.next;
		}
		System.out.println(n.data);
	}
	
	private static Node sumLists(Node l1, Node l2, int carry) {
		if(l1 == null && l2 == null && carry == 0) {
			return null;
		}
		
		Node result = new Node();
		int value = carry;
		
		if(l1 != null) {
			value += l1.data;
		}
		if(l2 != null) {
			value += l2.data;
		}
		result.data = value % 10;
		
		if(l1 != null || l2 != null) {
			Node next = sumLists(l1 == null ? null : l1.next,
								 l2 == null ? null : l2.next,
								 value >= 10 ? 1 : 0);
			result.next = next;
		}
		return result;
	}
}
```

</br>

## 심화학습. LinkedList에 숫자가 거꾸로가 아니면?

</br>

[![2023-04-12-2-10-53.png](https://i.postimg.cc/QMBfgk8F/2023-04-12-2-10-53.png)](https://postimg.cc/zLrw8hRN)

</br>

위의 첫 번째 그림처럼 두 개의 LinkedList의 길이가 다를 경우가 있을 수 있기 때문에, 우선 두 개의 LinkedList의 길이를 구하고, 두 개중 더 짧은 LinkedList가 있을 경우, 짧은 LinkedList의 앞에 0의 값을 갖는 노드로 채워줘야 한다. 그리고 맨 끝의 노드들이 1의 자리이기 때문에 뒤에서 부터 계산을 해야 된다. 그런데 아까는 캐리를 함수의 인자로 두 개의 노드와 함꼐 보내면 됐었는데, 여기서는 반대로 결과값을 받아서 캐리로 사용을 해야되는데 캐리의 함수를 결과로 받아버리면, 정작 합계 결과를 저장하고 있는 노드를 받을 수 없게 된다. 그래서 합계 결과를 저장하고 있는 노드와 캐리를 객체 안에 넣고, 객체의 주소를 반환해서 호출한 함수가 두 개 다 받아서 그 전 결과값을 저장하고 있는 노드와 캐리 둘 다 쓸 수 있게 한다.

</br>

[![2023-04-12-2-54-36.png](https://i.postimg.cc/66Hvr73Z/2023-04-12-2-54-36.png)](https://postimg.cc/t7xJy4FR)

</br>

부족한 자리수는 먼저 0으로 채워주고, 처음부터 4하고 0을 호출하고, 1하고 3을 두고 또 호출한다. 9하고 4 계속 돌다가, 마지막 노드에는 null을 가지고 있다. 둘 다 null인 위치가 되면 끝에 도착했다는 의미가 된다. 이 때 노드와 캐리를 저장할 객체를 하나 생성하여 반환한다. 캐리는 0으로 초기화하고, 노드는 null로 초기화한다.

이제 객체를 생성을 호출한 함수로 돌아간다. 캐리는 0이고, 9 + 4니깐 결과는 3, 캐리는 1이 된다. 그리고 합산 결과도 객체 안에 있는 노드의 앞에 추가한다. 그리고 이 객체 주소를 나를 호출했던 함수에 반환한다. 그러면 그 함수는 자기가 가지고 있던 숫자에 캐리를 더해서, 또 새로운 노드를 추가한다. 캐리가 1, 1 + 3이니깐 5가 된다. 여기서 더 이상 캐리가 없으니깐, 캐리를 0으로 바꿔주고, 여기서 생성된 새로운 노드를 객체 안에 있는 결과 리스트 앞에 또 추가를 한다. 처음으로 재귀호출한 함수에 도착하고, 캐리는 없고, 결과값 4를 결과 리스트 앞에 또 추가를 한다.

</br>

[![2023-04-12-2-13-40.png](https://i.postimg.cc/LXpjqznK/2023-04-12-2-13-40.png)](https://postimg.cc/B8mjkPTM)

</br>

그런데 만약에 마지막 숫자에서 캐리가 발생하면, 합산 작업을 마지막으로 한 번 더 해줘야 한다. 그래야 캐리에 있는 값을 잃어버리지 않기 때문이다. 그래서 나와서 마지막으로 한 번 더 수행해서 캐리를 노드로 만들어서 맨 앞에 추가해준다. 그리고 객체에 있는 결과값을 최종적으로 사용자에게 반환하면 된다.

</br>

### 전체 코드

</br>

``` java
package DataStructure;

import static DataStructure.LinkedList5.Node;

class Storage {
	int carry = 0;
	Node result = null;
}

public class TEST5 {
	public static void main(String[] args) {
		LinkedList5 l1 = new LinkedList5();
		l1.append(9);
		l1.append(1);
		l1.retrieve();
		
		LinkedList5 l2 = new LinkedList5();
		l2.append(1);
		l2.append(1);
		l2.retrieve();
		
		Node n = sumLists(l1.get(1), l2.get(1));
		while(n.next != null) {
			System.out.print(n.data + " -> ");
			n = n.next;
		}
		System.out.println(n.data);
	}
	
	private static Node sumLists(Node l1, Node l2) {
		int len1 = getListLength(l1);
		int len2 = getListLength(l2);
		
		if(len1 < len2) {
			l1 = LPadList(l1, len2 - len1);
		} else {
			l2 = LPadList(l2, len1 - len2);
		}
		
		Storage storage = addLists(l1, l2);
		if(storage.carry != 0) {
			storage.result = insertBefore(storage.result, storage.carry);
		}
		return storage.result;
	}
	
	private static Storage addLists(Node l1, Node l2) {
		if(l1 == null && l2 == null) {
			Storage storage = new Storage();
			return storage;
		}
 		Storage storage = addLists(l1.next, l2.next);
 		int value = storage.carry + l1.data + l2.data;
 		int data = value % 10;
 		storage.result = insertBefore(storage.result, data);
 		storage.carry = value / 10;
 		return storage;
	}
	
	private static int getListLength(Node l) {
		int total = 0;
		while(l != null) {
			total++;
			l = l.next;
		}
		return total;
	}
	
	private static Node insertBefore(Node node, int data) {
		Node before = new Node(data);
		if(node != null) {
			before.next = node;
		}
		return before;
	}
	
	private static Node LPadList(Node l, int length) {
		Node head = l;
		for(int i = 0; i < length; i++) {
			head = insertBefore(head, 0);
		}
		return head;
	}
}
```

</br>