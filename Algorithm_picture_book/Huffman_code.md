# 허프만 부호(Huffman code)

</br>

[![IMG-2122.jpg](https://i.postimg.cc/pVwkzZVq/IMG-2122.jpg)](https://postimg.cc/c6cQNfnn)

</br>

허프만 부호는 데이터를 부호화하는 알고리즘이다.

JPEG이나 ZIP 등의 이미지나 파일 압축에 사용된다. 예로 'ABAABACD'라는 문자열을 네트워크를 통해 전송하는 경우를 생각해보겠다. 데이터는 2진수(0과 1로)로 부호화해서 전송된다.

</br>

[![IMG-2123.jpg](https://i.postimg.cc/8c9Y6QKH/IMG-2123.jpg)](https://postimg.cc/4HvPDMT7)

</br>

예를 들어, ASCII(아스키)라는 문자 코드에선 A, B, C, D 각각의 문자가 그림처럼 부호화된다. ASCII에선 하나의 문자가 8비트로 표현된다.

</br>

[![IMG-2124.jpg](https://i.postimg.cc/rmKX0Jyq/IMG-2124.jpg)](https://postimg.cc/zbZP4TRQ)

</br>

ASCII에 의해 'ABAABACD'라는 문자열을 부호화해보았다. 그 결과 64비트가 된다. 통신량을 줄이기 위해 문자열을 64비트보다 작게 만드는 방법을 생각해보겠다. ASCII는 대부분의 문자를 구분해서 관리하기 위해 하나의 문자를 8비트로 표현하고 있다. 하지만 'ABAABACD'라는 문자열에선 단 네 개의 문자만 사용되고 있다. 이 문자들이 구분될 수 있도록 부호화하면 된다.

</br>

[![IMG-2125.jpg](https://i.postimg.cc/FsFbjB5b/IMG-2125.jpg)](https://postimg.cc/vDj6yXmD)

</br>

단순한 예로 그림처럼 부호화 규칙을 정해보았다. 하나의 문자를 2비트로 표현하고 있다.

</br>

[![IMG-2126.jpg](https://i.postimg.cc/L6hY4KFW/IMG-2126.jpg)](https://postimg.cc/KRSvQWz7)

</br>

규칙에 따라 ABAABACD를 부호화해보았다. 그 결과 데이터의 크기가 16비트가 되면서 꽤 많이 줄어든다. 물론 아무렇게나 정한 규칙이어서 문자열을 전송받는 쪽에도 부호화 규치을 전달할 필요가 있다. 편의상 여기선 규칙 전달에 필요한 통신량을 고려하지 않고 않는다. 문자열을 받은 쪽이 부호를 복호화하려면

</br>

[![IMG-2127.jpg](https://i.postimg.cc/c4MxNFrz/IMG-2127.jpg)](https://postimg.cc/ZCnt8FPP)

</br>

부호를 두 문자 단위로 잘라서

</br>

[![IMG-2128.jpg](https://i.postimg.cc/Dz4R7zxz/IMG-2128.jpg)](https://postimg.cc/qt01LpVf)

</br>

각각을 규칙에 맞게 복원하면 원래 문자열인 'ABAABACD'를 얻을 수 있다.

</br>

[![IMG-2129.jpg](https://i.postimg.cc/xCCJXWbq/IMG-2129.jpg)](https://postimg.cc/mcv2qpjG)

</br>

'ABAABACD'라는 문자열을 더 작게 부호화하는 방법을 생각해보겠다. 앞의 규칙에선 하나의 문자열을 2비트로 표현했지만

</br>

[![IMG-2130.jpg](https://i.postimg.cc/762C1Smy/IMG-2130.jpg)](https://postimg.cc/47XNs7D8)

</br>

A와 B를 1비트로 표현해서 더 작게 부호화할 수 있을 거 같다. 참고로 'ABAABACD'라는 문자열에선 C와 D보다 A와 B가 더 많이 사용되고 있다. 이 사실로부터 C와 D가 아닌 A와 B를 1비트로 표현하는 것이 좋아보인다.

</br>

[![IMG-2131.jpg](https://i.postimg.cc/fRShR5LZ/IMG-2131.jpg)](https://postimg.cc/WdVy9Ggf)

</br>

규칙에 따라 'ABAABACD'를 부호화했다. 그 결과 데이터의 크기가 10비트가 되면서 크기가 더 줄어든다.

</br>

[![IMG-2132.jpg](https://i.postimg.cc/MKhFdw62/IMG-2132.jpg)](https://postimg.cc/sv4mgtGw)

</br>

부호를 받은 쪽이 부호를 문자열로 복원하려면 각각을 규칙에 맞게 복원하면 되지만 예를 들어 10이라는 부호는 BA는 물론 C로도 표현할 수 있다.

</br>

[![IMG-2133.jpg](https://i.postimg.cc/BQWzCsQW/IMG-2133.jpg)](https://postimg.cc/qgLQkP3Q)

</br>

따라서 틀린 문자열이 복원돼 버린다.

</br>

[![IMG-2134.jpg](https://i.postimg.cc/VNHG0PHV/IMG-2134.jpg)](https://postimg.cc/HJX4FRmw)

</br>

이외에도 다양한 문자열이 복원될 수 있어서 해당 문자열이 정확하다고 확정지을 수가 없다.

</br>

[![IMG-2135.jpg](https://i.postimg.cc/QCgJb20s/IMG-2135.jpg)](https://postimg.cc/kR4SMh0h)

</br>

이처럼 부호를 보더라도 원래 문자열을 확정지을 수 없는 것을 '유일 복호 불가능'이라고 한다.

</br>

[![IMG-2136.jpg](https://i.postimg.cc/zfm3zyqt/IMG-2136.jpg)](https://postimg.cc/FYZhGsd3)

</br>

다른 한 가지 예를 보겠다. 편의상 A와 B, 두 개이 문자가 그림처럼 복호화된다고 가정해보겠다.

</br>

[![IMG-2137.jpg](https://i.postimg.cc/TPGGNgd6/IMG-2137.jpg)](https://postimg.cc/rDhvKdRn)

</br>

이 부호화 규칙에서 000001이라는 부호가 주어진 경우의 복호화 과정을 생각해보겠다.

</br>

[![IMG-2138.jpg](https://i.postimg.cc/SKD0ZP16/IMG-2138.jpg)](https://postimg.cc/cKg5CFSC)

</br>

복호화를 위해 선두의 숫자부터 차례대로 보겠다. 첫 숫자가 0이지만 이것만으로는 A를 의미하는지 B의 일부를 의미하는지 판단할 수 없다.

</br>

[![IMG-2139.jpg](https://i.postimg.cc/1X6sYHqy/IMG-2139.jpg)](https://postimg.cc/n9HyXq2W)

</br>

두 번째 문자까지의 숫자가 00이지만 AA를 의미하는지 B의 일부를 의미하는지 판단할 수 없다.

</br>

[![IMG-2140.jpg](https://i.postimg.cc/3RzDvthh/IMG-2140.jpg)](https://postimg.cc/jwQ5VQC3)

</br>

계속해서 세 번째 숫자까지 000이지만 AAA를 의미하는지 B의 일부를 의미하는지 판단할 수 없다.

</br>

[![IMG-2141.jpg](https://i.postimg.cc/JhnyYf4m/IMG-2141.jpg)](https://postimg.cc/dhbtLSyS)

</br>

동일한 네 번째 숫자까지도 판단이 어렵다.

</br>

[![IMG-2142.jpg](https://i.postimg.cc/prtLv4xm/IMG-2142.jpg)](https://postimg.cc/2b2DFH1Y)

</br>

다섯 번째도 마찬가지다.

</br>

[![IMG-2143.jpg](https://i.postimg.cc/0NT8GFzV/IMG-2143.jpg)](https://postimg.cc/CZ4TSvH8)

</br>

최종적으로 여섯 번째 숫자 1을 보고서야 선두 문자 0이 A를 의미하고 그 뒤에 00001가 B라는 것을 알 수 있다.

</br>

[![IMG-2144.jpg](https://i.postimg.cc/yY8zRsfV/IMG-2144.jpg)](https://postimg.cc/4nqMkkkM)

</br>

000001이라는 숫자는 AB라는 문자열로 한 번에 복원할 수 있다. 이 점에선 문제가 없다. 변환표에 있는 부호가 등장하면 즉시 원래 문자를 결정할 수 있는 것을 '순간 부호'라고 하지만 이 예처럼 더 뒤에 있는 문자를 확인하지 않으면 원래 문자를 판단할 수 없는 것은 '순간 부호'가 아니다. 따라서 부호를 복호화하려면 시간이 걸린다.

</br>

[![IMG-2145.jpg](https://i.postimg.cc/x1bjk9CX/IMG-2145.jpg)](https://postimg.cc/75wrd8S4)

</br>

효율이 좋은 부호화, 복호화를 위해서는 '유일 복호 기능' 그리고 '순간 부호' 인 것이 좋다. 예로 본 그림의 두 가지 부호화 규칙에 문제가 있는지 확인해보겠다.

</br>

[![IMG-2146.jpg](https://i.postimg.cc/VkyQVnfN/IMG-2146.jpg)](https://postimg.cc/F7xBffJt)

</br>

첫 번째 부호화 규칙을 가시화해보면

</br>

[![IMG-2147.jpg](https://i.postimg.cc/QMwyFrFd/IMG-2147.jpg)](https://postimg.cc/Z9PcQ2PG)

</br>

특정 부호가 주어진 경우 첫 번째 문자가 0이면 A로 확정한다.

</br>

[![IMG-2148.jpg](https://i.postimg.cc/XNzpXH8D/IMG-2148.jpg)](https://postimg.cc/rz58P97S)

</br>

하지만 1이면 B인 경우와 C 또는 D의 일부일 가능성이 있다.

</br>

[![IMG-2149.jpg](https://i.postimg.cc/7Y1hXH4j/IMG-2149.jpg)](https://postimg.cc/zVBqG1Vk)

</br>

마찬가지로 두 번째 부호화 규칙도 가시화해보겠다.

</br>

[![IMG-2150.jpg](https://i.postimg.cc/bNL8sspY/IMG-2150.jpg)](https://postimg.cc/ykJ2G6D2)

</br>

특정 부호가 주어진 경우 첫 번째 문자는 0이 될 수 밖에 없다.

</br>

[![IMG-2151.jpg](https://i.postimg.cc/NMbb1qMX/IMG-2151.jpg)](https://postimg.cc/XGGwbP9N)

</br>

하지만 이 0이 A일 수도 있고 B의 일부일 수도 있다.

</br>

[![IMG-2152.jpg](https://i.postimg.cc/gjQVDYPx/IMG-2152.jpg)](https://postimg.cc/QKgKNZCD)

</br>

유일 복호 기능이면서 순간 부호이려면 '어떤 부호도 다른 부호의 선두에 포함돼서는 안된다'는 것이 전제가 돼야 한다. 지금까지의 두 예에선 이것을 만족하고 있지 않았다. 허프만 부호는 유일 복호 기능이면서 순간 부호인 부호를 간단히 찾아내는 알고리즘이다. 실제로 허프만 부호로 부호화하는 과정을 보겠다.

</br>

[![IMG-2153.jpg](https://i.postimg.cc/Gtx85YVT/IMG-2153.jpg)](https://postimg.cc/1V43gg9y)

</br>

허프만 부호는 유일 복호 기능이면서 순간 부호이다. 먼저 각 문자의 등장 빈도를 계산한다. ABAABACD의 경우 그림의 비율이 된다. 다음은 사용된 문자를 등장 빈도가 높은 순으로 정렬한다. 이 예에선 ABCD 순이다.

</br>

[![IMG-2154.jpg](https://i.postimg.cc/d1mVsFBz/IMG-2154.jpg)](https://postimg.cc/G8tCKZ6Q)

</br>

다음은 등장 빈도가 낮은 순으로 두 개이 문자를 찾는다. 이 예에선 C(12.5%)와 D(12.5%)가 된다.

</br>

[![IMG-2155.jpg](https://i.postimg.cc/02ZZ6JjN/IMG-2155.jpg)](https://postimg.cc/hfzV6v9F)

</br>

두 개의 문자를 연결해서 트리 구조를 만든다.

</br>

[![IMG-2156.jpg](https://i.postimg.cc/TY2JXY0v/IMG-2156.jpg)](https://postimg.cc/Lh71tSGx)

</br>

두 개의 문자를 'C or D'로 합체해서 등장 빈도를 더한다.

</br>

[![IMG-2157.jpg](https://i.postimg.cc/6qMRQncJ/IMG-2157.jpg)](https://postimg.cc/wRs3ftn0)

</br>

'C or D'를 하나의 문자로 생각하고 동일한 작업을 반복한다. A, B, 'C or D'의 세 개 중에서 등장 빈도가 낮은 순으로 두 개의 문자를 찾는다.

</br>

[![IMG-2158.jpg](https://i.postimg.cc/kGw5HmKt/IMG-2158.jpg)](https://postimg.cc/9wRV4sxW)

</br>

여기선 B(25%)와 'C or D'(25%)가 된다.

</br>

[![IMG-2159.jpg](https://i.postimg.cc/fTLWb1YB/IMG-2159.jpg)](https://postimg.cc/JtfC666k)

</br>

두 개의 문자를 연결해서 트리 구조를 만든다.

</br>

[![IMG-2160.jpg](https://i.postimg.cc/TPrfSxXY/IMG-2160.jpg)](https://postimg.cc/sBDkQtXt)

</br>

두 개의 문자를 'B or C or D'로 합체하고 등장 빈도를 더한다.

</br>

[![IMG-2161.jpg](https://i.postimg.cc/YSfBRx1v/IMG-2161.jpg)](https://postimg.cc/LqXW6LQS)

</br>

'B or C or D'를 하나의 문자열로 간주하겠다.

</br>

[![IMG-2162.jpg](https://i.postimg.cc/25xghSDv/IMG-2162.jpg)](https://postimg.cc/rdKhLczF)

</br>

도일하게 등장 빈도가 작은 두 개의 문자를 선택하는데, 이번에는 마지막에 남은 A와 'B or C or D' 두 개를 연결하게 된다.

</br>

[![IMG-2163.jpg](https://i.postimg.cc/qRWfMZrZ/IMG-2163.jpg)](https://postimg.cc/1n07vBfp)

</br>

양쪽을 연결해서 트리 구조를 만든다.

</br>

[![IMG-2164.jpg](https://i.postimg.cc/8523VJd2/IMG-2164.jpg)](https://postimg.cc/cgcTRJbh)

</br>

모든 문자가 'A or B or C or D'로 하나의 문자가 됐다. 등장 빈도는 당연히 100%가 된다.

</br>

[![IMG-2165.jpg](https://i.postimg.cc/7ZhNmP00/IMG-2165.jpg)](https://postimg.cc/pmN8dH0L)

</br>

이것으로 허프먼 부호를 구하기 위한 트리 구조가 완성됐다.

</br>

[![IMG-2166.jpg](https://i.postimg.cc/02BS5YKK/IMG-2166.jpg)](https://postimg.cc/3d2NnDB3)

</br>

각 문자의 등장 빈도를 다시 표시했다. 다음은 0과 1을 이용한 부호화를 해보겠다.

</br>

[![IMG-2167.jpg](https://i.postimg.cc/pTC9wztT/IMG-2167.jpg)](https://postimg.cc/R63Vf3h5)

</br>

0과 1의 부호를, 상하로 연결하는 가지에 각각 할당한다.

</br>

[![IMG-2168.jpg](https://i.postimg.cc/3NyKtv8z/IMG-2168.jpg)](https://postimg.cc/GTCw29sj)

</br>

0과 1의 할당은 역순이어도 상관 없다. 단, 위쪽 가지를 1이라고 정하면 도중에 할당 방법을 변경할 수는 없다.

</br>

[![IMG-2169.jpg](https://i.postimg.cc/FzqKvxC9/IMG-2169.jpg)](https://postimg.cc/dZ2FmGKX)

</br>

모든 부호를 할당했다. 다음은 트리의 뿌리로부터 각 문자를 따라가면서 대응하는 문자를 결정한다.

</br>

[![IMG-2170.jpg](https://i.postimg.cc/pT3TbZ6P/IMG-2170.jpg)](https://postimg.cc/r0Cc5STH)

</br>

A인 경우

</br>

[![IMG-2171.jpg](https://i.postimg.cc/mZNfGjqV/IMG-2171.jpg)](https://postimg.cc/DmZYrr7b)

</br>

할당된 부호는 0이 된다.

</br>

[![IMG-2172.jpg](https://i.postimg.cc/254TBcnK/IMG-2172.jpg)](https://postimg.cc/PL51gM3W)

</br>

B인 경우

</br>

[![IMG-2173.jpg](https://i.postimg.cc/zXghBLCd/IMG-2173.jpg)](https://postimg.cc/gnGjt2BR)

</br>

할당된 부호는 10이 된다.

</br>

[![IMG-2174.jpg](https://i.postimg.cc/SsR2pjQf/IMG-2174.jpg)](https://postimg.cc/62s5rWv8)

</br>

C인 경우

</br>

[![IMG-2175.jpg](https://i.postimg.cc/rmHdycKX/IMG-2175.jpg)](https://postimg.cc/MMyZtC7d)

</br>

할당된 부호는 110이 된다.

</br>

[![IMG-2176.jpg](https://i.postimg.cc/VvMX354H/IMG-2176.jpg)](https://postimg.cc/H8YJMYqQ)

</br>

D인 경우

</br>

[![IMG-2177.jpg](https://i.postimg.cc/28Q4Gb11/IMG-2177.jpg)](https://postimg.cc/N509f07t)

</br>

할당된 부호는 111이 된다.

</br>

[![IMG-2178.jpg](https://i.postimg.cc/90GqLKF6/IMG-2178.jpg)](https://postimg.cc/K38zz9Tf)

</br>

이것으로 허프먼 부호에 의한 부호화가 완료됐다. 이 부호화 규칙을 이용해서 ABAABACD라는 문자열을 부호화하면 된다. '어떤 부호도 다른 부호의 선두에 포함돼서는 안된다.' 조건은 트리 구조이기 때문에 보장된다. 따라서 유일 복호 가능이면서 순간 부호가 된다. 또한, 등장 빈도가 높은 문자일 수록 비트 수가 작은 부호가 할당되므로 부호화 효율이 좋다는 것을 알 수 있다.

</br>

[![IMG-2179.jpg](https://i.postimg.cc/yd7qJS30/IMG-2179.jpg)](https://postimg.cc/xkpph8Rd)

</br>

구체적으로는 이 예의 경우 A의 등장 빈도(50%)보다 'C or D'의 등장 빈도(25%)가 작다. 따라서 'C or D'를 3비트로 표현해서라도 A를 1비트로 표현하는 것이 효율적이라는 것을 알 수 있다.

</br>

[![IMG-2180.jpg](https://i.postimg.cc/gc5MQZc4/IMG-2180.jpg)](https://postimg.cc/QVQkWVTW)

</br>

이렇게 찾은 부호화 규칙을 이용해서 ABAABACD를 부호화해보겠다.

</br>

[![IMG-2181.jpg](https://i.postimg.cc/ZKp1LcP6/IMG-2181.jpg)](https://postimg.cc/rKynV5Pp)

</br>

결과는 14비트가 되며 하나의 문자를 2비트로 표현한 것보다 더 짧아졌다.

</br>

[![IMG-2182.jpg](https://i.postimg.cc/wBZVZKgM/IMG-2182.jpg)](https://postimg.cc/LqkLgbqF)

</br>

다른 한 가지 예를 보겠다. 각 문자의 등장 빈도에 큰 차이가 없는 경우이다. 편의상 문자열 순서에 따라 등장 빈도가 낮아지도록 설정하겠다. 따라서 정렬은 불필요하다. 다음은 등장 빈도가 낮은 순으로 두 개의 문자를 찾는다.

</br>

[![IMG-2183.jpg](https://i.postimg.cc/x1qL2ssz/IMG-2183.jpg)](https://postimg.cc/rDXDG92V)

</br>

여기선 C(22%)와 D(18%)가 된다.

</br>

[![IMG-2185.jpg](https://i.postimg.cc/4d8Js12Y/IMG-2185.jpg)](https://postimg.cc/7G2vNSk4)

</br>

두 개의 문자를 연결해서 트리 구조를 만든다.

</br>

[![IMG-2186.jpg](https://i.postimg.cc/RZQxvRNv/IMG-2186.jpg)](https://postimg.cc/ZWRMc68Q)

</br>

두 개의 문자를 'C or D'로 합체해서 등장 빈도를 더한다.

</br>

[![IMG-2187.jpg](https://i.postimg.cc/NLqZc9ty/IMG-2187.jpg)](https://postimg.cc/SYdgLKJq)

</br>

'C or D'를 하나의 문자로 생각하고 동일한 작업을 반복한다. A, B, 'C or D'의 세 개 중에서 등장 빈도가 낮은 순으로 두 개의 문자를 찾는다.

</br>

[![IMG-2188.jpg](https://i.postimg.cc/3JwTC6rV/IMG-2188.jpg)](https://postimg.cc/F1w8hTLV)

</br>

이 경우 A(35%)와 B(25%)가 된다.


</br>

[![IMG-2189.jpg](https://i.postimg.cc/sgZbTCk6/IMG-2189.jpg)](https://postimg.cc/0zPtNF2D)

</br>

두 개의 문자를 연결해서 트리 구조를 만든다.

</br>

[![IMG-2190.jpg](https://i.postimg.cc/TwhsW8JJ/IMG-2190.jpg)](https://postimg.cc/TLM0Z4SK)

</br>

두 개의 문자를 'A or B'로 합체하고 등장 빈도를 더한다.

</br>

[![IMG-2191.jpg](https://i.postimg.cc/wMphYLMR/IMG-2191.jpg)](https://postimg.cc/LYxqzqzm)

</br>

'A or B'를 하나의 문자열로 생각한다.

</br>

[![IMG-2192.jpg](https://i.postimg.cc/tT06FWhv/IMG-2192.jpg)](https://postimg.cc/Y43jH4DQ)

</br>

동일하게 등장 빈도가 작은 두 개의 문자를 선택하는데, 이번에는 마지막에 남은 'A or B'와 'C or D' 두 개를 연결하게 된다.

</br>

[![IMG-2193.jpg](https://i.postimg.cc/xTFcKLQG/IMG-2193.jpg)](https://postimg.cc/KRBGbkR4)

</br>

양쪽을 연결해서 트리 구조를 만든다.

</br>

[![IMG-2194.jpg](https://i.postimg.cc/brwwnwFF/IMG-2194.jpg)](https://postimg.cc/hzNnWcn9)

</br>

모든 숫자가 'A or B C or D'로 하나의 문자가 됐다. 등장 빈도는 당연히 100%가 된다.

</br>

[![IMG-2195.jpg](https://i.postimg.cc/XvnSqDPs/IMG-2195.jpg)](https://postimg.cc/Bj7wwN4F)

</br>

이것으로 허프만 부호를 구하기 위한 트리 구조가 완성됐다.

</br>

[![IMG-2196.jpg](https://i.postimg.cc/wx1v97L7/IMG-2196.jpg)](https://postimg.cc/yWzBP6fH)

</br>

각 문자의 등장 빈도를 다시 표시했다.

</br>

[![IMG-2197.jpg](https://i.postimg.cc/ZqDSQxfj/IMG-2197.jpg)](https://postimg.cc/bGbWDkf2)

</br>

0과 1인 부호를 상하로 연결된 각 가지에 할당한다. 다음은 트리의 뿌리로부터 각 문자를 따라가면서 대응하는 문자를 결정한다.

</br>

[![IMG-2198.jpg](https://i.postimg.cc/02dqvsWz/IMG-2198.jpg)](https://postimg.cc/ppTSQgtv)

</br>

A인 경우 할당된 부호는 00이 된다. 

</br>

[![IMG-2199.jpg](https://i.postimg.cc/YCqTwmLP/IMG-2199.jpg)](https://postimg.cc/mtJmYkw3)

</br>

B인 경우 할당된 부호는 01이 된다.

</br>

[![IMG-2200.jpg](https://i.postimg.cc/rFvRB5HV/IMG-2200.jpg)](https://postimg.cc/crBJYtZ2)

</br>

C인 경우 할당된 부호는 10이 된다.

</br>

[![IMG-2201.jpg](https://i.postimg.cc/cHHJgJzk/IMG-2201.jpg)](https://postimg.cc/PLgH0dT1)

</br>

D인 경우 할당된 부호는 11이 된다.

</br>

[![IMG-2201.jpg](https://i.postimg.cc/cHHJgJzk/IMG-2201.jpg)](https://postimg.cc/PLgH0dT1)

</br>

이것으로 허프만에 의한 부호화를 완료했다.

앞의 예와 트리 구조가 다르며, 문자의 등장 빈도에 큰 차이가 없어서 모든 문자가 2비트의 부호로 표현된다. 예를 들어 등장 빈도가 가장 높은 A를 1비트로 표현하기 위해 C와 D를 3비트로 표현하려고 해도 'C or D'의 등장 빈도(40%)는 A의 등장 빈도(35%)보다 높아서 부호화 효율이 나빠진다.

이처럼 허프만 부호는 문자의 등장 빈도에 따라 효율이 좋은 부호화를 쉽게 구현할 수 있다는 것을 알 수 있다.