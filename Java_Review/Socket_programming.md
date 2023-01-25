Chapter 16. 네트워킹 Networking

# 2. 소켓 프로그래밍

소켓 프로그래밍은 소켓을 이용한 통신 프로그래밍을 뜻하는데, 소켓(socket)이란 프로세스간의 통신에 사용되는 양쪽 끝단(endpoint)을 의미한다. 서로 멀리 떨어진 두 사람이 통신하기 위해서 전화기가 필요한 것처럼, 프로세스간의 통신을 위해서는 그 무언가가 필요하고 그것이 바로 소켓이다.

자바에서는 `java.net`패키지를 통해 소켓 프로그래밍을 지원하는데, 소켓통신에 사용되는 프로토콜에 따라 다른 종류의 소켓을 구현하여 제공한다.

</br>

## 2.1 TCP와 UDP

TCP/IP 프로토콜은 이기종 시스템간의 통신을 위한 표준 프로토콜로 프로토콜의 집합이다. TCP와 UDP 모두 TCP/IP 프로토콜(TCP/IP protocol suites)에 포함되어 있으며, OSI 7계층의 전송계층(transport layer)에 해당하는 프로토콜이다.

TCP와 UDP는 전송 방식이 다르며, 각 방식에 따른 장단점이 있다. 어플리케이션의 특징에 따라 적절한 프로토콜을 선택하여 사용하면 된다.

<a href="https://ibb.co/dDqpvhb"><img src="https://i.ibb.co/1T5XNSs/16-2-1.png" alt="16-2-1" border="0"></a>

TCP를 이용한 통신은 전화에, UDP를 이용한 통신은 소포에 비유된다 TCP는 데이터를 전송하기 전에 먼저 상대편과 연결을 한 후에 데이터를 전소앟며 잘 전송되었는지 확인하고 전송에 실패했다면 해당 데이터를 재전송하기 때문에 신뢰 있는 데이터의 전송이 요구되는 통신에 적합하다. 예를 들면 파일을 주고받는데 적합하다.

UDP는 상대편과 연결하지 않고 데이터르 ㄹ전송하며, 데이터를 전송하지만 데이터가 다르게 수신되었는지 확인하지 않기 때문에 데이터가 전송되었는지 확인할 길이 없다. 또한 데이터를 보낸 순서대로 순신한다는 보장이 없다.

대신 이러한 확인과정이 필요하지 않기 때문에 TCP에 비해 빠른 전송이 가능하다. 게임이나 동영상의 데이터를 전송하는 경우와 같이 데이터가 중간에 손실되어 좀 끊기더라도 빠른 전송이 필요할 때 적합하다. 이때 전송 순서가 바뀌어 늦게 도착한 데이터는 무시하면 된다.

</br>

## 2.2 TCP소켓 프로그래밍

앞서 살펴본 것과 같이 TCP소켓 프로그래밍은 클라이언트와 서버간의 일대일 통신이다. 먼저 서버 프로그램이 실행되어 클라이언트 프로그램의 연결요청을 기다리고 있어야한다. 서버 프로그램과 클라이언트 프로그램간의 통신과정을 단계별로 보면 다음과 같다.

> 1. 서버 프로그램에서는 서버소켓을 사용해서 서버 컴퓨터의 특정 포트에서 클라이언트의 연결요청을 처리할 준비를 한다.
> 2. 크랄이언트 프로그램은 접속할 서버의 IP주소와 포트 정보를 가지고 소켓을 생성해서 서버에 연결을 요청한다.
> 3. 서버소켓은 클라이언트의 연결요청을 받으면 서버에 새로운 소켓을 생성해서 클라이언트의 소켓과 연결되도록 한다.
> 4. 이제 클라이언트의 소켓과 새로 생성된 서버의 소켓은 서버소켓과 관계없이 일대일 통신을 한다.

서버소켓(ServerSocket)은 포트와 결합(bind)되어 포트를 통해 원격 사용자의 연결요청을 기다리다가 연결요청이 올 때마다 새로운 소켓을 생성하여 상대편 소켓과 통신할 수 있도록 연결한다. 여기까지가 서버소켓의 역할이고, 실제적인 데이터 통신은 서버소켓과 관계없이 소켓과 소켓 간에 이루어진다.

이는 마치 전화시스템과 유사해서 서버소켓은 전화교환기에, 소켓은 전화기에 비유할 수 있다. 전화교환기(서버소켓)는 외부전화기(원격 소켓)로부터 걸려온 전화를 내부의 전화기(소켓)로 연결해주고 실제 통화는 전화기(소켓) 대 전화기(원격 소켓)로 이루어지게 하기 때문이다.

여러 개의 소켓이 하나의 포트를 공유해서 사용할 수 있지만, 서버소켓은 다르다. 서버소켓은 포트를 독정한다. 만일 한 포트를 둘 이상의 서버소켓과 연결하는 것이 가능하다 포트(port)는 호스트(컴퓨터)가 외부와 통신을 하기 위한 통로로 하나의 호스트가 65536개의 포트를 가지고 있으며 포트는 번호로 구별된다. 포트의 번호는 0~65535의 범위에 속하는 값인데 보통 1023번 이하의 포트는 FTP나 Telnet과 같은 기존의 다른 통신 프로그램들에 의해서 사용되는 경우가 많기 때문에 1023번 이상의 번호 중에서 사용하지 않는 포트를 골라서 사용해야한다.

> 두 서버소켓이 서로 다른 프로토콜을 사용하는 경우에는 같은 포트를 사용할 수 있다. 포트는 같아도 클라이언트 프로그램이 사용하는 프로토콜로 어떤 서버소켓과 연결되어야하는지 구별할 수 있기 때문이다. 그래도 가능하면 하나의 포트는 하나의 서버소켓만 사용하도록 하는 것이 바람직하다.

다시 정리하면, 서버소켓은 소켓간의 연결만 처리하고 실제 데이터는 소켓들끼리 서로 주고 받는다. 소켓들이 데이터를 주고받는 연결통로는 바로 입출력스트림이다.

소켓은 두 개의 스트림, 입력스트림과 출력스트림을 가지고 있으며 이 스트림들은 연결된 상대편 소켓의 스트림들과 교차연결된다. 한 소켓의 입력스트림은 상대편 소켓의 출력스트림과 연결되고, 출력스트림은 입력스트림과 연결된다. 그래서 한 소켓에서 출력스트림으로 데이터를 보내면 상대편 소켓에서는 입력스트림으로 받게 된다.

앞서 비유한 전화기(소켓)와 비슷해서 소켓이 두 개의 입출력스트림을 갖는 것처럼 전화기 역시 입력과 출력을 위한 두개의 라인을 가지고 있다.

자바에서는 TCP를 이용한 소켓프로그래밍을 위해 `Socket`과 `ServerSocket`크래스를 제공하며 다음과 같은 특징을 갖는다.

> **Socekt** 프로세스간의 통신을 담당하며, InputStream과 OutputStream을 가지고 있다. 이 두 스트림을 통해 프로세스간의 통신입출력이 이루어진다.   
**ServerSocekt** 포트와 연결(bind)되어 외부의 연결요청을 기다리다 연결요청이 들어오면, Socket을 생성해서 소켓과 소켓간의 통신이 이루어지도록 한다. 한 포트에 하나의 ServerSocket만 연결할 수 있다. (프로토콜이 다르면 같은 포트를 공유할 수 있다.)

</br>

예제 16-6 / ch16 / TcpIpServer.java

``` java
import java.net.*;
import java.io.*;
import java.util.*;
import java.text.SimpleDateFormat;

public class TcpIpServer {
	public static void main(String[] args) {
		ServerSocket serverSocket = null;
		
		try {
			// 서버소켓을 생성하여 7777번 포트와 결합(bind)시킨다.
			serverSocket = new ServerSocket(7777);
			System.out.println(getTime() + "서버가 준비되었습니다.");
		} catch (IOException e) { e.printStackTrace(); }
		
		while (true) {
			try {
				System.out.println(getTime() + "연결요청을 기다립니다.");
				// 서버소켓은 클라이언트의 연결요청이 올 때까지 실행을 멈추고 계쏙 기다린다.
				// 클라이언트의 연결요청이 오면 클라이언트 소켓과 통신할 새로운 소켓을 생성한다.
				Socket socket = serverSocket.accept();
				System.out.println(getTime() + socket.getInetAddress() + "로부터 연결요청이 들어왔습니다.");
				
				// 소켓의 출력스트림을 얻는다.
				OutputStream out = socket.getOutputStream();
				DataOutputStream dos = new DataOutputStream(out);
				
				// 원격 소켓(remote socket)에 데이터를 보낸다.
				dos.writeUTF("[Notice] Test Message1 from Server.");
				System.out.println(getTime() + "데이터를 전송했습니다.");
				
				// 스트림과 소켓을 닫아준다.
				dos.close();
				socket.close();
			} catch (IOException e) {
				e.printStackTrace();
			}
		}	// while
	}	// main
	
	// 현재시간을 문자열로 반환하는 함수
	static String getTime() {
		SimpleDateFormat f = new SimpleDateFormat("[hh:mm:ss]");
		return f.format(new Date());
	}
}	// class
```

```
[01:06:24]서버가 준비되었습니다.
[01:06:24]연결요청을 기다립니다.
[01:06:27]/127.0.0.1로부터 연결요청이 들어왔습니다.
[01:06:27]데이터를 전송했습니다.
[01:06:27]연결요청을 기다립니다.
^C
```

이 예제는 간단한 TCP/IP서버를 구현한 것이다. 이 예제를 실행하면 서버소켓이 7777번 포트에서 클라이언트 프로그램의 연결요청을 기다린다. 클라이언트의 요청이 올 때까지 진행을 멈추고 계속 기다린다. 그러다가 클라이언트 프로그램이 서버에 연결을 요청하면, 서버소켓은 새로운 소켓을 생성하여 클라이언트 프로그램의 소켓(원격소켓)과 연결한다.

새로 생성된 소켓은 "[Notice] Test Message1 from Server."라는 데이터를 원격소켓에 전송하고 연결을 종료한다. 그리고 서버소켓은 다시 클라이언트 프로그램의 요청을 기다린다. 위 실행결과는 서버 프로그램(TcpIpServer.java)을 실행시킨 후 클라이언트 프록르매(TcpIpClient.java)를 실행시키고 바로 Ctrl+C로 서버 프로그램을 종료시킨 것이다.

``` java
while (true) {
			try {
                ...
				Socket socket = serverSocket.accept();
                ...
```

클라이언트 프로그램의 요청을 지속적으로 처리하기 위해 무한반복문을 사용했기 떄문에 서버 프로그램을 종료시키려면 Ctrl+C를 눌러서 강제종료 시켜야한다.

</br>

예제 16-7 / ch16 / TcpIpClient.java

``` java
import java.net.*;
import java.io.*;
import java.util.*;
import java.text.SimpleDateFormat;

public class TcpIpClient {
	public static void main(String[] args) {
		try {
			String serverIp = "127.0.0.1";
			
			System.out.println("서버에 연결중입니다. 서버IP : " + serverIp);
			// 소켓을 생성하여 연결을 요천한다.
			Socket socket = new Socket(serverIp, 7777);
			
			// 소켓의 입력스트림을 얻는다.
			InputStream in = socket.getInputStream();
			DataInputStream dis = new DataInputStream(in);
			
			// 소켓으로부터 받은 데이터를 출력한다.
			System.out.println("서버로부터 받은 메세지 : " + dis.readUTF());
			System.out.println("연결을 종료합니다.");
			
			// 스트림과 소켓을 닫는다.
			dis.close();
			socket.close();
			System.out.println("연결이 종료되었습니다.");
		} catch (ConnectException ce) {
			ce.printStackTrace();
		} catch (IOException ie) {
			ie.printStackTrace();
		} catch (Exception e) {
			e.printStackTrace();
		}
	}	// main
}
```

```
서버에 연결중입니다. 서버IP : 127.0.0.1
서버로부터 받은 메세지 : [Notice] Test Message1 from Server.
연결을 종료합니다.
연결이 종료되었습니다.
```

이 예제는 이전 예제인 TCP/IP서버(TcpIpServer.java)와 통신하기 위한 클라이언트 프로그램이다. 연결하고자 하는 서버의 IP와 포트번호를 가지고 소켓을 생성하면 자동적으로 서버에 연결요청을 하게 된다.

``` java
String serverIp = "127.0.0.1";
Socket socket = new Socket(serverIp, 7777);
```

서버프로그램이 실행되고 있지 않거나 서버의 전원이 꺼져있어서 서버와 연결을 실패하면 `ConnectException`이 발생한다.

서버와 연결되면 소켓의 입력스트림을 얻어서 서버가 전송한 데이터를 읽을 수 있다.

``` java
InputStream in = socket.getInputStream();
DataInputStream dis = new DataInputStream(in);

// 소켓으로부터 받은 데이터를 출력한다.
System.out.println("서버로부터 받은 메세지 : " + dis.readUTF());
```

그리고 서버와의 작업이 끝나면 소켓과 스트림을 닫아야 한다.

``` java
dis.close();
socket.close();
```

위의 예제에서는 한 대의 호스트에서 서버 프로그램과 클라이언트 프로그램을 테스트할 수 있도록 서버의 IP를 127.0.0.1로 설정하였지만, 원래는 서버가 실제로 사용하고 있는 IP를 지정해 주어야 한다. 이제 서버와 클라이언트의 연결과정을 단계별로 그림과 함께 자세히 살펴보겠다. 서버의 IP는 192.168.10.100, 클라이언트의 IP는 192.168.10.101이라고 가정하겠다.

1. 서버프로그램(TcpIpServer.java)를 실행시킨다.

<a href="https://imgbb.com/"><img src="https://i.ibb.co/VMHLxmf/16-2-2.png" alt="16-2-2" border="0"></a>

2. 서버 소켓을 생성한다.

``` java
serverSocket = new ServerSocket(7777);  // TcpIpServer.java
```

<a href="https://imgbb.com/"><img src="https://i.ibb.co/Tt0kV96/16-2-3.png" alt="16-2-3" border="0"></a>

3. 서버소켓이 클라이언트 프로그램의 연결요청을 처리할 수 있도록 대기상태로 만든다. 클라이언트 프로그램의 연결요청이 오면 새로운 소켓을 생성해서 클라이언트 프로그램의 소켓과 연결한다.

``` java
Socket socket = serverSocket.accept();  // TcpIpServer.java
```

4. 클라이언트 프로그램(TcpIpClient.java)에서 소켓을 생성하여 서버소켓에 연결을 요청한다.

``` java
// TcpIpClient.java
Socket socket = new Socket(serverIp, 7777);
```

<a href="https://ibb.co/d2Sr2Kq"><img src="https://i.ibb.co/MVbsVN4/16-2-4.png" alt="16-2-4" border="0"></a>

5. 서버소켓은 클라이언트 프로그램의 연결요청을 받아 새로운 소켓을 생성하여 클라이언트 프로그램의 소켓과 연결한다.

``` java
Socket socket = serverSocket.accept();
```

<a href="https://ibb.co/s9F4GWT"><img src="https://i.ibb.co/YBtSM05/16-2-5.png" alt="16-2-5" border="0"></a>

6 . 서버소켓은 클라이언트 프로그램의 연결요청을 받아 새로운 소켓을 생성하여 새로운 클라이언트 프로그램의 소켓과 연결한다.

<a href="https://ibb.co/jWqprvJ"><img src="https://i.ibb.co/KLB1rjK/16-2-6.png" alt="16-2-6" border="0"></a>

</br>

예제 16-8 / ch16 / TcpIpServer2.java

``` java
import java.net.*;
import java.io.*;
import java.util.*;
import java.text.SimpleDateFormat;

public class TcpIpServer2 {
	public static void main(String[] args) {
		ServerSocket serverSocket = null;
		
		try {
			// 서버소켓을 생성하여 7777번 포트와 결합(bind)시킨다.
			serverSocket = new ServerSocket(7777);
			System.out.println(getTime() + "서버가 준비되었습니다.");
		} catch (IOException e) {
			e.printStackTrace();
		}
		
		while (true) {
			try {
				// 서버소켓
				System.out.println(getTime() + "연결요청을 기다립니다.");
				Socket socket = serverSocket.accept();
				System.out.println(getTime() + socket.getInetAddress() + "로부터 연결요청이 들어왔습니다.");
				
				System.out.println("getPort() : " + socket.getPort());
				System.out.println("getLocalPort() : " + socket.getLocalPort());
				
				// 소켓의 출력스트림을 얻는다.
				OutputStream out = socket.getOutputStream();
				DataOutputStream dos = new DataOutputStream(out);
				
				// 원격 소켓(remote socket)에 데이터를 보낸다.
				dos.writeUTF("[Notice] Test Message1 from Server.");
				System.out.println(getTime() + "데이터를 전송했습니다.");
				
				// 스트림과 소켓을 닫아준다.
				dos.close();
				socket.close();
			} catch (IOException e) {
				e.printStackTrace();
			}
		}	// while
	}	// main
	
	// 현재시간을 문자열로 반환하는 함수
	static String getTime() {
		SimpleDateFormat f = new SimpleDateFormat("[hh:mm:ss]");
		return f.format(new Date());
	}
}	// class
```

```
[02:00:43]서버가 준비되었습니다.
[02:00:43]연결요청을 기다립니다.
[02:00:45]/127.0.0.1로부터 연결요청이 들어왔습니다.
getPort() : 30088
getLocalPort() : 7777
[02:00:45]데이터를 전송했습니다.
[02:00:45]연결요청을 기다립니다.
```

`Socket`클래스에 정의된 `getPort()`와 `getLocalPort()`를 이용해서 TCP/IP통신에서 소켓이 사용하고 있는 포트를 알아낼 수 있다. `getPort()`가 반환하는 값은 상대편 소켓(원격 소켓)이 사용하는 포트이고 `getLocalPort()`가 변환하는 값은 소켓 자신이 사용하는 포트이다.

결과에서 보면 연결을 요청한 클라이언트 프로그램의 소켓이 사용한 포트는 30088번이고 서버 프로그램의 소켓은 7777번이다.

이를 통해 알 수 있는 것은 서버소켓이 7777번 포트를 사용하고 있어도, 서버소켓이 아닌 소켓은 7777번 포트를 사용할 수 있다는 것이다.

클라이언트 프로그램의 소켓이 사용하는 포트는 사용가능한 임의의 포트가 선택된다.

</br>

예제 16-9 / ch16 / TcpIpServer3.java

``` java
import java.net.*;
import java.io.*;
import java.util.*;
import java.text.SimpleDateFormat;

public class TcpIpServer3 {
	public static void main(String[] args) {
		ServerSocket serverSocket = null;
		
		try {
			// 서버소켓을 생성하여 7777번 포트와 결합(bind)시킨다.
			serverSocket = new ServerSocket(7777);
			System.out.println(getTime() + "서버가 준비되었습니다.");
		} catch (IOException e) {
			e.printStackTrace();
		}
		
		while (true) {
			try {
				System.out.println(getTime() + "연결요청을 기다립니다.");
				
				// 요청대기시간을 5초로 설정한다.
				// 5초동안 접속요청이 없으면 SocketTimeoutException이 발생한다.
				serverSocket.setSoTimeout(5 * 1000);
				Socket socket = serverSocket.accept();
				System.out.println(getTime() + socket.getInetAddress() + "로부터 연결요청이 들어왔습니다.");
				
				// 소켓의 출력스트림을 얻는다.
				OutputStream out = socket.getOutputStream();
				DataOutputStream dos = new DataOutputStream(out);
				
				// 원격 소켓(remote socket)에 데이터를 보낸다.
				dos.writeUTF("[Notice] Test Message1 from Server.");
				System.out.println(getTime() + "데이터를 전송했습니다.");
				
				// 스트림과 소켓을 닫아준다.
				dos.close();
				socket.close();
			}catch (SocketTimeoutException e) {
				System.out.println("지정된 시간동안 접속요청이 없어서 서버를 종료합니다.");
				System.exit(0);
			}catch (IOException e) {
				e.printStackTrace();
			}
		}	// while
	}	// main
	
	// 현재시간을 문자열로 반환하는 함수
	static String getTime() {
		SimpleDateFormat f = new SimpleDateFormat("[hh:mm:ss]");
		return f.format(new Date());
	}
}	// class
```

```
[02:15:37]서버가 준비되었습니다.
[02:15:37]연결요청을 기다립니다.
지정된 시간동안 접속요청이 없어서 서버를 종료합니다.
```

`ServerSocket`클래스의 `setSoTimeout(int timeout)`을 사용해서 서버소켓의 대기시간을 지정할 수 있다. timeout의 값은 천분의 일초단위이며 0을 입력하면 제한시간 없이 대기하게 된다. 지정한 대기시간이 지나면 `accept()`에서 `SocketTimeoutException`이 발생하므로 catch문에서 적절한 처리를 할 수 있다.

</br>

예제 16-10 / ch16 / TcpIpServer4.java

``` java
import java.net.*;
import java.io.*;
import java.util.*;
import java.text.SimpleDateFormat;

public class TcpIpServer4 implements Runnable {
	ServerSocket serverSocket;
	Thread[] threadArr;
	public static void main(String[] args) {
		// 5개의 쓰레드를 생성하는 서버를 생성한다.
		TcpIpServer4 server = new TcpIpServer4(5);
		server.start();
	}
	
	public TcpIpServer4(int num) {
		try {
			// 서버소켓을 생서하여 7777번 포트와 결합(bind)시킨다.
			serverSocket = new ServerSocket(7777);
			System.out.println(getTime() + "서버가 준비되었습니다.");
			
			threadArr = new Thread[num];
		} catch (IOException e) {
			e.printStackTrace();
		}
	}
	
	public void start() {
		for(int i = 0; i < threadArr.length; i++) {
			threadArr[i] = new Thread(this);
			threadArr[i].start();
		}
	}
		
	public void run() {
		while (true) {
			try {
				System.out.println(getTime() + "연결요청을 기다립니다.");
				
				// 요청대기시간을 5초로 설정한다.
				// 5초동안 접속요청이 없으면 SocketTimeoutException이 발생한다.
				serverSocket.setSoTimeout(5 * 1000);
				Socket socket = serverSocket.accept();
				System.out.println(getTime() + socket.getInetAddress() + "로부터 연결요청이 들어왔습니다.");
				
				// 소켓의 출력스트림을 얻는다.
				OutputStream out = socket.getOutputStream();
				DataOutputStream dos = new DataOutputStream(out);
				
				// 원격 소켓(remote socket)에 데이터를 보낸다.
				dos.writeUTF("[Notice] Test Message1 from Server.");
				System.out.println(getTime() + "데이터를 전송했습니다.");
				
				// 스트림과 소켓을 닫아준다.
				dos.close();
				socket.close();
			}catch (IOException e) {
				e.printStackTrace();
			}
		}	// while
	}	// run

	
	// 현재시간을 문자열로 반환하는 함수
	static String getTime() {
		SimpleDateFormat f = new SimpleDateFormat("[hh:mm:ss]");
		return f.format(new Date());
	}
}	// class
```

```
[02:35:18]서버가 준비되었습니다.
[02:35:18]연결요청을 기다립니다.
[02:35:18]연결요청을 기다립니다.
[02:35:18]연결요청을 기다립니다.
[02:35:18]연결요청을 기다립니다.
[02:35:18]연결요청을 기다립니다.
[02:35:21]/127.0.0.1로부터 연결요청이 들어왔습니다.
[02:35:21]데이터를 전송했습니다.
[02:35:21]연결요청을 기다립니다.
[02:35:21]/127.0.0.1로부터 연결요청이 들어왔습니다.
[02:35:21]데이터를 전송했습니다.
[02:35:21]연결요청을 기다립니다.
[02:35:21]/127.0.0.1로부터 연결요청이 들어왔습니다.
[02:35:21]데이터를 전송했습니다.
[02:35:21]연결요청을 기다립니다.
^C
```

여러 개의 쓰레드를 생성해서 클라이언트의 요청을 동시에 처리하도록 하였다. 서버에 접속하는 클라이언트의 수가 많을 때는 쓰레드를 이용해서 클라이언트의 요청을 병렬적으로 처리하는 것이 좋다. 그렇지 않으면 서버가 접속을 요청한 순서대로 처리하기 때문에 늦게 접속을 요청한 클라이언트는 오랜 시간을 기다릴 수 있다.

위의 실행결과는 서버 프로그램(TcpIpServer4.java)을 먼저 실행시킨 다음, 클라이언트 프로그램(TcpIpClient.java)을 여러 개 실행하여 얻은 결과이다.

</br>

예제 16-11 / ch16 / TcpIpServer5.java

``` java
import java.net.*;
import java.io.*;
import java.util.Scanner;

public class TcpIpServer5 {
	public static void main(String[] args) {
		ServerSocket serverSocket = null;
		Socket socket = null;
		
		try {
			// 서버소켓을 생성하여 7777번 포트와 결합(bind)시킨다.
			serverSocket = new ServerSocket(7777);
			System.out.println("서버가 준비되었습니다.");
			
			socket = serverSocket.accept();
			
			
		} catch (IOException e) {
			e.printStackTrace();
		}
	}	// main
}	// class

class Sender extends Thread {
	Socket socket;
	DataOutputStream out;
	String name;
	
	Sender(Socket socket) {
		this.socket = socket;
		try {
			out = new DataOutputStream(socket.getOutputStream());
			name = "[" + socket.getInetAddress() + " : " + socket.getPort() + "]";
		} catch (Exception e) {}
	}
	
	public void run() {
		Scanner scanner = new Scanner(System.in);
		while (out != null) {
			try {
				out.writeUTF(name + scanner.nextLine());
			} catch (IOException e) {}
		}
	}	// run()
}

class Receiver extends Thread {
	Socket socket;
	DataInputStream in;
	
	Receiver(Socket socket) {
		this.socket = socket;
		try {
			in = new DataInputStream(socket.getInputStream());
		} catch (IOException e) {}
	}
	
	public void run() {
		while (in != null) {
			try {
				System.out.println(in.readUTF());
			} catch (IOException e) {}
		}
	}	// run()
}
```

</br>

에제 16-12 / ch16 / TcpIpClient5.java

``` java
import java.net.*;
import java.io.*;

public class TcpIpClient5 {
	public static void main(String[] args) {
		try {
			String serverIp = "127.0.0.1";
			// 소켓을 생성하여 연결을 요천한다.
			Socket socket = new Socket(serverIp, 7777);
			
			System.out.println("서버에 연결되었습니다.");
			Sender sender = new Sender(socket);
			Receiver receiver = new Receiver(socket);
			
			sender.start();
			receiver.start();
		} catch (ConnectException ce) {
			ce.printStackTrace();
		} catch (IOException ie) {
			ie.printStackTrace();
		} catch (Exception e) {
			e.printStackTrace();
		}
	}	// main
}	// class
```

```
서버가 준비되었습니다.
Hello
[/127.0.0.1:7777]me, too
[/127.0.0.1:7777]안녕하세요
날씨가 좋군요.
```

```
서버가 연결되었습니다.
[/127.0.0.1:1355]Hello
me, too
안녕하세요
[/127.0.0.1:1355]날씨가 좋군요.
```

소켓으로 데이터를 송신하는 작업과 수신하는 작업을 별도의 쓰레드 `Sender`와 `Receiver`가 처리하도록 하여 송신과 수신이 동시에 이루어지도록 했다.

서버 프로그램(TcpIpServer5.java)과 클라이언트 프로그램(TcpIpClient5.java)의 화면에 입력한 데이터가 상대방의 화면에 출력되므로 1:1 채팅이 가능하다.

</br>

예제 16-13 / ch15 / TcpIpMultichatServer.java

``` java
import java.net.*;
import java.io.*;
import java.util.*;

public class TcpIpMultichatServer {
	HashMap clients;
	
	TcpIpMultichatServer() {
		clients = new HashMap();
		Collections.synchronizedMap(clients);
	}
	
	public void start() {
		ServerSocket serverSocket = null;
		Socket socket = null;
		
		try {
			serverSocket = new ServerSocket(7777);
			System.out.println("서버가 시작되었습니다.");
			
			while (true) {
				socket = serverSocket.accept();
				System.out.println("[" + socket.getInetAddress() + " : " + socket.getPort() + "]" + "에서 접속하였습니다.");
				ServerReceiver thread = new ServerReceiver(socket);
				thread.start();
			}
		} catch (Exception e) {
			e.printStackTrace();
		}
	}	// start()
	
	void sendToAll(String msg) {
		Iterator it = clients.keySet().iterator();
		
		while (it.hasNext()) {
			try {
				DataOutputStream out = (DataOutputStream)clients.get(it.next());
				out.writeUTF(msg);
			} catch (IOException e) {}
		}	// while
	}	// sentToAll
	
	public static void main(String[] args) {
		new TcpIpMultichatServer().start();
	}
	
	class ServerReceiver extends Thread {
		Socket socket;
		DataInputStream in;
		DataOutputStream out;
		
		ServerReceiver(Socket socket) {
			this.socket = socket;
			try {
				in = new DataInputStream(socket.getInputStream());
				out = new DataOutputStream(socket.getOutputStream());
			} catch (IOException e) {}
		}
		
		public void run() {
			String name = "";
			
			try {
				name = in.readUTF();
				sendToAll("#" + name + "님이 들어오셨습니다.");
				
				clients.put(name, out);
				System.out.println("현재 서버접속자 수는 " + clients.size() + "입니다.");
				while (in != null) {
					sendToAll(in.readUTF());
				}
			} catch (IOException e) {
				// ignore
			} finally {
				sendToAll("#" + name + "님이 나가셨습니다.");
				clients.remove(name);
				System.out.println("[" + socket.getInetAddress() + " : " + socket.getPort() + "]" + "에서 접속을 종료하였습니다.");
				System.out.println("현재 서버접속자 수는 " + clients.size() + "입니다.");
			}	// try
		}	// run
	}	// ReceiverThread
}	// class
```

</br>

예제 16-14 / ch16 / TcpIpMultichatClient.java

``` java
import java.net.*;
import java.io.*;
import java.util.Scanner;

public class TcpIpMultichatClient {
	public static void main(String[] args) {
		if(args.length != 1) {
			System.out.println("USAGE : java TcpIpMultichatClient 대화명");
			System.exit(0);
		}
		
		try {
			String serverIp = "127.0.0.1";
			// 소켓을 생성하여 연결을 요청한다.
			Socket socket = new Socket(serverIp, 7777);
			System.out.println("서버에 연결이 되었습니다.");
			Thread sender = new Thread(new ClientSender(socket, args[0]));
			Thread receiver = new Thread(new ClientReceiver(socket));
		} catch (ConnectException ce) {
			ce.printStackTrace();
		} catch (Exception e) {}
	}	// main
	
	static class ClientSender extends Thread {
		Socket socket;
		DataOutputStream out;
		String name;
		
		ClientSender(Socket socket, String name) {
			this.socket = socket;
			try {
				out = new DataOutputStream(socket.getOutputStream());
				this.name = name;
			} catch (Exception e) {}
		}
		
		public void run() {
			Scanner scanner = new Scanner(System.in);
			try {
				if(out != null) {
					out.writeUTF(name);
				}
			} catch (IOException e) {}
		}	// run()
	}	// Client Sender
	
	static class ClientReceiver extends Thread {
		Socket socket;
		DataInputStream in;
		
		ClientReceiver(Socket socket) {
			this.socket = socket;
			try {
				in = new DataInputStream(socket.getInputStream());
			} catch (IOException e) {}
		}
		
		public void run() {
			while (in != null) {
				try {
					System.out.println(in.readUTF());
				} catch (IOException e) {}
			}
		}	// run()
	}	// ClientReceiver
}	// class
```

```
서버가 시작되었습니다.
[/127.0.0.1 : 1037]에서 접속하였습니다.
현재 서버접속자 수는 1입니다.
[/127.0.0.1 : 1039]에서 접속하였습니다.
현재 서버접속자 수는 2입니다.
[/127.0.0.1 : 1042]에서 접속하였습니다.
현재 서버접속자 수는 3입니다.
[/127.0.0.1 : 1037]에서 접속을 종료하였습니다.
현재 서버접속자 수는 2입니다.
[/127.0.0.1 : 1039]에서 접속을 종료하였습니다.
현재 서버접속자 수는 1입니다.
[/127.0.0.1 : 1042]에서 접속을 종료하였습니다.
현재 서버접속자 수는 0입니다.
```

```
서버에 연결되었습니다.
#bbb님이 들어오셨습니다.
#ccc님이 들어오셨습니다.
안녕하세요?
[aaa]안녕하세요?
[bbb]네 어서오세요.
[ccc]반가워요
[bbb]저는 이만 가볼께요.
#bbb님이 나가셨습니다.
```

```
서버에 연결되었습니다.
#ccc님이 들어오셨습니다.
[aaa]안녕하세요?
네 어서오세요.
[bbb]네 어서오세요.
[ccc]반가워요
저는 이만 가볼께요.
[bbb]저는 이만 가볼께요.
```

```
서버에 연결되었습니다.
[aaa]안녕하세요?
[bbb]네 어서오세요.
반가워요
[ccc]반가워요
[bbb]저는 이만 가볼께요.
```

이번엔 이전의 예제를 발전시켜서 여러 클라이언트가 서버에 접속해서 채팅을 할 수 있는 멀티채팅서버 프로그램(TcpIpMultichatServer.java)을 작성했다.

서버 프로그램(TcpIpMultichatServer.java)을 보면 서버에 접속한 클라이언트(TcpIpMultichatClient.java)를 `HashMap`에 저장해서 관리하고 있다.

``` java
TcpIpMultichatServer() {
    clients = new HashMap();
    Collections.synchronizedMap(clients);   // 동기화 처리
}
```

클라이언트가 멀티채팅서버에 접속하면 `HashMap`에 저장되고 접속을 해제하면 `HashMap`에서 제거한다. 클라이언트가 데이터를 입력하면, 멀티채팅서버는 `HashMap`에 저장된 모든 클라이언트에게 데이터를 전송한다.

``` java
void sendToAll(String msg) {
    Iterator it = clients.keySet().iterator();
    
    while (it.hasNext()) {
        try {
            DataOutputStream out = (DataOutputStream)clients.get(it.next());
            out.writeUTF(msg);
        } catch (IOException e) {}
    }	// while
}	// sentToAll
```

멀티채팅서버의 `ServerReceiver`쓰레드는 클라이언트가 추가될 떄마다 생성되며 클라이언트의 입력을 서버에 접속된 모든 클라이언트에게 전송하는 일을 한다.

``` java
public void run() {
    try {
        clients.put(name, out);
        System.out.println("현재 서버접속자 수는 " + clients.size() + "입니다.");
        while (in != null) {
            sendToAll(in.readUTF());
        }
    } catch (IOException e) {
        // ignore
    } finally {
        sendToAll("#" + name + "님이 나가셨습니다.");
        clients.remove(name);
        ...
    }	// try
}	// run
```

이 쓰레드의 `run()`을 보면 클라이언트가 새로 추가되었을 때 클라이언트의 이름을 `key`로 클라이언트의 출력스트림을 `HashMap`인 `clients`에 저장해서 다른 클라이언트가 입력한 데이터를 전송하는데 사용하는 것을 알 수 있다.

만일 클라이언트가 종료되어 클라이언트의 입력스트림(in)이 null이 되면 while문을 빠져나가서 `clients`의 목록에서 해당 클라이언트를 제거한다.

</br>

## 2.3 UDP소켓 프로그래밍

TCP소켓 프로그래밍에서는 `Socket`과 `ServerSocket`을 사용하지만, UDP소켓 프로그래밍에서는 `DatagramSocket`과 `DatagramPacket`을 사용한다.

UDP는 연결지향적인 프로토콜이 아니기 때문에 `ServerSocket`이 필요하지 않다. UDP통신에서 사용하는 소켓은 `DatagramSocket`이며 데이터를 `DatagramPacket`에 담아서 전송한다.

`DatagramPacket`은 헤더와 데이터로 구성되어 있으며, 헤더에는 `DatagramPacket`을 수신할 호스트의 정보(호스트의 주소와 포트)가 저장되어 있다. 소포(packet)에 수신할 상대편의 주소를 적어서 보내는 것과 같다고 이해하면 된다.

그래서 `DatagramPacket`을 전송하면 `DatagramPacket`에 지정된 주소(호스트의 포트)의 `DatagramSocket`에 도착한다

</br>

예제 16-15 / ch16 / UdpClient.java

``` java
import java.net.*;
import java.io.*;

public class UdpClient {
	public void start() throws IOException, UnknownHostException{
		DatagramSocket datagramSocket = new DatagramSocket();
		InetAddress serverAddress = InetAddress.getByName("127.0.0.1");
		
		// 데이터가 저장될 공간으로 byte배열에 생성한다.
		byte[] msg = new byte[100];
		
		DatagramPacket outPacket = new DatagramPacket(msg, 1, serverAddress, 7777);
		DatagramPacket inPacket = new DatagramPacket(msg, msg.length);
		
		
		datagramSocket.send(outPacket);	// DatagramPacket을 전송한다.
		datagramSocket.receive(inPacket);	// DatagramPacket을 수신한다.
		
		System.out.println("current server time : " + new String(inPacket.getData()));
		
		datagramSocket.close();
	}	// start()
	
	public static void main(String[] args) {
		try {
			new UdpClient().start();
		} catch (Exception e) {
			e.printStackTrace();
		}
	}	// main
}	
```

```
current server time : [20:53:23]
```

</br>

예제 16-16 / ch16 / UdpServer.java

``` java
import java.net.*;
import java.io.*;
import java.util.Date;
import java.text.SimpleDateFormat;

public class UdpServer {
	public void start() throws IOException {
		// 포트 7777번을 사용하는 소켓을 생성한다.
		DatagramSocket socket = new DatagramSocket(7777);
		DatagramPacket iniPacket, outPacket;
		
		byte[] inMsg = new byte[10];
		byte[] outMsg;
		
		while (true) {
			// 데이터를 수신하기 위한 패킷을 생성한다.
			iniPacket = new DatagramPacket(inMsg, inMsg.length);
			
			// 패킷을 통해 데이터를 수신(receive)한다.
			socket.receive(iniPacket);
			
			// 수신할 패킷으로부터 clients의 IP주소와 Port를 얻는다.
			InetAddress address = iniPacket.getAddress();
			int port = iniPacket.getPort();
			
			// 서버의 현재 시간을 시분초 형태([hh:mm:ss])로 반환한다.
			SimpleDateFormat sdf = new SimpleDateFormat("[hh:mm:ss]");
			String time = sdf.format(new Date());
			outMsg = time.getBytes();	// time을 byte배열로 변환한다.
			
			// 패킷을 생성해서 client에게 전송(send)한다.
			outPacket = new DatagramPacket(outMsg, outMsg.length, address, port);
			socket.send(outPacket);
		}
	}	// start()
	
	public static void main(String[] args) {
		try {
			// UDP서버를 실행시킨다.
			new UdpServer().start();
		} catch (IOException e) {
			e.printStackTrace();
		}
	}
}
```

서버로부터 서버시간을 전송받아 출력하는 간단한 UDP소켓 클라이언트와 서버프로그램이다. 클라이언트가 `DatagramPacket`을 생성해서 `DatagramSocket`으로 서버에 전송하면, 서버는 전송받은 `DatagramPacket`의 `getAddress()`, `getPort()`를 호출해서 클라이언트의 정보를 얻어서 서버시간을 `DatagramPacket`에 담아서 전송한다.

> UdpClient를 실행하기 전에 UdpServer를 먼저 실행해야 한다.