# MySQL Workbench

MySQL Workbench는 MySQL에서 제공하는 GUI기반의 MySQL Client이다.

</br>

## MySQL Workbench 설치

검색엔진에 "mysql workbench`를 검색 후, MySQL 공식사이트의 다운로드 링크로 이동한다.

</br>

<a href="https://ibb.co/fXBQ9Rx"><img src="https://i.ibb.co/wd3Y7Hz/mysqlworkbench1.png" alt="mysqlworkbench1" border="0"></a>

</br>

그러면 위와 같은 사이트가 연결되는데, 빨간 박스의 "Download Now"를 눌러준다. 

</br>

<a href="https://ibb.co/PcNWm1H"><img src="https://i.ibb.co/9bN48y5/mysqlworkbench2.png" alt="mysqlworkbench2" border="0"></a>

</br>

빨간 박스에서 자신 컴퓨터에 맞는 운영체제를 선택 후

</br>

<a href="https://ibb.co/YPTHwYR"><img src="https://i.ibb.co/TYq9dpv/mysqlworkbench3.png" alt="mysqlworkbench3" border="0"></a>

</br>

"Download" 버튼을 눌러 MySQL Workbench를 설치한다.

</br>

## MySQL Workbench 사용법

</br>

<a href="https://ibb.co/x3t3Swc"><img src="https://i.ibb.co/zNTNhCL/mysqlworkbench4.png" alt="mysqlworkbench4" border="0"></a>

</br>

MySQL Workbench를 실행하면 위와 같은 화면이 뜨는데, 빨간 네모칸 안에 +를 버튼을 눌러준다.

</br>

<a href="https://ibb.co/GdZdddP"><img src="https://i.ibb.co/HKcKKKg/mysqlworkbench5.png" alt="mysqlworkbench5" border="0"></a>

</br>

그러면 위와 같은 화면이 띄워지고, "Connection Name"에 원하는 이름을 입력해주면 된다. 나는 "my server"라고 지정해주었다. 그리고 "Hostname"에는 localhost를 뜻하는 "127.0.0.1"를 넣어주었다. "Port"는 기본적으로 3306번 포트로 되어있는데 나의 컴퓨터에는 "3307"번 포트로 되어있어 "3307"번으로 넣어주었다. 비밀번호를 저장하고 싶은 경우에는 "Store in Vault"를 클릭하여 저장해주면 된다. 그 후, "Test Connection"을 클릭하면 된다.

</br>

<a href="https://imgbb.com/"><img src="https://i.ibb.co/D7qNfDt/mysqlworkbench6.png" alt="mysqlworkbench6" border="0"></a>

</br>

비밀번호를 입력 후, 위와 같이 뜬다면 연결 테스트에 성공한 것이고 "OK"버튼을 누르고, 또 "OK"버튼을 눌러 연결정보를 저장해준다.

</br>

<a href="https://ibb.co/58hD1rp"><img src="https://i.ibb.co/Fw4vh5Z/mysqlworkbench7.png" alt="mysqlworkbench7" border="0"></a>

</br>

그리고 아래쪽 빨간 네모박스의 "Schema"를 클릭하게 되면 MySQL Monitor를 통해 만들었던 스키마들을 위의 네모칸처럼 볼 수 있다. 그리고 오른쪽 빨간 네모박스의 "Query"칸에서 원하는 sql문을 입력하여 명령어로도 제어할 수 있다.

</br>

<a href="https://ibb.co/HXKzf8y"><img src="https://i.ibb.co/3kTN9Zb/mysqlworkbench7.png" alt="mysqlworkbench7" border="0"></a>

</br>

빨간 네모박스의 버튼들을 클릭하여 새로운 스키마와 테이블을 생성할 수 있다.

스키마와 테이블을 생성할 때에도 apply하기 전에 sql문들이 표시가 되는데 GUI기반의 MySQL Workbench 같은 경우에도 결국은 명령어로 MySQL Server를 제어한다는 것을 알 수 있다.