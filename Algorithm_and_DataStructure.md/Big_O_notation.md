# 빅오 표기법(Big-O notation)

</br>

## 빅오(Big-O)란?

- 빅오(Big-O)는 알고리즘의 성능을 수학적으로 표현해주는 표기법이다.
- 이 표기법으로 알고리즘의 시간과 공간복잡도를 표현할 수 있다.
- 빅오 표기법은 알고리즘의 실제 러닝타임을 표시하기보단 데이터나 사용자 증가율에 따른 알고리즘 성능을 예측하는 것이 목표이기 때문에 상수와 같은 숫자들은 모두 1이 된다.

</br>

## 빅오 표기법

</br>

### O(1) 알고리즘

</br>

O(1) 알고리즘은 입력 데이터의 크기에 상관없이 언제나 일정한 시간이 걸리는 알고리즘이다.

</br>

[![2023-04-03-10-46-19.png](https://i.postimg.cc/mrK4CNt1/2023-04-03-10-46-19.png)](https://postimg.cc/cK7PN37d)

</br>

위의 함수를 보면 첫 번째 배열의 값이 0인지 확인하는데, 인자로 받는 배열이 얼마나 큰지에 상관없이 언제나 일정한 속도로 결과를 반환한다.

이러한 경우에 이 알고리즘을 **O(1)의 시간복잡도를 가진다.** 라고 표현한다.

</br>

[![2023-04-03-10-52-44.png](https://i.postimg.cc/bwWw821g/2023-04-03-10-52-44.png)](https://postimg.cc/ZWPSxn7v)

</br>

O(1) 알고리즘을 그래프로 표현해보면, 가로축이 데이터의 크기이고, 세로축을 처리시간이라고 할 때, 데이터가 증가함에 따라 성능에 변함이 없다.

</br>

### O(n) 알고리즘

O(n) 알고리즘은 입력 데이터의 크기에 비례해서 처리시간이 걸리는 알고리즘을 표현할 때 사용한다.

</br>

[![2023-04-03-10-56-00.png](https://i.postimg.cc/HxPSPHqr/2023-04-03-10-56-00.png)](https://postimg.cc/2bhF1p8Y)

</br>

위의 함수는 n개의 데이터를 받으면, n번 루프를 도니깐 n이 하나 늘어날 때마다, 처리가 한 번씩 늘어나서 n의 크기만큼 처리시간이 걸리게 된다.

</br>

[![2023-04-03-10-58-22.png](https://i.postimg.cc/vBR71TwL/2023-04-03-10-58-22.png)](https://postimg.cc/jWXnms5L)

</br>

O(n) 알고리즘을 그래프로 표현해보면, 데이터가 증가함에 따라 비례해서 처리시간도 같이 증가한다. 언제나 데이터와 시간이 같은 비율로 증가하기 때문에 그래프는 직선으로 표현이 된다.

</br>

### O(n<sup>2</sup>) 알고리즘

</br>

[![2023-04-03-11-08-17.png](https://i.postimg.cc/y8RQNwwR/2023-04-03-11-08-17.png)](https://postimg.cc/871BKnkk)

</br>

위의 함수를 보면, n을 돌리면서, 그 안에서 n으로 루프를 또 돌릴 때, n<sup>2</sup>가 된다.

</br>

[![2023-04-03-11-10-03.png](https://i.postimg.cc/BvLKs0kW/2023-04-03-11-10-03.png)](https://postimg.cc/LqSXBrmv)

</br>

그래서 n개의 데이터를 받으면, 첫 번째 루프에서 n번 돌면서, 각각의 엘리먼트에서 n번씩 또 도니깐, 

</br>

[![2023-04-03-11-12-35.png](https://i.postimg.cc/bvzBFmB2/2023-04-03-11-12-35.png)](https://postimg.cc/4YSPYQZJ)

</br>

처리횟수가 n을 가로, 세로 길이로 가지는 면적만큼 되는 것이다. 그러면 n이 하나 늘어날 때마다 아래 한 줄, 오른쪽 한 줄 n만큼 또 주르륵 붙으니깐, 데이터가 커지면 커질수록 처리시간에 부담도 커진다.

</br>

[![2023-04-03-11-15-45.png](https://i.postimg.cc/wxVZD84Y/2023-04-03-11-15-45.png)](https://postimg.cc/qgN1dYd1)

</br>

O(n<sup>2</sup>)를 그래프로 보면, 다음과 같이 처음에는 조금씩 상승하다가, 나중에 가면 하나 추가할 때마다, 그래프가 수직상승한다.

</br>

### O(nm) 알고리즘

</br>

[![2023-04-03-11-18-24.png](https://i.postimg.cc/SQvLBgJz/2023-04-03-11-18-24.png)](https://postimg.cc/w3DsJc56)

</br>

위의 코드를 보면, O(n<sup>2</sup>)와 비슷하지만, n을 두 번 돌리는게 아니라, m을 n만큼 돌리는 것이다.

O(n<sup>2</sup>)와 달리 n은 크고, m은 작을 수 있기 때문에, 변수가 다르다면 빅오 표기법에도 반드시 다르게 표기해줘야 한다.

</br>

[![2023-04-03-11-22-03.png](https://i.postimg.cc/Fsv3czCD/2023-04-03-11-22-03.png)](https://postimg.cc/ThkKvd6D)

</br>

O(nm)도 O(n<sup>2</sup>)와 같이 데이터가 증가할수록 그래프가 점점 수직에 가까운 모양이 된다.

</br>

### O(n<sup>3</sup>) 알고리즘

</br>

[![2023-04-03-11-24-07.png](https://i.postimg.cc/FRFw7h5R/2023-04-03-11-24-07.png)](https://postimg.cc/DWDxNkzk)

</br>

n<sup>2</sup>에 n을 한 번 더 돌리면, n<sup>3</sup>이 된다. 위의 코드에서 보는 것과 같이 루프를 n을 가지고 삼중으로 돌리면 n<sup>3</sup>이 된다.

</br>

[![2023-04-03-11-26-29.png](https://i.postimg.cc/FRf8jDz5/2023-04-03-11-26-29.png)](https://postimg.cc/Vr8Kw9XD)

</br>

n<sup>3</sup>은 n<sup>2</sup>에서 n을 한 번 더 돌리니깐, 큐브 모양이 된다.

</br>

[![2023-04-03-11-27-55.png](https://i.postimg.cc/qBsQW99D/2023-04-03-11-27-55.png)](https://postimg.cc/K4YnMsct)

</br>

n<sup>3</sup>은 n<sup>2</sup>와 비슷한 양상을 보이지만, 데이터가 늘어남에 따라 가로, 세로, 높이까지 더해지다보니깐, 데이터가 증가함에 따라 더욱 더 급격하게 처리시간이 늘어나는 걸 그래프를 통해 확인할 수 있다.

</br>

### O(2<sup>n</sup>) 알고리즘

</br>

피보나치 수열은 1부터 시작해서 

</br>

[![2023-04-03-11-35-46.png](https://i.postimg.cc/HxH7qsc6/2023-04-03-11-35-46.png)](https://postimg.cc/Z97R3mLN)

</br>

한 면을 기준으로 정사각형을 만든다.

</br>

[![2023-04-03-11-36-51.png](https://i.postimg.cc/3r0zW8dL/2023-04-03-11-36-51.png)](https://postimg.cc/pyxs6tQ8)

</br>

1인 정사각형 두 개가 합쳐져서 큰 면이 2인 직사각형이 만들어지고, 한 면이 2인 정사격형을 추가적으로 만든다.

</br>

[![2023-04-03-11-39-12.png](https://i.postimg.cc/HnSrfwX2/2023-04-03-11-39-12.png)](https://postimg.cc/4H94ch87)

</br>

이제 큰 면이 3이 되었기 때문에 한 면이 3인 정사각형을 추가적으로 만든다.

</br>

[![2023-04-03-11-41-35.png](https://i.postimg.cc/KjXb4RF2/2023-04-03-11-41-35.png)](https://postimg.cc/7GNdWPfs)

</br>

이제 큰 면이 5가 되었기 때문에, 한 면이 5인 정사각형을 추가적으로 만든다.

</br>

[![2023-04-03-11-42-32.png](https://i.postimg.cc/bNzMgQm5/2023-04-03-11-42-32.png)](https://postimg.cc/NLzpfrq8)

</br>

또 큰 면이 8이 되었기 때문에, 한 면이 8인 정사각형을 추가적으로 만든다.

</br>

[![2023-04-03-11-43-43.png](https://i.postimg.cc/kMVFmDB5/2023-04-03-11-43-43.png)](https://postimg.cc/QV3Wg8gL)

</br>

그러면 이렇게 신비로운 기하학의 황금비율 피보나치의 나선형이 그려진다.

</br>

[![2023-04-03-11-44-54.png](https://i.postimg.cc/wMH607rk/2023-04-03-11-44-54.png)](https://postimg.cc/N9Jq0fBy)

</br>

그러면 이제 수학적으로 접근해보면,

</br>

[![2023-04-03-11-48-06.png](https://i.postimg.cc/zXKQqxV3/2023-04-03-11-48-06.png)](https://postimg.cc/7fP9VM1y)

</br>

피보나치 수열은 1부터 시작해서, 1의 다른 한 면은 1이니깐, 1을 한 번 더 써주고, 앞의 1을 더해서 2를 써준다. 다음에는 1과 2를 더해서 3을 써준다. 바로 앞에 숫자 2와 3을 더해서 5를 써주고, 다음에는 3과 5를 더해서 8을 써준다.

</br>

[![2023-04-03-11-49-41.png](https://i.postimg.cc/65fhHg8V/2023-04-03-11-49-41.png)](https://postimg.cc/gnrRjMqr)

</br>

피보나치 수열을 구현한 코드를 재귀함수를 이용해서 구현하면, 위의 코드가 되는데, 함수를 호출할 때마다 바로 전의 숫자와 전전 숫자를 알아야 더할 수 있기 때문에 해당 숫자를 알아내기 위해서 하나 뺀 숫자를 가지고 한 번 재귀호출을 하고, 두 개 뺀 숫자를 가지고, 한 번 더 재귀호출을 한다.

</br>

[![2023-04-03-11-52-37.png](https://i.postimg.cc/QMmGh0Yc/2023-04-03-11-52-37.png)](https://postimg.cc/sBM0J9r2)

</br>

이렇게 매번 함수가 호출 될 때마다 두 번씩 또 호출을 하는데, 그걸 트리의 높이만큼 반복한다.

</br>

[![2023-04-03-11-54-51.png](https://i.postimg.cc/dt55sgJs/2023-04-03-11-54-51.png)](https://postimg.cc/gn6V4SwQ)

</br>

그래프를 보면, n<sup>2</sup>이나 n<sup>3</sup>보다도 데이터 증가에 따라 처리시간이 현저하게 늘어나는 것을 확인할 수 있다.

그 밖에 m개씩 n번 늘어나는 알고리즘을 표현할 때는 2 대신에 m을 넣어 O(m<sup>n</sup>)로 표현하면 된다.

</br>

### O(log n) 알고리즘

O(log n)을 살펴보겠다.

</br>

[![2023-04-04-7-56-23.png](https://i.postimg.cc/vZhGbH6B/2023-04-04-7-56-23.png)](https://postimg.cc/SnnBG4dF)

</br>

O(log n)의 대표적인 알고리즘은 이진 검색이다. Ascending으로 정렬된 Array 안에서

</br>

[![2023-04-04-7-59-32.png](https://i.postimg.cc/QVLd94Xd/2023-04-04-7-59-32.png)](https://postimg.cc/K3N2C5k6)

</br>

6을 한번 찾아보겠다. 정렬이 되어있기 때문에 이진 검색을 하려면

</br>

[![2023-04-04-8-01-15.png](https://i.postimg.cc/1599TqfT/2023-04-04-8-01-15.png)](https://postimg.cc/Jt2VHt3c)

</br>

우선 가운데 값을 찾아서 key값과 비교한다. key값이 더 크기 때문에 가운데 값보다 오른쪽에 있다는 뜻이다. 

</br>

[![2023-04-04-8-02-16.png](https://i.postimg.cc/rmJHtKM0/2023-04-04-8-02-16.png)](https://postimg.cc/k62s0MVq)

</br>

그러면 앞에 데이터들은 더 이상 볼 필요가 없다.

</br>

[![2023-04-04-8-03-45.png](https://i.postimg.cc/GmLxHq9Q/2023-04-04-8-03-45.png)](https://postimg.cc/PP7w7bWp)

</br>

뒤쪽에 데이터 중 다시 중간값을 찾아서 key값과 비교한다.

</br>

[![2023-04-04-8-05-34.png](https://i.postimg.cc/hj550NQc/2023-04-04-8-05-34.png)](https://postimg.cc/Fd0prWxB)

</br>

key값이 가운데 값보다 작기 때문에, 앞에쪽 있다는 뜻이고, 그러면 뒤쪽 데이터는 필요가 없어진다. 이제 앞쪽을 보니 찾는 데이터와 남은 데이터가 일치한다.

이렇게 한 번 처리가 진행 될 때마다 검색해야 하는 데이터의 양이 절반씩 줄어드는 알고리즘을 O(log n) 알고리즘이라고 한다.

</br>

[![2023-04-04-8-11-04.png](https://i.postimg.cc/vmqpT4zP/2023-04-04-8-11-04.png)](https://postimg.cc/wtNWbTnJ)

</br>

이진 검색의 알고리즘을 구현하면 위의 코드와 같다. 처음 호출될 때는 시작번호는 0 끝번호는 배열의 맨 마지막 값이 된다. 주어진 범위에 중간값을 찾는다. key값이 중간값보다 작으면 중간값 바로 전까지 범위를 조정하여 다시 호출한다. key값이 중간값보다 큰 경우에는 중간값 다음부터 맨 마지막 값까지 범위를 조정하여 다시 호출한다.

이렇게 한 번 함수가 호출될 떄마다 중간값을 기준으로 절반은 검색 영역에서 제외시켜버리기 때문에 순차 검색이랑 비교해서 속도가 현저하게 빠르다.

</br>

[![2023-04-04-8-16-41.png](https://i.postimg.cc/8zrHMjNK/2023-04-04-8-16-41.png)](https://postimg.cc/87NMVkFM)

</br>

그래프를 보면 O(log n)이 O(n)보다도 훨씬 시간이 적게 든다. 그리고 데이터가 증가해도 성능이 크게 차이나지 않는다.

</br>

### O(sqrt(n))

</br>

$\sqrt{100}$ = 10이다. 왜냐하면 100 = 10 * 10이기 때문이다.   
$\sqrt{9}$ = 3이다. 9 = 3 * 3이기 때문이다.

</br>

[![2023-04-04-8-26-08.png](https://i.postimg.cc/PJMt6mYt/2023-04-04-8-26-08.png)](https://postimg.cc/ctryCtFj)

</br>

예를 들어, n이 4라면 n을 정사각형에 채우면

</br>

[![2023-04-04-8-27-25.png](https://i.postimg.cc/c46jkRQX/2023-04-04-8-27-25.png)](https://postimg.cc/9r5Jrqg7)

</br>

맨 위에 한 줄이 제곱근이 된다.

</br>

[![2023-04-04-8-29-02.png](https://i.postimg.cc/cCPcbnSb/2023-04-04-8-29-02.png)](https://postimg.cc/2LFvq33Q)

</br>

n이 9라면 마찬가지로 9개의 아이템을 정사각형으로 채우고

</br>

[![2023-04-04-8-30-41.png](https://i.postimg.cc/P5sgLLwy/2023-04-04-8-30-41.png)](https://postimg.cc/svm6qgKG)

</br>

맨 위에 한 줄이 제곱근이 된다.

</br>

[![2023-04-04-8-32-10.png](https://i.postimg.cc/NFwgQNB8/2023-04-04-8-32-10.png)](https://postimg.cc/JDPwq5yt)

</br>

n이 16이라면 마찬가지로 정사각형에 n을 다 채우고

</br>

[![2023-04-04-8-37-58.png](https://i.postimg.cc/xC7Sd6Qp/2023-04-04-8-37-58.png)](https://postimg.cc/r0SHnCK5)

</br>

맨 위에 한 줄만 돌리는 알고리즘을 빅오 표기법으로 하면 O(sqrt(n))이다.

</br>

## 빅오 표기법에서 중요한 점

</br>

빅오 표기법에서 상수는 과감하게 버린다.

</br>

[![2023-04-04-9-34-33.png](https://i.postimg.cc/Gps8p96Q/2023-04-04-9-34-33.png)](https://postimg.cc/B84QYZSL)

</br>

위의 코드는 n만큼씩 두 번 돌리기 떄문에 O(2n)만큼 시간이 걸린다. 하지만 빅오 표기법에서는 O(2n)을 O(n)으로 표기한다. 왜냐하면 빅오 표기법은 실제 알고리즘의 러닝타임을 재기 위해 만들어진 것이 아니고, 장기적으로 데이터 증가함에 따른 처리시간의 증가율을 예측하기 위해서 만들어진 표기법이기 때문이다. 상수는 고정된 숫자이기 때문에 증가율에 영향을 미칠 때, 언제나 고정된 상수만큼씩만 영향을 미치기 때문에 여기서 증가하지 않는 숫자는 제외하겠다는 것이다.

</br>

[![2023-04-04-9-38-21.png](https://i.postimg.cc/RFDDLsg9/2023-04-04-9-38-21.png)](https://postimg.cc/S2cdyr0t)

</br>

마찬가지로 n<sup>2</sup>도 차원이 늘어나지 않는 한 앞에 붙는 상수는 무시하고, n<sup>2</sup>+n<sup>2</sup>도 그냥 n<sup>2</sup>으로 표기해주면 된다.