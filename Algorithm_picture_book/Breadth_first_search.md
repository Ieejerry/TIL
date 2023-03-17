# 너비 우선 탐색(Breath first search)

</br>

<a href="https://ibb.co/C1M06M3"><img src="https://i.ibb.co/f1n09nz/Kakao-Talk-20230314-224342054.jpg" alt="Kakao-Talk-20230314-224342054" border="0"></a>

</br>

너비 우선 탐색은 그래프를 탐색하는 알고리즘이다.

</br>

<a href="https://ibb.co/GFYCwJs"><img src="https://i.ibb.co/N7DWh31/Kakao-Talk-20230314-224342054-01.jpg" alt="Kakao-Talk-20230314-224342054-01" border="0"></a>

</br>

A를 시작점, G를 목표로 해서 탐색을 시작한다.

</br>

<a href="https://ibb.co/KNYVWbT"><img src="https://i.ibb.co/jVd3Dbn/Kakao-Talk-20230314-224342054-02.jpg" alt="Kakao-Talk-20230314-224342054-02" border="0"></a>

</br>

A에서 도달할 수 있는 정점 B, C, D가 다음 이동 대상 후보가 된다.

</br>

<a href="https://ibb.co/Vv59P0n"><img src="https://i.ibb.co/fCLFPV6/Kakao-Talk-20230314-224342054-03.jpg" alt="Kakao-Talk-20230314-224342054-03" border="0"></a>

</br>

후보들 중에서 하나의 정점을 선택한다. 선택 기준은 후보 중 가장 먼저 후부에 추가된 것으로 한다. 동일한 시점에 후보가 된 정점의 경우에는 아무거나 선택해도 된다. 여기서는 왼쪽에 있는 정점부터 선택하도록 한다.

</br>

<a href="https://ibb.co/q5ThKgb"><img src="https://i.ibb.co/JQD8VpX/Kakao-Talk-20230314-224342054-04.jpg" alt="Kakao-Talk-20230314-224342054-04" border="0"></a>

</br>

모두 동일한 시점에 후보가 됐으므로 B를 선택한다.

</br>

<a href="https://ibb.co/WnhB1p6"><img src="https://i.ibb.co/XXQFTkb/Kakao-Talk-20230314-224342054-05.jpg" alt="Kakao-Talk-20230314-224342054-05" border="0"></a>

</br>

선택한 정점으로 이동한다.

</br>

<a href="https://ibb.co/wSZ8xqs"><img src="https://i.ibb.co/3p5VLbz/Kakao-Talk-20230314-224342054-06.jpg" alt="Kakao-Talk-20230314-224342054-06" border="0"></a>

</br>

현재 B에서 도달할 수 있는 E와 F가 새로운 후보로 추가된다.

</br>

<a href="https://ibb.co/M1dStM0"><img src="https://i.ibb.co/X5HLKSR/Kakao-Talk-20230314-224342054-07.jpg" alt="Kakao-Talk-20230314-224342054-07" border="0"></a>

</br>

후보 정점은 '선입선출(FIFO)' 구조로 관리하므로 '큐' 데이터 구조를 이용할 수 있다.

</br>

<a href="https://ibb.co/zPHyJxL"><img src="https://i.ibb.co/L9hL5Rq/Kakao-Talk-20230314-224342054-08.jpg" alt="Kakao-Talk-20230314-224342054-08" border="0"></a>

</br>

후보 중에서 가장 먼저 추가된 것은 C와 D이다. 이 중에서 왼쪽 C를 선택한다.

</br>

<a href="https://ibb.co/pv9GNPw"><img src="https://i.ibb.co/tMWknhK/Kakao-Talk-20230314-224342054-09.jpg" alt="Kakao-Talk-20230314-224342054-09" border="0"></a>

</br>

선택한 정점으로 이동한다.

</br>

<a href="https://ibb.co/fG6SFg9"><img src="https://i.ibb.co/6J9ZwM8/Kakao-Talk-20230314-224342054-10.jpg" alt="Kakao-Talk-20230314-224342054-10" border="0"></a>

</br>

현재 위치인 C에서 도달할 수 있는 H를 새로운 후보로 추가한다.

</br>

<a href="https://ibb.co/mG3VnkW"><img src="https://i.ibb.co/KXJptdv/Kakao-Talk-20230314-224342054-11.jpg" alt="Kakao-Talk-20230314-224342054-11" border="0"></a>

</br>

동일한 작업을 목표에 도달하거나 모든 정점의 탐색이 끝날 때까지 반복한다.

</br>

<a href="https://ibb.co/NxJTqjr"><img src="https://i.ibb.co/MntBHVf/Kakao-Talk-20230314-224342054-12.jpg" alt="Kakao-Talk-20230314-224342054-12" border="0"></a>

</br>

<a href="https://ibb.co/fG4y5KQ"><img src="https://i.ibb.co/Dg5vy6L/Kakao-Talk-20230314-224342054-13.jpg" alt="Kakao-Talk-20230314-224342054-13" border="0"></a>

</br>

<a href="https://ibb.co/bbYPRMB"><img src="https://i.ibb.co/6XGmJ7P/Kakao-Talk-20230314-224342054-14.jpg" alt="Kakao-Talk-20230314-224342054-14" border="0"></a>

</br>

<a href="https://ibb.co/Ht3rkxM"><img src="https://i.ibb.co/7nLG6RT/Kakao-Talk-20230314-224342054-15.jpg" alt="Kakao-Talk-20230314-224342054-15" border="0"></a>

</br>

<a href="https://ibb.co/NF2kNgs"><img src="https://i.ibb.co/x2qcgKD/Kakao-Talk-20230314-224342054-16.jpg" alt="Kakao-Talk-20230314-224342054-16" border="0"></a>

</br>

<a href="https://ibb.co/ygj6JfN"><img src="https://i.ibb.co/ZcDBCLf/Kakao-Talk-20230314-224342054-17.jpg" alt="Kakao-Talk-20230314-224342054-17" border="0"></a>

</br>

<a href="https://ibb.co/Rj6RsQk"><img src="https://i.ibb.co/sW18Nsd/Kakao-Talk-20230314-224342054-18.jpg" alt="Kakao-Talk-20230314-224342054-18" border="0"></a>

</br>

<a href="https://ibb.co/DgGbtfs"><img src="https://i.ibb.co/2Y86y3m/Kakao-Talk-20230314-224342054-19.jpg" alt="Kakao-Talk-20230314-224342054-19" border="0"></a>

</br>

<a href="https://ibb.co/WtKzZKH"><img src="https://i.ibb.co/TLh06hw/Kakao-Talk-20230314-224342054-20.jpg" alt="Kakao-Talk-20230314-224342054-20" border="0"></a>

</br>

<a href="https://ibb.co/W3BjTkP"><img src="https://i.ibb.co/RSQd53B/Kakao-Talk-20230314-224342054-21.jpg" alt="Kakao-Talk-20230314-224342054-21" border="0"></a>

</br>

<a href="https://ibb.co/wY1vxm3"><img src="https://i.ibb.co/4JxQ5r9/Kakao-Talk-20230314-224342054-22.jpg" alt="Kakao-Talk-20230314-224342054-22" border="0"></a>

</br>

<a href="https://ibb.co/JdgsWx7"><img src="https://i.ibb.co/KGSrcNq/Kakao-Talk-20230314-224342054-23.jpg" alt="Kakao-Talk-20230314-224342054-23" border="0"></a>

</br>

<a href="https://ibb.co/3kZ9phy"><img src="https://i.ibb.co/SJC4tvX/Kakao-Talk-20230314-224342054-24.jpg" alt="Kakao-Talk-20230314-224342054-24" border="0"></a>

</br>

<a href="https://ibb.co/Wg8Fr2k"><img src="https://i.ibb.co/0h4Z0GC/Kakao-Talk-20230314-224342054-25.jpg" alt="Kakao-Talk-20230314-224342054-25" border="0"></a>

</br>

<a href="https://ibb.co/Xpdnr7L"><img src="https://i.ibb.co/ftK3zkF/Kakao-Talk-20230314-224342054-26.jpg" alt="Kakao-Talk-20230314-224342054-26" border="0"></a>

</br>

<a href="https://ibb.co/QXsB6kX"><img src="https://i.ibb.co/stLSFCt/Kakao-Talk-20230314-224342054-27.jpg" alt="Kakao-Talk-20230314-224342054-27" border="0"></a>

</br>

<a href="https://ibb.co/hMdBhsC"><img src="https://i.ibb.co/X457NXV/Kakao-Talk-20230314-224342054-28.jpg" alt="Kakao-Talk-20230314-224342054-28" border="0"></a>

</br>

<a href="https://ibb.co/T47JMmZ"><img src="https://i.ibb.co/R3stTz1/Kakao-Talk-20230314-224342054-29.jpg" alt="Kakao-Talk-20230314-224342054-29" border="0"></a>

</br>

<a href="https://ibb.co/nwc3RQ0"><img src="https://i.ibb.co/L0tQv9P/Kakao-Talk-20230314-224348876.jpg" alt="Kakao-Talk-20230314-224348876" border="0"></a>

</br>

<a href="https://ibb.co/kmtGDWP"><img src="https://i.ibb.co/TWsw0FN/Kakao-Talk-20230314-224348876-01.jpg" alt="Kakao-Talk-20230314-224348876-01" border="0"></a>

</br>

<a href="https://ibb.co/CwVy729"><img src="https://i.ibb.co/rQ5h6sp/Kakao-Talk-20230314-224348876-02.jpg" alt="Kakao-Talk-20230314-224348876-02" border="0"></a>

</br>

<a href="https://ibb.co/hFy3PJb"><img src="https://i.ibb.co/0ycHgRT/Kakao-Talk-20230314-224348876-03.jpg" alt="Kakao-Talk-20230314-224348876-03" border="0"></a>

</br>

<a href="https://ibb.co/6yx1mgV"><img src="https://i.ibb.co/fX5n24B/Kakao-Talk-20230314-224348876-04.jpg" alt="Kakao-Talk-20230314-224348876-04" border="0"></a>

</br>

<a href="https://ibb.co/khdR5gc"><img src="https://i.ibb.co/Cnrkm50/Kakao-Talk-20230314-224348876-05.jpg" alt="Kakao-Talk-20230314-224348876-05" border="0"></a>

</br>

목표에 도달했으므로 탐색을 종료한다.

이와 같이 너비 우선 탐색은 시작점부터 가까운 순으로 너비를 넓혀 가며 탐색을 하는 방식이다.