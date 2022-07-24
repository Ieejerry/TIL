# 2. 자바개발환경 구축하기

</br>

## 2.1 자바 개발도구(JDK) 설치하기

자바로 프로그래밍을 하기위해서는 먼저 JDK(Java Development Kit)를 설치해야 한다. JDK를 설치하면, 자바가상머신(Java Virtual Machine, JVM)과 자바클래스 라이브러리(Java API)외에 자바를 개발하는데 필요한 프로그램들이 설치된다.

JDK의 설치가 끝났으면 설치된 디렉토리의 bin디렉토리(예: C:\jdk1.8\bin)를 path에 추가해주어야 한다. 이 디렉토리에는 자바로 프로그램을 개발하는데 필요한 실행파일들이 들어있다. path는 OS가 파일의 위치(디렉토리)를 파악하는데 사용하는 경로(path)로, path에 디렉토리를 등록하면, 해당 디렉토리에 포함된 파일을 파일 경로없이 파일 이름만으로도 사용할 수 있게 된다.

JDK의 bin디렉토리에 있는 주요 실행파일들은 다음과 같다.

- **javac.exe** 자바 컴파일러, 자바소스코드를 바이트코드로 컴파일한다.   C:\jdk1.8\work>javac Hello.java
- **java.exe** 자바 인터프리터, 컴파일러가 생성한 바이트코드를 해석하고 실행한다.   C:\jdk1.8\work>java Hello
- **javap.exe** 역어셈블러, 컴파일된 클래스파일을 원래의 소스로 변환한다.   C:\jdk1.8\work>javap Hello > Hello.java

위와 같이 하면 Hello.class파일이 역컴파일되어 Hello.java에 저장된다. 그러나 원래의 소스 전체가 아닌 선언부만 저장될 뿐이다. '-c'옵션을 이용하면, 바이트코드로 컴파일된 내용도 볼 수 있다.

> 바이트코드 - JVM이 이해할 수 있는 기계어, JVM은 바이트코드를 해당 OS의 기계어로 변환하여 OS로 전달함

- **javadoc.exe** 자동문서생성기, 소스파일에 있는 주석(/** */)을 이용하여 Java API문서와 같은 형식의 문서를 자동으로 생성한다.   C:\jdk1.8\work>javadoc Hello.java
- **jar.exe** 압축프로그램, 클래스파이로가 프로그램의 실행에 관련된 파일을 하나의 jar파일(.jar)로 압축하거나 압축해제한다.   
압축할 때 : C:\jdk1.8\work>jar cvf Hello.jar Hello1.class Hello2.class   
압축 풀 때 : C:\jdk1.8\work>jar xvf Hello.jar 

> JDK와 JRE
> - JDK - 자바개발도구(Java Development Kit)
> - JRE - 자바실행환경(Java Runtime Environment), 자바로 작성된 응용프로그램이 실행되기 위한 최소환경.
> - JDK = JRE + 개발에 필요한 실행파일(Javac.exe 등)
> - JRE = JVM + 클래스라이브러리(Java API)

</br>

## 2.2 Java API 문서 설치하기

**자바에서 제공하는 클래스 라이브러리(Java API)를 잘 사용하기 위해서는 Java API문서가 필수적이다. 이 문서에는 클래스 라이브러리의 모든 클래스에 대한 설명이 자세하게 나와 있다.**

이 문서에 나오는 모든 클래스를 다 공부할 필요는 없고, 자주 사용되는 것만을 공부한 다음 나머지는 영어사전처럼 필요할 때 찾아서 사용하면 된다.

Java API문서는 'http://java.sun.com/' 에서 다운받을 수 있다. 이 문서는 ZIP방식으로 압축되어 있으므로 압축을 풀어야 한다. 모두 html문서로 되어 있으며 자바와 관련된 여러 가지 유용한 내용이 수록되어 있다.

![Java API문서](https://ifh.cc/g/V7VmR9.png)