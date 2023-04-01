# 전자 서명(Electronic signature)

</br>

[![IMG-2428.jpg](https://i.postimg.cc/zDtGJBTN/IMG-2428.jpg)](https://postimg.cc/7bzk9qBt)

</br>

전자 서명은 메세지 인증 코드가 가지는 '인증'과 '변조 검출' 두 가지 기능에 '부인 방지'를 추가한 것이다.

메세지 인증 코드에 대해 간단히 살펴보겠다.

</br>

[![IMG-2429.jpg](https://i.postimg.cc/MTrJ8nNr/IMG-2429.jpg)](https://postimg.cc/FdcByH9j)

</br>

메세지 인증 코드란 메세지에 MAC을 부여하므로 메세지 전송자가 키의 소유자임을 증명하기 위한 구조이다. 여기선 편의상 메세지는 암호화하지 않고 전송되는 걸로 간주한다.

</br>

[![IMG-2430.jpg](https://i.postimg.cc/c6yjswmT/IMG-2430.jpg)](https://postimg.cc/XBLxLZty)

</br>

A는 메세지와 MAC 및 MAC 작성에 사용한 키를 B에게 보낸다.

</br>

[![IMG-2431.jpg](https://i.postimg.cc/fRwsmQcC/IMG-2431.jpg)](https://postimg.cc/0bHh13HK)

</br>

B는 받은 메세지와 키로부터 MAC을 재작성하고 그것이 받은 MAC과 같은 것인지 확인한다. 이것으로 전송자가 A인 것과 받은 메세지가 변조되지 않은 것을 확인할 수 있다.

</br>

[![IMG-2432.jpg](https://i.postimg.cc/1XPC2s5Y/IMG-2432.jpg)](https://postimg.cc/62jfGsZd)

</br>

하지만 메세지 인증 코드는 공통기를 이용하는 구조이므로 키를 가진 누구나나 메세지 전송자가 될 수 있다. 예를 들어 A가 B에게 메세지를 전송한 후에 해당 메세지는 B의 임의의로 작성한 것이라고 주장할 수 있다. 또한, 공통키를 이용하고 있어서 A가 B 이외의 사람에게 메세지를 전송하려면 다른 키를 준비해야 한다.

</br>

[![IMG-2433.jpg](https://i.postimg.cc/mrY7qMzB/IMG-2433.jpg)](https://postimg.cc/rdpdRDNP)

</br>

한편 전자 서명 구조에선 MAC이 아닌 전송자만 작성할 수 있는 '전자 서명'이라는 데이터를 이용해서 메세지 작성자가 누구인지 식별할 수 있다. 이 데이터를 전자 서명이라고 한다.

구조를 보도록 하겠다.

</br>

[![IMG-2434.jpg](https://i.postimg.cc/P5zxnM43/IMG-2434.jpg)](https://postimg.cc/18XPpwbw)

</br>

그림에 'Sig'라고 적힌 전자 서명은 A만 작성할 수 있다.

</br>

[![IMG-2435.jpg](https://i.postimg.cc/cJCr7nRF/IMG-2435.jpg)](https://postimg.cc/1gxms4YF)

</br>

A의 전자 서명이 첨부된 메세지를 전송한 경우, 전송자가 A인 것이 보장된다.

</br>

[![IMG-2436.jpg](https://i.postimg.cc/3Rpr9CdF/IMG-2436.jpg)](https://postimg.cc/qhJdvKcN)

</br>

메세지를 받은 B는 전자 서명이 A의 것인지 확인할 수 있지만, 동일한 전자 서명을 만들 수는 없다.

</br>

[![IMG-2437.jpg](https://i.postimg.cc/y8kHvXG3/IMG-2437.jpg)](https://postimg.cc/sMdq2Ss3)

</br>

메세지 인증 코드와 달리 공통키를 사용하지 않으므로 A는 동일 전자 서명을 사용해서 여러 사람에게 메세지를 전송할 수 있다.

전자 서명의 작성 방법을 구체적으로 살펴 보겠다. 메세지 인증 코드에선 MAC 작성에 사용하는 키가 공통이었지만

</br>

[![IMG-2438.jpg](https://i.postimg.cc/44q1CG43/IMG-2438.jpg)](https://postimg.cc/t7d6PLx0)

</br>

전자 서명 작성에는 '공개키 암호 방식'의 순서를 응용한다.

</br>

[![IMG-2439.jpg](https://i.postimg.cc/5tKCw56t/IMG-2439.jpg)](https://postimg.cc/McRHwQ0k)

</br>

A가 B에게 암호화한 데이터를 전송하려고 한다. 먼저 데이터를 전달 받은 B가 공개키(P)와 비밀키(S)를 만든다.

</br>

[![IMG-2440.jpg](https://i.postimg.cc/jqPD5YQ2/IMG-2440.jpg)](https://postimg.cc/K4cGqVWh)

</br>

B가 A에게 공개키를 전달한다.

</br>

[![IMG-2441.jpg](https://i.postimg.cc/pd3dWsmK/IMG-2441.jpg)](https://postimg.cc/TyqxQqqP)

</br>

A는 받은 공개키를 사용해서 데이터를 암호화한다.

</br>

[![IMG-2442.jpg](https://i.postimg.cc/7Z6PSF7g/IMG-2442.jpg)](https://postimg.cc/HVqCgP6x)

</br>

암호문을 B에게 보낸다.

</br>

[![IMG-2443.jpg](https://i.postimg.cc/8zjD7hQ4/IMG-2443.jpg)](https://postimg.cc/87Qx3fCf)

</br>

B는 받은 암호문을 비밀키를 사용해서 원 데이터로 복원한다. 이것으로 작업이 완료된다. 공개키 암호 방식에선 암호화에 공개키, 복호화에 비밀키를 사용했다. 따라서 공개키를 사용해서 누구나 데이터를 암호화할 수 있지만 비밀키는 B만 가지고 있으므로 B만 복호화할 수 있다는 것이 보장된다.

</br>

[![IMG-2444.jpg](https://i.postimg.cc/43s581fb/IMG-2444.jpg)](https://postimg.cc/Mn3VHVjv)

</br>

그러면 이 순서를 반대로 해서 비밀키를 암호화하고 공개키를 복호화하면 공개키를 복호화하면 비밀키를 가진 A만 암호화할 수 있지만, 공개키를 사용해서 누구나 복호화할 수 있는 암호문이 작성된다. 암호로서는 전혀 의미가 없지만, 관점을 바꾸면 이 암호문의 작성자가 비밀키를 가진 A라는 것이 보장되게 된다. 전자 서명에선 이 A만이 만들 수 있는 암호문을 '서명'으로 활용한다. 참고로 엄밀히 말해선 서명의 작성은 '암호문'과 다른 계산 방법인 경우도 있다. 하지만 서명의 작성에는 비밀키를 사용하고 서명 검증에선 공개키를 사용한다는 점은 공통이므로 여기선 편의상 그렇게 설명하고 있다.

</br>

[![IMG-2445.jpg](https://i.postimg.cc/FRmHk7xK/IMG-2445.jpg)](https://postimg.cc/Ty76Z2F8)

</br>

전자 서명을 사용한 메세지 교환 순서를 보도록 하겠다.

먼저 A가 전송하고 싶은 메세지와 비밀키, 공개키를 준비한다. 메세지 전송 측이 비밀키와 공개키를 준비하는 점이 공개키 암호 방식과 다르다.

</br>

[![IMG-2446.jpg](https://i.postimg.cc/wjmqWhfv/IMG-2446.jpg)](https://postimg.cc/LJmF5ZMK)

</br>

A는 B에게 공개키를 전달한다.

</br>

[![IMG-2447.jpg](https://i.postimg.cc/HnrDrgFx/IMG-2447.jpg)](https://postimg.cc/8fgnYqpQ)

</br>

비밀키를 사용해서 메세지를 암호화한다.

</br>

[![IMG-2448.jpg](https://i.postimg.cc/FstNYfsX/IMG-2448.jpg)](https://postimg.cc/HjtfKky6)

</br>

이것(메세지를 암호화한 것)이 전자 서명이다. 이후 그림에선 Sig라고 표시하고 있다.

</br>

[![IMG-2449.jpg](https://i.postimg.cc/9FjHWvJW/IMG-2449.jpg)](https://postimg.cc/5jpRgKhG)

</br>

메세지와 서명을 B에게 전송한다.

</br>

[![IMG-2450.jpg](https://i.postimg.cc/yN2rLZGV/IMG-2450.jpg)](https://postimg.cc/FfgZR7mq)

</br>

B는 공개키를 사용해서 암호문(서명)을 복호화한다.

</br>

[![IMG-2451.jpg](https://i.postimg.cc/x855VJ6N/IMG-2451.jpg)](https://postimg.cc/kRVKx437)

</br>

복호화한 메세지와 받은 메세지가 일치하는지 확인한다. 이것으로 데이터 교환이 마무리 된다. A의 공개키로 복호화할 수 있는 암호문은 A 본인만 만들 수 있는 것이다. 이 때문에 메세지를 전송한 것이 A라는 것과 메세지가 변조되지 않았다는 것을 판단할 수 있다. 또한, A의 서명은 공개키만 가진 B는 작성할 수 없으므로 부인 방지 역할도 하게 된다. 단, 공개키 암호 방식은 암호화와 복호화 모두 시간이 걸리는 경향이 있다.

</br>

[![IMG-2452.jpg](https://i.postimg.cc/xddc6kzF/IMG-2452.jpg)](https://postimg.cc/5XZ402pw)

</br>

따라서 계산 시간을 단축하기 위해 실제로는 메세지를 직접 암호화하는 것이 아니라

</br>

[![IMG-2453.jpg](https://i.postimg.cc/VLNpLmXP/IMG-2453.jpg)](https://postimg.cc/G9ZqX0MX)

</br>

먼저 메세지의 해시값을 구한 후

</br>

[![IMG-2454.jpg](https://i.postimg.cc/qRkQbxLH/IMG-2454.jpg)](https://postimg.cc/2qK43vM0)

</br>

그것을 암호화해서 서명으로 사용한다.

</br>

[![IMG-2455.jpg](https://i.postimg.cc/gcL4MjyJ/IMG-2455.jpg)](https://postimg.cc/s1ypxVNd)

</br>

메세지와 서명을 B에게 전송한다.

</br>

[![IMG-2456.jpg](https://i.postimg.cc/FK107CDR/IMG-2456.jpg)](https://postimg.cc/cKyvzhqy)

</br>

B도 마찬가지로 받은 메세지의 해시값을 구한다.

</br>

[![IMG-2457.jpg](https://i.postimg.cc/zGvyjbW2/IMG-2457.jpg)](https://postimg.cc/PCGffqS1)

</br>

다음은 받은 서명을 공개키로 복호화해서 해시값을 구한다.

</br>

[![IMG-2458.jpg](https://i.postimg.cc/Y0xvXQbZ/IMG-2458.jpg)](https://postimg.cc/xNcj8Nr3)

</br>

구한 두 개의 해시갑싱 같은지 확인이 되면 전자 서명을 사용한 데이터 교환이 완료된다. '인증', '변조 검출', '부인 방지' 기능을 모두 갖춘 전자 서명이지만 한 가지 문제가 있다.

</br>

[![IMG-2459.jpg](https://i.postimg.cc/qRxB04yC/IMG-2459.jpg)](https://postimg.cc/xJqV3rs0)

</br>

B는 전자 서명을 이용한 데이터 교환해서 메세지 전송자가 A라고 믿고 있지만

</br>

[![IMG-2460.jpg](https://i.postimg.cc/k5r7bByb/IMG-2460.jpg)](https://postimg.cc/k2crrMzJ)

</br>

실제로는 A로 가장한 X와 데이터를 주고받을 가능성이 존재한다.

</br>

[![IMG-2461.jpg](https://i.postimg.cc/Vs3wTJ3H/IMG-2461.jpg)](https://postimg.cc/XXctBYNw)

</br>

그 근본적인 원인은, 공개키 암호 방식에서 공개키가 누구 것인지 알 수 없다는 데 있다.

</br>

[![IMG-2462.jpg](https://i.postimg.cc/kgJph9Xp/IMG-2462.jpg)](https://postimg.cc/qzFwzPKs)

</br>

받은 공개키에는 작성자를 가리키는 정보가 일절 포함돼 있지 않다.

</br>

[![IMG-2463.jpg](https://i.postimg.cc/mr0VRGBR/IMG-2463.jpg)](https://postimg.cc/0607dFzH)

</br>

[![IMG-2464.jpg](https://i.postimg.cc/0yzpNHtN/IMG-2464.jpg)](https://postimg.cc/5XMH7pWc)

</br>

정말로 A가 작성한 공개키일 가능성도 있어서 확실하게 판단하기가 어렵다.

</br>

[![IMG-2465.jpg](https://i.postimg.cc/d0MTVQkW/IMG-2465.jpg)](https://postimg.cc/dhB0WY9d)

</br>

이 문제는 '전자 인증서'를 사용하면 해결할 수 있다. 전자 인증서에선 공개키에 작성자의 정보를 첨부한 것을 인증서로 사용한다.