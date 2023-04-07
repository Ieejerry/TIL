# 단방향 Linked List 구현 in Java

</br>

## Node 생성

</br>

``` java
class Node {
    int data;
    Node next = null;

    Node(int d) {
        this.data = d;
    }
}
```

</br>

Java로 단방향 Linked List를 구현해보겠다. `Node`라는 클래스가 있고, 이 `Node`는 `data`라는 변수의 정수형 데이터값을 가진다. 다음 `Node`의 주소값을 가질 `next`라는 변수도 있다. `next` 변수는 `null`로 초기화 해준다. 생성자의 파라미터를 통해 전달 받은 인자를 인스턴스 변수 `data`에 대입한다.

</br>

## 데이터 추가(append)

</br>

``` java
void append(int d) {
    Node end = new Node(d);
    Node n = this;
    while(n.next != null) {
        n = n.next;
    }
    n.next = end;
}
```

</br>

Linked List에 데이터를 추가할 때 사용할 메소드인 `append(int d)`를 추가한다. 메소드 `append(int d)`는 정수형 데이터를 매개변수로 받고, `end`라는 변수로 매개변수로 받은 데이터를 가지는 새로운 `Node`를 만들고, while문을 `n.next`가 `null`일 때까지 반복하며 Linked List의 끝까지 이동하고, 맨 끝 `Node`의 `next`에 해당 `Node`를 대입한다. 이렇게 하여 새로운 `Node`가 맨 마지막 노드가 된다.

</br>

## 데이터 삭제(delete)

</br>

``` java
void delete(int d) {
    Node n = this;
    while(n.next != null) {
        if(n.next.data == d) {
            n.next = n.next.next;
        } else {
            n = n.next;
        }
    }
}
```

</br>

삭제할 값을 매개변수 `int d`로 받는다. `n`이라는 임의의 포인터를 만든다. 포인터는 자기 자신을 가리키게 하고, 마지막 노드에 도착할 때까지 반복하는 while문안에 if문을 통해 다음 `Node`의 `data`와 매개변수로 받은 `d`와 같은지 확인한다. 만약 `n.next`의 `data`의 값이 매개변수 `d`와 같다면, 현재 `Node`의 `next`를 다음 노드의 다음 노드의 주소로 바꾸어준다. 하지만 다음 `Node`의 `data`값이 인자 `d`와 다르면 찾을 때까지 다음 노드로 이동하며 찾는다.

</br>

## 결과값 보기(retrieve)

</br>

``` java
void retrieve() {
    Node n = this;
    while(n.next != null) {
        System.out.print(n.data + " -> ");
        n = n.next;
    }
    System.out.println(n.data);
}
```

</br>

Linked List는 처음부터 찾아야하니, `Node` 포인터를 하나 선언해준다. 그리고 while문을 통해 다음 노드로 이동하며 `data`값을 노드의 `next`가 `null`이 될 때까지 출력한다. 하지만 마지막 노드에 도달하게 되면 마지막 노드의 값은 출력하지 않기 때문에, while문이 끝난 뒤에 한 번 더 마지막 노드의 `data`값을 출력한다.

</br>

## 전체 코드

</br>

``` java
package DataStructure;

public class UnidirectionalLinkedList {
	public static void main(String[] args) {
		Node head = new Node(1);
		head.append(2);
		head.append(3);
		head.append(4);
		head.retrieve();
		head.delete(2);
		head.delete(3);
		head.retrieve();
	}	
}

class Node {
    int data;
    Node next = null;

    Node(int d) {
        this.data = d;     
    }
    
    void append(int d) {
        Node end = new Node(d);
        Node n = this;
        while(n.next != null) {
            n = n.next;
        }
        n.next = end;
    }
    
    void delete(int d) {
        Node n = this;
        while(n.next != null) {
            if(n.next.data == d) {
                n.next = n.next.next;
            } else {
                n = n.next;
            }
        }
    }
    
    void retrieve() {
        Node n = this;
        while(n.next != null) {
            System.out.print(n.data + " -> ");
            n = n.next;
        }
        System.out.println(n.data);
    }
}
```