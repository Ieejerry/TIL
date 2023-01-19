Chapter 15. 입출력 I/O

# 6. 표준입출력과 File

</br>

## 6.1 표준입출력 - System.in, System.out, System.err

표준입출력은 콘솔(console, 도스창)을 통한 데이터 입력과 콘솔로의 데이터 출력을 의미한다. 자바에서는 표준 입출력(standard I/O)을 위해 3가지 입출력 슽릠, `System.in`, `System.out`, `System.err`을 제공하는데, 이 들은 자바 애플리케이션의 실행과 동시에 사용할 수 있게 자동적으로 생성되기 때문에 개발자가 별도로 스트림을 생성하는 코드를 작성하지 않고도 사용이 가능하다.

> **System.in** 콘솔로부터 데이터를 입력받는데 사용   
**System.out** 콘솔로 데이터를 출력하는데 사용   
**System.err** 콘솔로 데이터를 출력하는데 사용

`System`클래스의 소스에서 알 수 있듯이 `in`, `out`, `err`은 `System`클래스에 선언된 클래스변수(static변수)이다. 선언부분만을 봐서는 `out`, `in`, `err`의 타입은 `InputStream`과 `PrintStream`이지만 실제로는 버퍼를 이용하는 `BufferedInputStream`과 `BufferedOutputStream`의 인스턴스를 사용한다.

``` java
public final class System {
    public final static InputStream in = nullInputStream();
    public final static PrintStream out = nullPrintStream();
    public final static PrintStream err = nullPrintStream();
    ...
}
```

> Editplus나 이클립스와 같은 에디터에서는 콘솔로의 출력을 중간에 가로채서 에디터에 뿌려 주는 것이다. Editplus의 설정화면에서 'Capture Output'옵션을 선택하면 콘솔에 출력하는 내용이 Editplus의 하단에 출력된다.

</br>

예제 15-22 / ch15 / StandardIOEx1.java

``` java
import java.io.*;

public class StandardIOEx1 {
	public static void main(String[] args) {
		try {
			int input = 0;
			
			while ((input = System.in.read()) != -1) {
				System.out.println(("input : " + input + ", (char)input : " + (char)input));
			}
		} catch (IOException e) {
			e.printStackTrace();
		}
	}	// main
}
```

```
hello
input : 104, (char)input : h
input : 101, (char)input : e
input : 108, (char)input : l
input : 108, (char)input : l
input : 111, (char)input : o
input : 13, (char)input :           ← 특수문자라서 화면에 보이지 않는다.
input : 10, (char)input :
                                    ← 개행문자가 출력되어 줄바꿈 되었다.
^Z
```

화면에 커서가 입력을 기다리고 있는데, hello라고 입력하고 '^Z(Ctrl키와 z키를 동시에 누름)를 누르거나 Enter를 누르면, 입력한 문자들이 출력되고 프로그램이 종료된다.

예제를 실행하여 `System.in.read()`가 호출되면, 코드의 진행을 멈추고 콘솔에 커서가 깜빡이며 사용자의 입력을 기다린다.

``` java
while((input = System.in.read()) != -1) {
```

콘솔입력은 버퍼를 가지고 있기 때문에 BackSpace키를 이용해서 편집이 가능하며 한 번에 버퍼의 크기만큼 입력이 가능하다. 그래서 Enter키나 입력의 끝을 알리는 '^z'를 누르기 전까지는 아직 데이터가 입력 중인 것으로 간주되어 커서가 입력을 계속 기다리는 상태(블락킹 상태)에 머무르게 된다.

콘솔에 데이터를 입력하고 Enter키를 누르면 입력대기상태에서 벗어나 입력된 데이터를 읽기 시작하고 입력된 데이터를 모두 읽으면 다시 입력대기 상태가 된다.

이러한 과정이 반복되다가 사용자가 '^z'를 입력하면, `read()`는 입력이 종료되었음을 인식하고 -1을 반환하여 while문을 벗어나 프로그램이 종료된다.

> 윈도우에서 '^z', 유닉스와 메킨토시에서는 '^d'를 누르는 것이 스트림의 끝을 의미한다. 윈도우의 콘솔은 한 번에 최대 255자까지만 입력이 가능하다.

Enter키를 누른 것은 두 개의 특수문자 '\r'과 '\n'이 입력된 것으로 간주된다. '\r'은 캐리지리턴(carriage return), 즉 커서를 현재 라인의 첫 번째 칼럼으로 이동시키고 '\n'은 커서를 다음 줄로 이동시키는 줄바꿈(new line)을 한다.

그래서 Enter키를 누르면, 캐리지리턴과 줄바꿈이 수행되어 다음 줄의 첫 버내 칼럼으로 커서가 이동한다.

여기서 한 가지 문제는 Enter키도 사용자입력으로 간주되어 매 입력마다 '\r'과 '\n'이 붙기 때문에 이 들을 제거해주어야 하는 불편함이 있다. 이러한 불편함을 제거하려면 `System.in`에 `BufferedReader`를 이용해서 `readLine()`을 통해 라인단위로 데이터를 입력받으면 된다.

</br>

## 6.2 표준입출력의 대상변경 - setOut(), setErr(), setIn()

초기에는 `System.in`, `System.out`, `System.err`의 입출력대상이 콘솔화면이지만, `setIn()`, `setOut()`, `setErr()`를 사용하면 입출력을 콘솔 이외에 다른 입출력 대상으로 변경하는 것이 가능하다.

![image](https://ifh.cc/g/Zpvy8f.png)

그러나 JDK1.5부터 `Scanner`클래스가 제공되면서 `System.in`으로부터 데이터를 입력받아 작업하는 것이 편리해졌다.

</br>

예제 15-23 / ch15 / StandardIOEx2.java

``` java
public class StrandardIOEx2 {
	public static void main(String[] args) {
		System.out.println("out : Hello world!");
		System.err.println("err : Hello world!");
	}
}
```

```
err : Hello world!
out : Hello world!
```

`System.out`, `System.err` 모두 출력대상이 콘솔이기 때문에 `System.out`대신 `System.err`을 사용해도 같은 결과를 얻는다.

</br>

예제 15-24 / ch15 / StandardIOEx3.java

``` java
import java.io.*;

public class StandardIOEx3 {
	public static void main(String[] args) {
		PrintStream ps = null;
		FileOutputStream fos = null;
		
		try {
			fos = new FileOutputStream("test.txt");
			ps = new PrintStream(fos);
			System.setOut(ps);	// System.out의 출력대상을 test.txt파일로 변경
		} catch (FileNotFoundException e) {
			System.out.println("File not found");
		}
		
		System.out.println("Hello by System.out");
		System.out.println("Hello by System.err");
	}
}
```

```
C:\jdk1.8\work\ch15>java StandardIOEx3
Hello by System.err

C:\jdk1.8\work\ch15>type test.txt
Hello by System.out

C:\jdk1.8\work\ch15>
```

`System.out`의 출력소스에 test.txt파일로 변경하였기 때문에 `System.out`을 이용한 출력은 모두 test.txt파일에 저장된다. 그래서 실행결과에는 `System.err`를 이용한 출력만 나타난다.

`setOut()`과 같은 메소드를 사용하는 방법 외에도 커맨드라인에서 표준입출력의 대상을 간단히 바꿀수 있는 다음과 같은 방법이 있다.

```
C:\jdk1.8\work\ch15>java StandardIOEx2
out : Hello world!
err : Hello world!
```

StandardIOEx2의 `System.out`출력을 콘솔이 아닌 output.txt로 저장한다. 즉, `System.out`에 출력하는 것은 output.txt에 저장된다. 기존에 output.txt파일이 있었다면 기존의 내용은 삭제된다.

```
C:\jdk1.8\work\ch15>java StandardIOEx2 > output.txt
err : Hello world!

C:\jdk1.8\work\ch15>type output.txt
out : Hello world!
```

StandardIOEx2의 `System.out`출력을 output.txt에 저장한다. '>'를 사용했을 때와는 달리 '>>'는 기존 내용의 마지막에 새로운 내용이 추가된다.

```
C:\jdk1.8\work\ch15>java StandardIOEx2 >> output.txt
err : Hello world!

C:\jdk1.8\work\ch15>type output.txt
out : Hello world!
out : Hello world!
```

StandardIOEx2의 표준입력을 output.txt로 지정한다. 즉, 콘솔이 아닌 output.txt로부터 데이터를 입력받는다.

```
C:\jdk1.8\work\ch15>java StandardIOEx2 < output.txt
out : Hello world!
out : Hello world!
```

</br>

## 6.3 RandomAccessFile

자바에서는 입력과 출력이 각각 분리되어 별도로 작업을 하도록 설계되어 있는데, `RandomAccessFile`만은 하나의 클래스로 파일에 대한 입력과 출력을 모두 할 수 있도록 되어 있다. `InputStream`이나 `OutputStream`으로부터 상속받지 않고, `DataInput`인터페이스와 `DataOutput`인터페이스를 모두 구현했기 때문에 읽기와 쓰기가 모두 가능하다.

사실 `DataInputStream`은 `DataInput`인터페이스를, `DataOutputStram`은 `DataOutput`인터페이스를 구현했다. 이 두 클래스의 기본 자료형(primitive data type)을 읽고 쓰기 위한 메소드들은 모두 이 2개의 인터페이스에 정의되어있는 것들이다.

따라서, `RandomAccessFile`클래스도 `DataInputStream`과 `DataOutputStream`처럼, 기본자료형 단위로 데이터를 읽고 쓸 수 있다.

그래도 역시 `RandomAccessFile`클래스의 가장 큰 장점은 파일의 어느 위치에나 읽기/쓰기가 가능하다는 것이다. 다른 입출력 클래스들은 입출력소스에 순차적으로 읽기/쓰기를 하기 때문에 읽기와 쓰기가 제한적인데 반해서 `RandomAccessFile`클래스는 파일에 읽고 쓰는 위치에 제한이 없다.

이것을 가능하게 하기 위해서 내부적으로 파일 포인터를 사용하는데, 입출력 시에 작업이 수행되는 곳이 바로 파일 포인터가 위치한 곳이 된다.

파일 포인터의 위치는 파일의 제일 첫 부분(0부터 시작)이며, 읽기 또는 쓰기를 수행할 때마다 작어빙 수행된 다음 위치로 이동하게 된다. 순차적으로 읽기와 쓰기를 한다면, 파일 포인터를 이동시키기 위해 별도의 작업이 필요하지 않지만, 파일의 임의의 위치에 있는 내용에 대해서 작업하고자 한다면, 먼저 파일 포인터를 원하는 위치로 옮긴 다음 작업을 해야 한다.

현재 작업 중인 파일에서 파일 포인터의 위치를 알고 싶을 때는 `getFilePointer()`를 사용하면 되고, 파일 포인터의 위치를 옮기기 위해서는 `seek(long pos)`나 `skipBytes(int n)`를 사용하면 된다.

> 사실 모든 입출력에 사용되는 클래스들은 입출력 시 다음 작업이 이루어질 위치를 저장하고 있는 포인터를 내부적으로 갖고 있다. 다만 내부적으로만 사용될 수 있기 때문에 작업자가 포인터의 위치를 마음대로 변경할 수 없다는 것이 `RandomAccessFile`과 다른 점이다.

![image](https://ifh.cc/g/7Shvkl.png)

> RandomAccessFile의 인스터스를 "rw" mode로 생성할 때, 지정된 파일이 없으면 새로운 파일을 생성한다.

</br>

예제 15-25 / ch15 / RandomAccessFileEx1.java

``` java
import java.io.*;

public class RandomAccessFileEx1 {
	public static void main(String[] args) {
		try {
			RandomAccessFile raf = new RandomAccessFile("test.dat", "rw");
			System.out.println("파일 포인터의 위치 : " + raf.getFilePointer());
			raf.writeInt(100);
			System.out.println("파일 포인터의 위치 : " + raf.getFilePointer());
			raf.writeLong(100L);
			System.out.println("파일 포인터의 위치 : " + raf.getFilePointer());
		} catch (IOException e) {
			e.printStackTrace();
		}
	}
}
```

```
파일 포인터의 위치 : 0
파일 포인터의 위치 : 4
파일 포인터의 위치 : 12
```

이 예제는 파일에 출력작업이 수행되었을 때 파일 포인터의 위치가 어떻게 달라지는 지에 대해서 보여 준다. int가 4 byte이기 때문에 `writeInt()`를 호출한 다음 파일 포인터의 위치가 0에서 5로 바뀐 것을 알 수 있다. 마찬가지로 8 byte인 long을 출력하는 `writeLong()`을 호출한 후에는 파일 포인터의 위치가 4에서 12로 변경된 것을 알 수 있다.

</br>

예제 15-26 / ch15 / RandomAccessFileEx2.java

``` java
import java.io.*;

public class RandomAccessFileEx2 {
	public static void main(String[] args) {
//					   번호, 국어, 영어, 수학
		int[] score = { 1, 100,  90,  90,
						2,  70,  90, 100,
						3, 100, 100, 100,
						4,  70,  60,  80,
						5,  70,  90, 100
		};
		
		try {
			RandomAccessFile raf = new RandomAccessFile("score2.dat", "rw");
			for(int i = 0; i < score.length; i++) {
				raf.writeInt(score[i]);
			}
			
			while (true) {
				System.out.println(raf.readInt());
			}
		} catch (EOFException e) {
			// readInt()를 호출했을 때 더 이상 읽을 내용이 없으면 EOFException이 발생한다.
		} catch (IOException e) {
			e.printStackTrace();
		}
	}
}
```

이 예제는 int배열 `score`에 저장된 데이터를 score2.dat에 저장한 다음, 저장된 내용을 `readInt()`로 읽어서 출력하도록 한 것이다. 그러나 score2.dat파일은 생성되지만 화면에는 아무 것도 출력되지 않는다.

그 이유는 `writeInt()`를 수행하면서 파일 포인터의 위치가 파일의 마지막으로 이동되었기 때문이다. 그 다음에 `readInt()`를 호출했으므로 파일의 앞부분이 아닌 마지막부분부터 읽기 시작하기 때문에 아무 것도 읽지 못하고 EOFException이 발생해서 무한반복문을 벗어나게 된다.

그래서 다음과 같이 `seek(long pos)`를 이용해서 파일포인터의 위치를 다시 처음으로 이동시킨 다음에 `readInt()`를 호출하도록 해야 한다.

![image](https://ifh.cc/g/fSYkjs.png)

이처럼 `RandomAccessFile`을 'rw(읽기쓰기)모드'로 생성해서 작업할 때는 이러한 점을 염두에 두어야 한다.

</br>

예제 15-27 / ch15 / RandomAccessFileEx3.java

``` java
import java.io.*;

public class RandomAccessFileEx3 {
	public static void main(String[] args) {
		int sum = 0;
		
		try {
			RandomAccessFile raf = new RandomAccessFile("score2.dat", "r");
			int i = 4;
			
			while(true) {
				raf.seek(i);
				sum += raf.readInt();
				i += 16;
			}
		} catch (EOFException e) {
			System.out.println("sum : " + sum);
		} catch (IOException e) {
			e.printStackTrace();
		}
	}
}
```

```
sum : 410
```

이전 예제에서 데이터를 저장한 score2.dat파일에서 국어과목의 점수만을 합계를 내는 예제이다. 한 학생의 데이터가 번호와 3과목의 점수로 모두 4개의 int값(4 * 4 = 16 byte)으로 되어있기 때문에 i += 16과 같이 파일 포인터의 값을 16씩 증가시키면서 `readInt()`를 호출했다.

</br>

## 6.4 File

자바에서는 `File`클래스를 통해서 파일과 디렉토리를 다룰 수 있도록 하고 있다. 그래서 `File`인스턴스는 파일 일 수도 있고 디렉토리일 수도 있다.

![image](https://ifh.cc/g/HrCtnC.png)

</br>

![image](https://ifh.cc/g/A8McTt.png)

파일의 경로(path)와 디렉토리나 파일의 이름을 구분하는 데 사용되는 구분자가 OS마다 다를 수 있기 때문에, OS독립적으로 프로그램을 작성하기 위해서는 반드시 위의 멤버변수들을 이용해야 한다. 만일 윈도우에서 사용하는 구분자를 코드에 직접 적어 놓았다면, 이 코드는 다른 OS에서는 오류를 일으킬 수 있다.

</br>

예제 15-28 / ch15 / FileEx1.java

``` java
import java.io.*;

public class FileEx1 {
	public static void main(String[] args) throws IOException {
		File f = new File("C:\\Users\\iksrnd\\git\\Java_jungsuk_example\\ch15_ex\\src\\FileEx1.java");
		String fileName = f.getName();
		int pos = fileName.lastIndexOf(".");
		
		System.out.println("경로를 제외한 파일이름 - " + f.getName());
		System.out.println("확장자를 제외한 파일이름 - " + fileName.substring(0, pos));
		System.out.println("확장자 - " + fileName.substring(pos + 1));
		
		System.out.println("경로를 포함한 파일이름 - " + f.getPath());
		System.out.println("파일의 절대경로 - " + f.getAbsolutePath());
		System.out.println("파일의 정규경로 - " + f.getCanonicalPath());
		System.out.println("파일이 속해 있는 디렉토리 - " + f.getParent());
		System.out.println();
		System.out.println("File.pathSeparator - " + File.pathSeparator);
		System.out.println("File.pathSeparatorChar - " + File.pathSeparatorChar);
		System.out.println("File.separator - " + File.separator);
		System.out.println("File.separatorChar - " + File.separatorChar);
		System.out.println();
		System.out.println("user.dir = " + System.getProperty("user.dir"));
		System.out.println("sun.boot.class.path = " + System.getProperty("sun.boot.class.path"));
	}
}
```

```
경로를 제외한 파일이름 - FileEx1.java
확장자를 제외한 파일이름 - FileEx1
확장자 - java
경로를 포함한 파일이름 - C:\Users\iksrnd\git\Java_jungsuk_example\ch15_ex\src\FileEx1.java
파일의 절대경로 - C:\Users\iksrnd\git\Java_jungsuk_example\ch15_ex\src\FileEx1.java
파일의 정규경로 - C:\Users\iksrnd\git\Java_jungsuk_example\ch15_ex\src\FileEx1.java
파일이 속해 있는 디렉토리 - C:\Users\iksrnd\git\Java_jungsuk_example\ch15_ex\src

File.pathSeparator - ;
File.pathSeparatorChar - ;
File.separator - \
File.separatorChar - \

user.dir = C:\Users\iksrnd\git\Java_jungsuk_example\ch15_ex
sun.boot.class.path = null
```

`File`인스턴스를 생성하고 메소드를 이용해서 파일의 경로와 구분자 등의 정보를 출력하는 예제이다.

절대경로(absolute path)는 파일시스템의 루트(root)로부터 시작하는 파일의 전체 경로를 의미한다. OS에 따라 다르지만, 하나의 파일에 대해 둘 이상의 절대경로가 존재할 수 있다. 현재 디렉토리를 의미하는 '.'와 같은 기호나 링크를 포함하고 있는 경우가 이에 해당한다. 그러나 정규경로(canonical path)는 기호나 링크 등을 포함하지 않는 유일한 경로를 의미한다.

예를 들어, 'C:\Users\iksrnd\git\Java_jungsuk_example\ch15_ex\src\FileEx1.java'의 또 다른 절대경로는 'C:\Users\iksrnd\git\Java_jungsuk_example\ch15_ex\src\.\FileEx1.java'가 있지만, 정규경로는 'C:\Users\iksrnd\git\Java_jungsuk_example\ch15_ex\src\FileEx1.java' 단 하나 뿐이다.

시스템속성 중에서 user.dir의 값을 확인하면 현재 프로그램이 실행 중인 디렉토리를 알 수 있다. 그리고 우리가 OS의 시스템변수로 설정하는 classpath외에 sun.boot.class.path라는 시스템속성에 기본적이 classpath가 있어서 기본적인 경로들은 이미 설정되어 있다. 그래서 처음에 JDK설치 후 classpath를 따로 지정해주지 않아도 되는 것이다.

예제에서 사용된 `File f = new File("C:\\Users\\iksrnd\\git\\Java_jungsuk_example\\ch15_ex\\src\\FileEx1.java");`대신 다른 생성자를 사용해서 `File`인스턴스를 생성할 수 있다.

```
File f = new File("C:\\Users\\iksrnd\\git\\Java_jungsuk_example\\ch15_ex\\src", "FileEx1.java");
    또는
File dir = new File("C:\\Users\\iksrnd\\git\\Java_jungsuk_example\\ch15_ex\\src");
File f = new File(dir, "FileEx1.java");
```

한 가지 더 알아두어야 할 것은 `File`인스턴스를 생성했다고 해서 파일이나 디렉토리가 생성되는 것은 아니라는 것이다. 파일명이나 디렉토리명으로 지정된 문자열이 유효하지 않더라도 컴파일 에러나 예외를 발생시키지 않는다.

새로운 파일을 생성하기 위해서는 `File`인스턴스를 생성한 다음, 출력스트림을 생성하거나 `createNewFile()`을 호출해야한다.

```
1. 이미 존재하는 파일을 참조할 때 :
File f = new File("C:\\Users\\iksrnd\\git\\Java_jungsuk_example\\ch15_ex\\src", "FileEx1.java");

2. 기존에 없는 파일을 새로 생성할 때 :
File f = new File("C:\\Users\\iksrnd\\git\\Java_jungsuk_example\\ch15_ex\\src", "NewFile.java");
f.createNewFile();  // 새로운 파일이 생성된다.
```

![image](https://ifh.cc/g/YSBmj3.png)

</br>

예제 15-29 / ch15 / FileEx2.java

``` java
import java.io.*;

public class FileEx2 {
	public static void main(String[] args) {
		if(args.length != 1) {
			System.out.println("USAGE : java FileEx2 DIRECTORY");
			System.exit(0);
		}
		
		File f = new File(args[0]);
		
		if(!f.exists() || !f.isDirectory()) {
			System.out.println("유효하지 않은 디렉토리입니다.");
			System.exit(0);
		}
		
		File[] files = f.listFiles();
		
		for(int i = 0; i < files.length; i++) {
			String fileName = files[i].getName();
			System.out.println(files[i].isDirectory() ? "[" + fileName + "]" : fileName);
		}
	}	// main
}
```

```
C:\Users\iksrnd\git\Java_jungsuk_example\ch15_ex\src>java FileEx2
USAGE : java FileEx2 DIRECTORY

C:\Users\iksrnd\git\Java_jungsuk_example\ch15_ex\src>java FileEx2 git
유효하지 않은 디렉토리입니다.

C:\Users\iksrnd\git\Java_jungsuk_example\ch15_ex\src>java FileEx2 C:\Users
[Administrator]
[All Users]
[Default]
[Default User]
[DESKTOP-OTCFE5N]
desktop.ini
[iksrnd]
[Public]
```

지정한 디렉토리(폴더)에 포함된 파일과 디렉토리의 목록을 보여주는 예제이다.

</br>

예제 15-30 / ch15 / FileEx3.java

``` java
import java.io.*;
import java.util.ArrayList;

public class FileEx3 {
	static int totalFiles = 0;
	static int totalDirs = 0;
	
	public static void main(String[] args) {
		if(args.length != 1) {
			System.out.println("USAGE : java FileEx3 DIRECTORY");
			System.exit(0);
		}
		
		File dir = new File(args[0]);
		
		if(!dir.exists() || !dir.isDirectory()) {
			System.out.println("유효하지 않은 디렉토리입니다.");
			System.exit(0);
		}
		
		printFileList(dir);
		
		System.out.println();
		System.out.println("총 " + totalFiles + "개의 파일");
		System.out.println("총 " + totalDirs + "개의 디렉토리");
	}
	
	public static void printFileList(File dir) {
		System.out.println(dir.getAbsolutePath() + " 디렉토리");
		File[] files = dir.listFiles();
		
		ArrayList subDir = new ArrayList();
		
		for(int i = 0; i < files.length; i++) {
			String filename = files[i].getName();
			
			if(files[i].isDirectory()) {
				filename = "[" + filename + "]";
				subDir.add(i + "");
			}
			System.out.println(filename);
		}
		
		int dirNum = subDir.size();
		int fileNum = files.length - dirNum;
		
		totalFiles += fileNum;
		totalDirs += dirNum;
		
		System.out.println(fileNum + "개의 파일, " + dirNum + "개의 디렉토리");
		System.out.println();
		
		for(int i = 0; i < subDir.size(); i++) {
			int index = Integer.parseInt((String)subDir.get(i));
			printFileList(files[index]);
		}
	}	// printFileList
}
```

```
C:\Users\iksrnd\git\Java_jungsuk_example\ch15_ex\src 디렉토리
BufferedOutputStreamEx1.java
BufferedReaderEx1.java
DataInputStreamEx1.java
DataInputStreamEx2.java
DataInputStreamEx3.java
DataOutputStreamEx1.java
DataOutputStreamEx2.java
DataOutputStreamEx3.java
FileConversion.java
FileCopy.java
FileEx1.java
FileEx2.java
FileEx3.java
FileReaderEx1.java
FileViewer.java
InputStreamReaderEx.java
IOEx1.java
IOEx2.java
IOEx3.java
IOEx4.java
PipedReaderWriter.java
PrintStreamEx1.java
RandomAccessFileEx1.java
RandomAccessFileEx2.java
RandomAccessFileEx3.java
SequenceInputStreamEx.java
StandardIOEx1.java
StandardIOEx3.java
StrandardIOEx2.java
StringReaderWriterEx.java
30개의 파일, 0개의 디렉토리


총 30개의 파일
총 0개의 디렉토리
```

이전 예제를 발전시켜서 서브디렉토리와 그에 포함된 파일과 디렉토리의 목록까지 보내주도록 하였다.

`printFileList(File dir)`는 디렉토리에 포함된 파일과 디렉토리의 목록을 출력하는 메소드인데 재귀호출을 이용하였다.

``` java
ArrayList subDir = new ArrayList();
		
for(int i = 0; i < files.length; i++) {
    String filename = files[i].getName();
    
    if(files[i].isDirectory()) {
        filename = "[" + filename + "]";
        subDir.add(i + "");
    }
    System.out.println(filename);
}
```

먼저 파일의 목록을 출력하고 디렉토리인 경우 ArrayList에 담았다가 각 디렉토리에 대해 `printFileList(File dir)`를 재귀호출한다.

``` java
for(int i = 0; i < subDir.size(); i++) {
    int index = Integer.parseInt((String)subDir.get(i));
    printFileList(files[index]);
}
```

사실 ArrayList에 담지 않고 재귀호출만을 이용해도 처리가 가능하나 보다 정돈된 형태로 출력하기 위해서 이렇게 하였다.

</br>

예제 15-31 / ch15 / FileEx4.java

``` java
import java.io.*;
import java.text.SimpleDateFormat;
import java.util.Date;

public class FileEx4 {
	public static void main(String[] args) {
		String currDir = System.getProperty("user.dir");
		File dir = new File(currDir);
		
		File[] files = dir.listFiles();
		
		for(int i = 0; i < files.length; i++) {
			File f = files[i];
			String name = f.getName();
			SimpleDateFormat df = new SimpleDateFormat("yyyy-MM-dd HH:mma");
			String attribute = "";
			String size = "";
			
			if(files[i].isDirectory()) {
				attribute = "DIR";
			} else {
				size = f.length() + "";
				attribute = f.canRead() ? "R" : " ";
				attribute += f.canWrite() ? "W" : " ";
				attribute += f.isHidden() ? "H" : " ";
			}
			
			System.out.printf("%s %3s %6s %s\n", df.format(new Date(f.lastModified())), attribute, size, name);
		}
 	}
}	// end of class
```

```
2023-01-13 19:32오후 RW     397 .classpath
2023-01-13 19:32오후 RW       6 .gitignore
2023-01-13 19:32오후 RW     383 .project
2023-01-13 19:32오후 DIR        .settings
2023-01-14 13:22오후 RW       5 123.txt
2023-01-15 15:37오후 DIR        bin
2023-01-14 23:22오후 RW     346 convert.txt
2023-01-14 14:04오후 RW       9 sample.dat
2023-01-14 14:53오후 RW      20 score.dat
2023-01-15 14:04오후 RW      80 score2.dat
2023-01-15 15:37오후 DIR        src
2023-01-15 13:48오후 RW      12 test.dat
2023-01-15 13:48오후 RW      21 test.txt
```

현재 디렉토리에 속한 파일과 디렉토리의 이름과 크기 등 상세정보를 보여주는 예제이다.

</br>

예제 15-32 / ch15 / FileEx5.java

``` java
import java.io.*;
import java.text.SimpleDateFormat;
import java.util.*;

public class FileEx5 {
	public static void main(String[] args) {
		if(args.length != 1 || args[0].length() != 1 || "tTlLnN".indexOf(args[0]) == -1) {
			System.out.println("USAGE : java FileEx5 SORT_OPTION");
			System.out.println("SORT_OPTION : ");
			System.out.println("t Time ascending sort.");
			System.out.println("T Time ascending sort.");
			System.out.println("l Length ascending sort.");
			System.out.println("L Length ascending sort.");
			System.out.println("n Name ascending sort.");
			System.out.println("N Name ascending sort.");
			System.exit(0);
		}
		
		final char option = args[0].charAt(0);
		
		String currDir = System.getProperty("user.dir");
		File dir = new File(currDir);
		File[] files = dir.listFiles();
		
		Comparator comp = new Comparator() {
			public int compare(Object o1, Object o2) {
				long time1 = ((File)o1).lastModified();
				long time2 = ((File)o2).lastModified();
				
				long length1 = ((File)o1).length();
				long length2 = ((File)o2).length();
				
				String name1 = ((File)o1).getName().toLowerCase();
				String name2 = ((File)o2).getName().toLowerCase();
				
				int result = 0;
				
				switch (option) {
					case 't':
						if(time1 - time2 > 0) result = 1;
						else if(time1 - time2 == 0) result = 0;
						else if(time1 - time2 < 0) result = -1; 
						break;
					case 'T':
						if(time1 - time2 > 0) result = -1;
						else if(time1 - time2 == 0) result = 0;
						else if(time1 - time2 < 0) result = 1; 
						break;
					case 'l':
						if(length1 - length2 > 0) result = 1;
						else if(length1 - length2 == 0) result = 0;
						else if(length1 - length2 < 0) result = -1; 
						break;
					case 'L':
						if(length1 - length2 > 0) result = -1;
						else if(length1 - length2 == 0) result = 0;
						else if(length1 - length2 < 0) result = 1; 
						break;
					case 'n':
						result = name1.compareTo(name2);
						break;
					case 'N':
						result = name2.compareTo(name1);
						break;
				}
				return result;
			}	// compare
			
			public boolean equals(Object o) { return false; }	// not used.
		}; // end of Comparator
		
		Arrays.sort(files, comp);
		
		for(int i = 0; i < files.length; i++) {
			File f = files[i];
			String name = f.getName();
			SimpleDateFormat df = new SimpleDateFormat("yyyy-MM-dd HH:mm");
			String attribute = "";
			String size = "";
			
			if(files[i].isDirectory()) {
				attribute = "DIR";
			} else {
				size = f.length() + "";
				attribute = f.canRead() ? "R" : " ";
				attribute += f.canWrite() ? "W" : " ";
				attribute += f.isHidden() ? "H" : " ";
			}
			
			System.out.printf("%s %3s %6s %s\n", df.format(new Date(f.lastModified())), attribute, size, name);
		}	// for
	}	// main
}	// end of class
```

```
C:\Users\iksrnd\git\Java_jungsuk_example\ch15_ex\src>java FileEx5
USAGE : java FileEx5 SORT_OPTION
SORT_OPTION : 
t Time ascending sort.
T Time ascending sort.
l Length ascending sort.
L Length ascending sort.
n Name ascending sort.
N Name ascending sort.

C:\Users\iksrnd\git\Java_jungsuk_example\ch15_ex\src>java FileEx5 T
2023-01-15 16:10 DIR        bin
2023-01-15 15:54 DIR        src
2023-01-15 14:04 RW      80 score2.dat
2023-01-15 13:48 RW      12 test.dat
2023-01-15 13:48 RW      21 test.txt
2023-01-14 23:22 RW     346 convert.txt
2023-01-14 14:53 RW      20 score.dat
2023-01-14 14:04 RW       9 sample.dat
2023-01-14 13:22 RW       5 123.txt
2023-01-13 19:32 RW       6 .gitignore
2023-01-13 19:32 RW     397 .classpath
2023-01-13 19:32 DIR        .settings
2023-01-13 19:32 RW     383 .project

C:\Users\iksrnd\git\Java_jungsuk_example\ch15_ex\src>java FileEx5 L
2023-01-15 16:10 DIR        bin
2023-01-15 15:54 DIR        src
2023-01-13 19:32 RW     397 .classpath
2023-01-13 19:32 RW     383 .project
2023-01-14 23:22 RW     346 convert.txt
2023-01-15 14:04 RW      80 score2.dat
2023-01-15 13:48 RW      21 test.txt
2023-01-14 14:53 RW      20 score.dat
2023-01-15 13:48 RW      12 test.dat
2023-01-14 14:04 RW       9 sample.dat
2023-01-13 19:32 RW       6 .gitignore
2023-01-14 13:22 RW       5 123.txt
2023-01-13 19:32 DIR        .settings
```

이전의 파일의 속성을 보여 주는 예제에 정렬기능을 추가한 예제이다. 시간이나 파일크기, 이름으로 오름차순 또는 내림차순으로 파일목록을 정렬하여 볼 수 있다.

</br>

예제 15-33 / ch15 / FileEx6.java

``` java
import java.io.*;

public class FileEx6 {
	static int found = 0;
	
	public static void main(String[] args) {
		if(args.length != 2) {
			System.out.println("USAGE : java FileEx6 DIRECTORY KEYWORD");
			System.exit(0);
		}
		
		File dir = new File(args[0]);
		String keyword = args[1];
		
		if(!dir.exists() || !dir.isDirectory()) {
			System.out.println("유효하지 않은 디렉토리입니다.");
			System.exit(0);
		}
		
		try {
			findInFiles(dir, keyword);
		} catch (IOException e) {
			e.printStackTrace();
		}
		
		System.out.println();
		System.out.println("총 " + found + "개의 라인에서 '" + keyword + "'을/를 발견하였습니다. ");
	}
	
	public static void findInFiles(File dir, String keyword) throws IOException {
		File[] files = dir.listFiles();
		
		for(int i = 0; i < files.length; i++) {
			if(files[i].isDirectory()) {
				findInFiles(files[i], keyword);
			} else {
				String filename = files[i].getName();
				String extension = filename.substring(filename.lastIndexOf(".") + 1);
				extension = "," + extension + ",";
				
				if(",java,txt,bak".indexOf(extension) == -1) continue;
				
				filename = dir.getAbsolutePath() + File.separator + filename;
				
				FileReader fr = new FileReader(files[i]);
				BufferedReader br = new BufferedReader(fr);
				
				String data = "";
				int lineNum = 0;
				
				while((data = br.readLine()) != null) {
					lineNum++;
					
					if(data.indexOf(keyword) != -1) {
						found++;
						System.out.println("[" + filename + "(" + lineNum + ")" + "]" + data);
					}
				}	// while
				
				br.close();
			}
		}	// for
	}	// findInFiles
}	// class
```

```
[C:\Users\iksrnd\git\Java_jungsuk_example\ch15_ex\src\FileEx2.java(7)]			System.exit(0);
[C:\Users\iksrnd\git\Java_jungsuk_example\ch15_ex\src\FileEx2.java(14)]			System.exit(0);
[C:\Users\iksrnd\git\Java_jungsuk_example\ch15_ex\src\FileEx3.java(11)]			System.exit(0);
[C:\Users\iksrnd\git\Java_jungsuk_example\ch15_ex\src\FileEx3.java(18)]			System.exit(0);
[C:\Users\iksrnd\git\Java_jungsuk_example\ch15_ex\src\FileEx5.java(16)]			System.exit(0);
[C:\Users\iksrnd\git\Java_jungsuk_example\ch15_ex\src\FileEx6.java(9)]			System.exit(0);
[C:\Users\iksrnd\git\Java_jungsuk_example\ch15_ex\src\FileEx6.java(17)]			System.exit(0);

총 7개의 라인에서 'exit'을/를 발견하였습니다. 
```

이 전의 디렉토리에 포함된 파일의 목록 및 서브디렉토리의 목록을 출력한 것과 같이 재귀호출을 이용해서 지정한 디렉토리와 서브디렉토리에 포함된, 확장자가 'java', 'txt', 'bak'인 모든 파일의 내용을 읽어서 지정한 키워드가 포함된 라인을 출력하는 예제이다.

파일의 내용을 라인단위로 읽기 위해서 `BufferedReader`의 `readLine()`을 이용하였다.

``` java
extension = "," + extension + ",";
if(",java,txt,bak".indexOf(extension) == -1) continue;
```

구분자를 ','로 하여 확장자를 붙여서 문자열을 만든 다음, `indexOf()`를 이용해서 이 문자열에 확장자가 포함되었는지 확인하고 없으면 넘어가도록 되어 있다. 확장자(extension)의 뒤쪽이나 앞쪽에만 구분자를 붙이면 'ava'와 같이 부분적으로 일치하는 경우에 문제가 생긴다.

</br>

예제 15-34 / ch15 / FileEx7.java

``` java
import java.io.*;

public class FileEx7 {
	public static void main(String[] args) {
		if(args.length != 1) {
			System.out.println("USAGE : java FileEx7 pattern");
			System.exit(0);
		}
		
		String currDir = System.getProperty("user.dir");
		
		File dir = new File(currDir);
		final String pattern = args[0];
		
		// String[] list (FilenameFilter filer)
		String[] files = dir.list(new FilenameFilter() {
			public boolean accept(File dir, String name) {
				return name.indexOf(pattern) != -1;
			}
		});
		
		for(int i = 0; i < files.length; i++) {
			System.out.println(files[i]);
		}
	}	// end of main
}	// end of class
```

```
FileEx1.java
FileEx2.java
FileEx3.java
FileEx4.java
FileEx5.java
FileEx6.java
FileEx7.java
RandomAccessFileEx1.java
RandomAccessFileEx2.java
RandomAccessFileEx3.java
```

`FilenameFilter`를 구현해서 `String[] list(FilenameFilter filter)`와 함께 사용해서 특정 조건에 맞는 파일의 목록을 얻는 방법을 보여주는 예제이다.

`FilenameFilter`의 내용은 다음과 같이 `accept`메소드 하나만 선언되어 있으며 이 메소드만 구현해 주면 된다.

``` java
public interface FilenameFilter {
    boolean accept(File dir, String name);
}
```

</br>

예제 15-35 / ch15 / FileEx8.java

``` java
import java.io.*;

public class FileEx8 {
	static int deletedFiles = 0;
	
	public static void main(String[] args) {
		if(args.length != 1) {
			System.out.println("USAGE : java FileEx8 Extension");
			System.exit(0);
		}
		
		String currDir = System.getProperty("user.dir");
		
		File dir = new File(currDir);
		String ext = "." + args[0];
		
		delete(dir, ext);
		System.out.println(deletedFiles + "개의 파일이 삭제되었습니다.");
	}	// end of main
	
	public static void delete(File dir, String ext) {
		File[] files = dir.listFiles();
		
		for(int i = 0; i < files.length; i++) {
			if(files[i].isDirectory()) {
				delete(files[i], ext);
			} else {
				String filename = files[i].getAbsolutePath();
				
				if(filename.endsWith(ext)) {
					System.out.print(filename);
					if(files[i].delete()) {
						System.out.println(" - 삭제 성공");
						deletedFiles++;
					} else {
						System.out.println(" - 삭제 실패");
					}
				}
			}	// if(files[i].isDirectory()) { 
		}	// for
	}	// end of delete
}
```

```
C:\Users\iksrnd\git\Java_jungsuk_example\ch15_ex\java.bak - 삭제 성공
C:\Users\iksrnd\git\Java_jungsuk_example\ch15_ex\src\java.bak - 삭제 성공
2개의 파일이 삭제되었습니다.
```

이 예제 역시 재귀호출을 이용해서 지정된 디렉토리와 하위 디렉토리에 있는 파일 중에서 지정된 확장자를 가진 파일을 `delete()`를 호출해서 삭제한다. `delete()`는 해당 파일을 삭제하는데 성공하면 true를 실패하면 false를 반환한다.

</br>

예제 15-36 / ch15 / FileEx9.java

``` java
import java.io.*;

public class FileEx9 {
	public static void main(String[] args) {
		if(args.length != 1) {
			System.out.println("Usage : java FileEx9 DIRECTORY");
			System.exit(0);
		}
		
		File dir = new File(args[0]);
		
		if(!dir.exists() || !dir.isDirectory()) {
			System.out.println("유효하지 않은 디렉토리입니다.");
			System.exit(0);
		}
		
		File[] list = dir.listFiles();
		
		for(int i = 0; i < list.length; i++) {
			String fileName = list[i].getName();
			// 파일명
			String newFileName = "0000" + fileName;
			newFileName = newFileName.substring(newFileName.length() - 7);
			list[i].renameTo(new File(dir, newFileName));
		}
	}	// end of main
}
```

`renameTo(File f)`를 이용해서 파일의 이름을 바꾸는 간단한 예제이다. 여기서는 파일명이 숫자로 되어 있을 때 앞에 '0000'을 붙인 다음 `substring()`으로 이름의 길이를 맞춰 주는 내용으로 작성하였다.

파일이름이 '1.jpg', '2.jpg'와 같이 숫자로 되어 있는 경우, 파일이름으로 정렬을 하면 '1.jpg' 다음에 '2.jpg'가 아닌 '11.jpg'가 오게 된다. 이것을 바로 잡기위해 파일 이름 앞에 '0000'을 붙이면, 파일이름으로 정렬하였을 때 '00001.jpg'다음에 '00002.jpg'가 온다.

</br>

예제 15-37 / ch15 / FileSplit.java

``` java
import java.io.*;

public class FileSplit {
	public static void main(String[] args) {
		if(args.length < 2) {
			System.out.println("USAGE : java FileSplit filename SIZE_KB");
			System.exit(0);	// 프로그램을 종료한다.
		}
		
		final int VOLUME = Integer.parseInt(args[1]) * 1000;
		
		try {
			String filename = args[0];
			FileInputStream fis = new FileInputStream(filename);
			BufferedInputStream bis = new BufferedInputStream(fis);
			
			FileOutputStream fos = null;
			BufferedOutputStream bos = null;
			
			int data = 0;
			int i = 0;
			int number = 0;
			
			while((data = bis.read()) != -1) {
				if(i % VOLUME == 0) {
					if(i != 0) {
						bos.close();
					}
					
					fos = new FileOutputStream(filename + "_." + ++number);
					bos = new BufferedOutputStream(fos);
				}
				bos.write(data);
				i++;
			}
			
			bis.close();
			bos.close();
		} catch (IOException e) {
			e.printStackTrace();
		}
	}	// end of main
}
```

```
C:\Users\iksrnd\git\Java_jungsuk_example\ch15_ex>java FileSplit temp.dat 1000

C:\Users\iksrnd\git\Java_jungsuk_example\ch15_ex>dir temp.dat*
 C 드라이브 볼륨 : Windows
 볼륨 일련 번호 : 99CB-48D9

 C:\Users\iksrnd\git\Java_jungsuk_example\ch15_ex 디렉토리

2023-01-15 오후 16:03           4,881,080 tmep.dat
2023-01-15 오후 17:17           1,000,000 tmep.dat_.1
2023-01-15 오후 17:17           1,000,000 tmep.dat_.2
2023-01-15 오후 17:17           1,000,000 tmep.dat_.3
2023-01-15 오후 17:17           1,000,000 tmep.dat_.4
2023-01-15 오후 17:17           881,080 tmep.dat_.5
             6개 파일           9,762,160 바이트
             0개 디렉토리  146,579,038,208 바이트 남음
```

지정한 파일을 지정한 크기로 잘라서 여러 개의 파일로 만드는 예제이다.

</br>

예제 15-38 / ch15 / FileMerge.java

``` java
import java.io.*;

public class FIleMerge {
	public static void main(String[] args) {
		if(args.length != 1) {
			System.out.println("USAGE : java FileMerge filename");
			System.exit(0);
		}
		
		String mergeFilename = args[0];
		
		try {
			
			File tempFile = File.createTempFile("~mergetmp", ".tmp");
			tempFile.deleteOnExit();
			
			FileOutputStream fos = new FileOutputStream(tempFile);
			BufferedOutputStream bos = new BufferedOutputStream(fos);
			
			BufferedInputStream bis = null;
			
			int number = 1;
			
			File f = new File(mergeFilename + "_." + number);
			
			while(f.exists()) {
				f.setReadOnly();	// 작업중에 파일의 내용이 변경되지 않도록 한다.
				bis = new BufferedInputStream(new FileInputStream(f));
				
				int data = 0;
				while((data = bis.read()) != -1) {
					bos.write(data);
				}
				
				bis.close();
				
				f = new File(mergeFilename + "_." + ++number);
			}	// while
			
			bos.close();
			
			File oldFile = new File(mergeFilename);
			if(oldFile.exists())
				oldFile.delete();
			tempFile.renameTo(oldFile);
		} catch (IOException e) {}
	}	// main
}	// class
```

이전 예제에서 나눈 파일을 다시 합치는 예제이다. 작업할 임시파일을 새로 만들고 프로그램 종료시 자동 삭제 되도록 했다. 프로그램의 실행도중에 사용자에 의해 중단되거나 했을 때, 파일이 합쳐지는 과정에서 생성된 불완전한 파일이 생성되는 것을 막기 위해서 임시파일을 사용하는 것이다.

파일을 합치는 작업을 온전히 마치고 나면, 기존 파일을 삭제하고 임시파일의 이름을 기존 파일의 이름으로 변경한다.

``` java
File tempFile = File.createTempFile("~mergetmp", ".tmp");
tempFile.deleteOnExit();
```

임시파일이 생성되는 곳은 `createTempFile`메소드에서 지정할 수도 있지만, 지정하지 않으면, 시스템 속성인 'java.io.tmpdir'에 지정된 디렉토리가 된다.

> System.getProperty("java.io.tmpdir")를 출력해보면 임시 디렉토리의 위치를 확인할 수 있다.

``` java
File oldFile = new File(mergeFilename);
if(oldFile.exists()) oldFile.delete();
tempFile.renameTo(oldFile);
```

작업을 마치고 나면 기존 파일을 삭제하고 임시파일의 이름을 기존 파일의 이름으로 변경한다.