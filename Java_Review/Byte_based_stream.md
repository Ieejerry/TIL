Chapter 15. 입출력 I/O

# 2. 바이트기반 스트림

</br>

## 2.1 InputStream과 OutputStream

`InputStream`과 `OutputStream`은 모든 바이트기반의 스트림의 조상이며 다음과 같은 메소드가 선언되어 있다.

![image](https://ifh.cc/g/2Fk9ML.png)

</br>

![image](https://ifh.cc/g/yyZycl.png)

스트림의 종류에 따라서 `mark()`와 `reset()`을 사용하여 이미 읽은 데이터를 되돌려서 다시 읽을 수 있다. 이 기능을 지원하는 스트림인지 확인하는 `markSupported()`를 통해서 알 수 있다.

`flush()`는 버퍼가 있는 출력스트림의 경우에만 의미가 있으며, `OutputStream`에 정의된 `flush()`는 아무런 일도 하지 않는다.

프로그램이 종료될 때, 사용하고 닫지 않은 스트림을 JVM이 자동적으로 닫아 주기는 하지만, 스트림을 사용해서 모든 작업을 마치고 난 후에는 `close()`를 호출해서 반드시 닫아 주어야 한다. 그러나 `ByteArrayInputStream`과 같이 메모리를 사용하는 스트림과 `System.in`, `System.out`과 같은 표준 입출력 스트림은 닫아 주지 않아도 된다.

</br>

## 2.2 ByteArrayInputStream과 ByteArrayOutputStream

`ByteArrayInputStream`/`ByteArrayOutputStream`은 메모리, 즉 바이트배열에 데이터를 입출력 하는데 사용되는 스트림이다. 주로 다른 곳에 입출력하기 전에 데이터를 임시로 바이트배열에 담아서 변환 등의 작업을 하는데 사용된다.

**스트림이 종류가 달라도 읽고 쓰는 방법은 동일하다.**

</br>

예제 15-1 / ch15 / IOEx1.java

``` java
import java.io.*;
import java.util.Arrays;

public class IOEx1 {
	public static void main(String[] args) {
		byte[] inSrc = { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };
		byte[] outSrc = null;
		
		ByteArrayInputStream input = null;
		ByteArrayOutputStream output = null;
		
		input = new ByteArrayInputStream(inSrc);
		output = new ByteArrayOutputStream();
		
		int data = 0;
		
		while((data = input.read()) != -1) {
			output.write(data);	// void write(int b)
		}
		
		outSrc = output.toByteArray();	// 스트림의 내용을 byte배열로 반환한다.
		
		System.out.println("Input Source : " + Arrays.toString(inSrc));
		System.out.println("Output Source : " + Arrays.toString(outSrc));
	}
}
```

```
Input Source : [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
Output Source : [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

`ByteArrayInputStream`/`ByteArrayOutputStream`을 이용해서 바이트배열 `inSrc`의 데이터를 `outSrc`로 복사하는 예제인데, `read()`와 `write()`를 사용하는 가장 기본적인 방법을 보여준다. while문의 조건식이 조금 복잡한데, 이 조건식은 아래와 같은 순서로 처리된다.

``` java
(data = input.read()) != -1

① data = input.read() // read()를 호출한 반환값을 변수 data에 저장한다. (괄호 먼저)
② data != -1 // data에 저장된 값이 -1이 아닌지 비교한다.
```

바이트배열은 사용하는 자원이 메모리 밖에 없으므로 가비지컬렉터에 의해 자동적으로 자원을 반환하므로 `close()`를 이용해서 스트림을 닫지 않아도 된다. `read()`와 `write(int b)`를 사용하기 때문에 한 번에 1 byte만 읽고 쓰므로 작업효율이 떨어진다.

다음 예제는 배열을 사용해서 입출력 작업이 보다 효율적하였다.

</br>

예제 15-2 / ch15 / IOEx2.java

``` java
import java.io.*;
import java.util.Arrays;

public class IOEx2 {
	public static void main(String[] args) {
		byte[] inSrc = { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };
		byte[] outSrc = null;
		byte[] temp = new byte[10];
		
		ByteArrayInputStream input = null;
		ByteArrayOutputStream output = null;
		
		input = new ByteArrayInputStream(inSrc);
		output = new ByteArrayOutputStream();
		
		input.read(temp, 0, temp.length);	// 읽어 온 데이터를 배열 temp에 담는다.
		output.write(temp, 5, 5);	// temp[5]부터 5개의 데이터를 write한다.
		
		outSrc = output.toByteArray();
		
		System.out.println("Input Source : " + Arrays.toString(inSrc));
		System.out.println("temp : " + Arrays.toString(temp));
		System.out.println("Output Source : " + Arrays.toString(outSrc));
	}
}
```

```
Input Source : [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
temp : [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
Output Source : [5, 6, 7, 8, 9]
```

`int read(byte[] b, int off, int len)`와 `void write(byte[] b, int off, int len)`를 사용해서 입출력하는 방법을 보여주는 예제이다. 이전 예제와는 달리 byte배열을 사용해서 한 번에 배열의 크기만큼 읽고 쓸 수 있다. 바구니(배열 temp)를 이용하면 한 번에 더 많은 물건을 옮길 수 있다는 것과 같다고 이해하면 된다.

byte배열 `temp`의 크기(temp.length)가 10이라서 10 byte를 읽어왔지만 `output`에 출력할 때는 `temp[5]`부터 5 byte만 출력하였다.

``` java
input.read(temp, 0, temp.length);   // 읽어 온 데이터를 배열 temp에 담는다.
output.write(temp, 5, 5);   // temp[5]부터 5개의 데이터를 write한다.
```

배열을 이용한 입출력은 작업의 효율을 증가시키므로 가능하면 입출력 대상에 따라 알맞은 크기의 배열을 사용하는 것이 좋다.

</br>

예제 15-3 / ch15 / IOEx3.java

``` java
import java.io.*;
import java.util.Arrays;

public class IOEx3 {
	public static void main(String[] args) {
		byte[] inSrc = { 0, 1, 2, 3, 4, 5, 6, 7 ,8, 9 };
		byte[] outSrc = null;
		byte[] temp = new byte[4];	// 이전 예제의 배열의 크기가 다르다.
		
		ByteArrayInputStream input = null;
		ByteArrayOutputStream output = null;
		
		input = new ByteArrayInputStream(inSrc);
		output = new ByteArrayOutputStream();
		
		System.out.println("Input Source : " + Arrays.toString(inSrc));
		
		try {
			while(input.available() > 0) {
				input.read(temp);
				output.write(temp);
//				System.out.println("temp : " + Arrays.toString(temp));
				
				outSrc = output.toByteArray();
				printArrays(temp, outSrc);
			}
		} catch (IOException e) {}
	}	// main의 끝
	
	static void printArrays(byte[] temp, byte[] outSrc) {
		System.out.println("temp : " + Arrays.toString(temp));
		System.out.println("Output Source : " + Arrays.toString(outSrc));
	}
}
```

```
Input Source : [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
temp : [0, 1, 2, 3]
Output Source : [0, 1, 2, 3]
temp : [4, 5, 6, 7]
Output Source : [0, 1, 2, 3, 4, 5, 6, 7]
temp : [8, 9, 6, 7]
Output Source : [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 6, 7]
```

`read()`나 `write()`이 `IOException`을 발생시킬 수 있기 때문에 try-catch문으로 감싸주었다. `available()`은 블락킹(blocking)없이 읽어올 수 있는 바이트의 수를 반환한다.

마지막에 읽은 배열의 9번째와 10번째 요소값인 8과 9만을 출력해야하는데 `temp`에 남아 있던 6, 7까지 출력했다.

보다 나은 성능을 위해서 `temp`에 담긴 내용을 지우고 쓰는 것이 아니라 그냥 기존의 내용 위에 덮어 쓴다. 그래서 `temp`의 내용은 '[4, 5, 6, 7]'이었는데, 8과 9를 읽고 난 후에는 '[8, 9, 6, 7]'이 된다.

원하는 결과를 얻기 위해서는 아래 왼쪽의 코드를 오른쪽과 같이 수정해야 한다. 왼쪽의 코드는 배열의 내용전체를 출력하지만, 오른쪽의 코드는 읽어온 만큼(len)만 출력한다.

![image](https://ifh.cc/g/XfLX4h.png)

> 블락킹이란 데이터를 읽어올 때 데이터를 기다리기 위해 멈춰있는 것을 뜻한다. 예를 들어 사용자가 데이터를 입력하기 전까지 기다리고 있을 때 블락킹 상태에 있다고 한다.

</br>

예제 15-4 / ch15 / IOEx4.java

``` java
import java.io.*;
import java.util.Arrays;

public class IOEx4 {
	public static void main(String[] args) {
		byte[] inSrc = { 0, 1, 2, 3, 4, 5, 6, 7 ,8, 9 };
		byte[] outSrc = null;
		byte[] temp = new byte[4];
		
		ByteArrayInputStream input = null;
		ByteArrayOutputStream output = null;
		
		input = new ByteArrayInputStream(inSrc);
		output = new ByteArrayOutputStream();
		
		try {
			while(input.available() > 0) {
				int len = input.read(temp);	// 읽어 온 데이터의 개수를 반환한다.
				output.write(temp, 0, len);	// 읽어 온 만큼만 write한다.
			}
		} catch (IOException e) {}
		
		outSrc = output.toByteArray();
		
		System.out.println("Input Source : " + Arrays.toString(inSrc));
		System.out.println("temp : " + Arrays.toString(temp));
		System.out.println("Output Source : " + Arrays.toString(outSrc));
	}
}
```

```
Input Source : [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
temp : [8, 9, 6, 7]
Output Source : [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

이전 예제의 문제점을 수정한 예제이다. 출력할 때, `temp`에 저장된 모든 내용을 출력하는 대신 값을 읽어온 만큼만 출력하도록 변경하였다. 그래서 이전 예제와 달리 올바른 결과를 얻은 것을 확인할 수 있다.

</br>

## 2.3 FileInputStream과 FileOutputStream

`FileInputStream`/`FileOutputStream`은 파일에 입출력을 하기 위한 스트림이다.

![image](https://ifh.cc/g/zQ4QcP.png)

</br>

예제 15-5 / ch15 / FileViewer.java

``` java
import java.io.*;

public class FileViewer {
	public static void main(String[] args) throws IOException {
		FileInputStream fis = new FileInputStream(args[0]);
		int data = 0;
		
		while ((data = fis.read()) != -1) {
			char c = (char)data;
			System.out.println(c);
		}
	}
}
```

```
C:\jdk1.8\work\ch15>java.FileViewer FileView.java
import java.io.*;

public class FileViewer {
	public static void main(String[] args) throws IOException {
		FileInputStream fis = new FileInputStream(args[0]);
		int data = 0;
		
		while ((data = fis.read()) != -1) {
			char c = (char)data;
			System.out.println(c);
		}
	}
}
```

커맨드라인으로부터 입력받은 파일의 내용을 읽어서 그대로 화면에 출력하는 간단한 예제이다. `read()`의 반환값이 int형(4 byte)이긴 하지만, 더 이상 입력값이 없음을 알리는 -1을 제외하고는 0~255(1 byte)범위의 정수값이기 때문에, char형(2 byte)으로 변환한다 해도 손실되는 값은 없다.

`read()`가 한 번에 1 byte씩 파일로부터 데이터를 읽어 들이긴 하지만, 데이터의 범위가 십진수로 0~255(16진수로는 0x00~0xff)범위의 정수값이고, 또 읽을 수 있는 입력값이 더 이상 없음을 알릴 수 있는 값(-1)도 필요하다. 그래서 다소 크긴 하지만 정수형 중에서는 연산이 가장 효율적이고 빠른 int형 값을 반환하도록 한 것이다.

</br>

예제 15-6 / ch15 / FileCopy.java

``` java
import java.io.*;

public class FileCopy {
	public static void main(String[] args) {
		try {
			FileInputStream fis = new FileInputStream(args[0]);
			FileOutputStream fos = new FileOutputStream(args[1]);
			
			int data = 0;
			while ((data = fis.read()) != -1) {
				fos.write(data);	// void write(int b)
			}
			
			fis.close();
			fos.close();
		} catch (IOException e) {
			e.printStackTrace();
		}
	}
}
```

```
C:\jdk1.8\work\ch15>java FileCopy FileCopy.java FileCopy.bak

C:\jdk1.8\work\ch15>type FileCopy.bak
import java.io.*;

public class FileCopy {
	public static void main(String[] args) {
		try {
			FileInputStream fis = new FileInputStream(args[0]);
			FileOutputStream fos = new FileOutputStream(args[1]);
			
			int data = 0;
			while ((data = fis.read()) != -1) {
				fos.write(data);	// void write(int b)
			}
			
			fis.close();
			fos.close();
		} catch (IOException e) {
			e.printStackTrace();
		}
	}
}

C:\jdk1.8\work\ch15>
```

`FileInputStream`과 `FileOutputStream`을 사용해서 FileCopy.java파일의 내용을 그대로 FileCopy.bak로 복사하는 일을 한다.

단순히 FileCopy.java의 내용을 `read()`로 읽어서, `write(in b)`로 FileCopy.bak에 출력한다. 이처럼 텍스트파일을 다루는 경우에는 `FileInputStream`/`FileOutputStream`보다 문자기반의 스트림인 `FileReader`/`FileWriter`를 사용하는 것이 좋다.

> 기존의 파일에 새로운 내용을 추가하려면, FileOutputStream fos = new FileOutputStream(args[1], true);와 같이 생성자 두번째 매개변수의 값을 true로 해야한다.