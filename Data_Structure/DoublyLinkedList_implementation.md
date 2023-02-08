## Doubly linked list - Java 구현

이중 연결 리스트는 단순 연결 리스트를 기반으로 약간의 변형을 가한 것이기 때문에 단순 연결 리스트의 소스 코드를 수정하는 방법으로 접근하면 된다.

## 클래스

</br>

DoublyLinkedList.java

``` java
package list.doublylinkedlist.implementation;
 
public class DoublyLinkedList {
    // 첫번째 노드를 가리키는 필드
    private Node head;
    private Node tail;
    private int size = 0;
}
```

</br>

## 노드

노드에는 이전 노드에 대한 부분이 추가 된다.

</br>

``` java
private class Node {
    // 데이터가 저장될 필드
    private Object data;
    // 다음 노드를 가리키는 필드
    private Node next;
    private Node prev;
 
    public Node(Object input) {
        this.data = input;
        this.next = null;
        this.prev = null;
    }
 
    // 노드의 내용을 쉽게 출력해서 확인해볼 수 있는 기능
    public String toString() {
        return String.valueOf(this.data);
    }
}
```

</br>

아래는 linked list 대비 doubly linked list에서 변경된 부분을 보여주고 있다. 붉은색으로 표시된 부분이 추가된 부분이다.

**DoublyLinkedList.java VS LinkedList.java**

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/3051.png)

</br>

## 추가

</br>

### 시작 위치에 추가

</br>

``` java
public void addFirst(Object input) {
    // 노드를 생성한다.
    Node newNode = new Node(input);
    // 새로운 노드의 다음 노드로 헤드를 지정한다.
    newNode.next = head;
    // 기존에 노드가 있었다면 현재 헤드의 이전 노드로 새로운 노드를 지정한다.
    if (head != null)
        head.prev = newNode;
    // 헤드로 새로운 노드를 지정한다.
    head = newNode;
    size++;
    if (head.next == null) {
        tail = head;
    }
}
```

</br>

`head` 앞에 새로운 노드가 위치하게 되기 때문에 `head`의 이전 값으로 새로운 노드를 지정하는 부분이 추가 되었다.

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/3052.png)

</br>

### 끝에 추가

</br>

``` java
public void addLast(Object input) {
    // 노드를 생성한다.
    Node newNode = new Node(input);
    // 리스트의 노드가 없다면 첫번째 노드를 추가하는 메소드를 사용한다.
    if (size == 0) {
        addFirst(input);
    } else {
        // tail의 다음 노드로 생성한 노드를 지정한다.
        tail.next = newNode;
        // 새로운 노드의 이전 노드로 tail을 지정한다.
        newNode.prev = tail;
        // 마지막 노드를 갱신한다.
        tail = newNode;
        // 엘리먼트의 개수를 1 증가 시킨다.
        size++;
    }
}
```

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/3053.png)

</br>

### 특정 위치에 추가

</br>

``` java
public void add(int k, Object input) {
    // 만약 k가 0이라면 첫번째 노드에 추가하는 것이기 때문에 addFirst를 사용한다.
    if (k == 0) {
        addFirst(input);
    } else {
        Node temp1 = node(k - 1);
        // k 번째 노드를 temp2로 지정한다.
        Node temp2 = temp1.next;
        // 새로운 노드를 생성합니다.
        Node newNode = new Node(input);
        // temp1의 다음 노드로 새로운 노드를 지정한다.
        temp1.next = newNode;
        // 새로운 노드의 다음 노드로 temp2를 지정한다.
        newNode.next = temp2;
        // temp2의 이전 노드로 새로운 노드를 지정한다.
        if (temp2 != null)
            temp2.prev = newNode;
        // 새로운 노드의 이전 노드로 temp1을 지정한다.
        newNode.prev = temp1;
        size++;
        // 새로운 노드의 다음 노드가 없다면 새로운 노드가 마지막 노드이기 때문에 tail로 지정한다.
        if (newNode.next == null) {
            tail = newNode;
        }
    }
}
```

</br>

위의 코드를 보면 `temp1`을 지정하는 로직이 `node(k-1)`로 변경된 것을 볼 수 있다. 노드 탐색 작업이 빈번한 작업이기 때문에 별도의 메소드로 분리시켰다. 그 외의 코드 상의 변화는 앞뒤 노드를 연결해주는 것과 관련된 부분이다.

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/3055.png)

</br>

## 노드 찾기

아래는 노드를 찾는 작업을 메소드화시킨 것이다.

</br>

``` java
Node node(int index) {
    // 노드의 인덱스가 전체 노드 수의 반보다 큰지 작은지 계산
    if (index < size / 2) {
        // head부터 next를 이용해서 인덱스에 해당하는 노드를 찾는다.
        Node x = head;
        for (int i = 0; i < index; i++)
            x = x.next;
        return x;
    } else {
        // tail부터 prev를 이용해서 인덱스에 해당하는 노드를 찾는다.
        Node x = tail;
        for (int i = size - 1; i > index; i--)
            x = x.prev;
        return x;
    }
}
```

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/3054.png)

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2983.png)

</br>

위의 그림과 같이 리스트의 노드가 6개라고 했을 때 `get`의 인자로 전달된 인덱스가 2(30의 인덱스)이하라면 `head`부터 `next`를 이용해서 탐색을 한다. 인덱스가 3이상이라면 `tail`부터 `prev`를 이용해서 탐색을 할 수 있다. 즉 인덱스의 위치에 따라서 탐색 방향을 달리 할 수 있다. 덕분에 탐색 시간을 두배로 향상시킬 수 있다. 이것이 양방향으로 연결을 했을 때의 효용이다.

</br>

## 삭제

</br>

### 처음 노드 삭제

</br>

``` java
public Object removeFirst() {
    // 첫번째 노드를 temp로 지정하고 head의 값을 두번째 노드로 변경한다.
    Node temp = head;
    head = temp.next;
    // 데이터를 삭제하기 전에 리턴할 값을 임시 변수에 담는다.
    Object returnData = temp.data;
    temp = null;
    // 리스트 내에 노드가 있다면 head의 이전 노드를 null로 지정한다.
    if (head != null)
        head.prev = null;
    size--;
    return returnData;
}
```

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/3058.png)

</br>

### 특정 위치 노드 삭제

</br>

``` java
public Object remove(int k) {
    if (k == 0)
        return removeFirst();
    // k-1번째 노드를 temp로 지정한다.
    Node temp = node(k - 1);
    // temp.next를 삭제하기 전에 todoDeleted 변수에 보관한다.
    Node todoDeleted = temp.next;
    // 삭제 대상 노드를 연결에서 분리한다.
    temp.next = temp.next.next;
    if (temp.next != null) {
        // 삭제할 노드의 전후 노드를 연결한다.
        temp.next.prev = temp;
    }
    // 삭제된 노드의 데이터를 리턴하기 위해서 returnData에 데이터를 저장한다.
    Object returnData = todoDeleted.data;
    // 삭제된 노드가 tail이었다면 tail을 이전 노드를 tail로 지정한다.
    if (todoDeleted == tail) {
        tail = temp;
    }
    // cur.next를 삭제한다.
    todoDeleted = null;
    size--;
    return returnData;
}
```

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/3057.png)

</br>

### 마지막 노드 삭제

</br>

``` java
public Object removeLast() {
    return remove(size - 1);
}
```

</br>

### 인덱스로 엘리먼트 가져오기

</br>

``` java
public Object get(int k) {
    Node temp = node(k);
    return temp.data;
}
```

</br>

## 탐색

다음 코드는 특정 데이터가 저장된 인덱스를 알아내는 방법이다.

</br>

``` java
public int indexOf(Object data) {
    // 탐색 대상이 되는 노드를 temp로 지정한다.
    Node temp = head;
    // 탐색 대상이 몇번째 엘리먼트에 있는지를 의미하는 변수로 index를 사용한다.
    int index = 0;
    // 탐색 값과 탐색 대상의 값을 비교한다.
    while (temp.data != data) {
        temp = temp.next;
        index++;
        // temp의 값이 null이라는 것은 더 이상 탐색 대상이 없다는 것을 의미합니다.이 때 -1을 리턴한다.
        if (temp == null)
            return -1;
    }
    // 탐색 대상을 찾았다면 대상의 인덱스 값을 리턴한다.
    return index;
}
```

</br>

## 반복

반복자(iterator)를 이용해서 순차적으로 노드를 탐색하는 방법은 Linked list와 거의 같다. 그런데 doubly linked list는 반복과 관련해서 중요한 차이가 있다. 바로 탐색 방향을 자유롭게 변경할 수 있다는 것이다. 기존의 `iterator` 대비 3개의 메소드를 더 추가하겠다.

</br>

### 이전 노드 탐색

이중 연결 리스트의 기본적인 클래스 골격은 아래와 같다. `next`는 다음번 리턴 할 노드를 가르키고, `lastReturned`는 마지막으로 리턴된 노드를 가르킨다. `lastReturned`는 `next`를 한칸 뒤에서 따라다닌다. `nextIndex`는 `next`를 호출했을 때 다음 번 리턴될 노드의 인덱스 값을 의미한다.

</br>

``` java
public class ListIterator {
    private Node lastReturned;
    private Node next;
    private int nextIndex;
    ListIterator() {
        next = head;
        nextIndex = 0;
    }
}
```

</br>

이중 연결 리스트는 `next`와 `prev`를 가지고 있기 때문에 탐색의 방향을 원하는데로 지정할 수 있다.

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2991.png)

</br>

``` java
// 본 메소드를 호출하면 cursor의 참조값이 기존 cursor.next로 변경된다.
public Object next() {
    lastReturned = next;
    next = next.next;
    nextIndex++;
    return lastReturned.data;
}
 
// cursor의 값이 없다면 다시 말해서 더 이상 next를 통해서 가져올 노드가 없다면 false를 리턴한다.
// 이를 통해서 next를 호출해도 되는지를 사전에 판단할 수 있다.
public boolean hasNext() {
    return nextIndex < size();
}
 
public boolean hasPrevious() {
    return nextIndex > 0;
}
 
public Object previous() {
    if (next == null) {
        lastReturned = next = tail;
    } else {
        lastReturned = next = next.prev;
    }
    nextIndex--;
    return lastReturned.data;
}
```

</br>

다음은 탐색 과정에서 노드의 삭제, 추가와 관련된 작업을 구현한 코드이다.

</br>

``` java
public void add(Object input) {
    Node newNode = new Node(input);
    if (lastReturned == null) {
        head = newNode;
        newNode.next = next;
    } else {
        lastReturned.next = newNode;
        newNode.prev = lastReturned;
        if (next != null) {
            newNode.next = next;
            next.prev = newNode;
        } else {
            tail = newNode;
        }
    }
    lastReturned = newNode;
    nextIndex++;
    size++;
}
```

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/3059.png)

</br>

``` java
public void remove() {
    if (nextIndex == 0) {
        throw new IllegalStateException();
    }
    Node n = lastReturned.next;
    Node p = lastReturned.prev;
 
    if (p == null) {
        head = n;
        head.prev = null;
        lastReturned = null;
    } else {
        p.next = next;
        lastReturned.prev = null;
    }
 
    if (n == null) {
        tail = p;
        tail.next = null;
    } else {
        n.prev = p;
    }
 
    if (next == null) {
        lastReturned = tail;
    } else {
        lastReturned = next.prev;
    }
 
    size--;
    nextIndex--;
 
}
```

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/3060.png)

</br>

## 전체코드

</br>

``` java
package list.doublylinkedlist.implementation;
 
public class DoublyLinkedList {
    // 첫번째 노드를 가리키는 필드
    private Node head;
    private Node tail;
    private int size = 0;
 
    private class Node {
        // 데이터가 저장될 필드
        private Object data;
        // 다음 노드를 가리키는 필드
        private Node next;
        private Node prev;
 
        public Node(Object input) {
            this.data = input;
            this.next = null;
            this.prev = null;
        }
 
        // 노드의 내용을 쉽게 출력해서 확인해볼 수 있는 기능
        public String toString() {
            return String.valueOf(this.data);
        }
    }
 
    public void addFirst(Object input) {
        // 노드를 생성합니다.
        Node newNode = new Node(input);
        // 새로운 노드의 다음 노드로 헤드를 지정한다.
        newNode.next = head;
        // 기존에 노드가 있었다면 현재 헤드의 이전 노드로 새로운 노드를 지정한다.
        if (head != null)
            head.prev = newNode;
        // 헤드로 새로운 노드를 지정한다.
        head = newNode;
        size++;
        if (head.next == null) {
            tail = head;
        }
    }
 
    public void addLast(Object input) {
        // 노드를 생성합니다.
        Node newNode = new Node(input);
        // 리스트의 노드가 없다면 첫번째 노드를 추가하는 메소드를 사용한다.
        if (size == 0) {
            addFirst(input);
        } else {
            // tail의 다음 노드로 생성한 노드를 지정한다.
            tail.next = newNode;
            // 새로운 노드의 이전 노드로 tail을 지정한다.
            newNode.prev = tail;
            // 마지막 노드를 갱신합니다.
            tail = newNode;
            // 엘리먼트의 개수를 1 증가 시킨다.
            size++;
        }
    }
 
    Node node(int index) {
        // 노드의 인덱스가 전체 노드 수의 반보다 큰지 작은지 계산
        if (index < size / 2) {
            // head부터 next를 이용해서 인덱스에 해당하는 노드를 찾는다.
            Node x = head;
            for (int i = 0; i < index; i++)
                x = x.next;
            return x;
        } else {
            // tail부터 prev를 이용해서 인덱스에 해당하는 노드를 찾는다.
            Node x = tail;
            for (int i = size - 1; i > index; i--)
                x = x.prev;
            return x;
        }
    }
 
    public void add(int k, Object input) {
        // 만약 k가 0이라면 첫번째 노드에 추가하는 것이기 때문에 addFirst를 사용한다.
        if (k == 0) {
            addFirst(input);
        } else {
            Node temp1 = node(k - 1);
            // k 번째 노드를 temp2로 지정한다.
            Node temp2 = temp1.next;
            // 새로운 노드를 생성합니다.
            Node newNode = new Node(input);
            // temp1의 다음 노드로 새로운 노드를 지정한다.
            temp1.next = newNode;
            // 새로운 노드의 다음 노드로 temp2를 지정한다.
            newNode.next = temp2;
            // temp2의 이전 노드로 새로운 노드를 지정한다.
            if (temp2 != null)
                temp2.prev = newNode;
            // 새로운 노드의 이전 노드로 temp1을 지정한다.
            newNode.prev = temp1;
            size++;
            // 새로운 노드의 다음 노드가 없다면 새로운 노드가 마지막 노드이기 때문에 tail로 지정한다.
            if (newNode.next == null) {
                tail = newNode;
            }
        }
    }
 
    public String toString() {
        // 노드가 없다면 []를 리턴한다.
        if (head == null) {
            return "[]";
        }
        // 탐색을 시작한다.
        Node temp = head;
        String str = "[";
        // 다음 노드가 없을 때까지 반복문을 실행한다.
        // 마지막 노드는 다음 노드가 없기 때문에 아래의 구문은 마지막 노드는 제외된다.
        while (temp.next != null) {
            str += temp.data + ",";
            temp = temp.next;
        }
        // 마지막 노드를 출력결과에 포함시킨다.
        str += temp.data;
        return str + "]";
    }
 
    public Object removeFirst() {
        // 첫번째 노드를 temp로 지정하고 head의 값을 두번째 노드로 변경한다.
        Node temp = head;
        head = temp.next;
        // 데이터를 삭제하기 전에 리턴할 값을 임시 변수에 담는다.
        Object returnData = temp.data;
        temp = null;
        // 리스트 내에 노드가 있다면 head의 이전 노드를 null로 지정한다.
        if (head != null)
            head.prev = null;
        size--;
        return returnData;
    }
 
    public Object remove(int k) {
        if (k == 0)
            return removeFirst();
        // k-1번째 노드를 temp로 지정한다.
        Node temp = node(k - 1);
        // temp.next를 삭제하기 전에 todoDeleted 변수에 보관한다.
        Node todoDeleted = temp.next;
        // 삭제 대상 노드를 연결에서 분리한다.
        temp.next = temp.next.next;
        if (temp.next != null) {
            // 삭제할 노드의 전후 노드를 연결한다.
            temp.next.prev = temp;
        }
        // 삭제된 노드의 데이터를 리턴하기 위해서 returnData에 데이터를 저장한다.
        Object returnData = todoDeleted.data;
        // 삭제된 노드가 tail이었다면 tail을 이전 노드를 tail로 지정한다.
        if (todoDeleted == tail) {
            tail = temp;
        }
        // cur.next를 삭제한다.
        todoDeleted = null;
        size--;
        return returnData;
    }
 
    public Object removeLast() {
        return remove(size - 1);
    }
 
    public int size() {
        return size;
    }
 
    public Object get(int k) {
        Node temp = node(k);
        return temp.data;
    }
 
    public int indexOf(Object data) {
        // 탐색 대상이 되는 노드를 temp로 지정한다.
        Node temp = head;
        // 탐색 대상이 몇번째 엘리먼트에 있는지를 의미하는 변수로 index를 사용한다.
        int index = 0;
        // 탐색 값과 탐색 대상의 값을 비교한다.
        while (temp.data != data) {
            temp = temp.next;
            index++;
            // temp의 값이 null이라는 것은 더 이상 탐색 대상이 없다는 것을 의미합니다.이 때 -1을 리턴한다.
            if (temp == null)
                return -1;
        }
        // 탐색 대상을 찾았다면 대상의 인덱스 값을 리턴한다.
        return index;
    }
 
    // 반복자를 생성해서 리턴해준다.
    public ListIterator listIterator() {
        return new ListIterator();
    }
 
    public class ListIterator {
        private Node lastReturned;
        private Node next;
        private int nextIndex;
 
        ListIterator() {
            next = head;
            nextIndex = 0;
        }
 
        // 본 메소드를 호출하면 cursor의 참조값이 기존 cursor.next로 변경된다.
        public Object next() {
            lastReturned = next;
            next = next.next;
            nextIndex++;
            return lastReturned.data;
        }
 
        // cursor의 값이 없다면 다시 말해서 더 이상 next를 통해서 가져올 노드가 없다면 false를 리턴한다.
        // 이를 통해서 next를 호출해도 되는지를 사전에 판단할 수 있다.
        public boolean hasNext() {
            return nextIndex < size();
        }
 
        public boolean hasPrevious() {
            return nextIndex > 0;
        }
 
        public Object previous() {
            if (next == null) {
                lastReturned = next = tail;
            } else {
                lastReturned = next = next.prev;
            }
            nextIndex--;
            return lastReturned.data;
        }
 
        public void add(Object input) {
            Node newNode = new Node(input);
            if (lastReturned == null) {
                head = newNode;
                newNode.next = next;
            } else {
                lastReturned.next = newNode;
                newNode.prev = lastReturned;
                if (next != null) {
                    newNode.next = next;
                    next.prev = newNode;
                } else {
                    tail = newNode;
                }
            }
            lastReturned = newNode;
            nextIndex++;
            size++;
        }
 
        public void remove() {
            if (nextIndex == 0) {
                throw new IllegalStateException();
            }
            Node n = lastReturned.next;
            Node p = lastReturned.prev;
 
            if (p == null) {
                head = n;
                head.prev = null;
                lastReturned = null;
            } else {
                p.next = next;
                lastReturned.prev = null;
            }
 
            if (n == null) {
                tail = p;
                tail.next = null;
            } else {
                n.prev = p;
            }
 
            if (next == null) {
                lastReturned = tail;
            } else {
                lastReturned = next.prev;
            }
 
            size--;
            nextIndex--;
        }
    }
}
```