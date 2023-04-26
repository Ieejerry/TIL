# Graph 검색 DFS, BFS 구현 in Java

</br>

## 그래프 검색 방법

그래프 검색 방법에는 대표적으로 두 가지 방법이 있다.

1. Depth First Search(DFS) 깊이 우선 검색
2. Breadth First Search(BFS) 넓이 우선 검색

</br>

### Depth First Search(DFS)

Binary tree 순회 방법인 inorder, preorder, postorder들은 깊이 우선 검색에 속한다.

</br>

[![2023-04-25-7-46-42.png](https://i.postimg.cc/sXz106g4/2023-04-25-7-46-42.png)](https://postimg.cc/DWC2ScsS)

</br>

깊이 우선 검색은 하나의 자식 노드를 방문했으면, 해당 자식 노드의 자식 노드 그 자식 노드의 자식 노드 끝까지 파고들어 검색하는 것이다. 그리고 나와서 다음 줄기를 파고 들고, 나와서 그 다음 줄기를 파고 들고, 반복하며 줄기의 마지막 노드를 만날 때가지 파고 들고, 형제 노드들을 방문한다.

</br>

### Breadth First Search(BFS)

</br>

[![2023-04-25-7-49-30.png](https://i.postimg.cc/593pgD2p/2023-04-25-7-49-30.png)](https://postimg.cc/QVFpx45W)

</br>

넓이 우선 검색은 시작점에서 자신의 자식 노드들을 먼저 다 방문하고, 그 다음에 자식 노드의 노드를 방문하는 식으로 레벨 단위로 검색을 하는 것이다.

</br>

### DFS와 BFS 이동경로 비교

</br>

[![2023-04-25-7-50-52.png](https://i.postimg.cc/8PfJcr9W/2023-04-25-7-50-52.png)](https://postimg.cc/HVHsPjps)

</br>

## DFS, BFS 구현

DFS는 Stack으로 구현   
BFS는 Queue로 구현

</br>

### DFS : Stack 구현

</br>

[![2023-04-25-9-25-55.png](https://i.postimg.cc/d3qRj3Qz/2023-04-25-9-25-55.png)](https://postimg.cc/8J0r116H)

</br>

DFS를 진행하는 순서는 Stack을 하나 만들고 시작할 노드를 넣고 그 다음부터 시작을 한다. 스택에서 노드를 하나 꺼내서 해당 자식 노드를 전부 스택에 넣고 꺼낸 노드는 출력한다.

자식 노드를 스택에 넣을 때는 한 번 스택에 담았던 노드는 다시 넣지 않는다.

0부터 시작해서 왼쪽의 그래프를 순회한다.

</br>

[![2023-04-25-9-27-28.png](https://i.postimg.cc/cJhL8LjK/2023-04-25-9-27-28.png)](https://postimg.cc/944h6CcV)

</br>

0번 노드를 스택에 넣었다.

</br>

[![2023-04-25-9-29-07.png](https://i.postimg.cc/pLn0T9mZ/2023-04-25-9-29-07.png)](https://postimg.cc/68tVbpL2)

</br>

스택에 있던 노드 0을 꺼내고, 그 노드의 자식 노드 1를 스택에 넣는다. 그리고 꺼낸 노드 0은 출력한다.

</br>

[![2023-04-25-9-30-07.png](https://i.postimg.cc/4dFtV5Mh/2023-04-25-9-30-07.png)](https://postimg.cc/mzCtGQTb)

</br>

스택에 있던 노드 1을 꺼내고, 그 노드의 자식 노드 2, 3을 스택에 넣는다. 그리고 꺼낸 노드 1은 출력한다.

</br>

[![2023-04-25-9-31-56.png](https://i.postimg.cc/GmrKjbzP/2023-04-25-9-31-56.png)](https://postimg.cc/LnCj9Kch)

</br>

스택에 있던 노드 중 위에 있는 3을 꺼내고, 그 노드의 자식 노드 2는 이미 스택에 있기 때문제 제외하고, 노드 4, 5를 스택에 넣는다. 그리고 꺼낸 노드 3은 출력한다.

</br>

[![2023-04-25-9-33-53.png](https://i.postimg.cc/j5sr0Vsy/2023-04-25-9-33-53.png)](https://postimg.cc/cK5zwbtJ)

</br>

스택에 있던 노드 중 위에 있는 5을 꺼내고, 그 노드의 자식 노드 6, 7를 스택에 넣는다. 그리고 꺼낸 노드 5는 출력한다.

</br>

[![2023-04-25-9-36-23.png](https://i.postimg.cc/hvLySvpj/2023-04-25-9-36-23.png)](https://postimg.cc/N207Dshq)

</br>

스택에 있던 노드 중 위에 있는 7를 꺼내고, 노드 7은 자식 노드가 없기 때문에 그대로 출력한다.

</br>

[![2023-04-25-9-38-34.png](https://i.postimg.cc/9M8XLXGD/2023-04-25-9-38-34.png)](https://postimg.cc/BLFG6073)

</br>

스택에 있던 노드 중 위에 있는 6을 꺼내고, 그 노드의 자식 노드 8을 스택에 넣는다. 그리고 꺼낸 노드 6는 출력한다.

</br>

[![2023-04-25-10-04-47.png](https://i.postimg.cc/Vkpy6rzs/2023-04-25-10-04-47.png)](https://postimg.cc/ZW8ssq9X)

</br>

스택에 있던 노드 중 위에 있는 8를 꺼내고, 노드 8은 자식 노드가 없기 때문에 그대로 출력한다.

</br>

[![2023-04-25-10-05-58.png](https://i.postimg.cc/tRwFB9RZ/2023-04-25-10-05-58.png)](https://postimg.cc/rzGdmXrM)

</br>

스택에 있던 노드 중 위에 있는 4를 꺼내고, 노드 4의 자식 노드들은 이미 스택에 넣었었기 때문에 그대로 출력한다.

</br>

[![2023-04-25-10-08-20.png](https://i.postimg.cc/RZVKgdJh/2023-04-25-10-08-20.png)](https://postimg.cc/jLmD5zXY)

</br>

스택에 남아 있는 노드 2를 꺼내고, 노드 2의 자식 노드들은 이미 스택에 넣었었기 때문에 그대로 출력한다.

스택이 다 비었으면 순회가 완료된 것이다.

</br>

### BFS : Queue 구현

</br>

[![2023-04-25-10-10-19.png](https://i.postimg.cc/NM0nYmnj/2023-04-25-10-10-19.png)](https://postimg.cc/t1LkNZyK)

</br>

BFS 구현 방법은 우선 Queue를 하나 만들고 시작 노드를 넣어준다. DFS와 마찬가지로 Queue에 들어있는 노드를 하나 꺼내고, 그 노드의 자식 노드들을 전부 Queue에 넣고 꺼낸 노드는 출력한다. 자식 노드를 Queue에 넣을 때 한 번 Queue에 넣었던 노드는 다시 넣지 않는다.

Queue는 위에서 넣고, 밑에서 꺼낸다.

</br>

[![2023-04-25-10-13-55.png](https://i.postimg.cc/JzprQcj1/2023-04-25-10-13-55.png)](https://postimg.cc/YvmBrFXV)

</br>

Queue에 들어있는 노드 0을 꺼내고, 그 노드의 자식 노드 1을 Queue에 넣고 꺼낸 노드 0을 출력한다.

</br>

[![2023-04-25-10-15-33.png](https://i.postimg.cc/P5JsdG8j/2023-04-25-10-15-33.png)](https://postimg.cc/svk0JNc6)

</br>

Queue에 들어있는 노드 1을 꺼내고, 그 노드의 자식 노드 2, 3을 Queue에 넣고 꺼낸 노드 1을 출력한다.

</br>

[![2023-04-25-10-16-42.png](https://i.postimg.cc/TwqHrQW0/2023-04-25-10-16-42.png)](https://postimg.cc/7GhV439J)

</br>

Queue에 들어있는 노드 중 가장 아래에 있는 2를 꺼내고, 그 노드의 자식 노드들 중 Queue에 들어가지 않았던 노드 4를 Queue에 넣고 꺼낸 노드 2를 출력한다.

</br>

[![2023-04-25-10-18-44.png](https://i.postimg.cc/Nfyktpfn/2023-04-25-10-18-44.png)](https://postimg.cc/PPjwzbDb)

</br>

Queue에 들어있는 노드 중 가장 아래에 있는 3을 꺼내고, 그 노드의 자식 노드들 중 Queue에 들어가지 않았던 노드 5를 Queue에 넣고 꺼낸 노드 3을 출력한다.

</br>

[![2023-04-25-10-20-20.png](https://i.postimg.cc/NGZp5WVt/2023-04-25-10-20-20.png)](https://postimg.cc/qgX8FZ4D)

</br>

Queue에 들어있는 노드 중 가장 아래에 있는 4를 꺼내고, 그 노드의 자식 노드들은 이미 한 번 Queue에 넣었었기 때문에 그대로 노드 4를 출력한다.

</br>

[![2023-04-25-10-21-52.png](https://i.postimg.cc/pXx5GC58/2023-04-25-10-21-52.png)](https://postimg.cc/s1621pcD)

</br>

Queue에 남아있는 노드 5를 꺼내고, 그 노드의 자식 노드들 중 Queue에 들어가지 않았던 노드 6, 7를 Queue에 넣고 꺼낸 노드 5를 출력한다.


</br>

[![2023-04-25-10-23-35.png](https://i.postimg.cc/pTq4wqXT/2023-04-25-10-23-35.png)](https://postimg.cc/1nVv60Fh)

</br>

Queue에 들어있는 노드 중 가장 아래에 있는 6을 꺼내고, 그 노드의 자식 노드들 중 Queue에 들어가지 않았던 노드 8을 Queue에 넣고 꺼낸 노드 6을 출력한다.

</br>

[![2023-04-25-10-25-10.png](https://i.postimg.cc/kG21kCp1/2023-04-25-10-25-10.png)](https://postimg.cc/T5XJDzGg)

</br>

Queue에 들어있는 노드 중 가장 아래에 있는 7을 꺼내고, 그 노드는 자식 노드가 없기 때문에 그대로 출력한다.

</br>

[![2023-04-25-10-26-47.png](https://i.postimg.cc/KYSpKCsw/2023-04-25-10-26-47.png)](https://postimg.cc/9DbYKg2Y)

</br>

Queue에 남아있는 노드 8을 꺼내고, 그 노드는 자식 노드가 없기 때문에 그대로 출력한다.

Queue가 비었으면 순회가 완료된 것이다.

</br>

[![2023-04-25-10-26-47.png](https://i.postimg.cc/KYSpKCsw/2023-04-25-10-26-47.png)](https://postimg.cc/9DbYKg2Y)

</br>

DFS, BFS 두 가지 방법을 통해 순회를 하면서 출력한 결과이다. 그래프는 트리가 아니기 때문에 반드시 0부터 시작할 필요는 없다.

</br>

[![2023-04-25-10-30-34.png](https://i.postimg.cc/26V1sj4B/2023-04-25-10-30-34.png)](https://postimg.cc/DJ3fsTp2)

</br>

위의 처럼 3으로 시작해도 결과는 다르지만 규칙에 맞게 모든 노드들이 순회가 잘 된다.

**참고로 DFS를 구현할 때 재귀호출을 사용하면 훨씬 더 간결하고 세련되게 구현할 수 있다.**

</br>

### DFS : Recursion(재귀 함수)

재귀 함수를 이용한 순회 방법은 우선 노드에 방문하면 데이터를 출력하고 자식 노드들을 순서대로 재귀 호출하는 것이다. 자식 노드가 호출을 받으면 마찬가지로 자신의 데이터를 출력하고 자기 자식 노드들을 재귀 호출한다. 그렇게 호출을 받으면 반환하기 전에 자식 노드를 먼저 호출하기 때문에 재귀 호출로 깊이 우선 탐색이 가능해진다.

</br>

[![2023-04-25-10-40-30.png](https://i.postimg.cc/43rKTkwL/2023-04-25-10-40-30.png)](https://postimg.cc/PLQfm7gY)

</br>

시작 노드 0으로 함수를 호출한다. 함수가 호출되면 자식 노드를 호출하기 전에 먼저 자기 자신의 데이터를 출력한다. 만약 재귀호출을 다녀와서 호출을 하게 된다면 자식 노드들의 데이터가 먼저 출력되는 거꾸로된 출력이 된다.

그래서 호출이 되면 우선 출력을 한다.

</br>

[![2023-04-25-10-46-00.png](https://i.postimg.cc/mkqZ77qd/2023-04-25-10-46-00.png)](https://postimg.cc/K3Py23mL)

</br>

자식 노드 1을 호출하고, 노드 1을 출력한다.

</br>

[![2023-04-25-10-47-38.png](https://i.postimg.cc/k5X43Mxv/2023-04-25-10-47-38.png)](https://postimg.cc/75dDSkt5)

</br>

노드 1에는 자식 노드가 2, 3 두 개가 있다. 그 중 첫 번째 자식 2를 호출하고, 노드 2를 출력한다.

여기서 스택과 다른 점은 자식 노드가 하나 이상인 경우에 스택은 쌓고 나서 호출을 하기 때문에 자식 중에 맨 마지막으로 들어간 자식 노드가 먼저 출력이 되는데 재귀 호출은 정방향으로 호출하기 때문에 노드 2가 먼저 출력된다. 그리고 노드 2의 자식 노드 3과 4가 남아있는데 3은 1의 자식 노드이면서 2의 자식 노드이기도 하다. 여기서 3을 먼저 방문하게 되면 나중에 노드 1한테 돌아왔을 떄 1은 방문하지 않는다.하지만 노드 2는 자식 노드가 3도 있고 4도 있다. 어느 쪽으로 갈지에 따라서 3을 여기서 출력할지 말지 결정이 되는데 그 순서는 연결 관계를 입력할 때 어떤 노드와의 관계를 먼저 입력했느냐에 따라서 결정이 된다. 여기서는 왼쪽부터 입력되었다고 가정하고 4를 먼저 호출하도록 하겠다.

</br>

[![2023-04-25-10-52-49.png](https://i.postimg.cc/26y76Df4/2023-04-25-10-52-49.png)](https://postimg.cc/WFRkWxz3)

</br>

노드 4를 호출하고, 출력한다.

</br>

[![2023-04-25-10-54-46.png](https://i.postimg.cc/KjzGw0Bc/2023-04-25-10-54-46.png)](https://postimg.cc/hzkR7b2N)

</br>

여기서 노드 3은 1의 자식 노드이면서 4의 자식 노드이기도 하다. 그런데 여기서 먼저 만났기 떄문에 노드 3을 4의 자식 노드로서 호출하고 출력한다. 나중에 돌아와서 1이 호출하려고 했을 때 노드 3은 이미 호출했기 때문에 더 이상 호출하지 않는다.

</br>

[![2023-04-25-10-56-51.png](https://i.postimg.cc/3xnT5Xrd/2023-04-25-10-56-51.png)](https://postimg.cc/RW68wnHB)

</br>

노드 3의 자식 노드들은 노드 5를 제외하고 모두 호출되었다. 남은 노드 5를 호출하고 출력한다.

</br>

[![2023-04-25-10-58-11.png](https://i.postimg.cc/JhfY90Xs/2023-04-25-10-58-11.png)](https://postimg.cc/yJTTRVvK)

</br>

노드 5의 자식 노드는 6, 7 두 개가 있는데, 노드 6이 먼저 있기 때문에 노드 6을 호출하고 출력한다.

</br>

[![2023-04-25-10-56-51.png](https://i.postimg.cc/3xnT5Xrd/2023-04-25-10-56-51.png)](https://postimg.cc/RW68wnHB)

</br>

노드 6의 자식노드 8을 호출하고 출력한다. 노드 8은 더 이상 자식 노드가 없기 때문에 나와서 노드 6으로 이동하고, 노드 6도 더 이상 호출할 자식 노드가 없기 때문에 나와서 노드 5로 이동한다.

</br>

[![2023-04-25-11-00-42.png](https://i.postimg.cc/qR9tcf9V/2023-04-25-11-00-42.png)](https://postimg.cc/njGcZWF0)

</br>

노드 5의 아직 호출되지 않은 자식 노드 7을 호출하고 출력한다. 노드 7은 더 이상 자식 노드가 없기 때문에 시작 노드까지 이동한 다음에 종료된다.

## 전체 코드

</br>

``` java
package DataStructure;

import java.util.LinkedList;
import java.util.Iterator;
import java.util.Stack;
import java.util.NoSuchElementException;

class Graph {
	
	class Node { // Node
		int data;	// Node의 정수형 data
		LinkedList<Node> adjacent;	// 해당 노드의 인접한 Node
		boolean marked;	// 해당 노드에 방문했는지 확인하는 marking하는 flag
		
		Node(int data) {	// Node의 생성, data를 받고 marking flag는 false로 초기화하고 LinkedList를 준비 
			this.data = data;
			this.marked = false;
			adjacent = new LinkedList<>();
		}
	}
	
	Node[] nodes;	// 그래프안에 노드들을 저장할 배열 
	
	Graph(int size) {	// 간단하게 하기 위해 그래프의 노드 갯수는 고정 
		nodes = new Node[size];	// 노드의 갯수를 받아서 그 갯수만큼 배열을 생성 
		for(int i = 0; i < size; i++) {	// 편의를 위해 데이터와 배열방 번호를 동일하게 설정 
			nodes[i] = new Node(i);
		}
	}
	
	void addEdge(int i1, int i2) {	// 두 노드의 관계를 저장하는 함수 
		Node n1 = nodes[i1];	// 데이터가 인덱스와 같기 떄문에 받은 숫자를 인덱스로 사용 
		Node n2 = nodes[i2];
		
		if(!n1.adjacent.contains(n2)) {
			n1.adjacent.add(n2);
		}
		
		if(!n2.adjacent.contains(n1)) {
			n2.adjacent.add(n1);
		}
		
		// 두 개의 노드의 인접한 노드들을 저장하는 LinkedList에 상대방이 있는지 확인하고 없으면 서로 추가 
	}
	
	void dfs() {	// dfs()를 그냥 호출하면 0번부터 시작 
		dfs(0);
	}
	
	void dfs(int index) {	// 시작 인덱스를 받아서 dfs 순회 결과를 출력하는 함수 
		Node root = nodes[index];	// 해당 인덱스의 노드 가져오기 
		Stack<Node> stack = new Stack<>();	// Stack 하나 생성 
		stack.push(root);	// 현재 노드를 Stack에 추가 
		root.marked = true;	// Stack에 들어갔었는지 표시 
		while(!stack.isEmpty()) {	// Stack에 데이터가 없을 때 까지 반복 
			Node r = stack.pop();	// Stack에서 데이터 하나 출력 
			for(Node n : r.adjacent) {	// 가져온 노드들의 인접한 노드들중 Stack에 추가된 적 없는 노드를 추가  
				if(n.marked == false) {
					n.marked = true;
					stack.push(n);
				}
			}
			visit(r);
		}
	}
	
	void bfs() {	// bfs()를 그냥 호출하면 0번부터 시작 
		bfs(0);
	}
	
	void bfs(int index) { 
		Node root = nodes[index];	// bfs() 함수에서 인덱스로 받은 인자로 노드를 받아 옴 
		Queue<Node> queue = new Queue<>();// Queue를 하나 생성 
		queue.add(root);	// 데이터를 queue에 추가 
		root.marked = true;
		while(!queue.isEmpty()) {	// queue가 다 비어있을 때까지 반복 
			Node r = queue.remove();	// Queue에서 데이터 가져오기 
			for(Node n : r.adjacent) {	// Queue에서 꺼낸 노드의 추가된 적 없는 자식 노드들을 Queue에 추가 
				if(n.marked == false) {
					n.marked = true;
					queue.add(n);
				}
			}
			visit(r);
		}
		
	}
	
	void dfsR(Node r) {	// 재귀 호출을 이용한 dfs, 재귀 호출을 할 때는 LinkedList가 노드의 주소를 가지고 있기 때문에 재귀 함수는 노드를 받는 형태 
		if(r == null) return;	// 받은 노드가 null이면 그냥 반환 
		r.marked = true;	// 호출이 되었었다고 노드에 마킹 
		visit(r);	// 인접한 노드를 호출하기 전에 데이터를 먼저 출력 
		for(Node n : r.adjacent) {	// 호출이 되지 않은 인접한 노드들을 호
			if(n.marked == false) {
				dfsR(n);
			}
		}
	}
	
	void dfsR(int index) {	// 시작 노드를 다양하게 테스트하기 위해서 배열의 인덱스를 받는 형태로도 선언 
		Node r = nodes[index];	// 인덱스를 받으면 노드를 찾
		dfsR(r);	// 해당 노드를 시작으로 재귀호출 
	}
	
	void dfsR() {	// 아무것도 호출하지 않았을 때는 0부터 시작 
		dfsR(0);
	}
	
	void visit(Node n) {	// 방문했을 때 출력하는 함수 
		System.out.print(n.data + " ");
	}
}

public class BFSTest {
	public static void main(String[] args) {
		Graph g = new Graph(9);	// 9개의 노드를 갖는 그래프 생성 
		g.addEdge(0, 1);	// 그래프의 관계 명시 
		g.addEdge(1, 2);
		g.addEdge(1, 3);
		g.addEdge(2, 4);
		g.addEdge(2, 3);
		g.addEdge(3, 4);
		g.addEdge(3, 5);
		g.addEdge(5, 6);
		g.addEdge(5, 7);
		g.addEdge(6, 8);
		g.dfsR(3);
	}
}
```

</br>