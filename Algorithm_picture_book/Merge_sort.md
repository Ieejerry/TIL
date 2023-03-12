# 병합 정렬(Merge sort)

</br>

<a href="https://ibb.co/YZW5hnB"><img src="https://i.ibb.co/dgcNDC4/Kakao-Talk-20230312-111159597.jpg" alt="Kakao-Talk-20230312-111159597" border="0"></a>

</br>

병합 정렬은 수열을 정렬하는 알고리즘 중 하니이다.

</br>

<a href="https://ibb.co/PtB2Mg6"><img src="https://i.ibb.co/N7w0rKy/Kakao-Talk-20230312-111159597-01.jpg" alt="Kakao-Talk-20230312-111159597-01" border="0"></a>

</br>


처음에는 수열을 반씩 분할해 나간다.

</br>

<a href="https://ibb.co/cc593zT"><img src="https://i.ibb.co/XZBPLmJ/Kakao-Talk-20230312-111159597-02.jpg" alt="Kakao-Talk-20230312-111159597-02" border="0"></a>

</br>

<a href="https://ibb.co/hBHHrtL"><img src="https://i.ibb.co/Lx66B2Y/Kakao-Talk-20230312-111159597-03.jpg" alt="Kakao-Talk-20230312-111159597-03" border="0"></a>

</br>

<a href="https://ibb.co/tbrpb6p"><img src="https://i.ibb.co/hKzFKNF/Kakao-Talk-20230312-111159597-04.jpg" alt="Kakao-Talk-20230312-111159597-04" border="0"></a>

</br>

분할이 완료되었다.

다음은 분할한 각 그룹을 병합해 나간다. 병합할 때에는 병합 후의 그룹 내에서 숫자가 작은 순으로 나열되도록 한다.

</br>

<a href="https://ibb.co/jDTQwsh"><img src="https://i.ibb.co/zZrB2Ds/Kakao-Talk-20230312-111159597-05.jpg" alt="Kakao-Talk-20230312-111159597-05" border="0"></a>

</br>

<a href="https://ibb.co/r5z1v5b"><img src="https://i.ibb.co/CVYTWVJ/Kakao-Talk-20230312-111159597-06.jpg" alt="Kakao-Talk-20230312-111159597-06" border="0"></a>

</br>

여러 숫자를 포함하고 있는 그룹들을 서로 병합할 때는 선두의 숫자를 비교해서 작은 숫자를 이동한다.

</br>

<a href="https://ibb.co/wwvGKCk"><img src="https://i.ibb.co/TbCjHRf/Kakao-Talk-20230312-111159597-07.jpg" alt="Kakao-Talk-20230312-111159597-07" border="0"></a>

</br>

그림의 첫 4와 3을 비교한다.

</br>

<a href="https://ibb.co/gVdfx6j"><img src="https://i.ibb.co/KwDfJm0/Kakao-Talk-20230312-111159597-08.jpg" alt="Kakao-Talk-20230312-111159597-08" border="0"></a>

</br>

4 > 3이므로 3을 이동한다. 마찬가지로 남은 열의 선두를 비교해서

</br>

<a href="https://ibb.co/B3tLhKW"><img src="https://i.ibb.co/dMrBNJC/Kakao-Talk-20230312-111159597-09.jpg" alt="Kakao-Talk-20230312-111159597-09" border="0"></a>

</br>

4 < 7이므로 4를 이동한다.

</br>

<a href="https://ibb.co/V3LzwPk"><img src="https://i.ibb.co/PtrPDfV/Kakao-Talk-20230312-111159597-10.jpg" alt="Kakao-Talk-20230312-111159597-10" border="0"></a>

</br>

6 < 7이므로 6을 이동한다.

</br>

<a href="https://ibb.co/TRgRgdR"><img src="https://i.ibb.co/Npypybp/Kakao-Talk-20230312-111159597-11.jpg" alt="Kakao-Talk-20230312-111159597-11" border="0"></a>

</br>

남은 7을 이동한다.

그룹 병합 작업은 모든 숫자가 하나의 그룹이 될 때까지 재귀적으로 반복한다.

</br>

<a href="https://ibb.co/4Y8vrgM"><img src="https://i.ibb.co/QCPSwjn/Kakao-Talk-20230312-111159597-12.jpg" alt="Kakao-Talk-20230312-111159597-12" border="0"></a>

</br>

<a href="https://ibb.co/rpLW8WN"><img src="https://i.ibb.co/wQbvGvj/Kakao-Talk-20230312-111159597-13.jpg" alt="Kakao-Talk-20230312-111159597-13" border="0"></a>

</br>

<a href="https://ibb.co/C2xS3tv"><img src="https://i.ibb.co/ZmybpJK/Kakao-Talk-20230312-111159597-14.jpg" alt="Kakao-Talk-20230312-111159597-14" border="0"></a>

</br>

<a href="https://ibb.co/7ggtrgq"><img src="https://i.ibb.co/M88kP8m/Kakao-Talk-20230312-111159597-15.jpg" alt="Kakao-Talk-20230312-111159597-15" border="0"></a>

</br>

<a href="https://ibb.co/bQG1dDS"><img src="https://i.ibb.co/MZJnNQY/Kakao-Talk-20230312-111159597-16.jpg" alt="Kakao-Talk-20230312-111159597-16" border="0"></a>

</br>

병합이 끝나고 수열이 정렬된다.