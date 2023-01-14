Chapter 15. 입출력 I/O

# 1. 자바에서의 입출력

</br>

## 1.1 입출력이란?

I/O란 Input과 Output의 약자로 입력과 출력, 간단히 줄여서 입출력이라고 한다. 입출력은 컴퓨터 내부 또는 외부의 장치와 프로그램간의 데이터를 주고 받는 것을 말한다.

</br>

## 1.2 스트림(stream)

자바에서 입출력을 수행하려면, 즉 어느 한쪽에서 다른 쪽으로 데이터를 전달하려면, 두 대상을 연결하고 데이터를 전송할 수 있는 무언가가 필요한데 이것을 스트림(stream)이라고 정의했다. 입출력에서의 스트림은 14장의 스트림과 같은 용어를 쓰지만 다른 개념이다.

> 스트림은 TV와 DVD를 연결하는 입력선과 출력선과 같은 역할을 한다.

> 스트림이란 데이터를 운반하는데 사용되는 연결통로이다.

스트림은 연속적인 데이터의 흐름을 물에 비유해서 붙여진 이름인데, 여러 가지로 유사한 점이 많다. 물이 한쪽 방향으로만 흐르는 것과 같이 스트림은 단방향통신만 가능하기 때문에 하나의 스트림으로 입력과 출력을 동시에 처리할 수 없다.

그래서 입력과 출력을 동시에 수행하려면 입력을 위한 입력스트림(input stream)과 출력을 위한 출력스트림(output stream), 모두 2개의 스트림이 필요하다.

스트림은 먼저 보낸 데이터를 먼저 받게 되어 있으며 중간에 건너뜀 없이 연속적으로 데이터를 주고 받는다. 큐(queue)와 같은 FIFO(First In First Out)구조로 되어 있다고 생각하면 된다.

</br>

## 1.3 바이트기반 스트림 - InputStream, OutputStream

스트림은 바이트단위로 데이터를 전송하며 입출력 대상에 따라 다음과 같은 입출력스트림이 있다.

![image](https://ifh.cc/g/694zjA.png)

어떠한 대상에 대해서 작업을 할 것인지 그리고 입력을 할 것인지 출력을 할 것인지에 따라서 해당 스트림을 선택해서 사용하면 된다. 예를 들어 어떤 파일의 내용을 읽고자 하는 경우 `FileInputStream`을 사용하면 된다.

이들은 모두 `InputStream` 또는 `OutputStream`의 자손들이며, 각각 읽고 쓰는데 필요한 추상메소드를 자신에 맞게 구현해 놓았다.

자바에서는 `java.io`패키지를 통해서 많은 종류의 입출력관련 클래스들을 제공하고 있으며, 입출력을 처리할 수 있는 표준화된 방법을 제공함으로써 입출력의 대상이 달라져도 동일한 방법으로 입출력이 가능하다.

![image](https://ifh.cc/g/YYv2Kc.png)

`InputStream`의 `read()`와 `OutputStream`의 `write(int b)`는 입출력의 대상에 따라 읽고 쓰는 방법이 다를 것이기 때문에 각 상황에 알맞게 구현하라는 의미에서 추상메소드로 정의되어 있다.

`read()`와 `write(int b)`를 제외한 나머지 메소드들은 추상메소드가 아니니까 굳이 추상메소드인 `read()`와 `write(int b)`를 구현하지 않아도 이들을 사용하면 될 것이라고 생각할 수 있겠지만 사실 추상메소드인 `read()`와 `write(int b)`를 이용해서 구현한 것들이기 때문에 `read()`와 `write(int b)`가 구현되지 있지 않으면 이들은 아무런 의미가 없다.

``` java
public abstract class InputStream {
    ...
    // 입력스트림으로 부터 1 byte를 읽어서 반환한다. 읽을 수 없으면 -1을 반환한다.
    abstract int read();

    // 입력스트림으로부터 len개의 byte를 읽어서 byte배열 b의 off위치부터 저장한다.
    int read(byte[] b, int off, int len) {
        ...
        for(int i = 0; i < off + len; i++) {
            // read()를 호출해서 데이터를 읽어서 배열을 채운다.
            b[i] = (byte)read();
        }
    }
        ...
    // 입력스트림으로부터 byte배열 b의 크기만큼 데이터를 읽어서 배열 b에 저장한다.
    int read(byte[] b) {
        return read(b, 0, b.length);
    }
        ...
}
```

이 코드는 `InputStream`의 실제 소스코드의 일부를 이해하기 쉽게 약간 변경한 것인데, 여기서 `read(byte[] b, int off, int len)`의 코드를 보면 `read()`를 호출하는 것을 알 수 있다 `read()`가 추상메소드이지만 이처럼 `read(byte[] b, int off, int len)`의 내에서 `read()`를 호출할 수 있다.

`read(byte[] b)`도 `read(byte[], int off, int len)`를 호출하지만 `read(byte[] b, int off, int len)`가 다시 추상메소드 `read()`를 호출하기 때문에 `read(byte[] b)`도 추상메소드 `read()`를 호출한다고 할 수 있다.

메소드는 선언부만 알고 있어도 호출이 가능하기 때문에, 추상메소드를 호출하는 코드를 작성할 수 있다. 실제로는 추상클래스를 상속받아서 추상메소드를 구현한 클래스의 인스턴스에 대해서 추상메소드가 호출될 것이기 때문에 추상메소드를 호출하는 코드를 작성해도 아무런 문제가 되지 않는다

결론적으로 `read()`는 반드시 구현되어야하는 핵심적인 메소드이고, `read()`없이는 `read(byte[] b, int off, int len)`와 `read(byte[] b)`는 의미가 없다는 것을 확인할 수 있다.

</br>

## 1.4 보조 스트림

스트림의 기능을 보완하기 위한 보조스트림이 제공된다. 보조스트림은 실제 데이터를 주고받는 스트림이 아니기 때문에 데이터를 입출력할 수 있는 기능은 없지만, 스트림의 기능을 향상시키거나 새로운 기능을 추가할 수 있다. 그래서 보조스트림만으로는 입출력을 처리할 수 없고, 스트림을 먼저 생성한 다음에 이를 이용해서 보조스트림을 생성해야 한다.

예를 들어 test.txt라는 파일을 읽기위해 `FileInputStream`을 사용할 때, 입력 성능을 향상시키기 위해 버퍼를 사용하는 보조스트림인 `BufferedInputStream`을 사요하는 코드는 다음과 같다.

``` java
// 먼저 기반 스트림을 생성한다.
FileInputStram fis = new FileInputStream("test.txt");

// 기반 스트림을 이용해서 보조스트림을 생성한다.
BufferedInputStream bis = new BufferedInputStream(fis);

bis.read(); // 보조스트림인 BufferedInputStream으로부터 데이터를 읽는다.
```

코드 상으로는 보조스트림인 `BufferedInputStream`이 입력기능을 수행하는 것처럼 보이지만, 실제 입력기능은 `BufferInputStream`과 연결된 `FileInputStream`이 수행하고, 보조스트림인 `BufferedInputStream`은 버퍼만을 제공한다. 버퍼를 사용한 입출력과 사용하지 않은 입출력간의 성능차이는 상당히기 때문에 대부분의 경우에 버퍼를 이용한 보조스트림을 사용한다.

`BufferedInputStream`, `DataInputStream`, `DigestInputStream`, `LineNumberInputStream`, `PushbackInputStream`은 모두 `FilterInputStream`의 자손들이고, `FilterInputStream`은 `InputStream`의 자손이라서 결국 모든 보조스트림 역시 `InputStream`과 `OutputStream`의 자손들이므로 입출력방법이 같다.

![image](https://ifh.cc/g/kbn2W3.png)

</br>

## 1.5 문자기반 스트림 - Reader, Writer

지금까지 알아본 스트림은 모두 바이트기반의 스트림이었다. 바이트기반이라 함은 입출력의 단위가 1 byte라는 뜻이다. C언어와 달리 Java에서는 한 문자를 의미하는 char형이 1 byte가 아니라 2 byte이기 때문에 바이트기반의 스트림으로 2 byte인 문자를 처리하는 데는 어려움이 있다.

이 점을 보완하기 위해서 문자기반의 스트림이 제공된다. 문자데이터를 입출력할 때는 바이트 기반 스트림 대신 문자기반 스트림을 사용해야 한다.

> **InputStream → Reader**   
**OutputStream → Writer**

![image](https://ifh.cc/g/vzzYNn.png)

> StringBufferInputStream, StringBufferOutputStream은 StringReader와 StringWriter로 대체되어 더 이상 사용되지 않는다.

문자기반 스트림의 이름은 바이트기반 스트림의 이름에서 `InputStream`은 `Reader`로 `OutputStream`은 `Writer`로 바꾸면 된다. 단, `ByteArrayInputStream`에 대응하는 문자기반 스트림은 char배열을 사용하는 `CharArrayReader`이다.

다음 표는 바이트기반 스트림과 문자기반 스트림의 읽기와 쓰기에 사용되는 메소드를 비교한 것인데 byte배열 대신 char배열을 사용한다는 것과 추상메소드가 달라졌다. `Reader`와 `Writer`에서도 역시 추상메소드가 아닌 메소드들은 추상메소드를 이용해서 작성되었으며, 프로그래밍적인 관점에서 볼 때 `read()`를 추상메소드로 한느 것보다 `int read(char[] cbuf, int off, int len)`를 추상메소드로 하는 것이 더 바람직하다.

바이트기반 스트림과 문자기반 스트림은 이름만 조금 다를 뿐 활용방법은 거의 같다.

![image](https://ifh.cc/g/P4H4al.png)

보조스트림 역시 다음과 같은 문자기반 보조스트림이 존재하며 사용목적과 방식은 바이트기반 보조스트림과 다르지 않다.

![image](https://ifh.cc/g/jq0aM4.png)