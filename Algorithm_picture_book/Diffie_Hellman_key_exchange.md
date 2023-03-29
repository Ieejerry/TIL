# 디피-헬만 키 교환법(Diffie–Hellman key exchange)

</br>

[![IMG-2357.jpg](https://i.postimg.cc/Dz4Tq7Zm/IMG-2357.jpg)](https://postimg.cc/gwpQpF3P)

</br>

디피-헬만 키 교환법(Diffie–Hellman key exchange)은 안전하게 키를 교환하기 위한 기법이다. 수식을 사용해서 설명하기 전에 먼저 그림을 통해 개념적으로 접근해보도록 하겠다.

</br>

[![IMG-2358.jpg](https://i.postimg.cc/L8r7FL96/IMG-2358.jpg)](https://postimg.cc/yDynFJ3w)

</br>

두 개의 키를 합성하는 특별한 방법이 있다고 가정하겠다. 이 합성 방법으로 키 P와 키 S를 합성하면

</br>

[![IMG-2359.jpg](https://i.postimg.cc/Gh4q3tSB/IMG-2359.jpg)](https://postimg.cc/HVCQBYmH)

</br>

새로운 키 P-S가 만들어진다. 이 합성 방법에는 두 가지 특성이 있다.

</br>

[![IMG-2360.jpg](https://i.postimg.cc/WzFgVFbT/IMG-2360.jpg)](https://postimg.cc/K3bRrYMH)

</br>

첫 번째는 키 P와 그것을 이용해서 합성한 키 P-S가 있다고 해도

</br>

[![IMG-2361.jpg](https://i.postimg.cc/x1ypJCL9/IMG-2361.jpg)](https://postimg.cc/sMx4b3nL)

</br>

키 S를 추출하는 것은 불가능하다는 것이다. 즉, 키를 합성할 수는 있지만 분해할 수는 없다.

</br>

[![IMG-2362.jpg](https://i.postimg.cc/MZC99RDW/IMG-2362.jpg)](https://postimg.cc/14K0t82T)

</br>

두 번째는 합성된 키라도

</br>

[![IMG-2363.jpg](https://i.postimg.cc/BnqczC1G/IMG-2363.jpg)](https://postimg.cc/qz53hyLm)

</br>

새로운 키와 합성할 수 있다는 것이다. 그림에선 키 P-S를 이용해서 새로운 키 P-P-S가 만들어진다. 즉, 합성된 키를 다시 합성할 수 있다.

</br>

[![IMG-2364.jpg](https://i.postimg.cc/vHv55622/IMG-2364.jpg)](https://postimg.cc/mttcshs7)

</br>

이 합성 방법을 사용해서 A와 B 사이에 키를 안전하게 교환해보도록 하겠다.

</br>

[![IMG-2365.jpg](https://i.postimg.cc/K8z3LpM4/IMG-2365.jpg)](https://postimg.cc/BXrvfgNG)

</br>

먼저 A가 키 P를 준비한다. 이 키 P는 아무에게나 공개해도 괜찮다.

</br>

[![IMG-2366.jpg](https://i.postimg.cc/44P35bZc/IMG-2366.jpg)](https://postimg.cc/XXZ3N5rN)

</br>

A가 B에게 키 P를 전달한다.

</br>

[![IMG-2367.jpg](https://i.postimg.cc/CKbhfbmz/IMG-2367.jpg)](https://postimg.cc/8FPQ2f8S)

</br>

다음은 A와 B가 각각 비밀키 SA와 비밀키 SB를 준비한다. 키 SA와 키 SB는 제 3자가 모르게 관리해야 한다.

</br>

[![IMG-2368.jpg](https://i.postimg.cc/pXgMYp98/IMG-2368.jpg)](https://postimg.cc/F7g6hFVs)

</br>

A는 키 P와 비밀키 SA로부터 새로운 키 P-SA를 합성한다.

</br>

[![IMG-2369.jpg](https://i.postimg.cc/tRMKpYNf/IMG-2369.jpg)](https://postimg.cc/RqwsTC8Q)

</br>

B도 키 P와 비밀키 SB로부터 새로운 키 P-SB를 합성한다.

</br>

[![IMG-2370.jpg](https://i.postimg.cc/SR2tJffP/IMG-2370.jpg)](https://postimg.cc/30hZqp6j)

</br>

A가 B에게 키 P-SA를 보낸다.

</br>

[![IMG-2371.jpg](https://i.postimg.cc/8zSNg71G/IMG-2371.jpg)](https://postimg.cc/2V2P48b9)

</br>

마찬가지로 B도 A에게 P-SB를 보낸다.

</br>

[![IMG-2372.jpg](https://i.postimg.cc/J4bCxRj2/IMG-2372.jpg)](https://postimg.cc/w7TrT8fX)

</br>

A는 비밀키 SA와 B에게서 받은 키 P-SB를 합성해서 새로운 키 SA-P-SB를 얻는다.

</br>

[![IMG-2373.jpg](https://i.postimg.cc/GhP6YqC0/IMG-2373.jpg)](https://postimg.cc/hfjCR8vM)

</br>

동일하게 B도, 비밀키 SB와 A에게서 받은 키 P-SA를 합성해서 새로운 키 P-SA-SB를 얻는다. A와 B 모두 키 P-SA-SB를 가지게 된다. 이 키를 암호키, 복호키로 사용할 수 있다. 이 키 교환법의 안전성을 검증해보도록 하겠다.

</br>

[![IMG-2374.jpg](https://i.postimg.cc/hGQr8tdJ/IMG-2374.jpg)](https://postimg.cc/jWKPtKvK)

</br>

키 P, 키 P-SA, 키 P-SB는 인터넷을 경유해서 전송되기 때문에

</br>

[![IMG-2375.jpg](https://i.postimg.cc/pX0YgFQh/IMG-2375.jpg)](https://postimg.cc/xczzmq4n)

</br>

제 3자인 X가 훔쳐볼 가능성이 있다. 하지만 X가 얻은 키로는 키 P-SA-SB를 합성할 수 없다. 또한, 키는 분해할 수 없으므로 비밀키 SA와 SB를 얻을 수 없다. 따라서 X는 키 P-SA-SB를 만들 수 없으며 이 키 교환법은 안전하다고 볼 수 있다. 다음은 이 키 교환법을 수식으로 표현해보겠다.

</br>

[![IMG-2376.jpg](https://i.postimg.cc/6QV7Nssj/IMG-2376.jpg)](https://postimg.cc/d71Q8xVr)

</br>

먼저 mod 연산에 대해 설명하겠다. mod 연산은 나눗셈의 나머지를 구하는 연산이다. A mod B는 A를 B로 나누었을 때의 나머지 C를 구한다.

</br>

[![IMG-2377.jpg](https://i.postimg.cc/wTS3yxg4/IMG-2377.jpg)](https://postimg.cc/ppJP3H9K)

</br>

구체적인 숫자를 사용한 연산 예를 보겠다. 그러면 키 교환법을 수식으로 표현해보겠다.

</br>

[![IMG-2378.jpg](https://i.postimg.cc/nrXcrg5t/IMG-2378.jpg)](https://postimg.cc/RJzzbs4P)

</br>

가장 먼저 준비해야 하는 것은 키 P로, 수식에선 P와 G라는 두 개의 정수로 표현된다. P는 매우 큰 소수이고, G는 소수 P에 대응하는 '생성자'(또는 원시근(primitive root))라고 하는 숫자로부터 하나 선택한다. 소수 P의 생성자는 모든 소수 P에 대해 일정한 개수로 존재한다.

</br>

[![IMG-2379.jpg](https://i.postimg.cc/h4mV2YvY/IMG-2379.jpg)](https://postimg.cc/t7X1T2hd)

</br>

먼저 A가 소수 P와 생성자 G를 준비한다. 이들은 제 3자에게도 노출돼도 괜찮다.

</br>

[![IMG-2380.jpg](https://i.postimg.cc/tJzTLWLs/IMG-2380.jpg)](https://postimg.cc/n9CpmjVx)

</br>

A가 소수 P와 생성자 G를 B에게 전달한다.

</br>

[![IMG-2381.jpg](https://i.postimg.cc/15558gkK/IMG-2381.jpg)](https://postimg.cc/xqhS7dTk)

</br>

다은은 A와 B가 비밀값 X와 Y를 준비한다. 비밀값 X와 Y는 P-2보다도 작아야 한다.

</br>

[![IMG-2382.jpg](https://i.postimg.cc/c1TdGxvt/IMG-2382.jpg)](https://postimg.cc/dD7b8KmJ)

</br>

A와 B는 '(G를 비밀값으로 제곱) mod P'를 계산한다. 이 계산이 이론상의 '합성'에 해당한다.

</br>

[![IMG-2383.jpg](https://i.postimg.cc/bNWcqspr/IMG-2383.jpg)](https://postimg.cc/PPWF4fLn)

</br>

A와 B는 계산 결과를 서로 교환한다.

</br>

[![IMG-2384.jpg](https://i.postimg.cc/WzzCvPy0/IMG-2384.jpg)](https://postimg.cc/30MnXzYw)

</br>

A와 B는 서로에게서 받은 수를 자신의 비밀키로 제곱하고 mod P를 계산한다.

</br>

[![IMG-2385.jpg](https://i.postimg.cc/hjP3LBcN/IMG-2385.jpg)](https://postimg.cc/1g2HSbgK)

</br>

이 계산 결과는 A와 B 동일한 값이 된다. 이것으로 A와 B는 암호의 키로 사용할 수 있는 숫자를 공유하게 된다. 이 키 교환법의 안정성을 검증해보겠다.

</br>

[![IMG-2386.jpg](https://i.postimg.cc/J0Hxx7gY/IMG-2386.jpg)](https://postimg.cc/4HZpNGXp)

</br>

각각의 숫자는 인터넷을 경유해서 전달되므로

</br>

[![IMG-2387.jpg](https://i.postimg.cc/L8SdJGgF/IMG-2387.jpg)](https://postimg.cc/rKfZbn9f)

</br>

X가 훔쳐볼 가능성이 있다. 하지만 X가 얻은 숫자로는 A와 B가 공유하는 숫자를 계산할 수 없다. 또한, 비밀값 X와 Y를 구하는 것도 불가능하다. 소수 P, 생성자 G, G의 X승 mod P로부터 X를 구하는 문제는 '이산대수 문제'라고 불리며, 아직 효율적인 해법이 발견되지 않은 상태이다.

디피-헬만 키 교환법은 이 이산대수 문제를 이용한 키 교환법이라고 할 수 있다.