# 해시 함수(Hash function)

</br>

[![IMG-2253.jpg](https://i.postimg.cc/k5tZXh60/IMG-2253.jpg)](https://postimg.cc/JyMKpxQx)

</br>

해시 함수란 주어진 데이터를 고정 길이의 불규칙적인 숫자로 변환하는 함수이다. 믹서리를 생각하면 이해하기 쉽다.

</br>

[![IMG-2254.jpg](https://i.postimg.cc/6pFjSLjY/IMG-2254.jpg)](https://postimg.cc/gxqHLRPZ)

</br>

데이터를 해시 함수에 넣으면

</br>

[![IMG-2255.jpg](https://i.postimg.cc/6q6YRHq5/IMG-2255.jpg)](https://postimg.cc/FdqyXV02)

</br>

뷸규칙한 숫자를 출력한다. 해시 함수는 데이터를 분리하는 기계라고 생각하면 이해하기 쉽다. 출력된 불규칙한 숫자를 '해시값'이라고 한다. 해시값은 숫자지만 16진수로 표기하는 경우가 많다.

</br>

[![IMG-2256.jpg](https://i.postimg.cc/ydxDZcBC/IMG-2256.jpg)](https://postimg.cc/9R3X34rL)

</br>

컴퓨터는 모든 데이터를 0과 1로 이루어진 2진수로 관리하고 있다.

</br>

[![IMG-2257.jpg](https://i.postimg.cc/mZFQpWff/IMG-2257.jpg)](https://postimg.cc/DmnJmDwB)

</br>

해시값도 데이터의 일종이므로, 표기는 16진수로 하지만 내부에선 2진수로 관리된다.

</br>

[![IMG-2258.jpg](https://i.postimg.cc/8zwWf1WW/IMG-2258.jpg)](https://postimg.cc/gxXrfbgk)

</br>

실제로는 해시 함수는 컴퓨터 내부에서 수치 계산을 하고 있는 것이다. 이런 내용을 전제로 해시 함수의 특징을 보도록 하겠다.

</br>

[![IMG-2259.jpg](https://i.postimg.cc/bvkhFvTS/IMG-2259.jpg)](https://postimg.cc/B8Skj4RJ)

</br>

첫 번째 특징은 출력하는 값의 데이터 길이가 바뀌지 않는다는 것이다. 출력되는 데이터의 길이는 함수에 따라 다르지만, 예를 들어 SHA-1에선 20바이트 고정된다.

</br>

[![IMG-2262.jpg](https://i.postimg.cc/43J5jLvv/IMG-2262.jpg)](https://postimg.cc/pm6zFB6y)

</br>

매우 큰 데이터를 입력해도 출력되는 해시값의 데이터 길이는 바뀌지 않는다.

</br>

[![IMG-2265.jpg](https://i.postimg.cc/XqwLTTP8/IMG-2265.jpg)](https://postimg.cc/Pv51DFTp)

</br>

마찬가지로 아무리 작은 데이터를 입력해도 해시값의 데이터 길이는 같다.

</br>

[![IMG-2266.jpg](https://i.postimg.cc/9Q18XHQg/IMG-2266.jpg)](https://postimg.cc/sMQ9K8S5)

</br>

두 번째 특징은 입력이 동일하면 출력도 반드시 동일하다는 것이다.

</br>

[![IMG-2267.jpg](https://i.postimg.cc/brzLf6jf/IMG-2267.jpg)](https://postimg.cc/N9zR1kMd)

</br>

세 번째 특징은, 비슷한 데이터를 입력해도 1비트라도 다른 데이터라면 출력이 크게 달리진다는 점이다. 비슷한 데이터를 입력한다고 해서 해시값도 비슷해지는 것은 아니라는 것이다.

</br>

[![IMG-2268.jpg](https://i.postimg.cc/j25NhBb2/IMG-2268.jpg)](https://postimg.cc/5Yh647jW)

</br>

네 번째 특징은, 전혀 다른 데이터를 입력해도 동일한 해시값이 나올 수 있는 경우가 낮은 확률이지만 존재한다는 것이다. 이것을 '해시값 충돌'이라고 한다.

</br>

[![IMG-2269.jpg](https://i.postimg.cc/Y9yjt952/IMG-2269.jpg)](https://postimg.cc/BLHJgqZR)

</br>

다섯 번째 특징은, 해시값으로부터 원 데이터를 역산하는 것이 사실상 불가능하다는 것이다. 데이터 입력과 출력의 흐름이 단반향으로 이루어지며 이것은 '암호화'와 크게 다른 점이다.

</br>

[![IMG-2270.jpg](https://i.postimg.cc/HLNVgjDY/IMG-2270.jpg)](https://postimg.cc/nsvHKFhg)

</br>

마지막 특징으로 해시값을 결정하는 계산이 비교적 간단하다는 것을 들 수 있다.

</br>

[![IMG-2271.jpg](https://i.postimg.cc/9050DSQs/IMG-2271.jpg)](https://postimg.cc/ftCDF8Xv)

</br>

해시 함수의 알고리즘에는 몇 가지가 있지만, 현재는 SHA-2가 일반적으로 사용된다.

</br>

[![IMG-2272.jpg](https://i.postimg.cc/k48XPcvs/IMG-2272.jpg)](https://postimg.cc/KkGyntV3)

</br>

해시 함수는 다양한 상황에서 사용된다. 해시 함수의 이용 예로 '메세지 인증 코드'와 '해시 테이블'이 있다.