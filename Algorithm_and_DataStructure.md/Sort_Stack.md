# Stack 정렬하기

</br>

[![2023-04-17-10-31-36.png](https://i.postimg.cc/wB25QH9W/2023-04-17-10-31-36.png)](https://postimg.cc/SXXzmB28)

</br>

[![2023-04-17-10-35-22.png](https://i.postimg.cc/XqdTsxQ7/2023-04-17-10-35-22.png)](https://postimg.cc/ZvY7R8G1)

</br>

정렬이 되어있지 않은 Stack이 하나 주어졌다. 다른 데이터 구조 아무것도 쓸 수 없고, 추가적으로 Stack 하나 더 사용할 수 있다. 이 문제를 풀기 위해서는 정렬되어 있지 않은 데이터들을 두 번째 Stack으로 옮기면서 정렬을 시켜야 한다. 첫 번째 Stack에서 `pop()`하면서 두 번째 Stack의 데이터와 비교를 해서 자기보다 큰 데이터는 첫 번째 Stack으로 다시 옮기면 된다. 그래서 가장 작은 값이 가장 밑으로 오게 해주면 된다.

</br>

[![2023-04-17-10-39-19.png](https://i.postimg.cc/cCkXM3N4/2023-04-17-10-39-19.png)](https://postimg.cc/m1MYTtD0)

</br>

6을 `pop()`하였다. 하지만 두 번째 Stack은 비어있기 때문에 6을 그대로 `push()`해준다.

</br>

[![2023-04-17-10-43-38.png](https://i.postimg.cc/XvM3kGV8/2023-04-17-10-43-38.png)](https://postimg.cc/xXPW0dNJ)

</br>

그 다음 데이터인 1을 `pop()`하고, 두 번째 Stack의 데이터인 6과 비교한다. 6은 1보다 크기 때문에 두 번째 Stack에서 `pop()`하고 다시 첫 번째 Stack으로 `push()`해주고, 1은 두 번째 Stack에 `push()`해준다. 그 다음 다시 첫 번째 마지막 데이터인 6을 `pop()`하고, 두 번째 Stack의 마지막 데이터인 1과 비교한다.

</br>

[![2023-04-17-10-46-34.png](https://i.postimg.cc/zBFgrYds/2023-04-17-10-46-34.png)](https://postimg.cc/wy3vXZY2)

</br>

6은 1보다 크기 때문에 그래도 두 번째 Stack에 `push()`한다.

</br>

[![2023-04-17-10-48-06.png](https://i.postimg.cc/Dzt9KtWP/2023-04-17-10-48-06.png)](https://postimg.cc/B8BYT7Bj)

</br>

[![2023-04-17-10-53-17.png](https://i.postimg.cc/bJ1wX0vd/2023-04-17-10-53-17.png)](https://postimg.cc/0M2sDwDq)

</br>

다음 데이터인 5는 6보다 작기 때문에 6을 첫 번째 Stack으로 옮기고, 5를 두 번째 Stack에 넣는다. 그리고 6을 다시 비교하고, 두 번째 Stack에는 자신보다 작은 수들 밖에 없기 때문에 그대로 넣어준다.

</br>

[![2023-04-17-10-55-03.png](https://i.postimg.cc/vmLNpcsb/2023-04-17-10-55-03.png)](https://postimg.cc/B8bpFZbV)

</br>

다음 데이터인 3은 두 번째 Stack의 6과 5보다 작다. 그래서 6과 5를 차례대로 `pop()`한 후에, 첫 번째 Stack으로 `push()`해준다.

</br>

[![2023-04-17-10-57-57.png](https://i.postimg.cc/G2Tqbt04/2023-04-17-10-57-57.png)](https://postimg.cc/Vr1jRYkw)

</br>

그 다음, 3을 두 번째 Stack에 넣어주고, 5와 6을 다시 순서대로 꺼내서 두 번째 Stack에 넣어준다. 그러면 두 번째 Stack에는 역순으로 정렬이 되고, 그 상태에서 다시 첫 번째 Stack으로 부어주면 오름차순으로 정렬이 된다.

</br>

## 전체 코드

</br>

``` java
package DataStructure;

import java.util.Stack;

public class StackTest2 {
	public static void main(String[] args) {
		Stack<Integer> s1 = new Stack<>();
		s1.push(3);
		s1.push(5);
		s1.push(1);
		s1.push(6);
		sort(s1);
		System.out.println(s1.pop());
		System.out.println(s1.pop());
		System.out.println(s1.pop());
		System.out.println(s1.pop());
	}
	
	private static void sort(Stack<Integer> s1) {
		Stack<Integer> s2 = new Stack<>();
		while(!s1.empty()) {
			int tmp = s1.pop();
			while (!s2.isEmpty() && s2.peek() > tmp) {
				s1.push(s2.pop());
			}
			s2.push(tmp);
		}
		
		while (!s2.empty()) {
			s1.push(s2.pop());
		}
	}
}
```

```
1
3
5
6
```