# Tree의 종류

</br>

## Tree란?

</br>

[![2023-04-18-9-30-12.png](https://i.postimg.cc/Z5ybBmz7/2023-04-18-9-30-12.png)](https://postimg.cc/K1xSwdzB)

</br>

Array, LinkedList, Stack, Queue는 라인처럼 생긴 일직선 데이터 구조인데, 트리는 부모 자식관계를 가지는 구조이다. 그래서 Tree는 계층이고, 그룹이다. 이걸 가능하게 하는 것은 다 노드가 하나 이상의 자식을 갖기 때문이다. 트리의 노드중에는 부모를 아는 경우도 있고, 자식만 아는 경우도 있고, 어떠한 특정한 순서에 의해서 데이터가 관리되는 경우도 있고, 데이터가 막 섞여있는 경우도 있다.

그리고 트리의 맨 끝에 더 이상 자식이 없는 노드를 "leaf" 잎사귀라고 부른다.

</br>

## Binary Tree 이진 트리

</br>

[![2023-04-18-9-37-35.png](https://i.postimg.cc/nzMpxf2G/2023-04-18-9-37-35.png)](https://postimg.cc/r06vGbvD)

</br>

노드가 하나 이상의 자식을 가지면 트리라고 부른다. 그 중에 자식 노드가 최대 2개까지만 붙는 트리를 이진트리, Binary Tree라고 부른다. 자식노드가 3개 붙은 트리를 Ternary Tree라고 하고, 노드에 자식노드가 세 개씩 붙는다. 그리고 자식노드가 4개씩 붙는 트리도 있다. 그 중에 가장 관심을 가지는 트리가 이진트리이다.

</br>

## Binary Search Tree 이진 검색 트리

</br>

[![2023-04-18-9-43-16.png](https://i.postimg.cc/3NVg1hSS/2023-04-18-9-43-16.png)](https://postimg.cc/vx7g8Jdf)

</br>

Binary Tree는 다른 조건없이 노드의 자식노드가 최대 2개씩만 붙어 있는 트리를 말한다.

Binary Search Tree는 그 안에 데이터가 왼쪽 노드와 그 이하 자식노드들은 현재 노드보다 작아야하고, 오른쪽 노드와 그 이하 자식노드들은 현재 노드보다 커야한다. 그래서 노드를 보고, 해당 노드 값보다 큰 값을 찾고자 하면 오른쪽에서 찾으면 되고, 작은 값을 찾고 싶으면 무조건 왼쪽에 가서 찾으면 된다.

오른쪽에 Binary Search Tree는 모든 값들이 노드들을 기준으로 나눠어져 있어서 어떤 값을 찾을 때는 두 갈래 길에서 선택해서 가다보면 그 값을 찾을 수 있지만, 왼쪽의 Binary Tree는 값을 비교하면서 원하는 값을 찾기 힘들다.

</br>

## Balance 밸런스

</br>

[![2023-04-18-9-49-03.png](https://i.postimg.cc/1X2dLf5D/2023-04-18-9-49-03.png)](https://postimg.cc/RJ1GtCt0)

</br>

트리에서 밸런스가 맞다 안맞다는 왼쪽과 오른쪽의 노드의 개수가 정확하게 일치해야 하는 것은 아니다. 그러나 오른쪽처럼 너무나 지나치게 치우쳐져 있지만 않으면 밸런스가 맞다고 표현한다.

</br>

[![2023-04-18-9-51-43.png](https://i.postimg.cc/CLKD2mWC/2023-04-18-9-51-43.png)](https://postimg.cc/vDpcgL8D)

</br>

밸런스가 맞는 대표적인 트리는 red-black tree 그리고 AVL tree가 있다.

</br>

## Complete Binary Tree 완전 이진 트리

</br>

[![2023-04-18-9-54-00.png](https://i.postimg.cc/prW04KH9/2023-04-18-9-54-00.png)](https://postimg.cc/Q9zkW9Vs)

</br>

완전 이진 트리는 모든 노드들이 레벨별로 왼쪽부터 채워져 있으면 완전 이진 트리이다. 좀 더 정확히 말하면, 트리를 만들다보면 레벨(계층)이 생기는데, 마지막 레벨을 제외한 모든 서브 트리의 레벨이 같아야 하고, 마지막 레벨은 왼쪽부터 채워져 있으면 완전 이진 트리이다.

왼쪽 트리를 보면 레벨이 다 맞는데, 마지막 레벨 중간이 안 채워져 있고, 맨 끝이 채워져있다. 이런 경우 왼쪽 트리는 완전 이진 트리가 아니다.

</br>

## Full Binary Tree

</br>

[![2023-04-18-9-58-37.png](https://i.postimg.cc/pXN7P5J6/2023-04-18-9-58-37.png)](https://postimg.cc/z3jpjBMC)

</br>

오른쪽 트리처럼 하나의 자식노드만 갖고 있는 노드가 하나도 없는 이진 트리를 Full Binary Tree라고 한다. Full Binary Tree가 되려면 노드가 자식노드를 안 가지려면 하나도 안가져야 하고, 가지려면 둘을 가져야 한다.

</br>

## Perfect Binary Tree

</br>

[![2023-04-18-10-02-25.png](https://i.postimg.cc/rpcRTjDw/2023-04-18-10-02-25.png)](https://postimg.cc/XrHYcwKR)

</br>

Perfect Binary Tree는 오른쪽 트리처럼 양쪽으로 빈 공간없이 모든 노드가 두 개의 자식을 가지고, 레벨도 정확하게 딱 떨어지는 상태이다. 완벽하게 피라미드 구조를 형성하고 있다.