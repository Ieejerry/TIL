# Linked List 값에 따라 나누기 in Java

</br>

[![2023-04-11-4-00-14.png](https://i.postimg.cc/4dwXgr8g/2023-04-11-4-00-14.png)](https://postimg.cc/ft3G7gn2)

</br>

[![2023-04-11-4-01-25.png](https://i.postimg.cc/RFjx44c2/2023-04-11-4-01-25.png)](https://postimg.cc/phY6BNcB)

</br>

[![2023-04-11-4-03-08.png](https://i.postimg.cc/Y9QbLH55/2023-04-11-4-03-08.png)](https://postimg.cc/8JPhxqP4)

</br>

## 방법 1. 두줄로 세우기

</br>

[![2023-04-11-4-04-53.png](https://i.postimg.cc/DyS4xgZZ/2023-04-11-4-04-53.png)](https://postimg.cc/9rjfMyy5)

</br>

x보다 작은 값들은 첫 번째 줄로 세우고, x보다 크거나 같은 값들은 두 번째 줄로 세워서 나중에 두 줄을 합쳐주면 정렬이 완료된다.

</br>

[![2023-04-11-4-08-45.png](https://i.postimg.cc/dV7XQz0Y/2023-04-11-4-08-45.png)](https://postimg.cc/K12QJpLq)

</br>

포인터는 총 5가지를 사용한다. 기존의 LinkedList를 도는 포인터 `n`, 그리고 첫 번째 줄의 처음 노드를 가리키는 포인터 `s1`, 첫 번째 줄의 마지막 노드를 가리키는 포인터 `e1`, 두 번째 줄의 처음 노드를 가리키는 포인터 `s2`, 두 번째 줄의 마지막 노드를 가리키는 포인터 `e2`, 이렇게 5가지를 사용할 것이다.

기존의 LinkedList의 처음 노드부터 포인터 `n`이 위치해 있는데, `n`이 가리키는 노드의 값과 `x`의 값을 비교한다. `n`의 값은 8이고, `x`의 값은 5이다. 두 개를 비교하면 `n`의 값이 더 크기 때문에 두 번째 줄 첫 번째 값으로 8을 넣어준다. 이 때 포인터 `s2`, `e2`은 8을 가리키고 있다. 이제 포인터 `n`이 다음 노드로 5로 이동한다. 5와 `x`의 값 5를 비교하니, 크거나 같기 때문에, 두 번째 줄 8 뒤에 추가해준다. 그러면 두 번째 줄 마지막 노드를 가리키는 포인터 `e2`가 5로 이동한다.

이런 식으로 반복하다보면 포인터 `n`은 LinkedList의 끝을 지나 `null`을 만나면서, LinkedList를 한 번 다 돌게 되고, 위의 그림처럼 정렬이 된다.

</br>

[![2023-04-11-4-19-52.png](https://i.postimg.cc/vBVb13t1/2023-04-11-4-19-52.png)](https://postimg.cc/LY2rwk7R)

</br>

이제 두 개의 줄을 하나로 합쳐주면 정렬이 완료가 되는데, 첫 번째 줄의 마지막 노드를 가리키는 포인터 `e1`의 노드의 `next` 값을 두 번째 줄의 처음 노드를 가리키는 포인터 `s2`의 노드로 주게 되면 두 개의 줄이 합쳐지면서 정렬이 완료된다.

</br>

### 전체 코드

</br>

``` java
package DataStructure;

class LinkedList4 {
    Node header;

    static class Node {
        int data;
        Node next = null;
    }

    LinkedList4() {
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

public class TEST2 {
	public static void main(String[] args) {
		LinkedList4 ll = new LinkedList4();
		ll.append(7);
		ll.append(2);
		ll.append(8);
		ll.append(5);
		ll.append(3);
		ll.append(4);
		ll.retrieve();
		
		LinkedList4.Node n = Partition(ll.get(1), 5);
		while(n.next != null) {
			System.out.print(n.data + " -> ");
			n = n.next;
		}
		System.out.println(n.data);
	}
	
	private static LinkedList4.Node Partition(LinkedList4.Node n, int x) {
		LinkedList4.Node s1 = null;
		LinkedList4.Node e1 = null;
		LinkedList4.Node s2 = null;
		LinkedList4.Node e2 = null;
		
		while(n != null) {
			LinkedList4.Node next = n.next;
			n.next = null;
			if(n.data < x) {
				if(s1 == null) {
					s1 = n;
					e1 = s1;
				} else {
					e1.next = n;
					e1 = n;
				}
			} else {
				if(s2 == null) {
					s2 = n;
					e2 = s2;
				} else {
					e2.next = n;
					e2 = n;
				}
			}
			n = next;
		}
		if(s1 == null) {
			return s2;
		}
		e1.next = s2;
		return s1;
	}
}
```

</br>

## 방법 2. 앞뒤로 붙이기

</br>

[![2023-04-11-4-40-24.png](https://i.postimg.cc/yxV2yjzY/2023-04-11-4-40-24.png)](https://postimg.cc/MMFsWyTh)

</br>

위의 방법은 포인터를 5가지나 사용하기 때문에 복잡하고 어렵다. 그래서 3가지의 포인터로만 이용해보겠다.

기존의 LinkedList를 도는 포인터 `n`과 새롭게 정렬되는 LinkedList의 헤더를 가리키는 포인터 `h`와 꼬리를 가리키는 포인터 `t`, 3 가지 포인터를 이용하겠다. `n`이 가리키는 노드의 값이 `x`보다 크거나 같을 경우, 포인터 `t`가 가리키는 노드의 다음에 넣어주고, `x`보다 작을 경우, 포인터 `h`가 가리키는 노드의 이전에 넣어주면 된다. 포인터 `n`이 기존의 LinkedList를 한번 다 돌면 정렬은 자연스럽게 완료가 되어, 새로운 LinkedList를 그대로 반환하면 된다.