Chapter 15. 입출력 I/O

# 4. 문자기반 스트림

문자데이터를 다루는데 사용된다는 것을 제외하고는 바이트기반 스트림과 문자기반 스트림의 사용방법은 거의 같다.

</br>

## 4.1 Reader와 Writer

바이트기반 스트림의 조상이 `InputStream`/`OutputStream`인 것과 같이 문자기반의 스트림에서는 `Reader`/`Writer`가 그와 같은 역할을 한다. 다음은 `Reader`/`Writer`의 메소드인데 byte배열 대신 char배열을 사용한다는 것 외에는 `InputStream`/`OutputStream`의 메소드와 다르지 않다.

![image](https://ifh.cc/g/LzofPc.png)

</br>

![image](https://ifh.cc/g/gNkDZ3.png)

문자기반 스트림이라는 것이 단순히 2 byte로 스트림을 처리하는 것만을 의미하지는 않는다. 문자 데이터를 다루는데 필요한 또 하나의 정보는 인코딩(encoding)이다.

문자기반 스트림, 즉 `Reader`/`Writer` 그리고 그 자손들은 여러 종류의 인코딩과 자바에서 사용하는 유니코드(UTF-16)간의 변환을 자동적으로 처리해준다. `Reader`는 특정 인코딩을 읽어서 유니코드로 변환하고 `Writer`는 유니코드를 특정 인코딩으로 변환하여 저장한다.

</br>

## 4.2 FileReader와 FileWriter

`FileReader`/`FileWrite`는 파일로부터 텍스트데이터를 읽고, 파일에 쓰는데 사용된다. 사용방법은 `FileInputStream`/`FileOutputStream`과 다르지 않다.

</br>

예제 15-16 / ch15 / FileReaderEx1.java

``` java
import java.io.*;

public class FileReaderEx1 {
	public static void main(String[] args) {
		try {
			String fileName = "test.txt";
			FileInputStream fis = new FileInputStream(fileName);
			FileReader fr = new FileReader(fileName);
			
			int data = 0;
			// FileInputStream을 이용해서 파일내용을 읽어 화면에 출력한다.
			while((data = fis.read()) != -1) {
				System.out.print((char)data);
			}
			System.out.println();
			fis.close();
			
			// FileReader를 이용해서 파일내용을 읽어 화면에 출력한다.
			while((data = fr.read()) != -1) {
				System.out.print((char)data);
			}
			System.out.println();
			fr.close();
		} catch (IOException e) {
			e.printStackTrace();
		}
	}	// main
}
```

```
C:\jdk1.8\work\ch15>type test.txt
Hello, 안녕하세요?

C:\jdk1.8\work\ch15>java FileReaderEx1
Hello, ìëíì¸ì?
Hello, 안녕하세요?
```

이 예제는 바이트기반 스트림인 `FileInputStream`과 문자기반 스트림인 `FileReader`의 차이점을 보여 주기 위한 것으로 같은 내용의 파일(test.txt)을 한번은 `FileInputStream`으로 다른 한번은 `FileReader`로 읽어서 화면에 출력했다. `FileInputStream`을 사용했을 때는 한글이 깨져서 출력된다.

</br>

예제 15-17 / ch15 / FileConversion.java

``` java
import java.io.*;

public class FileConversion {
	public static void main(String[] args) {
		try {
			FileReader fr = new FileReader(args[0]);
			FileWriter fw = new FileWriter(args[1]);
			
			int data = 0;
			while ((data = fr.read()) != -1) {
				if(data != '\t' && data != '\n' && data != ' ' && data != '\r')
					fw.write(data);
			}
			
			fr.close();
			fw.close();
		} catch (IOException e) {
			e.printStackTrace();
		}
	}	// main
}
```

```
C:\jdk1.8\work\ch15>java FileConversion FileConversion.java convert.txt

C:\jdk1.8\work\ch15>type convert.txt
importjava.io.*;publicclassFileConversion{publicstaticvoidmain(String[]args){try{FileReaderfr=newFileReader("src\\FileConversion.java");FileWriterfw=newFileWriter(args[1]);intdata=0;while((data=fr.read())!=-1){if(data!='\t'&&data!='\n'&&data!=''&&data!='\r')fw.write(data);}fr.close();fw.close();}catch(IOExceptione){e.printStackTrace();}}//main}
```

파일의 공백을 모두 없애는 예제인데 입력스트림으로부터 읽은 데이터를 변환해서 출력스트림에 쓰는 작업의 예를 보여 주기 위한 것이다.

</br>

## 4.3 PipedReader와 PipedWriter

`PipedReader`/`PipedWriter`는 쓰레드 간에 데이터를 주고 받을 때 사용된다. 다른 스트림과는 달리 입력과 출력스트림을 하나의 스트림으로 연결(connect)해서 데이터를 주고받는다는 특징이 있다.

스트림을 생성한 다음에 어느 한쪽 쓰레드에서 `connect()`를 호출해서 입력스트림과 출력스트림을 연결한다. 입출력을 마친 후에는 어느 한쪽 스트림만 닫아도 나머지 스트림은 자동으로 닫힌다. 이 점을 제외하고는 일반 입출력방법과 다르지 않다.

</br>

예제 15-18 / ch15 / PipedReaderWriter.java

``` java
import java.io.*;

public class PipedReaderWriter {
	public static void main(String[] args) {
		InputThread inThread = new InputThread("InputThread");
		OutputThread outThread = new OutputThread("Output Thread");
		
		// PipedReader와 PipedWriter을 연결한다.
		inThread.connect(outThread.getOutput());
		
		inThread.start();
		outThread.start();
	}	// main
}

class InputThread extends Thread {
	PipedReader input = new PipedReader();
	StringWriter sw = new StringWriter();
	
	InputThread(String name) {
		super(name);	// Thread(String name);
	}
	
	public void run() {
		try {
			int data = 0;
			
			while((data = input.read()) != -1) {
				sw.write(data);
			}
			System.out.println(getName() + " received : " + sw.toString());
		} catch (IOException e) {}
	}	// run
	
	public PipedReader getInput() {
		return input;
	}
	
	public void connect(PipedWriter output) {
		try {
			input.connect(output);
		} catch (IOException e) {}
	}	// connect
}

class OutputThread extends Thread {
	PipedWriter output = new PipedWriter();
	
	OutputThread(String name) {
		super(name);	// Thread(String name);
	}
	
	public void run() {
		try {
			String msg = "Hello";
			System.out.println(getName() + " sent : " + msg);
			output.write(msg);
			output.close();
		} catch (IOException e) {}
	}	// run
	
	public PipedWriter getOutput() {
		return output;
	}
	
	public void connect(PipedReader input) {
		try {
			output.connect(input);
		} catch (IOException e) {}
	}	// connect
}
```

```
Output Thread sent : Hello
InputThread received : Hello
```

두 쓰레드가 `PipedReader`/`PipedWriter`를 이용해서 서로 메세지를 주고받는 예제이다. 쓰레드를 시작하기 전에 `PipedReader`와 `PipedWriter`를 연결해야 한다.

`StringWriter`는 `CharArrayWriter`처럼 메모리를 사용하는 스트림인데 내부적으로 `StringBuffer`를 가지고 있어서 출력하는 내용이 여기에 저장된다.

</br>

## 4.4 StringReader와 StringWriter

`StringReader`/`StringWriter`는 `CharArrayReader`/`CharArrayWriter`와 같이 입출력 대상이 메모리인 스트림이다. `StringWriter`에 출력되는 데이터는 내부의 `StringBuffer`에 저장되며 `StringWriter`의 다음과 같은 메소드를 이용해서 저장된 데이터를 얻을 수 있다.

> **StringBuffer getBuffer()** StringWriter에 출력한 데이터가 저장된 StringBuffer를 반환한다.   
**String toString()** StringWriter에 출력된 (StringBuffer에 저장된) 문자열을 반환한다.

근본적으로는 String도 char배열이지만, 아무래도 char배열보다는 String으로 처리하는 것이 여러모로 편리한 경우가 더 많다.

</br>

예제 15-19 / ch15 / StringReaderWriterEx.java

``` java
import java.io.*;

public class StringReaderWriterEx {
	public static void main(String[] args) {
		String inputData = "ABCD";
		StringReader input = new StringReader(inputData);
		StringWriter output = new StringWriter();
		
		int data = 0;
		
		try {
			while((data = input.read()) != -1) {
				output.write(data);	// void write(int b)
			}
		} catch (IOException e) {}
		
		System.out.println("Input Data : " + inputData);
		System.out.println("Output Data : " + output.toString());
//		System.out.println("Output Data : " + output.getBuffer().toString());
	}
}
```

```
Input Data : ABCD
Output Data : ABCD
```