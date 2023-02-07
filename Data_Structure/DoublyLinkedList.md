# Doubly linked list(이중 연결 리스트)

</br>

## 소개

doubly linked list의 핵심은 노드와 노드가 서로 연결되어 있다는 점이다. 아래 그림을 보면 단순 연결 리스트(linked list)와는 다르게 노드가 이전 노드(previous)와 다음 노드(next)로 구성되어 있다.

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2949.png)

</br>

이것의 가장 큰 장점은 양방향으로 연결되어 있기 때문에 노드를 탐색하는 방향이 양쪽으로 가능하다는 것이다.

</br>

## 장점

양방향 탐색의 가장 큰 장점은 특정 인덱스 위치의 엘리먼트를 가져올 때와 반복자를 이용해서 탐색할 때 드러난다.

</br>

## 인덱스의 데이터 가져오기

아래 그림을 보면 노드가 6개일 때 3번째 엘리먼트 이전은 처음부터 시작해서 `next`를 이용해서 탐색하고, 4번째 이후의 엘리먼트는 마지막 노드부터 `previous`를 이용해서 조회한다. 단순 연결 리스트가 최악의 경우 노드 전체를 탐색해야 했던 것에 비해서 양방향 연결 리스트는 탐색해야 하는 엘리먼트가 반으로 줄어 든다.

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2976.png)

</br>

## 노드 탐색하기

단방향 연결 리스트는 다음 노드의 탐색만 가능했던 것에 비해서 이중 연결 리스트의 경우 앞뒤로 탐색이 가능하다. 상황에 따라 탐색의 방향이 바뀌어야 하는 경우라면 이중 연결 리스트를 사용한다.

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2968.png)

</br>

## 단점

우선 이전 노드를 지정하기 위한 변수를 하나 더 사용해야 한다. 그래서 메모리를 더 많이 사용한다. 또 구현이 조금 더 복잡해진다는 단점도 있다. 하지만 장점이 크기 때문에 현실에서 사용하는 연결 리스트는 대부분 이중 연결 리스트이다. 아래는 양방향의 연결을 만들기 위해서 치뤄야 하는 대가라고 할 수 있다. 거의 비슷하지만 약간의 작업이 더 추가 되었다.

</br>

## 노드의 추가

단순 연결 리스트와 거의 비슷하다. 중요한 차이점은 양방향으로 연결을 해야 한다는 점이다. 새로운 노드(25)를 기존의 노드(20, 30)와 연결하는 방법만 살펴보겠다.

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2958.png)

</br>

25의 다음 노드로 30을 연결한다.

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2959.png)

</br>

30의 이전 노드로 25를 연결한다.

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2960.png)

</br>

20의 다음 노드로 25를 지정하다.

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2961.png)

</br>

25의 이전 노드로 20을 지정한다.

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2962.png)

</br>

노드의 추가가 끝난다.

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2963.png)

</br>

## 노드의 제거

노드를 제거하는 방법도 거의 비슷하다.

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2969.png)

</br>

삭제하려는 노드의 이전 노드(20)을 찾는다.

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2970.png)

</br>

삭제하려는 노드(30)도 찾는다.

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2971.png)

</br>

삭제하려는 노드의 다음 노드(40)도 찾는다.

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2972.png)

</br>

30을 삭제한다.

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2973.png)

</br>

20의 다음 노드로 40을 지정한다.

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2974.png)

</br>

40의 이전 노드로 20을 지정한다.

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2975.png)

</br>

삭제가 완료 되었다.