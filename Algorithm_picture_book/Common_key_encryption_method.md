# 공통키 암호 방식(Common key encryption method)

</br>

[![IMG-2273.jpg](https://i.postimg.cc/0NHFtL63/IMG-2273.jpg)](https://postimg.cc/qty1qDxX)

</br>

공통키 암호 방식은 암호화와 복호화에 동일한 키를 사용하는 암호 방식이다.

</br>

[![IMG-2274.jpg](https://i.postimg.cc/WbXn60qY/IMG-2274.jpg)](https://postimg.cc/nC9Bnjkq)

</br>

공통키 암호 방식을 사용한 데이터 전송의 전체 흐름을 보도록 하겠다.

</br>

[![IMG-2275.jpg](https://i.postimg.cc/fyb3wSWk/IMG-2275.jpg)](https://postimg.cc/tZLRkTxH)

</br>

A가 B에게 인터넷을 경유해서 데이터를 전송하려고 하고 있다. 데이터는 인터넷상의 다양한 네트워크나 장비를 통해서 B에게 전달된다.

</br>

[![IMG-2276.jpg](https://i.postimg.cc/8CDzpftD/IMG-2276.jpg)](https://postimg.cc/fV2N5LGg)

</br>

따라서 데이터를 그냥 전달하려고 하면

</br>

[![IMG-2277.jpg](https://i.postimg.cc/HxYn28y3/IMG-2277.jpg)](https://postimg.cc/PL7dfxK8)

</br>

악의를 지닌 제 3자가 데이터를 훔쳐볼 가능성이 있다.

</br>

[![IMG-2278.jpg](https://i.postimg.cc/GmPb5hrf/IMG-2278.jpg)](https://postimg.cc/Jsnwy8s3)

</br>

이 때문에 비밀로 하고 싶은 데이터는 암호화해서 전송할 필요가 있다.

</br>

[![IMG-2280.jpg](https://i.postimg.cc/ZK4myz6F/IMG-2280.jpg)](https://postimg.cc/jCgmG9gL)

</br>

키를 사용해서 데이터를 암호화한 암호문을 만든다.

</br>

[![IMG-2281.jpg](https://i.postimg.cc/KvJ6kkGx/IMG-2281.jpg)](https://postimg.cc/qz6bW765)

</br>

암호문을 B에게 전송한다.

</br>

[![IMG-2282.jpg](https://i.postimg.cc/PJFMhjHs/IMG-2282.jpg)](https://postimg.cc/9wZ9tszJ)

</br>

B는 A에게서 받은 암호문을 동일한 키를 사용해서 복호화한다.

</br>

[![IMG-2283.jpg](https://i.postimg.cc/L8jjQfJM/IMG-2283.jpg)](https://postimg.cc/HrsJVr0S)

</br>

이것으로 B는 원 데이터를 얻을 수 있다.

</br>

[![IMG-2284.jpg](https://i.postimg.cc/QCpWYZMJ/IMG-2284.jpg)](https://postimg.cc/7JZ6bc05)

</br>

데이터를 암호화해두면 설령 악의를 지닌 제 3자가 훔쳐본다고 해도 안심할 수 있다. 암호화와 복호화에 동일한 키를 사용하는 것이 공통키 암호 방식의 특징이다.

</br>

[![IMG-2285.jpg](https://i.postimg.cc/0Q9gKpw5/IMG-2285.jpg)](https://postimg.cc/v122pxhC)

</br>

공통키 암호 방식의 계산 방법에는 위의 그림과 같은 것들이 있다. 현재는 AES가 주로 사용되고 있다. 다음은 공통키 암호 방식의 문제점에 대해 알아보겠다.

</br>

[![IMG-2286.jpg](https://i.postimg.cc/htG1vhvF/IMG-2286.jpg)](https://postimg.cc/ppgF1WKk)

</br>

상황을 약간 앞으로 돌리도록 하겠다.

</br>

[![IMG-2287.jpg](https://i.postimg.cc/8PphXshF/IMG-2287.jpg)](https://postimg.cc/RqY6NSp9)

</br>

암호문은 X가 훔쳐볼 가능성이 있다.

</br>

[![IMG-2288.jpg](https://i.postimg.cc/NGpyMDHM/IMG-2288.jpg)](https://postimg.cc/vDx82WXF)

</br>

A와 B는 직접 대면한 적이 없는 관계이며 암호화에 사용된 키를 B가 모른다고 가정하겠다.

</br>

[![IMG-2289.jpg](https://i.postimg.cc/4xbRfLY2/IMG-2289.jpg)](https://postimg.cc/RWFDGTQw)

</br>

A는 특정 수단을 사용해서 B에게 키를 전달해야 한다.

</br>

[![IMG-2291.jpg](https://i.postimg.cc/SQMS0Gf3/IMG-2291.jpg)](https://postimg.cc/PNdsYYcQ)

</br>

A는 암호문과 동일하게 인터넷을 통해서 B에게 키를 전송한다.

</br>

[![IMG-2292.jpg](https://i.postimg.cc/P5F9rgt4/IMG-2292.jpg)](https://postimg.cc/nXB03w9j)

</br>

B는 A가 보낸 키를 사용해서

</br>

[![IMG-2293.jpg](https://i.postimg.cc/Vvp0NsVw/IMG-2293.jpg)](https://postimg.cc/y3h8QKKp)

</br>

암호문을 복호화한다.

</br>

[![IMG-2294.jpg](https://i.postimg.cc/MH7vmkZ2/IMG-2294.jpg)](https://postimg.cc/K3YGmHgJ)

</br>

하지만 이 키도 X가 훔쳐볼 가능성이 있다.

</br>

[![IMG-2295.jpg](https://i.postimg.cc/X7qR5fsx/IMG-2295.jpg)](https://postimg.cc/2Vp9RZRB)

</br>

즉, X도 키를 사용해서 암호문을 복호화할 수 있다는 의미이다. 키를 전달하는 방법에 문제가 있다는 것을 알 수 있다.

</br>

[![IMG-2296.jpg](https://i.postimg.cc/GhNmThx8/IMG-2296.jpg)](https://postimg.cc/crRSVWj0)

</br>

그래서 A는 X가 훔쳐보지 못하도록 키 전체를 암호화하는 방법을 생각했다.

</br>

[![IMG-2297.jpg](https://i.postimg.cc/Qd8ZM2R9/IMG-2297.jpg)](https://postimg.cc/nCPPRPVp)

</br>

컴퓨터에게는 키도 데이터의 일종에 불과하다.

</br>

[![IMG-2298.jpg](https://i.postimg.cc/WbQJL7KH/IMG-2298.jpg)](https://postimg.cc/Whw400sG)

</br>

따라서

</br>

[![IMG-2299.jpg](https://i.postimg.cc/1X84bgKS/IMG-2299.jpg)](https://postimg.cc/0Kq8wy3X)

</br>

새로운 키를 사용해서 암호화할 수 있다.

</br>

[![IMG-2300.jpg](https://i.postimg.cc/zXmR4j4P/IMG-2300.jpg)](https://postimg.cc/vDzBVWYW)

</br>

키의 암호문을

</br>

[![IMG-2301.jpg](https://i.postimg.cc/sgj1R0mK/IMG-2301.jpg)](https://postimg.cc/YhPt6RJm)

</br>

B에게 전달한다. B는 데이터의 암호문과 그것을 복호화하기 위한 키의 암호문을 가지고 있다.

</br>

[![IMG-2302.jpg](https://i.postimg.cc/XJdn5wxp/IMG-2302.jpg)](https://postimg.cc/R6Cr5JkB)

</br>

키의 암호문도 다시 X에게 노출될 가능성이 있다.

</br>

[![IMG-2303.jpg](https://i.postimg.cc/T3KMmV3f/IMG-2303.jpg)](https://postimg.cc/CRpQpf8Q)

</br>

다음은 '키의 암호화에 사용한 새로운 키'를 B에게 전달만 하면 된다.

A는 이 '새로운 키'를 어떻게 B에게 전달하면 좋을 지 보겠다.

암호화하지 않으면 X가 '새로운 키'를 훔쳐서 사용할 수 있다. 암호화하면 다시 새로운 키가 생겨서 문제가 반복된다. 정라하면, '공통키 암호 방식'에서 키를 안전하게 전달할 방법이 필요한 것이다. 이것을 '키 배분 문제'라고 한다. 해결 방법으로는 '키 교환 프로토콜을 사용하는 방법'과 '공개키 암호 방식을 사용하는 방법' 두 가지가 있다.