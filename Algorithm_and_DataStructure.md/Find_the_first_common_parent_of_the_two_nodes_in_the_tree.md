# Tree에서 두노드의 첫번째 공통부모 찾기

</br>

[![2023-05-05-1-15-23.png](https://i.postimg.cc/PJP4ptgC/2023-05-05-1-15-23.png)](https://postimg.cc/30QpzHJh)

</br>

## Solution 1 - 길이 맞추기

</br>

[![2023-05-05-7-49-01.png](https://i.postimg.cc/hvkQGsSz/2023-05-05-7-49-01.png)](https://postimg.cc/rR9wnSRM)

</br>

이진트리에서 임의의 두 노드의 첫 번째 공통되는 부모 노드를 찾아야한다. 하지만 두 노드가 공통되는 부모의 노드까지의 길이가 다를 수 있기 때문에 두 노드간의 길이를 맞춰줘야 한다. 그래서 각 노드부터 root까지의 길이를 재고, 길이가 긴 노드와 짧은 노드의 차이를 계산해서 길이가 긴 노드가 그 차이만큼 올라간다. 그리고 둘이 같이 한칸씩 올라가면서 비교를 한다. 올라가다가 두 노드가 같은 노드를 가리키게 되면 바로 그 노드가 첫 번째 공통되는 부모 노드가 된다. 이 알고리즘은 트리의 깊이 만큼만 가면 되기 떄문에 트리의 깊이가 d이라고 했을 때, O(d)만큼의 시간 복잡도를 갖는다.

</br>

### Solution 1 코드

</br>

``` java
package DataStructure;

import java.util.HashMap;

class Tree9 {
	static class Node {	// 노드 생성 
		int data;
		Node left;
		Node right;
		Node parent;	// 부모 노드 저장할 변수 
		
		Node(int data) {	// 생성자로 멤버변수에 data 대입 
			this.data = data;
		}
	}
	
	Node root;	// root를 저장 
	HashMap<Integer, Node> rootMap;	// 값으로 root를 찾기 쉽게 Map 선언
	
	Tree9(int size) {
		rootMap = new HashMap<>();	// Tree를 생성할 때 Map을 준비 
		root = makeBST(0, size - 1, null);	// 이진트리를 만드는 함수 호출 
	}
	
	Node makeBST(int start, int end, Node parent) {	// 이진 검새 트리 생성하는 함수 
		if(start > end) return null;
		int mid = (start + end) / 2;
		Node node = new Node(mid);
		node.left = makeBST(start, mid - 1, node);
		node.right = makeBST(mid + 1, end, node);
		node.parent = parent;
		rootMap.put(mid, node);	// 이진 트리를 만들 때, 값으로 노드를 찾아올 수 있게 Map에 노드를 추가 
		return node;
	}
	
	Node getNode(int data) {	// 값으로 노드를 가져오는 함수 
		return rootMap.get(data);
	}
	
	Node commonAncestor(int d1, int d2) {	// 공통 부모를 찾는 함수 
		Node p = getNode(d1);
		Node q = getNode(d2);
		int diff = depth(p) - depth(q);	// root부터 각 노드까지의 길이의 차이 계산 
		Node first = diff > 0 ? q : p;	// 길이가 짧은 걸 first에 대입 
		Node second = diff > 0 ? p : q;	// 길이가 긴 걸 second에 대입 
		second = goUpBy(second, Math.abs(diff));	// 긴 것을 차이만큼 올라가서 양쪽 노드의 길이를 맞춰주는 함수 
		while(first != second && first != null && second != null) {	// 한 칸씩 둘이 같이 올라가면서 둘이 만나는 지점을 찾음
			first = first.parent;
			second = second.parent;
		}
		return first == null || second == null ? null : first;	// 둘 중 하나가 먼저 root를 지나치면 그냥 나오고, 두개 다 null이 아닌 상태로 while문을 나오면 first 노드 반환 
	}
	
	Node goUpBy(Node node, int diff) {	// 노드와 숫자를 받아서 그 숫자만큼 노드가 위로 올라가는 함수 
		while(diff > 0 && node != null) {
			node = node.parent;
			diff--;
		}
		return node;
	}
	
	int depth(Node node) {	// 노드에 root까지의 길이 구하는 함수 
		int depth = 0;
		while(node != null) {
			node = node.parent;
			depth++;
		}
		return depth;
	}
}

public class CommonParentTest {
	public static void main(String[] args) {
		Tree9 t = new Tree9(10);
		Tree9.Node fa = t.commonAncestor(3, 5);
		System.out.println("The first common ancestor is " + fa.data);
	}
}
```

```
The first common ancestor is 4
```

</br>

## Solution 2 - 형제 검색

</br>

[![2023-05-05-7-50-13.png](https://i.postimg.cc/y6mgHwtB/2023-05-05-7-50-13.png)](https://postimg.cc/V5NL9HzH)

</br>

트리의 깊이 너무 깊어 root와의 거리가 아주 멀고, 두 개의 노드가 서로 근처에 있을 확률이 있을 경우, 하나의 노드를 잡고, 올라가면서 그 주변에 자신이 찾는 노드가 있는지 확인하면 더 빨리 찾을 수 있다. 예를 들어 노드 15와 10의 공통 부모를 찾는다. 우선 노드 15의 부모 노드로 올라가서 그 부모 노드의 자식 노드의 서브 트리에 다른 찾는 노드가 있는지 확인한다. 없으면 다시 올라가서 그 부모의 부모 노드 0의 자식 노드 서브 트리에 찾는 노드가 있는지 확인한다. 그래도 없으면 한 번 더 올라가서 노드 1의 다른 자식 노드 서브 트리에 찾는 노드 10이 있는지 확인한다. 그 서브 트리 안에 찾던 노드 10을 발견했다. 그러면 노드 1이 첫 번째 공통 부모 노드인 것을 알게 되었다. 이 알고리즘은 첫 번째 공통 부모의 서브트리의 갯수를 t이라고 할 때, O(t)의 시간복잡도를 갖는다. 만약 최악의 경우 root가 공통부모일 경우 O(n)의 시간 복잡도를 갖는다.

</br>

### Solution 2 코드

</br>

``` java
package DataStructure;

import java.util.HashMap;

class Tree9 {
	static class Node {	// 노드 생성 
		int data;
		Node left;
		Node right;
		Node parent;	// 부모 노드 저장할 변수 
		
		Node(int data) {	// 생성자로 멤버변수에 data 대입 
			this.data = data;
		}
	}
	
	Node root;	// root를 저장 
	HashMap<Integer, Node> rootMap;	// 값으로 root를 찾기 쉽게 Map 선언
	
	Tree9(int size) {
		rootMap = new HashMap<>();	// Tree를 생성할 때 Map을 준비 
		root = makeBST(0, size - 1, null);	// 이진트리를 만드는 함수 호출 
	}
	
	Node makeBST(int start, int end, Node parent) {	// 이진 검새 트리 생성하는 함수 
		if(start > end) return null;
		int mid = (start + end) / 2;
		Node node = new Node(mid);
		node.left = makeBST(start, mid - 1, node);
		node.right = makeBST(mid + 1, end, node);
		node.parent = parent;
		rootMap.put(mid, node);	// 이진 트리를 만들 때, 값으로 노드를 찾아올 수 있게 Map에 노드를 추가 
		return node;
	}
	
	Node getNode(int data) {	// 값으로 노드를 가져오는 함수 
		return rootMap.get(data);
	}
	
	Node commonAncestor(int d1, int d2) {	// 공통 부모를 찾는 함수 
		Node p = getNode(d1);
		Node q = getNode(d2);
		int diff = depth(p) - depth(q);	// root부터 각 노드까지의 길이의 차이 계산 
		Node first = diff > 0 ? q : p;	// 길이가 짧은 걸 first에 대입 
		Node second = diff > 0 ? p : q;	// 길이가 긴 걸 second에 대입 
		second = goUpBy(second, Math.abs(diff));	// 긴 것을 차이만큼 올라가서 양쪽 노드의 길이를 맞춰주는 함수 
		while(first != second && first != null && second != null) {	// 한 칸씩 둘이 같이 올라가면서 둘이 만나는 지점을 찾음
			first = first.parent;
			second = second.parent;
		}
		return first == null || second == null ? null : first;	// 둘 중 하나가 먼저 root를 지나치면 그냥 나오고, 두개 다 null이 아닌 상태로 while문을 나오면 first 노드 반환 
	}
	
	Node goUpBy(Node node, int diff) {	// 노드와 숫자를 받아서 그 숫자만큼 노드가 위로 올라가는 함수 
		while(diff > 0 && node != null) {
			node = node.parent;
			diff--;
		}
		return node;
	}
	
	int depth(Node node) {	// 노드에 root까지의 길이 구하는 함수 
		int depth = 0;
		while(node != null) {
			node = node.parent;
			depth++;
		}
		return depth;
	}
	
	boolean covers(Node root, Node node) {	// 인자로 받은 노드가 root의 자손인지를 확인하는 함수 
		if(root == null) return false;	// root에 다다를 때까지 자손을 못 찾으면 false를 반
		if(root == node) return true; // 찾으면 true을 반환
		return covers(root.left, node) || covers(root.right, node);	// 해당 노드의 왼쪽, 오른쪽 자식 노드들을 검사 
	}
	
	Node commonAncestor2(int d1, int d2) {	// 공통 부모를 찾는 노드 
		Node p = getNode(d1);
		Node q = getNode(d2);
		if(!covers(root, p) || !covers(root, q)) {	// root에서 p, q의 존재 여부를 확인 
			return null;	// 이 값들이 시작 노드 밑에 없으면 null 반환 
		} else if(covers(p, q)) {	// p가 q의 부모 노드이면 p에서 두 노드가 처음 만남 
			return p;
		} else if(covers(q, p)) {	// q가 p의 부모 노드이면 q에서 두 노드가 처음 만남 
			return q;
		}
		Node sibling = getSibling(p);	// 그 외에는 형제 노드를 가져옴 
		Node parent = p.parent;	// 형제, 부모 노드 가져옴 
		while(!covers(sibling, q)) {	// 레벨을 한 칸씩 올라가면서 두 번째 노드가 형제의 하위 트리에 속해 있는지 확인 
			sibling = getSibling(parent);
			parent = parent.parent;
		}
		return parent;
	}
	
	Node getSibling(Node node) {	// 부모 노드를 받아와서 현재 노드가 부모의 어쪽 자식인지 확인하고, 반대쪽 자식 노드 반환해서 형제 노드를 가져옴  
		if(node == null || node.parent == null) {
			return null;
		}
		Node parent = node.parent;
		return parent.left == node ? parent.right : parent.left;
	}
}

public class CommonParentTest {
	public static void main(String[] args) {
		Tree9 t = new Tree9(10);
		Tree9.Node fa = t.commonAncestor2(0, 3);
		System.out.println("The first common ancestor is " + fa.data);
	}
}
```

</br>

## Solution 3 - 부모 노드가 없을 경우 

</br>

[![2023-05-05-8-19-43.png](https://i.postimg.cc/D0WD3rfY/2023-05-05-8-19-43.png)](https://postimg.cc/n9JTvQDv)

</br>

지금까지 부모 노드의 주소를 알고 있었지만, 만약에 부모 노드의 주소가 없을 경우, root에서부터 내려오면서 찾는 노드 p나 q가 이하 서브 트리에 존재하는지 확인한다. 예를 들어 노드 13이랑 15의 공통 부모를 찾는다고 하면 root에서 시작해서 p나 q가 왼쪽 서브 트리에 있는지, 오른쪽 서브 트리에 있는지 찾아보고 두 노드가 같은 서브 트리에 있으면 그쪽으로 가서 다시 물어보는 방식이다. 노드 1로 내려가서 노드 1의 왼쪽 서브 트리에 있는지, 오른쪽 서브 트리에 있는지 확인한다. 왼쪽 있으니, 노드 0으로 내려가서 p나 q가 왼쪽 서브 트리에 있는지, 오른쪽 서브 트리에 있는지 확인한다. 이번에는 양쪽에 하나씩 존재한다. 그러면 노드 0이 첫 번째 공통 부모가 된다. 이 알고리즘은 root에서 시작했을 때, 양쪽의 서브 트리에 존재하는지 확인할 때, p나 q 두 개 다 확인해야하기 때문에 O(2n)의 시간 복잡도를 갖고, 한 번 레벨이 내려갈 때마다 검색해야 하는 양이 절반씩 줄어들기 때문에  2n/2 그 다음은 2n/2<sup>2</sup>만큼 줄어 든다. 한 번 호출될 때마다 검색해야 하는 양이 절반씩 줄어들기 때문에 O(log n)이 된다. 그런데 호출 될 때마다 검색했던 곳을 반복적으로 또 검색을 하기 때문에 O(log n)<sup>2</sup>가 된다. O(log n)<sup>2</sup>는 O(n)보다 작기 때문에 O(n)으로 표시하면 된다.

</br>

### Solution 3 코드

</br>

``` java
package DataStructure;

import java.util.HashMap;

class Tree9 {
	static class Node {	// 노드 생성 
		int data;
		Node left;
		Node right;
		Node parent;	// 부모 노드 저장할 변수 
		
		Node(int data) {	// 생성자로 멤버변수에 data 대입 
			this.data = data;
		}
	}
	
	Node root;	// root를 저장 
	HashMap<Integer, Node> rootMap;	// 값으로 root를 찾기 쉽게 Map 선언
	
	Tree9(int size) {
		rootMap = new HashMap<>();	// Tree를 생성할 때 Map을 준비 
		root = makeBST(0, size - 1, null);	// 이진트리를 만드는 함수 호출 
	}
	
	Node makeBST(int start, int end, Node parent) {	// 이진 검새 트리 생성하는 함수 
		if(start > end) return null;
		int mid = (start + end) / 2;
		Node node = new Node(mid);
		node.left = makeBST(start, mid - 1, node);
		node.right = makeBST(mid + 1, end, node);
		node.parent = parent;
		rootMap.put(mid, node);	// 이진 트리를 만들 때, 값으로 노드를 찾아올 수 있게 Map에 노드를 추가 
		return node;
	}
	
	Node getNode(int data) {	// 값으로 노드를 가져오는 함수 
		return rootMap.get(data);
	}
	
	Node commonAncestor(int d1, int d2) {	// 공통 부모를 찾는 함수 
		Node p = getNode(d1);
		Node q = getNode(d2);
		int diff = depth(p) - depth(q);	// root부터 각 노드까지의 길이의 차이 계산 
		Node first = diff > 0 ? q : p;	// 길이가 짧은 걸 first에 대입 
		Node second = diff > 0 ? p : q;	// 길이가 긴 걸 second에 대입 
		second = goUpBy(second, Math.abs(diff));	// 긴 것을 차이만큼 올라가서 양쪽 노드의 길이를 맞춰주는 함수 
		while(first != second && first != null && second != null) {	// 한 칸씩 둘이 같이 올라가면서 둘이 만나는 지점을 찾음
			first = first.parent;
			second = second.parent;
		}
		return first == null || second == null ? null : first;	// 둘 중 하나가 먼저 root를 지나치면 그냥 나오고, 두개 다 null이 아닌 상태로 while문을 나오면 first 노드 반환 
	}
	
	Node goUpBy(Node node, int diff) {	// 노드와 숫자를 받아서 그 숫자만큼 노드가 위로 올라가는 함수 
		while(diff > 0 && node != null) {
			node = node.parent;
			diff--;
		}
		return node;
	}
	
	int depth(Node node) {	// 노드에 root까지의 길이 구하는 함수 
		int depth = 0;
		while(node != null) {
			node = node.parent;
			depth++;
		}
		return depth;
	}
	
	boolean covers(Node root, Node node) {	// 인자로 받은 노드가 root의 자손인지를 확인하는 함수 
		if(root == null) return false;	// root에 다다를 때까지 자손을 못 찾으면 false를 반
		if(root == node) return true; // 찾으면 true을 반환
		return covers(root.left, node) || covers(root.right, node);	// 해당 노드의 왼쪽, 오른쪽 자식 노드들을 검사 
	}
	
	Node commonAncestor2(int d1, int d2) {	// 공통 부모를 찾는 노드 
		Node p = getNode(d1);
		Node q = getNode(d2);
		if(!covers(root, p) || !covers(root, q)) {	// root에서 p, q의 존재 여부를 확인 
			return null;	// 이 값들이 시작 노드 밑에 없으면 null 반환 
		} else if(covers(p, q)) {	// p가 q의 부모 노드이면 p에서 두 노드가 처음 만남 
			return p;
		} else if(covers(q, p)) {	// q가 p의 부모 노드이면 q에서 두 노드가 처음 만남 
			return q;
		}
		Node sibling = getSibling(p);	// 그 외에는 형제 노드를 가져옴 
		Node parent = p.parent;	// 형제, 부모 노드 가져옴 
		while(!covers(sibling, q)) {	// 레벨을 한 칸씩 올라가면서 두 번째 노드가 형제의 하위 트리에 속해 있는지 확인 
			sibling = getSibling(parent);
			parent = parent.parent;
		}
		return parent;
	}
	
	Node getSibling(Node node) {	// 부모 노드를 받아와서 현재 노드가 부모의 어쪽 자식인지 확인하고, 반대쪽 자식 노드 반환해서 형제 노드를 가져옴  
		if(node == null || node.parent == null) {
			return null;
		}
		Node parent = node.parent;
		return parent.left == node ? parent.right : parent.left;
	}
	
	Node commonAncestor3(int d1, int d2) {	// 공통 부모를 찾는 노드 
		Node p = getNode(d1);
		Node q = getNode(d2);
		if(!covers(root, q) || !covers(root, q)) {	// p나 q가 트리 안에 존재하지 않으면 null 반
			return null;
		}
		return ancestorHelper(root, p, q); // 재귀 함수 호출 
	}
	
	Node ancestorHelper(Node root, Node p, Node q) {
		if(root == null || root == p || root == q) {	// 노드가 null이면 잎사귀 끝까지 왔으니 null을 반환 
			return root;	// 노드가 찾는 p나 q중에 하나까지 도달했으면 해당 노드를 반환 
		}
		boolean pIsOnLeft = covers(root.left, p);	// 노드 p가 왼쪽 트리에 있는지 확인 존재하지 않으면 오른쪽 트리에 존재 
		boolean qIsOnLeft = covers(root.left, q);	// 노드 q가 왼쪽 트리에 있는지 확인 존재하지 않으면 오른쪽 트리에 존재
		if(pIsOnLeft != qIsOnLeft) {	// 두 노드가 다른 방향이면 첫 번째 공통 분모 
			return root;
		}
		Node childSide = pIsOnLeft ? root.left : root.right;	// 두 노드가 같은 쪽으로 존재하면 같은 쪽으로 내려가 검색 
		return ancestorHelper(childSide, p, q);
	}
}

public class CommonParentTest {
	public static void main(String[] args) {
		Tree9 t = new Tree9(10);
		Tree9.Node fa = t.commonAncestor3(2, 8);
		System.out.println("The first common ancestor is " + fa.data);
	}
}
```

```
The first common ancestor is 4
```

</br>

## Solution 4 - 최적화 시키기

</br>

[![2023-05-05-9-09-31.png](https://i.postimg.cc/QCHGmBBh/2023-05-05-9-09-31.png)](https://postimg.cc/q6V5MvX5)

</br>

위의 방법 같은 경우, root에서부터 노드를 찾을 때까지 매번 서브 트리들을 죄다 검색하고, 다음 노드에서 검색했던 곳을 또 검색하기 때문에 비효율적인 면이 있다. 그래서 postorder로 모든 노드들을 딱 한 번씩만 돌면서 반환 받은 왼쪽과 오른쪽 노드를 보고 양쪽 다 노드를 찾아온 순간에 그 노드가 바로 공통 부모가 된다. 예를 들어 노드 15와 10의 공통 부모를 찾아보겠다. postorder는 Left -> Right -> root 순으로 검색을 한다. root에서부터 왼쪽으로 이동한다. 노드 1에 도착하고 왼쪽 노드가 있기 때문에 또 왼쪽으로 이동한다. 노드 0에 도착하고 왼쪽 노드가 또 있기 때문에 노드 13으로 이동한다. 노드 13의 왼쪽 노드는 null이고, 오른쪽 노드도 null이기 때문에 자신이 찾으려는 노드인지 확인한다. 찾으려는 노드가 아니기 때문에 노드 13은 부모 노드에게 null을 반환하다. 그럼 부모 노드 0에서 다시 오른쪽으로 이동한다. 노드 12는 왼쪽 노드가 있기 때문에 노드 15로 이동한다. 하지만 노드 15의 왼쪽 노드는 null이고, 오른쪽 노드도 null이기 때문에 자기 자신도 찾으려는 노드가 아니기 때문에 null을 반환한다. 그리고 부모 노드 12의 오른쪽 노드 14로 이동한다. 노드 14도 왼쪽, 오른쪽이 null이고, 자신도 찾는 노드가 아니기 때문에 null을 반환한다. 이제 부모 노드 12는 자식들로 부터 null을 반환 받고, 자기 자신을 비교하는데 노드 12는 찾는 노드 중에 하나이다. 그래서 이 때 부모 노드에게 12를 반환한다. 이제 부모 노드 0은 왼쪽은 null이고, 오른쪽에서 12를 반환 받았다. 양쪽 다 null이 아닐 경우 부모 노드가 공통 부모가 되는데 한 쪽이 null이기 떄문에 자기 자신을 비교한다. 노드 0도 찾는 노드가 아니기 때문에 12를 자기 부모 노드 1에 반환한다. 이제 노드 1의 오른쪽 노드 2로 이동한다. 노드 2의 왼쪽 노드가 null이기 때문에 노드 3으로 이동한다. 노드 3의 왼쪽 노드는 null이고, 오른쪽 노드 10으로 이동한다. 노드 10의 왼쪽 노드는 null이고, 오른쪽 노드도 null이다. 자기 자신을 찾는 노드와 비교한다. 노드 10은 찾는 노드이다. 부모 노드 3에 10을 반환한다. 노드 3은 양쪽 노드 중 하나는 null이고, 자신도 찾는 값이 아니기 때문에 부모 노드 2에 10을 반환한다. 노드 2도 양쪽중 한 쪽이 null이고, 자기 자신도 찾는 값이 아니기 떄문에 부모 노드 1에 10을 반환한다. 노드 1은 왼쪽에서 12를, 오른쪽에서 10을 반환 받았다. 양쪽에 모두 null 아니고 값이 들어왔기 때문에 노드 1은 공통 부모가 된다. 그래서 공통 부모인 자신을 반환한다. 그 다음 부모 노드는 반환 받은 값이 찾는 값들도 아니기 때문에 공통 부모 라는 것을 인식하고 공통 부모 노드를 반환한다.

</br>

``` java
package DataStructure;

import java.util.HashMap;

class Tree9 {
	static class Node {	// 노드 생성 
		int data;
		Node left;
		Node right;
		Node parent;	// 부모 노드 저장할 변수 
		
		Node(int data) {	// 생성자로 멤버변수에 data 대입 
			this.data = data;
		}
	}
	
	Node root;	// root를 저장 
	HashMap<Integer, Node> rootMap;	// 값으로 root를 찾기 쉽게 Map 선언
	
	Tree9(int size) {
		rootMap = new HashMap<>();	// Tree를 생성할 때 Map을 준비 
		root = makeBST(0, size - 1, null);	// 이진트리를 만드는 함수 호출 
	}
	
	Node makeBST(int start, int end, Node parent) {	// 이진 검새 트리 생성하는 함수 
		if(start > end) return null;
		int mid = (start + end) / 2;
		Node node = new Node(mid);
		node.left = makeBST(start, mid - 1, node);
		node.right = makeBST(mid + 1, end, node);
		node.parent = parent;
		rootMap.put(mid, node);	// 이진 트리를 만들 때, 값으로 노드를 찾아올 수 있게 Map에 노드를 추가 
		return node;
	}
	
	Node getNode(int data) {	// 값으로 노드를 가져오는 함수 
		return rootMap.get(data);
	}
	
	Node commonAncestor(int d1, int d2) {	// 공통 부모를 찾는 함수 
		Node p = getNode(d1);
		Node q = getNode(d2);
		int diff = depth(p) - depth(q);	// root부터 각 노드까지의 길이의 차이 계산 
		Node first = diff > 0 ? q : p;	// 길이가 짧은 걸 first에 대입 
		Node second = diff > 0 ? p : q;	// 길이가 긴 걸 second에 대입 
		second = goUpBy(second, Math.abs(diff));	// 긴 것을 차이만큼 올라가서 양쪽 노드의 길이를 맞춰주는 함수 
		while(first != second && first != null && second != null) {	// 한 칸씩 둘이 같이 올라가면서 둘이 만나는 지점을 찾음
			first = first.parent;
			second = second.parent;
		}
		return first == null || second == null ? null : first;	// 둘 중 하나가 먼저 root를 지나치면 그냥 나오고, 두개 다 null이 아닌 상태로 while문을 나오면 first 노드 반환 
	}
	
	Node goUpBy(Node node, int diff) {	// 노드와 숫자를 받아서 그 숫자만큼 노드가 위로 올라가는 함수 
		while(diff > 0 && node != null) {
			node = node.parent;
			diff--;
		}
		return node;
	}
	
	int depth(Node node) {	// 노드에 root까지의 길이 구하는 함수 
		int depth = 0;
		while(node != null) {
			node = node.parent;
			depth++;
		}
		return depth;
	}
	
	boolean covers(Node root, Node node) {	// 인자로 받은 노드가 root의 자손인지를 확인하는 함수 
		if(root == null) return false;	// root에 다다를 때까지 자손을 못 찾으면 false를 반
		if(root == node) return true; // 찾으면 true을 반환
		return covers(root.left, node) || covers(root.right, node);	// 해당 노드의 왼쪽, 오른쪽 자식 노드들을 검사 
	}
	
	Node commonAncestor2(int d1, int d2) {	// 공통 부모를 찾는 노드 
		Node p = getNode(d1);
		Node q = getNode(d2);
		if(!covers(root, p) || !covers(root, q)) {	// root에서 p, q의 존재 여부를 확인 
			return null;	// 이 값들이 시작 노드 밑에 없으면 null 반환 
		} else if(covers(p, q)) {	// p가 q의 부모 노드이면 p에서 두 노드가 처음 만남 
			return p;
		} else if(covers(q, p)) {	// q가 p의 부모 노드이면 q에서 두 노드가 처음 만남 
			return q;
		}
		Node sibling = getSibling(p);	// 그 외에는 형제 노드를 가져옴 
		Node parent = p.parent;	// 형제, 부모 노드 가져옴 
		while(!covers(sibling, q)) {	// 레벨을 한 칸씩 올라가면서 두 번째 노드가 형제의 하위 트리에 속해 있는지 확인 
			sibling = getSibling(parent);
			parent = parent.parent;
		}
		return parent;
	}
	
	Node getSibling(Node node) {	// 부모 노드를 받아와서 현재 노드가 부모의 어쪽 자식인지 확인하고, 반대쪽 자식 노드 반환해서 형제 노드를 가져옴  
		if(node == null || node.parent == null) {
			return null;
		}
		Node parent = node.parent;
		return parent.left == node ? parent.right : parent.left;
	}
	
	Node commonAncestor3(int d1, int d2) {	// 공통 부모를 찾는 노드 
		Node p = getNode(d1);
		Node q = getNode(d2);
		if(!covers(root, q) || !covers(root, q)) {	// p나 q가 트리 안에 존재하지 않으면 null 반
			return null;
		}
		return ancestorHelper(root, p, q); // 재귀 함수 호출 
	}
	
	Node ancestorHelper(Node root, Node p, Node q) {
		if(root == null || root == p || root == q) {	// 노드가 null이면 잎사귀 끝까지 왔으니 null을 반환 
			return root;	// 노드가 찾는 p나 q중에 하나까지 도달했으면 해당 노드를 반환 
		}
		boolean pIsOnLeft = covers(root.left, p);	// 노드 p가 왼쪽 트리에 있는지 확인 존재하지 않으면 오른쪽 트리에 존재 
		boolean qIsOnLeft = covers(root.left, q);	// 노드 q가 왼쪽 트리에 있는지 확인 존재하지 않으면 오른쪽 트리에 존재
		if(pIsOnLeft != qIsOnLeft) {	// 두 노드가 다른 방향이면 첫 번째 공통 분모 
			return root;
		}
		Node childSide = pIsOnLeft ? root.left : root.right;	// 두 노드가 같은 쪽으로 존재하면 같은 쪽으로 내려가 검색 
		return ancestorHelper(childSide, p, q);
	}
	
	Node commonAncestor4(int d1, int d2) {
		Node p = getNode(d1);
		Node q = getNode(d2);
		return commonAncestor4(root, p, q);	// 노드를 받는 함수에 전달 
	}
	
	Node commonAncestor4(Node root, Node p, Node q) {
		if(root == null) return null;	// 트리의 잎사귀 노드까지 오면 null을 반환하면서 재귀 호출을 돌려보냄 
		if(root == p && root == q) return root;	// p와 q root가 모두 같은 경우 해당 노드가 공통 부모가 된다. 
		Node x = commonAncestor4(root.left, p, q);	//  postorder에 입각해서 root의 왼쪽부터 검색 
		if(x != null && x != p && x != q) {	// 오른쪽을 검색하기 전에 어떤 값을 전달 받았는데 null도, p도 q도 아니면 공통 부모를 찾은 것이기 때문에 해당 노드를 반환 
			return x;
		}
		Node y = commonAncestor4(root.right, p, q);
		if(y != null & y != p && y != q) {	// 어떤 값을 전달 받았는데 null도, p도 q도 아니면 공통 부모를 찾은 것이기 때문에 해당 노드를 반환 
			return y;
		}
		if(x != null & y != null) {	// 양쪽에서 데이터를 받아왔는데 양쪽다 null이 아닌 경우, 찾는 값을 하나씩 찾아서 왔다는 것이다. 그래서 해당 노드가 공통 부모 노드가 된다.
			return root;
		} else if(root == p || root == q) {	// 해당 노드가 p나 q인 경우 찾은 노드를 반환 
			return root;
		} else {
			return x == null ? y : x;	// 두 개의 자식으로부터 받은 노드 중에 하나가 null이면 두 개중 null이 아닌 node를 반환 
		}
	}
}

public class CommonParentTest {
	public static void main(String[] args) {
		Tree9 t = new Tree9(10);
		Tree9.Node fa = t.commonAncestor4(6, 8);
		System.out.println("The first common ancestor is " + fa.data);
	}
}
```

```
The first common ancestor is 7
```

</br>

## Solution 5 - 정확한 결과 가져오기 

</br>

[![2023-05-05-9-09-31.png](https://i.postimg.cc/QCHGmBBh/2023-05-05-9-09-31.png)](https://postimg.cc/q6V5MvX5)

</br>

위의 방법의 단점은 만약에 주어진 두 개의 노드중 하나가 트리에 존재하지 않는 경우, 찾은 노드중에 하나를 반환한다. 노드에 무언가 표시가 없기 때문에 root에서 이 노드가 찾는 노드인지, 공통 부모인지 알 수가 없다. 그래서 공통 부모를 찾았다는 결과를 반환하면 좋다. 기존 코드에서는 노드나 null을 반환했는데 그 대신 어떤 임의의 저장 공간을 만들어서 여기에 찾았는지의 여부를 객체에 묶어서 해당 포인터를 반환하는 것이다.

</br>

``` java
package DataStructure;

import java.util.HashMap;

class Tree9 {
	static class Node {	// 노드 생성 
		int data;
		Node left;
		Node right;
		Node parent;	// 부모 노드 저장할 변수 
		
		Node(int data) {	// 생성자로 멤버변수에 data 대입 
			this.data = data;
		}
	}
	
	Node root;	// root를 저장 
	HashMap<Integer, Node> rootMap;	// 값으로 root를 찾기 쉽게 Map 선언
	
	Tree9(int size) {
		rootMap = new HashMap<>();	// Tree를 생성할 때 Map을 준비 
		root = makeBST(0, size - 1, null);	// 이진트리를 만드는 함수 호출 
	}
	
	Node makeBST(int start, int end, Node parent) {	// 이진 검새 트리 생성하는 함수 
		if(start > end) return null;
		int mid = (start + end) / 2;
		Node node = new Node(mid);
		node.left = makeBST(start, mid - 1, node);
		node.right = makeBST(mid + 1, end, node);
		node.parent = parent;
		rootMap.put(mid, node);	// 이진 트리를 만들 때, 값으로 노드를 찾아올 수 있게 Map에 노드를 추가 
		return node;
	}
	
	Node getNode(int data) {	// 값으로 노드를 가져오는 함수 
		return rootMap.get(data);
	}
	
	Node commonAncestor(int d1, int d2) {	// 공통 부모를 찾는 함수 
		Node p = getNode(d1);
		Node q = getNode(d2);
		int diff = depth(p) - depth(q);	// root부터 각 노드까지의 길이의 차이 계산 
		Node first = diff > 0 ? q : p;	// 길이가 짧은 걸 first에 대입 
		Node second = diff > 0 ? p : q;	// 길이가 긴 걸 second에 대입 
		second = goUpBy(second, Math.abs(diff));	// 긴 것을 차이만큼 올라가서 양쪽 노드의 길이를 맞춰주는 함수 
		while(first != second && first != null && second != null) {	// 한 칸씩 둘이 같이 올라가면서 둘이 만나는 지점을 찾음
			first = first.parent;
			second = second.parent;
		}
		return first == null || second == null ? null : first;	// 둘 중 하나가 먼저 root를 지나치면 그냥 나오고, 두개 다 null이 아닌 상태로 while문을 나오면 first 노드 반환 
	}
	
	Node goUpBy(Node node, int diff) {	// 노드와 숫자를 받아서 그 숫자만큼 노드가 위로 올라가는 함수 
		while(diff > 0 && node != null) {
			node = node.parent;
			diff--;
		}
		return node;
	}
	
	int depth(Node node) {	// 노드에 root까지의 길이 구하는 함수 
		int depth = 0;
		while(node != null) {
			node = node.parent;
			depth++;
		}
		return depth;
	}
	
	boolean covers(Node root, Node node) {	// 인자로 받은 노드가 root의 자손인지를 확인하는 함수 
		if(root == null) return false;	// root에 다다를 때까지 자손을 못 찾으면 false를 반
		if(root == node) return true; // 찾으면 true을 반환
		return covers(root.left, node) || covers(root.right, node);	// 해당 노드의 왼쪽, 오른쪽 자식 노드들을 검사 
	}
	
	Node commonAncestor2(int d1, int d2) {	// 공통 부모를 찾는 노드 
		Node p = getNode(d1);
		Node q = getNode(d2);
		if(!covers(root, p) || !covers(root, q)) {	// root에서 p, q의 존재 여부를 확인 
			return null;	// 이 값들이 시작 노드 밑에 없으면 null 반환 
		} else if(covers(p, q)) {	// p가 q의 부모 노드이면 p에서 두 노드가 처음 만남 
			return p;
		} else if(covers(q, p)) {	// q가 p의 부모 노드이면 q에서 두 노드가 처음 만남 
			return q;
		}
		Node sibling = getSibling(p);	// 그 외에는 형제 노드를 가져옴 
		Node parent = p.parent;	// 형제, 부모 노드 가져옴 
		while(!covers(sibling, q)) {	// 레벨을 한 칸씩 올라가면서 두 번째 노드가 형제의 하위 트리에 속해 있는지 확인 
			sibling = getSibling(parent);
			parent = parent.parent;
		}
		return parent;
	}
	
	Node getSibling(Node node) {	// 부모 노드를 받아와서 현재 노드가 부모의 어쪽 자식인지 확인하고, 반대쪽 자식 노드 반환해서 형제 노드를 가져옴  
		if(node == null || node.parent == null) {
			return null;
		}
		Node parent = node.parent;
		return parent.left == node ? parent.right : parent.left;
	}
	
	Node commonAncestor3(int d1, int d2) {	// 공통 부모를 찾는 노드 
		Node p = getNode(d1);
		Node q = getNode(d2);
		if(!covers(root, q) || !covers(root, q)) {	// p나 q가 트리 안에 존재하지 않으면 null 반
			return null;
		}
		return ancestorHelper(root, p, q); // 재귀 함수 호출 
	}
	
	Node ancestorHelper(Node root, Node p, Node q) {
		if(root == null || root == p || root == q) {	// 노드가 null이면 잎사귀 끝까지 왔으니 null을 반환 
			return root;	// 노드가 찾는 p나 q중에 하나까지 도달했으면 해당 노드를 반환 
		}
		boolean pIsOnLeft = covers(root.left, p);	// 노드 p가 왼쪽 트리에 있는지 확인 존재하지 않으면 오른쪽 트리에 존재 
		boolean qIsOnLeft = covers(root.left, q);	// 노드 q가 왼쪽 트리에 있는지 확인 존재하지 않으면 오른쪽 트리에 존재
		if(pIsOnLeft != qIsOnLeft) {	// 두 노드가 다른 방향이면 첫 번째 공통 분모 
			return root;
		}
		Node childSide = pIsOnLeft ? root.left : root.right;	// 두 노드가 같은 쪽으로 존재하면 같은 쪽으로 내려가 검색 
		return ancestorHelper(childSide, p, q);
	}
	
	class Result {	// 결과를 저장할 클래스 
		Node node;	// 노드를 저장할 주소 
		boolean isAncestor;	// 찾았는지 여부 저장 
		
		Result(Node n, boolean isAnc) {	// 생성자에서 값을 받아 넘겨줌 
			node = n;
			isAncestor = isAnc;
		}
	}
	
	Node commonAncestor4(int d1, int d2) {
		Node p = getNode(d1);
		Node q = getNode(d2);
		return commonAncestor4(root, p, q);	// 노드를 받는 함수에 전달 
	}
	
	Node commonAncestor4(Node root, Node p, Node q) {
		if(root == null) return null;	// 트리의 잎사귀 노드까지 오면 null을 반환하면서 재귀 호출을 돌려보냄 
		if(root == p && root == q) return root;	// p와 q root가 모두 같은 경우 해당 노드가 공통 부모가 된다. 
		Node x = commonAncestor4(root.left, p, q);	//  postorder에 입각해서 root의 왼쪽부터 검색 
		if(x != null && x != p && x != q) {	// 오른쪽을 검색하기 전에 어떤 값을 전달 받았는데 null도, p도 q도 아니면 공통 부모를 찾은 것이기 때문에 해당 노드를 반환 
			return x;
		}
		Node y = commonAncestor4(root.right, p, q);
		if(y != null & y != p && y != q) {	// 어떤 값을 전달 받았는데 null도, p도 q도 아니면 공통 부모를 찾은 것이기 때문에 해당 노드를 반환 
			return y;
		}
		if(x != null & y != null) {	// 양쪽에서 데이터를 받아왔는데 양쪽다 null이 아닌 경우, 찾는 값을 하나씩 찾아서 왔다는 것이다. 그래서 해당 노드가 공통 부모 노드가 된다.
			return root;
		} else if(root == p || root == q) {	// 해당 노드가 p나 q인 경우 찾은 노드를 반환 
			return root;
		} else {
			return x == null ? y : x;	// 두 개의 자식으로부터 받은 노드 중에 하나가 null이면 두 개중 null이 아닌 node를 반환 
		}
	}
	
	Node commonAncestor5(int d1, int d2) {
		Node p = getNode(d1);
		Node q = getNode(d2);
		Result r = commonAncestor5(root, p, q);
		if(r.isAncestor) {
			return r.node;
		}
		return null;
	}
	
	Result commonAncestor5(Node root, Node p, Node q) {
		if(root == null) return new Result(null, false);	// 트리의 잎사귀 노드까지 오면 null을 저장한 Result 객체를 반환하면서 재귀 호출을 돌려보냄 
		if(root == p && root == q) return new Result(root, true);	// p와 q root가 모두 같은 경우 해당 노드가 공통 부모가 된다. 
		Result rx = commonAncestor5(root.left, p, q);	//  postorder에 입각해서 root의 왼쪽부터 검색 
		if(rx.isAncestor) {	// isAncestor가 true이면 해당 객체 반환 
			return rx;
		}
		Result ry = commonAncestor5(root.right, p, q);
		if(ry.isAncestor) {	// isAncestor가 true이면 해당 객체 반환 
			return ry;
		}
		if(rx.node != null & ry.node != null) {	// 공통 부모를 찾은 순간 
			return new Result(root, true);	// true로 객체 반환 
		} else if(root == p || root == q) {	// 해당 노드가 p나 q인 경우 찾은 노드를 반환 
			boolean isAncestor = rx.node != null || ry.node != null;
			return new Result(root, isAncestor);
		} else {
			return new Result(rx.node != null ? rx.node : ry.node, false);
		}
	}
}

public class CommonParentTest {
	public static void main(String[] args) {
		Tree9 t = new Tree9(10);
		Tree9.Node fa = t.commonAncestor5(0, 8);
		System.out.println("The first common ancestor is " + fa.data);
	}
}
```

```
The first common ancestor is 4
```