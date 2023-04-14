# LinkedList 루프찾기

</br>

[![2023-04-13-3-59-17.png](https://i.postimg.cc/zDccGwPw/2023-04-13-3-59-17.png)](https://postimg.cc/Wt0n9ZVt)

</br>

[![2023-04-13-4-02-48.png](https://i.postimg.cc/Dybnvw5Z/2023-04-13-4-02-48.png)](https://postimg.cc/3d7P97s5)

</br>

LinkedList 안에 어떤 노드에 `next`값이 이미 그 리스트안에 연결되어 있는 다른 노드를 가리키고 있는 경우에 위의 그림처럼 루프가 생기는데, 리스트 안에 루프가 있는지 찾고, 있으면 루프를 시작하는 노드를 찾아서 반환하라는 문제이다.

이 문제를 해결하기 위해서는 2칸씩 이동하는 `f`포인터와 1칸씩 이동하는 `s`포인터를 선언한다. 포인터 `f`가 먼저 루프를 돌고 있는 동안, 포인터 `s`가 뒤따라 가다가 서로 만나는 지점을 찾는다.

두 포인터가 만나는 순간 포인터 `f`는 그 자리에 그대로 있고, 포인터 `s`만 리스트의 처음 노드로 보낸 다음, 두 포인터를 현재 자리에서 둘 다 한 칸씩 이동하도록 한다. 포인터 `f`는 루프 안에 있기 때문에 계속 루프를 돌다가, 다시 포인터 `s`를 만나게 되는데, 두 포인터가 두 번째로 만나는 자리가 루프의 시작점이다.

</br>

## 전체 코드

</br>

``` java
package DataStructure;

import static DataStructure.LinkedList5.Node;

import DataStructure.LinkedList5.Node;

public class TEST7 {
	public static void main(String[] args) {
		Node n1 = new Node(1);
		Node n2 = n1.addNext(2);
		Node n3 = n2.addNext(3);
		Node n4 = n3.addNext(4);
		Node n5 = n4.addNext(5);
		Node n6 = n5.addNext(6);
		Node n7 = n6.addNext(7);
		Node n8 = n7.addNext(8);
		n8.addNext(n4);
		
		Node n = findLoop(n1);
		
		if(n != null) {
			System.out.println("Start of loop : " + n.data);
		} else {
			System.out.println("Loop not found");
		}
	}
	
	private static Node findLoop(Node head) {
		Node fast = head;
		Node slow = head;
		
		while(fast != null && fast.next != null) {
			slow = slow.next;
			fast = fast.next.next;
			if(fast == slow) {
				break;
			}
		}
		
		if(fast == null || fast.next == null) {
			return  null;
		}
		
		slow = head;
		
		while(fast != slow) {
			slow = slow.next;
			fast = fast.next;
		}
		
		return fast;
	}
}
```