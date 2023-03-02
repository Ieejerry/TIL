# 배열(Array)

</br>

<a href="https://ibb.co/N7RnLnn"><img src="https://i.ibb.co/zNdHSHH/Kakao-Talk-20230301-144420221.jpg" alt="Kakao-Talk-20230301-144420221" border="0"></a>

</br>

배열(Array)은 데이터 구조의 하나로 여러 개의 값을 저장하기 위한 구조이다.

</br>

<a href="https://ibb.co/tZdc9Cf"><img src="https://i.ibb.co/s5BQZ3S/Kakao-Talk-20230301-144420221-01.jpg" alt="Kakao-Talk-20230301-144420221-01" border="0"></a>

</br>

각 요소에 첨자/index(데이터가 몇 번째 칸에 있는지 나타태는 숫자)를 사용해 접근할 수 있다.

</br>

<a href="https://ibb.co/6tcQ8fV"><img src="https://i.ibb.co/s1p7CMk/Kakao-Talk-20230301-144420221-02.jpg" alt="Kakao-Talk-20230301-144420221-02" border="0"></a>

</br>

데이터는 연속된 메모리 영역에 순서대로 저장된다.

</br>

<a href="https://ibb.co/VSNFKFN"><img src="https://i.ibb.co/pzPHmHP/Kakao-Talk-20230301-144420221-03.jpg" alt="Kakao-Talk-20230301-144420221-03" border="0"></a>

</br>

<a href="https://ibb.co/PWkJ5gG"><img src="https://i.ibb.co/C9L4nQK/Kakao-Talk-20230301-144420221-04.jpg" alt="Kakao-Talk-20230301-144420221-04" border="0"></a>

</br>

<a href="https://ibb.co/Bnn2YbV"><img src="https://i.ibb.co/3RRmP2y/Kakao-Talk-20230301-144420221-05.jpg" alt="Kakao-Talk-20230301-144420221-05" border="0"></a>

</br>

<a href="https://ibb.co/FsYYvjw"><img src="https://i.ibb.co/8zxx3S5/Kakao-Talk-20230301-144420221-06.jpg" alt="Kakao-Talk-20230301-144420221-06" border="0"></a>

</br>

<a href="https://ibb.co/qW4vmYd"><img src="https://i.ibb.co/ZYw0czV/Kakao-Talk-20230301-144420221-07.jpg" alt="Kakao-Talk-20230301-144420221-07" border="0"></a>

</br>

연속된 영역에 저장돼 있어서 첨자(index)를 사용해서 메모리의 주소를 계산할 수 있다. 따라서 각 데이터에 바로 접근할 수 있다.

</br>

<a href="https://ibb.co/3MQMt8j"><img src="https://i.ibb.co/rcNcnLz/Kakao-Talk-20230301-144420221-08.jpg" alt="Kakao-Talk-20230301-144420221-08" border="0"></a>

</br>

배열은 임의의 위치에 데이터를 추가, 삭제해야 하는 경우에 리스트에 비해 많은 시간이 걸리는 단점이 있다.

</br>

<a href="https://ibb.co/YBTnWWX"><img src="https://i.ibb.co/Xxk044D/Kakao-Talk-20230301-144420221-09.jpg" alt="Kakao-Talk-20230301-144420221-09" border="0"></a>

</br>

예를 들어 "Green"을 두 번째 요소에 추가하는 경우를 생각해보겠다.

</br>

<a href="https://ibb.co/6PyJb1Y"><img src="https://i.ibb.co/BZfKjrL/Kakao-Talk-20230301-144420221-10.jpg" alt="Kakao-Talk-20230301-144420221-10" border="0"></a>

</br>

먼저, 배열의 마지막에 추가를 위한 공간을 확보한다.

</br>

<a href="https://ibb.co/BtHkNsZ"><img src="https://i.ibb.co/56XZFc8/Kakao-Talk-20230301-144420221-11.jpg" alt="Kakao-Talk-20230301-144420221-11" border="0"></a>

</br>

<a href="https://ibb.co/sQ5rX48"><img src="https://i.ibb.co/J2xPSTD/Kakao-Talk-20230301-144420221-12.jpg" alt="Kakao-Talk-20230301-144420221-12" border="0"></a>

</br>

공간이 비므로 하나씩 데이터를 옆으로 이동한다.

</br>

<a href="https://ibb.co/NyCT5Fc"><img src="https://i.ibb.co/0G2sTnH/Kakao-Talk-20230301-144420221-13.jpg" alt="Kakao-Talk-20230301-144420221-13" border="0"></a>

</br>

빈 공간에 "Green"을 추가해서 작업을 완료한다.

반대로 두 번째 요소를 삭제할 때는

</br>

<a href="https://ibb.co/FKjDR8n"><img src="https://i.ibb.co/rm1wD5v/Kakao-Talk-20230301-144420221-15.jpg" alt="Kakao-Talk-20230301-144420221-15" border="0"></a>

</br>

먼저 요소를 삭제하고

</br>

<a href="https://ibb.co/D78ndNt"><img src="https://i.ibb.co/tbx5RS4/Kakao-Talk-20230301-144420221-16.jpg" alt="Kakao-Talk-20230301-144420221-16" border="0"></a>

</br>

<a href="https://ibb.co/3ypnkBd"><img src="https://i.ibb.co/C5bfWh8/Kakao-Talk-20230301-144420221-17.jpg" alt="Kakao-Talk-20230301-144420221-17" border="0"></a>

</br>

빈 공간을 하나씩 왼쪽으로 옮겨서 메꾼다.

</br>

<a href="https://ibb.co/gPzVFk0"><img src="https://i.ibb.co/b2zJRc4/Kakao-Talk-20230301-144420221-18.jpg" alt="Kakao-Talk-20230301-144420221-18" border="0"></a>

</br>

마지막으로 남은 공간을 삭제한다.

</br>

## 배열(Array)의 특징

배열은 메모리에 순차적으로 저장되기 때문에 "Random Acess"로 index만 알면 몇 번째에 있든 같은 시간으로 빠르게 데이터를 조회할 수 있고, 맨 마지막 index에 데이터 추가, 삭제 또한 빠르다.

하지만 배열은 메모리에 순차적으로 저장되어 있기 때문에 중간에 데이터를 수정 및 삭제를 하기 위해서는 공간을 확보 및 메꿈을 해야 하고, 그러려면 순차적으로 저장되어 있는 데이터들을 이동시켜야 한다. 데이터를 하나씩 이동해야 하기 때문에 시간이 오래걸리고, 저장된 데이터가 많을수록 그 시간은 더 길어진다는 단점이 있다.