# LinkedList

</br>

## 소개

`LinkedList`는 `ArrayList`와는 다르게 엘리먼트와 엘리먼트 간의 연결(link)을 이용해서 리스트를 구현한 것이다. 그래서 이름도 linked list이다. 그렇게 보면 linked list에서 가장 중요한 것은 연결이 무엇인가를 파악하는 것이라고 할 수 있다.

</br>

### 메모리

먼저 컴퓨터가 동작하는 원리에 대해서 조금 살펴보겠다. 컴퓨터에는 3가지 중요한 부품이 있다. CPU와 메모리(memory) 그리고 스토리지(storage)이다.

메모리는 아래와 같이 생겼다. 보통 RAM이라고 부른다.

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2901.png)

</br>

스토리지는 아래와 같은 것들이 있다. HDD와 SSD 이다.

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2927.png)

</br>

메모리는 속도가 매우 빠르다. 반대로 용량이 작다. 그리고 전기를 끄면 데이터가 사라지는 속성을 가지고 있다. 반면에 스토리지는 속도가 느리다. 하지만 용량이 훨씬 크고 전기를 꺼도 데이터가 남아 있다. 

이런 이유로 데이터는 기본적으로 스토리지에 저장된다. 하지만 스토리지는 매우 느리기 때문에 CPU와 함께 일을 하기에는 속도면에서 부족하다. 그래서 어떤 프로그램을 실행하면 그 프로그램과 데이터는 메모리로 옮겨진다. CPU는 메모리에 로드된 데이터를 이용해서 여러가지 일을 하게 된다.

이걸 그림으로 표시하면 아래와 같다.

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2917.png)

</br>

그러므로 실행속도를 결정하는 것은 대체로 메모리이다. 데이터 스트럭쳐를 배우는 이유는 메모리의 효율적인 사용이라고 할 수 있다.

</br>

## 메모리의 구조

메모리는 건물에 비유할 수 있다. 아래 그림은 배열을 사용하는 것과 linked list를 사용하는 것을 비유해서 보여주고 있다. 어떤 한 회사가 한 건물의 일부를 임대해서 사용한다고 비유하겠다.

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2903.png)

</br>

### ArrayList

첫번째 회사는 모든 직원이 한곳에 모여있어야 한다는 철학이 있기 때문에 사무실이 모여있다. 배열은 건물을 이런 식으로 사용하는 것과 비슷하다. 만약 회사가 성장해서 사무실이 좁아지면 더 이상 새로운 직원을 뽑을 수 없다. 붙어있는 공간이 없기 때문이다. 만약 더 많은 공간이 필요하다면 더 많은 사람을 수용할 수 있는 공간을 찾아서 전체가 이사해야 한다.

</br>

### LinkedList

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2928.png)

</br>

`linkedlist`는 한 건물 내에서 한 회사가 임대한 사무실이 서로 떨어져 있다. 덕분에 직원이 늘어도 큰 걱정이 없다. 건물에서 비어있는 곳 아무데나 임대해서 들어가면 된다. 그런데 방문자가 사무실을 찾는 방법이 좀 비효율적이다. 위의 그림에 있는 방문자가 3번째 사무실을 찾아가려면 우선 첫 번째 화살표의 사무실을 찾아가야 한다. 이 사무실의 직원에게 다음 사무실이 어딘지 물어보고, 그럼 알려주는 사무실로 이동 한 후에 다시 물어봐서 그다음 사무실로 이동해야 한다.

이렇게 물어물어 사무실을 찾아가야 하는 방식이 `LinkedList`이다. 그래서 `LinkedList`에서는 몇 번째 엘리먼트를 찾는 것이 느리다.

반면에 `ArrayList`는 엘리먼트가 같은 곳에 모여있다. 만약에 3번째 자리로 가고 싶다면 한 번에 3번째 방으로 갈 수 있다. 찾고자 하는 사무실이 몇 번째에 있는지 알고 있다면 `ArrayList`는 매우 빠르다.

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2929.png)

</br>

### 연결

배열과는 다르게 `LinkList`는 그 위치가 흩어져 있기 때문에 서로 연결되어 있어야 한다. 바로 그런 점에서 연결이라는 이름을 갖게 되었다.

`ArrayList`에서는 엘리먼트라는 이름을 사용했지만 `LinkedList`와 같이 연결된 엘리먼트들은 노드(node, 마디, 교점의 의미) 혹은 버텍스(vertex, 정점, 꼭지점의 의미)라고 부른다. 이런 용어들은 연결성이 강조된 표현이다.

</br>

## 구조

리스트는 노드(엘리먼트)들의 모임이다. 따라서 내부적으로 노드를 가지고 있어야 한다. `ArrayList`의 경우 엘리먼트가 배열의 엘리먼트이다. `LinkedList`는 배열 대신에 다른 구조를 사용한다.

노드는 최소한 두 가지 정보를 알고 있어야 한다. 노드의 값과 다음 노드이다. 각각의 노드가 다음 노드를 알고 있기 때문에 하나의 연결된 값의 모임을 만들 수 있다. 아래 그림은 `LinkedList`의 구조를 보여준다.

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2939.png)

</br>

이것을 구현하는 방법은 여러가지이다. 만약 사용 언어가 C라면 구조체, 자바와 같은 객체지향 언어라면 객체에 데이터 필드와 링크 필드를 만든다. 보통 데이터 필드는 `value`라는 이름의 변수, 링크 필드는 `next` 변수를 사용한다. `value`에는 노드의 값이 저장되고, `next`에는 다음 노드의 포인터나 참조값을 저장해서 노드와 노드를 연결시키는 방법을 사용한다.

</br>

### Head

위의 그림을 보면 `head`라는 것이 있다. 건물의 비유를 다시 사용해보겠다. 건물에 들어가려면 출입문을 찾아야 한다. 리스트를 하나의 건물로 비유하자면 출입문에 해당하는 것이 `head`이다. `LinkedList`를 사용하기 위해서는 이 `head`가 가리키는 첫번째 노드를 찾아야 한다.

</br>

## 데이터의 추가

</br>

### 시작부분에 추가

노드를 첫 번째 위치에 추가해보겠다.

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2943.png)

</br>

우선 새로운 노드를 생성한다.

</br>

``` java
Vertex temp = new Vertex(input);
```

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2944.png)

</br>

새로운 노드의 다음 노드로 첫번째 노드를 가리킨다.

</br>

``` java
temp.next = head;
```

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2945.png)

</br>

새로 만들어진 노드가 첫번째 노드가 되도록 `head`의 값을 변경한다.

</br>

``` java
head = temp;
```

</br>

위 작업에 대한 전체코드이다.

</br>

``` java
Vertex temp = new Vertex(input);
temp.next = head;
head = temp;
```

</br>

## 중간에 추가

3번째 자리(인덱스 2)에 90을 추가해보겠다.

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2930.png)

</br>

3번째 자리는 붉은 화살표가 표시된 부분이다. 즉 6과 23 사이에 90을 위치시키는 것이다. 우선 3번째 자리를 찾아야 한다.

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2919.png)

</br>

`head`를 참조해서 첫번째 노드를 찾았다.

</br>

``` java
Vertex temp1 = head;
```

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2920.png)

</br>

23의 자리에 새로운 노드를 위치시키기 위해서는 6을 알고 있어야 한다. 6의 `next`로 새로운 노드를 지정해야 하기 때문이다. 아래는 6을 `temp1`으로 지정하기 위한 반복문이다.

</br>

``` java
//현재 k의 값은 2
while (--k != 0)
  temp1 = temp1.next;
```

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2921.png)

</br>

6의 `next`를 이용해서 23을 찾아서 `temp2`로 지정한다.

</br>

``` java
Vertex temp2 = temp1.next;
```

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2922.png)

</br>

값이 90인 새로운 노드를 생성한다.

</br>

``` java
Vertex newVertex = new Vertex(input);
```

</br>

6의 다음 노드로 새로운 노드를 지정한다.

</br>

``` java
temp1.next = newVertex;
```

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2924.png)

</br>

새로운 노드의 다음 노드로 23번을 지정한다.

</br>

``` java
newVertex.next = temp2;
```

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2926.png)

</br>

이렇게 해서 90을 3번째 자리에 위치시켰다.

이것이 `arraylist`와 `LinkedList`의 핵심적인 차이점이다. 배열의 경우는 엘리먼트를 중간에 추가/삭제할 경우 해당 엘리먼트의 뒤에 있는 모든 엘리먼트의 자리 이동이 필요하다. 그래서 배열은 추가/삭제가 느리다. 반대로 `LinkedList`의 경우 추가/삭제가 될 엘리먼트의 이전, 이후 노드의 참조값(next)만 변경하면 되기 때문에 속도가 빠르다.

</br>

### 전체 코드

``` java
Vertex temp1 = head;
while (--k != 0)
  temp1 = temp1.next;
Vertex temp2 = temp1.next;
Vertex newVertex = new Vertex(input);
temp1.next = newVertex;
newVertex.next = temp2;
```

</br>

## 데이터의 제거

데이터를 제거하는 것도 추가하는 것과 비슷하다. 아래 리스트에서 세번째 노드(인덱스 2)를 제거하는 과정을 알아보겠다.

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2932.png)

</br>

우선 `head`를 이용해서 첫번째 노드를 찾는다.

</br>

``` java
Vertex cur = head;
```

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2933.png)

</br>

두번째 노드로 이동한다.

</br>

``` java
//k = 2
while (--k != 0)
  cur = cur.next;
```

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2934.png)

</br>

세번째 노드를 찾았다.

</br>

``` java
Vertex tobedeleted = cur.next;
```

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2935.png)

</br>

두번째 노드의 `next`를 23으로 변경한다. 이제 90을 지워도 된다.

</br>

``` java
cur.next = cur.next.next;
```

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2936.png)

</br>

90을 삭제해서 메모리에서 제거한다.

</br>

``` java
delete tobedeleted;
```

</br>

### 전체 코드

``` java
Vertex cur = head;
while (--k != 0)
  cur = cur.next;
Vertex tobedeleted = cur.next;
cur.next = cur.next.next;
delete tobedeleted;
```

</br>

## 인덱스를 이용한 데이터 조회

인덱스를 이용해서 데이터를 조회할 때 `LinkedList`는 `head`가 가리키는 노드부터 시작해서 순차적으로 노드를 찾아가는 과정을 거쳐야 한다. 만약 찾고자 하는 엘리먼트가 가장 끝에 있다면 모든 노드를 탐색해야 한다.

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2937.png)

</br>

반면에 `Array`를 이용해서 리스트를 구현하면 인덱스를 이용해서 해당 엘리먼트에 바로 접근 할 수 있기 때문에 매우 빠르다.

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2938.png)

</br>

## trade off

트래이드 오프는 어떤 특성이 좋아지면 다른 특성이 나뻐지는 상황을 의미한다. `ArrayList`와 `LinkedList`는 트레이드 오프의 좋은 사례라고 할 수 있다.

</br>

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/1335/2885.png)