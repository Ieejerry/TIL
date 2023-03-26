# 암호의 기본(Basics of password)

</br>

[![IMG-2227.jpg](https://i.postimg.cc/7ZSzXHSf/IMG-2227.jpg)](https://postimg.cc/FYs1HQW4)

</br>

현재 인터넷 사회에서 암호 기술은 필수 기술이 되고 있다.

</br>

[![IMG-2228.jpg](https://i.postimg.cc/bYM2hDTZ/IMG-2228.jpg)](https://postimg.cc/hhLG8GNn)

</br>

A가 B에게 인터넷을 경유해서 데이터를 전달하려고 한다. 데이터는 인터넷상의 다양한 네트워크나 장비를 통해서 B에게 전달된다.

</br>

[![IMG-2229.jpg](https://i.postimg.cc/mkxz7KhQ/IMG-2229.jpg)](https://postimg.cc/2bwSDcQ6)

</br>

따라서 데이터를 그냥 전달하려고 하면

</br>

[![IMG-2230.jpg](https://i.postimg.cc/jS8DMDLq/IMG-2230.jpg)](https://postimg.cc/XrCNJ7ft)

</br>

악의를 지닌 제 3자가 데이터를 훔쳐볼 가능성이 있다.

</br>

[![IMG-2231.jpg](https://i.postimg.cc/1tD51X5q/IMG-2231.jpg)](https://postimg.cc/HcsCQpMY)

</br>

이 때문에 비밀로 하고 싶은 데이터는 암호화해서 전송할 필요가 있다.

</br>

[![IMG-2232.jpg](https://i.postimg.cc/x8swwVHm/IMG-2232.jpg)](https://postimg.cc/QKTY7PfN)

</br>

암호화한 데이터를 '암호문'이라고 한다.

</br>

[![IMG-2233.jpg](https://i.postimg.cc/1zPvrYV1/IMG-2233.jpg)](https://postimg.cc/NKJ8gDxd)

</br>

암호문을 B에게 전송한다.

</br>

[![IMG-2234.jpg](https://i.postimg.cc/vHfj7n29/IMG-2234.jpg)](https://postimg.cc/yk6vsDHY)

</br>

B는 A에게서 받은 암호문의 암호를 해제하고 원 데이터를 얻는다. 암호문을 원 데이터로 복원하는 것을 '복호'라고 한다.

</br>

[![IMG-2235.jpg](https://i.postimg.cc/1tD67ykW/IMG-2235.jpg)](https://postimg.cc/DJy883ys)

</br>

데이터를 암호화해두면 설령 악의를 지니 제 3자가 훔쳐본다고 해도 안심할 수 있다. 지금까지 본 것처럼 현대 인터넷 사회에선 암호화 기술이 매우 중요하다.

</br>

[![IMG-2236.jpg](https://i.postimg.cc/CxWz3WH9/IMG-2236.jpg)](https://postimg.cc/zyFzW2Qk)

</br>

암호화란 구체적으로 어떤 처리를 의미하는지 알아보겠다.

컴퓨터는 모든 데이터를 0과 1로 구성되는 2진수로 괸리한다.

</br>

[![IMG-2237.jpg](https://i.postimg.cc/bvVD6sVH/IMG-2237.jpg)](https://postimg.cc/rdWwsFkK)

</br>

데이터에는 텍스트, 음악, 사진 등 다양한 형식이 있지만

</br>

[![IMG-2238.jpg](https://i.postimg.cc/SxynkWwf/IMG-2238.jpg)](https://postimg.cc/zVczkRDy)

</br>

컴퓨터 내에선 모든 데이터가 2진수로 관리되고 있다.

</br>

[![IMG-2239.jpg](https://i.postimg.cc/SRFK5868/IMG-2239.jpg)](https://postimg.cc/9RbVwDNF)

</br>

이 내용을 바탕으로 데이터 암호화에 대해 생각해보도록 하겠다.

</br>

[![IMG-2240.jpg](https://i.postimg.cc/nLNVj7w5/IMG-2240.jpg)](https://postimg.cc/FfgXwfvg)

</br>

데이터는 컴퓨터에게 있어 의미를 지닌 숫자들의 나열이다.

</br>

[![IMG-2241.jpg](https://i.postimg.cc/50c1NJXW/IMG-2241.jpg)](https://postimg.cc/SXGHDwLg)

</br>

암호문도 숫자의 나열로 관리되고 있지만 컴퓨터가 해석할 수 없는 임의의 숫자로 구성돼있다.

암호화란 데이터에 어떤 연산을 적용해서 컴퓨터가 해석할 수 없는 숫자를 변경하는 것을 의미한다.

</br>

[![IMG-2242.jpg](https://i.postimg.cc/4dCHcn88/IMG-2242.jpg)](https://postimg.cc/JyqhV7CJ)

</br>

암호화이 수치 계산에선 '키'를 이용한다.

</br>

[![IMG-2243.jpg](https://i.postimg.cc/52YtmbQD/IMG-2243.jpg)](https://postimg.cc/0zvxkgfC)

</br>

키도 숫자로 만들어진다.

</br>

[![IMG-2244.jpg](https://i.postimg.cc/vmvwrNhp/IMG-2244.jpg)](https://postimg.cc/R3qY9GjR)

</br>

즉, 암호화 키를 이용한 수치 계산을 통해 데이터의 내용을 제 3자가 해석할 수 없도록 변환하는 것이다.

</br>

[![IMG-2245.jpg](https://i.postimg.cc/3RJNmpXF/IMG-2245.jpg)](https://postimg.cc/DWH7KSYS)

</br>

반대로 복호화란 키를 이용한 수치 계산을 통해 암호문을 원 데이터로 복원하는 것이다.

</br>

[![IMG-2246.jpg](https://i.postimg.cc/GhYDcFq4/IMG-2246.jpg)](https://postimg.cc/jLx2c7VT)

</br>

예로 데이터와 키를 그림에 있는 값으로 하고, 계산 방법을 XOR로 했을 때의 구체적인 과정을 보겠다.

</br>

[![IMG-2247.jpg](https://i.postimg.cc/sDpBFVgS/IMG-2247.jpg)](https://postimg.cc/6yp6nxR5)

</br>

XOR(비배타적 논리합)이란 그림의 진리값 표를 이용해 연산하는 것이다.

</br>

[![IMG-2248.jpg](https://i.postimg.cc/ZYNn3T3g/IMG-2248.jpg)](https://postimg.cc/c6sdGGFM)

</br>

XOR에선 그림의 식이 성립하는 것이 특징이다. 즉, 어떤 값 A와 어떤 값 B를 XOR로 계산한 결과가 C라고 하면 C에 대해 A나 B를 다시 XOR로 계산하면 다른 한 쪽의 값을 얻을 수 있다는 것을 의미한다.

</br>

[![IMG-2249.jpg](https://i.postimg.cc/4dkd2qRw/IMG-2249.jpg)](https://postimg.cc/wt2g7Wvs)

</br>

데이터에 대해 키를 이용해서 XOR을 계산하면

</br>

[![IMG-2250.jpg](https://i.postimg.cc/ZYjb6Cnw/IMG-2250.jpg)](https://postimg.cc/Sj2bhQW9)

</br>

이런 암호문을 얻을 수 있다.

</br>

[![IMG-2251.jpg](https://i.postimg.cc/VNj1vN2B/IMG-2251.jpg)](https://postimg.cc/rdF7YqVK)

</br>

이번에는 암호문을 복호화해보겠다. 암호문에 대해 다시 키를 이용해서 XOR 계산을 하면

</br>

[![IMG-2252.jpg](https://i.postimg.cc/T2kxpFNS/IMG-2252.jpg)](https://postimg.cc/23BMtcDF)

</br>

원 데이터를 얻을 수 있다. 이처럼 XOR이라는 계산 방법을 이용한 암호에선 암호화와 복호화에 동일한 키를 사용하게 된다.