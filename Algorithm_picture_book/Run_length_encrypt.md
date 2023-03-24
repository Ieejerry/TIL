# 연속길이 부호(Run length Encrypt)

</br>

[![IMG-2104.jpg](https://i.postimg.cc/VLpRgkt2/IMG-2104.jpg)](https://postimg.cc/JG3Z4mPQ)

</br>

5x5 칸에 세 가지 색을 이용해 그린 그림을 부호화해보겠다. 먼저 단순한 기법을 사용해보겠다.

</br>

[![IMG-2105.jpg](https://i.postimg.cc/kX3NRpdd/IMG-2105.jpg)](https://postimg.cc/kDsRkw4j)

</br>

세 가지 색에 각각 Y(Yellow), G(Green), B(Blue) 라는 문자를 부여했다.

</br>

[![IMG-2106.jpg](https://i.postimg.cc/ydGPG15J/IMG-2106.jpg)](https://postimg.cc/62dn2XBw)

</br>

도형의 왼쪽 상단을 기점으로 해서 한 줄씩 Y, G, B 문자로 변환한 결과 도형을 25문자로 부호화할 수 있다.

다음은 그림을 연속길이 부호화해서 25문자보다 작은 문자 수로 표현해보도록 하겠다. 연속길이 부호는, 부호와 그것이 연속된 횟수를 한 세트로 해서 부호화하는 기법이다. 예를 들어 첫 부분의 'YYYY'는 'Y4'로 표현해서 두 개의 문자로 표현할 수 있다.

</br>

[![IMG-2107.jpg](https://i.postimg.cc/280498ZC/IMG-2107.jpg)](https://postimg.cc/XpyGpWLP)

</br>

동일한 작업을 반복해서 연속길이 부호화를 완료했다. 결과적으로 5 문자가 적은 20 문자로 압축됐다. 그림이 한 줄에 다섯 칸으로 돼있다는 정보를 알고 있으면, 부호로부터 그림을 복원해낼 수 있다.

이 작업은 '압축'과 반대되는 개념으로 '해제'라고 한다.

데이터 중에는 연속길이 부호에 적합한 것과 그렇지 않은 것이 있다.

</br>

[![IMG-2108.jpg](https://i.postimg.cc/pVwQnXFT/IMG-2108.jpg)](https://postimg.cc/14KVkSMh)

</br>

부호화된 것을 자세히 보면, 전체 문자 수가 줄었지만, 같은 색이 연속되지 않는 부분에서는 연속길이 부호화 후에 오히려 문자 수가 늘어났다.

</br>

[![IMG-2109.jpg](https://i.postimg.cc/9XbVDzSP/IMG-2109.jpg)](https://postimg.cc/fkV1FWMk)

</br>

예를 들어 그림과 같이 데이터 연속성이 부족한 것을 연속길이 부호화하면

</br>

[![IMG-2110.jpg](https://i.postimg.cc/sXcFG0nf/IMG-2110.jpg)](https://postimg.cc/9Rrgv15s)

</br>

부호가 우너래보다 50배 늘어나게 된다.

</br>

[![IMG-2111.jpg](https://i.postimg.cc/QtSPdKtH/IMG-2111.jpg)](https://postimg.cc/yggnfd0H)

</br>

반대로 그림처럼 데이터 연속성이 있는 것을 부호화하면

</br>

[![IMG-2112.jpg](https://i.postimg.cc/vTcP8PkN/IMG-2112.jpg)](https://postimg.cc/V0P9DFYq)

</br>

부호가 10 문자가 된다. 원래의 25 문자와 비교하면 압축률이 꽤 높은 것을 알 수 있다. 이처럼 연속길이 부호는 부호화 대상에 따라 압축 효과가 있을 수도 있고 없을 수도 있다. 이 때문에 데이터가 일정 수 이상 연속되는 경우에만 연속길이 부호화하는 등의 고민이 필요하다.

</br>

[![IMG-2113.jpg](https://i.postimg.cc/76yGZbc8/IMG-2113.jpg)](https://postimg.cc/JyP4T7MP)

</br>

연속길이 부호의 사용 예로 흑백 팩스를 생각해보겠다. 그림의 도형을 팩스를 통해 보내려고 할 때, 단순히 각 칵을 W(White), B(Black)이라는 글자로 표현하면 25 문자가 된다. 통신량을 줄이기 위해 연속길이 부호화로 데이터를 압축한다.

</br>

[![IMG-2114.jpg](https://i.postimg.cc/s20zTLYn/IMG-2114.jpg)](https://postimg.cc/GBY62qSY)

</br>

부호화 결과 1 문자 늘어서 26 문자가 된다. 이 경우는 연속길이 부호를 이용하는 의미가 없다. 하지만 흑백 사진에서 사용되는 것은 흰색과 검정색 두 가지 색밖에 없다. 따라서 흰색 칸이 연속된 후에 나오는 것은 검정색 칸으로 정해져 있다. W와 B라는 문자가 없어도 부호로부터 도형을 복원할 수 있을 듯하다.

</br>

[![IMG-2115.jpg](https://i.postimg.cc/Vkxp5cFP/IMG-2115.jpg)](https://postimg.cc/gxKNBQ5g)

</br>

W와 B라는 문자를 제거하면 13 문자가 돼서 크기가 반정도로 줄어든다. 단, 부호의 첫 번째 숫자는 흰색 칸이 연속되는 수라는 것을 규칙으로 정할 필요가 있다. 이 규칙이 있으면 부호로부터 원 이미지를 제대로 복원할 수 있다.

</br>

[![IMG-2116.jpg](https://i.postimg.cc/VshRzWR3/IMG-2116.jpg)](https://postimg.cc/kDx8c8Lc)

</br>

그러면 다음과 같은 그림을 부호화하려고 한다.

</br>

[![IMG-2117.jpg](https://i.postimg.cc/sx5qpHf0/IMG-2117.jpg)](https://postimg.cc/p5XsvZFD)

</br>

앞서 본 것과 달리 그림의 첫 번째 칸이 흰색이 아닌 검정색이다.

</br>

[![IMG-2118.jpg](https://i.postimg.cc/4NSV6fMq/IMG-2118.jpg)](https://postimg.cc/w7D1Hp9Q)

</br>

일단 동일한 방법으로 부호화해보았다. 부호의 첫 번째 숫자는 검정색 칸이 연속된 수를 나타내고 있지만 부호의 첫 번째 숫자는 흰색 칸이 연속된 수라는 규칙을 지키고 있지 않는다. 그대로 복원하면 흰색과 검정색이 바뀐 그림이 된다.

</br>

[![IMG-2119.jpg](https://i.postimg.cc/T3vm77dJ/IMG-2119.jpg)](https://postimg.cc/PPKPNM8C)

</br>

부호의 첫 번째 숫자는 흰색 칸이 연속된 수라는 규칙을 지키려면 부호의 선두에 0을 추가했다. 도형의 첫 번째 칸이 0이라는 것은 흰색 칸이 없다는 의미가 된다. 선두에 0을 추가하므로 문자 수는 하나 늘었지만 정해진 규칙에 의해 데이터를 압축할 수가 있다.

</br>

[![IMG-2120.jpg](https://i.postimg.cc/hG67mp5m/IMG-2120.jpg)](https://postimg.cc/rdGmXCcy)

</br>

연속길이 부호는 일반적으로 데이터의 연속성이 빈약한 텍스트보다 이미지 데이터의 압축에 적합하다. 어느 경우 높은 압축 효과를 얻기 위한 고민이 필요하다.