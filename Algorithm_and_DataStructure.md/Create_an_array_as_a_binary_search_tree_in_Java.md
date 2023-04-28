# 배열을 이진검색트리로 만들기 in Java

</br>

[![2023-04-28-7-11-10.png](https://i.postimg.cc/KjWyTysr/2023-04-28-7-11-10.png)](https://postimg.cc/q62YfWrz)

</br>

[![2023-04-28-7-11-10.png](https://i.postimg.cc/KjWyTysr/2023-04-28-7-11-10.png)](https://postimg.cc/q62YfWrz)

</br>

위의 배열은 이미 정렬이 되어있고, 배열의 길이가 고정이기 때문에 이진 검색을 하려면 배열의 가장 가운데에 있는 숫자를 보고 검색하고자 하는 숫자가 작으면 왼쪽, 더 크면 오른쪽 이런 식으로 찾아 들어가면 된다.

</br>

[![2023-04-28-7-19-33.png](https://i.postimg.cc/SNWHf85z/2023-04-28-7-19-33.png)](https://postimg.cc/0byt8698)

</br>

예를 들어 2를 찾으려면, 배열을 반으로 잘라서 중간값을 찾는다. 위에 배열에서는 배열 길이가 10이기 때문에 4나 5가 중간값이 된다. 위의 배열은 길이가 짝수여서 딱 나누어져서 중간의 값이 없기 때문에 중간에 있는 두 개의 숫자중에 앞에 있는 숫자 중간값으로 하는 규칙을 만들고, 중간값 4를 주이진 값 2와 비교하여 같으면 주어진 값을 찾은 것이고, 주어진 값이 더 작으면 왼쪽, 크면 오른쪽에 있는 것이다. 여기서는 2가 4보다 작기 때문에 주어진 값 2는 4보다 왼쪽에 있다. 그러면 오른쪽의 데이터들은 안 봐도 되기 때문에 4부터 오른쪽 값들은 검색 목록에서 제외한다. 

</br>

[![2023-04-28-7-11-58.png](https://i.postimg.cc/vZN3dZxv/2023-04-28-7-11-58.png)](https://postimg.cc/HrbQwH2J)

</br>

이제 4의 왼쪽 값들 중에 중간값을 찾는다. 중간값은 중간에 있는 1이나 2가 되는데, 앞에서 중간값은 두 숫자중에 앞에 있는 숫자를 채택한다는 규칙을 만들었기 때문에 1이 중간값이 된다. 그러면 1과 2를 비교하고, 2는 1보다 크기 때문에 1보다 왼쪽에 있는 값들 이제 안 봐도 되기 때문에 1의 오른쪽 숫자중에 찾아야 한다.

</br>

[![2023-04-28-7-23-12.png](https://i.postimg.cc/fTw15kh2/2023-04-28-7-23-12.png)](https://postimg.cc/8s0yzpcM)

</br>

이제 또 중간값을 찾는데 2와 3중에 앞에 있는 숫자인 2를 중간값으로 한다. 그리고 주어진 값 2와 중간값 2를 비교한다. 주어진 값과 중간값이 같기 때문에 원하는 데이터를 찾게된다.

데이터를 정확하게 반씩 잘라서 영역을 좁혀 나감으로써 데이터를 찾아낼 수 있게 구현된 트리가 이진 검색 트리이다.

</br>

[![2023-04-28-7-23-12.png](https://i.postimg.cc/fTw15kh2/2023-04-28-7-23-12.png)](https://postimg.cc/8s0yzpcM)

</br>

위에 배열로 이동했던 경로를 이진 검색 트리로 표현해보겠다. 우선 중간값 4는 root 노드가 된다. 이제 4를 기준으로 작은 쪽 S, 큰 쪽 B, 두 개의 그룹으로 나뉜다.

</br>

[![2023-04-28-7-32-28.png](https://i.postimg.cc/MGPrsYqd/2023-04-28-7-32-28.png)](https://postimg.cc/2qWwyhqZ)

</br>

작은 쪽 그룹을 먼저 보면 이 그룹의 중간값은 1이 된다. 1을 노드로 추가한다. 이 때 이 값은 root보다 작으니깐 왼쪽에 추가한다.

</br>

[![2023-04-28-7-34-17.png](https://i.postimg.cc/XvmkG1VS/2023-04-28-7-34-17.png)](https://postimg.cc/qtc3WLhj)

</br>

또 중간값 1을 기준으로 작은 쪽 S, 큰 쪽 B 두 그룹으로 나뉜다. 작은 쪽을 먼저 보면 데이터가 하나이기 때문에 중간값은 0이 된다. 그런데 이 때 0은 1보다 작기 때문에 왼쪽에 붙인다.

</br>

[![2023-04-28-7-36-07.png](https://i.postimg.cc/NMvrv3sM/2023-04-28-7-36-07.png)](https://postimg.cc/DW5zqYbk)

</br>

이제 오른쪽에 남은 그룹을 보면 2와 3중에 왼쪽에 있는 2가 중간값이 되고, 이 그룹의 위의 중간값은 1이기 떄문에 1에 붙여준다. 근데 이 때 2는 1보다 크기 때문에 1의 오른쪽에 붙여준다.  

</br>

[![2023-04-28-7-37-30.png](https://i.postimg.cc/Kc6cqPYG/2023-04-28-7-37-30.png)](https://postimg.cc/NLxwLrTS)

</br>

남은 3의 중간값은 3이기 때문에 2에 3을 붙여준다. 3은 2보다 크기 때문에 2의 오른쪽에 붙여준다.

</br>

[![2023-04-28-7-40-33.png](https://i.postimg.cc/QxYmZdRd/2023-04-28-7-40-33.png)](https://postimg.cc/qzny84JP)

</br>

그러면 4의 왼쪽 그룹은 끝이 나고, 오른쪽 그룹을 보겠다. 오른쪽 그룹의 중간값은 7이 된다. 7은 4보다 크기 때문에 4의 오른쪽에 붙여준다.

</br>

[![2023-04-28-10-27-17.png](https://i.postimg.cc/d3SsBndg/2023-04-28-10-27-17.png)](https://postimg.cc/rRx2y1f9)

</br>

이제 7을 기준으로 작은 그룹 S, 큰 그룹 B로 나뉜다. 왼쪽 그룹에 5와 6중 규칙에 의해 5가 중간값이 된다. 중간값 5는 7보다 작기 때문에 7의 왼쪽에 붙게 된다.

</br>

[![2023-04-28-10-28-53.png](https://i.postimg.cc/hvFWPwLD/2023-04-28-10-28-53.png)](https://postimg.cc/zbkPxx26)

</br>

그리고 5 다음에 6은 5의 오른쪽에 있기 때문에 5의 오른쪽에 붙여준다.

</br>

[![2023-04-28-10-30-15.png](https://i.postimg.cc/XJbkjkZM/2023-04-28-10-30-15.png)](https://postimg.cc/gwgZ4Rq4)

</br>

7 기준의 큰 그룹의 중간값은 8이 된다. 8은 7보다 크기 때문에 7의 오른쪽에 붙여준다.

</br>

[![2023-04-28-10-31-21.png](https://i.postimg.cc/j2W5BGsR/2023-04-28-10-31-21.png)](https://postimg.cc/JHLMkYDF)

</br>

8의 오른쪽에 9는 8보다 크기 때문에 8의 오른쪽에 붙여준다.

이렇게 정렬된 배열을 가지고 이진 검색 트리를 만들었다. 이진 검색으로 큰지 작은지만 비교해서 가다보면 원하는 값을 찾을 수 있다. 한 번 이동할 때마다 찾아야하는 데이터의 양이 절반씩 줄어들기 때문에 이 알고리즘의 시간 복잡도는 노드의 갯수를 n이라고 했을 때, O(log n)의 시간 복잡도를 갖는다.

이 알고리즘은 중간값을 찾고 두 개로 나눠서, 또 중간값을 찾고 또 두 개로 나눠서 또 중간값을 찾는 로직이 반복된다. 그래서 같은 일을 처리하는 함수를 하나 만들고 재귀적으로 호출하면 좋다. 함수에 필요한 정보는 트리로 만들 데이터가 들어있는 배열이 필요하고 매번 처리해야 하는 데이터의 그룹들이 달라지기 때문에 해당 그룹이 시작하는 인덱스와 끝나는 인덱스를 받아서 어디서부터 어디까지 그룹을 트리로 만들어야 되는지를 함수가 알 수 있게 인자로 전달해줘야 한다. 중간값은 인자로 받은 그룹의 시작값과 끝값을 더한 다음 2로 나누면 중간값을 알 수 있다.

## 전체 코드

</br>

``` java
package DataStructure;

class Tree2 {	// Tree2 클래스 생성 
	class Node {	// Node 내부 클래스 생성 
		int data;	// 정수형 데이터 
		Node left;	// 왼쪽 노드를 저장할 변수 
		Node rigth;	// 오른쪽 노드를 저장할 변수 
		
		Node(int data) {	// 생성자에서 데이터를 받아서 노드에 저장 
			this.data = data;
		}
	}
	
	// Tree의 멤버 변수 
	Node root;	// Tree가 시작되는 root 노드 
	
	public void makeTree(int[] a) {	// 배열 정보를 받아서 Tree를 만드는 일을 시작해주는 메소드 선언 
		root = makeTreeR(a, 0, a.length - 1);	// 이 함수는 재귀 호출을 반복적으로 실행하기 앞서서 재귀호출에 필요한 데이터를 처음으로 던져주는 일을 한다. 그리고 재귀호출이 끝나면 가장 꼭대기에 있는 root노드의 주소를 받아서 멤버변에 저장  
	}
	
	public Node makeTreeR(int[] a, int start, int end) {	// 재귀 함수, 인자로는 배열 정와 시작 인덱스, 끝 인덱스를 받는다.
		if(start > end) return null;	// 이 함수를 반복적으로 호출하다가 시작점이 끝나는 점보다 커져버리면 그 땐 재귀호출을 마치고 null을 반환 
		// 끝나는 시점을 명확하게 해주는 것은 재귀호출에서 가장 중요한 부분이다. 그렇지 않으면 무한 루프를 돌게 된다. 
		int mid = (start + end) / 2;	// 받은 시작점과 끝지점으로 중간지점을 계산하고 
		Node node = new Node(a[mid]);	// 그 중간지점에 저장된 값으로 노드를 생성 
		node.left = makeTreeR(a, start, mid - 1);	// 재귀호출, 시작점부터 중간값 바로 앞에 있는 인덱스까지의 서브 트리를 현재 노드의 left에 저장 
		node.rigth = makeTreeR(a, mid + 1, end);	// 재귀호출, 중간값 바로 다음 인덱스부터 끝지점까지의 데이터로 만든 서브 트리는 현재 노드의 right 노드에 저장
		return node;	// node 반환 
	}
	
	public void searchBTree(Node n, int find) {	// 트리가 잘 만들어졌는지 이진 검색으로 확인하는 함, 검색을 할 시작 노드와 찾을 데이터를 함수의 인자로 받음 
		if(find < n.data) {	// 찾아야하는 값이 현재 노드의 데이터보다 작은 지를 비교하고 
			System.out.println("Data is smaller than " + n.data);	// 우선 진행경로를 확인하기 위해 데이터를 출력 
			searchBTree(n.left, find);	// 찾는 값이 더 작기 때문에 왼쪽 노드 주소와 찾는 값을 넘기고 재귀 호출 
		} else if (find > n.data) {	// 찾는 값이 받은 데이터보다 큰 지를 비교 
			System.out.println("Data is bigger than " + n.data);	// 로그 남김
			searchBTree(n.rigth, find);	// 찾는 값보다 더 크기 때문에 오른쪽 서브 트리에 root주소를 넘김 
		} else {	// 데이터가 크지도 작지도 않으면 같은 것이기 때문에 더 이상 재귀호출을 할 필요가 없기 때문에 찾았다고 로그를 남기고 함수를 종료 
			System.out.println("Data found!");
		}
	}
}

public class BinarySearchTreeTest {
	public static void main(String[] args) {
		int[] a = new int[10];	// 길이가 10인 배열 생성 
		for(int i = 0; i < a.length; i++) {	// 배열에 숫자들을 대입 
			a[i] = i;
		}
		
		Tree2 t = new Tree2();	// Tree2 생성 
		t.makeTree(a);	// makeTree 함수를 호출하여 해당 배열로 트리를 만들고 멤버변수 root에 저장 
		t.searchBTree(t.root, 2);	// searchBTree로 결과 확인 
	}
}
```

```
Data is smaller than 4
Data is bigger than 1
Data found!
```