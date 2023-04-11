# 단방향 Linked List 중간노드 삭제 in Java

</br>

[![2023-04-11-12-59-37.png](https://i.postimg.cc/hG9bgLZg/2023-04-11-12-59-37.png)](https://postimg.cc/2qSB7ZfX)

</br>

[![2023-04-11-1-00-50.png](https://i.postimg.cc/g0DXNNBw/2023-04-11-1-00-50.png)](https://postimg.cc/HJrkL4mH)

</br>

LinkedList에서 노드를 삭제하는 방법은 삭제할 노드의 전 노드가 삭제할 노드의 다음 노드의 주소값을 가지게 하면 된다. 하지만 여기서는 삭제할 노드 단 하나의 정보만을 가지고 있다. 단방향 LinkedList이기 때문에 그 노드의 다음 노드의 정보까지만 알 수 있고, 삭제할 노드 전 노드의 정보는 없다.

</br>

[![2023-04-11-1-06-09.png](https://i.postimg.cc/85kSmbqz/2023-04-11-1-06-09.png)](https://postimg.cc/bG5Wz1y7)

</br>

이런 경우, 다음 노드의 정보를 삭제할 노드에 엎어씌우면, 두 개의 노드는 똑같아진다. 그 다음, 원래 다음 노드였던 노드를 삭제하면 된다.

</br>

## 전체 코드

</br>

``` java
package DataStructure;

class LinkedList3 {
    Node header;

    static class Node {
        int data;
        Node next = null;
    }

    LinkedList3() {
        header = new Node();
    }

    void append(int d) {
        Node end = new Node();
        end.data = d;
        Node n = header;
        while(n.next != null) {
            n = n.next;
        }
        n.next = end;
    }
    
    void delete(int d) {
        Node n = header;
        while(n.next != null) {
            if(n.next.data == d) {
                n.next = n.next.next;
            } else {
                n = n.next;
            }
        }
    }
    
    void retrieve() {
        Node n = header.next;
        while(n.next != null) {
            System.out.print(n.data + " -> ");
            n = n.next;
        }
        System.out.println(n.data);
    }
    
    public Node get(int i) {
        Node n = header;
        for(int j=0;j<i;j++){
            n = n.next;
        }
        return n;
    }
}

public class TEST {
	public static void main(String[] args) {
		LinkedList3 ll = new LinkedList3();
		ll.append(1);
		ll.append(2);
		ll.append(3);
		ll.append(4);
		ll.retrieve();
		
		deleteNode(ll.get(3));
		ll.retrieve();
	}
	
	static boolean deleteNode(LinkedList3.Node n) {
		if(n == null || n.next == null) {
			return false;
		} 
		LinkedList3.Node next = n.next;
		n.data = next.data;
		n.next = next.next;
		return true;
	}
}
```

</br>