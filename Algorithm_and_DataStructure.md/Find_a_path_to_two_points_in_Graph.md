# Graph에서 두지점의 경로찾기

</br>

[![2023-04-26-11-08-44.png](https://i.postimg.cc/Jnt7wPzB/2023-04-26-11-08-44.png)](https://postimg.cc/mzfWC3Mb)

</br>

[![2023-04-26-11-15-19.png](https://i.postimg.cc/zXqWLHp2/2023-04-26-11-15-19.png)](https://postimg.cc/YjyjZ95Q)

</br>

그래프에서 노드 A, 노드 B 두 개의 노드 간에는 어떤 식으로든 경로가 존재한다. 그런데 그래프의 중간에 edge가 하나 끊어지면 두 노드간의 경로가 없어진다. 이렇게 두 개의 떨어져 있는 노드를 서로 연결해주는 전제 경로가 있는지 확인하는 함수를 만들어야 한다.

</br>

## 전체 코드

</br>

``` java
package DataStructure;

import java.io.Serial;
import java.util.LinkedList;

class Graph2 {	// 그래프 클래스 생성 
	class Node {	// 노드 선언 
		int data;
		boolean marked;
		LinkedList<Node> adjacent;
		
		Node(int data) {
			this.data = data;
			this.marked = false;
			this.adjacent = new LinkedList<Node>();
		}
	}
	
	Node[] nodes;	// 노드를 관리할 배열 생성 
	
	Graph2(int size) {	// 생성자에서 노드를 노드를 생성 
		nodes = new Node[size];
		for(int i = 0; i < size; i++) {
			nodes[i] = new Node(i);
		}
	}
	
	void addEdge(int i1, int i2) {	// edge를 추가하는 함수 
		Node n1 = nodes[i1];
		Node n2 = nodes[i2];
		
		if(!n1.adjacent.contains(n2)) {
			n1.adjacent.add(n2);
		}
		
		if(!n2.adjacent.contains(n1)) {
			n2.adjacent.add(n1);
		}
	}
	
	void initMarks() {	// 검색에 들어가기 전에 모든 마킹 플래그들이 false로 되어 있는지 확실히 하기 위해서 마킹 플래그를 전부 false로 초기화 해주는 함
		for(Node n : nodes) {
			n.marked = false;
		}
	}
	
	boolean search(int i1, int i2) {	// 배열 인덱스로 호출하면 노드로 변환해서 호출하는 함
		return search(nodes[i1], nodes[i2]);
	}
	
	boolean search(Node start, Node end) {	// start와 end 노드를 받아 두 개의 노드간에 경로가 존재하는지 확인하는 함수 
		initMarks();	// marking flag를 초기화하는 함수 호출해서 모든 플래그들이 false가 되도록 함 
		LinkedList<Node> q = new LinkedList<>();	// Queue로 사용할 LinkedList 생성 
		q.add(start);	// 시작 노드를 큐에 추가 
		while(!q.isEmpty()) {
			Node root = q.removeFirst();	// 큐에서 데이터를 하나 꺼내서 
			if(root == end) {	// 꺼낸 노드가 end 노드인지 확인해서 end 노드이면 바로 true를 반환해서 함수를 종료 
				return true;
			}
			for(Node n : root.adjacent) {	// 그 노드의 인접한 노드를 돌면서 
				if(n.marked == false) {	// 큐에 안 들어왔던 노드들만 큐에 추가 
					n.marked = true;
					q.add(n);
				}	// 해당 노드들의 인접한 노드들을 전부 돌면서 큐에 추가  
			}
		}	// 인접한 노드들을 다 추가한 이후에는 다시 올라가서 큐에서 데이터를 꺼내서 똑같은 작업을 큐에 데이터가 하나도 남아있지 않을 때까지 반복
		return false;	// 모든 작업을 마친 후에도 아직도 리턴이 안되었다면 그건 경로를 찾지 못했다는 의미로 false를 반환 
	}
}

public class GraphTest {
	public static void main(String[] args) {
		Graph2 g = new Graph2(9);	// 9개의 노드를 가지는 그래프를 생성 
		g.addEdge(0, 1);	// 그래프의 관계 명시 
		g.addEdge(1, 2);
//		g.addEdge(1, 3);
//		g.addEdge(2, 4);
//		g.addEdge(2, 3);
		g.addEdge(3, 4);
		g.addEdge(3, 5);
		g.addEdge(5, 6);
		g.addEdge(5, 7);
		g.addEdge(6, 8);
		System.out.println(g.search(1, 8));	// 그래프의 1과 8이 연결되어있는지 확인 
	}
}
```

</br>