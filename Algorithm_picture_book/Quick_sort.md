# 퀵 정렬(Quick sort)

</br>

<a href="https://ibb.co/8YkGj4P"><img src="https://i.ibb.co/wct8Krp/Kakao-Talk-20230312-114646728.jpg" alt="Kakao-Talk-20230312-114646728" border="0"></a>

</br>

퀵 정렬은 수열을 정렬하는 알고리즘 중 하나이다. 다른 알고리즘에 비해 비교 및 교환 횟수가 적은 것이 특징으로 대부분의 경우 빠른 속도로 정렬할 수 있다.

그러면 실제로 알고리즘의 과정을 보도록 하겠다.

</br>

<a href="https://ibb.co/WvVkLKW"><img src="https://i.ibb.co/b5bskdg/Kakao-Talk-20230312-114646728-01.jpg" alt="Kakao-Talk-20230312-114646728-01" border="0"></a>

</br>

처음 작업 대상은 모든 숫자이다.

</br>

<a href="https://ibb.co/kyGdMKK"><img src="https://i.ibb.co/59172TT/Kakao-Talk-20230312-114646728-02.jpg" alt="Kakao-Talk-20230312-114646728-02" border="0"></a>

</br>

정렬 기준이 되는 숫자를 하나 선택한다. 이 숫자를 피봇(pivot)이라고 부른다. 피봇은 보통 하나의 숫자를 랜덤으로 선택한 것이다. 여기서는 편의상 항상 가장 오른쪽에 있는 수를 피봇으로 선택하고 있다.

</br>

<a href="https://ibb.co/ZSWS6Lj"><img src="https://i.ibb.co/HCnCDFS/Kakao-Talk-20230312-114646728-03.jpg" alt="Kakao-Talk-20230312-114646728-03" border="0"></a>

</br>

알기 쉽게 피봇에 마커를 표시한다.

</br>

<a href="https://ibb.co/rsYbh0k"><img src="https://i.ibb.co/RyfhKb2/Kakao-Talk-20230312-114646728-04.jpg" alt="Kakao-Talk-20230312-114646728-04" border="0"></a>

</br>

계속해서 가장 왼쪽 수에 왼쪽 마커, 오른쪽 수의 오른쪽 마커를 표시한다. 퀵 정렬은 이 마커들을 사용해서 일련의 작업을 재귀적으로 반복하는 알고리즘이다.

</br>

<a href="https://ibb.co/3Cq5Lhd"><img src="https://i.ibb.co/6Wxcfsw/Kakao-Talk-20230312-114646728-05.jpg" alt="Kakao-Talk-20230312-114646728-05" border="0"></a>

</br>

<a href="https://ibb.co/X7BgCMR"><img src="https://i.ibb.co/n72vLtJ/Kakao-Talk-20230312-114646728-06.jpg" alt="Kakao-Talk-20230312-114646728-06" border="0"></a>

</br>

왼쪽 마커를 오른쪽으로 이동한다. 왼쪽 마커가 피봇 수 이상인 수에 도착하면 멈춘다.

</br>

<a href="https://ibb.co/C0mFXS5"><img src="https://i.ibb.co/F7mtfdb/Kakao-Talk-20230312-114646728-07.jpg" alt="Kakao-Talk-20230312-114646728-07" border="0"></a>

</br>

8 >= 6 이므로 정지한다. 계속해서 오른쪽 마커를 왼쪽으로 이동한다. 오른쪽 마커는 피봇보다 작은 숫자에 도달하면 멈춘다.

</br>

<a href="https://ibb.co/4dK478k"><img src="https://i.ibb.co/9tcyNbP/Kakao-Talk-20230312-114646728-08.jpg" alt="Kakao-Talk-20230312-114646728-08" border="0"></a>

</br>

<a href="https://ibb.co/wwwBKsX"><img src="https://i.ibb.co/hZZLKfj/Kakao-Talk-20230312-114646728-09.jpg" alt="Kakao-Talk-20230312-114646728-09" border="0"></a>

</br>

4 < 6 이므로 정지한다.

</br>

<a href="https://ibb.co/0rDggWC"><img src="https://i.ibb.co/x6Cppc1/Kakao-Talk-20230312-114646728-10.jpg" alt="Kakao-Talk-20230312-114646728-10" border="0"></a>

</br>

좌우 마커가 멈춘 시점에서 마커의 숫자를 교체한다. 이와 같이 왼쪽 마커의 역할은 피봇 이상인 수를 발견하는 것이고 오른쪽 마커의 역할은 피봇보다 작은 수를 발견하는 것이다. 숫자를 바꾸므로 수열의 왼쪽에 피봇보다 작은 수, 오른쪽에 피봇 이상인 수를 모을 수 있다.

교체한 후에는 다시 왼쪽 마커를 오른쪽으로 이동한다. 앞서 본 것처럼 왼쪽 마커는 피봇 숫자보다 이상인 수에 도달하면 멈춘다.

</br>

<a href="https://ibb.co/W2p6KP4"><img src="https://i.ibb.co/BCKtsr5/Kakao-Talk-20230312-114646728-11.jpg" alt="Kakao-Talk-20230312-114646728-11" border="0"></a>

</br>

<a href="https://ibb.co/1XT935G"><img src="https://i.ibb.co/t2DbStp/Kakao-Talk-20230312-114646728-12.jpg" alt="Kakao-Talk-20230312-114646728-12" border="0"></a>

</br>

<a href="https://ibb.co/VSv9MhQ"><img src="https://i.ibb.co/xjMLzcf/Kakao-Talk-20230312-114646728-13.jpg" alt="Kakao-Talk-20230312-114646728-13" border="0"></a>

</br>

<a href="https://ibb.co/x82cBHH"><img src="https://i.ibb.co/CswXY22/Kakao-Talk-20230312-114646728-14.jpg" alt="Kakao-Talk-20230312-114646728-14" border="0"></a>

</br>

9 >= 6 이므로 정지한다. 계속해서 오른쪽 마커

</br>

<a href="https://ibb.co/gDDZbgR"><img src="https://i.ibb.co/LCCdDpZ/Kakao-Talk-20230312-114646728-15.jpg" alt="Kakao-Talk-20230312-114646728-15" border="0"></a>

</br>

<a href="https://ibb.co/6NtJf81"><img src="https://i.ibb.co/cx8X7wC/Kakao-Talk-20230312-114646728-16.jpg" alt="Kakao-Talk-20230312-114646728-16" border="0"></a>

</br>

오른쪽 마커가 왼쪽 마커와 만날 때도 동작을 멈춘다.

좌우 마커가 정지했을 때 동일한 위치인 경우 해당 수를 피봇 수와 교체한다.

</br>

<a href="https://ibb.co/LPwYyPF"><img src="https://i.ibb.co/hM5LNM6/Kakao-Talk-20230312-114646728-17.jpg" alt="Kakao-Talk-20230312-114646728-17" border="0"></a>

</br>

<a href="https://ibb.co/MsgkQ4p"><img src="https://i.ibb.co/g3rZhpw/Kakao-Talk-20230312-114646728-18.jpg" alt="Kakao-Talk-20230312-114646728-18" border="0"></a>

</br>

좌우 마커가 있는 수를 정렬 완료 상태로 둔다. 이것으로 첫 작업이 완료된다.

</br>

<a href="https://ibb.co/ZTqWXh8"><img src="https://i.ibb.co/7ys2CGW/Kakao-Talk-20230312-114646728-19.jpg" alt="Kakao-Talk-20230312-114646728-19" border="0"></a>

</br>

일련에 작업에 의해 수열을 피봇의 왼쪽에는 '피봇보다 작은 수'로

</br>

<a href="https://ibb.co/NKj77P0"><img src="https://i.ibb.co/w4WYYXn/Kakao-Talk-20230312-114646728-20.jpg" alt="Kakao-Talk-20230312-114646728-20" border="0"></a>

</br>

피봇의 오른쪽에는 '피봇보다 큰 수'로 나눌 수 있다. 둘로 나누어진 수열에 대해 일련의 작업을 재귀적으로 반복한다.

</br>

<a href="https://ibb.co/yd3V6yc"><img src="https://i.ibb.co/Kb1m2qp/Kakao-Talk-20230312-114646728-21.jpg" alt="Kakao-Talk-20230312-114646728-21" border="0"></a>

</br>

다음은 왼쪽에 있는 수열을 작업 대상으로 한다.

</br>

<a href="https://ibb.co/vwpG5wt"><img src="https://i.ibb.co/NV5PhV4/Kakao-Talk-20230312-114646728-22.jpg" alt="Kakao-Talk-20230312-114646728-22" border="0"></a>

</br>

세 개의 마커를 표시한다. 동일한 방법으로 작업을 진행한다.

</br>

<a href="https://ibb.co/JdDHHwZ"><img src="https://i.ibb.co/xsx66tZ/Kakao-Talk-20230312-114646728-23.jpg" alt="Kakao-Talk-20230312-114646728-23" border="0"></a>

</br>

<a href="https://ibb.co/z44t8kL"><img src="https://i.ibb.co/7110g9T/Kakao-Talk-20230312-114646728-24.jpg" alt="Kakao-Talk-20230312-114646728-24" border="0"></a>

</br>

<a href="https://ibb.co/S0rZTV2"><img src="https://i.ibb.co/gwVc1tG/Kakao-Talk-20230312-114646728-25.jpg" alt="Kakao-Talk-20230312-114646728-25" border="0"></a>

</br>

<a href="https://ibb.co/1MFhKrX"><img src="https://i.ibb.co/ypHG56k/Kakao-Talk-20230312-114646728-26.jpg" alt="Kakao-Talk-20230312-114646728-26" border="0"></a>

</br>

<a href="https://ibb.co/jZj3Yjh"><img src="https://i.ibb.co/PzV1yVx/Kakao-Talk-20230312-114646728-27.jpg" alt="Kakao-Talk-20230312-114646728-27" border="0"></a>

</br>

<a href="https://ibb.co/cY6bFPJ"><img src="https://i.ibb.co/tLqZsSB/Kakao-Talk-20230312-114646728-28.jpg" alt="Kakao-Talk-20230312-114646728-28" border="0"></a>

</br>

<a href="https://ibb.co/2F4r13R"><img src="https://i.ibb.co/3TZb9mV/Kakao-Talk-20230312-114646728-29.jpg" alt="Kakao-Talk-20230312-114646728-29" border="0"></a>

</br>

<a href="https://ibb.co/cywTc0S"><img src="https://i.ibb.co/RgNHpfk/Kakao-Talk-20230312-114707162.jpg" alt="Kakao-Talk-20230312-114707162" border="0"></a>

</br>

<a href="https://ibb.co/cvwMzQF"><img src="https://i.ibb.co/QckzsMN/Kakao-Talk-20230312-114707162-01.jpg" alt="Kakao-Talk-20230312-114707162-01" border="0"></a>

</br>

<a href="https://ibb.co/q9wx1VD"><img src="https://i.ibb.co/nfSRktw/Kakao-Talk-20230312-114707162-02.jpg" alt="Kakao-Talk-20230312-114707162-02" border="0"></a>

</br>

<a href="https://ibb.co/7p1ggc7"><img src="https://i.ibb.co/mycvvsQ/Kakao-Talk-20230312-114707162-03.jpg" alt="Kakao-Talk-20230312-114707162-03" border="0"></a>

</br>

일련의 작업이 끝나면 피봇의 왼쪽에는 '피봇보다 작은 수'로

</br>

<a href="https://ibb.co/Dz0dYxZ"><img src="https://i.ibb.co/8N1kbWH/Kakao-Talk-20230312-114707162-04.jpg" alt="Kakao-Talk-20230312-114707162-04" border="0"></a>

</br>

피봇의 오른쪽에는 '피봇보다 큰 수'로 나눌 수 있다.

</br>

<a href="https://ibb.co/wJrsw6S"><img src="https://i.ibb.co/hX1fZ8B/Kakao-Talk-20230312-114707162-05.jpg" alt="Kakao-Talk-20230312-114707162-05" border="0"></a>

</br>

다시 재귀적으로 위의 작업을 반복한다. 왼쪽에 있는 수열을 작업 대상으로 한다.

</br>

<a href="https://ibb.co/CvSxd3r"><img src="https://i.ibb.co/HY9mvfJ/Kakao-Talk-20230312-114707162-06.jpg" alt="Kakao-Talk-20230312-114707162-06" border="0"></a>

</br>

대상 수열의 수가 하나인 경우 정렬이 완료된다.

</br>

<a href="https://ibb.co/XZDWkpd"><img src="https://i.ibb.co/BVGfKj7/Kakao-Talk-20230312-114707162-07.jpg" alt="Kakao-Talk-20230312-114707162-07" border="0"></a>

</br>

두 번째 작업에서 나누어진 수열의 오른쪽을 작업 대상으로 한다.

</br>

<a href="https://ibb.co/4NJLqXp"><img src="https://i.ibb.co/SvJgjMB/Kakao-Talk-20230312-114707162-08.jpg" alt="Kakao-Talk-20230312-114707162-08" border="0"></a>

</br>

세 개의 마커를 표시한다.

</br>

<a href="https://ibb.co/ckQgtFh"><img src="https://i.ibb.co/gmJjwTZ/Kakao-Talk-20230312-114707162-09.jpg" alt="Kakao-Talk-20230312-114707162-09" border="0"></a>

</br>

왼쪽 마커를 오른쪽으로 이동한다.

</br>

<a href="https://ibb.co/wB2Ynb0"><img src="https://i.ibb.co/gmc60Xj/Kakao-Talk-20230312-114707162-10.jpg" alt="Kakao-Talk-20230312-114707162-10" border="0"></a>

</br>

왼쪽 마커가 오른쪽 마커와 만나도 멈추지 않는다. 이것은 오른쪽 마커의 움직임과 다르다.

</br>

<a href="https://ibb.co/tX3dpKt"><img src="https://i.ibb.co/L5vGdRW/Kakao-Talk-20230312-114707162-11.jpg" alt="Kakao-Talk-20230312-114707162-11" border="0"></a>

</br>

왼쪽 마커는 작업 대상 수열의 오른쪽 끝에 도달하면 멈춘다. 이때 작업 대상 범위 내에서 피봇인 수가 가장 큰 수가 된다.

</br>

<a href="https://ibb.co/TcvqXmw"><img src="https://i.ibb.co/fM1GR4X/Kakao-Talk-20230312-114707162-12.jpg" alt="Kakao-Talk-20230312-114707162-12" border="0"></a>

</br>

다음은 오른쪽 마커를 이동하지만 왼쪽 마커에 추월당한 경우에는 움직이지 않고 종료한다.

</br>

<a href="https://ibb.co/m9NVGrK"><img src="https://i.ibb.co/F5HLKk1/Kakao-Talk-20230312-114707162-13.jpg" alt="Kakao-Talk-20230312-114707162-13" border="0"></a>

</br>

왼쪽 마커가 작업 대상의 오른쪽 끝에 도달한 경우, 피봇 수를 정렬 완료 상태로 두고 일련의 작업을 종료한다.

</br>

<a href="https://ibb.co/r3HnTcp"><img src="https://i.ibb.co/ScBqWdm/Kakao-Talk-20230312-114707162-14.jpg" alt="Kakao-Talk-20230312-114707162-14" border="0"></a>

</br>

이후로는 동일한 작업을 모든 수가 정렬 완료 상태가 될 때까지 반복하면 된다.

</br>

<a href="https://ibb.co/6wRSb8L"><img src="https://i.ibb.co/NC6qprb/Kakao-Talk-20230312-114707162-15.jpg" alt="Kakao-Talk-20230312-114707162-15" border="0"></a>

</br>

<a href="https://ibb.co/VmgvdF0"><img src="https://i.ibb.co/m89Hmnr/Kakao-Talk-20230312-114707162-16.jpg" alt="Kakao-Talk-20230312-114707162-16" border="0"></a>

</br>

<a href="https://ibb.co/gtW1pWn"><img src="https://i.ibb.co/NWNhPN4/Kakao-Talk-20230312-114707162-17.jpg" alt="Kakao-Talk-20230312-114707162-17" border="0"></a>

</br>

<a href="https://ibb.co/PgPCnHm"><img src="https://i.ibb.co/zZBfYvn/Kakao-Talk-20230312-114707162-18.jpg" alt="Kakao-Talk-20230312-114707162-18" border="0"></a>

</br>

<a href="https://ibb.co/s3NcCnx"><img src="https://i.ibb.co/2KCRSxV/Kakao-Talk-20230312-114707162-19.jpg" alt="Kakao-Talk-20230312-114707162-19" border="0"></a>

</br>

<a href="https://ibb.co/W6Ktn1K"><img src="https://i.ibb.co/Qfmd9Gm/Kakao-Talk-20230312-114707162-20.jpg" alt="Kakao-Talk-20230312-114707162-20" border="0"></a>

</br>

<a href="https://ibb.co/q1vtNW0"><img src="https://i.ibb.co/s3Z0K65/Kakao-Talk-20230312-114707162-21.jpg" alt="Kakao-Talk-20230312-114707162-21" border="0"></a>

</br>

<a href="https://ibb.co/swZtw2X"><img src="https://i.ibb.co/VSs3Stk/Kakao-Talk-20230312-114707162-22.jpg" alt="Kakao-Talk-20230312-114707162-22" border="0"></a>

</br>

<a href="https://ibb.co/w4Tjv1b"><img src="https://i.ibb.co/L1MHGfq/Kakao-Talk-20230312-114707162-23.jpg" alt="Kakao-Talk-20230312-114707162-23" border="0"></a>

</br>

<a href="https://ibb.co/tYzjqfm"><img src="https://i.ibb.co/p4QVfD0/Kakao-Talk-20230312-114707162-24.jpg" alt="Kakao-Talk-20230312-114707162-24" border="0"></a>

</br>

<a href="https://ibb.co/1XsdxBL"><img src="https://i.ibb.co/xgmfQwD/Kakao-Talk-20230312-114707162-25.jpg" alt="Kakao-Talk-20230312-114707162-25" border="0"></a>

</br>

<a href="https://ibb.co/MSjrp34"><img src="https://i.ibb.co/mTYktMw/Kakao-Talk-20230312-114707162-26.jpg" alt="Kakao-Talk-20230312-114707162-26" border="0"></a>

</br>

<a href="https://ibb.co/g9gP0bP"><img src="https://i.ibb.co/1Q2dCYd/Kakao-Talk-20230312-114707162-27.jpg" alt="Kakao-Talk-20230312-114707162-27" border="0"></a>

</br>

<a href="https://ibb.co/N9xTVKX"><img src="https://i.ibb.co/X7XY2t9/Kakao-Talk-20230312-114707162-28.jpg" alt="Kakao-Talk-20230312-114707162-28" border="0"></a>

</br>

<a href="https://ibb.co/qpYqKW2"><img src="https://i.ibb.co/yqFvtYx/Kakao-Talk-20230312-114707162-29.jpg" alt="Kakao-Talk-20230312-114707162-29" border="0"></a>

</br>

<a href="https://ibb.co/WVj0t9P"><img src="https://i.ibb.co/3RQvzXM/Kakao-Talk-20230312-114716080.jpg" alt="Kakao-Talk-20230312-114716080" border="0"></a>

</br>

<a href="https://ibb.co/xL89y7z"><img src="https://i.ibb.co/qjFqzrm/Kakao-Talk-20230312-114716080-01.jpg" alt="Kakao-Talk-20230312-114716080-01" border="0"></a>

</br>

<a href="https://ibb.co/hW9ZmJB"><img src="https://i.ibb.co/ncmnLN7/Kakao-Talk-20230312-114716080-02.jpg" alt="Kakao-Talk-20230312-114716080-02" border="0"></a>

</br>

<a href="https://ibb.co/H25pqWV"><img src="https://i.ibb.co/N3cnK8s/Kakao-Talk-20230312-114716080-03.jpg" alt="Kakao-Talk-20230312-114716080-03" border="0"></a>

</br>

<a href="https://ibb.co/sm5dd7F"><img src="https://i.ibb.co/p0WBBq3/Kakao-Talk-20230312-114716080-04.jpg" alt="Kakao-Talk-20230312-114716080-04" border="0"></a>

</br>

<a href="https://ibb.co/CPYWsQs"><img src="https://i.ibb.co/mN2SF4F/Kakao-Talk-20230312-114716080-05.jpg" alt="Kakao-Talk-20230312-114716080-05" border="0"></a>

</br>

<a href="https://ibb.co/8KzXtcm"><img src="https://i.ibb.co/Qb8XtdJ/Kakao-Talk-20230312-114716080-06.jpg" alt="Kakao-Talk-20230312-114716080-06" border="0"></a>

</br>

<a href="https://ibb.co/1Kvf097"><img src="https://i.ibb.co/QnbFJ6p/Kakao-Talk-20230312-114716080-07.jpg" alt="Kakao-Talk-20230312-114716080-07" border="0"></a>

</br>

<a href="https://ibb.co/K0NrzgF"><img src="https://i.ibb.co/bWHKRVz/Kakao-Talk-20230312-114716080-08.jpg" alt="Kakao-Talk-20230312-114716080-08" border="0"></a>

</br>

<a href="https://ibb.co/tLyJ2yH"><img src="https://i.ibb.co/dmn5pnf/Kakao-Talk-20230312-114716080-09.jpg" alt="Kakao-Talk-20230312-114716080-09" border="0"></a>

</br>

<a href="https://ibb.co/7X52Fd6"><img src="https://i.ibb.co/s2GyrdM/Kakao-Talk-20230312-114716080-10.jpg" alt="Kakao-Talk-20230312-114716080-10" border="0"></a>

</br>

<a href="https://ibb.co/vBBCjS9"><img src="https://i.ibb.co/fSSVxsJ/Kakao-Talk-20230312-114716080-11.jpg" alt="Kakao-Talk-20230312-114716080-11" border="0"></a>

</br>

<a href="https://ibb.co/syPmyhK"><img src="https://i.ibb.co/NZ3VZX9/Kakao-Talk-20230312-114716080-12.jpg" alt="Kakao-Talk-20230312-114716080-12" border="0"></a>

</br>

모든 수가 정렬 완료 상태가 되었다.