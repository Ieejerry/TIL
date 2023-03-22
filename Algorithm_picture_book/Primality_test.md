# 소수 판별법(Primality test)

</br>

[![IMG-2058.jpg](https://i.postimg.cc/ZnrXqQ7N/IMG-2058.jpg)](https://postimg.cc/gL2gSgPc)

</br>

소수 판별법은 특정 자연수가 소수인지를 판별하는 방법이다. 소수(prime number)란 1과 자신 이외는 약수로 가지지 않는 1보다 큰 자연수이다. 현대 암호 기술에서 자주 사용되는 'RSA ₩암호'에선 매우 큰 소수를 다룬다. RSA 암호에선 소수 판별법이 중요한 역할을 한다.

</br>

[![IMG-2059.jpg](https://i.postimg.cc/kg3XfVtM/IMG-2059.jpg)](https://postimg.cc/svmr2gcb)

</br>

소수 판별법을 설명하기 전에 mod 연산에 대해 알아보겠다. mod 연산은 나눗셈의 나머지를 구하는 연산이다. A mod B는 A를 B로 나누었을 때의 나머지 C를 구한다.

</br>

[![IMG-2060.jpg](https://i.postimg.cc/FK1rK0MZ/IMG-2060.jpg)](https://postimg.cc/nsbbR9cj)

</br>

구체적인 숫자를 사용한 연산 예를 보겠다.

</br>

[![IMG-2061.jpg](https://i.postimg.cc/GmHV8zpH/IMG-2061.jpg)](https://postimg.cc/Hr1BFwXg)

</br>

3599라는 숫자가 소수인지 판별하는 예를 보도록 하겠다. 단순한 방법으로는 3599를 2보다 큰 수로 차례대로 사용해가면서 완전히 나누어지는지를 확인하는 방법이 있다. '완전히 나누어진다'는 것은 나머지를 구하는 연산인 mod 연산의 결과가 0인 것을 의미한다. 3599의 제곱근은 59.99...이므로 2부터 59까지의 숫자를 차례대로 mod 연산을 하면 된다.

</br>

[![IMG-2070.jpg](https://i.postimg.cc/zfNQtNjR/IMG-2070.jpg)](https://postimg.cc/YvX80JTp)

</br>

실제로 mod 연산을 해보면 3599가 59로 완전히 나누어진다는 것을 알 수 있다.

</br>

[![IMG-2071.jpg](https://i.postimg.cc/1X1MtcjV/IMG-2071.jpg)](https://postimg.cc/Hc3bv5HT)

</br>

즉, 3599는 소수가 아니라는 결과가 된다. 하지만 이 방법은 판별한 숫자가 클수록 연산에 많은 시간이 걸려서 현실적이지 못하다.

</br>

[![IMG-2072.jpg](https://i.postimg.cc/ZKNM3YLq/IMG-2072.jpg)](https://postimg.cc/zVJ7Yr6m)

</br>

이 문제를 해결하는 방법으로 '페르마 테스트(Fermat test)'가 있다. 페르마 테스트는 확률적 소수 판별법이라고 불리며, 어떤 수가 '소수일 가능성이 높은지'를 판별하는 것이다. 페르마 테스트의 전체 지식이 되는 소수의 성질에 대해 설명하도록 하겠다.

</br>

[![IMG-2073.jpg](https://i.postimg.cc/WzFf5sLX/IMG-2073.jpg)](https://postimg.cc/JH8qnVhk)

</br>

예를 들어 소수인 5라는 숫자의 성질을 보도록 하겠다.

</br>

[![IMG-2078.jpg](https://i.postimg.cc/h4N76KRT/IMG-2078.jpg)](https://postimg.cc/hhbj7Wjt)

</br>

소수 5보다 작은 수를 각각 5 제곱하면 글미과 같은 결과가 된다.

</br>

[![IMG-2079.jpg](https://i.postimg.cc/YSQXGdNy/IMG-2079.jpg)](https://postimg.cc/Lq6kGBbz)

</br>

다음은 각각의 숫자를 mod 연산을 이용해 5로 나누어본다.

</br>

[![IMG-2080.jpg](https://i.postimg.cc/XNPwWwdZ/IMG-2080.jpg)](https://postimg.cc/K4nKr39F)

</br>

계산 결과는 그림과 같다.

</br>

[![IMG-2081.jpg](https://i.postimg.cc/vDRgVtt3/IMG-2081.jpg)](https://postimg.cc/K3N8XLVM)

</br>

원래 숫자와 나머지 값을 자세히 보면 양족이 일치하는 것을 알 수 있다.

</br>

[![IMG-2082.jpg](https://i.postimg.cc/50CFNrw6/IMG-2082.jpg)](https://postimg.cc/hzKG2pZB)

</br>

이를 통해 소수 5에 대해 위와 같은 식이 성립한다는 것을 알 수 있다.

</br>

[![IMG-2083.jpg](https://i.postimg.cc/T3swL92m/IMG-2083.jpg)](https://postimg.cc/G4kr6vyh)

</br>

이번에는 합성수(composite number)인 6이라는 숫자에 생각해보겠다.

</br>

[![IMG-2084.jpg](https://i.postimg.cc/02BxcNg1/IMG-2084.jpg)](https://postimg.cc/GHGZpdhX)

</br>

합성수라는 것은 소수가 아닌 자연수라는 것을 의미한다. 6이라는 숫자는 2 * 3으로 나타낼 수 있으므로 소수가 아니다.

</br>

[![IMG-2085.jpg](https://i.postimg.cc/43G05C3T/IMG-2085.jpg)](https://postimg.cc/gxM4zTRM)

</br>

동일한 계산을 하면

</br>

[![IMG-2086.jpg](https://i.postimg.cc/HWf1yhbT/IMG-2086.jpg)](https://postimg.cc/K4rWXQ9W)

</br>

5와 2의 경우 우너래 숫자와 나머지가 일치하지 않는 것을 알 수 있다.

</br>

[![IMG-2087.jpg](https://i.postimg.cc/cHg51d9w/IMG-2087.jpg)](https://postimg.cc/CB04mpVx)

</br>

사실은 5뿐만 아니라 모든 소수 p에 대해 이 식이 성립한다는 것이 이미 증명돼 있다.

</br>

[![IMG-2088.jpg](https://i.postimg.cc/Nfp8nWbc/IMG-2088.jpg)](https://postimg.cc/WhqJFYQW)

</br>

이것을 '페르마의 소정리'라고 한다. 페르마의 소정리를 만족하는지 여부로 소수 판별을 하는 방법이 '페르마 테스트'이다.

</br>

[![IMG-2089.jpg](https://i.postimg.cc/BvV4wQPK/IMG-2089.jpg)](https://postimg.cc/94Z6D2pm)

</br>

페르마 테스트를 사용해서 113이라는 수가 소수인지 판별해보겠다.

</br>

[![IMG-2090.jpg](https://i.postimg.cc/rmwR5mXR/IMG-2090.jpg)](https://postimg.cc/sBb2r323)

</br>

113보다 작은 수를 적당히 세 개 선택한다.

</br>

[![IMG-2091.jpg](https://i.postimg.cc/NMKTWMJq/IMG-2091.jpg)](https://postimg.cc/BLGXFqfM)

</br>

이 숫자들을 113 제곱한 후에 113으로 나눈 나머지를 구한다.

</br>

[![IMG-2092.jpg](https://i.postimg.cc/gJLXg7jG/IMG-2092.jpg)](https://postimg.cc/47ZxdBp0)

</br>

어떤 숫자라도 원래 숫자와 나머지 값이 일치한다.

</br>

[![IMG-2093.jpg](https://i.postimg.cc/G2v38n9T/IMG-2093.jpg)](https://postimg.cc/k6XPzZQ7)

</br>

일치하는지 여부를 확인하는 횟수를 늘릴수록 소수일 확실성이 높아진다.

</br>

[![IMG-2094.jpg](https://i.postimg.cc/qRwYZ15Z/IMG-2094.jpg)](https://postimg.cc/R63XWL9c)

</br>

단, p보다 작은 모든 수를 확인하려면 많은 시간이 걸린다. 실제로는 몇 개의 수만 확인해서 소수일 가능성이 충분히 높다고 판단할 수 있으면 '아마도 소수'라고 판정하고 있다. 예를 들어 RSA 암호에서 사용되는 소수 판별법에는 페르마 테스트를 개선한 '밀러-라빈(Miller-Rabin) 테스트'가 사용되고 있다. 방법에선 테스트를 반복해서 소수가 아닌 확률이 0.5의 80승보다 작은 단계에서 해당 수를 소수라고 판별한다.

</br>

[![IMG-2095.jpg](https://i.postimg.cc/KvSqDSjv/IMG-2095.jpg)](https://postimg.cc/xq539ZLW)

</br>

또한, 페르마 테스트를 모두 만족한다고 해도 소수라는 것을 확정할 수 없다.

</br>

[![IMG-2096.jpg](https://i.postimg.cc/RhrH5kZV/IMG-2096.jpg)](https://postimg.cc/tZ5TFm6L)

</br>

조사할 숫자가 소수이면 페르마 테스트에 부합하다.

</br>

[![IMG-2097.jpg](https://i.postimg.cc/kg9X3nNp/IMG-2097.jpg)](https://postimg.cc/QH4rcZyQ)

</br>

한편 조사할 숫자가 합성수인 경우 페르마 테스트에 걸리는 숫자가 대부분이지만

</br>

[![IMG-2098.jpg](https://i.postimg.cc/yYRTxzgK/IMG-2098.jpg)](https://postimg.cc/fJwdqpfq)

</br>

소수처럼 페르마 테스트에 부합한 합성수가 아주 적은 확률이지만 존재한다.

</br>

[![IMG-2099.jpg](https://i.postimg.cc/bwtY43B3/IMG-2099.jpg)](https://postimg.cc/zyq1gS5g)

</br>

예를 들어 561이라는 숫자를 생각해보겠다.

</br>

[![IMG-2100.jpg](https://i.postimg.cc/cLB3VxjD/IMG-2100.jpg)](https://postimg.cc/RWqqtBvf)

</br>

561이라는 숫자는 3 11 17 로 나타낼 수 있으므로 합성수이지 소수가 아니다.

</br>

[![IMG-2101.jpg](https://i.postimg.cc/02drNtfj/IMG-2101.jpg)](https://postimg.cc/WhzsWwxc)

</br>

하지만 페르마 테스트에 부합하다.

</br>

[![IMG-2102.jpg](https://i.postimg.cc/jq6R6DJk/IMG-2102.jpg)](https://postimg.cc/kD4rqXsx)

</br>

이런 합성수를 '카마이클 수(Carmichael number)' 또는 '절대 유사소수(absolute pseudoprimes)'라고 한다. 카마이클 수를 작은 것부터 차례로 나열한 것이 위의 그림으로, 많지 않다는 것을 알 수 있다.

</br>

[![IMG-2103.jpg](https://i.postimg.cc/B6QBhLnc/IMG-2103.jpg)](https://postimg.cc/mcJ9krMt)

</br>

소수가 페르마 테스트에 모두 부합되는 것은 맞지만, 페르마 테스트를 모두 만족한다고 해서 해당 수가 소수라고 단언할 수 없다. 어디까지나 페르마 테스트는 확률적인 소수 판별법이다. 하지만 다른 효율적인 판별법이 없어서 많은 곳에서 사용되고 있다.