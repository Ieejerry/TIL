# 이분 탐색(Binary search)

</br>

<a href="https://ibb.co/5XQHrMc"><img src="https://i.ibb.co/cKWn6gT/Kakao-Talk-20230314-221343309.jpg" alt="Kakao-Talk-20230314-221343309" border="0"></a>

</br>

이분 탐색은 정렬된 배열에서 데이터를 탐색하는 알고리즘이다.

숫자 6을 탐색해보겠다.

</br>

<a href="https://ibb.co/stM3gdb"><img src="https://i.ibb.co/6Nfsy7r/Kakao-Talk-20230314-221343309-01.jpg" alt="Kakao-Talk-20230314-221343309-01" border="0"></a>

</br>

먼저 배열의 정중앙에 있는 수를 찾는다. 여기선 5가 된다.

</br>

<a href="https://ibb.co/Rvr0gMJ"><img src="https://i.ibb.co/NVDjFkG/Kakao-Talk-20230314-221343309-02.jpg" alt="Kakao-Talk-20230314-221343309-02" border="0"></a>

</br>

5와 탐색할 수인 6을 비교한다. 5 < 6 이므로 6은 5보다 오른쪽에 잇다는 것을 알 수 있다.

</br>

<a href="https://ibb.co/FnFhjD2"><img src="https://i.ibb.co/cxjy7r0/Kakao-Talk-20230314-221343309-03.jpg" alt="Kakao-Talk-20230314-221343309-03" border="0"></a>

</br>

<a href="https://ibb.co/Cnsr1qz"><img src="https://i.ibb.co/sFJBmh2/Kakao-Talk-20230314-221343309-04.jpg" alt="Kakao-Talk-20230314-221343309-04" border="0"></a>

</br>

필요가 없어진 숫자는 후보에서 제외힌다.

</br>

<a href="https://ibb.co/5MLhGhy"><img src="https://i.ibb.co/8K9gNgp/Kakao-Talk-20230314-221343309-05.jpg" alt="Kakao-Talk-20230314-221343309-05" border="0"></a>

</br>

남은 배열의 정중앙에 있는 수를 찾는다. 여기서 7이 된다.

</br>

<a href="https://ibb.co/wynxykY"><img src="https://i.ibb.co/CBjTBcW/Kakao-Talk-20230314-221343309-06.jpg" alt="Kakao-Talk-20230314-221343309-06" border="0"></a>

</br>

7과 6을 비교한다. 6 < 7 이므로 5은 7보다 왼쪽에 있다는 것을 알 수 있다.

</br>

<a href="https://ibb.co/YcKSYzz"><img src="https://i.ibb.co/CbXyNkk/Kakao-Talk-20230314-221343309-07.jpg" alt="Kakao-Talk-20230314-221343309-07" border="0"></a>

</br>

<a href="https://ibb.co/TcxZVGg"><img src="https://i.ibb.co/BL5mXJC/Kakao-Talk-20230314-221343309-08.jpg" alt="Kakao-Talk-20230314-221343309-08" border="0"></a>

</br>

필요 없어진 숫자를 후보에서 제외한다.

</br>

<a href="https://ibb.co/cF8kF8X"><img src="https://i.ibb.co/gTWmTWF/Kakao-Talk-20230314-221343309-09.jpg" alt="Kakao-Talk-20230314-221343309-09" border="0"></a>

</br>

남은 배열의 정중앙에 있는 수를 찾는다. 여기서 6이 된다. 6 = 6으로 대상 숫자를 발견했다.

이진 탐색은 배열이 정렬돼 있다는 것을 활용해서 탐색할 범위를 매번 반씩 줄여나갈 수 있다.