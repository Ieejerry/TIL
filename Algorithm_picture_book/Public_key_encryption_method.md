# 공개키 암호 방식(Public key encryption method)

</br>

[![IMG-2304.jpg](https://i.postimg.cc/KjrqbMsC/IMG-2304.jpg)](https://postimg.cc/zHvSSVNk)

</br>

공개키 암호 방식은 암호화와 복호화에 서로 다른 키를 사용하는 방식이다.

</br>

[![IMG-2305.jpg](https://i.postimg.cc/Hxb30MHj/IMG-2305.jpg)](https://postimg.cc/zbXn8Vy1)

</br>

암호화에 사용하는 키를 '공개키', 복호화에 사용하는 키를 '비밀키'라고 한다.


</br>

[![IMG-2306.jpg](https://i.postimg.cc/SRqdgKNd/IMG-2306.jpg)](https://postimg.cc/HcZbxdM8)

</br>

공통키 암호 방식에 비해 공개키 암호 방식의 경우 암호화 및 복호화에 시간이 많이 걸리는 경향이 있다.

</br>

[![IMG-2307.jpg](https://i.postimg.cc/GtQQV14C/IMG-2307.jpg)](https://postimg.cc/QKF1Kwg4)

</br>

공개키 암호 방식의 계산 방법으로는 그림과 같은 것이 있다.

</br>

[![IMG-2308.jpg](https://i.postimg.cc/02kZmr42/IMG-2308.jpg)](https://postimg.cc/RqYcxC9j)

</br>

공개키 암호 방식을 사용하는 데이터 교환의 전체적인 흐름을 보도록 하겠다. A가 B에게 인터넷을 통해 데이터를 전송하려고 하고 있다.

</br>

[![IMG-2309.jpg](https://i.postimg.cc/gjNV4q7c/IMG-2309.jpg)](https://postimg.cc/fSSSRXZ1)

</br>

먼저 데이터를 전달 받는 B가 공개키와 비밀키를 만든다.

</br>

[![IMG-2310.jpg](https://i.postimg.cc/P5LWzDQh/IMG-2310.jpg)](https://postimg.cc/LJpgmnW0)

</br>

그 중 공개키를 A에게 전송한다.

</br>

[![IMG-2311.jpg](https://i.postimg.cc/hvymV4Jf/IMG-2311.jpg)](https://postimg.cc/m19hssys)

</br>

A는 B에게 받은 공개키를 사용해서 데이터를 암호화한다.

</br>

[![IMG-2312.jpg](https://i.postimg.cc/C1v5QPw2/IMG-2312.jpg)](https://postimg.cc/7G2qCNG1)

</br>

암호문을 B에게 전송한다.

</br>

[![IMG-2313.jpg](https://i.postimg.cc/DZ54KfPB/IMG-2313.jpg)](https://postimg.cc/njjh4J5D)

</br>

B는 받은 암호문을 비밀키로 사용해 복호화한다. B는 원 데이터를 얻을 수 있다. 공개키와 암호문 모두 인터넷을 통해 전달되므로

</br>

[![IMG-2314.jpg](https://i.postimg.cc/wjhvpT6L/IMG-2314.jpg)](https://postimg.cc/xX1YGQN1)

</br>

악의를 가진 제 3자(X)가 훔쳐볼 가능성이 있다. 하지만 공개키로는 암호문을 복호화할 수 없으므로 X는 원 데이터를 얻을 수 없다. 공통키 암호 방식과 달리 공개키 암호 방식에선 '키 분배 문제'가 발생하지 않는다.

</br>

[![IMG-2315.jpg](https://i.postimg.cc/QM8XZQYZ/IMG-2315.jpg)](https://postimg.cc/xXZrKzS6)

</br>

이외에도 공개키 암호 방식은 불특정다수 간 데이터 교환이 쉽다는 장점이 있다. 구체적으로 보겠다. B가 미리 공개키와 비밀키를 준비했다고 하자. 공개키는 다른 사람들에게 노출돼도 문제가 없다.

</br>

[![IMG-2316.jpg](https://i.postimg.cc/VLXrYFgJ/IMG-2316.jpg)](https://postimg.cc/mt22jC04)

</br>

따라서 B는 공개키를 인터넷상에 공개할 수 있다.

</br>

[![IMG-2317.jpg](https://i.postimg.cc/QMYV6Y8y/IMG-2317.jpg)](https://postimg.cc/94TW0pqd)

</br>

반면 비밀키는 노출되지 않도록 엄중하게 관리할 필요가 있다.

</br>

[![IMG-2318.jpg](https://i.postimg.cc/50ZyJHF5/IMG-2318.jpg)](https://postimg.cc/vgtbLZhD)

</br>

B에게 데이터를 전송하고 싶은 사람이 여러 명인 경우를 생각해보겠다.

</br>

[![IMG-2319.jpg](https://i.postimg.cc/sx7XgVpk/IMG-2319.jpg)](https://postimg.cc/1VRPW17B)

</br>

데이터를 전송하는 사람은 B가 공개한 공개키를 가져온다.

</br>

[![IMG-2320.jpg](https://i.postimg.cc/y8vNdpZ8/IMG-2320.jpg)](https://postimg.cc/BjP37gpr)

</br>

전송하고 싶은 데이터를 이 공개키로 암호화한다.

</br>

[![IMG-2321.jpg](https://i.postimg.cc/15KmC7Mr/IMG-2321.jpg)](https://postimg.cc/gnnbrDCx)

</br>

그리고 암호문을 B에게 보낸다.

</br>

[![IMG-2322.jpg](https://i.postimg.cc/ZqWJqbmw/IMG-2322.jpg)](https://postimg.cc/SXbBTpJ9)

</br>

B는 받은 암호문을 비밀키를 사용해서 복호화한다. 이것으로 B는 원 데이터를 얻을 수 있다. 이처럼 데이터를 전송하는 상대방 모두가 키를 가지고 있을 필요가 없다. 또한, 데이터를 받는 쪽만 노출되지 않은 키를 소유하면 되므로 안전성도 높다.

</br>

[![IMG-2323.jpg](https://i.postimg.cc/59SWbYvx/IMG-2323.jpg)](https://postimg.cc/5jyRmtnG)

</br>

한편 공개키 암호 방식에는 두 가지 문제점이 있다. 첫 번째는 암호화 및 복호화에 시간이 많이 걸린다는 점이다. 따라서 상세한 데이터를 연속적으로 교환하는 구조에는 적합하지 않다. 이 문제를 해결하려면 '하이브리드 암호 방식'을 사용해야 한다.

</br>

[![IMG-2324.jpg](https://i.postimg.cc/5y7PjVbm/IMG-2324.jpg)](https://postimg.cc/BPF5wR88)

</br>

두 번째는 공개키의 신뢰도에 관한 문제이다. 상황을 B가 공개키와 비밀키로 만든 시점으로 돌려보겠다.

</br>

[![IMG-2325.jpg](https://i.postimg.cc/c4z9S0Dx/IMG-2325.jpg)](https://postimg.cc/ZCrFPtt2)

</br>

설명을 위해 B가 작성한 공개키를 'PB', 비밀키를 'SB'라고 표시하겠다.

</br>

[![IMG-2326.jpg](https://i.postimg.cc/C5QNSssP/IMG-2326.jpg)](https://postimg.cc/JHjJQJgZ)

</br>

A가 B에게 보낸 데이터를 훔쳐 보려는 X가, 공개키 Px와 비밀키 Sx를 만든다.

</br>

[![IMG-2327.jpg](https://i.postimg.cc/R0BTSFwB/IMG-2327.jpg)](https://postimg.cc/JspXKRT6)

</br>

B가 공개키 PB를 A에게 보낼 때에

</br>

[![IMG-2328.jpg](https://i.postimg.cc/FHjjB48n/IMG-2328.jpg)](https://postimg.cc/FYHdY29j)

</br>

X가 공개키 PB를 자신이 만든 Px로 바꾼다.

</br>

[![IMG-2329.jpg](https://i.postimg.cc/ZRgBq7Xd/IMG-2329.jpg)](https://postimg.cc/S26NTrSS)

</br>

공개키 Px를 A에게 전달한다. 공개키 자체에는 누가 작성한지를 표시하는 수단이 없다. 따라서 A가 받은 공개키가 바뀐 것이라는 것을 알 수 없다.

</br>

[![IMG-2330.jpg](https://i.postimg.cc/y8PPvRDb/IMG-2330.jpg)](https://postimg.cc/k22K5BFQ)

</br>

A는 공개키 Px로 데이터를 암호화한다.

</br>

[![IMG-2331.jpg](https://i.postimg.cc/mrkQj5fP/IMG-2331.jpg)](https://postimg.cc/5HcYNptJ)

</br>

A가 암호문을 B에게 보내려고 할 때

</br>

[![IMG-2332.jpg](https://i.postimg.cc/HsmXRx1D/IMG-2332.jpg)](https://postimg.cc/5jPXFftn)

</br>

X가 이 암호문을 가로챈다. 이 암호문은 X가 만든 공개키 Px로 암호화된 것으로

</br>

[![IMG-2333.jpg](https://i.postimg.cc/rsMsnD0f/IMG-2333.jpg)](https://postimg.cc/FdCh1sxS)

</br>

X가 가진 비밀키Sx로 복호화할 수 있다.

</br>

[![IMG-2334.jpg](https://i.postimg.cc/Jnc4kR6Z/IMG-2334.jpg)](https://postimg.cc/JD0LwCWz)

</br>

X는 A가 B에게 보내려고 한 데이터를 가로챈다.

</br>

[![IMG-2335.jpg](https://i.postimg.cc/pLw2cm3K/IMG-2335.jpg)](https://postimg.cc/MnY2vp6G)

</br>

다음은 X가 B의 공개키인 PB로 데이터를 암호화한다.

</br>

[![IMG-2337.jpg](https://i.postimg.cc/fLHpFFk1/IMG-2337.jpg)](https://postimg.cc/KkM030P5)

</br>

작성한 암호문을 B에게 전달한다.

</br>

[![IMG-2338.jpg](https://i.postimg.cc/FRcGbB3j/IMG-2338.jpg)](https://postimg.cc/47fzsw8d)

</br>

이 암호문은 B가 만든 공개키 PB로 작성한 것이므로 B는 자신이 가지고 있는 SB로 복호화할 수 있다. B는 아무런 문제 없이 받은 암호문을 복호화할 수 있으므로 도중에 데이터가 노출된 것을 꿈에도 모른다. 이와 같이 도중에 공개키를 바꿔치기 해서 데이터를 가로채는 기법은 'man-in-the-middle 공격'이라고 한다. 문제 원인은, A가 받은 공개키의 작성자가 B인지 판단할 수 있는 방법이 없다는 것이다.

</br>

[![IMG-2339.jpg](https://i.postimg.cc/FRmkqWwb/IMG-2339.jpg)](https://postimg.cc/948fwpmz)

</br>

이 문제를 해결하려면 '전자 인증서'을 사용하면 된다.