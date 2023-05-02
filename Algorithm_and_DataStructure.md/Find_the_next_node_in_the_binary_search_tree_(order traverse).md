# 이진검색트리에서 다음노드 찾기 (inorder traverse)

</br>

[![2023-05-01-3-00-30.png](https://i.postimg.cc/xjh5dKT9/2023-05-01-3-00-30.png)](https://postimg.cc/Thjg75Ds)

</br>

[![2023-05-01-3-09-13.png](https://i.postimg.cc/rFfsq99p/2023-05-01-3-09-13.png)](https://postimg.cc/CzfSNkXy)

</br>

inorder순으로 임의의 노드의 다음 노드를 찾는 문제이다. inorder순은 어떤 노드든 호출된 순간 left -> root -> right 순으로 방문을 시도한다. 어떤 노드의 다음 노드는 그 노드의 위에 있을 수도 있고, 노드의 아래에 있을 수 있다. 만약에 주어진 노드의 오른쪽 자식 노드가 있으면 아래에 있는 것이고, 오른쪽 자식 노드가 없으면 위에 있는 것이다.

오른쪽 자식 노드가 있는 경우를 먼저 보면 inorder는 나 자신을 출력하고 오른쪽으로 간다. 바로 오른쪽 노드가 다음 노드이면 좋겠지만, 노드에 도착하면 먼저 inorder순서에 입각해서 left가 있는지 확인한다. 그리고 left가 있으면 left를 우선 방문한다. 그런데 여기서 left가 또 있으면 또 들어간다. 그러면 결국 left로 타고 들어간 줄기의 맨 마지막 노드가 다음 노드가 된다.

오른쪽 자식 노드가 없는 경우를 보면 오른쪽 노드가 없으면 다음 노드는 위에 있다는 뜻이다. 오른쪽 노드가 없다는 것은 해당 노드 선상에서는 방문을 완료한 것이기 때문에 호출한 부모 노드에게 control이 반환된다. 이 때 자신이 부모의 왼쪽 자식이였는지, 오른쪽 자식이였는지를 알아야 한다. 왼쪽 자식이였다면 inorder의 순서에 입각해서 부모가 다음 순서가 되겠지만, 만약에 오른쪽 자식이였다면 부모는 이미 출력한 상태이기 때문에 부모의 부모에게 가서 다시 확인한다. 내 부모가 조부모의 왼쪽 자식이였는지, 오른쪽 자식이였는지를 확인한다. 트리가 길어서 계속 오른쪽 자식이였다면 계속 반복하며 타고 올라가다가 어느 순간 이 노드가 왼쪽 자식으로써 호출된 경우를 만나면 그 부모 노드가 다음 노드가 된다.

</br>

### 전체 코드

</br>

``` java
package DataStructure;

class Tree8 {	// 트리 생성  
	class Node {	// 노드 생성 
		int data;
		Node left;
		Node right;
		Node parent;	// 부모 노드 저장할 변수 
		
		Node(int data) {
			this.data = data;
		}
	}
	
	Node root;	// 루트 노드 저장 
	
	Tree8(int size) {	// 트리를 생성하면 이진 검색 트리 생성 
		root = makeBST(0, size - 1, null);
	}
	
	Node makeBST(int start, int end, Node parent) {	// 이진 검새 트리 생성하는 함수 
		if(start > end) return null;
		int mid = (start + end) / 2;
		Node node = new Node(mid);
		node.left = makeBST(start, mid - 1, node);
		node.right = makeBST(mid + 1, end, node);
		node.parent = parent;
		return node;
	}
	
	void findNext(Node node) {	// 다음 노드를 찾는 함수 
		if(node.right == null) {	// 오른쪽 노드가 없는 경우 
			System.out.println(findAbove(node.parent, node).data + " is " + node.data + "'s next");	// 위에서 찾기, 재귀 함수를 호출할 때, 부모 노드와 함께 현재 노드도 인자로 넘김 그래야 내가 어느 쪽 자식이였는지를 확인 가능 
		} else {	// 오른쪽 자식이 있으면 아래에서 찾기 
			System.out.println(findBelow(node.right).data + " is " + node.data + "'s next");
		}
	}
	
	Node findAbove(Node root, Node child) {	// 위에서 찾는 함수 
		if(root == null) return null;	// null Exception  처리 
		if(root.left == child) return root;	// 부모의 왼쪽 노드가 자신과 같으면 그 부모가 바로 다음 노드이기 때문에 부모 노드를 반환 
		return findAbove(root.parent, root);	// 그렇지 않으면 또 부모의 부모를 가지고 해당 함수를 다시 호출, 이 때 부모의 노드도 같이 보내서 부모가 조부모의 어느 쪽 자식이였는지를 비교 
	}
	
	Node findBelow(Node root) {
		if(root.left == null) return root;	// 돌다가 재귀 호출을 멈추는 순간은 왼쪽의 더 이상 자식이 없을 때, 해당 노드가 다음 노드가 된다. 
		return findBelow(root.left);	// 왼쪽 자식 노드를 계속 넘겨주면서 반복적으로 실행해서 맨 마지막 왼쪽 노드를 찾기 
	}
}

public class InorderTest2 {
	public static void main(String[] args) {
		Tree8 t = new Tree8(10);	// 트리 생성 
		t.findNext(t.root.left.right.right);
		t.findNext(t.root.left);
		t.findNext(t.root);
		t.findNext(t.root.left.left);
		t.findNext(t.root.right.left.right);
	}
}
```

```
4 is 3's next
2 is 1's next
5 is 4's next
1 is 0's next
7 is 6's next
```