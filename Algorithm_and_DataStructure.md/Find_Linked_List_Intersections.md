# Linked List 교차점찾기 in Java

</br>

[![2023-04-12-6-25-52.png](https://i.postimg.cc/8PbbVpQr/2023-04-12-6-25-52.png)](https://postimg.cc/jLLfHrjs)

</br>

[![2023-04-12-6-27-48.png](https://i.postimg.cc/gJYYQHvh/2023-04-12-6-27-48.png)](https://postimg.cc/nsPbQ7SV)

</br>

[![2023-04-12-6-28-33.png](https://i.postimg.cc/y62NYcKM/2023-04-12-6-28-33.png)](https://postimg.cc/qgXr1tzw)

</br>

문제에서 교차점이라는 말은 두 개의 리스트가 중간에 합쳐지는 지점이다.

</br>

[![2023-04-12-6-30-22.png](https://i.postimg.cc/Sxs1T22K/2023-04-12-6-30-22.png)](https://postimg.cc/VdxF5NFy)

</br>

두 리스트를 전부 비교하려면 시간이 많이 들기 때문에 일단 시간을 줄이기 위해 리스트의 끝을 맞춰준다. 그리고 중간에 합쳐지면 결국 끝나는 지점은 같기 때문이다.

현재 가지고 있는 리스트는 단방향으로 뒤를 맞춰줘도 뒤에서부터 찾아서 앞으로 비교를 할 수 없다.

</br>

[![2023-04-12-6-36-48.png](https://i.postimg.cc/rp9v7XyV/2023-04-12-6-36-48.png)](https://postimg.cc/4KmLh0hq)

</br>

그래서 앞에서부터 비교하는 방법은 두 개의 리스트 길이를 뒤를 기준으로 맞춰서 앞을 잘라준 다음에 앞에서부터 한 번만 돌면서 비교를 하면 교차점을 찾을 수 있다.

</br>

## 전체 코드

</br>

``` java
package DataStructure;

import static DataStructure.LinkedList5.Node;

import DataStructure.LinkedList5.Node;

public class TEST6 {
	public static void main(String[] args) {
		Node n1 = new Node(5);
		Node n2 = n1.addNext(7);
		Node n3 = n2.addNext(9);
		Node n4 = n3.addNext(10);
		Node n5 = n4.addNext(7);
		Node n6 = n5.addNext(6);
		
		Node m1 = new Node(6);
		Node m2 = m1.addNext(8);
		Node m3 = m2.addNext(n4);
		
		Node n = getIntersection(n1, n2);
		
		if(n != null) {
			System.out.println("Intersection : " + n.data);
		} else {
			System.out.println("Not found");
		}
	}
	
	private static Node getIntersection(Node l1, Node l2) {
		int len1 = getListLength(l1);
		int len2 = getListLength(l2);
		
		if(len1 > len2) {
			l1 = l1.get(len1 - len2);
		} else if(len1 < len2) {
			l2 = l2.get(len2 - len1);
		}
		
		while(l1 != null && l2 != null) {
			if(l1 == l2) {
				return l1;
			}
			l1 = l1.next;
			l2 = l2.next;
		}
		return null;
	}
	
	private static int getListLength(Node l) {
		int total = 0;
		while(l != null) {
			total++;
			l = l.next;
		}
		return total;
	}
}
```