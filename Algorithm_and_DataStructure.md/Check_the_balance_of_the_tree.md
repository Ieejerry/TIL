# Tree의 Balance 확인하기

</br>

[![2023-04-30-10-02-04.png](https://i.postimg.cc/WpJJXZD0/2023-04-30-10-02-04.png)](https://postimg.cc/fkDLbJfb)

</br>

## Balance 정의

</br>

[![2023-04-30-10-03-47.png](https://i.postimg.cc/s2XMSGdQ/2023-04-30-10-03-47.png)](https://postimg.cc/18kR1tzs)

</br>

현재 위의 트리는 밸런스가 잘 맞다. 길이가 다른 서브 트리들이 있지만 하나 이상 차이가 나지 않기 떄문이다.

</br>

[![2023-04-30-10-05-39.png](https://i.postimg.cc/MH8Zsv4Y/2023-04-30-10-05-39.png)](https://postimg.cc/JDPW04Ry)

</br>

9번 노드에 자식 노드를 하나 추가하면 8번 노드에서 봤을 떄 양쪽 자식 노드의 서브 트리를 비교했을 때, 하나는 0, 하나는 2가 되기 때문에 밸런스가 맞지 않게 된다. 

</br>

[![2023-04-30-10-08-14.png](https://i.postimg.cc/NfjvQ61H/2023-04-30-10-08-14.png)](https://postimg.cc/WtCHnJYN)

</br>

8번 노드의 왼쪽 자식 노드를 추가하겠다. 이제 밸런스가 맞아졌다. 양쪽 노드의 가장 긴 줄기만 비교해서 결정을 하자고 판단한 경우, 현재 위의 트리는 밸런스가 맞다. 4에서 볼 때, 왼쪽은 3번 노드가 가장 길고, 오른쪽은 10번 노드가 가장 긴데, 둘을 비교하면 길이차이가 하나밖에 나지 않기 때문이다. 그러면 양쪽 서브트리의 가장 긴 줄기만 비교한다고 가정하고 구현 방법을 생각해보겠다.

우선 노드들을 하나씩 돌면서 자식 노드들을 재귀 호출한다. 그리고 서브 트리의 길이를 측정하는 함수를 만들어서 결과값을 받아 온 뒤 양쪽 서브트리의 길이를 비교하다가 두 개의 서브트리가 하나 이상 차이가 나면 바로 false를 반환하면 된다.

</br>

### 전체 코드

</br>

``` java
package DataStructure;

import DataStructure.Tree3.Node;

class Tree4 {	// Tree 클래스 생성 
	class Node {	// Node 내부 클래스 생성 
		int data;
		Node left;
		Node right;
		
		Node(int data) {
			this.data = data;
		}
	}
	
	Node root;	// root를 저장할 노드 
	
	Tree4(int size) {	// Tree4 생성자를 통해 이진트리 생성 
		root = makeBST(0, size - 1);
		root.right.right.right.right = new Node(10);
	}
	
	Node makeBST(int start, int end) {	// 이진 트리를 구현하는 함수 
		if(start > end) return null;
		int mid = (start + end) / 2;
		Node node = new Node(mid);
		node.left = makeBST(start, mid - 1);
		node.right = makeBST(mid + 1, end);
		return node;
	}
	
	boolean isBalanced(Node root) {	// boolean 타입의 데이터를 반환하는 함수 선언 함수의 인자로는 노드의 주소를 받는다. 
		if(root == null) return true;	// 마지막 노드를 지났으면 더 이상 진행하지 않고, true를 반환 
		int heightDiff = getHeight(root.left) - getHeight(root.right);	// 양 쪽 서브트리의 길이를 받아서 그 차이를 저장 
		if(Math.abs(heightDiff) > 1) {	// 그 차이가 1이상 차이가 나면 
			return false;	// false를 반환 
		} else {	// 그렇지 않으면 
			return isBalanced(root.left) && isBalanced(root.right);	// 왼쪽과 오른쪽이 모두 밸런스가 맞는지 and 연산자로 둘 다 맞는 경우에만 true로 반환 
		}
	}
	
	int getHeight(Node root) {	// 노드를 던지면 해당 노드를 루트로 이하 서브 트리의 가장 긴 줄기의 레벨이 몇인지 알아오는 함수 
		if(root == null) return -1;	// 돌다가 트리의 마지막 노드를 지나면 -1를 반환해서 레벨 카운팅 번호에서 하나를 빼줌 
		return Math.max(getHeight(root.right), getHeight(root.right)) + 1;	// 그렇지 않으면 왼쪽 오른쪽 자식 노드들을 반복적으로 호출하면서 둘 중 더 긴 줄기를 선택하고 거기다가 1를 더해서 반환, 반환할 때마다 1를 더하면 함수가 벗겨질 때마다 레벨이 하나씩 증가하면서 세어나간다.  
	}
}

public class BalanceTest {
	public static void main(String[] args) {
		Tree4 t = new Tree4(10);	// 10개의 노드를 가지는 이진 트리 생성 
		System.out.println(t.isBalanced(t.root));	// isBalanced 함수 호출하여 출력 
	}
}
```

```
false
```

</br>

## 시간 복잡도 줄이기

</br>

그렇지만 위의 방법은 한 번 노드가 호출될 때마다 `getHeight()`함수가 해당 노드에서부터 양쪽으로 서브트리의 마지막까지 돌면서 길이를 재는데, 문제는 노드가 호출될 때마다 매번 다시 가서 길이를 재기 때문에 O(n log n)의 시간 복잡도를 갖는다. 비효율적이다.

</br>

[![2023-04-30-10-36-38.png](https://i.postimg.cc/R0ybxfvw/2023-04-30-10-36-38.png)](https://postimg.cc/hJ809XzG)

</br>

그래서 노드를 돌면서 동시에 길이를 재는 방법으로 구현을 해야한다. 위의 길이를 재는 함수와 마찬가지로 함수에서 돌아올 때 +1를 해서 반환하므로써 서브트리의 길이를 호출한 함수의 전달한다. 그런데 돌면서 비교를 하다가 중간에 언밸런스한 서브 트리를 발견하면 false를 반환해야 한다. 그런데 이미 정수형으로 서브트리의 길이를 반환하기로 했다. 그래서 정수중의 가장 작은 값을 false라고 규칙을 만들어서 가장 작은 경우 false로 반환한다. 이렇게되면 노드들을 한 번씩만 방문하면 되기 떄문에 O(n)의 시간 복잡도를 갖는다.

</br>

### 전체 코드

</br>

``` java
package DataStructure;

import DataStructure.Tree3.Node;

class Tree5 {	// Tree 클래스 생성 
	class Node {	// Node 내부 클래스 생성 
		int data;
		Node left;
		Node right;
		
		Node(int data) {
			this.data = data;
		}
	}
	
	Node root;	// root를 저장할 노드 
	
	Tree5(int size) {	// Tree4 생성자를 통해 이진트리 생성 
		root = makeBST(0, size - 1);
//		root.right.right.right.right = new Node(10);
	}
	
	Node makeBST(int start, int end) {	// 이진 트리를 구현하는 함수 
		if(start > end) return null;
		int mid = (start + end) / 2;
		Node node = new Node(mid);
		node.left = makeBST(start, mid - 1);
		node.right = makeBST(mid + 1, end);
		return node;
	}
	
	boolean isBalanced(Node root) {	// boolean 타입의 데이터를 반환하는 함수 선언 함수의 인자로는 노드의 주소를 받는다. 
		if(root == null) return true;	// 마지막 노드를 지났으면 더 이상 진행하지 않고, true를 반환 
		int heightDiff = getHeight(root.left) - getHeight(root.right);	// 양 쪽 서브트리의 길이를 받아서 그 차이를 저장 
		if(Math.abs(heightDiff) > 1) {	// 그 차이가 1이상 차이가 나면 
			return false;	// false를 반환 
		} else {	// 그렇지 않으면 
			return isBalanced(root.left) && isBalanced(root.right);	// 왼쪽과 오른쪽이 모두 밸런스가 맞는지 and 연산자로 둘 다 맞는 경우에만 true로 반환 
		}
	}
	
	int getHeight(Node root) {	// 노드를 던지면 해당 노드를 루트로 이하 서브 트리의 가장 긴 줄기의 레벨이 몇인지 알아오는 함수 
		if(root == null) return -1;	// 돌다가 트리의 마지막 노드를 지나면 -1를 반환해서 레벨 카운팅 번호에서 하나를 빼줌 
		return Math.max(getHeight(root.right), getHeight(root.right)) + 1;	// 그렇지 않으면 왼쪽 오른쪽 자식 노드들을 반복적으로 호출하면서 둘 중 더 긴 줄기를 선택하고 거기다가 1를 더해서 반환, 반환할 때마다 1를 더하면 함수가 벗겨질 때마다 레벨이 하나씩 증가하면서 세어나간다.  
	}
	
	int checkHeight(Node root) {	// 길이를 재는 함수 선언 
		if(root == null) return -1;	// 재귀 호출이 끝나는 시점은 마지막 노드를 지나면 레벨에서 하나 뺀다. 
		int leftHeight = checkHeight(root.left);	// 왼쪽 노드를 돌면서 서브트리의 길이를 잰다. 
		if(leftHeight == Integer.MIN_VALUE) return Integer.MIN_VALUE;	// 	받은 결과값이 정수값중 가장 작으면 false를 반환 
		int rightHeight = checkHeight(root.right);	// 오른쪽 노드를 돌면서 서브트리의 길이를 잰다. 
		if(rightHeight == Integer.MIN_VALUE) return Integer.MIN_VALUE;	// 	받은 결과값이 정수값중 가장 작으면 false를 반환 
		int heightDiff = leftHeight - rightHeight;	// false가 아닌 경우에는 해당 결과값이 서브트리의 길이가 되기 때문에 양쪽 서브트리의 가장 긴 줄기끼리 비교하여 
		if(Math.abs(heightDiff) > 1) {	// 그 차이가 1이 넘으면
			return Integer.MIN_VALUE;	// false를 반
		} else {	// 아니면 두 개의 길이중 큰 값에 1를 더해서 반환 
			return Math.max(leftHeight, rightHeight) + 1;	// 여기서 1를 더해서 반환하면 재귀 호출을 맨 끝에서 한 커풀 벗겨질 때마다 1씩 증가해서 길이로 사용 가능 
		}
	}
	
	boolean isBalanced2(Node root) {	// 재귀 함수를 호출해줄 함수 선언 
		return checkHeight(root) != Integer.MIN_VALUE;	// checkHeight 결과값이 정수의 가장 작은 값이 아니면 	true를 반환 
	}
}

public class BalanceTest2 {
	public static void main(String[] args) {
		Tree5 t = new Tree5(10);	// 10개의 노드를 가지는 이진 트리 생성 
		System.out.println(t.isBalanced2(t.root));	// isBalanced 함수 호출하여 출력 
	}
}
```

```
true
```

</br>

## 가장 짧은 줄기와 긴 줄기의 Balance 비교

</br>

[![2023-04-30-10-08-14.png](https://i.postimg.cc/NfjvQ61H/2023-04-30-10-08-14.png)](https://postimg.cc/WtCHnJYN)

</br>

Balance가 맞다는 의미를 다른 관점에서 해석해보겠다. 우선 1번 노드에서 볼 때 양쪽 Balance가 1밖에 차이가 나지 않기 때문에 밸런스가 맞다. 하지만 4번 노드 기준에서 양쪽의 긴 줄기끼리만 비교하였을 때는 밸런스가 맞지만, 왼쪽 서브 트리의 가장 짧은 줄기와 오른쪽 서브 트리의 가장 긴 줄기가 2개 차이 나기 때문에 밸런스가 맞다는 것에 조금 더 엄격한 규칙을 줘서 가장 긴 줄기로만 비교하는 것이 아니라 그 어떤 서브 트리도 길이 차이가 1이상 나면 안되게 재정의를 하겠다. 그러면 노드가 길이를 반환할 때, 가장 작은 값과 가장 큰 값을 반환해야 한다. 그런데 자바는 두 개의 데이터를 반환할 수 없기 때문에 객체를 이용해서 처음에 함수를 호출할 떄 객체의 주소를 전달해서 호출한 함수의 결과를 반환하지 않고, 객체에 저장을 한다. 이번에는 나오면서 길이를 세는 것이 아니라, 들어갈 때 길이를 세서 각 서브트리의 마지막 노드에 도착했을 때, 객체의 값을 업데이트하도록 하겠다.

</br>

### 전체 코드

</br>

``` java
package DataStructure;

import DataStructure.Tree3.Node;

class Tree6 {	// Tree 클래스 생성 
	class Node {	// Node 내부 클래스 생성 
		int data;
		Node left;
		Node right;
		
		Node(int data) {
			this.data = data;
		}
	}
	
	Node root;	// root를 저장할 노드 
	
	Tree6(int size) {	// Tree4 생성자를 통해 이진트리 생성 
		root = makeBST(0, size - 1);
		root.right.right.right.right = new Node(10);	// 10번 노드 추가 
		root.right.right.left = new Node(11);	// 11번 노드 추가 
	}
	
	Node makeBST(int start, int end) {	// 이진 트리를 구현하는 함수 
		if(start > end) return null;
		int mid = (start + end) / 2;
		Node node = new Node(mid);
		node.left = makeBST(start, mid - 1);
		node.right = makeBST(mid + 1, end);
		return node;
	}
	
	boolean isBalanced(Node root) {	// boolean 타입의 데이터를 반환하는 함수 선언 함수의 인자로는 노드의 주소를 받는다. 
		if(root == null) return true;	// 마지막 노드를 지났으면 더 이상 진행하지 않고, true를 반환 
		int heightDiff = getHeight(root.left) - getHeight(root.right);	// 양 쪽 서브트리의 길이를 받아서 그 차이를 저장 
		if(Math.abs(heightDiff) > 1) {	// 그 차이가 1이상 차이가 나면 
			return false;	// false를 반환 
		} else {	// 그렇지 않으면 
			return isBalanced(root.left) && isBalanced(root.right);	// 왼쪽과 오른쪽이 모두 밸런스가 맞는지 and 연산자로 둘 다 맞는 경우에만 true로 반환 
		}
	}
	
	int getHeight(Node root) {	// 노드를 던지면 해당 노드를 루트로 이하 서브 트리의 가장 긴 줄기의 레벨이 몇인지 알아오는 함수 
		if(root == null) return -1;	// 돌다가 트리의 마지막 노드를 지나면 -1를 반환해서 레벨 카운팅 번호에서 하나를 빼줌 
		return Math.max(getHeight(root.right), getHeight(root.right)) + 1;	// 그렇지 않으면 왼쪽 오른쪽 자식 노드들을 반복적으로 호출하면서 둘 중 더 긴 줄기를 선택하고 거기다가 1를 더해서 반환, 반환할 때마다 1를 더하면 함수가 벗겨질 때마다 레벨이 하나씩 증가하면서 세어나간다.  
	}
	
	int checkHeight(Node root) {	// 길이를 재는 함수 선언 
		if(root == null) return -1;	// 재귀 호출이 끝나는 시점은 마지막 노드를 지나면 레벨에서 하나 뺀다. 
		int leftHeight = checkHeight(root.left);	// 왼쪽 노드를 돌면서 서브트리의 길이를 잰다. 
		if(leftHeight == Integer.MIN_VALUE) return Integer.MIN_VALUE;	// 	받은 결과값이 정수값중 가장 작으면 false를 반환 
		int rightHeight = checkHeight(root.right);	// 오른쪽 노드를 돌면서 서브트리의 길이를 잰다. 
		if(rightHeight == Integer.MIN_VALUE) return Integer.MIN_VALUE;	// 	받은 결과값이 정수값중 가장 작으면 false를 반환 
		int heightDiff = leftHeight - rightHeight;	// false가 아닌 경우에는 해당 결과값이 서브트리의 길이가 되기 때문에 양쪽 서브트리의 가장 긴 줄기끼리 비교하여 
		if(Math.abs(heightDiff) > 1) {	// 그 차이가 1이 넘으면
			return Integer.MIN_VALUE;	// false를 반
		} else {	// 아니면 두 개의 길이중 큰 값에 1를 더해서 반환 
			return Math.max(leftHeight, rightHeight) + 1;	// 여기서 1를 더해서 반환하면 재귀 호출을 맨 끝에서 한 커풀 벗겨질 때마다 1씩 증가해서 길이로 사용 가능 
		}
	}
	
	boolean isBalanced2(Node root) {	// 재귀 함수를 호출해줄 함수 선언 
		return checkHeight(root) != Integer.MIN_VALUE;	// checkHeight 결과값이 정수의 가장 작은 값이 아니면 	true를 반환 
	}
	
	class Level {	// 레벨 정보를 저장할 클래스 선언 
		int min = Integer.MAX_VALUE;	// min은 정수중 가장 큰 값으로 초기화하여 어떤 값과 비교해도 새로운 값으로 업데이트 되도록 함  
		int max = Integer.MIN_VALUE;	// max는 정수중 가장 작은 값으로 초기화하여 어떤 값과 비교해도 새로운 값으로 업데이트 되도록 함 
	}
	
	boolean isBalanced3(Node root) {	// 재귀 함수를 호출해줄 함수 선언 
		Level obj = new Level();	// Level 객체 생성 
		checkBalanced(root, obj, 0);	// 시작 노드와 저장할 객체 그리고 레벨은 0부터 시작해서 재귀 함수 호출 
		if(Math.abs(obj.min - obj.max) > 1) return false;	// 재귀 함수가 종료되면 객체의 가장 작은 서브트리의 길이와 가장 큰 서브트리의 길이의 차이가 1이상이면 언밸런스하다고 판
		else return true;
	}
	
	void checkBalanced(Node node, Level obj, int level) {	// 재귀적으로 호출하면서 객체의 값을 업데이트해줄 함수 선언 
		if(node == null) {	// 노드가 null이면 맨 마지막 노드를 지났기 때문에 
			if(level < obj.min) obj.min = level;
			else if(level > obj.max) obj.max = level;	// 모든 서브트리의 맨 끝에서 객체의 정보를 업데이트 
			// 들어가면서 레벨을 하나씩 증가하면 길이는 맨 마지막 노드에서 나오기 때문에 중간에 비교할 필요가 없다. 그래서 항상 노드가 null일 때, 서브트리의 길이를 비교하고, 객체의 값을 업데이트 
			return;	// 노드의 마지막이기 때문에 재귀 호출하지 않고 종료 
		}
		checkBalanced(node.left, obj, level + 1);
		checkBalanced(node.right, obj, level + 1);	// 레벨만 하나씩 증가시키면서 양쪽 노드들을 재귀 호출 
	}
}

public class BalanceTest3 {
	public static void main(String[] args) {
		Tree6 t = new Tree6(10);	// 10개의 노드를 가지는 이진 트리 생성 
		System.out.println(t.isBalanced(t.root));	// isBalanced 함수 호출하여 출력 
		System.out.println(t.isBalanced2(t.root));	// isBalanced2 함수 호출하여 출력 
		System.out.println(t.isBalanced3(t.root));	// isBalanced3 함수 호출하여 출력 
	}
}
```

```
true
true
false
```