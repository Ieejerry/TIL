# Linked List 중복값 삭제 in Java

</br>

## 정렬되지 않은 LinkedList의 중복값 제거(단, 버퍼를 사용하지 않기)

</br>

[![2023-04-09-11-23-46.png](https://i.postimg.cc/ydB32Htm/2023-04-09-11-23-46.png)](https://postimg.cc/06WNJL8j)

</br>

입력 데이터는 위의 그림과 같다. 정렬도 안되어 있고, 중복된 값도 있다.

</br>

### 버퍼를 사용한 정렬되지 않은 LinkedList의 중복값 제거

우선 무언가를 저장할 수 있는 버퍼공간을 HashSet으로 선언한다. 왜냐하면 HashSet이라는 데이터 구조는 key값을 가지고 데이터를 찾는데 걸리는 시간이 1밖에 걸리지 않는다.

</br>

[![2023-04-09-11-32-39.png](https://i.postimg.cc/GtL7L68Y/2023-04-09-11-32-39.png)](https://postimg.cc/dkfmnH9t)

</br>

이제 LinkedList를 돌면서, 어떤 데이터가 있는지 HashSet에 저장하다가, HashSet에 이미 있는 값은 중복되기 때문에 그런 노드를 삭제한다. 그렇게 LinkedList를 돌게되면 위의 그림 같이 HashSet 버퍼에는 중복값이 삭제된 데이터들이 저장된다. 이 과정은 버퍼 공간을 최악을 경우, LinkedList의 길이만큼 만들어야 하기 때문에 공간복잡도는 O(n)이 되고, 반복을 1회만 하기 때문에 시간복잡도도 O(n)이 된다.

</br>

### 버퍼를 사용하지 않고 정렬되지 않은 LinkedList의 중복값 제거

</br>

[![2023-04-09-11-40-05.png](https://i.postimg.cc/ZYWjcPPJ/2023-04-09-11-40-05.png)](https://postimg.cc/7bygP2QR)

</br>

버퍼 대신 포인터를 사용하여 중복을 제거한다. 여기서는 포인터 `n`과 러너 `r`이라는 변수를 선언한다. 포인터 `n`이 지정한 노드의 데이터값과 일치하는 데이터를 갖는 노드가 있는지, 러너 `r`이 `n`이 지정한 노드부터 LinkedList를 돌면서 찾고, 일치하는 데이터를 갖고 있는 노드를 발견하면 해당 노드를 삭제한다. 그러면 위와 같은 똑같은 결과가 반환된다.

버퍼를 사용하지 않고, 포인터를 이용하였기 때문에 공간복잡도는 O(1)이 되고, 러너 `r`이 n<sup>2</sup>만큼 돌기 때문에 시간복잡도는 O(n<sup>2</sup>)가 된다.

위의 버퍼를 활용할 때보다 시간은 더 많이 들지만, 공간효율성이 있다.

</br>

## 전체코드

</br>

``` java
package DataStructure;

class LinkedList2 {
    Node header;

    static class Node {
        int data;
        Node next = null;
    }

    LinkedList2() {
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
    
    void removeDups() {
    	Node n = header;
    	while(n != null && n.next != null) {
    		Node r = n;
    		while(r.next != null) {
    			if(n.data == r.next.data) {
    				r.next = r.next.next;
    			} else {
    				r = r.next;
    			}
    		}
    		n = n.next;
    	}
    }
}

public class RemoveDups {
	public static void main(String[] args) {
		LinkedList2 ll = new LinkedList2();
		ll.append(2);
		ll.append(1);
		ll.append(2);
		ll.append(3);
		ll.append(4);
		ll.append(3);
		ll.append(2);
		ll.append(2);
		ll.retrieve();
		ll.removeDups();
		ll.retrieve();
	}
}
```