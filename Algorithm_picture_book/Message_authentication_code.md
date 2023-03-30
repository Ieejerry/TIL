# 메세지 인증 코드(Message authentication code)

</br>

[![IMG-2391.jpg](https://i.postimg.cc/tJM4L3d5/IMG-2391.jpg)](https://postimg.cc/dZGFCTxk)

</br>

메세지 인증 코드는 '인증'과 '변조 검출'의 두 가지 기능을 가지는 구조이다. 먼저 메세지 인증 코드가 필요한 상황을 생각해보겠다. A가 B에게서 상품을 사기 위해 상품 번호를 나타내는 'abc'라는 메세지를 보낸다. 여기서 A는 메세지를 암호화한다.

</br>

[![IMG-2392.jpg](https://i.postimg.cc/9XKVHQ5J/IMG-2392.jpg)](https://postimg.cc/DmrRqFzX)

</br>

암호화에는 '공통키 암호 방식'을 사용하기로 한다.

</br>

[![IMG-2393.jpg](https://i.postimg.cc/kgFdSNVp/IMG-2393.jpg)](https://postimg.cc/qNRYV3xs)

</br>

A는 안전한 방법으로 키를 B에게 보낸다. 키 교환 방법은 '공개키 암호 방식' 또는 '디피-헬만 키 교환법' 같은 키 교환 프로토콜을 사용한다.

</br>

[![IMG-2394.jpg](https://i.postimg.cc/fRg1mHz5/IMG-2394.jpg)](https://postimg.cc/bZk6j922)

</br>

[![IMG-2395.jpg](https://i.postimg.cc/BQ7mVXrn/IMG-2395.jpg)](https://postimg.cc/dLdR7tQb)

</br>

A는 공유한 키를 사용해서 메세지를 암호문으로 만든다.

</br>

[![IMG-2397.jpg](https://i.postimg.cc/BZMpjjQB/IMG-2397.jpg)](https://postimg.cc/jCnP9dfD)

</br>

암호문을 B에게 보내고

</br>

[![IMG-2398.jpg](https://i.postimg.cc/wB8cCJ0g/IMG-2398.jpg)](https://postimg.cc/ZWHd3WGM)

</br>

B는 이것을 복호화해서 메세지인 상품 번호 'abc'를 확인할 수 있다. 지금까지는 문제가 없는 경우지만 다음과 같은 상황이 발생할 수도 있다.

</br>

[![IMG-2399.jpg](https://i.postimg.cc/9Mx9Qqt4/IMG-2399.jpg)](https://postimg.cc/34vNLNq7)

</br>

상황을, A가 B에게 암호문을 보내는 부분으로 되돌리겠다. A가 B에게 전송하려고 한 암호문을

</br>

[![IMG-2400.jpg](https://i.postimg.cc/zG1y5jZt/IMG-2400.jpg)](https://postimg.cc/SJDSfcKC)

</br>

악의를 지닌 X가 통신 도중에 변조한 상황을 생각해보겠다. B는 암호문을 받지만 변조된 것을 눈치재지 못한다.

</br>

[![IMG-2401.jpg](https://i.postimg.cc/s2H74N16/IMG-2401.jpg)](https://postimg.cc/yJ9DVnmc)

</br>

변조된 암호문을 B가 복호화하면 메세지가 'xyz'로 변경돼 있다. B는 'xyz'가 주문한 상품 번호라고 믿고 A에게 잘못된 상품을 발송한다. 암호는 어디까지나 수치 계산 처리에 불과하기 때문에, 변조된 암호문이라도 복호화 계산을 할 수가 있다. 원 메세지가 긴 문장이라면 변조에 의해 의미가 이상해지기 때문에 변조됐다는 사실을 알 수 있다. 하지만 원 메세지가 상품 번호처럼 사람이 직접 이해할 수 없는 데이터라면 복호화해도 변조된 사실을 인지하기가 어렵다. 변조를 감지하려면 암호화는 다른 또 다른 수단이 필요하다. 메세지 인증 코드를 사용하면 메세지 변조를 감지할 수 있다. 실제 흐름을 보기 위해

</br>

[![IMG-2402.jpg](https://i.postimg.cc/0QxRZc3S/IMG-2402.jpg)](https://postimg.cc/Z9fM5FJY)

</br>

상황을 A가 B에게 암호문을 전달하는 부분으로 되돌려 보겠다.

</br>

[![IMG-2403.jpg](https://i.postimg.cc/MTzN1XMb/IMG-2403.jpg)](https://postimg.cc/2qX0DkxV)

</br>

A는 메세지 인증 코드 작성을 위한 키를 만들고

</br>

[![IMG-2404.jpg](https://i.postimg.cc/mk5nxwd8/IMG-2404.jpg)](https://postimg.cc/fSYCmxQ9)

</br>

안전한 방법으로 B에게 키를 전달한다.

</br>

[![IMG-2405.jpg](https://i.postimg.cc/qRmbnwd4/IMG-2405.jpg)](https://postimg.cc/ygZyCFdb)

</br>

A는 암호문과 키를 사용해서 특정 값을 만든다.

</br>

[![IMG-2406.jpg](https://i.postimg.cc/85n4sChC/IMG-2406.jpg)](https://postimg.cc/sQ77NsHF)

</br>

여기선 '7f05'라는 값이 만들어진다. 이 카와 암호문을 조합해서 만든 값을 '메세지 인증 코드'라고 한다.

</br>

[![IMG-2407.jpg](https://i.postimg.cc/BvnwvkdM/IMG-2407.jpg)](https://postimg.cc/G46j773y)

</br>

메세지 인증 코드는 영어로 'MAC(Message Authentication Code)'라고 부르기 때문에, 지금부터는 'MAC'이라고 표기하겠다. 맥은, 키와 암호문을 조합한 문자열의 '해시값'이라고 보면 된다. MAC 작성 방법은 HMAC, OMAC, CMAC 등이 있다. 현재는 HMAC이 주로 사용되고 있다.

</br>

[![IMG-2408.jpg](https://i.postimg.cc/W4Zq01L3/IMG-2408.jpg)](https://postimg.cc/cKsJSZJy)

</br>

A는 B에게 작성한 MAC과 암호문을 보낸다.

</br>

[![IMG-2409.jpg](https://i.postimg.cc/W1FdP14n/IMG-2409.jpg)](https://postimg.cc/HrmYwHXc)

</br>

B가 암호문과 MAC을 받았다. B는 받은 암호문이 변조됐는지를 확인할 필요가 있다.

</br>

[![IMG-2410.jpg](https://i.postimg.cc/bNMvLfR2/IMG-2410.jpg)](https://postimg.cc/ykmBY5tV)

</br>

A와 마찬가지로 B도 암호문과 키를 사용해서 MAC을 작성한다.

</br>

[![IMG-2411.jpg](https://i.postimg.cc/zGKqjbB9/IMG-2411.jpg)](https://postimg.cc/pmVNVdKZ)

</br>

B가 직접 계산한 MAC과 A에게서 받은 MAC이 일치하는 것을 확인했다. 이를 통해 B가 받은 암호문은 변조되지 않은 것임을 알 수 있다.

</br>

[![IMG-2413.jpg](https://i.postimg.cc/y8jstqmP/IMG-2413.jpg)](https://postimg.cc/G44WT5S8)

</br>

이후로는 암호문용 키를 사용해서 복호화하기만 하면 된다.

</br>

[![IMG-2414.jpg](https://i.postimg.cc/XYj0w2Ry/IMG-2414.jpg)](https://postimg.cc/vcNjyvHQ)

</br>

무사히 A가 주문한 상품 번호인 'abc'라는 메세지를 추출할 수 있다.

</br>

[![IMG-2415.jpg](https://i.postimg.cc/pTNGBrm1/IMG-2415.jpg)](https://postimg.cc/1gHrm9cp)

</br>

상황을, A가 암호문을 B에게 전송하려는 시점으로 돌려보겠다. 만약 악의를 지닌 X가 통신 중에 암호문을 변조하면 어떻게 될까? A가 B에게 전달하려고 한 암호문과 MAC 중에서

</br>

[![IMG-2416.jpg](https://i.postimg.cc/KzNPg8BT/IMG-2416.jpg)](https://postimg.cc/xJXJwYsj)

</br>

암호문을 X가 변조한다.

</br>

[![IMG-2417.jpg](https://i.postimg.cc/C55qBHFy/IMG-2417.jpg)](https://postimg.cc/p5NT3jhk)

</br>

B는 암호문으로부터 MAC을 계산해서

</br>

[![IMG-2418.jpg](https://i.postimg.cc/6q885W0t/IMG-2418.jpg)](https://postimg.cc/jnrxMrmF)

</br>

A가 받은 MAC과 일치하지 않는다는 것을 알았다. 이를 통해 B는 암호문이나 맥, 또는 양쪽 모두가 변조됐을 가능성이 있다고 생각한다. A에게서 받은 암호문과 MAC을 파기하고 A에게 다시 전송을 요청하면 된다.

</br>

[![IMG-2419.jpg](https://i.postimg.cc/GtDsx3sz/IMG-2419.jpg)](https://postimg.cc/kRn4nmst)

</br>

X가 암호문의 변조 내용에 맞추어 MAC도 변조한다면 어떻게 될까? X는 MAC을 계산하기 위한 키를 가지고 있지 않으므로

</br>

[![IMG-2420.jpg](https://i.postimg.cc/VsFwdQTc/IMG-2420.jpg)](https://postimg.cc/QVVwyPh6)

</br>

MAC을 변조했다고 해도 암호문의 변조에 맞추는 것은 불가능하다.

</br>

[![IMG-2421.jpg](https://i.postimg.cc/Kvg50xy6/IMG-2421.jpg)](https://postimg.cc/mtBMDxkj)

</br>

[![IMG-2422.jpg](https://i.postimg.cc/J7XqqR89/IMG-2422.jpg)](https://postimg.cc/XXVdNSp8)

</br>

B가 MAC을 다시 계산하면 변조된 암호문에 대한 MAC과 일치하지 않아서 통신 주엥 어딘가에서 변조가 발생했다는 것을 알 수 있다. 이와 같이 메세지 인증 코드라 불리는 MAC을 이용하면 통신상의 변조를 방지할 수 있다. 단, 여기에도 결점이 있다.

</br>

[![IMG-2423.jpg](https://i.postimg.cc/Fz1XM1xg/IMG-2423.jpg)](https://postimg.cc/SY0P8S3J)

</br>

일련의 처리를 단순화해보겠다. 먼저 A와 B는 암호화에 사용하는 키와 MAC을 계산하기 위한 키를 공유하고 있다. 따라서

</br>

[![IMG-2424.jpg](https://i.postimg.cc/268sW3gR/IMG-2424.jpg)](https://postimg.cc/94Kg5XWJ)

</br>

A가 메세지를 암호화해서 MAC을 계산할 수 있도록

</br>

[![IMG-2425.jpg](https://i.postimg.cc/Z0kswqsq/IMG-2425.jpg)](https://postimg.cc/30BZR3TM)

</br>

B도 마찬가지로 메세지를 암호화해서 MAC을 계산할 수 있다. 즉, 원 메세지를 작성한 것이 A인지 B인지를 증명할 수 없게 된다.

</br>

[![IMG-2426.jpg](https://i.postimg.cc/bNH4mx8c/IMG-2426.jpg)](https://postimg.cc/6yqH3GyY)

</br>

따라서 A가 악의를 지닌 경우

</br>

[![IMG-2427.jpg](https://i.postimg.cc/kgY1HwpZ/IMG-2427.jpg)](https://postimg.cc/9DTYRPVt)

</br>

메세지를 보낸 후에 '그건 B가 조작한 메세지야'라고 자신이 보낸 것을 사후 부인할 수 있게 된다.