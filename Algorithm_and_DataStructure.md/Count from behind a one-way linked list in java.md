# 단방향 Linked List 뒤부터 세기 in Java

</br>

## 단방향 LinkedList의 끝에서 k번째 노드 찾기

</br>

[![2023-04-10-1-38-39.png](https://i.postimg.cc/Xv5N6TRv/2023-04-10-1-38-39.png)](https://postimg.cc/kVnPxhXr)

</br>

단방향 LinkedList 같은 경우, 항상 맨앞에서부터 순차적으로 카운터를 시작하기 떄문에 뒤에서 부터 카운트를 시작하는 방법에 대해 알아보겠다.

</br>

### 방법 1. 전체 길이 - k + 1

LinkedList의 맨처음 노드부터 순차적으로 이동하면서 전체 노드의 개수를 카운트하고, `전체 노드 개수 - k + 1`의 노드를 찾는다.

</br>

``` java
    int k = 2;
    Node kth = KthToLast(first, k);
    System.out.println("Last k(" + k + ")th data is " + kth.data);
}

private static Node KthToLast(Node first, int k) {
    Node n = first;
    int total = 1;
    while(n.next != null)  {
        total++;
        n = n.next;
    }
    n = first;
    for(int i = 1; i < total - k + 1; i++) {
        n = n.next;
    }
    return n;
}
```

</br>

### 방법 2. 재귀호출

재귀호출은 조건이 만족할 때까지 자신을 계속 호출하는데, 여기서 끝까지 들어갔다가 나올 때 뒤에서부터 세면서 나오면 된다.

첫번째 노드를 가지고 함수를 호출한다. 이 함수는 자기가 받은 노드의 다음 노드를 가지고 자기 자신을 또 호출하는 것이다. 이 함수에는 노드가 `null`이 될 때까지 계속 자기 자신을 재귀호출한다. 노드가 `null`일 경우, 이 함수는 0을 반환한다. 그리고 반환값에 계속 1를 더해서, 반환을 한다.

그러면 맨 처음 노드에서는 k값을 가지고 끝까지 갔다가, 하나씩 나오면서 +1를 한다. 그리고 최종 반환값과 k값을 비교해서 k가 몇 번째 노드인지 알 수 있게 된다.

</br>

``` java
private static int KthToLast(Node n, int k) {
    if(n == null) {
        return 0;
    }

    int count = KthToToLast(n.next, k) + 1;
    if(count == k) {
        System.out.println(k + "th to last node is " + n.data);
    }
    return count;
}
```

</br>

하지만 위의 코드는 `Node`의 값을 반환하는 거지, `Node`를 반환하는 것이 아니기 때문에 `Node` 객체를 반환하는 코드로 수정하겠다.

</br>

``` java
class Reference {
    public int count = 0;
}

private static Node KthToLast(Node n, int k, Reference r) {
    if(n == null) {
        return null;
    }

    Node found = KthToToLast(n.next, k, r) + 1;
    r.count++;
    if(r.count == k) {
        return n;
    }
    return found;
}
```

</br>

#### 공간복잡도와 시간복잡도

LinkedList의 길이를 n으로 볼 때, O(n)의 공간을 사용하는 알고리즘이며, LinkedList의 맨 처음부터 맨 끝까지 갔다가 최악의 경우, 맨 앞까지 다시 돌아와야하기 때문에 시간복잡도는 O(2n), 상수를 제외하면 시간복잡도는 O(n)이 된다.

</br>

### 방법 3. 포인터

공간을 전혀 사용하지 않고, 구현하는 방법이 있는데, 포인터를 두 개를 선언해서 한 개(p1)를 k만큼 먼저 앞으로 가게 해두고, 다른 한 개의 포인터(p2)를 맨 앞 노드에 그대로 둔 상태에서, 포인터 두 개를 동시에 하나씩 이동을 시킨다. 그렇게 하나씩 이동하다가 두 포인터 중, 먼저 null을 만나면 그 때 뒤에 따라오던 포인터의 노드가 k번째가 된다.

</br>

``` java
private static Node KthToLast(Node first, int k) {
    Node p1 = first;
    Node p2 = first;

    for(int i = 0; i < k; i++) {
        if(p1 == null) {
            return null;
        }
        p1 = p1.next;
    }

    while(p1 != null) {
        p1 = p1.next;
        p2 = p2.next;
    }
    return p2;
}
```

</br>

이렇게 포인터를 사용한 알고리즘은 O(n)의 시간복잡도를 갖고, 공간을 별도의 버퍼를 사용하지 않으므로 O(1)의 공간복잡도를 갖는다.