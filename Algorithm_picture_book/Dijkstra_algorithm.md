# 다익스트라 기법(Dijkstra algorithm)

</br>

<a href="https://ibb.co/kKPhF1q"><img src="https://i.ibb.co/R2JCWyQ/IMG-1959.jpg" alt="IMG-1959" border="0"></a>

</br>

다익스트라 기법은 그래프의 최단 경로를 찾는 알고리즘이다. 벨만-포드법보다 효율적인 방법이다.

</br>

<a href="https://ibb.co/NWqJGZ5"><img src="https://i.ibb.co/7rDZ02P/IMG-1960.jpg" alt="IMG-1960" border="0"></a>

</br>

먼저 각 정점의 초기 가중치를 설정한다. 시작점은 0, 그 외의 정점은 무한대로 설정한다.

</br>

<a href="https://ibb.co/qWRsvwM"><img src="https://i.ibb.co/P95hd8Z/IMG-1961.jpg" alt="IMG-1961" border="0"></a>

</br>

시작점붙 시작하겠다.

</br>

<a href="https://ibb.co/vw1YRdD"><img src="https://i.ibb.co/YR2Zwdb/IMG-1962.jpg" alt="IMG-1962" border="0"></a>

</br>

현재 있는 정점에서 갈 수 있는, 탐색하지 않은 정점을 찾는다. 발견한 정점은 다음에 진행할 후보로 설정한다. 여기선 정점B와 정점C가 후보가 된다. 후보인 각 정점의 가중치를 계산한다. 계산 방법은 '현재 있는 정점의 가중치 + 현재 있는 정점에서 후보 정점까지 가는 가중치'가 된다. 예를 들어 정점B의 경우 현재 있는 시작점 가중치가 0이므로 0 + 2 = 2가 된다. 동일한 방식으로 C의 가중치는 0 + 5 = 5가 된다. 계산한 결과가 현재 가중치보다 작으면 가중치를 새로운 값으로 변경한다.

</br>

<a href="https://ibb.co/bv7Gm1R"><img src="https://i.ibb.co/s1tXRjJ/IMG-1963.jpg" alt="IMG-1963" border="0"></a>

</br>

정점B, C의 현재 가중치는 무한대로 계산한 결과가 더 작다. 따라서 각각을 새로운 값으로 변경한다.

</br>

<a href="https://ibb.co/3zXCsQf"><img src="https://i.ibb.co/6BhWZLv/IMG-1964.jpg" alt="IMG-1964" border="0"></a>

</br>

후보 정점 중에서 가주이가 가장 작은 정점을 선택한다. 여기선 정점B가 된다. 이 시점에서 선택한 정점B로 가는 경로 A-B는 시작점에서 정점B로 가는 최단 경로로 정해진다. 왜냐하면 다른 경로를 사용하면 반드시 정점C를 경유해야 해서 결과적으로 현재 경로보다 가중치가 높아지기 때문이다.

</br>

<a href="https://ibb.co/4tk2BjQ"><img src="https://i.ibb.co/PjkMB5S/IMG-1965.jpg" alt="IMG-1965" border="0"></a>

</br>

최단 경로를 결정한 정점B로 이동한다.

</br>

<a href="https://ibb.co/CnrwQQS"><img src="https://i.ibb.co/MRXg77J/IMG-1966.jpg" alt="IMG-1966" border="0"></a>

</br>

현재 있는 정점에서 갈 수 있는 정점을 새로운 후보로 추가한다. 여기선 C, D, E가 된다. 앞의 계산 방법과 동일한 방법으로 각 후보 정점들의 가중치를 계산한다. 정점B에서 정점C로 가는 가중치를 2 + 6 = 8이 되지만 현재 값인 5가 더 작기 때문에 변경하지 않는다.

</br>

<a href="https://ibb.co/1Ryvf9C"><img src="https://i.ibb.co/DwcVD7B/IMG-1967.jpg" alt="IMG-1967" border="0"></a>

</br>

나머지 정점D와 E의 가중치를 변경한다.

</br>

<a href="https://ibb.co/T4Tf0tp"><img src="https://i.ibb.co/Jvd1pH0/IMG-1968.jpg" alt="IMG-1968" border="0"></a>

</br>

후보 정점 중에서 가중치가 가장 작은 정점을 선택한다. 여기서 정점D가 된다. 이 시점에서 선택한 정점D로 가는 경로 A-B-D가 시작점에서 정점D로 가는 최단 경로로 결정된다. 경로 A-B-D는 후보 정점 중에서 가장 가중치가 낮은 것을 선택한 결과이다. 따라서 다른 정점을 경유해서 D로 가면 가중치가 반드시 지금보다 높아지게 된다. 이처럼 다익스트라 기법은 각 정점으로 향하는 최단 경로를 하나씩 결정해가며 그래프를 탐색하는 알고리즘이다.

</br>

<a href="https://ibb.co/18Mjcf5"><img src="https://i.ibb.co/syCz7vG/IMG-1969.jpg" alt="IMG-1969" border="0"></a>

</br>

동일한 작업을 종점 G에 도착할 때까지 반복한다.

</br>

<a href="https://ibb.co/8DDq5LQ"><img src="https://i.ibb.co/SXXbn4Z/IMG-1970.jpg" alt="IMG-1970" border="0"></a>

</br>

<a href="https://ibb.co/0rBTwmZ"><img src="https://i.ibb.co/m4vkxbt/IMG-1971.jpg" alt="IMG-1971" border="0"></a>

</br>

<a href="https://ibb.co/JKGZtw4"><img src="https://i.ibb.co/zrBdxTY/IMG-1972.jpg" alt="IMG-1972" border="0"></a>

</br>

<a href="https://ibb.co/kxvmyST"><img src="https://i.ibb.co/6mLXZWS/IMG-1973.jpg" alt="IMG-1973" border="0"></a>

</br>

<a href="https://ibb.co/0Qqc1Xj"><img src="https://i.ibb.co/BwLtvPV/IMG-1974.jpg" alt="IMG-1974" border="0"></a>

</br>

<a href="https://ibb.co/BnC0Dv8"><img src="https://i.ibb.co/cYr45Rz/IMG-1975.jpg" alt="IMG-1975" border="0"></a>

</br>

<a href="https://ibb.co/B4CG53S"><img src="https://i.ibb.co/3fCv9dL/IMG-1976.jpg" alt="IMG-1976" border="0"></a>

</br>

<a href="https://ibb.co/qDrNQCQ"><img src="https://i.ibb.co/0nGCbKb/IMG-1977.jpg" alt="IMG-1977" border="0"></a>

</br>

<a href="https://ibb.co/tZ8CmGy"><img src="https://i.ibb.co/q0k1ySb/IMG-1978.jpg" alt="IMG-1978" border="0"></a>

</br>

<a href="https://ibb.co/2S3xSvM"><img src="https://i.ibb.co/ypFtp6k/IMG-1979.jpg" alt="IMG-1979" border="0"></a>

</br>

<a href="https://ibb.co/JFzY90T"><img src="https://i.ibb.co/rfZBVTh/IMG-1980.jpg" alt="IMG-1980" border="0"></a>

</br>

<a href="https://ibb.co/BwnHSSf"><img src="https://i.ibb.co/HXhLkkK/IMG-1981.jpg" alt="IMG-1981" border="0"></a>

</br>

<a href="https://ibb.co/PzGH6Ww"><img src="https://i.ibb.co/G3QS5Mc/IMG-1982.jpg" alt="IMG-1982" border="0"></a>

</br>

<a href="https://ibb.co/9HT2Cfd"><img src="https://i.ibb.co/HTzYkM9/IMG-1983.jpg" alt="IMG-1983" border="0"></a>

</br>

<a href="https://ibb.co/PDz8fbb"><img src="https://i.ibb.co/5KxVfzz/IMG-1984.jpg" alt="IMG-1984" border="0"></a>

</br>

<a href="https://ibb.co/vJnCZ3Z"><img src="https://i.ibb.co/TH3Dm4m/IMG-1985.jpg" alt="IMG-1985" border="0"></a>

</br>

<a href="https://ibb.co/DrqKcrp"><img src="https://i.ibb.co/CPr0CP2/IMG-1986.jpg" alt="IMG-1986" border="0"></a>

</br>

종점 G에 도착했으므로 탐색을 종료한다.

최종적으로 만들어진 주황색 트리를 최단 경로트리라고 하며, 각 정점으로 가는 최단 경로를 나타낸다. 두꺼운 선으로 강조하고 있는 것은 시작점A에서 종점G까지의 최단 경로이다. 가중치 계산과 변경을 모든 간선에 대해 반복하는 벨만-포드법과 달리, 다익스트라 기법은 정점 선택 방법을 고민해서 효율이 좋은 최단 경로를 구한다.

</br>

<a href="https://ibb.co/GCmXsC8"><img src="https://i.ibb.co/nQpT3QY/IMG-1987.jpg" alt="IMG-1987" border="0"></a>

</br>

다익스트라 기법은 벨만-포드법과 마찬가지로 방향에 따라 가중치가 다른 경우나 일방 통행의 간선이 존재해도

</br>

<a href="https://ibb.co/3TYwBKL"><img src="https://i.ibb.co/S672RS9/IMG-1988.jpg" alt="IMG-1988" border="0"></a>

</br>

최단 경로를 제대로 구할 수 있다.

</br>

<a href="https://ibb.co/2SgtjKY"><img src="https://i.ibb.co/ScRnKv7/IMG-1989.jpg" alt="IMG-1989" border="0"></a>

</br>

참고로 그림처럼 간선에 방향이 설정돼 있는 그래프를 '방향성 그래프', 설정돼 있지 않은 것을 '비방향성 그래프'라고 한다.

</br>

<a href="https://ibb.co/2d3HjbL"><img src="https://i.ibb.co/6F0L4dp/IMG-1990.jpg" alt="IMG-1990" border="0"></a>

</br>

다익스트라 기법에선 마이너스 가중치를 포함하는 경우에는 최단 경로가 잘못되는 경우가 있다. 이 점은 벨만-포드법과 다른 점이다.

</br>

<a href="https://ibb.co/PYSkgJX"><img src="https://i.ibb.co/wLvt48G/IMG-1991.jpg" alt="IMG-1991" border="0"></a>

</br>

위 그래프에선 마이너스 가중치가 있는 C-B를 통과하는 경로 A-C-B-G(가중치 2)가 올바른 최단 경로이다.

</br>

<a href="https://ibb.co/80MJJR4"><img src="https://i.ibb.co/TkcZZnq/IMG-1992.jpg" alt="IMG-1992" border="0"></a>

</br>

다익스트라 기법을 적용해서 풀어보겠다.

</br>

<a href="https://ibb.co/BfmTbQ7"><img src="https://i.ibb.co/WHQBZMd/IMG-1993.jpg" alt="IMG-1993" border="0"></a>

</br>

시작점A에서 도달할 수 있는, 검색이 완료되지 않은 정점은 B와 C이다. 각각의 가중치는 2와 4이다.

</br>

<a href="https://ibb.co/tzhp564"><img src="https://i.ibb.co/2S63Bry/IMG-1994.jpg" alt="IMG-1994" border="0"></a>

</br>

이 시점에서 다익스트라 기법은 경로 A-B가 시작점A에서 B로 가는 최단 경로라고 결정한다. 다른 경로를 사용하는 경우에는 반드시 C를 경유해야 하지만, A-C의 가중치가 A-B의 가중치보다 크기 때문이다. 이미 알고 있는 것처럼 이것은 모든 간선의 가중치가 0보다 큰 경우, 즉 그래프상에 마이너스 가중치가 존재하지 않는다는 조건하에서이다.

</br>

<a href="https://ibb.co/3s8xpw3"><img src="https://i.ibb.co/qn4HNzS/IMG-1995.jpg" alt="IMG-1995" border="0"></a>

</br>

<a href="https://ibb.co/yNHjL4r"><img src="https://i.ibb.co/j8nX7JS/IMG-1996.jpg" alt="IMG-1996" border="0"></a>

</br>

<a href="https://ibb.co/mR6gJhb"><img src="https://i.ibb.co/Rgzd2QY/IMG-1997.jpg" alt="IMG-1997" border="0"></a>

</br>

알고리즘은 시작점A로부터 종점G까지의 최단 경로가 A-B-G이고 그 가중치가 3이라는 결론을 짓는다. 앞서 설명한 것처럼 이 결과는 틀린 것이다.

</br>

<a href="https://ibb.co/1zd4vdc"><img src="https://i.ibb.co/6X1qn1Q/IMG-1998.jpg" alt="IMG-1998" border="0"></a>

</br>

참고로 위 그래프처럼

</br>

<a href="https://ibb.co/1RSvzy9"><img src="https://i.ibb.co/SVLsfYK/IMG-1999.jpg" alt="IMG-1999" border="0"></a>

</br>

특정 경로를 지나는 가중치가 마이너스가 되는 '음의 폐로'로 포함하는 그래프에선 다익스트라 기법을 사용하면 최단 경로가 존재하지 않음에도 불구하고 잘못된 최단 경로를 찾아낸다.

</br>

<a href="https://ibb.co/TkvS0Jv"><img src="https://i.ibb.co/FKxMYcx/IMG-2001.jpg" alt="IMG-2001" border="0"></a>

</br>

이와 같이 다익스트라 기법은 마이너스 가중치를 포함하는 그래프에선 사용할 수 없다.

반대로 다익스트라 기법은, 그래프에 마이너스 가중치가 존재하지 않는 경우에 벨만-포드법보다 더 적은 계산량으로 최단 경로를 구할 수 있다.