# 리스트(List)

</br>

<a href="https://ibb.co/mBPWbCP"><img src="https://i.ibb.co/9vd5c9d/00001.jpg" alt="00001" border="0"></a>

</br>

리스트(List)는 데이터 구조의 하나로 여러 개의 값을 저장하기 위한 구조이다.

</br>

<a href="https://ibb.co/g9B0GRN"><img src="https://i.ibb.co/mTMnmck/Kakao-Talk-20230227-214954295.jpg" alt="Kakao-Talk-20230227-214954295" border="0"></a>

</br>

데이터와 포인터가 한 쌍으로 구성된 것이 특징으로, 포인터가 다음 데이터의 메모리 위치를 가리킨다.

</br>

<a href="https://ibb.co/b1f5bQB"><img src="https://i.ibb.co/MnXkBZV/Kakao-Talk-20230227-214954295-01.jpg" alt="Kakao-Talk-20230227-214954295-01" border="0"></a>

</br>

<a href="https://ibb.co/Y8brTJw"><img src="https://i.ibb.co/d67hJXx/Kakao-Talk-20230227-214954295-02.jpg" alt="Kakao-Talk-20230227-214954295-02" border="0"></a>

</br>

리스트에선 데이터가 메모리상의 떨어진 영역에 흩어져서 저장된다.

</br>

<a href="https://ibb.co/mCgLxRq"><img src="https://i.ibb.co/DDTxq1C/Kakao-Talk-20230227-214954295-03.jpg" alt="Kakao-Talk-20230227-214954295-03" border="0"></a>

</br>

<a href="https://ibb.co/MD88zCB"><img src="https://i.ibb.co/0jBB0Gs/Kakao-Talk-20230227-214954295-04.jpg" alt="Kakao-Talk-20230227-214954295-04" border="0"></a>

</br>

<a href="https://ibb.co/2dz8vS9"><img src="https://i.ibb.co/pdHWfQ7/Kakao-Talk-20230227-214954295-05.jpg" alt="Kakao-Talk-20230227-214954295-05" border="0"></a>

</br>

<a href="https://ibb.co/HVfnxSs"><img src="https://i.ibb.co/1Lt8dg5/Kakao-Talk-20230227-214954295-06.jpg" alt="Kakao-Talk-20230227-214954295-06" border="0"></a>

</br>

<a href="https://ibb.co/TK7xrh7"><img src="https://i.ibb.co/YD1Fbj1/Kakao-Talk-20230227-214954295-07.jpg" alt="Kakao-Talk-20230227-214954295-07" border="0"></a>

</br>

흩어져 저장돼 있으므로 포인터를 처음부터 순서대로 따라가야만 원하는 데이터에 접근할 수 있다.

</br>

<a href="https://ibb.co/j54jcrb"><img src="https://i.ibb.co/7zy0w1j/Kakao-Talk-20230227-214954295-08.jpg" alt="Kakao-Talk-20230227-214954295-08" border="0"></a>

</br>

<a href="https://ibb.co/h2SVF5Y"><img src="https://i.ibb.co/0YxryNs/Kakao-Talk-20230227-214954295-09.jpg" alt="Kakao-Talk-20230227-214954295-09" border="0"></a>

</br>

<a href="https://ibb.co/MS4HGD5"><img src="https://i.ibb.co/Sy8gdX7/Kakao-Talk-20230227-214954295-10.jpg" alt="Kakao-Talk-20230227-214954295-10" border="0"></a>

</br>

데이터를 추가는 추가할 위치의 앞뒤 포인터를 변경만 하면 되므로 간단하다고 볼 수 있다.

</br>

## 리스트의 특징

리스트의 데이터를 노드(Node)라고 부르는데, 노드에는 데이터가 저장되는 데이터필드, 포인터 즉, 다음 노드의 정보가 저장되는 링크필드로 이루어져 있다.

리스트의 장점은 데이터 추가 및 삭제가 매우 빠르다는 것이다. 왜냐하면 다음 노드의 정보가 저장되어 있는 링크필드의 값을 바꿔주기만 하면 되기 때문이다.

단점은 메모리를 많이 잡아먹는다는 것이다. 왜냐하면 데이터가 저장되는 데이터필드 뿐만 아니라 다음 노드의 정보를 저장하는 링크필드까지 저장해야하기 때문이가. 그리고 데이터 조회가 느리다. 리스트에서 원하는 데이터를 찾으려면 처음 노드부터 찾는 노드까지 순차적으로 하나씩 찾아야하기 때문이다.

이러한 단점을 보안하기 위해 이전 노드의 정보까지 저장하는 "DoublyLinkedList"가 있는데 한 노드의 앞뒤로 링크필드가 있어 이전 노드의 정보와 다음 노드의 정보를 저장한다. 그래서 조회를 할 경우, 조회하고자 하는 데이터의 index가 리스트 크기의 절반보다 크면 뒤에서 부터 역순으로 찾고, 절반보다 작으면 앞에서 부터 순차적으로 찾는다. 이렇게 함으로써 조회하는 속도를 절반쯤 줄일 수 있다. 하지만 이전 노드의 정보를 추가적으로 저장해야하기 때문에 메모리를 더 많이 잡아먹는다.