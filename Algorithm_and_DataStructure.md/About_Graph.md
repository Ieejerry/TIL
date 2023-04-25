# 그래프(Graph)에 대해서

</br>

## tree

</br>

[![2023-04-24-9-15-14.png](https://i.postimg.cc/nch47m9d/2023-04-24-9-15-14.png)](https://postimg.cc/4njHRm5t)

</br>

tree의 특성은 root가 있고, 아래로 자식 노드들이 있고, 노드를 연결하는 edge가 있고, edge의 방향은 위에서 아래로, 들어오는 곳은 하나고, 나가는 곳은 여러 개가 될 수 있다.

</br>

## Graph

</br>

[![2023-04-24-9-16-12.png](https://i.postimg.cc/q7shWBCh/2023-04-24-9-16-12.png)](https://postimg.cc/t1g4xjkp)

</br>

Graph의 특성은 edge의 방향을 위아래로 조정할 수도 있고, 심지어 방향을 아예 안 가질 수도 있다. 들어오는 곳이 여러 개가 될 수도 있고, 옆에 노드와 서로 주고 받기도 하며, edge가 돌아서 자기 자신을 가리키기도 하고, 그 안에 돌고 돌아서 서클을 만들기도 하고, 그래서 root도 없어지는 복잡한 구조를 가지고 있다. graph는 tree와 같은 제약이 없다.

**tree는 graph의 한 형태이다.**

**tree는 root가 있고, 들어오는 곳이 한 개이고, 사이클이 없는 아래로만 흐르는 방향 그래프이다.**

</br>

### Graph의 특성

</br>

[![2023-04-24-9-18-17.png](https://i.postimg.cc/6pwynJPB/2023-04-24-9-18-17.png)](https://postimg.cc/bsCyfM85)

</br>

왼쪽 그래프는 연결선에 화살표가 있고, 오른쪽 그래프는 연결선에 화살표가 없다. 그래프는 방향이 있을 수도 있고, 없을 수도 있다. 그래서 방향이 있는 그래프는 Directed 그래프, 방향이 없는 그래프는 Undirected 그래프라고 한다. tree는 항상 위에서 아래로 흐르기 때문에 Directed 그래프가 된다.

방향 그래프에는 Self edge라고, 자기 자신을 가리키는 경우도 있다.

</br>

[![2023-04-24-9-26-25.png](https://i.postimg.cc/Y2zVMTWJ/2023-04-24-9-26-25.png)](https://postimg.cc/rzzg9ngJ)

</br>

그래프는 노드들이 그래프 내부에 서클을 만드는 경우가 있고, 아닌 경우가 있는데, 하나 이상의 서클이 있는 그래프를 Cyclic 그래프라고 하고, 서클이 하나도 없는 그래프를 Acyclic 그래프라고 한다.

</br>

## 그래프를 표현하는 방법

- Adjacency Matrix
- Adjacency List

그래프를 표현하는 방법에는 위의 두 가지 방법이 있는데, Adjacency Matrix는 이차원 배열에다가 표현하는 방법이고, Adjacency List는 배열에 노드들을 나열하고 관계를 LinkedList로 표현하는 방법이다.

</br>

### Adjacency Matrix

</br>

[![2023-04-24-9-31-48.png](https://i.postimg.cc/j5ZFQ7tR/2023-04-24-9-31-48.png)](https://postimg.cc/hzQsKhXY)

</br>

Adjacency Matrix는 그래프를 표에다가 표현하는 방법이다. 서로 연결된 노드들은 1, 연결되어 있지 않으면 0으로 2차원 배열방은 채우는 구조이다.

</br>

### Adjacency List

</br>

[![2023-04-24-9-37-23.png](https://i.postimg.cc/dVXFKgy8/2023-04-24-9-37-23.png)](https://postimg.cc/75gd3sX6)

</br>

Adjacency List 표현 방법은, 배열방에다가 모든 노드들을 넣고, 각 배열방에 있는 해당 노드와 인접한 노드들을 LinkedList로 순서 상관없이 나열해서 저장하는 방법이다.

Adjacency List에서 노드들은 관계를 나타낸다. edge의 갯수를 m이라고 할 때, 총 노드의 갯수는 2m개가 생성된다.