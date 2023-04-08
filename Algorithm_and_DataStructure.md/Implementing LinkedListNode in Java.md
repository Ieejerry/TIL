# LinkedListNode의 구현 in Java

`Node`라는 클래스로 단방향 Linked List를 구현하였는데, `Node`클래스는 살짝 취약하기 때문에, `Node`클래스를 감싸는 `LinkedList` 만들어보겠다.

`Node`클래스는 `header`가 LinkedList의 첫 번째 값이기도 하면서, 대표이다. 어떤 프로세스가 이 `header`값이 더 이상 필요가 없어져 삭제해버리면 어떤 객체가 아직까지 이 `header`의 포인터를 가지고 있는 경우에 문제가 발생하게 된다. 이러한 문제를 해결하기 위해 `Node`클래스를 `LinkedList`라는 클래스로 감싸서 `LinkedList`에 `header`를 데이터가 아닌 `LinkedList`의 시작을 알려주는 용도로만 쓰도록 하나 저장을 한다. 그리고 그 안에 `Node`클래스를 하나 만든다.

</br>

## 전체코드

</br>

``` java
class LinkedList {
    Node header;

    static class Node {
        int data;
        Node next = null;
    }

    LinkedList() {
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
}

public class LinkedListNode {
    public static void main(String[] args) {
        LinkedList ll = new LinkedList();
        ll.append(1);
        ll.append(2);
        ll.append(3);
        ll.append(4);
        ll.retrieve();
    }
}
```

</br>

`LinkedList`클래스를 만들고, 그 안에 `header` `Node`를 선언한다. 그리고 이 안에 `Node`를 선언한다. `Node`는 마찬가지로 `data`와 `next` 다음 주소 값을 가지게 된다. `next`의 초기값은 `null`이다.

그리고 생성자를 통해 `LinkedList`를 생성할 때, `header` 노드를 생성하도록 한다. 그리고 그 밖에 노드 추가, 삭제, 출력 메소드를 뒤에 넣어준다.

전의 `append()`, `delete()`, `retrieve`메소드에 처음 시작 노드를 `this`가 아닌 `header`로 시작하도록 선안하여 운영한다.

그래서 앞으로 `delete()`에서 첫 번째 값을 지울 수 있게 된다. 왜냐하면 첫 번째 값은 `header`이고, `header`는 데이터로 사용되지 않고, 관리용도로만 쓰이기 때문이다.

`retrieve()`메소드에서는 `header` 다음 데이터를 `n`에 할당해서 `n`부터 출력되도록 하는 것이다.