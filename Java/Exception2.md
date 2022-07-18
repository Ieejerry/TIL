# 예외 2 - 예외 던지기

</br>

## 예외의 강제

API를 사용할 때 설계자의 의도에 따라서 예외를 반드시 처리해야 하는 경우가 있다.

``` java
package exception;
import java.io.*;	// 사용할 클래스들이 java.io 패키지에 들어가 있기 때문에 import 해준다.
public class CheckedExceptionDemo {
    public static void main(String[] args) {
        BufferedReader bReader = new BufferedReader(new FileReader("out.txt"));	// FileReader 클래스에 out.txt라는 텍스트 파일을 인자로 주고, 이 객체를 BufferedReader 클래스 생성자의 인자로 전달하고, 인스턴스한다.
        String input = bReader.readLine();
        System.out.println(input); 
    }
}
```

위의 코드는 `out.txt` 파일을 읽어서 그것을 화면에 출력하는 코드이다. 이 코드를 실행시키려면 `out.txt` 파일을 프로젝트의 루트 디렉토리에 위치시켜야 한다.

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/516/2066.png)

위의 코드를 컴파일해보면 아래와 같은 에러가 발생하면서 컴파일이 되지 않는다.

``` java
Exception in thread "main" java.lang.Error: Unresolved compilation problems: 
    Unhandled exception type FileNotFoundException
    Unhandled exception type IOException
 
    at org.opentutorials.javatutorials.exception.CheckedExceptionDemo.main(CheckedExceptionDemo.java:5)
```

`Unhandled exception type FileNotFoundException`

이것은 아래 로직에 대한 예외처리가 필요하다는 뜻이다.

``` java
new FileReader("out.txt")
```

`FileReader`의 생성자를 문서에서 찾아보면 아래와 같은 부분이 있다.

![image](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/516/2067.png)

Throws는 한국어로는 '던지다'로 번역된다. 위의 내용은 생성자 `FileReader`의 인자 `fileName`의 값에 해당하는 파일이 디렉토리이거나 어떤 이유로 사용할 수 없다면 `FileNotFoundException`을 발생시킨다는 의미다.

이것은 `FileReader`의 생성자가 동작할 때 파일을 열 수 없는 경우가 생길 수 있고, 이런 경우 생성자 `FileReader`에서는 이 문제를 처리할 수 없기 때문에 이에 대한 처리를 생성자의 사용자에게 위임하겠다는 의미다. 그것을 던진다(throw)고 표현하고 있다. 따라서 API의 사용자 쪽에서는 예외에 대한 처리를 반드시 해야 한다는 의미다. 따라서 아래와 같이 해야 `FileReader` 클래스를 사용할 수 있다.

``` java
package exception;
import java.io.*;   // 사용할 클래스들이 java.io 패키지에 들어가 있기 때문에 import 해준다.
public class CheckedExceptionDemo {
    public static void main(String[] args) {
        try {   // FileNotFoundException로 인해 발생하는 에러를 예외 처리해준다.
            BufferedReader bReader = new BufferedReader(new FileReader("out.txt")); // FileReader 클래스에 out.txt라는 텍스트 파일을 인자로 주고, 이 객체를 BufferedReader 클래스 생성자의 인자로 전달하고, 인스턴스한다.
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        }
        String input = bReader.readLine();
        System.out.println(input); 
    }
}
```

`BufferedReader` 클래스의 `readLine` 메소드는 `IOException`을 발생시킬 수 있다.

``` java
package exception;
import java.io.*;   // 사용할 클래스들이 java.io 패키지에 들어가 있기 때문에 import 해준다.
public class CheckedExceptionDemo {
    public static void main(String[] args) {
        try {   // FileNotFoundException로 인해 발생하는 에러를 예외 처리해준다.
            BufferedReader bReader = new BufferedReader(new FileReader("out.txt")); // FileReader 클래스에 out.txt라는 텍스트 파일을 인자로 주고, 이 객체를 BufferedReader 클래스 생성자의 인자로 전달하고, 인스턴스한다.
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        }
        try{    // IOException로 인해 발생하는 에러를 예외처리 해준다.
            String input = bReader.readLine();
        } catch (IOException e){
            e.printStackTrace();
        }       
        System.out.println(input); 
    }
}
```

그런데 위의 코드는 컴파일되지 않는다. 여기에는 함정이 있는데 변수 `bReader`를 보면, 이 변수는 `try`의 중괄호 안에서 선언되어 있다. 그리고 이 변수는 11행에서 사용되는데 `bReader`가 선언된 6행과 사용될 11행은 서로 다른 중괄호이다. 따라서 11행에서는 6행에서 선언된 `bReader`에 접근할 수 없다.

``` java
package exception;
import java.io.*;	// 사용할 클래스들이 java.io 패키지에 들어가 있기 때문에 import 해준다.
public class CheckedExceptionDemo {
    public static void main(String[] args) {
    	BufferedReader bReader = null;	// bReader를 전역변수로 선언 및 null 할당
        String input = null;	// input 전역변수 선언 및 null 할당

		try {   // FileNotFoundException로 인해 발생하는 에러를 예외 처리해준다.
			bReader = new BufferedReader(new FileReader("out.txt"));    // FileReader 클래스에 out.txt라는 텍스트 파일을 인자로 주고, 이 객체를 BufferedReader 클래스 생성자의 인자로 전달하고, 인스턴스한다.
		} catch (FileNotFoundException e) {
			e.printStackTrace();
		}
		try {   // IOException로 인해 발생하는 에러를 예외처리 해준다.
			input = bReader.readLine();
		} catch (IOException e) {
			e.printStackTrace();
		}
        System.out.println(input); 
    }
}
```

</br>

## throw와 throws

지금까지 예외를 처리하는 방법으로 `try`...`catch`...`finally`를 알아보았다. 이외에 다른 방법도 있다.  `throw`를 사용하는 것이다. `throw`는 예외처리를 다음 사용자에게 넘기는 것이다.

``` java
package exception;
 
class B{
    void run(){	// run() 메소드 정의
    }
}
class C{
    void run(){	// run() 메소드 정의
        B b = new B();	// 클래스 B를 변수 b로 인스턴스함
        b.run();	// 인스턴스 b에서 run() 메소드 호출
    }
}
public class ThrowExceptionDemo {
    public static void main(String[] args) {
         C c = new C();	// 클래스 C를 변수 c로 인스턴스함
         c.run();	// 인스턴스 c에서 run() 메소드 호출
    }   
}

// 클래스 B로 부터 클래스 C는 사용자이고, 클래스 C로부터 클래스 ThrowExceptionDemo는 사용자이다. 그리고 클래스 ThrowExceptionDemo 사용자는 애플리케이션 사용자(End User)이다.
// B => C => ThrowExceptionDemo => End-User
```

`ThrowExceptionDemo.main`(클래스 `ThrowExceptionDemo`의 메소드 `main`)은 `C.run`의 사용자이다. `C.run`은 `B.run`의 사용자이다. 반대로 `B.run`의 다음 사용자는 `C.run`이고 `C.run`의 다음 사용자는 `ThrowExceptionDemo.main`이 되는 셈이다.

``` java
package exception;

import java.io.*;

class B{
    void run(){	// run() 메소드 정의
    	BufferedReader bReader = null;	// bReader를 전역변수로 선언 및 null 할당
        String input = null;	// input 전역변수 선언 및 null 할당

		try {   // FileNotFoundException로 인해 발생하는 에러를 예외 처리해준다.
			bReader = new BufferedReader(new FileReader("out.txt"));    // FileReader 클래스에 out.txt라는 텍스트 파일을 인자로 주고, 이 객체를 BufferedReader 클래스 생성자의 인자로 전달하고, 인스턴스한다.
		} catch (FileNotFoundException e) {
			e.printStackTrace();
		}
		try {   // IOException로 인해 발생하는 에러를 예외처리 해준다.
			input = bReader.readLine();
		} catch (IOException e) {
			e.printStackTrace();
		}
        System.out.println(input); 
    }
}
class C{
    void run(){	// run() 메소드 정의
        B b = new B();	// 클래스 B를 변수 b로 인스턴스함
        b.run();	// 인스턴스 b에서 run() 메소드 호출
    }
}
public class ThrowExceptionDemo {
    public static void main(String[] args) {
         C c = new C();	// 클래스 C를 변수 c로 인스턴스함
         c.run();	// 인스턴스 c에서 run() 메소드 호출
    }   
}

// 클래스 B로 부터 클래스 C는 사용자이고, 클래스 C로부터 클래스 ThrowExceptionDemo는 사용자이다. 그리고 클래스 ThrowExceptionDemo 사용자는 애플리케이션 사용자(End User)이다.
// B => C => ThrowExceptionDemo => End-User
```

위의 코드는 `B.run`이 `FileReader`의 생성자와 `BufferedReader.readLine`가 던진 예외를 `try`...`catch`로 처리한다. 즉 `B.run`이 예외에 대한 책임을 지고 있다.

그런데 `B.run`이 예외 처리를 직접 하지 않고 다음 사용자 `C.run`에게 넘길 수 있다.

``` java
package exception;

import java.io.*;

class B{
    void run() throws IOException, FileNotFoundException{	// run() 메소드 정의 및 IOException, FileNotFoundException 예외처리를 다음 사용자에게 강제
    	BufferedReader bReader = null;	// bReader를 전역변수로 선언 및 null 할당
        String input = null;	// input 전역변수 선언 및 null 할당

		bReader = new BufferedReader(new FileReader("out.txt"));    // FileReader 클래스에 out.txt라는 텍스트 파일을 인자로 주고, 이 객체를 BufferedReader 클래스 생성자의 인자로 전달하고, 인스턴스한다.
		input = bReader.readLine();
		System.out.println(input); 
    }
}
class C{
    void run(){	// run() 메소드 정의
        B b = new B();	// 클래스 B를 변수 b로 인스턴스함
        b.run();	// 인스턴스 b에서 run() 메소드 호출
    }
}
public class ThrowExceptionDemo {
    public static void main(String[] args) {
         C c = new C();	// 클래스 C를 변수 c로 인스턴스함
         c.run();	// 인스턴스 c에서 run() 메소드 호출
    }   
}

// 클래스 B로 부터 클래스 C는 사용자이고, 클래스 C로부터 클래스 ThrowExceptionDemo는 사용자이다. 그리고 클래스 ThrowExceptionDemo 사용자는 애플리케이션 사용자(End User)이다.
// B => C => ThrowExceptionDemo => End-User
```

`B` 내부의 `try`...`catch` 구문은 제거되었고 `run` 옆에 `throws IOException, FileNotFoundException`이 추가되었다. 이것은 `B.run` 내부에서 `IOException, FileNotFoundException`에 해당하는 예외가 발생하면 이에 대한 처리를 `B.run`의 사용자에게 위임하는 것이다. 위의 코드에서 `B.run`의 사용자는 `C.run`이다. 따라서 `C.run`은 아래와 같이 수정돼야 한다.

``` java
package exception;

import java.io.*;

class B{
    void run() throws IOException, FileNotFoundException{	// run() 메소드 정의 및 IOException, FileNotFoundException 예외처리를 다음 사용자에게 강제
    	BufferedReader bReader = null;	// bReader를 전역변수로 선언 및 null 할당
        String input = null;	// input 전역변수 선언 및 null 할당

		bReader = new BufferedReader(new FileReader("out.txt"));    // FileReader 클래스에 out.txt라는 텍스트 파일을 인자로 주고, 이 객체를 BufferedReader 클래스 생성자의 인자로 전달하고, 인스턴스한다.
		input = bReader.readLine();
		System.out.println(input); 
    }
}
class C{
    void run(){	// run() 메소드 정의
        B b = new B();	// 클래스 B를 변수 b로 인스턴스함
        try {
            b.run();
        } catch (FileNotFoundException e) {	// FileNotFoundException 예외처리
            e.printStackTrace();
        } catch (IOException e) {	// IOException 예외처리
            e.printStackTrace();
        }
    }
}
public class ThrowExceptionDemo {
    public static void main(String[] args) {
         C c = new C();	// 클래스 C를 변수 c로 인스턴스함
         c.run();	// 인스턴스 c에서 run() 메소드 호출
    }   
}

// 클래스 B로 부터 클래스 C는 사용자이고, 클래스 C로부터 클래스 ThrowExceptionDemo는 사용자이다. 그리고 클래스 ThrowExceptionDemo 사용자는 애플리케이션 사용자(End User)이다.
// B => C => ThrowExceptionDemo => End-User
```

이 책임을 다시 main에게 넘겨보겠다.

``` java
package exception;

import java.io.*;

class B{
    void run() throws IOException, FileNotFoundException{	// run() 메소드 정의 및 IOException, FileNotFoundException 예외처리를 다음 사용자에게 강제
    	BufferedReader bReader = null;	// bReader를 전역변수로 선언 및 null 할당
        String input = null;	// input 전역변수 선언 및 null 할당

		bReader = new BufferedReader(new FileReader("out.txt"));    // FileReader 클래스에 out.txt라는 텍스트 파일을 인자로 주고, 이 객체를 BufferedReader 클래스 생성자의 인자로 전달하고, 인스턴스한다.
		input = bReader.readLine();
		System.out.println(input); 
    }
}
class C{
    void run() throws IOException, FileNotFoundException{	// run() 메소드 정의 및 IOException, FileNotFoundException 예외처리를 다음 사용자에게 강제
        B b = new B();	// 클래스 B를 변수 b로 인스턴스함
        b.run();
    }
}
public class ThrowExceptionDemo {
    public static void main(String[] args) {
         C c = new C();	// 클래스 C를 변수 c로 인스턴스함
         try {
             c.run();
         } catch (FileNotFoundException e) {	// FileNotFoundException 예외처리
        	 System.out.println("out.txt 파일은 설정 파일 입니다. 이 파일이 프로잭트 루트 디렉토리에 존재해야 합니다.");
         } catch (IOException e) {	// IOException 예외처리
             e.printStackTrace();
         }
    }   
}

// 클래스 B로 부터 클래스 C는 사용자이고, 클래스 C로부터 클래스 ThrowExceptionDemo는 사용자이다. 그리고 클래스 ThrowExceptionDemo 사용자는 애플리케이션 사용자(End User)이다.
// B => C => ThrowExceptionDemo => End-User
```

`out.txt` 파일을 찾을 수 없는 상황은 `B.run` 입장에서는 어떻게 할 수 있는 일이 아니다. 엔드유저인 애플리케이션의 사용자가 `out.txt` 파일을 루트 디렉토리에 위치시켜야 하는 문제이기 때문에 애플리케이션의 진입점인 메소드 `main`으로 책임을 넘기고 있다.

예외는 API를 사용하면서 발생할 수 있는 잠재적 위협에 대한 API 개발자의 강력한 암시다. 이 암시를 무시해서는 안 된다.