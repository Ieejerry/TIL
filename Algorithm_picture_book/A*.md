# A*(에이 스타)

</br>

<a href="https://ibb.co/xXhKL0S"><img src="https://i.ibb.co/2Wq0hQ7/IMG-2002.jpg" alt="IMG-2002" border="0"></a>

</br>

A*(에이 스타라고 읽는다.)는 다익스트라 기법을 발전시킨 것이다. 이 미로의 최단 경로를 먼저 다익스트라 기법으로 찾아보겠다.

</br>

<a href="https://ibb.co/Dtr5WLb"><img src="https://i.ibb.co/mGN6TSB/IMG-2003.jpg" alt="IMG-2003" border="0"></a>

</br>

미로는 각 정점 사이의 가중치가 1인 그래프라고 해석할 수 있다.

</br>

<a href="https://ibb.co/q1xHTcs"><img src="https://i.ibb.co/Bswh0QZ/IMG-2004.jpg" alt="IMG-2004" border="0"></a>

</br>

이 것을 전제로 다익스트라 기법으로 최단 경로를 찾아보겠다.

</br>

<a href="https://ibb.co/DRQT5FS"><img src="https://i.ibb.co/879t6wS/IMG-2005.jpg" alt="IMG-2005" border="0"></a>

</br>

최단 경로를 찾았지만 미로상의 대부분의 길을 지나고 있다. 다익스트라 기법에선 시작점부터의 가중치를 고려해서 다음으로 갈 정점을 결정한다.

</br>

<a href="https://ibb.co/c83G9BC"><img src="https://i.ibb.co/n1mHyGn/IMG-2006.jpg" alt="IMG-2006" border="0"></a>

</br>

이 때문에 화살표가 가리키고 있는 경로도 목표로부터 멀어진다는 것을 고려하지 않고 탐색할 수가 있다. A*에선 시작점부터의 가중치뿐만 아니라 현시점에서 목표까지의 추정 가중치도 함꼐 고려해서 탐색한다.

</br>

<a href="https://ibb.co/1zYnj9v"><img src="https://i.ibb.co/cYKvVNg/IMG-2007.jpg" alt="IMG-2007" border="0"></a>

</br>

이 추정치는 자유롭게 설정할 수 있으며 여기선 왼쪽 아래에 있는 목표로부터의 직선 경로를 반올림한 값을 이용하도록 한다. 이처럼 다익스트라 기법은 각 정점으로 향하는 최단 경로를 하나씩 결정해가며 그래프를 탐색하는 알고리즘이다. 사람이 미리 설정하는 추정 가중치를 '발견적 가중치(heuristic weight)'라고 한다.

</br>

<a href="https://ibb.co/4WNgnQF"><img src="https://i.ibb.co/LSphXG0/IMG-2008.jpg" alt="IMG-2008" border="0"></a>

</br>

여기서 설정한 추정 가중치는 해당 지점의 고도를 나타낸다고 생각하면 이해하기 쉽다. 오른쪽 아래에 있는 목표 지점이 가장 낮고 왼쪽 위에 있는 가중치 8인 지점이 가장 높은 곳이 된다. 언덕을 올라가는 것보다 내려가는 것이 쉽다. 미로를 탐색할 때에 언덕을 내려가도록 하는 것이 쉽다. 즉, 가중치가 낮은 쪽으로 이동하게 하면 쉽게 목표에 도달할 수 있다.

</br>

<a href="https://ibb.co/DrtvxpH"><img src="https://i.ibb.co/MBstY6x/IMG-2009.jpg" alt="IMG-2009" border="0"></a>

</br>

이번에는 A*를 사용해보겠다.

</br>

<a href="https://ibb.co/DDxN5P5"><img src="https://i.ibb.co/HDW0nLn/IMG-2010.jpg" alt="IMG-2010" border="0"></a>

</br>

먼저 시작 지점을 탐색 완료했다고 표시한다.

</br>

<a href="https://ibb.co/NtTfWDp"><img src="https://i.ibb.co/zQ6CP9b/IMG-2011.jpg" alt="IMG-2011" border="0"></a>

</br>

시작점으로부터 갈 수 있는 칸의 가중치를 각각 계산한다. 가중치는 '거기에 도달할 때까지의 가중치'와 '발견적 가중치'의 합계로 계산한다.

</br>

<a href="https://ibb.co/dcty8ZX"><img src="https://i.ibb.co/8BbV1kG/IMG-2012.jpg" alt="IMG-2012" border="0"></a>

</br>

가중치가 가장 낮은 칸을 하나 선택한다.

</br>

<a href="https://ibb.co/6JVvRY2"><img src="https://i.ibb.co/zHj8hs1/IMG-2013.jpg" alt="IMG-2013" border="0"></a>

</br>

선택한 칸을 탐색 완료 상태로 표시한다.

</br>

<a href="https://ibb.co/grkRrtH"><img src="https://i.ibb.co/j8nr83B/IMG-2014.jpg" alt="IMG-2014" border="0"></a>

</br>

탐색을 완료한 칸에서 갈 수 있는 칸의 가중치를 계산한다.

</br>

<a href="https://ibb.co/zZxtqxW"><img src="https://i.ibb.co/Hq4954L/IMG-2015.jpg" alt="IMG-2015" border="0"></a>

</br>

가중치가 가장 낮은 칸을 하나 선택한다.

</br>

<a href="https://ibb.co/WFpcZwD"><img src="https://i.ibb.co/4MgjzGs/IMG-2016.jpg" alt="IMG-2016" border="0"></a>

</br>

선택한 점을 탐색 완료 상태로 표시한다. 이후로는 같은 작업을 목표에 도착할 때까지 반복한다.

</br>

<a href="https://ibb.co/k2gm9NG"><img src="https://i.ibb.co/r2GdcDQ/IMG-2017.jpg" alt="IMG-2017" border="0"></a>

</br>

다익스트라 기법보다 효율적으로 미로를 탐색할 수 있었다.

</br>

<a href="https://ibb.co/7jZpj5N"><img src="https://i.ibb.co/DzvMzyg/IMG-2018.jpg" alt="IMG-2018" border="0"></a>

</br>

발견적 가중치를, 직선거리가 아닌 실제로 소요되는 최단 가중추라고 해보겠다.

</br>

<a href="https://ibb.co/jr2KGjT"><img src="https://i.ibb.co/ZMPsKbV/IMG-2019.jpg" alt="IMG-2019" border="0"></a>

</br>

이번에는 다른 길로 빠지지 않고 최단 경로를 따라 목표에 도착했다. 현실적으로는 실제로 소요되는 최단 가중치를 알고 있는 경우는 없다. 그것을 알고 있다면 탐색할 필요가 없기 때문이다. 이처럼 A*에선 발견적 가중치를 어떻게 설정하는지가 중요한 요소가 된다. 발견적 가중치가 실제로 소요되는 최단 가중치에 가까울 수록 더 효율적으로 미로를 탐색할 수 있다.

</br>

<a href="https://ibb.co/vQQDn0D"><img src="https://i.ibb.co/ZYYNDqN/IMG-2020.jpg" alt="IMG-2020" border="0"></a>

</br>

반대로 발견적 가중치의 조정에 실패한 경우에는 어떻게 되는지 보도록 하겠다. 여기선 극단적인 예로 발견적 가중치를 최단 경로만 제외하고 모두 0으로 설정해보겠다.

</br>

<a href="https://ibb.co/kmxDNQY"><img src="https://i.ibb.co/phxKYJC/IMG-2021.jpg" alt="IMG-2021" border="0"></a>

</br>

다익스트라 기법보다 효율이 나쁜 결과를 보여준다. 하지만 최단 경로는 제대로 찾았다. A*에선 발견적 가중치를 '현 시점부터 목표까지의 최단 가중치'이하로 설정하는 경우에는 효율의 차이는 있지만 제대로 된 최단 경로를 찾는다는 것이 보장된다.

</br>

<a href="https://ibb.co/ZBnxSMp"><img src="https://i.ibb.co/X7htDCr/IMG-2022.jpg" alt="IMG-2022" border="0"></a>

</br>

나쁜 예로 발견적 가중치를 현 시점부터 목표까지의 최단 가중치보다 크게 설정해보겠다. 여기선 최단 경로에만 설정했던 발견적 가중치를 2배 값으로 설정했다. 이를 통해 현시점부터 목표까지의 최단 가중치를 크게 상회하게 된다.

</br>

<a href="https://ibb.co/94DBvY1"><img src="https://i.ibb.co/pK7NPXM/IMG-2023.jpg" alt="IMG-2023" border="0"></a>

</br>

알고리즘은 탐색이 완료됐다고 판단하지만 찾은 경로는 최단 경로와 다르다.

</br>

<a href="https://ibb.co/zVYgkbt"><img src="https://i.ibb.co/whXqvC2/IMG-2024.jpg" alt="IMG-2024" border="0"></a>

</br>

이처럼 A*가 똑똑한 탐색 알고리즘이 되는지 여부는 설정 방법에 달려있다.

게임 프로그래밍에서 플레이어를 쫓는 적의 움직임을 계산할 때 등에 자주 사용된다. 하지만 계산량이 많아져서 게임 전체의 진행 속도에 악영향을 끼칠 수도 있다. 다른 알고리즘과 조합해서 제한적인 상황에 사용하는 등 사용 시에는 고민이 필요하다.