# Binary Tree의 3가지 순회방법 구현하기

</br>

[![2023-04-22-5-44-36.png](https://i.postimg.cc/wTWKDDrv/2023-04-22-5-44-36.png)](https://postimg.cc/4mhFgHsk)

</br>

## Tree에서 데이터를 가져오는 방법

Binary Tree을 횡단하면서 트리의 모든 데이터를 가져오는 방법에는 `Inorder`, `Preorder`, `Postorder` 이렇게 세 가지가 있다.

</br>

### Inorder

</br>

[![2023-04-22-5-48-06.png](https://i.postimg.cc/05X1hLYn/2023-04-22-5-48-06.png)](https://postimg.cc/grh7ZtBL)

</br>

Inorder는 root 노드를 시작으로 root 노드의 왼쪽이 먼저, 그 다음은 호출한 노드, 오른쪽 노드 즉, Left -> Root -> Right 순으로 횡단한다.

위의 그림의 1부터 시작해서 왼쪽 2로 가고, 2에서 왼쪽이 먼저이기 때문에 4로 간다. 4 노드에는 더 이상 자식 노드가 없기 때문에 4를 출력한다. 그 다음 올라가서 왼쪽 다음에 호출한 노드인 2를 출력하고, 오른쪽 노드 5로 간다. 오른쪽 노드도 자식 노드가 없기 때문에 5를 출력하고, 2를 호출한 노드 1로 올라가서, 왼쪽 노드는 다 호출했기 때문에 1를 출력한다. 마지막으로 오른쪽 노드로 이동하는데, 오른쪽 노드 3도 자식 노드가 없기 때문에 3을 출력하고 끝이 난다.

</br>

[![2023-04-22-5-54-00.png](https://i.postimg.cc/RZyDRmz6/2023-04-22-5-54-00.png)](https://postimg.cc/xXG5fW8n)

</br>

### Preorder

</br>

[![2023-04-22-5-55-52.png](https://i.postimg.cc/43FVt4Cq/2023-04-22-5-55-52.png)](https://postimg.cc/VSnJP8kW)

</br>

Preorder의 'Pre'의 의미는 bofore, 먼저, 미리, 전에 그런 뜻이다. 그래서 자기 자신을 먼저 출력하고, 그 다음에 왼쪽, 그리고 오른쪽 순으로 횡단한다.

1부터 시작해서 자기 자신을 먼저 출력하고, 왼쪽 노드 2로 이동한다. 그리고 자기 자신 2를 출력하고, 왼쪽 노드 4로 이동하여, 4를 출력하고 더 이상 자식 노드가 없기 때문에 다시 위로 올라가서, 오른쪽 노드 5로 이동하여 5를 출력한다. 노드 5도 더 이상 자식 노드가 없기 때문에 노드 2로 이동하고, 노드 2는 미리 출력을 하였기 때문에 다시 노드 1로 올라간다. 노드 1도 미리 출력하였기 때문에 오른쪽 노드 3으로 이동하여 3을 출력한다. 노드 3은 자식 노드를 갖고 있지 않기 때문에 끝이 난다.

</br>

[![2023-04-22-5-59-09.png](https://i.postimg.cc/76KHbhpJ/2023-04-22-5-59-09.png)](https://postimg.cc/47hkSf4X)

</br>

### Postorder

</br>

[![2023-04-22-6-01-36.png](https://i.postimg.cc/zvn1KfQk/2023-04-22-6-01-36.png)](https://postimg.cc/p5X7tPR9)

</br>

Postorder의 'Post'는 after, 나중에, 후에 라는 뜻이다. 순환 순서는 왼쪽 -> 오른쪽 -> 자기 자신 순으로 출력한다.

1부터 시작해서 왼쪽 노드 2부터 들어가고, 이어서 왼쪽 노드 4로 바로 들어간다. 4에서 더 이상 자식 노드가 없기 때문에 4를 출력하고, 올라가서 자기 자신을 출력하기 전에, 오른쪽 노드 5로 이동하여 5를 출력하고 올라와서 왼쪽, 오른쪽 모두 출력하였으니, 자기 자신 노드 2를 출력하고, 다시 노드 1로 올라가서 왼쪽은 다 출력하였고, 다시 오른쪽 노드 3으로 이동하여 3을 출력하고, 노드 3은 자식 노드가 없기 때문에 다시 노드 1로 올라가서 1을 출력하고 끝이 난다.

</br>

[![2023-04-22-6-04-55.png](https://i.postimg.cc/mDkDY73y/2023-04-22-6-04-55.png)](https://postimg.cc/N9hBY9zK)

</br>

## 전체코드

</br>

``` java
package DataStructure;

class Node2 {
	int data;
	Node2 left;
	Node2 right;
}

class Tree {
	public Node2 root;
	
	public void setRoot(Node2 node) {
		this.root = node;
	}
	
	public Node2 getRoot() {
		return root;
	}
	
	public Node2 makeNode(Node2 left, int data, Node2 right) {
		Node2 node = new Node2();
		node.data = data;
		node.left = left;
		node.right = right;
		return node;
	}
	
	public void inorder(Node2 node) {
		if(node != null) {
			inorder(node.left);
			System.out.println(node.data);
			inorder(node.right);
		}
	}
	
	public void preorder(Node2 node) {
		if(node != null) {
			System.out.println(node.data);
			preorder(node.left);
			preorder(node.right);
		}
	}
	
	public void postorder(Node2 node) {
		if(node != null) {
			postorder(node.left);
			postorder(node.right);
			System.out.println(node.data);
		}
	}
}

public class TreeTest {
	public static void main(String[] args) {
		Tree t = new Tree();
		Node2 n4 = t.makeNode(null, 4, null);
		Node2 n5 = t.makeNode(null, 5, null);
		Node2 n2 = t.makeNode(n4, 2, n5);
		Node2 n3 = t.makeNode(null, 3, null);
		Node2 n1 = t.makeNode(n2, 1, n3);
		t.setRoot(n1);
		t.inorder(t.getRoot());
		System.out.println();
		t.preorder(t.getRoot());
		System.out.println();
		t.postorder(t.getRoot());	
	}
}
```

```
4
2
5
1
3

1
2
4
5
3

4
5
2
3
1
``` 