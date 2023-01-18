Chapter 15. 입출력 I/O

# 5. 문자기반의 보조스트림

</br>

## 5.1 BufferedReader와 BufferedWriter

`BufferedReader`/`BufferedWriter`는 버퍼를 이용해서 입출력의 효율을 높일 수 있도록 해주는 역할을 한다. 버퍼를 이용하면 입출력의 효율이 비교할 수 없을 정도로 좋아지기 때문에 사용하는 것이 좋다.

`BufferedReader`의 `readline()`을 사용하면 데이터를 라인단위로 읽을 수 있고 `BufferedWriter`는 `newline()`이라는 줄바꿈 해주는 메소드를 가지고 있다.

</br>

예제 15-20 / ch15 / BufferedReaderEx1.java

``` java
import java.io.*;

public class BufferedReaderEx1 {
	public static void main(String[] args) {
		try {
			FileReader fr = new FileReader("BufferedReaderEx1.java");
			BufferedReader br = new BufferedReader(fr);
			
			String line = "";
			for(int i = 1; (line = br.readLine()) != null; i++) {
				// ";"를 포함한 라인을 출력한다.
				if(line.indexOf(";") != -1)
					System.out.println(i + ":" + line);
			}
			
			br.close();
		} catch (IOException e) {}
	}	// main
}
```

```
1:import java.io.*;
6:			FileReader fr = new FileReader("src\\BufferedReaderEx1.java");
7:			BufferedReader br = new BufferedReader(fr);
9:			String line = "";
10:			for(int i = 1; (line = br.readLine()) != null; i++) {
11:				// ";"를 포함한 라인을 출력한다.
12:				if(line.indexOf(";") != -1)
13:					System.out.println(i + ":" + line);
16:			br.close();
```

`BufferedReader`의 `readline()`을 이용해서 파일을 라인단위로 읽은 다음 `indexOf()`를 이용해서 ';'를 포함하고 있는지 확인하여 출력하는 예제이다. 파일에서 특정 문자 또는 문자열을 포함한 라인을 쉽게 찾아낼 수 있다.

</br>

## 5.2 InputStreamReader와 OutputStreamWriter

`InputStreamReader`/`OutputStreamWriter`는 이름에서 알 수 있는 것과 같이 바이트기반 스트림을 문자기반 스트림으로 연결시켜주는 역할을 한다. 그리고 바이트기반 스트림의 데이터를 지정된 인코딩의 문자데이터로 변환하는 작업을 수행한다.

> InputStreamReader/OutputStreamWriter는 Reader/Writer의 자손이다.

![image](https://ifh.cc/g/2DOkMX.png)

</br>

![image](https://ifh.cc/g/nG1WwK.png)

한글윈도우에서 중국어로 작성된 파일을 읽을 때 `InputStreamReader(InputStream in, String encoding)`을 이용해서 인코딩이 중국어로 되어 있다는 것을 지정해주어야 파일 내용이 깨지지 않고 올바르게 보인다. 인코딩을 지정해 주지 않는다면 OS에서 사용하는 인코딩을 사용해서 파일을 해석해서 보여 주기 때문에 원래 작성된 데로 볼 수 없다.

이와 마찬가지로 `OutputStreamWriter`를 이용해서 파일에 텍스트데이터를 저장할 때 생성자 `OutputStreamWriter(OutputStream out, String encoding)`를 이용해서 인코딩을 지정하지 않으면 OS에서 사용하는 인코딩으로 데이터를 저장한다.

> 시스템 속성에서 sun.jnu.encoding의 값을 보면 OS에서 사용하는 인코딩의 종류를 알 수 있다.

``` java
Properties prop = System.getProperties();
System.out.println(prop.get("sun.jnu.encoding"));
```

</br>

예제 15-21 / ch15 / InputStreamReaderEx.java

``` java
import java.io.*;

public class InputStreamReaderEx {
	public static void main(String[] args) {
		String line = "";
		
		try {
			InputStreamReader isr = new InputStreamReader(System.in);
			BufferedReader br = new BufferedReader(isr);
			
			System.out.println("사용중인 OS의 인코딩 : " + isr.getEncoding());
			
			do {
				System.out.print("문장을 입력하세요. 마치시리면 q를 입력하세요.>");
				line = br.readLine();
				System.out.println("입력하신 문장 : " + line);
			} while(!line.equalsIgnoreCase("q"));
			
//			br.close();	// System.in과 같은 표준입출력은 닫지 않아도 된다.
			System.out.println("프로그램을 종료합니다.");
		} catch (IOException e) {}
	}	// main
}
```

```
사용중인 OS의 인코딩 : UTF8
문장을 입력하세요. 마치시리면 q를 입력하세요.>asdf
입력하신 문장 : asdf
문장을 입력하세요. 마치시리면 q를 입력하세요.>hello
입력하신 문장 : hello
문장을 입력하세요. 마치시리면 q를 입력하세요.>q
입력하신 문장 : q
프로그램을 종료합니다.
```

`BufferedReader`의 `readline()`을 이용해서 사용자의 화면입력을 라인단위로 입력받으면 편리하다. 그래서 `BufferedReader`와 `InputStream`인 `System.in`을 연결하기 위해 `InputStreamReader`를 사용하였다. JDK1.5부터는 `Scanner`가 추가되어 이와 같은 방식을 사용하지 않아도 간단하게 처리가 가능하다.

그리고, 현재 사용 중인 OS의 인코딩을 확인하려면 생성자 `InputStreamReader(InputStream in)`를 사용해서 `InputStreamReader`의 인스턴스를 생성한 다음, `getEncoding()`을 호출하면 된다.