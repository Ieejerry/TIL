Chapter 15. 입출력 I/O

# 3. 바이트기반의 보조스트림

</br>

## 3.1 FilterInputStream과 FilterOutputStream

`FilterInputStream`/`FilterOutputStream`은 `InputStream`/`OutputStream`의 자손이면서 모든 보조스트림의 조상이다. 보조스트림은 자체적으로 입출력을 수행할 수 없기 때문에 기반스트림을 필요로 한다. 다음은 `FilterInputStream`/`FilterOutputStream`의 생성자이다.

``` java
protected FilterInputStream(InputStream in)
public FilterOutputStream(OutputStream out)
```

`FilterInputStream`/`FilterOutputStream`의 모든 메소드는 단순히 기반스트림의 메소드를 그대로 호출할 뿐이다. `FilterInputStream`/`FilterOutputStream`자체로는 아무런 일도 하지 않음을 의미한다. `FilterInputStream`/`FilterOutputStream`은 상속을 통해 원하는 작업을 수행핟록 읽고 쓰는 메소드를 오버라이딩해야 한다.

``` java
public class FilterInputStream extends InputStream {
    protected volatile InputStream in;
    protected FilterInputStream(InputStream in) {
        this.in = in;
    }

    public int read() throws IOException {
        return in.read();
    }
    ...
}
```

생성자 `FilterInputStream(InputStream in)`는 접근 제어자가 `protected`이기 때문에 `FilterInputStream`의 인스턴스를 생성해서 사용할 수 없고 상속을 통해서 오버라이딩되어야 한다. `FilterInputStream`/`FilterOutputStream`을 상속받아서 기반스트림에 보조기능을 추가한 보조스트림 클래스는 다음과 같다.

> **FilterInputStream의 자손** BufferedInputStream, DataInputStream, PushbackInputStream 등   
**FilterOutputStream의 자손** BufferedOutputStream, DataOutputStream, PrintStream 등

</br>

## 3.2 BufferedInputStream과 BufferedOutputStream

`BufferedInputStream`/`BufferedOutputStream`은 스트림의 입출력 효율을 높이기 위해 버퍼를 사용하는 보조스트림이다. 한 바이트씩 입출력하는 것 보다는 버퍼(바이트배열)를 이용해서 한 번에 여러 바이트를 입출력하는 것이 빠르기 때문에 대부분의 입출력 작업에 사용된다.

![image](https://ifh.cc/g/wv0xnD.png)

`BufferedInputStream`의 버퍼크기는 입력소스로부터 한 번에 가져올 수 있는 데이터의 크기로 지정하면 좋다. 보통 입력소스가 파일인 경우 8192(8K) 정도의 크기로 하는 것이 보통이며, 버퍼의 크기를 변경해가면서 테스트하면 최적의 버퍼크기를 알아낼 수 있다.

프로그램에서 입력소스로부터 데이터를 읽기 위해 처음으로 `read`메소드를 호출하면, `BufferedInputStream`은 입력소스로 부터 버퍼 크기만큼의 데이터를 읽어다 자신의 내부 버퍼에 저장한다. 이제 프로그램에서는 `BufferedInputStream`의 버퍼에 저장된 데이터를 읽으면 되는 것이다. 외부의 입력소스로 부터 읽는 것보다 내부의 버퍼로 부터 읽는 것이 훨씬 빠르기 때문에 그만큼 작업 효율이 높아진다.

프로그램에서 버퍼에 저장된 모든 데이터를 다 읽고 그 다음 데이터를 읽기위해 `read`메소드가 호출되면, `BufferedInputStream`은 입력소스로부터 다시 버퍼크기 만큼의 데이터를 읽어다 버퍼에 저장해 놓는다. 이와 같은 작업이 계속해서 반복된다.

![image](https://ifh.cc/g/L7rxVC.png)

`BuffedOutputStream` 역시 버퍼를 이용해서 출력소스와 작업을 하게 되는데, 입력소스로부터 데이터를 읽을 때와는 반대로, 프로그램에서 `write`메소드를 이용한 출력이 `BufferedOutputStream`의 버퍼에 저장된다. 버퍼가 가득 차면, 그 때 버퍼의 모든 내용을 출력소스에 출력한다. 그리고는 버퍼를 비우고 다시 프로그램으로부터의 출력을 저장할 준비를 한다.

버퍼가 가득찼을 때만 출력소스에 출력을 하기 때문에, 마지막 출력부분이 출력소스에 쓰이지 못하고 `BufferedOutputStream`의 버퍼에 남아있는 채로 프로그램이 종료될 수 있다.

그래서 프로그램에서 모든 출력작업을 마친 후 `BufferedOutputStream`에 `close()`나 `flush()`를 호출해서 마지막에 버퍼에 있는 모든 내용이 출력소스에 출력되도록 해야 한다.

> BufferedOutputStream의 close()는 flush()를 호출하여 버퍼의 내용을 출력스트림에 쓰도록 한 후, BufferedOutputStream인스턴스의 참조변수에 null을 지정함으로써 사용하던 자원들이 반환되게 한다.

</br>

예제 15-7 / ch15 / BufferedOutputStreamEx1.java

``` java
import java.io.*;

public class BufferedOutputStreamEx1 {
	public static void main(String[] args) {
		try {
			FileOutputStream fos = new FileOutputStream("123.txt");
			// BufferedOutputStream의 버퍼 크기를 5로 한다.
			BufferedOutputStream bos = new BufferedOutputStream(fos, 5);
			// 파일 123.txt에 1 부터 9까지 출력한다.
			for(int i = '1'; i <= '9'; i++) {
				bos.write(i);
			}
			
			fos.close();
		} catch (IOException e) {
			e.printStackTrace();
		}
	}
}
```

```
C:\jdk1.8\work\ch15> java BufferedOutputStreamEx1

C:\jdk1.8\work\ch15>type 123.txt
12345
```

크기가 5인 `BufferedOutputStream`을 이용해서 파일 123.txt에 1부터 9까지 출력하는 예제인데 결과를 보면 5까지만 출력된 것을 알 수 있다. 그 이유는 버퍼에 남아있는 데이터가 출력되지 못한 상태로 프로그램이 종료되었기 때문이다.

이 예제는 `fos.close()`를 호추랳서 스트림을 닫아주기는 했지만, 이렇게 해서는 `BufferedOutputStream`의 버퍼에 있는 내용이 출력되지 않는다. `bos.close();`와 같이 해서 `BufferedOutputStream`의 `close()`를 호출해 주어야 버퍼에 남아있던 모든 내용이 출력된다. `BufferedOutputStream`의 `close()`는 기반 스트림인 `FileOutputStream`의 `close()`를 호출하기 때문에 `FileOutputStream`의 `close()`를 따로 호출해주지 않아도 된다.

아래의 코드는 `BufferedOutputStream`의 조상인 `FilterOutputStream`의 소스코드인데 `FilterOutputStream`에 정의된 `close()`는 `flush()`를 호출한 다음에 기반스트림의 `close()`를 호추하는 것을 알 수 있다. `BufferedOutputStream`는` FilterOutputStream`의 `close()`를 오버라이딩 없이 그대로 상속받는다.

``` java
public class FilterOutputStream extends OutputStream {
    protected OutputStream out;
    public FilterOutputStream(OutputStream out) {
        this.out = out;
    }
    ...
    public void close() throws IOException {
        try {
            flush();
        } catch(IOException ignored) {}
        out.close();    // 기반 스트림의 close()를 호출한다.
    }
}
```

이처럼 보조스트림을 사용한 경우에는 기반스트림의 close()나 flush()를 호출할 필요없이 단순히 보조스트림의 `close()`를 호출하기만 하면 된다.

</br>

## 3.3 DataInputStream과 DataOutputStream

`DataInputStream`/`DataOutputStream`도 각각 `FilterInputStream`/`FilterOutputStream`의 자손이며 `DataInputStream`은 `DataInput`인터페이스를, `DataOutputStream`은 `DataOutput`인터페이스를 구현하였기 때문에, 데이터를 읽고 쓰는데 있어서 byte단위가 아닌, 8가지 기본 자료형의 단위로 읽고 쓸 수 있다는 장점이 있다.

`DataOutputStream`이 출력하는 형식은 각 기본 자료형 값을 16진수로 표현하여 저장한다. 예를 들어 int값을 출력한다면, 4 byte의 16진수로 출력된다.

각 자료형의 크기가 다르므로, 출력한 데이터를 다시 읽어 올 때는 출력했을 때의 순서를 염두에 두어야 한다.

![image](https://ifh.cc/g/yvlR2b.png)

</br>

![image](https://ifh.cc/g/JtMYDp.png)

</br>

예제 15-8 / ch15 / DataOutputStreamEx1.java

``` java
import java.io.*;

public class DataOutputStreamEx1 {
	public static void main(String[] args) {
		FileOutputStream fos = null;
		DataOutputStream dos = null;
		
		try {
			fos = new FileOutputStream("sample.dat");
			dos = new DataOutputStream(fos);
			dos.writeInt(10);
			dos.writeFloat(20.0f);
			dos.writeBoolean(true);
			
			dos.close();
		} catch (IOException e) {
			e.printStackTrace();
		}
	}	// main
}
```

`FileOutputStream`을 기반으로 하는 `DataOutputStream`을 생성한 후, `DataOutputStream`의 메소드들을 이용해서 sample.dat파일에 값들을 출력했다. 이 때 출력한 값들은 이진 데이터(binary data)로 저장 된다. 문자 데이터(text data)가 아니므로 문서 편집기로 sample.dat를 열어 봐도 알 수 없는 글자들로 이루어져 있다. 파일을 16진수코드로 볼 수 있는 UltraEdit과 같은 프로그램이나 `ByteArrayOutputStream`을 사용하면 이진데이터를 확인할 수 있다.

</br>

예제 15-9 / ch15 / DataOutputStreamEx2.java

``` java
import java.io.*;
import java.util.Arrays;

public class DataOutputStreamEx2 {
	public static void main(String[] args) {
		ByteArrayOutputStream bos = null;
		DataOutputStream dos = null;
		
		byte[] result = null;
		
		try {
			bos = new ByteArrayOutputStream();
			dos = new DataOutputStream(bos);
			dos.writeInt(10);
			dos.writeFloat(20.0f);
			dos.writeBoolean(true);
			
			result = bos.toByteArray();
			
			String[] hex = new String[result.length];;
			
			for(int i = 0; i < result.length; i++) {
				if(result[i] < 0) {
					hex[i] = String.format("%02x", result[i] + 256);
				} else {
					hex[i] = String.format("%02x", result[i]);
				}
			}
			
			System.out.println("10진수 : " + Arrays.toString(result));
			System.out.println("16진수 : " + Arrays.toString(hex));
			
			dos.close();
		} catch (IOException e) {
			e.printStackTrace();
		}
	}	// main
}
```

```
10진수 : [0, 0, 0, 10, 65, -96, 0, 0, 1]
16진수 : [00, 00, 00, 0a, 41, a0, 00, 00, 01]
```

이전 예제를 변경해서 `FileOutputStream`대신 `ByteArrayOutputStream`를 사용하였다. 결과를 보면 첫 번째 4 byte인 0, 0, 0, 10는 `writeInt(10)`에 의해서 출력된 값이고, 두 번째 4 byte인 65, -96, 0, 0은 `writeFloat(20.0f)`에 의해서 출력된 것이다. 그리고 마지막 1 byte는 `writeBoolean(true)에 의해서 출력된 것이다.

![image](https://ifh.cc/g/6XKHxv.png)

위와 같이 모든 bit의 값이 1인 1 byte의 데이터가 있다고 할 때, 왼쪽에서 첫 번째 비트를 부호로 인식하지 않으면 부호 없는 1 byte가 되어 범위는 0~255이므로 이 값은 최대값인 255가 되지만, 부호로 인식하는 경우 범위는 -128~127이 되고, 이 값은 0보다 1작은 값인 -1이 된다.

결국 같은 데이터이지만 자바의 자료형인 byte의 범위가 부호 있는 1 byte 정수의 범위인 -128~127이기 때문에 -1로 인식한다는 것이다. 그래서 이 값을 0~255사이의 값으로 변환하려면 256을 더해주어야 한다.

예를 들어 -1의 경우 -1 + 256 = 255가 된다. 그리고 반대의 경우 256을 빼면 된다. 그 다음에 `String.format()`을 사용해서 10진 정수를 16진 정수로 변환하여 출력했다.

이처럼 `ByteArrayInputStream`/`ByteArrayOutputStream`을 사용하면 byte단위의 데이터 변환 및 조작이 가능하다.

> InputStream의 read()는 반환타입이 int이며 0~255의 값을 반환하므로 256을 더하거나 뺄 필요가 없다. 반면에 read(byte[] b)와 같이 byte배열을 사용하는 경우 상황에 따라 0~255범위의 값으로 변환해야할 필요가 있다.

사실 `DataOutputStream`에 의해서 어떻게 저장되는지 몰라도 `DataOutputStream`의 `write`메소드들로 기록한 데이터는 `DataInputStream`의 `read`메소드들로 읽기만 하면 된다.

이 때 한 가지 주의해야 할 것은 이 예제와 같이 여러 가지 종류의 자료형으로 출력한 경우, 읽을 때는 반드시 쓰인 순서대로 읽어야 한다는 것이다.

</br>

예제 15-10 / ch15 / DataInputStreamEx1.java

``` java
import java.io.*;

public class DataInputStreamEx1 {
	public static void main(String[] args) {
		try {
			FileInputStream fis = new FileInputStream("sample.dat");
			DataInputStream dis = new DataInputStream(fis);
			
			System.out.println(dis.readInt());
			System.out.println(dis.readFloat());
			System.out.println(dis.readBoolean());
			dis.close();
		} catch (IOException e) {
			e.printStackTrace();
		}
	}	// main
}
```

```
10
20.0
true
```

예제 15-8을 실행해서 만들어진 sample.dat를 읽어서 화면에 출력하는 예제이다. sample.dat파일로부터 데이터를 읽어올 때, 아무런 변환이나 자릿수를 셀 필요없이 단순히 `readInt()`와 같이 읽어올 데이터의 타입에 맞는 메소드를 사용하기만 하면 된다.

문자로 데이터를 저장하면, 다시 데이터를 읽어 올 때 문자들을 실제 값으로 변환하는, 예를 들면 문자열 "100"을 숫자 100으로 변환하는, 과정을 거쳐야 하고, 또 읽어야 할 데이터의 개수를 결정해야하는 번거로움이 있다.

하지만 이처럼 `DataInputStream`과 `DataOutputStream`을 사용하면, 데이터를 변환할 필요도 없고, 자리수를 세어서 따지지 않아도 되므로 편리하고 빠르게 데이터를 저장하고 읽을 수 있다.

</br>

예제 15-11 / ch15 / DataOutputStreamEx3.java

``` java
import java.io.*;

public class DataOutputStreamEx3 {
	public static void main(String[] args) {
		int[] score = { 100, 90, 95, 85, 50 };
		
		try {
			FileOutputStream fos = new FileOutputStream("score.dat");
			DataOutputStream dos = new DataOutputStream(fos);
			
			for(int i = 0; i < score.length; i++) {
				dos.writeInt(score[i]);
			}
			
			dos.close();
		} catch (IOException e) {
			e.printStackTrace();
		}
	}	// main
}
```

```
C:\jdk1.8\work\ch15>java DataOutputStreamEx3

C:\jdk1.8\work\ch15>type score.data
   d   Z   _   U   2
```

int형 배열 `score`의 값들을 `DataOutputStream`을 이용해서 score.dat파일에 출력하는 예제이다. type명령으로 score.dat의 내용을 문자로 변환해서 보여주기 때문이다. 파일에 실제 저장된 내용은 다음과 같다.

> Editplus의 편집(Edit) 메뉴에서 'Hex 뷰어'를 선택하면 파일 'score.dat'의 실제 저장된 내용을 볼 수 있다.

![image](https://ifh.cc/g/m3rzDy.png)

int의 크기가 4 byte이므로 모두 20 byte의 데이터가 저장되어 있다. 참고로 16진수 두 자리가 1 byte이다. 밑줄 아래의 숫자는 10진수로 변환한 결과이다.

다음 예제에서는 이 파일을 읽어서 데이터의 총합을 구할 것이다.

</br>

예제 15-12 / ch15 / DataInputStreamEx2.java

``` java
import java.io.*;

public class DataInputStreamEx2 {
	public static void main(String[] args) {
		int sum = 0;
		int score = 0;
		
		FileInputStream fis = null;
		DataInputStream dis = null;
		
		try {
			fis = new FileInputStream("score.dat");
			dis = new DataInputStream(fis);
			
			while(true) {
				score = dis.readInt();
				System.out.println(score);
				sum += score;
			}
		} catch (EOFException e) {
			System.out.println("점수의 총합은 " + sum + "입니다.");
		} catch (IOException ie) {
			ie.printStackTrace();
		} finally {
			try {
				if(dis != null)
					dis.close();
			} catch (IOException ie) {
				ie.printStackTrace();
			}
		}	// try
	}	// main
}
```

```
100
90
95
85
50
점수의 총합은 420입니다.
```

`DataInputStream`의 `readInt()`와 같이 데이터를 읽는 메소드는 더 이상 읽을 데이터가 없으면 `EOFException`을 발생시킨다. 그래서 다른 입력스트림과는 달리 무한반복문과 `EOFException`을 처리하는 catch문을 이용해서 데이터를 읽는다.

원래 while문으로 작업을 마친 후에 스트을 닫아 줘야 하는데, while문이 무한 반복문이기 때문에 `finally`블럭에서 스트림을 닫도록 처리하였다.

``` java
        ...
    } finally {
        try {
            if(dis != null) // dis가 null인지 확인한다.
                dis.close();    // 스트림을 닫는다.
        } catch(IOException ie) {
            ie.printStackTrace();
        }
    }   // try
        ...
```

참조변수 `dis`가 null일 때 `close()`를 호출하면 `NullPointException`이 발생하므로 if문을 사용해서 `dis`가 null인지 체크한 후에 `close()`를 호출해야 한다. 그리고 `close()`는 `IOException`을 발생시킬 수 있으므로 try-catch블럭으로 감싸주었다.

지금까지는 try블럭 내에서 스트림을 닫아주었지만, 작업도중에 예외가 발생해서 스트림을 닫지 못하고 try블럭에 빠져나갈 수 있기 때문에 이처럼 finally블럭을 이용해서 스트림을 닫아주는 것이 더 확실한 방법이다.

사실 프로그램이 종료될 때, 가비지 컬렉터가 사용하던 자원들을 모두 해제 해주기 때문에 이렇게 간단하 예제에서는 스트림을 닫지 않아도 별문제가 되지는 않는다. 그래도 가능하면 스트림을 사용한 직후에 바로 닫아서 자원을 반환하는 것이 좋다.

JDK1.7부터는 try-with-resources문을 이용해서 `close()`를 직접 호출하지 않아도 자동호출되도록 할 수 있다. 아래의 예제는 예제15-12를 try-with-resources문을 이용해서 변경한 것인데, 전보다 훨씬 간결해졌다.

</br>

예제 15-13 / ch15 / DataInputStreamEx3.java

``` java
import java.io.*;

public class DataInputStreamEx3 {
	public static void main(String[] args) {
		int sum = 0;
		int score = 0;
		
		try(FileInputStream fis = new FileInputStream("score.dat");
			DataInputStream dis = new DataInputStream(fis)) {
			
			while(true) {
				score = dis.readInt();
				System.out.println(score);
				sum += score;
			}
		} catch (EOFException e) {
			System.out.println("점수의 총합은 " + sum + "입니다.");
		} catch (IOException ie) {
			ie.printStackTrace();
		}	// try
	}	// main
}
```

</br>

## 3.4 SequenceInputStream

`SequenceInputStream`은 여러 개의 입력스트림을 연속적으로 연결해서 하나의 스트림으로부터 데이터를 읽는 것과 같이 처리할 수 있도록 도와준다. `SequenceInputStream`의 생성자를 제외하고 나머지 작업은 다른 입력스트림과 다르지 않다. 큰 파일을 여러 개의 작은 파일로 나누었다가 하나의 파일로 합치는 것과 같은 작업을 수행할 때 사용하면 좋다.

> SequenceInputStream은 다른 보조 스트림들과는 달리 FilterInputStream의 자손이 아닌 InputStream을 바로 상속 받아서 구현하였다.

![image](https://ifh.cc/g/5HGQkP.png)

`Vector`에 연결할 입력스트림들을 저장한 다음 `Vector`의 `Enumeration elements()`를 호출해서 생성자의 매개변수로 사용한다.

[사용 예1]

``` java
Vector files = new Vector();
files.add(new FileInputStream("file.001"));
files.add(new FileInputStream("file.002"));
SequenceInputStream in = new SequenceInputStream(files.elements());
```

[사용 예2]

``` java
FileInputStream file1 = new FileInputStream("file.001");
FileInputStream file2 = new FileInputStream("file.002");
SequenceInputStream in = new SequenceInputStream(file1, file2);
```

</br>

예제 15-14 / ch15 / SequenceInputStreamEx.java

``` java
import java.io.*;
import java.util.*;

public class SequenceInputStreamEx {
	public static void main(String[] args) {
		byte[] arr1 = { 0, 1, 2 };
		byte[] arr2 = { 3, 4, 5 };
		byte[] arr3 = { 6, 7, 8 };
		byte[] outSrc = null;
		
		Vector v = new Vector();
		v.add(new ByteArrayInputStream(arr1));
		v.add(new ByteArrayInputStream(arr2));
		v.add(new ByteArrayInputStream(arr3));
		
		SequenceInputStream input = new SequenceInputStream(v.elements());
		ByteArrayOutputStream output = new ByteArrayOutputStream();
		
		int data = 0;
		
		try {
			while((data = input.read()) != -1) {
				output.write(data);	// void write(int n)
			}
		} catch (IOException e) {}
		
		outSrc = output.toByteArray();
		
		System.out.println("Input Source1 : " + Arrays.toString(arr1));
		System.out.println("Input Source2 : " + Arrays.toString(arr2));
		System.out.println("Input Source3 : " + Arrays.toString(arr3));
		System.out.println("Output Source : " + Arrays.toString(outSrc));
	}
}
```

```
Input Source1 : [0, 1, 2]
Input Source2 : [3, 4, 5]
Input Source3 : [6, 7, 8]
Output Source : [0, 1, 2, 3, 4, 5, 6, 7, 8]
```

3개의 `ByteArrayInputStream`을 `Vector`와 `SequenceInputStream`을 이용해서 하나의 입력스트림처럼 다룰 수 있다. `Vector`에 저장된 순서대로 입력되므로 순서에 주의해야 한다.

</br>

## 3.5 PrintStream

`PrintStream`은 데이터를 기반스트림에 다양한 형태로 출력할 수 있는 `print`, `println`, `printf`와 같은 메소드를 오버로딩하여 제공한다.

`PrintStream`은 데이터를 적절한 문자로 출력하는 것이기 때문에 문자기반 스트림의 역할을 수행한다. 그래서 JDK1.1에서 부터 `PrintStream`보다 향상된 기능의 문자기반 스트림인 `PrintWriter`가 추가되었으나 그 동안 매우 빈번히 사용되던 `System.out`이 `PrintStream`이다 보니 둘 다 사용할 수 밖에 없게 되었다.

`PrintStream`과 `PrintWriter`는 거의 같은 기능을 가지고 있지만 `PrintWriter`가 `PrintStream`에 비해 다양한 언어의 문자를 처리하는데 적합하기 때문에 가능하면 `PrintWriter`를 사용하는 것이 좋다.

> PrintStream은 지금까지 알게 모르게 많이 사용해왔다. System클래스의 static멤버인 out과 err, 즉 System.out, System.err이 PrintStream이다.

![image](https://ifh.cc/g/H50kCZ.png)

`print()`나 `println()`을 이용해서 출력하는 중에 `PrintStream`의 기반스트림에서 IOException이 발생하면 `checkError()`를 통해서 인지할 수 있다. `println()`이나 `print()`는 예외를 던지지 않고 내부에서 처리하도록 정의하였는데, 그 이유는 `println()`과 같은 메소드가 매우 자주 사용되는 것이기 때문이다.

만일 `println()`이 예외를 던지도록 정의되었다면 `println()`을 사용하는 모든 곳에 try-catch문을 사용해야 한다.

``` java
public class PrintStream extends FileOutputStream implements Appendable, Closeable {
        ...
    private boolean trouble = false;
    public void print(int i) {
        write(String.ValueOf(i));   // write(i + "");와 같다.
    }

    private void write(String s) {
        try {
            ...
        } catch(IOException x) {
            trouble = true;
        }
    }
        ...
    public boolean checkError() {
        if(out != null) flush();
        return trouble;
    }
}
```

> i + ""와 String.ValueOf(i)는 같은 결과를 얻지만, String valueOf(i)가 더 성능이 좋다.

`printf()`는 JDK1.5부터 추가된 것으로, C언어와 같이 편리한 형식화된 출력을 지원하게 되었다. `printf()`에 사용될 수 있는 옵션은 꽤나 다양한데 그에 대한 자세한 내용은 Java API문서에서 `Formatter`클래스를 참고하면 된다. 우선 자주 사용되는 옵션들만 골라서 정리해보았다.

![image](https://ifh.cc/g/OnFgZC.png)

</br>

![image](https://ifh.cc/g/8Wzlr5.png)

</br>

![image](https://ifh.cc/g/wK2JDP.png)

</br>

![image](https://ifh.cc/g/6QKZp3.png)

</br>

![image](https://ifh.cc/g/1Pofck.png)

</br>

예제 15 -15 / ch15 / PrintStreamEx1.java

``` java
import java.util.Date;

public class PrintStreamEx1 {
	public static void main(String[] args) {
		int i = 65;
		float f = 1234.56789f;
		
		Date d = new Date();
		
		System.out.printf("문자 %c의 코드느 %d%n", i, i);
		System.out.printf("%d는 8진수로 %o, 16진수로 %x%n", i, i, i);
		System.out.printf("%3d%3d%3d\n", 100, 90, 80);
		System.out.println();
		System.out.printf("123456789012345678901234567890%n");
		System.out.printf("%s%-5s%5s%n", "123", "123", "123");
		System.out.println();
		System.out.printf("%-8.1f%8.1f %e%n", f, f, f);
		System.out.println();
		System.out.printf("오늘은 %tY년 %tm월 %td일입니다. %n", d, d, d);
		System.out.printf("지금은 %tH시 %tM분 %tS초입니다. %n", d, d, d);
		System.out.printf("지금은 %1$tH시 %1$tM분 %1$tS초입니다. %n", d);
	}
}
```

```
문자 A의 코드느 65
65는 8진수로 101, 16진수로 41
100 90 80

123456789012345678901234567890
123123    123

1234.6    1234.6 1.234568e+03

오늘은 2023년 01월 14일입니다. 
지금은 16시 25분 28초입니다. 
지금은 16시 25분 28초입니다. 
```

한 가지 덧붙여 설명할 것은 매개변수(argument)의 개수에 대한 것인데, 형식화된 문자열에 사용된 옵션의 개수와 매개변수의 개수가 일치하도록 신경 써야 한다.

``` java
System.out.printf("지금은 %tH시 %tM분 %tS초입니다. %n", d, d, d);
System.out.printf("지금은 %1$tH시 %1$tM분 %1$tS초입니다. %n", d);
```

위의 두 문장은 같은 결과를 출력하는데, 두 번째 문장의 경우 형식화된 문자열에 사용된 옵션의 개수와 매개변수의 개수가 일치하지 않는다는 것을 알 수 있다. 이처럼 '숫자$'를 옵션 앞에 붙여 줌으로써 출력된 매개변수를 지정해 줄 수 있다. 예를 들어, '1$'라면 첫 번째 매개변수를 의미한다.