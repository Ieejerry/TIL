Chapter 16. 네트워킹 Networking

# 1. 네트워킹(Networking)

네트워킹(Networking)이란 두 대 이상의 컴퓨터를 케이블로 연결하여 네트워크(network)를 구성하는 것을 말한다. 네트워킹의 개념은 컴퓨터를 서로 연결하여 데이터를 손쉽게 주고받거나 또는 자원프틴터와 같은 주변기기를 함께 공유하고자 하는 노력에서 시작되었다.

초기의 네트워크는 단 몇 대의 컴퓨터로 구성되었으나 지금은 전세계의 셀 수도 없을 만큼의 많은 수의 컴퓨터가 인터넷이라는 하나의 거대한 네트워크를 구성하고 있으며, 인터넷을 통해 다양하고 방대한 양의 데이터를 공유하는 것이 가능해졌다.

자바에서 제공하는 `java.net`패키지를 사용하면 이러한 네트워크 어플리케이션의 데이터 통신 부분을 쉽게 작성할 수 있으며, 간단한 네트워크 어플리케이션은 단 몇 줄의 자바코드만으로도 작성이 가능하다.

</br>

## 1.1 클라이언트/서버(client/server)

'클라이언트/서버'는 컴퓨터간의 관계를 역할로 구분하는 개념이다. 서버(server)는 서비스를 제공하는 컴퓨터(service provider)이고, 클라이언트(client)는 서비스를 사용하는 컴퓨터(service user)가 된다.

일반적으로 서버는 다수의 클라이언트에게 서비스를 제공하기 때문에 고사양의 하드웨어를 갖춘 컴퓨터이지만, 하드웨어의 사양으로 서버와 클라이언트를 구분하는 것이 아니기 때문에 하드웨어의 사양에 관계없이 서비스를 제공하는 소프트웨어가 실행되는 컴퓨터를 서버라 한다.

서비스는 서버가 클라이언트로부터 요청받은 작업을 처리하여 그 결과를 제고하는 것을 뜻하며 서버가 제공하는 서비스의 종류에 따라 파일서버(file server), 메일서버(mail server), 어플리케이션 서버(application server) 등이 있다. 예를 들어 파일서버(file server)는 클라이언트가 요청한 파일을 제공하는 서비스를 수행한다.

서버에 접속하는 클라이언트의 수에 따라 하나의 서버가 여러 가지 서비스를 제공하기도 하고 하나의 서비스를 여러 대의 서버로 제공하기도 한다.

서버가 서비스를 제공하기 위해서는 서버프로그램이 있어야 하고 클라이언트가 서비스를 제공받기 위해서는 서버프로그램과 연결할 수 있는 클라이언트 프로그램이 있어야 한다. 예를 들어 웹서버에 접속하여 정보를 얻기 위해서는 웹브라우저(클라이언트 프로그램)가 있어야 하고, FTP서버에 접속해서 파일을 전송받기 위해서는 알FTP와 같은 FTP클라이언트 프로그램이 필요하다.

일반 PC의 경우 주로 서버에 접속하는 클라이언트 역할을 수행하지만, FTP SErv-U와 같은 FTP서버프로그램이나 Tomcat과 같은 웹서버프로그램을 설치하면 서버역할도 수행할 수 있다.

파일공유프로그램인 소리바다나 프루나와 같은 프로그램은 클라이언트프로그램과 서버프로그램을 하나로 합친 것으로 이를 설치한 컴퓨터는 클라이언트인 동시에 서버가 되어 다른 컴퓨터로부터 파일을 가져오는 동시에 또 다른 컴퓨터에게 파일을 제공할 수 있다.

네트워크를 구성할 때 전용서버를 두는 것을 서버기반모델(server-based model)이라 하고 별도의 전용서버없이 각 클라이언트가 서버역할을 동시에 수행하는 것을 P2P모델(pear-to-pear)이라 한다.

각 모델의 특징과 장단점은 다음과 같다.

![image](https://ifh.cc/g/lhQvCp.png)

</br>

## 1.2 IP주소(IP address)

IP주소는 컴퓨터(호스트, host)를 구별하는데 사용되는 고유한 값으로 인터넷에 연결된 모든 컴퓨터는 IP주소를 갖는다. IP주소는 4 byte(32 bit)의 정수로 구성되어 있으며, 4개의 정수가 마침표를 구부낮로 'a.b.c.d'와 같은 형식으로 표현된다. 여거서 a, b, c, d는 부호없는 1 byte값, 즉 0~255사이의 정수이다.

IP주소는 다시 네트워크주소와 호스트주소로 나눌 수 있는데, 32 bit(4 byte)의 IP주소중에서 네트웤주소와 호스트주소가 각각 몇 bit를 차지하는 지는 네트워크를 어떻게 구성하였는지에 따라 달라진다. 그리고 서로 다른 두 호스트의 IP주소의 네트워크주소가 같다는 것은 두 호스트가 같은 네트워크에 포함되어 있다는 것을 의미한다.

윈도우즈 OS에서 호스트의 IP주소를 확인하려면 콘솔에서 ipconfig.exe를 실행시키면 된다.

```
C:\Users\iksrnd>ipconfig

Windows IP 구성

무선 LAN 어댑터 Wi-Fi:

   연결별 DNS 접미사. . . . :
   링크-로컬 IPv6 주소 . . . . : fe80::3ba9:4f12:723b:19d9%22
   IPv4 주소 . . . . . . . . . : 172.30.1.37
   서브넷 마스크 . . . . . . . : 255.255.255.0
   기본 게이트웨이 . . . . . . : 172.30.1.254
```

위의 결과에서 얻은 IP주소와 서브넷 마스크를 2진수로 표현하면 다음과 같다.

![image](https://ifh.cc/g/FRhwDx.png)

IP주소와 서브넷 마스크를 비트연산자 '&'로 연산하면 IP주소에서 네트워크 주소만을 뽑아낼 수 있다.

![image](https://ifh.cc/g/0mzaWK.png)

'&'연산자는 bit의 값이 모두 1일 때만 1을 결과로 얻기 때문에 IP주소의 마지막 8 bit는 모두 0이 되었다. 이 결과로 부터 IP주소 192.168.10.100의 네트워크 주소는  24 bit(192.168.10)이라는 것과 호스트 주소는 마지막 8 bit(100)이라는 것을 알 수 있다.

IP주소에서 네트워크주소가 차지하는 자리수가 많을수록 호스트 주소의 범위가 줄어들기 때문에 네트워크의 규모가 작아진다. 이 경우 호스트 주소와 자리수가 8자리이기 때문에 256개(2<sup>8</sup>)의 호스트만 이 네트워크에 포함될 수 있다.

호스트 주소가 0인 것은 네트워크 자신을 나타내고, 255는 브로드캐스트 주소로 사용되기 때문에 실제로는 네트워크에 포함 가능한 호스트 개수는 254개이다.

이처럼 IP주소와 서브넷 마스크를 '&'연산하면 네트워크 주소를 얻어낼 수 있어서 서로 다른 두 호스트의 IP주소를 서브넷 마스크로 '&'연산을 수행해서 비교하면 이 두 호스트가 같은 네트워크 상에 존재하는지를 쉽게 확인할 수 있다.

</br>

## 1.3 InetAddress

자바에서는 IP주소를 다루기 위한 클래스로 `InetAddress`를 제공하며 다음과 같은 메소드가 정의되어 있다.

![image](https://ifh.cc/g/ggSHhS.png)

</br>

예제 16-1 / ch16 / NetworkEx1.java

``` java
import java.net.*;
import java.util.*;

public class NetworkEx1 {
	public static void main(String[] args) {
		InetAddress ip = null;
		InetAddress[] ipArr = null;
		
		try {
			ip = InetAddress.getByName("www.naver.com");
			System.out.println("getHostName() : " + ip.getHostName());
			System.out.println("getHostAddress() : " + ip.getHostAddress());
			System.out.println("toString() : " + ip.toString());
			
			byte[] ipAddr = ip.getAddress();
			System.out.println("getAddress() : " + Arrays.toString(ipAddr));
			
			String result = "";
			for(int i = 0; i < ipAddr.length; i++) {
				result += (ipAddr[i] < 0) ? ipAddr[i] + 256 : ipAddr[i];
				result += ".";
			}
			System.out.println("getAddress() + 256 : " + result);
			System.out.println();
		} catch (UnknownHostException e) {
			e.printStackTrace();
		}
		
		try {
			ip = InetAddress.getLocalHost();
			System.out.println("getHostName() : " + ip.getHostName());
			System.out.println("getHostAddress() : " + ip.getHostAddress());
			System.out.println();
		} catch (UnknownHostException e) {
			e.printStackTrace();
		}
		
		try {
			ipArr = InetAddress.getAllByName("www.naver.com");
			
			for(int i = 0; i < ipArr.length; i++) {
				System.out.println("ipArr[" + i + "] :" + ipArr[i]);
			}
		} catch (UnknownHostException e) {
			e.printStackTrace();
		}
	}	// main
}
```

```
getHostName() : www.naver.com
getHostAddress() : 223.130.195.200
toString() : www.naver.com/223.130.195.200
getAddress() : [-33, -126, -61, -56]
getAddress() + 256 : 223.130.195.200.

getHostName() : DESKTOP-OTCFE5N
getHostAddress() : 172.30.1.37

ipArr[0] :www.naver.com/223.130.195.200
ipArr[1] :www.naver.com/223.130.200.107
```

`InetAddress`의 주요 메소드들을 활용하는 예제이다. 하나의 도메인명(www.naver.com)에 여러 IP주소가 맵핑될 수도 있고 또 그 반대의 경우도 가능하기 때문에 전자의 경우 `getAllByName()`을 통해 모든 IP주소를 얻을 수 있다.

그리고 `getLocalHost()`를 사용하면 호스트명과 IP주소를 알아낼 수 있다.

</br>

## 1.4 URL(Uniform Resource Locator)

URL은 인터넷에 존재하는 여러 서버들이 제공하는 자원에 접근할 수 있는 주소를 표현하기 위한 것으로 '프로토콜://호스트명:포트번호/경로명/파일명?쿼리스트링#참조'의 형태로 이루어져 있다.

> URL에서 포트번호, 쿼리, 참조는 생략할 수 있다.

> http://www.codechobo.com:80/sample/heelo.html?referer=codechobo#index1   
**프로토콜** 자원에 접근하기 위해 서버와 통신하는데 사용되는 통신규약(hhtp)   
**호스트명** 자원을 제공하는 서버의 이름(www.codechobo.com)   
**포트번호** 통신에 사용되는 서버의 포트번호(80)   
**경로명** 접근하려는 자원이 저장된 서버상의 위치(/sample/)   
**파일명** 접근하려는 자원의 이름(hello.html)  
**쿼리(query)** URL에서 '?'이후의 부분(referer=codechobo)   
**참조(anchor)** URL에서 '#'이후의 부분(index1)

> HTTP프로토콜에서는 80번 포트를 사용하기 때문에 URL에서 포트번호를 생략하는 경우 80으로 간주한다. 각 프로토콜에 따라 통신에 사용되는 포트번호가 다르며 생략되면 각 프로토콜의 기본 포트가 사용된다.

자바에서는 URL을 다루기 위한 클래스로 URL클래스를 제공하며 다음과 같은 메소드가 정의되어 있다.

![image](https://ifh.cc/g/FjTb1c.png)

URL객체를 생성하는 방법은 다음과 같다.

``` java
URL url = new URL("http://www.codechobo.com/sample/hello.html");
URL url = new URL("www.codechobo.com","/sample/hello.html");
URL url = new URL("http", "www.codechobo.com", 80, "/sample/hello.html");
```

</br>

예제 16-2 / ch16 / NetworkEx2.java

``` java
import java.net.*;

public class NetworkEx2 {
	public static void main(String[] args) throws Exception{
		URL url = new URL("https://ehyssng.tistory.com/173");
		
		System.out.println("url.getAuthority() : " + url.getAuthority());
		System.out.println("url.getContent() : " + url.getContent());
		System.out.println("url.getDefaultPort() : " + url.getDefaultPort());
		System.out.println("url.getPort() : " + url.getPort());
		System.out.println("url.getFile() : " + url.getFile());
		System.out.println("url.getHost() : " + url.getHost());
		System.out.println("url.getPath() : " + url.getPath());
		System.out.println("url.getProtocol() : " + url.getProtocol());
		System.out.println("url.getQuery() : " + url.getQuery());
		System.out.println("url.getRef() : " + url.getRef());
		System.out.println("url.getUserInfo() : " + url.getUserInfo());
		System.out.println("url.toExternalForm() : " + url.toExternalForm());
		System.out.println("url.toURI() : " + url.toURI());
	}
}
```

```
url.getAuthority() : ehyssng.tistory.com
url.getContent() : sun.net.www.protocol.http.HttpURLConnection$HttpInputStream@385c9627
url.getDefaultPort() : 443
url.getPort() : -1
url.getFile() : /173
url.getHost() : ehyssng.tistory.com
url.getPath() : /173
url.getProtocol() : https
url.getQuery() : null
url.getRef() : null
url.getUserInfo() : null
url.toExternalForm() : https://ehyssng.tistory.com/173
url.toURI() : https://ehyssng.tistory.com/173
```

</br>

## 1.5 URLConnection

`URLConnection`은 어플리케이션과 URL간의 통신연결을 나타내는 클래스의 최상위 클래스로 추상클래스이다. `URLConnection`을 상속받아 구현한 클래스로는 `HttpURLConnection`과 `JarURLConnection`이 있으며 URL의 프로토콜이 http프로토콜이라면 `openConnection()`은 `HttpURLConnection`은 반환한다. `URLConnection`을 사용해서 연결하고자 하는 자원에 접근하고 읽고 쓰기를 할 수 있다. 그 외에 관련된 정보를 읽고 쓸 수 있는 메소드가 제공된다.

> OpenConnection()은 URL클래스의 메소드이다.

> HttpURLConnecton은 sun.net.www.protocol.http패키지에 속해있다.

<a href="https://ibb.co/wJDWkRb"><img src="https://i.ibb.co/0BPM7cW/16-1-6.png" alt="16-1-6" border="0"></a>

</br>

예제 16-3 / ch16 / NetworkEx3.java

``` java
import java.net.*;

public class NetworkEx3 {
	public static void main(String[] args) {
		URL url = null;
		String address = "https://ehyssng.tistory.com/173";
		
		try {
			url = new URL(address);
			URLConnection conn = url.openConnection();
			
			System.out.println("conn.toString() : " + conn);
			System.out.println("conn.getAllowUserInteraction() : " + conn.getAllowUserInteraction());
			System.out.println("conn.getConnectTimeout() : " + conn.getConnectTimeout());
			System.out.println("conn.getContent() : " + conn.getContent());
			System.out.println("conn.getContentEncoding() : " + conn.getContentEncoding());
			System.out.println("conn.getContentLength() : " + conn.getContentLength());
			System.out.println("conn.getContentType() : " + conn.getContentType());
			System.out.println("conn.getDate() : " + conn.getDate());
			System.out.println("conn.getDefaultAllowUserInteraction() : " + conn.getDefaultAllowUserInteraction());
			System.out.println("conn.getDefaultUseCaches() : " + conn.getDefaultUseCaches());
			System.out.println("conn.getDoInput() : " + conn.getDoInput());
			System.out.println("conn.getDoOutput() : " + conn.getDoOutput());
			System.out.println("conn.getExpiration() : " + conn.getExpiration());
			System.out.println("conn.getHeaderFields() : " + conn.getHeaderFields());
			System.out.println("conn.getIfModifiedSince() : " + conn.getIfModifiedSince());
			System.out.println("conn.getLastModified() : " + conn.getLastModified());
			System.out.println("conn.getReadTimeout() : " + conn.getReadTimeout());
			System.out.println("conn.getURL() : " + conn.getURL());
			System.out.println("conn.getUseCaches() : " + conn.getUseCaches());
		} catch (Exception e) {
			e.printStackTrace();
		}
	}	// main
}
```

```
conn.toString() : sun.net.www.protocol.https.DelegateHttpsURLConnection:https://ehyssng.tistory.com/173
conn.getAllowUserInteraction() : false
conn.getConnectTimeout() : 0
conn.getContent() : sun.net.www.protocol.http.HttpURLConnection$HttpInputStream@385c9627
conn.getContentEncoding() : null
conn.getContentLength() : 49676
conn.getContentType() : text/html;charset=UTF-8
conn.getDate() : 1674140623000
conn.getDefaultAllowUserInteraction() : false
conn.getDefaultUseCaches() : true
conn.getDoInput() : true
conn.getDoOutput() : false
conn.getExpiration() : 0
conn.getHeaderFields() : {null=[HTTP/1.1 200], T_USERID=[f685c1999409d1c2230f4c6e337cab6071da8b41], X-Content-Type-Options=[nosniff], Pragma=[no-cache], Date=[Thu, 19 Jan 2023 15:03:43 GMT], Strict-Transport-Security=[max-age=31536000 ; includeSubDomains], Cache-Control=[no-cache, no-store, max-age=0, must-revalidate], Set-Cookie=[REACTION_GUEST=f211f461594a1e77c52cd693c690f2addbd62e20], Vary=[Accept-Encoding], Expires=[0], X-XSS-Protection=[1; mode=block], Content-Length=[49676], Content-Type=[text/html;charset=UTF-8]}
conn.getIfModifiedSince() : 0
conn.getLastModified() : 0
conn.getReadTimeout() : 0
conn.getURL() : https://ehyssng.tistory.com/173
conn.getUseCaches() : true
```

</br>

예제 16-4 / ch16 / NetworkEx4.java

``` java
import java.net.*;
import java.io.*;

public class NetworkEx4 {
	public static void main(String[] args) {
		URL url = null;
		BufferedReader input = null;
		String address = "https://ehyssng.tistory.com/173";
		String line = "";
		
		try {
			url = new URL(address);
			input = new BufferedReader(new InputStreamReader(url.openStream()));
			
			while ((line = input.readLine()) != null) {
				System.out.println(line);
			}
			input.close();
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}
```

```
<!doctype html>
<html lang="ko">
                                                                <head>
                
                
                        <!-- BusinessLicenseInfo - START -->
        
            <link href="https://tistory1.daumcdn.net/tistory_admin/userblog/userblog-ce2b1cf88ca4f3e019bc6a3b9c241e836905a98e/static/plugin/BusinessLicenseInfo/style.css" rel="stylesheet" type="text/css"/>

            <script>function switchFold(entryId) {
    var businessLayer = document.getElementById("businessInfoLayer_" + entryId);

    if (businessLayer) {
        if (businessLayer.className.indexOf("unfold_license") > 0) {
            businessLayer.className = "business_license_layer";
        } else {
            businessLayer.className = "business_license_layer unfold_license";
        }
    }
}
</script>

        
        <!-- BusinessLicenseInfo - END -->
        <!-- DaumShow - START -->
        ...
```

URL에 연결하여 그 내용을 읽어오는 예제이다. 만일 URL이 유효하지 않으면 `Malformed- URLException`이 발생한다. 읽어올 데이터가 문자데이터이기 때문에 `BufferdReader`를 사용하였다. `openStream()`을 호출해서 URL의 `InputStream`을 얻은 이후로는 파일로 부터 데이터를 읽는 것과 다르지 않다.

`openStream()`은 `openConnection()`을 호출해서 `URLConnection`을 얻은 다음 여기에 다시 `getInputStream()`을 호출한 것과 같다. 즉, URL에 연결해서 `InputStream`을 얻어 온다.

<a href="https://imgbb.com/"><img src="https://i.ibb.co/zGbzhPS/16-1-7.png" alt="16-1-7" border="0"></a>

</br>

예제 16-5 / ch15 / NetworkEx5.java

``` java
import java.net.*;
import java.io.*;

public class NetworkEx5 {
	public static void main(String[] args) {
		URL url = null;
		InputStream in = null;
		FileOutputStream out = null;
		String address = "http://www.codechobo.com/book/src/javajungsuk3_src.zip";
		
		int ch = 0;
		
		try {
			url = new URL(address);
			in = url.openStream();
			out = new FileOutputStream("javajungsuk3_src.zip");
			
			while ((ch = in.read()) != -1) {
				out.write(ch);
			}
			in.close();
			out.close();
		} catch (Exception e) {
			e.printStackTrace();
		}
	}	// main
}
```

```
C:\jdk1.8\work\ch16\dir *.zip
 C 드라이브의 볼륨에는 이름이 없습니다.
 볼륨 일련 번호: B962-DF19

 C:\jdk1.8\work\ch16 디렉토리

2023-01-20  04:36p         10,922,314 javajungsuk3_src.zip
               1개 파일     10,922,314 바이트
            0 디렉토리  63,450,337,280 바이트 남음
```

이전 예제와 유사한데 텍스트가 데이터가 아닌 이진 데이터를 읽어서 파일에 저장한다는 것만 다르다. 그래서 `FileReader`가 아닌 `FileOutputStream`을 사용하였다.