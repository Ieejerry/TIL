# 힙(Heap)

</br>

<a href="https://ibb.co/T0fPQg9"><img src="https://i.ibb.co/s1fsTV8/Kakao-Talk-20230305-134213882.jpg" alt="Kakao-Talk-20230305-134213882" border="0"></a>

</br>

힙(Heap)은 트리 구조의 하나로 '우선순위 큐(priority queue)'를 구현할 때 사용된다.

</br>

<a href="https://ibb.co/R0Bk73t"><img src="https://i.ibb.co/qsW3xNh/Kakao-Talk-20230305-134213882-01.jpg" alt="Kakao-Talk-20230305-134213882-01" border="0"></a>

</br>

우선순위 큐는 데이터 구조의 하니이다.

</br>

<a href="https://ibb.co/Vg9NxmY"><img src="https://i.ibb.co/c63vwLh/Kakao-Talk-20230305-134213882-02.jpg" alt="Kakao-Talk-20230305-134213882-02" border="0"></a>

</br>

우선순위 큐에는 데이터를 자유롭게 추가할 수 있다.

</br>

<a href="https://ibb.co/4NzQjFZ"><img src="https://i.ibb.co/121S90f/Kakao-Talk-20230305-134213882-03.jpg" alt="Kakao-Talk-20230305-134213882-03" border="0"></a>

</br>

반면 데이터를 추출할 때는 최솟값부터 순서대로 선택된다.

</br>

<a href="https://ibb.co/9hD44TS"><img src="https://i.ibb.co/Jq1pp7g/Kakao-Talk-20230305-134213882-04.jpg" alt="Kakao-Talk-20230305-134213882-04" border="0"></a>

</br>

추가는 자유롭게 하고 추출할 때는 작은 값부터 꺼내는 것이 우선순위 큐이다.

</br>

<a href="https://ibb.co/h7RNYhq"><img src="https://i.ibb.co/xCSbFP4/Kakao-Talk-20230305-134213882-05.jpg" alt="Kakao-Talk-20230305-134213882-05" border="0"></a>

</br>

그러면 힙 구조를 보도록 하겠다.

자식 노드의 숫자느 반드시 부모의 숫자보다 커야한다는 규칙이 있다.

</br>

<a href="https://ibb.co/DGbTyQK"><img src="https://i.ibb.co/VHN5ZTB/Kakao-Talk-20230305-134213882-06.jpg" alt="Kakao-Talk-20230305-134213882-06" border="0"></a>

</br>

힙에 숫자를 추가하는 경우를 보겠다.

</br>

<a href="https://ibb.co/x5LbgZd"><img src="https://i.ibb.co/gg98WYh/Kakao-Talk-20230305-134213882-07.jpg" alt="Kakao-Talk-20230305-134213882-07" border="0"></a>

</br>

추가되는 수는 먼저 가장 후미에 저장된다.

</br>

<a href="https://ibb.co/t4925GC"><img src="https://i.ibb.co/37nFH3h/Kakao-Talk-20230305-134213882-08.jpg" alt="Kakao-Talk-20230305-134213882-08" border="0"></a>

</br>

부모의 숫자가 큰 때는 부모와 자식을 교환한다.

</br>

<a href="https://ibb.co/3ynHwZL"><img src="https://i.ibb.co/5WPVdHf/Kakao-Talk-20230305-134213882-09.jpg" alt="Kakao-Talk-20230305-134213882-09" border="0"></a>

</br>

부모6 > 자식5이므로 숫자를 교환했다. 이런 처리를 교환이 발생하지 않을 때까지 반복한다.

</br>

<a href="https://ibb.co/GPdYsSn"><img src="https://i.ibb.co/4NFvsrK/Kakao-Talk-20230305-134213882-10.jpg" alt="Kakao-Talk-20230305-134213882-10" border="0"></a>

</br>

부모1 < 자식5이므로 부모의 숫자가 작다. 따라서 교환이 발생하지 않는다.

</br>

<a href="https://ibb.co/x7GHRTq"><img src="https://i.ibb.co/z4bJ0vV/Kakao-Talk-20230305-134213882-11.jpg" alt="Kakao-Talk-20230305-134213882-11" border="0"></a>

</br>

이것으로 힙에 숫자 추가가 완료된다.

</br>

<a href="https://ibb.co/d63p4dK"><img src="https://i.ibb.co/Y8KdBzj/Kakao-Talk-20230305-134213882-12.jpg" alt="Kakao-Talk-20230305-134213882-12" border="0"></a>

</br>

<a href="https://ibb.co/Qv73YSt"><img src="https://i.ibb.co/PGsv1X0/Kakao-Talk-20230305-134213882-13.jpg" alt="Kakao-Talk-20230305-134213882-13" border="0"></a>

</br>

힙에서 숫자를 꺼낼 때는 가장 위에 있는 숫자가 추출된다. 가장 위에 있는 숫자가 없어졌으므로 힙의 구조를 다시 정리해야 한다.

</br>

<a href="https://ibb.co/Q6dFjyT"><img src="https://i.ibb.co/zSJhHqB/Kakao-Talk-20230305-134213882-14.jpg" alt="Kakao-Talk-20230305-134213882-14" border="0"></a>

</br>

가장 후미에 있는 숫자를 가장 위로 이동한다.

</br>

<a href="https://ibb.co/SdcPcNB"><img src="https://i.ibb.co/b2FPF1X/Kakao-Talk-20230305-134213882-15.jpg" alt="Kakao-Talk-20230305-134213882-15" border="0"></a>

</br>

부모 숫자보다 자식 숫자가 작은 경우는 자식의 좌우에 있는 숫자 중 더 작은 쪽과 교환한다.

</br>

<a href="https://ibb.co/XxJTYfj"><img src="https://i.ibb.co/zVfw6WQ/Kakao-Talk-20230305-134213882-16.jpg" alt="Kakao-Talk-20230305-134213882-16" border="0"></a>

</br>

부모6 > 자식(우)5 > 자식(좌)3 이므로 왼쪽 자식과 부모를 교환한다.

</br>

<a href="https://ibb.co/9g37ph0"><img src="https://i.ibb.co/yPBrNpC/Kakao-Talk-20230305-134213882-17.jpg" alt="Kakao-Talk-20230305-134213882-17" border="0"></a>

</br>

이 처리를 교환이 발생하지 않을 때까지 반복한다.

</br>

<a href="https://ibb.co/X2MN3Px"><img src="https://i.ibb.co/JBg0yTj/Kakao-Talk-20230305-134213882-18.jpg" alt="Kakao-Talk-20230305-134213882-18" border="0"></a>

</br>

자식(우)8 > 부모6 > 자식(좌)4 이므로 왼쪽 자식과 부모를 교환한다.

</br>

<a href="https://ibb.co/4WHJQp9"><img src="https://i.ibb.co/6YkNdFV/Kakao-Talk-20230305-134213882-19.jpg" alt="Kakao-Talk-20230305-134213882-19" border="0"></a>

</br>

이것으로 숫자 추출 처리가 완료되었다. 이처럼 힙을 사용하면 최솟값을 빠르게 추출할 수 있다. 단, 도중에 있는 데이터를 추출할 수는 없다. 힙은 우선순위 큐나 다익스트라 기법 등에서도 사용되고 있다.