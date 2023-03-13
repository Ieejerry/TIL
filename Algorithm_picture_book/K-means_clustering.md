# K-means법(K-means clustering)

</br>

<a href="https://ibb.co/g6jdvg9"><img src="https://i.ibb.co/jH6zV4f/Kakao-Talk-20230313-205050325.jpg" alt="Kakao-Talk-20230313-205050325" border="0"></a>

</br>

K-means법은 클러스터링 알고리즘 중 하나이다.

</br>

<a href="https://ibb.co/HC99Y4B"><img src="https://i.ibb.co/VxkkD9J/Kakao-Talk-20230313-205050325-01.jpg" alt="Kakao-Talk-20230313-205050325-01" border="0"></a>

</br>

클러스터링(clustering)이란 데이터가 주어졌을 때

</br>

<a href="https://ibb.co/BK8f80p"><img src="https://i.ibb.co/dJnfn8T/Kakao-Talk-20230313-205050325-02.jpg" alt="Kakao-Talk-20230313-205050325-02" border="0"></a>

</br>

'비슷한 것'들을 묶어 그룹으로 분류하는 작업을 가리킨다.

</br>

<a href="https://ibb.co/f4fkSvy"><img src="https://i.ibb.co/6gzHZBT/Kakao-Talk-20230313-205050325-03.jpg" alt="Kakao-Talk-20230313-205050325-03" border="0"></a>

</br>

이때 개별 그룹을 '클러스터(cluster)'라고 한다. '비슷한 것'의 기준은 각 데이터 간 거리나 좌표 등 알고리즘에 따라 달라진다.

</br>

<a href="https://ibb.co/h7xR4zh"><img src="https://i.ibb.co/smpvNYk/Kakao-Talk-20230313-205050325-04.jpg" alt="Kakao-Talk-20230313-205050325-04" border="0"></a>

</br>

K-means법은 각 클러스터의 중심점으로부터의 거리로 데이터를 분류한다.

알고리즘의 과정을 보도록 하겠다.

</br>

<a href="https://ibb.co/G3fQRgC"><img src="https://i.ibb.co/JFWjHXr/Kakao-Talk-20230313-205050325-05.jpg" alt="Kakao-Talk-20230313-205050325-05" border="0"></a>

</br>

먼저 클러스터링을 하고 싶은 데이터를 준비한다. 다음은 클러스터의 수를 정한다. 클러스터 수를 미리 정하는 것이 k-means법의 특징이다. 여기선 클러스터 수를 3으로 설정하고 있다.

</br>

<a href="https://ibb.co/4N16vFY"><img src="https://i.ibb.co/RHjxrgB/Kakao-Talk-20230313-205050325-06.jpg" alt="Kakao-Talk-20230313-205050325-06" border="0"></a>

</br>

클러스터의 중심점이 될 세 점을 임의의 위치에 설치한다.

</br>

<a href="https://ibb.co/DV4b5Qm"><img src="https://i.ibb.co/NVx3ZKf/Kakao-Talk-20230313-205050325-07.jpg" alt="Kakao-Talk-20230313-205050325-07" border="0"></a>

</br>

각 데이터로부터 가장 가까운 중심점을 계산을 통해 결정한다.

</br>

<a href="https://ibb.co/d6jGHRk"><img src="https://i.ibb.co/6brgqkD/Kakao-Talk-20230313-205050325-08.jpg" alt="Kakao-Talk-20230313-205050325-08" border="0"></a>

</br>

각 데이터가 속하는 클러스터로 분류한다.

</br>

<a href="https://ibb.co/X7n7bwy"><img src="https://i.ibb.co/n7X7bW3/Kakao-Talk-20230313-205050325-09.jpg" alt="Kakao-Talk-20230313-205050325-09" border="0"></a>

</br>

각 클러스터의 중심을 재계산해서 해당 위치로 클러스터의 중심점을 이동시킨다. 중심점을 이동하므로 '가장 가까운 중심점'이 바뀌는 데이터가 생긴다.

</br>

<a href="https://ibb.co/vqsK4Dd"><img src="https://i.ibb.co/H4NkTXP/Kakao-Talk-20230313-205050325-10.jpg" alt="Kakao-Talk-20230313-205050325-10" border="0"></a>

</br>

가장 가까운 클러스터의 중심점을 재계산하고 각 데이터를 클러스터로 재분류한다. '각 데이터의 클러스터 분류'와 '중심점을 클로스터 중심으로 이동'을 중심점이 수렴할 때까지(움직일 수 없을 때까지) 반복한다.

</br>

<a href="https://ibb.co/mXvKw5X"><img src="https://i.ibb.co/RBhKmTB/Kakao-Talk-20230313-205050325-11.jpg" alt="Kakao-Talk-20230313-205050325-11" border="0"></a>

</br>

<a href="https://ibb.co/WPLWbcP"><img src="https://i.ibb.co/Br9VXgr/Kakao-Talk-20230313-205050325-12.jpg" alt="Kakao-Talk-20230313-205050325-12" border="0"></a>

</br>

<a href="https://ibb.co/YpGx8bf"><img src="https://i.ibb.co/cDdjtx2/Kakao-Talk-20230313-205050325-13.jpg" alt="Kakao-Talk-20230313-205050325-13" border="0"></a>

</br>

<a href="https://ibb.co/QmFmn26"><img src="https://i.ibb.co/12f2KD9/Kakao-Talk-20230313-205050325-14.jpg" alt="Kakao-Talk-20230313-205050325-14" border="0"></a>

</br>

<a href="https://ibb.co/YRv7gV2"><img src="https://i.ibb.co/8KFDkQM/Kakao-Talk-20230313-205050325-15.jpg" alt="Kakao-Talk-20230313-205050325-15" border="0"></a>

</br>

중심점이 수렴하므로 작업을 종료한다. 작업을 반복하다보면 중심점이 반듯이 수렴하게 된다는 것은 수학적으로 이미 증명된 사실이다. 이것으로 클러스터링이 완료되었다. 데이터가 비슷한 것끼리 분류된 것을 확인할 수 있다.

</br>

<a href="https://ibb.co/Pr6THrH"><img src="https://i.ibb.co/wdzJmdm/Kakao-Talk-20230313-205050325-16.jpg" alt="Kakao-Talk-20230313-205050325-16" border="0"></a>

</br>

동일한 데이터에 대해 클러스터 수를 2로 설정하면 어떻게 되는지 확인해보겠다.

</br>

<a href="https://ibb.co/XJLQPnr"><img src="https://i.ibb.co/Th2fGQx/Kakao-Talk-20230313-205050325-17.jpg" alt="Kakao-Talk-20230313-205050325-17" border="0"></a>

</br>

중심점을 임의로 설정하고

</br>

<a href="https://ibb.co/bdZWn0d"><img src="https://i.ibb.co/pX80p7X/Kakao-Talk-20230313-205050325-18.jpg" alt="Kakao-Talk-20230313-205050325-18" border="0"></a>

</br>

'각 데이터의 클러스터 분류'와 '중심점을 클로스터 중심으로 이동'을 중심점이 수렴할 때까지(움직일 수 없을 때까지) 반복한다.

</br>

<a href="https://ibb.co/GFg8n1m"><img src="https://i.ibb.co/b7pCQyt/Kakao-Talk-20230313-205050325-19.jpg" alt="Kakao-Talk-20230313-205050325-19" border="0"></a>

</br>

<a href="https://ibb.co/k9sJ7vz"><img src="https://i.ibb.co/qW3CSVh/Kakao-Talk-20230313-205050325-20.jpg" alt="Kakao-Talk-20230313-205050325-20" border="0"></a>

</br>

<a href="https://ibb.co/pyq9CpQ"><img src="https://i.ibb.co/JQZMXPq/Kakao-Talk-20230313-205050325-21.jpg" alt="Kakao-Talk-20230313-205050325-21" border="0"></a>

</br>

<a href="https://ibb.co/mTTwX0R"><img src="https://i.ibb.co/MSS4Gfg/Kakao-Talk-20230313-205050325-22.jpg" alt="Kakao-Talk-20230313-205050325-22" border="0"></a>

</br>

<a href="https://ibb.co/FmtTDdy"><img src="https://i.ibb.co/n6SJLKY/Kakao-Talk-20230313-205050325-23.jpg" alt="Kakao-Talk-20230313-205050325-23" border="0"></a>

</br>

<a href="https://ibb.co/0sksQMQ"><img src="https://i.ibb.co/Rj1j707/Kakao-Talk-20230313-205050325-24.jpg" alt="Kakao-Talk-20230313-205050325-24" border="0"></a>

</br>

<a href="https://ibb.co/7Rf4nqt"><img src="https://i.ibb.co/gP2VSxZ/Kakao-Talk-20230313-205050325-25.jpg" alt="Kakao-Talk-20230313-205050325-25" border="0"></a>

</br>

중심점에 수렴했다. 이번에는 왼쪽과 아래에 위치한 두 개의 데이터 그룹이 하나의 클러스터로 분류된다. 이와 같이 k-means법은 클러스터 수를 미리 정해두어야 하므로 이 수가 최적의 수가 아니면 유효한 결과가 나오지 않을 수도 있다. 최적의 클러스터 수를 추측하기 위해 데이터를 사전에 분석하거나 클러스터 수를 몇 번 변경해가며 k-means법을 실행해보는 기법이 있다.

</br>

<a href="https://ibb.co/f1f0my0"><img src="https://i.ibb.co/986YR1Y/Kakao-Talk-20230313-205050325-26.jpg" alt="Kakao-Talk-20230313-205050325-26" border="0"></a>

</br>

이번에는 동일한 데이터에 대해 중심점의 위치를 변경하면 어떻게 되는지 보도록 하겠다.

</br>

<a href="https://ibb.co/r5KTxZK"><img src="https://i.ibb.co/tYwkqbw/Kakao-Talk-20230313-205050325-27.jpg" alt="Kakao-Talk-20230313-205050325-27" border="0"></a>

</br>

'각 데이터의 클러스터의 분류'와 '중심점을 클로스터 중심으로 이동'을 중심점이 수렴할 때까지(움직일 수 없을 때까지) 반복한다.

</br>

<a href="https://ibb.co/5LdQgCT"><img src="https://i.ibb.co/gJG0LQy/Kakao-Talk-20230313-205050325-28.jpg" alt="Kakao-Talk-20230313-205050325-28" border="0"></a>

</br>

<a href="https://ibb.co/y4NwczK"><img src="https://i.ibb.co/Dr1xHBm/Kakao-Talk-20230313-205050325-29.jpg" alt="Kakao-Talk-20230313-205050325-29" border="0"></a>

</br>

<a href="https://ibb.co/B2Yqk2k"><img src="https://i.ibb.co/XxGSHxH/Kakao-Talk-20230313-205052949.jpg" alt="Kakao-Talk-20230313-205052949" border="0"></a>

</br>

<a href="https://ibb.co/PCZCV0C"><img src="https://i.ibb.co/HgDg93g/Kakao-Talk-20230313-205052949-01.jpg" alt="Kakao-Talk-20230313-205052949-01" border="0"></a>

</br>

<a href="https://ibb.co/qkLDpGY"><img src="https://i.ibb.co/yWmNqTF/Kakao-Talk-20230313-205052949-02.jpg" alt="Kakao-Talk-20230313-205052949-02" border="0"></a>

</br>

<a href="https://ibb.co/JWLK41k"><img src="https://i.ibb.co/FkvKMr7/Kakao-Talk-20230313-205052949-03.jpg" alt="Kakao-Talk-20230313-205052949-03" border="0"></a>

</br>

중심점이 수렴했다. 이번에는 오른쪽 상단과 오른쪽 하단에 위치한 두 개의 데이터 그룹이 하나의 클러스터로 분류된다. k-means법은 임의의 위치에 배치되는 중심점에 의해 클러스터링 결과가 달라지는 성질이 있다.