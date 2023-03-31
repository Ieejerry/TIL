# 전자 인증서(Electronic certificate)

</br>

[![IMG-2467.jpg](https://i.postimg.cc/pXHZTxmz/IMG-2467.jpg)](https://postimg.cc/nM37RyYh)

</br>

공개키 암호 방식이나 전자 서명에선 공개키가 정말로 통신하고자 하는 상대인지 보장되지 않는다는 문제가 있었다.

</br>

[![IMG-2468.jpg](https://i.postimg.cc/wBQzC9R2/IMG-2468.jpg)](https://postimg.cc/kVGL83cR)

</br>

따라서 A가 B에게 공개키를 보내려고 할 때에

</br>

[![IMG-2469.jpg](https://i.postimg.cc/9QPsMJXF/IMG-2469.jpg)](https://postimg.cc/yDdLphSw)

</br>

악의를 지닌 제 3자가 공개키를 바꾸어 전달해도 받는 측에선 눈치재지 못할 수도 있다.

</br>

[![IMG-2470.jpg](https://i.postimg.cc/CMD3Xhyq/IMG-2470.jpg)](https://postimg.cc/w3q4sdjq)

</br>

전자 인증서를 이용하면 공개키 작성자가 누구인지를 보증할 수 있다.

</br>

[![IMG-2471.jpg](https://i.postimg.cc/8cHtGnBq/IMG-2471.jpg)](https://postimg.cc/BPjxcpzg)

</br>

전자 인증서의 구조를 구체적으로 보도록 하겠다.

A는 공개키 PA와 비밀키 SA 쌍을 가지고 있으며

</br>

[![IMG-2472.jpg](https://i.postimg.cc/W3m7mfKh/IMG-2472.jpg)](https://postimg.cc/CB1DSJwg)

</br>

공개키 PA를 B에게 보내려고 한다.

</br>

[![IMG-2473.jpg](https://i.postimg.cc/tC4zPkz4/IMG-2473.jpg)](https://postimg.cc/DmRs3qD9)

</br>

A는 먼저 인증 기관(CA: Certification Authority)에 공개키 PA가 자신의 것임을 나타내는 인증서 발행을 의뢰한다. 인증 기관은 전자 서명을 관리하기 위한 조직이다. 원론상으로는 누구든 인증 기관을 만들 수 있어서 많은 기관이 존재한다. 따라서 정부나 외부 기관을 통해 감사를 받은 대기업 등 신뢰할 수 있는 기관을 이용하는 것이 안전하다.

</br>

[![IMG-2474.jpg](https://i.postimg.cc/yxvtjN5g/IMG-2474.jpg)](https://postimg.cc/PvvSrddT)

</br>

인증 기관은 자신이 준비한 공개키 PC와 비밀키 SC를 보유하고 있다.

</br>

[![IMG-2475.jpg](https://i.postimg.cc/Vk1D7tnJ/IMG-2475.jpg)](https://postimg.cc/mtXYktd4)

</br>

A는 공개키 PA와 메일 주소를 포함한 개인 정보를 준비해서

</br>

[![IMG-2476.jpg](https://i.postimg.cc/RCdF65d2/IMG-2476.jpg)](https://postimg.cc/NLyYSnWx)

</br>

인증 기관에 보낸다.

</br>

[![IMG-2477.jpg](https://i.postimg.cc/rp96ncDk/IMG-2477.jpg)](https://postimg.cc/mch6kv3X)

</br>

확인을 완료하면 인증 기관의 비밀키 SC를 이용해서 A의 데이터로부터 전자 서명을 작성한다.

</br>

[![IMG-2478.jpg](https://i.postimg.cc/T1tgCy6D/IMG-2478.jpg)](https://postimg.cc/ZvyWq50b)

</br>

작성한 전자 서명과 데이터를 하나의 파일로 만든다.

</br>

[![IMG-2479.jpg](https://i.postimg.cc/G25bKrfp/IMG-2479.jpg)](https://postimg.cc/yg0qYqsq)

</br>

그리고 이 파일을 A에게 보낸다.

</br>

[![IMG-2480.jpg](https://i.postimg.cc/fb6NS5S3/IMG-2480.jpg)](https://postimg.cc/t1tfL35y)

</br>

이 파일이 A의 전자 인증서가 된다.

</br>

[![IMG-2481.jpg](https://i.postimg.cc/J0FcRy2W/IMG-2481.jpg)](https://postimg.cc/wRhsVBzW)

</br>

A는 공개키 대신에 전자 인증서를 B에게 보낸다.

</br>

[![IMG-2482.jpg](https://i.postimg.cc/nLt8Hry7/IMG-2482.jpg)](https://postimg.cc/zyp27zXX)

</br>

B는 받은 인증서에 적힌 메일 주소가 A의 것인지 확인한다.

</br>

[![IMG-2483.jpg](https://i.postimg.cc/8zXHH0HC/IMG-2483.jpg)](https://postimg.cc/pm8zVk3N)

</br>

계속해서 B는 인증 기관의 공개키를 취득한다.

</br>

[![IMG-2484.jpg](https://i.postimg.cc/3N6897dB/IMG-2484.jpg)](https://postimg.cc/D4r3y9QJ)

</br>

인증서 내의 서명이 인증 기관의 것인지 검증한다. 인증서의 서명은 인증 기관의 공개키 PC로만 검증할 수 있다. 즉, 검증 결과에 문제가 없다면 이 인증서는 인증 기관이 발행한 것이라는 것이 보증된다.

</br>

[![IMG-2485.jpg](https://i.postimg.cc/j5rVv2xv/IMG-2485.jpg)](https://postimg.cc/DW5Yw2bb)

</br>

인증서가 인증 기관에서 발행된 것이고 A의 것임이 확인됐으므로 인증서에서 A의 공개키 PA를 꺼낸다. 이것으로 A에게서 B로의 공개키 전달이 완료된다.

</br>

[![IMG-2486.jpg](https://i.postimg.cc/MTzPvQKk/IMG-2486.jpg)](https://postimg.cc/v1SLKDVX)

</br>

공개키 전달에 문제가 없는지 보도록 하겠다.

</br>

[![IMG-2487.jpg](https://i.postimg.cc/Y2nnC05V/IMG-2487.jpg)](https://postimg.cc/6TZLHW5L)

</br>

악의를 지닌 X가 A로 위장해서 B에게 공개키 PX를 전달하려고 한다.

</br>

[![IMG-2488.jpg](https://i.postimg.cc/3RbXY4kF/IMG-2488.jpg)](https://postimg.cc/xJMJPdyX)

</br>

하지만 B는 인증서로 전달되지 않는 공개키를 신뢰할 필요가 없다.

</br>

[![IMG-2489.jpg](https://i.postimg.cc/wjdrsvVk/IMG-2489.jpg)](https://postimg.cc/tY2kK981)

</br>

그렇다면 X가 A로 위장해서 인증 기관에 자신의 공개키를 등록하려고 하면 어떻게 될까?

</br>

[![IMG-2490.jpg](https://i.postimg.cc/vZHWjwHs/IMG-2490.jpg)](https://postimg.cc/pp4hh7FG)

</br>

X는 A의 메일 주소를 소유하고 있지 않아서 인증서를 발급 받을 수 없다. X는 X의 메일 주소를 이용한 증명서만 작성할 수 있게 된다. 따라서 A의 인증서를 가져올 수 없다. 전자 인증서를 사용해서 공개키 작성자를 확인할 수 있다는 것을 보았다.

</br>

[![IMG-2491.jpg](https://i.postimg.cc/3xvK3dwC/IMG-2491.jpg)](https://postimg.cc/pmPNZVzp)

</br>

그런데 앞에서 B는 인증 기관의 공개키를 받았다고 했지만

</br>

[![IMG-2492.jpg](https://i.postimg.cc/1zYh6S45/IMG-2492.jpg)](https://postimg.cc/8FW0Qqhq)

</br>

여기서 한가지 의문이 생긴다. B가 받은 공개키 PC는 정말 인증 기관이 발급한 것일까?

</br>

[![IMG-2493.jpg](https://i.postimg.cc/gJRSJbZ7/IMG-2493.jpg)](https://postimg.cc/cgxM9jT7)

</br>

공개키 자체는 작성자를 확인할 수단이 없으므로 인증 기관으로 위장한 X가 작성한 것일 수도 있다. 즉, 공개키가 가진 문제가 동일하게 발생하는 것이다.

</br>

[![IMG-2494.jpg](https://i.postimg.cc/HsPQfPJ8/IMG-2494.jpg)](https://postimg.cc/4mV7cPQX)

</br>

실은 이 인증 기관의 공개키 PC도

</br>

[![IMG-2495.jpg](https://i.postimg.cc/yNTWzkfp/IMG-2495.jpg)](https://postimg.cc/WDhsGbc0)

</br>

전자 인증서로 전달된다. 그렇다면 이 인증 기관의 인증서에는 누가 서명하는 것일까?

</br>

[![IMG-2496.jpg](https://i.postimg.cc/Dzf40rb3/IMG-2496.jpg)](https://postimg.cc/cvjL58mF)

</br>

더 상위에 있는 인증 기관이다.

</br>

[![IMG-2497.jpg](https://i.postimg.cc/50Y0Qn4T/IMG-2497.jpg)](https://postimg.cc/LYSRrkZ3)

</br>

인증 기관은 트리 구조로 돼 있으며 상위의 인증 기관이 하위 인증 기관의 인증서를 작성한다. 인증 기관의 트리 구조는 어떻게 형성되는 것일까?

</br>

[![IMG-2498.jpg](https://i.postimg.cc/T3tgrNx3/IMG-2498.jpg)](https://postimg.cc/rDtDTJzB)

</br>

예를 들어 많은 신뢰를 받는 인증 기관 Y가 있다고 하자

</br>

[![IMG-2499.jpg](https://i.postimg.cc/J0TMTXzZ/IMG-2499.jpg)](https://postimg.cc/MfjCHvRp)

</br>

여기에 새로운 회사 G가 인증 기관을 하고 싶다고 해도 신용도가 없다.

</br>

[![IMG-2500.jpg](https://i.postimg.cc/RhCn6wYH/IMG-2500.jpg)](https://postimg.cc/nj5LN9pF)

</br>

[![IMG-2501.jpg](https://i.postimg.cc/6Qd7MHJZ/IMG-2501.jpg)](https://postimg.cc/KK8vzDYc)

</br>

그래서 G는 Y사에게서 전자 인증서를 발급받는다. 물론 Y사는 G사가 인증 기관 업무를 적절히 수행하고 있는지를 감독한다.

인증서가 발행되면 B사는 A사의 신뢰를 받고 있는 회사라고 어필할 수 있다.

</br>

<a href="https://ibb.co/HzGNQRM"><img src="https://i.ibb.co/qsm0wh4/IMG-2502.jpg" alt="IMG-2502" border="0"></a>

</br>

이처럼 더 큰 조직이 작은 조직의 신뢰를 담보하는 형태로 트리 구조가 형성된다. 인증 기관의 최상위 기관은 어떻게 형성돼 있을까?

</br>

<a href="https://ibb.co/zsj9vxX"><img src="https://i.ibb.co/dB1CYMP/IMG-2503.jpg" alt="IMG-2503" border="0"></a>

</br>

최상위에 있는 인증 기관은 '최상위 인증 기관(Root CA)'라고 하며 자신의 정당성을 스스로 증명하게 된다. 참고로 최상위 인증 기관이 스스로 인증하는 인증서는 '최상위 인증서'라고 한다. 최상위 인증서는 기관 자체가 신뢰받지 못하면 이용할 수가 없다. 따라서 대기업이나 정부 관련 기관 등 이미 사회적으로 신뢰를 얻고 있는 기관이 많다.

</br>

<a href="https://ibb.co/FqgX0vH"><img src="https://i.ibb.co/prJQRDh/IMG-2504.jpg" alt="IMG-2504" border="0"></a>

</br>

지금까지 개인 간의 공개키 교환 흐름을 다뤘지만

</br>

<a href="https://ibb.co/wJX2ksZ"><img src="https://i.ibb.co/N1PGvSg/IMG-2505.jpg" alt="IMG-2505" border="0"></a>

</br>

웹사이트와 통신할 때도 전자 인증서가 사용된다. 웹사이트로부터 공개키가 붙은 인증서를 받으면 해당 사이트가 제 3자에 의해 위장되지 않은 것을 확인할 수 있다.

</br>

<a href="https://ibb.co/CPsqKqJ"><img src="https://i.ibb.co/MB5bkb8/IMG-2506.jpg" alt="IMG-2506" border="0"></a>

</br>

이 인증서는 '서버 인증서'라고 하는 것으로 인증 기관에 의해 발행된다.

</br>

<a href="https://ibb.co/48BcZ9N"><img src="https://i.ibb.co/1rH3fh2/IMG-2507.jpg" alt="IMG-2507" border="0"></a>

</br>

개인의 경우 인증서는 메일 주소와 연결되지만 서버 인증서는 도메인과 연결된다.

</br>

<a href="https://ibb.co/XxgH15k"><img src="https://i.ibb.co/60xQztJ/IMG-2508.jpg" alt="IMG-2508" border="0"></a>

</br>

서버 인증서는, 공개키가 인증서의 도메인을 관리하는 조직이 발핸한 것임을 보증한다. 즉, 웹사이트의 도메인을 관리하고 있는 조직과 웹사이트의 내용이 담긴 서버를 관리하고 있는 조직이 동일하다는 것을 확인할 수 있다. 이와 같이 전자 인증서는 인증 기관의 통해서 공개키 작성자를 보증하는 사회적 구조이다.