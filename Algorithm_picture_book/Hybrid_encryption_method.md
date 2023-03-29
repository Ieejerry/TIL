# 하이브리드 암호 방식(Hybrid encryption method)

</br>

[![IMG-2340.jpg](https://i.postimg.cc/VNNHQgMt/IMG-2340.jpg)](https://postimg.cc/DStc1qxf)

</br>

공통키 암호 방식에는 키를 어떻게 안전하게 교환해야 하는지 '키 분배 문제'가 있었다.

</br>

[![IMG-2341.jpg](https://i.postimg.cc/CKdJ61TH/IMG-2341.jpg)](https://postimg.cc/VSQjJzNd)

</br>

한편 공개키 암호 방식에는 암호화와 복호화의 처리 속도가 느리다는 문제가 있었다.

</br>

[![IMG-2343.jpg](https://i.postimg.cc/KvFfhQhY/IMG-2343.jpg)](https://postimg.cc/Z07pr8Rk)

</br>

하이브리드 방식은 이 두 가지의 방식을 결합해서 약점을 보완한 방식이다. 데이터 암호화에는 처리 속도가 빠른 공통키 암호 방식을 사용한다. 반면, 공통키 암호 방식에서 사용하는 키는 키 분배가 불필요한 공개키 암호 방식을 이용한다. 하이브릐드 암호 방식의 구체적인 흐름을 보도록 하겠다.

</br>

[![IMG-2344.jpg](https://i.postimg.cc/288Wxtfn/IMG-2344.jpg)](https://postimg.cc/mhJhL8kr)

</br>

A가 B에게 인터넷을 통해서 데이터를 전달하려고 하는 상황이다. 데이터는 처리 속도가 빠른 공통키 암호 방식으로 암호화한다.

</br>

[![IMG-2345.jpg](https://i.postimg.cc/kgRB13YR/IMG-2345.jpg)](https://postimg.cc/87Dpc3ST)

</br>

암호화에 필요한 키는 복호화에도 사용하므로 A는 키를 B에게 전달해야 한다.

</br>

[![IMG-2346.jpg](https://i.postimg.cc/0QVk5cHq/IMG-2346.jpg)](https://postimg.cc/62GJYLXH)

</br>

키도 데이터의 일종이다. 키를 공개키 암호 방식으로 암호화하므로 안전하게 B에게 저달할 수 있다.

</br>

[![IMG-2347.jpg](https://i.postimg.cc/ZR5mQ6Ys/IMG-2347.jpg)](https://postimg.cc/Z92XBBd6)

</br>

B는 공개키와 비밀키를 생성한다.

</br>

[![IMG-2348.jpg](https://i.postimg.cc/XvQS9XKf/IMG-2348.jpg)](https://postimg.cc/XZGzbjzq)

</br>

공개키를 A에게 보낸다. A는 B에게서 받은 공개키를 사용해서

</br>

[![IMG-2349.jpg](https://i.postimg.cc/1z5RkkJK/IMG-2349.jpg)](https://postimg.cc/3kVHpcMy)

</br>

공통키 암호 방식에 사용하는 키를 암호화한다.

</br>

[![IMG-2350.jpg](https://i.postimg.cc/DwfK0qLv/IMG-2350.jpg)](https://postimg.cc/56rrkQsT)

</br>

암호화한 키를 B에게 전달한다. B는 비밀키를 사용해서 키의 암호문을 복호화한다.

</br>

[![IMG-2351.jpg](https://i.postimg.cc/xCvsLZVW/IMG-2351.jpg)](https://postimg.cc/34wCTnRB)

</br>

키의 암호문을 복호화한다.

</br>

[![IMG-2352.jpg](https://i.postimg.cc/qMMmCQb5/IMG-2352.jpg)](https://postimg.cc/rz3GBGL1)

</br>

이것으로 A는 공통키 암호 방식에 사용하는 키를 B에게 안전하게 전달할 수 있다.

</br>

[![IMG-2353.jpg](https://i.postimg.cc/SskLbNHv/IMG-2353.jpg)](https://postimg.cc/2q9L4mkQ)

</br>

이후로는 이 키를 사용해서 암호화한 데이터를 보내기만 하면 된다. 데이터 암호화에는 처리 속도가 빠른 공통키 암호 방식을 사용한다.

</br>

[![IMG-2355.jpg](https://i.postimg.cc/TPRhRLYg/IMG-2355.jpg)](https://postimg.cc/TK4T0Pb3)

</br>

B는 무사히 원 데이터를 취득할 수 있다.

</br>

[![IMG-2356.jpg](https://i.postimg.cc/BvQDmwFr/IMG-2356.jpg)](https://postimg.cc/qNSzRwjw)

</br>

이와 같이 하이브리드 암호 방식은 안전성과 속도를 모두 만족한다. 하이브리드 암호 방식은 인터넷상에서 정보를 안전하게 교환하기 위한 프로토콜인 'SSL'에서 사용되고 있다.