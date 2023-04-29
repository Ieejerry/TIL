# 이진트리를 레벨단위 리스트로 변형하기

</br>

[![2023-04-29-4-22-33.png](https://i.postimg.cc/Nf6YWr51/2023-04-29-4-22-33.png)](https://postimg.cc/9rQv90PM)

</br>

[![2023-04-29-4-23-28.png](https://i.postimg.cc/59v62yXt/2023-04-29-4-23-28.png)](https://postimg.cc/4nfJ8JbC)

</br>

위와 같이 트리가 있을 때, 각 레벨별로 LinkedList를 생성해야 한다. 이 문제를 풀기 위해서는 두 가지 방법으로 접근이 가능하다. 

</br>

## 첫 번째 방법

</br>

[![2023-04-29-4-27-57.png](https://i.postimg.cc/vZvPFGrq/2023-04-29-4-27-57.png)](https://postimg.cc/LJnkjK0L)

</br>

함수가 호출 될 때마다 현재 노드의 레벨이 몇 번째 레벨인지를 함수의 인자로 받는다. 예를 들어 첫 번째 노드를 호출할 때는 레벨을 0으로 초기화 시켜서 함수를 호출하고, 해당 노드에서 왼쪽 오른쪽 노드를 다시 호출할 때는 자기가 받은 레벨 변호에 1를 더해서 다시 호출하는 것이다. 그러면 각 노드들은 호출 받았을 때 자기가 몇 번째 LinkedList에 들어가야하는지를 함수의 인자로 받아서 알고 있기 때문에 그냥 그 리스트에 해당 노드를 추가하면 된다.

</br>

## 첫 번째 방법

</br>

[![2023-04-29-4-35-31.png](https://i.postimg.cc/nzsbhXTc/2023-04-29-4-35-31.png)](https://postimg.cc/ygzrfYww)

</br>

BFS를 변형한 형태인데, 시작할 때 root를 LinkedList에 담고 시작한다. 그리고 새로운 LinkedList 하나를 추가해서 바로 위에 있는 LinkedList의 노드들을 돌면서 자식 노드들을 추가한다. 바로 위에 있는 리스트에는 root 노드 하나이기 때문에 root의 자식 노드 1과 7를 밑에 LinkedList에 추가한다. 다 담았으면 새로운 리스트를 새롭게 생성하고, 그리고 바로 위에 있는 리스트에 있는 노드들을 돌면서 자식 노드들을 추가한다. 노드 1의 자식 노드 0하고 2 두 개를 넣고, 노드 7의 자식 노드 5하고 8를 넣는다. 이렇게 노드들 다 넣고, 새로운 리스트를 생성한다. 그리고 또 그 위에 노드들의 자식 노드들을 새로운 리스트에 추가한다. 노드 0은 자식 노드가 없기 때문에 넘어가고, 노드 2의 자식 노드 3을 넣어주고, 노드 5의 자식 노드 6을 넣어주고, 8의 자식 노드 9를 넣어준다. 이렇게 바로 위의 레벨의 노드들을 돌면서 밑에 LinkedList에 추가하면 레벨별로 LinkedList에 노드들이 담긴다.

</br>

[![2023-04-29-4-39-46.png](https://i.postimg.cc/VLJrPgX3/2023-04-29-4-39-46.png)](https://postimg.cc/PPkrmm34)

</br>

두 가지 방법 모두 다 노드 갯수만큼 재귀호출을 하고 노드 갯수만큼 루프를 놀기 때문에 O(n)의 시간 복잡도를 갖고, 두 가지 방법 모두 레벨 갯수만큼 배열방과 각방의 레벨 단위로 모든 노드를 다 담아서 결과로 반환해야 하기 때문에 O(n)의 공간 복잡도를 갖는다. 첫 번째 방법은 재귀적으로 호출할 때 내부적으로 스택이 사용되어서 반환한 함수를 계속 기억하고 있다. 그래서 첫 번째 방법은 재귀호출을 구현하는데 필요한 O(log n)의 공간이 추가적으로 필요하다.

</br>

## 전체 코드

</br>

``` java
package DataStructure;

import java.util.LinkedList;
import java.util.ArrayList;

class Tree3 {	// Tree 클래스 생성 
	class Node {	// 이진 트리 노드 생성 
		int data;
		Node left;
		Node right;
		
		Node(int data) {
			this.data = data;
		}
	}
	
	Node root;	// 루트를 저장 
	
	Tree3(int size) {	// 생성과 동시에 이진트리를 생성 
		root = makeBST(0, size - 1);
	}
	
	Node makeBST(int start, int end) {	// 이진 트리를 구현하는 함수 
		if(start > end) return null;
		int mid = (start + end) / 2;
		Node node = new Node(mid);
		node.left = makeBST(start, mid - 1);
		node.right = makeBST(mid + 1, end);
		return node;
	}
	
	ArrayList<LinkedList<Node>> BSTtoList() {	// 재귀 호출을 할 때, 레벨을 함수의 인자로 받아 LinkedList에 추가하는 함수  
		ArrayList<LinkedList<Node>> lists = new ArrayList<>();	// 재귀함수를 호출하기 전에 함수를 호출할 초기값들을 던져줄 함수를 구현, 결과값으로 넘겨줄 배열방을 만들어서 그 안에 LinkedList들을 담아서 반환
		BSTtoList(root, lists, 0); // 재귀 함수에 시작할 때 만들었던 이진 트리의 시작 노드와 결과를 담을 배열방 주소, 그리고 현재 레벨 0이라고 알려주는 함수를 호출 
		return lists;	// 재귀호출을 통해 획득한 결과를 반환 
	}
	
	void BSTtoList(Node root, ArrayList<LinkedList<Node>> lists, int level) {	// 재귀 함수 정의 
		if(root == null) return;	// 호출 받은 노드가 null이면 그냥 나가기 , 재귀 호출에서는 어디서 멈출지를 명시하는 것은 매우 중요하다. 
		LinkedList<Node> list = null;	// 해당 노드를 담을 리스트 선언 
		if(lists.size() == level) {	// 새로운 레벨에 노드를 처음 호출할 때 해당 레벨의 리스트가 배열방에 존재하지 않기 때문에 
			list = new LinkedList<Node>();	// 새로운 리스트를 하나 만들어서 배열에 추가 
			lists.add(list);
		} else {	// 배열에 해당 레벨의 리스트가 존재하면 
			list = lists.get(level);	// 그곳에 노드를 추가해야 되기 떄문에 레벨 번호로 기존에 있는 리스트의 시작 주소를 획득해 온다. 
		}
		list.add(root);	// 해당 리스트에 노드를 추가 
		BSTtoList(root.left, lists, level + 1);
		BSTtoList(root.right, lists, level + 1);	// 자식 노드들로 level + 1하여 재귀 호출 
	}
	
	ArrayList<LinkedList<Node>> BSTtoList2() {
		ArrayList<LinkedList<Node>> result = new ArrayList<LinkedList<Node>>();	// 결과값을 담을 배열을 선언 
		LinkedList<Node> current = new LinkedList<>();	// 현재 레벨의 노드를 담을 LinkedList 선언 
		if(root != null) {	// 초기값으로 루트 노드를 먼저 담음 
			current.add(root);
		}
		
		while(current.size() > 0) {	// current 리스트에 현재 레벨의 노드들을 담기 위해 현재 레벨에 노드가 있는 동안에는 계속 반복 
			result.add(current);	// while문 이전에 실행한 결과를 올라와서 배열방에 담고 또 새로운 레벨을 시작하는데 처음 시작할 때는 루트 노드를 current에 담았기 때문에 첫 번째 레벨에는 루트만 하나 담기게 된다. 
			LinkedList<Node> parent = current;	// 현재 레벨을 부모 레벨로 변경 
			current = new LinkedList<Node>();	// 현재 레벨은 새로 시작 
			for(Node parents : parent) {
				if(parents.left != null) current.add(parents.left);
				if(parents.right != null) current.add(parents.right);	// 왼쪽이나 오른쪽에 자식이 있으면 현재 레벨에 모두 추가 
			}
		}
		return result;	// 더 이상 현재 레벨에 담을 자식 노드가 하나도 남아있지 않으면 결과 리스트를 담은 배열을 반환 
	}
	
	void printList(ArrayList<LinkedList<Node>> arr) {	// 결과를 출력하는 함수 
		for(LinkedList<Node> list : arr) {	// 	배열을 돌면서 리스트를 가져오기 
			for(Node node : list) {	// 리스트 안에서 노드를 가져오기 
				System.out.print(node.data + " ");	// 노드의 데이터 출력 
			}
			System.out.println();	// 리스트가 하나 끝날 때마다 새로운 라인에 출력 
		}
	}
}

public class BinaryTreeTest {
	public static void main(String[] args) {
		Tree3 t = new Tree3(10);
		t.printList(t.BSTtoList());
	}
}
```