# 보안의 기본(The basics of security)

</br>

[![IMG-2204.jpg](https://i.postimg.cc/tTN1DWp6/IMG-2204.jpg)](https://postimg.cc/dkDtV77Q)

</br>

인터넷을 경유해서 데이터를 전달할 때 데이터는 다양한 네트워크나 장비를 경유해서 목적지에 도달하게 된다. 따라서 인터넷을 안전하게 사용하기 위해서는 보안 기술이 필수 불가결이 되고 있다.

먼저 인터넷에서 데이터를 주고 받을 때에 발생할 수 있는 대표적인 문제 네 가지를 소개하도록 하겠다.

</br>

[![IMG-2205.jpg](https://i.postimg.cc/4yKgnRL3/IMG-2205.jpg)](https://postimg.cc/fShFgph4)

</br>

A가 B에게 메세지를 전송할 때에

</br>

[![IMG-2206.jpg](https://i.postimg.cc/jSTS3C3Q/IMG-2206.jpg)](https://postimg.cc/Xp2WpNbp)

</br>

경로 상에 있는 X가 메세지 내용을 훔쳐볼 가능성이 있다. 이 문제를 '도청(interception)'이라고 한다.

</br>

[![IMG-2207.jpg](https://i.postimg.cc/YC2wmFyV/IMG-2207.jpg)](https://postimg.cc/WhyyBdV6)

</br>

A가 B에게 메세지를 전달했다고 생각하지만

</br>

[![IMG-2208.jpg](https://i.postimg.cc/yxTbVQBN/IMG-2208.jpg)](https://postimg.cc/bSsTgRZX)

</br>

X가 B로 위장했을 가능성이 있다.

</br>

[![IMG-2209.jpg](https://i.postimg.cc/Kvwn17zc/IMG-2209.jpg)](https://postimg.cc/JG3ygkZS)

</br>

반대로 B가 A에게 메세지를 받았다고 생각하지만

</br>

[![IMG-2210.jpg](https://i.postimg.cc/htRXF2vm/IMG-2210.jpg)](https://postimg.cc/56p4Lqw9)

</br>

X가 A로 위장했을 가능성도 있다. 이 문제를 '위장'이라고 한다.

</br>

[![IMG-2211.jpg](https://i.postimg.cc/QMx5PfYb/IMG-2211.jpg)](https://postimg.cc/JsvGH5LD)

</br>

A가 B에게 메세지 전송을 확실하게 완료했다고 해도

</br>

[![IMG-2212.jpg](https://i.postimg.cc/pV890NXv/IMG-2212.jpg)](https://postimg.cc/hhDPj5dZ)

</br>

도중에 X가 메세지 내용을 변경했을 가능성이 있다. 이 문제를 '변조(falsification)'이라고 한다.

3자가 의도적으로 변조한 것 외에도 통신상의 장애로 인해 데이터가 망가진 상태로 전달될 수도 있다.

</br>

[![IMG-2213.jpg](https://i.postimg.cc/Nf9dCj2M/IMG-2213.jpg)](https://postimg.cc/bsP0s8Tc)

</br>

B가 A에게서 메세지를 받았다고 생각하지만

</br>

[![IMG-2214.jpg](https://i.postimg.cc/WtLgHjxF/IMG-2214.jpg)](https://postimg.cc/64c87sWt)

</br>

메세지의 전송자인 A가 악의를 지닌 경우

</br>

[![IMG-2215.jpg](https://i.postimg.cc/hvSfzvF0/IMG-2215.jpg)](https://postimg.cc/YGspTpC4)

</br>

나중에 A가 '그건 내가 보낸 게 아니야'하고 부인할 가능성이 있다. 이런 경우에는 인터넷상에서의 상거래나 계약 행위 등이 성립하지 않게 된다. 이 문제를 '사후 부인'이라고 한다.

</br>

[![IMG-2216.jpg](https://i.postimg.cc/pTLwmMGF/IMG-2216.jpg)](https://postimg.cc/06hW4Fqk)

</br>

대표적인 네 가지 문제를 소개했다.

</br>

[![IMG-2217.jpg](https://i.postimg.cc/JtVYcfqK/IMG-2217.jpg)](https://postimg.cc/PvyMdF08)

</br>

이 문제들은 사람 사이에서만 발생하는 것이 아니라 웹사이트를 열람하는 경우에도 동일하게 발생할 수 있다.

</br>

[![IMG-2218.jpg](https://i.postimg.cc/pVDSPTX6/IMG-2218.jpg)](https://postimg.cc/Hjkz2TMw)

</br>

위와 같은 문제를 해결하기 위해선 어떤 보안 기술들이 존재하는지 각 문제들에 대처할 수 있는 기술을 보도록 하겠다.

</br>

[![IMG-2219.jpg](https://i.postimg.cc/L683G6qf/IMG-2219.jpg)](https://postimg.cc/ThBbDxJY)

</br>

첫 번째 문제인 '도청'을 방지하기 위해서는 '암호화'기술을 사용한다.

</br>

[![IMG-2220.jpg](https://i.postimg.cc/hGLmfHzc/IMG-2220.jpg)](https://postimg.cc/CZK52rsQ)

</br>

두 번째 문제인 '위장'을 방지하기 위해서는 '메세지 인증 코드'나

</br>

[![IMG-2221.jpg](https://i.postimg.cc/fWrVTw2Y/IMG-2221.jpg)](https://postimg.cc/bd1ymjjv)

</br>

'전자 서명'기술을 사용한다.

</br>

[![IMG-2222.jpg](https://i.postimg.cc/qMKvJ2Cd/IMG-2222.jpg)](https://postimg.cc/zVJrpbjd)

</br>

세 번째 문제인 '변조'를 방지하는 경우에도 '메세지 인증 코드'나

</br>

[![IMG-2223.jpg](https://i.postimg.cc/3NmNcGX7/IMG-2223.jpg)](https://postimg.cc/H8WTJVvP)

</br>

'전자 서명'기술을 사용한다. 이 '전자 서명'기술은 네 번째 문제인 '사후 부인'에도 도움이 된다.

</br>

[![IMG-2224.jpg](https://i.postimg.cc/43jJRdN3/IMG-2224.jpg)](https://postimg.cc/t1t0h960)

</br>

정리하면 다음 표와 같다.

</br>

[![IMG-2225.jpg](https://i.postimg.cc/GtxrDxPB/IMG-2225.jpg)](https://postimg.cc/SYRwF8vq)

</br>

참고로 '전자 서명'기술에서 문제가 되는 '공개키의 소유자를 식별할 수 없는 문제'를 해결하기 위해 '전자 서명서'라는 기술도 사용한다.