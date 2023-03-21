# 유클리드 호제법

</br>

<a href="https://ibb.co/LQPWCvV"><img src="https://i.ibb.co/wJLXKY5/IMG-2025.jpg" alt="IMG-2025" border="0"></a>

</br>

유클리드 호제법은 두 수의 최대공약수를 구하는 일고리즘이다. 유클리드에 의해 기원전 300년경에 발견된 것으로 세계에서 가장 오래된 알고리즘으로 알려져 있다.

</br>

<a href="https://ibb.co/WVgd2p5"><img src="https://i.ibb.co/fD4KxGF/IMG-2027.jpg" alt="IMG-2027" border="0"></a>

</br>

예로 1112와 695의 최대공약수를 계산해보도록 하겠다.

</br>

<a href="https://ibb.co/YPRLxRF"><img src="https://i.ibb.co/wB0zf0F/IMG-2028.jpg" alt="IMG-2028" border="0"></a>

</br>

일반적인 방법에선 두 개의 수를 소인수분해해서

</br>

<a href="https://ibb.co/BfHxLSh"><img src="https://i.ibb.co/51XyTfQ/IMG-2029.jpg" alt="IMG-2029" border="0"></a>

</br>

공통되는 소수를 최대공약수(GCD)로 구한다. 1112와 695의 최대공약수는 139라는 것을 알 수 있다. 하지만 이 방법에선 두 개의 수가 커질수록 소인수분해가 어려워진다. 유클리드 호제법에선 더 효율적으로 최대공약수를 구하는 것이 가능하다.

</br>

<a href="https://ibb.co/60Nd20Q"><img src="https://i.ibb.co/b57fx5t/IMG-2030.jpg" alt="IMG-2030" border="0"></a>

</br>

유클리드 호제법의 설명에 앞서 mod 연산에 대해 알아보겠다. mod 연산은 나눗셈의 나머지를 구하는 연산이다. A mod B는 A를 B로 나누었을 때의 나머지 C를 구한다.

</br>

<a href="https://ibb.co/wcfdhX2"><img src="https://i.ibb.co/8YHmgpQ/IMG-2031.jpg" alt="IMG-2031" border="0"></a>

</br>

구체적인 숫자를 사용한 연산 예를 보겠다.

</br>

<a href="https://ibb.co/h77V61x"><img src="https://i.ibb.co/kHHX76V/IMG-2032.jpg" alt="IMG-2032" border="0"></a>

</br>

그러면 유클리드 호제법의 과정을 보도록 하겠다.

</br>

<a href="https://ibb.co/8j5cjLM"><img src="https://i.ibb.co/hKWfKJs/IMG-2033.jpg" alt="IMG-2033" border="0"></a>

</br>

먼저 큰 숫자를 작은 숫자로 나눈 나머지를 구한다. 즉, 큰 숫자와 작은 숫자로 mod연산을 한다. 

</br>

<a href="https://ibb.co/StPXrMH"><img src="https://i.ibb.co/McsD6tK/IMG-2034.jpg" alt="IMG-2034" border="0"></a>

</br>

나눗셈의 결과 417이 나머지가 된다.

</br>

<a href="https://ibb.co/0ZHh1sY"><img src="https://i.ibb.co/P4qwJD1/IMG-2035.jpg" alt="IMG-2035" border="0"></a>

</br>

이번에는 나눈 수 695와 나머지 417로 mod연산을 한다.

</br>

<a href="https://ibb.co/b65k91w"><img src="https://i.ibb.co/D1fZ24c/IMG-2036.jpg" alt="IMG-2036" border="0"></a>

</br>

그 결과 278이 나온다.

</br>

<a href="https://ibb.co/2dkLfYr"><img src="https://i.ibb.co/qpr4PF8/IMG-2037.jpg" alt="IMG-2037" border="0"></a>

</br>

동일한 계산을 반복한다. 417과 287로 mod연산을 한다.

</br>

<a href="https://ibb.co/4YHMRnn"><img src="https://i.ibb.co/Yyx8BFF/IMG-2038.jpg" alt="IMG-2038" border="0"></a>

</br>

139가 나온다.

</br>

<a href="https://ibb.co/PcK6zpC"><img src="https://i.ibb.co/T46gqXh/IMG-2039.jpg" alt="IMG-2039" border="0"></a>

</br>

278과 138로 mod 연산을 하면

</br>

<a href="https://ibb.co/smFYxNM"><img src="https://i.ibb.co/kHhCbwW/IMG-2040.jpg" alt="IMG-2040" border="0"></a>

</br>

0이 나온다. 즉, 278은 139로 나누어지며 나머지가 없다.

</br>

<a href="https://ibb.co/CVvmv0V"><img src="https://i.ibb.co/XFpjpJF/IMG-2041.jpg" alt="IMG-2041" border="0"></a>

</br>

나머지가 0이 됐을 때 마지막 계산에서 나누는 수로 사용된 139가 1112와 695의 최대공약수가 된다.

어떻게 유클리드 호제법으로 최대공약수를 구하는지 알아보도록 하겠다.

</br>

<a href="https://ibb.co/S6f508H"><img src="https://i.ibb.co/VLwJDZb/IMG-2042.jpg" alt="IMG-2042" border="0"></a>

</br>

1112와 695를 각각 막대의 길이로 나타내본다.

</br>

<a href="https://ibb.co/Cm9vyqY"><img src="https://i.ibb.co/5Gjv3dS/IMG-2043.jpg" alt="IMG-2043" border="0"></a>

</br>

최대공약수를 n으로 해서 눈금을 나누어본다. 최대공약수가 139인지 알고 있으므로 이해하기 쉽도록 1112는 8눈금, 695는 6눈금으로 표시했다. 실제로는 각 막대를 몇 등분할 수 있는지 모른다. 단, 1112와 695 모두 최대공약수 n의 배수인 것은 알고있다. 여기서 앞서 계산한 것처럼 큰 숫자를 작은 숫자로 나눈 나머지를 구한다.

</br>

<a href="https://ibb.co/wY2Rg05"><img src="https://i.ibb.co/PtVNjmq/IMG-2044.jpg" alt="IMG-2044" border="0"></a>

</br>

<a href="https://ibb.co/bztqHHn"><img src="https://i.ibb.co/9sPzwwj/IMG-2045.jpg" alt="IMG-2045" border="0"></a>

</br>

417이라는 결과가 나온다. 그림을 통해 417도 n눈금으로 정확히 표시할 수 있다는 것을 알 수 있다. 동일한 방법으로 mod 연산을 반복한다.

</br>

<a href="https://ibb.co/KhLcQXJ"><img src="https://i.ibb.co/NCmgksM/IMG-2046.jpg" alt="IMG-2046" border="0"></a>

</br>

<a href="https://ibb.co/WpZqscL"><img src="https://i.ibb.co/4gz9JjH/IMG-2050.jpg" alt="IMG-2050" border="0"></a>

</br>

695를 417로 나누면 나머지 278이 나온다. 이 나머지 278도 n을 정수 배한 숫자로 동일한 최대공약수를 가진다.

</br>

<a href="https://ibb.co/LPvGkbs"><img src="https://i.ibb.co/yRV3fGx/IMG-2051.jpg" alt="IMG-2051" border="0"></a>

</br>

<a href="https://ibb.co/dMQtCMg"><img src="https://i.ibb.co/xLMY9LH/IMG-2055.jpg" alt="IMG-2055" border="0"></a>

</br>

계속해서 계산을 반복한다.

</br>

<a href="https://ibb.co/9yYhf2t"><img src="https://i.ibb.co/mhz0Yt8/IMG-2052.jpg" alt="IMG-2052" border="0"></a>

</br>

<a href="https://ibb.co/7kTdX63"><img src="https://i.ibb.co/41Dn75b/IMG-2053.jpg" alt="IMG-2053" border="0"></a>

</br>

278은 139로 나누어지므로 나머지가 0이 된다. 이 때 최대공약수 n이 139라는 것을 알 수 있다.

</br>

<a href="https://ibb.co/1qk8VQY"><img src="https://i.ibb.co/MVmMTSy/IMG-2054.jpg" alt="IMG-2054" border="0"></a>

</br>

이와 같이 유클리드 호제법에선 나눈셈만 반복하면 최대공약수를 구할 수 있다. 두 개의 숫자가 큰 수라도 정해진 순서로 계산하면 효율적으로 최대공약수를 구할 수 있는 것이 큰 장점이다.