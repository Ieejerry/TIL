# 벨만 포드법(Bellman ford algorithm)

</br>

<a href="https://ibb.co/m67ZC4W"><img src="https://i.ibb.co/SRpYXBC/IMG-1935.jpg" alt="IMG-1935" border="0"></a>

</br>

벨만-포드(Bellman-Ford)법은 그래프의 최단 경로 문제를 해결하기 위한 알고리즘이다.

</br>

<<a href="https://ibb.co/4W5BzKV"><img src="https://i.ibb.co/G7bgyn5/IMG-1936.jpg" alt="IMG-1936" border="0"></a>

</br>

각 정점의 초기 가중치를 설정한다. 시작점은 0, 그 외의 정점은 무한대로 설정한다.

</br>

<a href="https://ibb.co/SxSrjcC"><img src="https://i.ibb.co/CtL2c6G/IMG-1937.jpg" alt="IMG-1937" border="0"></a>

</br>

모든 간선 중에서 하나를 선택한다. 여기선 A-B를 연결하는 간선을 선택했다. 선택한 간선의 한쪽 정점에서 다른 정점으로 이동하기 위한 가중치를 계산한다. 계산 방법은 '시작 정점의 가중치 + 간선의 가중치'이다. 계산은 한 방향씩 하지만 어느쪽을 먼저 계산할지는 고려하지 않아도 된다.

여기선 가중치가 작은 정점에서 큰 정점으로 가는 방향을 먼저 계산하도록 하겠다. 정점 B보다도 A가 현재 가중치가 작으므로 정점 A에서 정점B로 가는 경우를 먼저 계산한다. 정점A의 가중치가 0이므로 정점A에서 B로 가는 가중치는 0 + 9로 9가 된다. 계산한 결과가 현재 값보다 작으면 가중치를 새로운 값으로 변경한다.

</br>

<a href="https://ibb.co/6sR53fX"><img src="https://i.ibb.co/DKDnxSr/IMG-1938.jpg" alt="IMG-1938" border="0"></a>

</br>

정점B의 현재 값은 무한대로 9가 작다. 따라서 가중치를 9로 변견한다. 값이 변경된 경우에는 어느 정점에서 온 경로인지를 표시해둔다.(위 그림에서 주황색으로 표시).

계속해서 반대 방향인 정점B에서 정점A로 향하는 경우를 계산해보겠다. 정점B의 가중치가 9이므로 정점B에서 정점A로 가는 가중치는 9 + 9 = 18이 된다. 정점A의 현재 값 0과 비교하면 현재 값이 작음으로 가중치를 변경하지 않는다.

가중치가 큰 정점에서 작은 정점으로 향하는 경우는 간선의 가중치가 마이너스가 아닌 이상 변경될 일이 없다.

동일한 작업을 모든 간선에 적용한다. 간선의 순서는 임의이지만 여기서는 더 왼쪽에 있는 간선부터 계산해가도록 하겠다.

</br>

<a href="https://ibb.co/TwDs71k"><img src="https://i.ibb.co/tHw9vz4/IMG-1939.jpg" alt="IMG-1939" border="0"></a>

</br>

간선을 하나 선택한다.

</br>

<a href="https://ibb.co/DD2Xkzg"><img src="https://i.ibb.co/MD0TpZ5/IMG-1940.jpg" alt="IMG-1940" border="0"></a>

</br>

가중치를 변경했다.

</br>

<a href="https://ibb.co/vqt6PmR"><img src="https://i.ibb.co/LRGXt6H/IMG-1941.jpg" alt="IMG-1941" border="0"></a>

</br>

동일한 방식으로 또 다른 간선을 선택한다.

</br>

<a href="https://ibb.co/WKLYfJZ"><img src="https://i.ibb.co/KyJ3Wvd/IMG-1942.jpg" alt="IMG-1942" border="0"></a>

</br>

가중치를 변경했다. 현시점에선 정점A에서 정점B로 가는 경우 정점A에서 직접 가는 것보다 정점C를 경유하는 것이 가중치가 작다는 것을 알 수 있다.

모든 간선에 대해 변경 작업을 진행해간다.

</br>

<a href="https://ibb.co/Wy3Qbhq"><img src="https://i.ibb.co/xjsypkP/IMG-1943.jpg" alt="IMG-1943" border="0"></a>

</br>

이것으로 1라운드 작업이 끝난 것이다.

동일한 작업을 가중치가 변경되지 않을 때까지 반복한다.

</br>

<a href="https://ibb.co/ScqKsYx"><img src="https://i.ibb.co/T1zHvjT/IMG-1944.jpg" alt="IMG-1944" border="0"></a>

</br>

정점의 가중치가 변경되지 않았으므로 작업을 멈춘다.

</br>

<a href="https://ibb.co/ZXgDdMv"><img src="https://i.ibb.co/XL5RXC6/IMG-1945.jpg" alt="IMG-1945" border="0"></a>

</br>

이 시점에서 알고리즘에 의한 탐색이 완료되며 시작점에서 모든 정점까지의 최단 경로가 나온다.

</br>

<a href="https://ibb.co/6vpQmKV"><img src="https://i.ibb.co/vsr9HNg/IMG-1946.jpg" alt="IMG-1946" border="0"></a>

</br>

처음 상태로 되돌려보겠다. 이번에는 시작점인 A에서 접근할 수 있는 간선의 변경이 마지막에 되도록 모든 간선의 변경 작업을 역순, 즉 오른쪽에서부터 진행해보도록 하겠다.

</br>

<a href="https://ibb.co/tx5xGTD"><img src="https://i.ibb.co/qWwWS3p/IMG-1947.jpg" alt="IMG-1947" border="0"></a>>

</br>

1라운드의 변경 작업이 끝났다. 1라운드가 끝난 시점에서, 시작점 A로부터 1회 이동으로 도달할 수 있는 정점이 가중치만 변경된 것을 알 수 있다.

2라운드 변경 작업을 진행한다.

</br>

<a href="https://ibb.co/fNfcLyn"><img src="https://i.ibb.co/rpYWNzc/IMG-1948.jpg" alt="IMG-1948" border="0"></a>

</br>

2라운드 변경 작업을 끝냈다. 2라운드 변경이 끝난 시점에서, A로부터 2회 이동으로 도달할 수 있는 정점의 가중치만 변경된 것을 알 수 있다. 사실은 변경 작업을 N회 실시한 시점에서 A로부터 이동을 N회 이하로 제한한 각 정점까지의 최단 경로가 구해진다. 그림은 변경 작업을 2회한 상태이므로 시작점에서 2회 이하로 이동한 각 정점의 최단 경로가 구해진 상태이다. 어디까지나 2회 이하의 이동 시에 최단 경로이다.

예를 들어 F는 실제는 A-C-D-F라는 경로를 지나는 것이 가중치가 적지만 3회 이동을 필요로 하므로 고려하지 않았다.

또한, 점 B는 3회 이동한 경우의 최단 경로지만 간선을 변경하는 순서로 인해 우연히 이렇게 된 것이다. 즉, 간선을 변경하는 순서에 따라선 변경한 횟수 이상의 이동을 필요로 하는 최단 경로가 있을 수 있다.

정점이 n개 있다고 하고 동일한 정점을 지나지않도록 n-1회 이동하면 반드시 모든 정점을 지날 수 있다. 즉, 많아도 n-1회 변경 작업을 하면 모든 점에 대한 최단 경로를 구할 수 있다. 또한 도중에 변경되지 않은 경우라도 최단 경로가 확정됐다는 것을 판단할 수 있으므로 거기서 작업을 중단한다.

그러면 모든 정점에 대한 최단 경로를 구할 때까지 그림의 상태로부터 변경 작업을 재개해보겠다.

</br>

<a href="https://ibb.co/q5vY8vb"><img src="https://i.ibb.co/gVxZ8xs/IMG-1949.jpg" alt="IMG-1949" border="0"></a>

</br>

변경이 없으면 작업을 멈춘다.

</br>

<a href="https://ibb.co/M9wnfXF"><img src="https://i.ibb.co/SJYNcLF/IMG-1950.jpg" alt="IMG-1950" border="0"></a>

</br>

앞의 방법과 동일하게 모든 정점에 대한 최단 경로를 구했다.

</br>

<a href="https://ibb.co/Pmg32Sn"><img src="https://i.ibb.co/yfqGz31/IMG-1951.jpg" alt="IMG-1951" border="0"></a>

</br>

참고로 그래프의 A-B처럼 각 방향의 가중치가 다른 경우 또는 일반 통행만 가능한 경우에도

</br>

<a href="https://ibb.co/R2zq1hm"><img src="https://i.ibb.co/D45ZNGy/IMG-1952.jpg" alt="IMG-1952" border="0"></a>

</br>

벨만-포드법으로 최단 경로를 구할 수 있다.

참고로 그림처럼 간선에 방향이 설정돼 있는 그래프를 '방향성 그래프', 설정돼 있지 않은 것을 '비방향성 그래프'라고 한다.

</br>

<a href="https://ibb.co/VLpyPwn"><img src="https://i.ibb.co/grF1B4q/IMG-1953.jpg" alt="IMG-1953" border="0"></a>

</br>

음에 가중치를 포함하는 경우에는 어떻게 되는지 알아보겠다.

음의 가중치란 그림에선 C-B에 있는 '-3'를 가리킨다.

가중치가 음의 값이라는 것은 무슨 의미이냐면 예를 들어 시작점 A로부터 종점 G까지 차로 이동하는 경우를 생각해보겠다. 각 가중치는 연료의 소비량을 나타낸다고 생각할 수 있다. 이 경우 '음의 가중치' 위치에는 주요소가 있으며 연료를 주유한다고 생각할 수 있다.

</br>

<a href="https://ibb.co/41vrJ4j"><img src="https://i.ibb.co/rd8rv5Z/IMG-1954.jpg" alt="IMG-1954" border="0"></a>

</br>

벨만-포드법에선 이처럼 '음의 가중치'를 포함하더라도 올바른 최단 경로를 구할 수 있다.

</br>

<a href="https://ibb.co/FxFtJKk"><img src="https://i.ibb.co/WxL1F6N/IMG-1955.jpg" alt="IMG-1955" border="0"></a>

</br>

그래프처럼 C-B의 음의 가중치가 -3에서 -6이 된 경우, 문제 없이 최단 경로를 구할 수 있을 것처럼 보이지만

</br>

<a href="https://ibb.co/4mpMXRC"><img src="https://i.ibb.co/GxRk8QG/IMG-1956.jpg" alt="IMG-1956" border="0"></a>

</br>

A-C-B를 일주했을 때의 합계가 -1이 된다. 이런 경우를 '음의 폐로'라고 한다.

</br>

<a href="https://ibb.co/8NGbry0"><img src="https://i.ibb.co/ydKp6zX/IMG-1957.jpg" alt="IMG-1957" border="0"></a>

</br>

음의 폐로가 존재하는 경우 해당 경로를 계속 순회하면 가중치가 계속 작아지게 된다. 따라서 어떤 방법을 사용해도 최단 경로를 구할 수 없다. 이 그래프의 최단 경로를 벨만-포드법으로 구하려고 하면, 몇 번이고 변경 작업을 해도 어느 정점의 값이 바뀌므로 종료되지 않는다. 반대로 벨만-포드법은 정점의 수 -1의 작업으로 변경 작업이 완료되므로 변경이 n회 이상이 되면 그래프의 어딘가에 음의 폐로가 존재한다는 의미가 된다.

</br>

<a href="https://ibb.co/8gSjMpV"><img src="https://i.ibb.co/XxvzXgT/IMG-1958.jpg" alt="IMG-1958" border="0"></a>

</br>

이와 같이 벨만-포드법은 계산량이 많은 알고리즘이지만 음의 가중치가 있어도 최단 경로를 구할 수 있으며 음의 폐로가 존재한다는 것도 감지할 수 있다.