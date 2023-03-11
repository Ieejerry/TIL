# 힙 정렬(Heap sort)

</br>

<a href="https://ibb.co/VmdQbm2"><img src="https://i.ibb.co/m8mXd86/Kakao-Talk-20230311-174857516.jpg" alt="Kakao-Talk-20230311-174857516" border="0"></a>

</br>

힙 정렬은 수열을 정렬하는 알고리즘 중 하나로, 힙이라는 데이터 구조를 사용하는 것이 특징이다.

</br>

<a href="https://ibb.co/YNZKdjV"><img src="https://i.ibb.co/HKdMPg9/Kakao-Talk-20230311-174857516-01.jpg" alt="Kakao-Talk-20230311-174857516-01" border="0"></a>

</br>

처음에는 힙에 모든 숫자를 저장한다. 힙은 내림차순으로 구축한다.

</br>

<a href="https://ibb.co/19k40XT"><img src="https://i.ibb.co/p3Sk1Kd/Kakao-Talk-20230311-174857516-02.jpg" alt="Kakao-Talk-20230311-174857516-02" border="0"></a>

</br>

<a href="https://ibb.co/Dt9rxFR"><img src="https://i.ibb.co/2yvZDrk/Kakao-Talk-20230311-174857516-03.jpg" alt="Kakao-Talk-20230311-174857516-03" border="0"></a>

</br>

<a href="https://ibb.co/3vgT1Qn"><img src="https://i.ibb.co/zFqmsDz/Kakao-Talk-20230311-174857516-04.jpg" alt="Kakao-Talk-20230311-174857516-04" border="0"></a>

</br>

<a href="https://ibb.co/r20BDHv"><img src="https://i.ibb.co/MkSzF79/Kakao-Talk-20230311-174857516-05.jpg" alt="Kakao-Talk-20230311-174857516-05" border="0"></a>

</br>

<a href="https://ibb.co/wSZGYVN"><img src="https://i.ibb.co/0Cp4QTj/Kakao-Talk-20230311-174857516-06.jpg" alt="Kakao-Talk-20230311-174857516-06" border="0"></a>

</br>

<a href="https://ibb.co/dMxZNxj"><img src="https://i.ibb.co/r0N9BNF/Kakao-Talk-20230311-174857516-07.jpg" alt="Kakao-Talk-20230311-174857516-07" border="0"></a>

</br>

<a href="https://ibb.co/jVPf65G"><img src="https://i.ibb.co/wJFg0LC/Kakao-Talk-20230311-174857516-08.jpg" alt="Kakao-Talk-20230311-174857516-08" border="0"></a>

</br>

<a href="https://ibb.co/R085NC8"><img src="https://i.ibb.co/fpJc9CJ/Kakao-Talk-20230311-174857516-09.jpg" alt="Kakao-Talk-20230311-174857516-09" border="0"></a>

</br>

힙에 모든 숫자를 저장했다. 참고로 힙 구축에는 더 효율적인 방법이 있지만 여기서는 간단한 방법을 사용하고 있다.

힙에 저장된 숫자를 하나씩 꺼낸다. 내림차순 힙은 큰 것부터 순서대로 데이터를 추출하는 성질이 있으므로 꺼낸 숫자를 역순으로 나열하면 정렬이 완료된다.

</br>

<a href="https://ibb.co/DVbYqVB"><img src="https://i.ibb.co/FxWXPxQ/Kakao-Talk-20230311-174857516-10.jpg" alt="Kakao-Talk-20230311-174857516-10" border="0"></a>

</br>

<a href="https://ibb.co/1b7VCQc"><img src="https://i.ibb.co/GFnwZpm/Kakao-Talk-20230311-174857516-11.jpg" alt="Kakao-Talk-20230311-174857516-11" border="0"></a>

</br>

<a href="https://ibb.co/T1MNw10"><img src="https://i.ibb.co/ZSzbfSg/Kakao-Talk-20230311-174857516-12.jpg" alt="Kakao-Talk-20230311-174857516-12" border="0"></a>

</br>

<a href="https://ibb.co/B34JnM4"><img src="https://i.ibb.co/vqsWXns/Kakao-Talk-20230311-174857516-13.jpg" alt="Kakao-Talk-20230311-174857516-13" border="0"></a>

</br>

<a href="https://ibb.co/0J7gbPL"><img src="https://i.ibb.co/PCL7HBy/Kakao-Talk-20230311-174857516-14.jpg" alt="Kakao-Talk-20230311-174857516-14" border="0"></a>

</br>

<a href="https://ibb.co/6PxR2YV"><img src="https://i.ibb.co/VSZWdVr/Kakao-Talk-20230311-174857516-15.jpg" alt="Kakao-Talk-20230311-174857516-15" border="0"></a>

</br>

<a href="https://ibb.co/qrHhNRC"><img src="https://i.ibb.co/4VbC8j2/Kakao-Talk-20230311-174857516-16.jpg" alt="Kakao-Talk-20230311-174857516-16" border="0"></a>

</br>

모든 숫자를 힙에서 꺼내면 정렬이 완료된다. 여기서는 이 배열과 별도로 힙이라는 데이터 구조를 준비했지만 보통은 수열이 저장돼 있는 배열 자체에 힙을 넣어서 배열상에서 숫자를 교체해가며 정렬한다.

</br>

<a href="https://ibb.co/10RDN5j"><img src="https://i.ibb.co/7SrwD5L/Kakao-Talk-20230311-174857516-17.jpg" alt="Kakao-Talk-20230311-174857516-17" border="0"></a>

</br>

<a href="https://ibb.co/V3tKcpL"><img src="https://i.ibb.co/d7rhwJf/Kakao-Talk-20230311-174857516-18.jpg" alt="Kakao-Talk-20230311-174857516-18" border="0"></a>

</br>

<a href="https://ibb.co/NTNj5Fq"><img src="https://i.ibb.co/MB1VrgH/Kakao-Talk-20230311-174857516-19.jpg" alt="Kakao-Talk-20230311-174857516-19" border="0"></a>

</br>

<a href="https://ibb.co/sQTp33C"><img src="https://i.ibb.co/rMBKyy3/Kakao-Talk-20230311-174857516-20.jpg" alt="Kakao-Talk-20230311-174857516-20" border="0"></a>

</br>

<a href="https://ibb.co/6P6kBq5"><img src="https://i.ibb.co/zRKzJtw/Kakao-Talk-20230311-174857516-21.jpg" alt="Kakao-Talk-20230311-174857516-21" border="0"></a>

</br>

구체적으로는 힙상의 각 요소(노드)와 배열 간에 그림과 같은 대응 관계를 만든다.

보면 알겠지만 배열 안에 힙을 무리해서 구겨 넣은 상태라고 할 수 있다.

</br>

<a href="https://ibb.co/kDdQKPd"><img src="https://i.ibb.co/s1ByjXB/Kakao-Talk-20230311-174857516-22.jpg" alt="Kakao-Talk-20230311-174857516-22" border="0"></a>

</br>

그러면 실제로 정렬 작업을 해보도록 하겠다.

</br>

<a href="https://ibb.co/gD7kXGn"><img src="https://i.ibb.co/khyNrpd/Kakao-Talk-20230311-174857516-23.jpg" alt="Kakao-Talk-20230311-174857516-23" border="0"></a>

</br>

여기선 이해를 돕기 위해 트리 구조의 힙을 표시한 상태로 두겠다.

</br>

<a href="https://ibb.co/3c6mXPB"><img src="https://i.ibb.co/m4Z5sP6/Kakao-Talk-20230311-174857516-24.jpg" alt="Kakao-Talk-20230311-174857516-24" border="0"></a>

</br>

<a href="https://ibb.co/nbKBgM3"><img src="https://i.ibb.co/kxPJH23/Kakao-Talk-20230311-174857516-26.jpg" alt="Kakao-Talk-20230311-174857516-26" border="0"></a>

</br>

앞서 본 것처럼 힙에 숫자를 넣는 작업부터 시작하겠다.

</br>

<a href="https://ibb.co/qnVmk5f"><img src="https://i.ibb.co/FWC8gVM/Kakao-Talk-20230311-174857516-27.jpg" alt="Kakao-Talk-20230311-174857516-27" border="0"></a>

</br>

<a href="https://ibb.co/CsJm3HY"><img src="https://i.ibb.co/G3sn458/Kakao-Talk-20230311-174857516-28.jpg" alt="Kakao-Talk-20230311-174857516-28" border="0"></a>

</br>

<a href="https://ibb.co/Jc0wDKg"><img src="https://i.ibb.co/tHkTV4F/Kakao-Talk-20230311-174857516-29.jpg" alt="Kakao-Talk-20230311-174857516-29" border="0"></a>

</br>

<a href="https://ibb.co/mRqrvxS"><img src="https://i.ibb.co/wdWZJvY/Kakao-Talk-20230311-174909672.jpg" alt="Kakao-Talk-20230311-174909672" border="0"></a>

</br>

<a href="https://ibb.co/N6Sz75z"><img src="https://i.ibb.co/7J4FbPF/Kakao-Talk-20230311-174909672-01.jpg" alt="Kakao-Talk-20230311-174909672-01" border="0"></a>

</br>

트리 구조의 힙 내에서 숫자가 바뀌면 배열 내에서도 동일하게 숫자를 교체한다.

</br>

<a href="https://ibb.co/yXfc4g8"><img src="https://i.ibb.co/G0x4HCV/Kakao-Talk-20230311-174909672-02.jpg" alt="Kakao-Talk-20230311-174909672-02" border="0"></a>

</br>

힙에 모든 숫자를 저장했다. 동시에 배열이 내림차순으로 정리되었다. 다음은 힙에 저장한 숫자를 하나씩 꺼낸다. 내림차순 힙은 큰 것부터 순서대로 데이터가 추출된다.

</br>

<a href="https://ibb.co/rpNVvyZ"><img src="https://i.ibb.co/QHt4Xm6/Kakao-Talk-20230311-174909672-03.jpg" alt="Kakao-Talk-20230311-174909672-03" border="0"></a>

</br>

배열 내에선 선두에 있는 숫자가 힙 내에서 가장 큰 숫자가 된다.

</br>

<a href="https://ibb.co/rxsC5Hq"><img src="https://i.ibb.co/D9pxwQm/Kakao-Talk-20230311-174909672-04.jpg" alt="Kakao-Talk-20230311-174909672-04" border="0"></a>

</br>

배열의 선두 숫자를 힙의 마지막 요소에 대응하는 배열과 바꾸면 작업이 완료된다.

</br>

<a href="https://ibb.co/J5hjNMr"><img src="https://i.ibb.co/pJmjg94/Kakao-Talk-20230311-174909672-05.jpg" alt="Kakao-Talk-20230311-174909672-05" border="0"></a>

</br>

힙의 구조가 유지되도록 정리한다.

</br>

<a href="https://ibb.co/yX2W25w"><img src="https://i.ibb.co/2yJgJPD/Kakao-Talk-20230311-174909672-06.jpg" alt="Kakao-Talk-20230311-174909672-06" border="0"></a>

</br>

<a href="https://ibb.co/JsRv1Lp"><img src="https://i.ibb.co/d50PT9p/Kakao-Talk-20230311-174909672-07.jpg" alt="Kakao-Talk-20230311-174909672-07" border="0"></a>

</br>

<a href="https://ibb.co/fqrd9xr"><img src="https://i.ibb.co/mbh50ch/Kakao-Talk-20230311-174909672-08.jpg" alt="Kakao-Talk-20230311-174909672-08" border="0"></a>

</br>

<a href="https://ibb.co/s1TNrKM"><img src="https://i.ibb.co/dpNVyPz/Kakao-Talk-20230311-174909672-09.jpg" alt="Kakao-Talk-20230311-174909672-09" border="0"></a>

</br>

<a href="https://ibb.co/9qtcHWp"><img src="https://i.ibb.co/D7pzfQ1/Kakao-Talk-20230311-174909672-10.jpg" alt="Kakao-Talk-20230311-174909672-10" border="0"></a>

</br>


이 작업을 모든 숫자가 작업 완료 상태가 될 때까지 반복한다.

</br>

<a href="https://ibb.co/qxzSvL0"><img src="https://i.ibb.co/N7XvMg1/Kakao-Talk-20230311-174909672-11.jpg" alt="Kakao-Talk-20230311-174909672-11" border="0"></a>

</br>

정렬을 완료