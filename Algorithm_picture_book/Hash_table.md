# 해시 테이블(Hash table)

</br>

<a href="https://ibb.co/t3WGmcs"><img src="https://i.ibb.co/d7zTW62/Kakao-Talk-20230304-171334845.jpg" alt="Kakao-Talk-20230304-171334845" border="0"></a>

</br>

해시 테이블은 데이터 구조의 하나이다.

</br>

<a href="https://ibb.co/f4HTfTn"><img src="https://i.ibb.co/m64PkPX/Kakao-Talk-20230304-171334845-01.jpg" alt="Kakao-Talk-20230304-171334845-01" border="0"></a>

</br>

해시 테이블은 키(key)오 값(value)이 한 쌍으로 구성된 데이터를 저장한다.

여기선 이름을 키로, 성별을 값으로 저장하고 있다.

</br>

<a href="https://ibb.co/CWsNy5Y"><img src="https://i.ibb.co/fQGBWYy/Kakao-Talk-20230304-171334845-02.jpg" alt="Kakao-Talk-20230304-171334845-02" border="0"></a>

</br>

예를 들어 그림의 데이터를 배열에 저장하는 경우를 생각해보겠다.

</br>

<a href="https://ibb.co/Bs4RLqw"><img src="https://i.ibb.co/PCT8xwt/Kakao-Talk-20230304-171334845-03.jpg" alt="Kakao-Talk-20230304-171334845-03" border="0"></a>

</br>

6개 상자로 이루어진 배열을 준비해서 데이터를 저장한다. 여기서 Ally의 성별을 알고싶다고 가정하겠다.

Ally가 배열의 몇 번째 상자에 저장돼 있는지 모른다. 따라서 앞에서부터 차례대로 확인해야 한다. 이 처리를 '선형 탐색'이라고 한다.

</br>

<a href="https://ibb.co/qjVFfYt"><img src="https://i.ibb.co/54wxyhN/Kakao-Talk-20230304-171334845-04.jpg" alt="Kakao-Talk-20230304-171334845-04" border="0"></a>

</br>

0번 상자에 저장된 데이터의 키는 'Joe'이며 'Ally'가 아니다.

</br>

<a href="https://ibb.co/K2kT1Dk"><img src="https://i.ibb.co/Byx01Gx/Kakao-Talk-20230304-171334845-05.jpg" alt="Kakao-Talk-20230304-171334845-05" border="0"></a>

</br>

1번 상자에 저장된 키도 'Ally'가 아니다.

</br>

<a href="https://ibb.co/Yf5xV2s"><img src="https://i.ibb.co/j3CSjhX/Kakao-Talk-20230304-171334845-06.jpg" alt="Kakao-Talk-20230304-171334845-06" border="0"></a>

</br>

2번 상자에 저장된 키도 'Ally'가 아니다.

</br>

<a href="https://ibb.co/tMPxQcY"><img src="https://i.ibb.co/SX7d50V/Kakao-Talk-20230304-171334845-07.jpg" alt="Kakao-Talk-20230304-171334845-07" border="0"></a>

</br>

3번 상자에 저장된 키도 'Ally'가 아니다.

</br>

<a href="https://ibb.co/Yj4JFpf"><img src="https://i.ibb.co/VB0bc2M/Kakao-Talk-20230304-171334845-08.jpg" alt="Kakao-Talk-20230304-171334845-08" border="0"></a>

</br>

4번 상자에 저장된 데이터의 키가 'Ally'와 일치한다. 대응되는 값을 꺼내면 Ally의 성별이 여성(F)이라는 것을 알 수 있다.

이와 같이 선형 탐색은 데이터량에 비례해서 계산 시간이 늘어난다. 배열 탐색에 시간이 걸리므로 탐색에는 적합하지 않은 구조라는 것을 알 수 있다. 이 문제를 해결해주는 것이 해시 테이블이다.

</br>

<a href="https://ibb.co/cQmVVbF"><img src="https://i.ibb.co/DQqTTGC/Kakao-Talk-20230304-171334845-09.jpg" alt="Kakao-Talk-20230304-171334845-09" border="0"></a>

</br>

먼저 데이터를 저장하기 위한 배열을 준비한다. 준비됐으면 데이터를 추가해보겠다.

</br>

<a href="https://ibb.co/pQTWBwM"><img src="https://i.ibb.co/3vbf9dj/Kakao-Talk-20230304-171334845-10.jpg" alt="Kakao-Talk-20230304-171334845-10" border="0"></a>

</br>

Joe의 데이터를 추가하는 경우이다.

</br>

<a href="https://ibb.co/m4mCXDC"><img src="https://i.ibb.co/CQq5M15/Kakao-Talk-20230304-171334845-11.jpg" alt="Kakao-Talk-20230304-171334845-11" border="0"></a>

</br>

해시 함수를 이용해서 키의 해시값을 계산한다. 해시 함수는 데이터를 고정된 길이의 수치로 변환하는 함수이다.

</br>

<a href="https://ibb.co/VQCbYTc"><img src="https://i.ibb.co/SdmHwB4/Kakao-Talk-20230304-171334845-12.jpg" alt="Kakao-Talk-20230304-171334845-12" border="0"></a>

</br>

구한 해시값을 배열의 상자 수인 5로 나누어 나머지를 구한다. 나머지를 구하는 연산을 'mod 연산'이라고 한다. mod 연산 결과 3이라는 숫자가 나온다.

</br>

<a href="https://ibb.co/642kz2t"><img src="https://i.ibb.co/Hr0j60P/Kakao-Talk-20230304-171334845-13.jpg" alt="Kakao-Talk-20230304-171334845-13" border="0"></a>

</br>

구한 수와 동일한 배열의 3번 상자에 Joe의 데이터를 저장한다. 이 처리를 반복해서 다른 데이터도 하나씩 채워간다.

</br>

<a href="https://ibb.co/L8nJPK9"><img src="https://i.ibb.co/CzhMtLV/Kakao-Talk-20230304-171334845-14.jpg" alt="Kakao-Talk-20230304-171334845-14" border="0"></a>

</br>

Sue의 데이터를 저장하려면

</br>

<a href="https://ibb.co/HPyy4Qx"><img src="https://i.ibb.co/fNWWF7n/Kakao-Talk-20230304-171334845-15.jpg" alt="Kakao-Talk-20230304-171334845-15" border="0"></a>

</br>

키의 해시값을 구해서 배열의 상자 수인 5로 mod 연산을 한다. 결과는 1이 나온다.

</br>

<a href="https://ibb.co/1Zydkkf"><img src="https://i.ibb.co/316Mnny/Kakao-Talk-20230304-171334845-16.jpg" alt="Kakao-Talk-20230304-171334845-16" border="0"></a>

</br>

배열 1번 상자에 Sue의 데이터를 저장한다.

</br>

<a href="https://ibb.co/khWDwG3"><img src="https://i.ibb.co/K93sf5N/Kakao-Talk-20230304-171334845-17.jpg" alt="Kakao-Talk-20230304-171334845-17" border="0"></a>

</br>

Dan의 데이터를 저장하려면

</br>

<a href="https://ibb.co/RDPgqfj"><img src="https://i.ibb.co/P64rdKD/Kakao-Talk-20230304-171334845-18.jpg" alt="Kakao-Talk-20230304-171334845-18" border="0"></a>

</br>

키의 해시값을 구해서 배열의 상자 수인 5로 mod 연산을 한다. 결과는 4가 나온다.

</br>

<a href="https://ibb.co/RHJNvHt"><img src="https://i.ibb.co/9Ydh8YB/Kakao-Talk-20230304-171334845-19.jpg" alt="Kakao-Talk-20230304-171334845-19" border="0"></a>

</br>

배열의 4번 상자에 Dan의 데이터를 저장한다.

</br>

<a href="https://ibb.co/z62DRHF"><img src="https://i.ibb.co/y4k7yBp/Kakao-Talk-20230304-171334845-20.jpg" alt="Kakao-Talk-20230304-171334845-20" border="0"></a>

</br>

Nell의 데이터를 저장하려면

</br>

<a href="https://ibb.co/gWtB0BK"><img src="https://i.ibb.co/1XRwCwW/Kakao-Talk-20230304-171334845-21.jpg" alt="Kakao-Talk-20230304-171334845-21" border="0"></a>

</br>

키의 해시값을 구해서 배열의 상자 수인 5로 mod 연산을 한다. 결과는 1가 나온다.

</br>

<a href="https://ibb.co/Tqzb9Kk"><img src="https://i.ibb.co/prCRYWx/Kakao-Talk-20230304-171334845-22.jpg" alt="Kakao-Talk-20230304-171334845-22" border="0"></a>

</br>

배열의 1번 상자에 Nell의 데이터를 저장한다. 1번 상자에는 이미 Sue의 데이터가 저장돼 있다. 이런 경우에는

</br>

<a href="https://ibb.co/J5rHZzK"><img src="https://i.ibb.co/GcCRmV0/Kakao-Talk-20230304-171334845-23.jpg" alt="Kakao-Talk-20230304-171334845-23" border="0"></a>

</br>

리스트 구조로 기존 데이터와 연결한다.

해시 테이블에는 몇 가지 종류가 있으며 리스트를 이용하는 방법을 '연쇄법'이라고 한다.

</br>

<a href="https://ibb.co/fkm5MT8"><img src="https://i.ibb.co/GWgL7rs/Kakao-Talk-20230304-171334845-24.jpg" alt="Kakao-Talk-20230304-171334845-24" border="0"></a>

</br>

Ally의 데이터를 저장하기 위해서

</br>

<a href="https://ibb.co/Ry8Y8zT"><img src="https://i.ibb.co/3zK4KBm/Kakao-Talk-20230304-171334845-25.jpg" alt="Kakao-Talk-20230304-171334845-25" border="0"></a>

</br>

키의 해시값을 구해서 배열의 상자 수인 5로 mod 연산을 한다. 결과는 3이 나온다.

</br>

<a href="https://ibb.co/PrhLHgv"><img src="https://i.ibb.co/6yPMCF7/Kakao-Talk-20230304-171334845-26.jpg" alt="Kakao-Talk-20230304-171334845-26" border="0"></a>

</br>

배열의 3번 상자에는 'Joe'의 데이터가 이미 있으므로 'Ally'를 리스트로 연결한다.

</br>

<a href="https://ibb.co/wQnjF24"><img src="https://i.ibb.co/GMZN4rR/Kakao-Talk-20230304-171334845-27.jpg" alt="Kakao-Talk-20230304-171334845-27" border="0"></a>

</br>

Bob의 데이터를 저장하기 위해서

</br>

<a href="https://ibb.co/vcfy7h3"><img src="https://i.ibb.co/3TV6Dvp/Kakao-Talk-20230304-171334845-28.jpg" alt="Kakao-Talk-20230304-171334845-28" border="0"></a>

</br>

키의 해시값을 구해서 배열의 상자 수인 5로 mod 연산을 한다. 결과는 3이 나온다.

</br>

<a href="https://ibb.co/cQ0NmNX"><img src="https://i.ibb.co/5Lm575x/Kakao-Talk-20230304-171334845-29.jpg" alt="Kakao-Talk-20230304-171334845-29" border="0"></a>

</br>

배열의 3번 상자에는 Joe와 Ally의 데이터가 있으므로 'Bob'를 리스트로 연결한다.

</br>

<a href="https://ibb.co/zHZy9DJ"><img src="https://i.ibb.co/vvk7yRY/Kakao-Talk-20230304-171439165.jpg" alt="Kakao-Talk-20230304-171439165" border="0"></a>

</br>

모든 데이터를 저장하면 해시 테이블이 완성된다.

</br>

<a href="https://ibb.co/r5RSdyg"><img src="https://i.ibb.co/ZcpP2T3/Kakao-Talk-20230304-171439165-01.jpg" alt="Kakao-Talk-20230304-171439165-01" border="0"></a>

</br>

Dan의 성별을 찾는 경우를 생각해보겠다. Dan이 배열의 몇 번째 상자에 저장돼 있는지 알려면

</br>

<a href="https://ibb.co/tBgRQpg"><img src="https://i.ibb.co/Zd59Gz5/Kakao-Talk-20230304-171439165-02.jpg" alt="Kakao-Talk-20230304-171439165-02" border="0"></a>

</br>

키인 Dan의 해시값을 구해서 배열의 상자 수인 5로 mod 연산을 한다. 결과는 4가 나온다.

</br>

<a href="https://ibb.co/ZMY4Dy4"><img src="https://i.ibb.co/jrW0X70/Kakao-Talk-20230304-171439165-03.jpg" alt="Kakao-Talk-20230304-171439165-03" border="0"></a>

</br>

배열의 4번 상자에 저장된 데이터의 키가 Dan과 일치한다. 대응되는 값을 꺼내면 Dan의 성별이 남성(M)이라는 것을 알 수 있다.

</br>

<a href="https://ibb.co/8zFRvjg"><img src="https://i.ibb.co/WDSd8cv/Kakao-Talk-20230304-171439165-04.jpg" alt="Kakao-Talk-20230304-171439165-04" border="0"></a>

</br>

Ally의 성별을 찾는 경우를 생각해보겠다. Ally가 배열의 몇 번째 상자에 저장돼 있는지 알기 위해서

</br>

<a href="https://ibb.co/N6mkHg7"><img src="https://i.ibb.co/5WnzfX2/Kakao-Talk-20230304-171439165-05.jpg" alt="Kakao-Talk-20230304-171439165-05" border="0"></a>

</br>

키인 Ally의 해시값을 구해서 배열의 상자 수인 5로 mod 연산을 한다. 결과는 3이 나온다.

</br>

<a href="https://ibb.co/QYhNds7"><img src="https://i.ibb.co/F8cwVGk/Kakao-Talk-20230304-171439165-06.jpg" alt="Kakao-Talk-20230304-171439165-06" border="0"></a>

</br>

배열의 3번 상자에는 Joe가 있으며 Ally가 아니다. Joe의 데이터를 선두로 하는 리스트를 선형 탐색한다.

</br>

<a href="https://ibb.co/Cz15c0X"><img src="https://i.ibb.co/7XYJfyT/Kakao-Talk-20230304-171439165-07.jpg" alt="Kakao-Talk-20230304-171439165-07" border="0"></a>

</br>

키를 Ally로 하는 데이터를 발견했다. 대응하는 값을 추출하면 'Ally'의 성별이 여성(F)인 것을 알 수 있다.

</br>

<a href="https://ibb.co/X8rSNZM"><img src="https://i.ibb.co/dgwG10x/Kakao-Talk-20230304-171439165-08.jpg" alt="Kakao-Talk-20230304-171439165-08" border="0"></a>

</br>

해시 테이블은 해시 함수를 이용해서 배열 내의 특정 데이터를 빠르게 접근할 수 있다. 한편 해시값이 충돌할 때는 리스트를 이용하고 있어서 저장할 데이터 수가 정해져있지 않더라도 유연하게 대응할 수 있다. 해시 테이블에 사용하는 배열의 크기가 너무 작으면 충돌이 많아지고, 선형 탐색의 빈도가 높아지게 된다. 반대로 크기가 너무 크면 데이터가 없는 상자가 많아져서 메모리를 낭비하게 된다. 데이터의 유연한 저장과 빠른 접근이 가능한 해시 테이블은 프로그래밍 언어의 연관 배열(associative array)등에 사용되고 있다. 해시 테이블에는 몇 가지 종류가 있으며 리스트를 이용하는 방법을 '연쇄법'이라고 한다.