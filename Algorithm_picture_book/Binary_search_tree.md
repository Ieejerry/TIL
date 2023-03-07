# 이진 탐색 트리(Binary search tree)

</br>

<a href="https://ibb.co/89KDkjh"><img src="https://i.ibb.co/gJjMYDn/Kakao-Talk-20230305-141514022.jpg" alt="Kakao-Talk-20230305-141514022" border="0"></a>

</br>

이진 탐색 트리(binary search tree)는 데이터 구조의 하나이다.

숫자가 적혀 있는 부분을 노드라고 한다. 이진 탐색 트리는 두 가지 성질을 지닌다. 첫 번째 성질은, 모든 노드는 왼쪽 가지에 포함되는 어떤 숫자보다도 큰 숫자가 된다는 것이다.

</br>

<a href="https://ibb.co/VQHDKVs"><img src="https://i.ibb.co/LJQ6GS3/Kakao-Talk-20230305-141514022-01.jpg" alt="Kakao-Talk-20230305-141514022-01" border="0"></a>

</br>

예를 들어 노드9는 그 왼쪽에 있는 가지의 모든 숫자보다 크다.

</br>

<a href="https://ibb.co/BB7MMjF"><img src="https://i.ibb.co/Ttn33Rd/Kakao-Talk-20230305-141514022-02.jpg" alt="Kakao-Talk-20230305-141514022-02" border="0"></a>

</br>

마찬가지로 노드15는 그 왼쪽 가지에 있는 어떤 숫자보다 크다.

</br>

<a href="https://ibb.co/89KDkjh"><img src="https://i.ibb.co/gJjMYDn/Kakao-Talk-20230305-141514022.jpg" alt="Kakao-Talk-20230305-141514022" border="0"></a>

</br>

두 번째 성질은, 모든 노드는 그 노드의 오른쪽 가지에 포함되는 어떤 숫자보다 작은 숫자가 된다는 것이다.

</br>

<a href="https://ibb.co/pPq7fWh"><img src="https://i.ibb.co/RS8F3hj/Kakao-Talk-20230305-141514022-03.jpg" alt="Kakao-Talk-20230305-141514022-03" border="0"></a>

</br>

얘를 들어 노드15는 그 오른쪽 가지에 있는 어떤 수보다도 작다.

</br>

<a href="https://ibb.co/89KDkjh"><img src="https://i.ibb.co/gJjMYDn/Kakao-Talk-20230305-141514022.jpg" alt="Kakao-Talk-20230305-141514022" border="0"></a>

</br>

이 두 개의 성질로부터 다음 조건이 성립된다.

</br>

<a href="https://ibb.co/X2mvsr9"><img src="https://i.ibb.co/mDQMqVm/Kakao-Talk-20230305-141514022-04.jpg" alt="Kakao-Talk-20230305-141514022-04" border="0"></a>

</br>

먼저 이진 탐색 트리의 최소 노드는 최상단에 있는 노드로부터 왼쪽 가지만 계속 따라가면 나오는 가장 끝에 있는 노드가 된다.

</br>

<a href="https://ibb.co/51CkH51"><img src="https://i.ibb.co/4FC2rjF/Kakao-Talk-20230305-141514022-05.jpg" alt="Kakao-Talk-20230305-141514022-05" border="0"></a>

</br>

반대로 이진 탐색 트리에서 최대 노드는 최상단의 노드로부터 오른쪽 가지만 계속 따라가면 나오는 가장 끝에 있는 노드가 된다.

</br>

<a href="https://ibb.co/89KDkjh"><img src="https://i.ibb.co/gJjMYDn/Kakao-Talk-20230305-141514022.jpg" alt="Kakao-Talk-20230305-141514022" border="0"></a>

</br>

이진 탐색 트리에 노드를 추가하는 경우의 순서를 보도록 하겠다.

</br>

<a href="https://ibb.co/BZqnP6r"><img src="https://i.ibb.co/J753dpy/Kakao-Talk-20230305-141514022-06.jpg" alt="Kakao-Talk-20230305-141514022-06" border="0"></a>

</br>

예를 들어 1을 추가하는 경우이다.

</br>

<a href="https://ibb.co/yV1PW0F"><img src="https://i.ibb.co/HXs4n7T/Kakao-Talk-20230305-141514022-07.jpg" alt="Kakao-Talk-20230305-141514022-07" border="0"></a>

</br>

노드 추가 위치를 이진 탐색 트리의 최상단 노드부터 탐색해간다.

</br>

<a href="https://ibb.co/JsXccV7"><img src="https://i.ibb.co/qrbDDKs/Kakao-Talk-20230305-141514022-08.jpg" alt="Kakao-Talk-20230305-141514022-08" border="0"></a>

</br>

1 < 15이므로 왼쪽으로 진행한다.

</br>

<a href="https://ibb.co/jM99bR0"><img src="https://i.ibb.co/SnDD5rY/Kakao-Talk-20230305-141514022-09.jpg" alt="Kakao-Talk-20230305-141514022-09" border="0"></a>

</br>

1 < 9 이므로 왼쪽으로 진행한다.

</br>

<a href="https://ibb.co/QdTnQH3"><img src="https://i.ibb.co/GT8kpM4/Kakao-Talk-20230305-141514022-10.jpg" alt="Kakao-Talk-20230305-141514022-10" border="0"></a>

</br>

1 < 3 이므로 왼쪽으로 진행해야 하지만 노드가 없으므로 새로운 노드로 추가한다.

</br>

<a href="https://ibb.co/PM4GhJy"><img src="https://i.ibb.co/0KZyM1L/Kakao-Talk-20230305-141514022-11.jpg" alt="Kakao-Talk-20230305-141514022-11" border="0"></a>

</br>

이것으로 1 추가 작업이 완료된다.

</br>

<a href="https://ibb.co/tHfsDyf"><img src="https://i.ibb.co/2F2tdX2/Kakao-Talk-20230305-141514022-12.jpg" alt="Kakao-Talk-20230305-141514022-12" border="0"></a>

</br>

다음은 4를 추가해보도록 하겠다.

</br>

<a href="https://ibb.co/TWyJnB0"><img src="https://i.ibb.co/vX9frxd/Kakao-Talk-20230305-141514022-13.jpg" alt="Kakao-Talk-20230305-141514022-13" border="0"></a>

</br>

앞에 예와 마찬가지로 추가할 위치를 찾는다. 이진 탐색 트리의 최상단 노드부터 탐색해간다.

</br>

<a href="https://ibb.co/kKJstLR"><img src="https://i.ibb.co/jhzPSCc/Kakao-Talk-20230305-141514022-14.jpg" alt="Kakao-Talk-20230305-141514022-14" border="0"></a>

</br>

4 < 15 이므로 왼쪽으로 진행한다.

</br>

<a href="https://ibb.co/xqvJgWR"><img src="https://i.ibb.co/0yNh9Td/Kakao-Talk-20230305-141514022-15.jpg" alt="Kakao-Talk-20230305-141514022-15" border="0"></a>

</br>

4 < 9 이므로 왼쪽으로 진행한다.

</br>

<a href="https://ibb.co/fnhZTmt"><img src="https://i.ibb.co/hZPrTpH/Kakao-Talk-20230305-141514022-16.jpg" alt="Kakao-Talk-20230305-141514022-16" border="0"></a>

</br>

4 > 3 이므로 오른쪽으로 진행한다.

</br>

<a href="https://ibb.co/T0cDQfP"><img src="https://i.ibb.co/bv1j40N/Kakao-Talk-20230305-141514022-17.jpg" alt="Kakao-Talk-20230305-141514022-17" border="0"></a>

</br>

4 < 8 이므로 왼쪽으로 진행해야 하지만 왼쪽에 노드가 없으므로 새로운 노드로 추가한다.

</br>

<a href="https://ibb.co/KKCWKqv"><img src="https://i.ibb.co/kmYXm8C/Kakao-Talk-20230305-141514022-18.jpg" alt="Kakao-Talk-20230305-141514022-18" border="0"></a>

</br>

이것으로 4 추가 작업이 완료된다.

이진 탐색 트리에서 노드를 삭제하는 순서를 보도록 하겠다.

</br>

<a href="https://ibb.co/7yTZQVD"><img src="https://i.ibb.co/zfLBFbg/Kakao-Talk-20230305-141514022-19.jpg" alt="Kakao-Talk-20230305-141514022-19" border="0"></a>

</br>

예를 들어 28을 삭제하는 경우를 보겠다.

</br>

<a href="https://ibb.co/rZXXByT"><img src="https://i.ibb.co/0fzz0J8/Kakao-Talk-20230305-141514022-20.jpg" alt="Kakao-Talk-20230305-141514022-20" border="0"></a>

</br>

자식 노드가 없는 노드는 대상 노드를 삭제만 하면 작업이 끝난다.

</br>

<a href="https://ibb.co/DbW2h5V"><img src="https://i.ibb.co/BP3Mbqz/Kakao-Talk-20230305-141514022-21.jpg" alt="Kakao-Talk-20230305-141514022-21" border="0"></a>

</br>

다음은 8을 삭제해보도록 하겠다.

</br>

<a href="https://ibb.co/XjQKPDb"><img src="https://i.ibb.co/DzJvFYt/Kakao-Talk-20230305-141514022-22.jpg" alt="Kakao-Talk-20230305-141514022-22" border="0"></a>

</br>

자식 노드가 하나인 노드를 삭제할 때는 대상 노드를 삭제하고

</br>

<a href="https://ibb.co/yVS6QYq"><img src="https://i.ibb.co/0QtCGFr/Kakao-Talk-20230305-141514022-23.jpg" alt="Kakao-Talk-20230305-141514022-23" border="0"></a>

</br>

삭제한 노드의 위치로 자식 노드를 이동시키면 끝이다.

</br>

<a href="https://ibb.co/9wxb0Xf"><img src="https://i.ibb.co/z83XgcL/Kakao-Talk-20230305-141514022-24.jpg" alt="Kakao-Talk-20230305-141514022-24" border="0"></a>

</br>

마지막으로 9를 삭제해보겠다.

</br>

<a href="https://ibb.co/pdSqMRK"><img src="https://i.ibb.co/QM40TCH/Kakao-Talk-20230305-141514022-25.jpg" alt="Kakao-Talk-20230305-141514022-25" border="0"></a>

</br>

자식 노드가 두 개인 노드를 삭제할 때는 먼저 대상 노드를 삭제하고

</br>

<a href="https://ibb.co/3RJqQfr"><img src="https://i.ibb.co/1zS5jsv/Kakao-Talk-20230305-141514022-26.jpg" alt="Kakao-Talk-20230305-141514022-26" border="0"></a>

</br>

삭제한 노드의 왼쪽 가지에서 최대 노드를 찾습니다.

</br>

<a href="https://ibb.co/HNsF2Pm"><img src="https://i.ibb.co/k3fHyDY/Kakao-Talk-20230305-141514022-27.jpg" alt="Kakao-Talk-20230305-141514022-27" border="0"></a>

</br>

삭제한 노드의 위치로 이동시킨다.

</br>

<a href="https://ibb.co/gmSFxFT"><img src="https://i.ibb.co/jbyZSZM/Kakao-Talk-20230305-141514022-28.jpg" alt="Kakao-Talk-20230305-141514022-28" border="0"></a>

</br>

이것으로 이진 탐색 트리의 두 가지 성질을 유지하면서 노드를 삭제할 수 있었다. 참고로 이동 대상 노드(여기선 4)도 자식 노드를 지니는 경우에는 동일한 처리를 재귀적으로 반복하면 된다. 또한, 이동 대상으로 '왼쪽 가지의 최대 노드'를 사용했지만 반대로 '오른쪽 가지의 최소 노드'를 사용해도 된다.

이번에는 이진 탐색 트리에서 노드를 탐색하는 순서를 보도록 하겠다.

</br>

<a href="https://ibb.co/mRV31nS"><img src="https://i.ibb.co/VLcsrF3/Kakao-Talk-20230305-141514022-29.jpg" alt="Kakao-Talk-20230305-141514022-29" border="0"></a>

</br>

예를 들어 12를 탐색하는 경우를 보겠다.

</br>

<a href="https://ibb.co/0FySH2Q"><img src="https://i.ibb.co/KLxkThm/Kakao-Talk-20230305-141518430.jpg" alt="Kakao-Talk-20230305-141518430" border="0"></a>

</br>

이진 탐색 트리의 최상단 노드부터 탐색을 시작한다.

</br>

<a href="https://ibb.co/X2nNHDq"><img src="https://i.ibb.co/smTk7CZ/Kakao-Talk-20230305-141518430-01.jpg" alt="Kakao-Talk-20230305-141518430-01" border="0"></a>

</br>

12 < 15 이므로 왼쪽으로 진행한다.

</br>

<a href="https://ibb.co/Wvdng1D"><img src="https://i.ibb.co/Sw1NRpQ/Kakao-Talk-20230305-141518430-02.jpg" alt="Kakao-Talk-20230305-141518430-02" border="0"></a>

</br>

12 > 4 이므로 오른쪽으로 진행한다. 12를 발견했다.

</br>

<a href="https://ibb.co/vmtfdQx"><img src="https://i.ibb.co/hHqrdZR/Kakao-Talk-20230305-141518430-03.jpg" alt="Kakao-Talk-20230305-141518430-03" border="0"></a>

</br>

이와 같이 이진 탐색 트리를 사용하면 효율적인 탐색이 가능하다는 것을 알 수 있다.

</br>

<a href="https://ibb.co/Vwy8kbh"><img src="https://i.ibb.co/0sN3z1W/Kakao-Talk-20230305-141518430-04.jpg" alt="Kakao-Talk-20230305-141518430-04" border="0"></a>

</br>

하지만 트리가 직선에 가까운 형태가 되면 선형 탐색과 마찬가지로 탐색 효율이 매우 나빠진다.

</br>

<a href="https://ibb.co/zhNkBKc"><img src="https://i.ibb.co/7Jb9Z7c/Kakao-Talk-20230305-141518430-05.jpg" alt="Kakao-Talk-20230305-141518430-05" border="0"></a>

</br>

한편, 항상 균형을 유지하도록 하는 구조도 있다. 이것을 '자가 균형 이진 탐색 트리(self-balancing binary search tree)'라고 하며 탐색 효율을 유지할 수 있다.