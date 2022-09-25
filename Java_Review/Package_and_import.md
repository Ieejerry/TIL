Chapter 7. 객체지향 프로그래밍2

# 3. package와 import

## 3.1 패키지(package)

패키지란, 클래스의 묶음이다. 패키지에는 클래스 또는 인터페이스를 포함시킬 수 있으며, 서로 관련된 클래스들끼리 그룹 단위로 묶어 놓음으로써 클래스를 효율적으로 관리할 수 있다. 같은 이름의 클래스 일지라도 서로 다른 패키지에 존재하는 것이 가능하므로, 자신만의 패키지 체계를 유지함으로써 다른 개발자가 개발한 클래스 라이브러리의 클래스와 이름이 충돌하는 것을 피할 수 있다.

지금까지는 단순히 클래스 이름으로만 클래스를 구분 했지만, 사실 클래스의 실제 이름(full name)은 패키지명을 포함한 것이다.

예를 들면 `String`클래스의 실제 이름은 `java.lang.String`이다. `java.lang`패키지에 속한 `String`클래스라는 의미이다. 그래서 같은 이름의 클래스일 지라도 서로 다른 패키지에 속하면 패키지명으로 구별이 가능하다.

**클래스가 물리적으로 하나의 클래스파일(.class)인 것과 같이 패키지는 물리적으로 하나의 디렉토리이다.** 그래서 어떤 패키지에 속한 클래스는 해당 디렉토리에 존재하는 클래스파일(.class)이어야 한다.

예를 들어, `java.lang.String`클래스는 물리적으로 디렉토리 java의 서브디렉토리인 lang에 속한 String.class파일이다. 그리고 우리가 자주 사용하는 `System`클래스 역시 `java.lang`패키지에 속하므로 lang디렉토리에 포함되어 있다.

> 클래스 파일들을 압축한 것이 jar파일(*.jar)이며, jar파일은 'jar.exe'외에도 알집이나 winzip으로 압축을 풀 수 있다.

디렉토리가 하위 디렉토리를 가질 수 있는 것처럼, 패키지도 다른 패키지를 포함할 수 있으며 점'.'으로 구분한다. 예를 들면 `java.lang`패키지에서 `lang`패키지는 `java`패키지의 하위패키지이다.

> - 하나의 소스파일에는 첫 번째 문장으로 단 한 번의 패키지 선언만을 허용한다.
> - 모든 클래스는 반드시 하나의 패키지에 속해야 한다.
> - 패키지는 점(.)을 구분자로 하여 계층구조로 구성할 수 있다.
> - 패키지는 물리적으로 클래스 파일(.class)을 포함하는 하나의 디렉토리이다.

</br>

## 3.2 패키지의 선언

패키지를 선언하는 것은 아주 간단하다. 클래스나 인터페이스의 소스파일(.java)의 맨 위에 당므과 같이 한 줄만 적어주면 된다.

``` java
package 패키지명;
```

위와 같은 패키지 선언문은 반드시 소스파일에서 주석과 공백을 제외한 첫 번째 문장이어야 하며, 하나의 소스파일에 단 한 번만 선언될 수 있다. 해당 소스파일에 포함된 모든 클래스나 인터페이스는 선언된 패키지에 속하게 된다.

패키지명은 대소문자를 모두 허용하지만, 클래스명과 쉽게 구분하기 위해서 소문자로 하는 것을 원칙으로 하고 있다.

모든 클래스는 반드시 하나의 패키지에 포함되어야 하는데, 그럼에도 불구하고 지금까지 소스파일을 작성할 때 패키지를 선언하지 않고도 아무런 문제가 없었던 이유는 자바에서 기본적으로 제공하는 '이름없는 패키지(unnamed package)' 때문이다.

소스파일에 자신이 속할 패키지를 지정하지 않은 클래스는 자동적으로 '이름 없는 패캐지'에 속하게 된다. 결국 패키지를 지정하지 않는 모든 클래스들은 같은 패키지에 속하는 셈이다.

예제 7-9 / ch7 / PackageTest.java

``` java
package com.codechobo.book;

public class PackageTest {
	public static void main(String[] args) {
		System.out.println("Hello World!");
	}
}
```

위의 예제를 작성한 뒤 다음과 같이 `-d`옵션을 추가하여 컴파일을 한다.

```
C:\jdk1.8\work>jacac -d . PackageTest.java
```

`-d`옵션은 소스파일에 지정된 경로를 통해 패키지의 위치를 찾아서 클래스파일을 생성한다. 만일 지정된 패키지와 일치하는 디렉토리가 존재하지 않는다면 자동적으로 생성한다.

`-d`옵션 뒤에는 해당 패키지의 루트(root)디렉토리의 경로를 적어준다. 여기서는 현재 디렉토리(.) 즉, 'C:\jdk1.8\work'로 지정했기 때문에 컴파일을 수행하고 나면 다음과 같은 구조로 디렉토리가 생성된다.

![image](https://ifh.cc/g/BkD3Y9.png)

기존에 디렉토리가 존재하지 않았으므로 컴파일러가 패키지의 계층구조에 맞게 새로 디렉토리를 새엉하고 컴파일된 클래스파일(PackageTest.class)를 book디렉토리에 놓았다.

이제는 패키지의 루트 디렉토리를 클래스패스(classpath)에 포함시켜야 한다. `com.codechobo.book`패키지의 루트 디렉토리는 디렉토리 'com'의 상위 디렉토리인 'C:\jdk1.8\work'이다. 이 디렉토리를 클래스패스에 포함시켜야만 실행 시 JVM이 PackageTest클래스를 찾을 수 있다.

> 클래스패스(classpath)는 컴파일러(javac.exe)나 JVM 등이 클래스의 위치를 찾는데 사용되는 경로이다.

윈도우즈에서 '제어판 - 시스템 - 고급 시스템 설정 - 환경 변수 - 새로 만들기'에서 변수이름에 'CLASSPATH'를 입력하고 변수 값에는 '.;c:\jdk1.8\work'를 입력한다.

';'를 구분자로 하여 여러 개의 경로를 클래스패스에 짖어할 수 있으며, 맨 앞에 '.;'를 추가한 이유는 현재 디렉토리(.)를 클래스패스에 포함시키기 위해서다.

클래스패스를 지정해주지 않으면 기본적으로 현재 디렉토리(.)가 클래스패스로 지정되지만, 이처럼 클래스패스를 따로 지정해주는 경우에는 더 이상 현재 디렉토리가 자동적으로 클래스패스로 지정되지 않기 때문에 이처럼 별도로 추가를 해주어야 한다.

이제 PackageTest 예제를 실행해보겠다.

```
c:\WINDOWS>java com.codechobo.book.PackageTest
Hello World!
```

실행 시에는 이와 같이 `PackageTest`클래스의 패키지명을 모두 적어주어야 한다.

</br>

## 3.3 import문

소스코드를 작성할 때 다른 패키지의 클래스를 사용하려면 패키지명이 포함된 클래스 이름을 사용해야 한다. 하지만, 매번 패키지명을 붙여서 작성하기란 여간 불편한 일이 아니다.

클래스의 코드를 작성하기 전에 import문으로 사용하고자 하는 클래스의 패키지를 미리 명시해주면 소스코드에 사용되는 클래스이름에서 패키지명은 생략할 수 있다.

import문의 역할은 컴파일러에게 소스파일에 사용된 클래스의 패키지에 대한 정보를 제공하는 것이다. 컴파일 시에 컴파일러는 import문을 통해 소스파일에 사용된 클래스들이 패키지를 알아 낸 다음, 모든 클래스이름 앞에 패키지명을 붙여 준다.

> import문은 프로그램의 성능에 전혀 영향을 미치지 않는다. import문을 많이 사용하면 컴파일 시간이 아주 조금 더 걸릴 뿐이다.

## 3.4 import문의 선언

모든 소스파일(.java)에서 import문은 package문 다음에, 그리고 클래스 선언문 이전에 위치해야 한다. import문은 package문과 달리 한 소스파일에 여러 번 선언할 수 있다.

> 일반적인 소스파일(*.java)의 구성은 다음의 순서로 되어 있다.
> 1. package문
> 2. import문
> 3. 클래스 선언

import문을 선언하는 방법은 다음과 같다.

``` java
import 패키지명.클래스명;
    또는
import 패키지명.*;
```

키워드 `import`와 패키지명을 생략하고자 하는 클래스의 이름을 패키지명과 함께 써주면 된다. 같은 패키지에서 여러 개의 클래스가 사용될 때, import문을 여러 번 사용하는 대신 `패키지명.*`을 이용해서 지정된 패키지에 속하는 모든 클래스를 패키지명 없이 사용할 수 있다.

클래스이름을 지정해주는 대신 '*'을 사용하면, 컴파일러는 해당 패키지에서 일치하는 클래스이름을 찾아야 하는 수고를 더 해야 한다. 단지 그 뿐이다. **실행 시 성능상의 차이는 전혀 없다.**

``` java
import java.util.Calendar;
import java.util.Date;
import java.util.ArrayList;
```

이처럼 import문을 여러 번 사용하는 대신 아래와 같이 한 문장으로 처리할 수 있다.

``` java
import java.util.*;
```

한 패키지에서 여러 클래스를 사용하는 경우 클래스의 이름을 일일이 지정해주는 것보다 '패키지명.*'와 같이 하는 것이 편리하다.

하지만, import하는 패키지의 수가 많을 때는 어느 클래스가 어느 패키지에 속하는지 구별하기 어렵다는 단점이 있다.

한 가지 더 알아두어야 할 것은 import문에서 클래스의 이름 대신 '*'을 사용하는 것이 하위 패키지의 클래스까지 포함하는 것은 아니다.

``` java
import java.util.*;
import java.text.*;
```

그래서 위의 두 문장 대신 다음과 같이 할 수는 없다.

``` java
import java.*;
```

예제 7-10 / ch7 / ImportTest.java

``` java
import java.text.SimpleDateFormat;
import java.util.Date;

public class ImportTest {
	public static void main(String[] args) {
		Date today = new Date();
		
		SimpleDateFormat date = new SimpleDateFormat("yyyy/MM/dd");
		SimpleDateFormat time = new SimpleDateFormat("hh:mm:ss a");
		
		System.out.println("오늘 날짜는 " + date.format(today));
		System.out.println("현재 시간은 " + time.format(today));
	}
}
```

```
오늘 날짜는 2022/09/25
현재 시간은 11:44:01 오후
```

현재 날짜와 시간을 지정된 형식에 맞춰 출력하는 예제이다. `SimpleDateFormat`과 `Date`클래스는 다른 패키지에 속한 클래스이므로 import문으로 어느 패키지에 속한 클래스인지 명시해 주었다. 그래서 소스에서 클래스이름 앞에 패키지명을 생략할 수 있었다.

만일 import문을 지정하지 않았다면 다음과 같이 클래스이름에 패키지명도 적어줘야 한다.

``` java
java.util.Date today = new java.util.Date();
		
java.text.SimpleDateFormat date = new java.text.SimpleDateFormat("yyyy/MM/dd");
java.text.SimpleDateFormat time = new java.text.SimpleDateFormat("hh:mm:ss a");
```

import문으로 패키지를 지정하지 않으면 위와 같이 모든 클래스이름 앞에 패키지명을 반드시 붙여야 한다. 단, 같은 패키지 내의 클래스들은 import문을 지정하지 않고도 패키지명을 생략할 수 있다.

지금까지 `System`과 `String` 같은 `java.lang`패키지의 클래스들을 패키지명 없이 사용할 수 있었던 이유는 모든 소스파일에는 묵시적으로 다음과 같은 import문이 선언되어 있기 때문이다.

``` java
import java.lang.*;
```

`java.lang`패키지는 매우 빈번히 사용되는 중요한 클래스들이 속한 패키지이기 때문에 따로 import문으로 지정하지 않아도 되도록 한 것이다.

</br>

## 3.5 static import문

import문을 사용하면 클래스의 패키지명을 생략할 수 있는 것과 같이 static import문을 사용하면 static멤버를 호출할 때 클래스 이름을 생략할 수 있다. 특정 클래스의 static멤버를 자주 사용할 때 편리하다. 그리고 코드도 간결해진다.

``` java
import static java.lang.Integer.*;  // Integer클래스의 모든 static메소드
import static java.lang.Math.random;    // Math.random()만. 괄호 안붙임.
import static java.lang.System.out; // System.out을 out만으로 참조 가능
```

만일 위와 같이 static import문을 선언하였다면, 아래의 왼쪽 코드를 오른쪽 코드와 같이 간략히 할 수 있다.

![image](https://ifh.cc/g/xsWvjT.png)

예제 7-11 / ch7 / StaticImportTest.java

``` java
import static java.lang.System.out;
import static java.lang.Math.*;

public class StaticImportEx1 {
	public static void main(String[] args) {
		// System.out.println(Math.random());
		out.println(random());
		
		// System.out.println("Math.PI : " + Math.PI);
		out.println("Math.PI : " + PI);
	}
}
```

```
0.13678092964373767
Math.PI : 3.141592653589793
```