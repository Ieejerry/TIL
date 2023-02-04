# LinkedList - Java 구현

`ArrayList`와 `LinkedList` 모두 `List`에 대해서 구현방법만 달리한 것이다. 따라서 사용방법은 거의 같다.

</br>

## 객체생성

우선 두개의 파일을 만들겠다.

</br>

LinkedList.java

``` java
package list.linkedlist.implementation;
 
public class LinkedList {
    
}
```

</br>

Main.java

``` java
package list.linkedlist.implementation;
 
public class Main {
    public static void main(String[] args) {
        LinkedList numbers = new LinkedList();
    }
}
```

</br>

## 노드(버텍스) 구현

`LinkedList`에서 가장 중요한 것이 바로 노드의 구현이다. 노드는 실제로 데이터가 저장되는 그릇과 같은 것이기 때문에 이것부터 구현을 시작한다. 자바는 객체지향 언어이기 때문에 노드는 객체로 만들기 딱 좋은 대상이다. 그리고 노드 객체는 리스트의 내부 부품이기 때문에 외부에는 노출되지 않는 것이 좋다. 그래서 `private`으로 지정했다. 사용자는 이 객체에 대해서 알 필요가 없다. 단지 값을 넣고 빼는 것으로 충분하다.

`head`는 첫번째 노드를 지정하는 참조값이다. `tail`은 마지막 노드를 지정한다. `size`는 노드의 크기를 의미한다. 노드를 변경할 때마다 이 값들을 수정해야 한다. `tail`이나 `size`는 마지막 노드를 찾거나 노드의 수를 셀 때 연산의 횟수를 획기적으로 줄여준다.

객체 `Node`는 내부적으로 `data`와 `next` 변수를 가지고 있다. `data`는 노드의 값이고, `next`는 다음 노드를 가리키는 참조값이다.

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2947.png)

</br>

이상의 내용을 코드화 시켜보겠다.

</br>

``` java
public class LinkedList {
    // 첫번째 노드를 가리키는 필드
    private Node head;
    private Node tail;
    private int size = 0;

    private class Node {
        // 데이터가 저장될 필드
        private Object data;
        // 다음 노드를 가리키는 필드
        private Node next;
        public Node(Object input) {
            this.data = input;
            this.next = null;
        }
        // 노드의 내용을 쉽게 출력해서 확인해볼 수 있는 기능
        public String toString() {
            return String.valueOf(this.data);
        }
    }
}
```

</br>

## 데이터 추가

</br>

### 시작에 추가

</br>

``` java
public void addFirst(Object input) {
    // 노드를 생성한다.
    Node newNode = new Node(input);
    // 새로운 노드의 다음 노드로 해드를 지정한다.
    newNode.next = head;
    // 헤드로 새로운 노드를 지정한다.
    head = newNode;
    size++;
    if(head.next == null) {
        tail = head;
    }
}
```

</br>

### 끝에 추가

리스트의 끝에 데이터를 추가할 때는 `tail`을 사용한다. `tail`이 없이도 구현이 가능하다. 하지만 `tail`이 없다면 마지막 노드를 찾아야 한다. 리스트의 끝에 데이터를 추가하는 작업은 자주 있는 작업이고, 마지막 노드를 찾는 작업은 첫 노드부터 마지막 노드까지 순차적으로 탐색을 해야 하기 때문에 최악의 상황이라고 할 수 있다. 그래서 `tail`을 사용한다.

</br>

``` java
public void addLast(Object input) {
    // 노드를 생성한다.
    Node newNode = new Node(input);
    // 리스트의 노드가 없다면 첫번째 노드를 추가하는 메소드를 사용한다.
    if(size == 0) {
        addFirst(input);
    } else {
        // 마지막 노드의 다음 노드로 생성한 노드를 지정한다.
        tail.next = newNode;
        // 마지막 노드를 갱신한다.
        tail = newNode;
        // 엘리먼트의 개수를 1 증가 시킨다.
        size++;
    }
}
```

</br>

### 중간에 추가

중간에 노드를 추가하는 방법에 앞서 특정 위치의 노드를 찾아내는 방법을 먼저 알아보겠다.

</br>

``` java
Node node(int index) {
    Node x = head;
    for (int i = 0; i < index; i++)
        x = x.next;
    return x;
}
```

</br>

이제 `node` 메소드를 이용해서 특정 위치에 노드를 추가하는 메소드를 만들어보겠다.

</br>

``` java
public void add(int k, Object input) {
    // 만약 k가 0이라면 첫번째 노드에 추가하는 것이기 때문에 addFirst를 사용한다.
    if(k == 0) {
        addFirst(input);
    } else {
        Node temp1 = node(k - 1);
        // k 번째 노드를 temp2로 지정한다.
        Node temp2 = temp1.next;
        // 새로운 노드를 생성한다.
        Node newNode = new Node(input);
        // temp1의 다음 노드로 새로운 노드를 지정한다.
        temp1.next = newNode;
        // 새로운 노드의 다음 노드로 temp2를 지정한다.
        newNode.next = temp2;
        size++;
        // 새로운 노드의 다음 노드가 없다면 새로운 노드가 마지막 노드이기 때문에 tail로 지정한다.
        if(newNode.next == null) {
            tail = newNode;
        }
    }
}
```

</br>

## 출력

데이터가 추가 되고 있는지 확인하는 방법이 필요하다. `LinkedList`의 `toString` 메소드를 구현해서 리스트가 제대로 만들어지고 있는지는 확인하는 코드를 작성해보겠다.

</br>

``` java
public String toString() {
    // 노드가 없다면 []를 리턴한다.
    if(head == null) {
        return "[]";
    }       
    // 탐색을 시작한다.
    Node temp = head;
    String str = "[";
    // 다음 노드가 없을 때까지 반복문을 실행한다.
    // 마지막 노드는 다음 노드가 없기 때문에 아래의 구문이 마지막 노드는 제외된다.
    while(temp.next != null) {
        str += temp.data + ", ";
        temp = temp.next;
    }
    // 마지막 노드를 출력결과에 포함시킨다.
    str += temp.data;
    return str + "]";
}
```

</br>

``` java
LinkedList numbers = new LinkedList();
numbers.addLast(10);
numbers.addLast(20);
numbers.addLast(30);
System.out.println(numbers);
```

```
[10, 20, 30]
```

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
    size--;
    return returnData;
}
```

</br>

``` java
LinkedList numbers = new LinkedList();
numbers.addLast(5);
numbers.addLast(10);
numbers.addLast(20);
numbers.addLast(30);
System.out.println(numbers.removeFirst());
System.out.println(numbers);
```

```
5
[10, 20, 30]
```

</br>

### 중간의 데이터를 삭제

</br>

``` java
public Object remove(int k) {
    if(k == 0)
        return removeFirst();
    // k-1번째 노드를 temp의 값으로 지정한다.
    Node temp = node(k - 1);
    // 삭제 노드를 todoDeleted에 기록해 둔다. 
    // 삭제 노드를 지금 제거하면 삭제 앞 노드와 삭제 뒤 노드를 연결할 수 없다.  
    Node todoDeleted = temp.next;
    // 삭제 앞 노드의 다음 노드로 삭제 뒤 노드를 지정한다.
    temp.next = temp.next.next;
    // 삭제된 데이터를 리턴하기 위해서 returnData에 데이터를 저장한다.
    Object returnData = todoDeleted.data; 
    if(todoDeleted == tail) {
        tail = temp;
    }
    // cur.next를 삭제한다.
    todoDeleted = null; 
    size--;
    return returnData;
}
```

</br>

``` java
LinkedList numbers = new LinkedList();
numbers.addLast(10);
numbers.addLast(15);
numbers.addLast(20);
numbers.addLast(30);
System.out.println(numbers.remove(1));
System.out.println(numbers);
```

```
15
[10, 20, 30]
```

</br>

## 엘리먼트의 크기

엘리먼트의 크기를 알아내는 법은 간단하다. 내부적으로 `size`라는 값을 유지하고 있기 때문에 이 값을 돌려주기만 하면 된다.

</br>

``` java
public int size() {
    return size;
}
```

</br>

``` java
LinkedList numbers = new LinkedList();
numbers.addLast(10);
numbers.addLast(20);
numbers.addLast(30);
System.out.println(numbers.size());
```

```
3
```

</br>

## 엘리먼트 가져오기

</br>

``` java
public Object get(int k) {
    Node temp = node(k);
    return temp.data;
}
```

</br>

``` java
LinkedList numbers = new LinkedList();
numbers.addLast(10);
numbers.addLast(20);
numbers.addLast(30);
System.out.println(numbers.get(0));
System.out.println(numbers.get(1));
System.out.println(numbers.get(2));
```

```
10
20
30
```

</br>

## 탐색

특정한 값을 가진 엘리먼트의 인덱스 값을 알아내는 방법을 알아보겠다. 값이 있다면 그 값이 발견되는 첫번째 인덱스 값을 리턴하고 값이 없다면 -1을 리턴한다.

</br>

``` java
public int indexOf(Object data) {
    // 탐색 대상이 되는 노드를 temp로 지정한다.
    Node temp = head;
    // 탐색 대상이 몇번째 엘리먼트에 있는지를 의미하는 변수로 `index`를 사용한다.
    int index = 0;
    // 탐색 값과 탐색 대상의 값을 비교한다. 
    while(temp.data != data) {
        temp = temp.next;
        index++;
        // temp의 값이 null이라는 것은 더 이상 탐색 대상이 없다는 것을 의미한다.이 때 -1을 리턴한다.
        if(temp == null)
            return -1;
    }
    // 탐색 대상을 찾았다면 대상의 인덱스 값을 리턴한다.
    return index;
}
```

</br>

``` java
LinkedList numbers = new LinkedList();
numbers.addLast(10);
numbers.addLast(20);
numbers.addLast(30);
System.out.println(numbers.indexOf(10));
System.out.println(numbers.indexOf(20));
System.out.println(numbers.indexOf(30));
```

```
0
1
2
```

</br>

## 반복

</br>

### Iterator 객체 생성과 next 메소드

기본적인 반복작업은 아래와 같다.

</br>

``` java
for(int i = 0; i < numbers.size(); i++) {
    System.out.println(numbers.get(i));
}
```

</br>

위와 같은 방법으로 반복을 사용해도 되지만 `LinkedList`에서는 이것은 바람직하지 않은 방법이다. 왜냐하면 `ArrayList`와 다르게 `LinkedList`에서 `get`은 효율적이지 않기 때문이다. `get`을 호출할 때마다 내부적으로는 반복문이 실행된다. 이런 경우 `Iterator`를 사용하는 것이 유리하다. `Iterator`는 내부적으로 반복 처리된 노드가 무엇인지에 대한 정보를 유지하기 때문이다.

</br>

``` java
ListIterator it = numbers.listIterator();
while (it.hasNext()) {
    System.out.println(it.next());
}
```

</br>

`LinkedList`의 `listIterator` 메소드를 만들어보겠다.

</br>

``` java
// 반복자를 생성해서 리턴해준다.
public ListIterator listIterator() {
    return new ListIterator();
}
```

</br>

`ListIterator` 객체는 아래와 같다.

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

다음 노드의 값을 리턴하는 `next` 메소드의 코드는 아래와 같다.

</br>

``` java
// 본 메소드를 호출하면 cursor의 참조값이 기존 cursor.next로 변경된다. 
public Object next() {
    lastReturned = next;
    next = next.next;
    nextIndex++;
    return lastReturned.data;
}
```

</br>

``` java
LinkedList numbers = new LinkedList();
numbers.addLast(10);
numbers.addLast(20);
numbers.addLast(30);
LinkedList.ListIterator li = numbers.listIterator();
System.out.println(li.next());
System.out.println(li.next());
System.out.println(li.next());
```

```
10
20
30
```

</br>

### hasNext 

</br>

``` java
public boolean hasNext() {
    return nextIndex < size();
}
```

</br>

``` java
LinkedList numbers = new LinkedList();
numbers.addLast(10);
numbers.addLast(20);
numbers.addLast(30);
LinkedList.ListIterator li = numbers.listIterator();
while(li.hasNext()) {
    System.out.println(li.next());
}
```

```
10
20
30
```

</br>

### add

</br>

``` java
public void add(Object input) {
    Node newNode = new Node(input);
    if(lastReturned == null) {
        head= newNode;
        newNode.next = next;
    } else {
        lastReturned.next = newNode;
        newNode.next = next;
    }
    lastReturned = newNode;
    nextIndex++;
    size++;
}
```

</br>

``` java
LinkedList numbers = new LinkedList();
numbers.addLast(10);
numbers.addLast(30);
LinkedList.ListIterator li = numbers.listIterator();
while(li.hasNext()) {
    if((int)li.next() == 10)
        li.add(20);
}
System.out.println(numbers);
```

```
[10, 20, 30]
```

</br>

### remove

</br>

``` java
public void remove() {
    if(nextIndex == 0) {
        throw new IllegalStateException();
    }
    LinkedList.this.remove(nextIndex - 1);
    nextIndex--;
}
```

</br>

``` java
LinkedList numbers = new LinkedList();
numbers.addLast(10);
numbers.addLast(15);
numbers.addLast(20);
numbers.addLast(30);
LinkedList.ListIterator li = numbers.listIterator();
while(li.hasNext()) {
    if((int)li.next() == 15)
        li.remove();
}
System.out.println(numbers);
```

```
[10, 20, 30]
```

</br>

###  전체코드

</br>

LinkedList.java

``` java
package list.linkedlist.implementation;
 
public class LinkedList {
    // 첫번째 노드를 가리키는 필드
    private Node head;
    private Node tail;
    private int size = 0;

    private class Node {
        // 데이터가 저장될 필드
        private Object data;
        // 다음 노드를 가리키는 필드
        private Node next;
        public Node(Object input) {
            this.data = input;
            this.next = null;
        }
        // 노드의 내용을 쉽게 출력해서 확인해볼 수 있는 기능
        public String toString() {
            return String.valueOf(this.data);
        }
    }

    public void addFirst(Object input) {
        // 노드를 생성합니다.
        Node newNode = new Node(input);
        // 새로운 노드의 다음 노드로 해드를 지정한다.
        newNode.next = head;
        // 헤드로 새로운 노드를 지정한다.
        head = newNode;
        size++;
        if(head.next == null) {
            tail = head;
        }
    }

    public void addLast(Object input) {
        // 노드를 생성합니다.
        Node newNode = new Node(input);
        // 리스트의 노드가 없다면 첫번째 노드를 추가하는 메소드를 사용한다.
        if(size == 0) {
            addFirst(input);
        } else {
            // 마지막 노드의 다음 노드로 생성한 노드를 지정한다.
            tail.next = newNode;
            // 마지막 노드를 갱신합니다.
            tail = newNode;
            // 엘리먼트의 개수를 1 증가 시킨다.
            size++;
        }
    }
    Node node(int index) {
        Node x = head;
        for (int i = 0; i < index; i++)
            x = x.next;
        return x;
    }

    public void add(int k, Object input) {
        // 만약 k가 0이라면 첫번째 노드에 추가하는 것이기 때문에 addFirst를 사용한다.
        if(k == 0) {
            addFirst(input);
        } else {
            Node temp1 = node(k-1);
            // k 번째 노드를 temp2로 지정한다.
            Node temp2 = temp1.next;
            // 새로운 노드를 생성합니다.
            Node newNode = new Node(input);
            // temp1의 다음 노드로 새로운 노드를 지정한다.
            temp1.next = newNode;
            // 새로운 노드의 다음 노드로 temp2를 지정한다.
            newNode.next = temp2;
            size++;
            // 새로운 노드의 다음 노드가 없다면 새로운 노드가 마지막 노드이기 때문에 tail로 지정한다.
            if(newNode.next == null) {
                tail = newNode;
            }
        }
    }

    public String toString() {
        // 노드가 없다면 []를 리턴한다.
        if(head == null) {
            return "[]";
        }       
        // 탐색을 시작합니다.
        Node temp = head;
        String str = "[";
        // 다음 노드가 없을 때까지 반복문을 실행한다.
        // 마지막 노드는 다음 노드가 없기 때문에 아래의 구문은 마지막 노드는 제외된다.
        while(temp.next != null) {
            str += temp.data + ",";
            temp = temp.next;
        }
        // 마지막 노드를 출력결과에 포함시킨다.
        str += temp.data;
        return str+"]";
    }

    public Object removeFirst() {
        // 첫번째 노드를 temp로 지정하고 head의 값을 두번째 노드로 변경한다.
        Node temp = head;
        head = temp.next;
        // 데이터를 삭제하기 전에 리턴할 값을 임시 변수에 담는다. 
        Object returnData = temp.data;
        temp = null;
        size--;
        return returnData;
    }

    public Object remove(int k) {
        if(k == 0)
            return removeFirst();
        // k-1번째 노드를 temp의 값으로 지정한다.
        Node temp = node(k-1);
        // 삭제 노드를 todoDeleted에 기록해 둔다. 
        // 삭제 노드를 지금 제거하면 삭제 앞 노드와 삭제 뒤 노드를 연결할 수 없다.  
        Node todoDeleted = temp.next;
        // 삭제 앞 노드의 다음 노드로 삭제 뒤 노드를 지정한다.
        temp.next = temp.next.next;
        // 삭제된 데이터를 리턴하기 위해서 returnData에 데이터를 저장한다.
        Object returnData = todoDeleted.data; 
        if(todoDeleted == tail) {
            tail = temp;
        }
        // cur.next를 삭제한다.
        todoDeleted = null; 
        size--;
        return returnData;
    }

    public Object removeLast() {
        return remove(size-1);
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
        while(temp.data != data) {
            temp = temp.next;
            index++;
            // temp의 값이 null이라는 것은 더 이상 탐색 대상이 없다는 것을 의미한다.이 때 -1을 리턴한다.
            if(temp == null)
                return -1;
        }
        // 탐색 대상을 찾았다면 대상의 인덱스 값을 리턴한다.
        return index;
    }
 
    // 반복자를 생성해서 리턴해준다.
    public ListIterator listIterator() {
        return new ListIterator();
    }
     
    class ListIterator {
        private Node lastReturned;
        private Node next;
        private int nextIndex;
         
        ListIterator() {
            next = head;
            nextIndex = 0;
        }
         
        // 본 메소드를 호출하면 next의 참조값이 기존 next.next로 변경된다. 
        public Object next() {
            lastReturned = next;
            next = next.next;
            nextIndex++;
            return lastReturned.data;
        }
         
        public boolean hasNext() {
            return nextIndex < size();
        }
         
        public void add(Object input) {
            Node newNode = new Node(input);
            if(lastReturned == null) {
                head= newNode;
                newNode.next = next;
            } else {
                lastReturned.next = newNode;
                newNode.next = next;
            }
            lastReturned = newNode;
            nextIndex++;
            size++;
        }
         
        public void remove() {
            if(nextIndex == 0) {
                throw new IllegalStateException();
            }
            LinkedList.this.remove(nextIndex - 1);
            nextIndex--;
        }    
    }
}
```