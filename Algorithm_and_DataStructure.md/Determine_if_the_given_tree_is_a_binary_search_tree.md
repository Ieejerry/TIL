# 주어진 트리가 이진검색트리인지 확인하기

</br>

[![2023-05-01-12-52-09.png](https://i.postimg.cc/5txPmB13/2023-05-01-12-52-09.png)](https://postimg.cc/68mLWG82)

</br>

## 첫 번째 솔루션

</br>

[![2023-05-01-12-53-02.png](https://i.postimg.cc/wT8nmstW/2023-05-01-12-53-02.png)](https://postimg.cc/Th0k81Jm)

</br>

위의 트리가 이진 검색을 할 수 있는 트리인지를 확인해야 한다. 이진 검색 트리는 어떤 노드를 붙잡고 가도 노드의 왼쪽 트리들은 자기보다 작은 값을 가지고, 오른쪽 노드들은 자기보다 큰 값을 가진다.

</br>

[![2023-05-01-12-57-58.png](https://i.postimg.cc/T1Rmz977/2023-05-01-12-57-58.png)](https://postimg.cc/2bKVv4fh)

</br>

inorder 순회는 left -> root -> right 순으로 트리르 횡단하는 순횡 방법이다. 위의 결과를 보면 inorder 방법으로 순회를 하면 이진 검색 트리를 값의 순서와 일치한다. 그래서 이 값으로 정렬이 된 배열에 담을 수 있다.

그러면 트리의 값들을 inorder로 순회를 해서 배열에 담은 다음에 배열에서 값들이 ascending order가 되어있는지만 확인하면 된다.

</br>

### 첫 번째 솔루션 코드

</br>

``` java
package DataStructure;

import DataStructure.Tree6.Node;

class Tree7 {
	class Node {
		int data;
		Node left;
		Node right;
		
		Node(int data) {
			this.data = data;
		}
	}
	
	Node root;	// 루트 노드를 멤버 변수로 선언 
	int size;	// 사이즈를 멤버 변수로 선언 
	
	Tree7(int size) {	// 트리를 생성할 때, 사이즈로 이진 트리 생성 
		this.size = size;
		root = makeBST(0, size - 1);
		root.right.right.right.left = new Node(10);
		this.size++;
	}
	
	Node makeBST(int start, int end) {	// 이진 트리를 구현하는 함수 
		if(start > end) return null;
		int mid = (start + end) / 2;
		Node node = new Node(mid);
		node.left = makeBST(start, mid - 1);
		node.right = makeBST(mid + 1, end);
		return node;
	}
	
	boolean isValidateBST1() {
		int[] array = new int[size];	// 노드 갯수 만큼의 길이를 가지는 배열 생성 
		inorder(root, array);	// 시작 노드와 순서대로 가져온 데이터를 담을 배열의 주소를 넘기면서 inorder함수 호출 
		for(int i = 1; i < array.length; i++) {	// inorder 함수에서 저장한 배열을 돌면서 바로 왼쪽에 있는 데이터가 현재 데이터보다 크면 false 반환 
			if(array[i] < array[i - 1]) {
				return false;
			}
		}
		return true;	// 돌면서 잘못된 부분이 없으면 true를 반환 
	}
	
	int index = 0;	// 몇 번 배열까지 담았는지 기억하고 있을 정수 선언 
	void inorder(Node root, int[] array) {
		if(root != null) {	// 노드가 null이 아닐 때까지 반복 
			inorder(root.left, array);	// 순서에 입각해서 왼쪽 노드를 먼저 호출 
			array[index] = root.data;	// 나 자신을 배열에 출력 
			index++;	// 배열의 데이터 사이즈를 하나 증가 
			inorder(root.right, array);	// 노드의 오른쪽 서브 트리들을 재귀적으로 호출 
		}
	}
}

public class InorderTest {
	public static void main(String[] args) {
		Tree7 t = new Tree7(10);	// 트리 생성 
		System.out.println("Solution 1 - using inorder: " + t.isValidateBST1());	// 첫 번째 솔루션의 결과값 출력 
	}
}
```

```
Solution 1 - using inorder: false
```

</br>

## 두 번째 솔루션

</br>

[![2023-05-01-1-27-21.png](https://i.postimg.cc/tggVN5vp/2023-05-01-1-27-21.png)](https://postimg.cc/YvJ9p1ws)

</br>

그런데 위와 같이 배열에 값을 담으면 n만큼의 공간이 추가로 소요된다. 어차피 필요한 것은 비교할 바로 앞의 값이기 때문에 시작할 때 바로 앞에 값을 담을 저장공간을 하나 선언하고, 트리를 돌면서 그 값과 노드의 값을 비교하고, 비교한 뒤에는 현재의 노드값을 이 공간에 저장을 해서 다음 노드가 전 노드의 값과 비교하면 배열만큼의 공간을 아낄 수 있다.

</br>

### 두 번째 솔루션 코드

</br>

``` java
package DataStructure;

class Tree7 {
	class Node {
		int data;
		Node left;
		Node right;
		
		Node(int data) {
			this.data = data;
		}
	}
	
	Node root;	// 루트 노드를 멤버 변수로 선언 
	int size;	// 사이즈를 멤버 변수로 선언 
	
	Tree7(int size) {	// 트리를 생성할 때, 사이즈로 이진 트리 생성 
		this.size = size;
		root = makeBST(0, size - 1);
//		root.right.right.right.left = new Node(10);
//		this.size++;
	}
	
	Node makeBST(int start, int end) {	// 이진 트리를 구현하는 함수 
		if(start > end) return null;
		int mid = (start + end) / 2;
		Node node = new Node(mid);
		node.left = makeBST(start, mid - 1);
		node.right = makeBST(mid + 1, end);
		return node;
	}
	
	boolean isValidateBST1() {
		int[] array = new int[size];	// 노드 갯수 만큼의 길이를 가지는 배열 생성 
		inorder(root, array);	// 시작 노드와 순서대로 가져온 데이터를 담을 배열의 주소를 넘기면서 inorder함수 호출 
		for(int i = 1; i < array.length; i++) {	// inorder 함수에서 저장한 배열을 돌면서 바로 왼쪽에 있는 데이터가 현재 데이터보다 크면 false 반환 
			if(array[i] < array[i - 1]) {
				return false;
			}
		}
		return true;	// 돌면서 잘못된 부분이 없으면 true를 반환 
	}
	
	int index = 0;	// 몇 번 배열까지 담았는지 기억하고 있을 정수 선언 
	void inorder(Node root, int[] array) {
		if(root != null) {	// 노드가 null이 아닐 때까지 반복 
			inorder(root.left, array);	// 순서에 입각해서 왼쪽 노드를 먼저 호출 
			array[index] = root.data;	// 나 자신을 배열에 출력 
			index++;	// 배열의 데이터 사이즈를 하나 증가 
			inorder(root.right, array);	// 노드의 오른쪽 서브 트리들을 재귀적으로 호출 
		}
	}
	
	Integer last_printed = null;	// 바로 이전 노드에 있었던 값을 저장하는 last_printed라는 변수를 정수 객체에 주소를 넘길 수 있도록 클래스 타입으로 선언 
	boolean isValidateBST2() {
		return isValidateBST2(root);	// 인자가 없이 호출되면 root 노드를 시작 노드로 재귀 호출을 시작 
	}
	
	boolean isValidateBST2(Node n) {	// 재귀 함수는 노드를 받고 boolean 타입으로 true나 false를 반환 
		if(n == null) return true;	// 노드의 마지막을 지나면 true를 반환 
		if(!isValidateBST2(n.left))	return false;	// 왼쪽 노드들을 돌면서 결과를 받아서 만약에 정렬되어있지 않은 값을 이미 만났으면 false를 반환 
		if(last_printed != null && n.data < last_printed) {	// 그렇지 않으면 바로 전에 저장된 값을 현재 노드의 값과 비교 
			return false;	// 만약 전의 값이 현재값보다 더 크면 순서가 틀렸기 때문에 false를 반환 
		}
		last_printed = n.data;	// 문제 없이 통과 되었으면 현재 데이터 값을 이전 값에 할당 
		if(!isValidateBST2(n.right)) return false;	// 오른쪽 노드들을 돌다가 문제가 되는 결과를 받으면 false를 반환 
		return true;	// 끝까지 false 조건에 안 걸리면 true를 반환 
	}
}

public class InorderTest {
	public static void main(String[] args) {
		Tree7 t = new Tree7(10);	// 트리 생성 
		System.out.println("Solution 1 - using inorder: " + t.isValidateBST1());	// 첫 번째 솔루션의 결과값 출력 
		System.out.println("Solution 2 - without array: " + t.isValidateBST2());	//  번째 솔루션의 결과값 출력 
	}
}
```

```
Solution 1 - using inorder: true
Solution 2 - without array: true
```

</br>

## 세 번째 솔루션

</br>

[![2023-05-01-2-12-35.png](https://i.postimg.cc/PxkjQG2q/2023-05-01-2-12-35.png)](https://postimg.cc/nsTgnW88)

</br>

root에서 내려가면서 해당 노드가 가질 수 있는 값의 영역을 제한하는 방법이 있다. 현재 4에서 시작해서 왼쪽으로 내려가면 이하 값들은 4보다 작아야 한다. 그런데 여기서 1을 지나갈 때 조건이 더해진다. 왼쪽으로 가면 4가 아니라 1보다 작아야 하고, 오른쪽으로 가면 1보다는 크고, 4보다는 작아야 한다. 그리고 2에서 다시 오른쪽으로 갈 때는 조건이 더해져서 2보다는 크고, 4보다는 작아야 한다. 이렇게 왼쪽으로 갈 때는 맥시멈 조건을 변경하고, 오른쪽으로 갈 때는 미니멈 조건을 자기 노드값으로 변경해서 다음 노드를 호출하다가 조건의 영역을 벗어나는 값을 발견하면 바로 false를 반환한다. 

</br>

### 세 번째 솔루션 코드

</br>

``` java
package DataStructure;

class Tree7 {
	class Node {
		int data;
		Node left;
		Node right;
		
		Node(int data) {
			this.data = data;
		}
	}
	
	Node root;	// 루트 노드를 멤버 변수로 선언 
	int size;	// 사이즈를 멤버 변수로 선언 
	
	Tree7(int size) {	// 트리를 생성할 때, 사이즈로 이진 트리 생성 
		this.size = size;
		root = makeBST(0, size - 1);
		root.right.right.right.left = new Node(9); this.size++;
		root.right.right.right.right = new Node(9); this.size++;
		root.right.right.right.left.left = new Node(9); this.size++;
		root.right.right.right.left.right = new Node(9); this.size++;
		root.right.right.right.left.left.left = new Node(8); this.size++;
		root.right.right.right.left.left.right = new Node(9); this.size++;
	}
	
	Node makeBST(int start, int end) {	// 이진 트리를 구현하는 함수 
		if(start > end) return null;
		int mid = (start + end) / 2;
		Node node = new Node(mid);
		node.left = makeBST(start, mid - 1);
		node.right = makeBST(mid + 1, end);
		return node;
	}
	
	boolean isValidateBST1() {
		int[] array = new int[size];	// 노드 갯수 만큼의 길이를 가지는 배열 생성 
		inorder(root, array);	// 시작 노드와 순서대로 가져온 데이터를 담을 배열의 주소를 넘기면서 inorder함수 호출 
		for(int i = 1; i < array.length; i++) {	// inorder 함수에서 저장한 배열을 돌면서 바로 왼쪽에 있는 데이터가 현재 데이터보다 크면 false 반환 
			if(array[i] < array[i - 1]) {
				return false;
			}
		}
		return true;	// 돌면서 잘못된 부분이 없으면 true를 반환 
	}
	
	int index = 0;	// 몇 번 배열까지 담았는지 기억하고 있을 정수 선언 
	void inorder(Node root, int[] array) {
		if(root != null) {	// 노드가 null이 아닐 때까지 반복 
			inorder(root.left, array);	// 순서에 입각해서 왼쪽 노드를 먼저 호출 
			array[index] = root.data;	// 나 자신을 배열에 출력 
			index++;	// 배열의 데이터 사이즈를 하나 증가 
			inorder(root.right, array);	// 노드의 오른쪽 서브 트리들을 재귀적으로 호출 
		}
	}
	
	Integer last_printed = null;	// 바로 이전 노드에 있었던 값을 저장하는 last_printed라는 변수를 정수 객체에 주소를 넘길 수 있도록 클래스 타입으로 선언 
	boolean isValidateBST2() {
		return isValidateBST2(root);	// 인자가 없이 호출되면 root 노드를 시작 노드로 재귀 호출을 시작 
	}
	
	boolean isValidateBST2(Node n) {	// 재귀 함수는 노드를 받고 boolean 타입으로 true나 false를 반환 
		if(n == null) return true;	// 노드의 마지막을 지나면 true를 반환 
		if(!isValidateBST2(n.left))	return false;	// 왼쪽 노드들을 돌면서 결과를 받아서 만약에 정렬되어있지 않은 값을 이미 만났으면 false를 반환 
		if(last_printed != null && n.data < last_printed) {	// 그렇지 않으면 바로 전에 저장된 값을 현재 노드의 값과 비교 
			return false;	// 만약 전의 값이 현재값보다 더 크면 순서가 틀렸기 때문에 false를 반환 
		}
		last_printed = n.data;	// 문제 없이 통과 되었으면 현재 데이터 값을 이전 값에 할당 
		if(!isValidateBST2(n.right)) return false;	// 오른쪽 노드들을 돌다가 문제가 되는 결과를 받으면 false를 반환 
		return true;	// 끝까지 false 조건에 안 걸리면 true를 반환 
	}
	
	boolean isValidateBST3() {
		return isValidateBST3(root, Integer.MIN_VALUE, Integer.MAX_VALUE);	// 재귀 함수의 인자를 초기화하여 호출 
	}
	
	boolean isValidateBST3(Node n, int min, int max) {	// 노드와 최소, 최대값을 받는 재귀 함수 선언 
		if(n == null) {	// 노드가 null이면 재귀 호출을 종료 
			return true;
		}
		if(n.data < min || n.data > max) {	// 노드의 값이 최소, 최대값의 영역을 벗어나면 false를 반환 
			return false;
		}
		if(!isValidateBST3(n.left, min, n.data) || !isValidateBST3(n.right, n.data, max)) {	// 그렇지 않으면 왼쪽 오른쪽 노드들을 가지고 다시 함수를 호출, 왼쪽으로 이동할 때는 최대값을 현재값으로 대체, 오른쪽으로 이동할 때는 최소값을 현재값으로 대체하여 범위를 좁혀준다. 
			return false;	// 두 개의 결과중에 하나라도 false가 있으면 false를 반환 
		}
		return true;	// 모든 조건을 통과하면 true를 반환 
 	}
}

public class InorderTest {
	public static void main(String[] args) {
		Tree7 t = new Tree7(10);	// 트리 생성 
		System.out.println("Solution 1 - using inorder: " + t.isValidateBST1());	// 첫 번째 솔루션의 결과값 출력 
		System.out.println("Solution 2 - without array: " + t.isValidateBST2());	//  번째 솔루션의 결과값 출력 
		System.out.println("Solution 3 - min/max: " + t.isValidateBST3());	//  번째 솔루션의 결과값 출력 
	}
}
``` 

```
Solution 1 - using inorder: true
Solution 2 - without array: true
Solution 3 - min/max: true
```

</br>

이진 검색 트리에서 중복값을 허용할지 말지는 상황에 따라 달라지는데, 위의 코드에서는 중복이 되지만, 순서가 섞이지는 않는다. 따라서 데이터가 정렬이 되어있는 한 이진 검색은 가능하다. 

즉, 중복되는 값이 있다고 해서 이진 검색 트리가 아니라고 할 수는 없다. 그래서 세 개의 솔루션 모두 true를 반환한다. 하지만 대부분의 경우에는 이진검색트리의 중복값을 허용하지 않는다. 