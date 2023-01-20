Chapter 15. 입출력 I/O

# 7. 직렬화(Serialization)

</br>

## 7.1 직렬화란?

직렬화(Serialization)란 객체를 데이터 스트림으로 만드는 것을 뜻한다. 즉, 객체에 저장된 데이터를 스트림에 쓰기(write)위해 연속적인(serial) 데이터로 변환하는 것을 말한다.

반대로 스트림으로부터 데이터를 읽어서 객체를 만드는 것을 역직렬화(deserialization)라고 한다.

객체는 클래스에 정의된 인스턴스변수의 집합이다. 객체에는 클래스변수나 메소드가 포함되지 않는다. 객체는 오직 인스턴스변수들로만 구성되어 있다.

인스턴스변수는 인스턴스마다 다른 값을 가질 수 있어야하기 때문에 별도의 메모리공간이 필요하지만 메소드는 변하는 것이 아니라서 메모리를 낭비해 가면서 인스턴스마다 같은 내용의 코드(메소드)를 포함시킬 이유는 없다.

객체를 저장한다는 것은 바로 객체의 모든 인스턴스변수이 값을 저장한다는 것과 같은 의미이다. 어떤 객체를 저장하고자 한다면, 현재 객체의 모든 인스턴스변수의 값을 저장하기만 하면 된다. 그리고 저장했던 객체를 다시 생성하려면, 객체를 생성한 후에 저장했던 값을 읽어서 생성한 객체의 인스턴스변수에 젖아하면 되는 것이다.

클래스에 정의된 인스턴스변수가 단순히 기본형일 때는 인스턴스변수의 값을 저장하는 일이 간단하지만, 인스턴스변수의 타입이 참조형일 때는 그리 간단하지 않다. 예를 들어 인스턴스변수의 타입이 배열이라면 배열에 저장된 값들도 모두 저장되어야할 것이다.

객체를 직렬화/역직렬화할 수 있는 `ObjectInputStream`/`ObjectOutputStream`을 사용하면 된다.

> 두 객체가 동일한지 판단하는 기준이 두 객체의 인스턴스변수의 값들이 같고 다름이다.

</br>

## 7.2 ObjectInputStream, ObjectOutputStream

직렬화(스트림에 객체를 출력)에는 `ObjectOutputStream`을 사용하고 역직렬화(스트림으로부터 객체를 입력)에는 `ObjectInputStream`을 사용한다.

`ObjectInputStream`과 `ObjectOutputStream`은 각각 `InputStream`과 `OutputStream`을 직접 상속받지만 기반스트림을 필요로 하는 보조스트림이다. 그래서 객체를 생성할 때 입출력(직렬화/역직렬화)할 스트림을 지정해주어야 한다.

``` java
ObjectInputStream(InputStream in)
ObjectOutputStream(OutputStream out)
```

만일 파일에 객체를 저장(직렬화)하고 싶다면 다음과 같이 하면 된다.

``` java
FileOutputStream fos = new FileOutputStream("objectfile.ser");
ObjectOutputStream out = new ObjectOutputStream(fos);

out.writeObject(new UserInfo());
```

위의 코드는 objectfile.ser이라는 파일에 `UserInfo`객체를 직렬화하여 저장한다. 출력할 스트림(FileOutputStream)을 생성해서 이를 기반스트림으로 하는 `ObjectOutputStream`을 생성한다.

`ObjectOutputStream`의 `writeObject(Object obj)`을 사용해서 객체를 출력하면, 객체가 파일에 직렬화되어 저장된다.

직렬화할 때와는 달리 입력스트림을 사용하고 `writeObject(Object obj)`대신 `readObject()`를 사용하여 저장된 데이터를 읽기만 하면 객체로 역직렬화된다.

다만 `readObject()`의 반환타입이 Object이기 때문에 객체 원래의 타입으로 형변환 해주어야 한다.

``` java
FileInputSteram fis = new FileInputStream("objectfile.ser");
ObjectInputStream in = new ObjectInputStream(fis);

UserInfo info = (UserInfo)in.readObject();
```

`ObjectInputStream`과 `ObjectOutputStream`에는 `readObject()`와 `writeObject()`이외에도 여러 가지 타입의 값을 입출력할 수 있는 메소드를 제공한다.

![image](https://ifh.cc/g/jNpvfG.png)

이 메소드들은 직렬화와 역직렬화를 직접 구현할 때 주로 사용되며, `defaultReadObject()`와 `defaultWriteObject()`는 자동 직렬화를 수행한다.

객체를 직렬화/역직렬화하는 작업은 객체의 모든 인스턴스변수가 참조하고 있는 모든 객체에 대한 것이기 때문에 상당히 복잡하며 시간도 오래 걸린다. `readObject()`와 `writeObject()`를 사용한 자동 직렬화가 편리하기는 하지만 직렬화작업시간을 단축시키려면 직렬화하고자 하는 객체의 클래스에 추가적으로 다음과 같은 2개의 메소드를 직집 구현해주어야 한다.

``` java
private void wirteObject(ObjectOutputStream out) throws IOException {
    // write메소들를 사용해서 직렬화를 수행한다.
}

private void readObject(ObjectInputStream in) throws IOExeption, ClassNotFoundException {
    // read메소드를 사용해서 역직렬화를 수행한다.
}
```

</br>

## 7.3 직렬화가 가능한 클래스 만들기 - Serializable, transient

직렬화가 가능한 클래스를 만드는 방법은 간단하다. 직렬화하고자 하는 클래스가 `java.io.Serializable`인터페이스를 구현하도록 하면 된다.

예를 들어 왼쪽과 같이 `UserInfo`라는 클래스가 있을 때, 이 클래스를 직렬화가 가능하도록 변경하려면 오른쪽과 같이 `Serializable`인터페이스를 구현하도록 변경하면 된다.

![image](https://ifh.cc/g/CfRKyZ.png)

`Serializable`인터페이스는 아무런 내용도 없는 빈 인터페이스이지만, 직렬화를 고려하여 작성한 클래스인지를 판단하는 기준이 된다.

``` java
public interface Serializable { }
```

아래와 같이 `Serializable`을 구현한 클래스를 상속받는다면, `Serializable`을 구현하지 않아도 된다. `UserInfo`는 `Serializable`을 구현하지 않았지만 조상인 `SuperUserInfo`가 `Serializable`를 구현하였으므로 `UserInfo` 역시 직렬화가 가능하다.

``` java
public class SuperUserInfo implements Serializable {
    String name;
    String password;
}

public class UserInfo extends SuperUserInfo {
    int age;
}
```

위의 경우 `UserInfo`객체를 직렬화화면 조상인 `SuperUserInfo`에 정의된 인스턴스변수 `name`, `password`도 함께 직렬화된다.

그러나 다음과 같이 조상클래스가 `Serializable`을 구현하지 않았다면 자손클래스를 직렬화할 때 조상클래스에 정의된 인스턴스변수 `name`과 `password`는 직렬화 대상에서 제외된다.

``` java
public class SuperUserInfo {
    String name;
    String password;
}

public class UserInfo extends SuperUserInfo implements Serializable {
    int age;
}
```

조상클래스에 정의된 인스턴스변수 `name`과 `password`를 직렬화 대상에 포함시키기 위해서는 조상클래스가 `Serializable`을 구현하도록 하던가, `UserInfo`에서 조상의 인스턴스변수들이 직렬화되도록 처리하는 코드를 직접 추가해 주어야한다.

아래의 `UserInfo`클래스는 `Serializable`을 구현하고 있지만, 이 클래스의 객체를 직렬화하면 `java.io.NotSerializableException`이 발생하면서 직렬화에 실패한다. 그 이유는 직렬화할 수 없는 클래스의 객체를 인스턴스변수가 참조하고 있기 때문이다.

모든 클래스의 최고조상인 `Object`는 `Serializable`을 구현하지 않았기 때문이다. 직렬화할 수 없다.

``` java
public class UserInfo implements Serializable {
    String name;
    String passwrod;
    int age;

    Object obj = new Object();  // Object객체는 직렬화할 수 없다.
}
```

위의 경우와 비교해서 다음과 같은 경우에는 직렬화가 가능하다. 인스턴스변수 `obj`의 타입이 직렬화가 안 되는 `Object`이긴 하지만 실제로 저장된 객체는 직렬화가 가능한 `String`인스턴스이기 때문에 직렬화가 가능하다.

인스턴스변수의 타입이 아닌 실제로 연결된 객체의 종류에 의해서 결정된다.

``` java
public class UserInfo implements Serializable {
    String name;
    String password;
    int age;

    Object obj = new String("abc"); // String은 직렬활될 수 있다.
}
```

직렬화하고자 하는 객체의 클래스에 직렬화가 안 되는 객체에 대한 참조를 포함하고 있다면, 제어자 `transient`를 붙여서 직렬화 대상에서 제외되도록 할 수 있다.

또는 `password`와 같이 보안상 직렬화되면 안 되는 값에 대해서 `transient`를 사용할 수 있다. 다르게 표현하면 `transient`가 붙은 인스턴스변수의 값은 그 타입의 기본값으로 직렬화된다.

즉, `UserInfo`객체를 역직렬화하면 참조변수인 `obj`와 `password`의 값은 null이 된다.

``` java
public class UserInfo implements Serializable {
    String name;
    transient Stirng password;   // 직렬화 대상에서 제외된다.
    int age;

    transient  Object obj = new Object();   // 직렬화 대상에서 제외된다.
}
```

</br>

예제 15-39 / ch15 / UserInfo.java

``` java
public class UserInfo implements java.io.Serializable {
	String name;
	String password;
	int age;
	
	public UserInfo() {
		this("Unknown", "1111", 0);
	}
	
	public UserInfo(String name, String password, int age) {
		this.name = name;
		this.password = password;
		this.age = age;
	}
	
	public String toString() {
		return "(" + name + ", " + password + ", " + age + ")";
	}
}
```

예제 15-39는 예제 15-40에 사용될 `UserInfo`클래스의 소스이다. 그래서 예제 15-40을 실행하기 전에 예제 15-39를 먼저 컴파일해야 한다.

</br>

예제 15-40 / ch15 / SerialEx1.java

``` java
import java.io.*;
import java.util.ArrayList;

public class SerialEx1 {
	public static void main(String[] args) {
		try {
			String fileName = "UserInfo.ser";
			FileOutputStream fos = new FileOutputStream(fileName);
			BufferedOutputStream bos = new BufferedOutputStream(fos);
			
			ObjectOutputStream out = new ObjectOutputStream(bos);
			
			UserInfo u1 = new UserInfo("JavaMan", "1234", 30);
			UserInfo u2 = new UserInfo("JavaWoman", "4321", 26);
			
			ArrayList<UserInfo> list = new ArrayList<>();
			list.add(u1);
			list.add(u2);
			
			// 객체를 직렬화한다.
			out.writeObject(u1);
			out.writeObject(u2);
			out.writeObject(list);
			out.close();
			System.out.println("직렬화가 잘 끝났습니다.");
		} catch (IOException e) {
			e.printStackTrace();
		}
	}	// main
}	// class
```

```
직렬화가 잘 끝났습니다.
```

생성한 객체를 직렬화하여 파일(UserInfo.ser)에 저장하는 예제이다. 버퍼를 이용한 `FileOut putStream`을 기반으로 하는 `ObjectOutputStream` 생성한 다음, `writeObject()`를 이용해서 객체를 `ObjectOutputStream`에 출력하면 UserInfo.ser 파일에 객체가 직렬화되어 저장된다.

이 예제처럼 ArrayList와 같은 객체를 직렬화하면 ArrayList에 저장된 모든 객체들과 각 객체의 인스턴스변수가 참조하고 있는 객체들까지 모두 직렬화된다.

> 확장자를 직렬화(Serialization)의 약자인 'ser'로 하는 것이 보통이지만 이에 대한 제약은 없다.

</br>

예제 15-41 / ch15 / SerialEx2.java

``` java
import java.io.*;
import java.util.ArrayList;

public class SerialEx2 {
	public static void main(String[] args) {
		try {
			String fileName = "UserInfo.ser";
			FileInputStream fis = new FileInputStream(fileName);
			BufferedInputStream bis = new BufferedInputStream(fis);
			
			ObjectInputStream in = new ObjectInputStream(bis);
			
			// 객체를 읽을 때는 출력한 순서와 일치해야한다.
			UserInfo u1 = (UserInfo)in.readObject();
			UserInfo u2 = (UserInfo)in.readObject();
			ArrayList list = (ArrayList)in.readObject();
			
			System.out.println(u1);
			System.out.println(u2);
			System.out.println(list);
			in.close();
		} catch (Exception e) {
			e.printStackTrace();
		}
	}	// main
}	// class
```

```
(JavaMan, 1234, 30)
(JavaWoman, 4321, 26)
[(JavaMan, 1234, 30), (JavaWoman, 4321, 26)]
```

이 전의 예제에서 직렬화한 객체를 역직렬화하는 예제이다. 전과는 반대로 `FileInputStream`과 `ObjectInputStream`을, 그리고 `writeObject()`대신 `readObject()`를 사용했다는 점을 제외하고는 거의 같다.

`ObjectInputStream`의 `readObject()`로 직렬화한 객체를 역직렬화했는데, `readObject()`의 리턴타입이 Object이므로 원래의 타입으로 형변환을 해주어야 한다.

한 가지 주의해야 할 점은 객체를 역직렬화할 때는 직렬화할 때의 순서와 일치해야 한다. 예를 들어 객체 `u1`, `u2` `list`의 순서로 직렬화 했다면, 역직렬화할 때도 `u1`, `u2`, `list`의 순서로 처리해야한다.

그래서 직렬화할 객체가 많을 때는 각 객체를 개별적으로 직렬화하는 것보다 ArrayList와 같은 컬렉션에 저장해서 직렬화하는 것이 좋다.

역직렬화할 때 ArrayList 하만 역직렬화 하면 되므로 역직렬화할 객체의 순서를 고려하지 않아도 되기 때문이다.

</br>

예제 15-42 / ch15 / UserInfo2.java

``` java
import java.io.*;

class SuperUserInfo {
	String name;
	String password;
	
	SuperUserInfo() {
		this("Unknown", "1111");
	}
	
	SuperUserInfo(String name, String password) {
		this.name = name;
		this.password = password;
	}
}	// class SuperUserInfo

public class UserInfo2 extends SuperUserInfo implements java.io.Serializable {
	int age;
	
	public UserInfo2() {
		this("Unknown", "1111",0);
	}
	
	public UserInfo2(String name, String password, int age) {
		super(name, password);
		this.age = age;
	}
	
	public String toString() {
		return "(" + name + ", " + password + ", " + age + ")";
	}
	
	private void writeObject(ObjectOutputStream out) throws IOException {
		out.writeUTF(name);
		out.writeUTF(password);
		out.defaultWriteObject();
	}
	
	private void readObject(ObjectInputStream in) throws IOException, ClassNotFoundException {
		name = in.readUTF();
		password = in.readUTF();
		in.defaultReadObject();
	}
}	// class UserInfo2
```

이 예제는 직렬화되지 않는 조상으로부터 상속받은 인스턴스변수에 대한 직렬화를 구현한 것이다. 직렬화된 객체의 클래스에 아래와 같이 `writeObject()`와 `readObject()`를 추가해서 조상으로부터 상속받은 인스턴스변수인 `name`과 `password`가 직접 직렬화되도록 해야 한다. 이 메소드들은 직렬화/역직렬화 작업시에 자동적으로 호출된다.

이 두 메소드와 접근 제어자가 `private`이라는 사실이 좀 의외하겠지만, 이것은 단순히 미리 정해진 규칙이다.

``` java
private void writeObject(ObjectOutputStream out) throws IOException {
    out.writeUTF(name);
    out.writeUTF(password);
    out.defaultWriteObject();
}

private void readObject(ObjectInputStream in) throws IOException, ClassNotFoundException {
    name = in.readUTF();
    password = in.readUTF();
    in.defaultReadObject();
}
```

`name`과 `password`의 타입이 String이기 때문에 `writeUTF()`/`readUTF()`를 사용했으며 이 외에도 `ObjectInputStream`, `ObjectOutputStream`에는 `writeInt()`, `readInt()`와 같은 타입에 따른 다양한 종류의 메소드들을 제공하므로 각 인스턴스변수의 타입에 맞는 것을 선택해서 사용하면 된다. 그리고 `defaultWriteObject()`는 `UserInfo2`클래스 자신에 정의된 인스턴스변수 `age`의 직렬화를 수행한다.

</br>

## 7.4 직렬화 가능한 클래스의 버전관리

직렬화된 객체를 역직렬화할 때는 직렬화 했을 때와 같은 클래스를 사용해야 한다. 그러나 클래스이 이름이 같더라도 클래스의 내용이 변경된 경우 역직렬화는 실패하며 다음과 같은 예외가 발생한다.

```
java.io.InvalidClassException: UserInfo; local class incompatible:
stream classdesc serialVersinoUID = 6953673583338942489, local
class serialVersinoUID = -6256164443556992367
...
```

위 예외의 내용은 직렬화 할 때와 역직렬화 할 때의 클래스의 버전이 같아야 하는데 다르다는 것이다. 객체가 직렬화할 때 클래스에 정의된 멤버들의 정보를 이용해서 `serialVersinoUID`라는 클래스의 버전을 자동생성해서 직렬화 내용에 포함된다.

그래서 역직렬화할 때 클래스의 버전을 비교함으로써 직렬화할 때의 클래스의 버전과 일치하는지 확인할 수 있다.

그러나 static변수나 상수 또는 `transient`가 붙은 인스턴스변수가 추가되는 경우에는 직렬화에 영향을 미치지 않기 때문에 클래스의 버전을 다르게 인식하도록 할 필요가 없다.

네트워크로 객체를 직렬화하여 전송하는 경우, 보내는 쪽과 받는 쪽이 모두 같은 버전의 클래스를 가지고 있어야하는데 클래스가 조금만 변경되어도 해당 클래스를 재배포하는 것은 프로그램을 관리하기 어렵게 만든다.

이럴 때는 클래스의 버전을 수동으로 관리해줄 필요가 있다.

``` java
class MyData implements java.io.Serializable {
    int value;
}
```

위와 같이 `MyData`라는 직렬화가 가능한 클래스가 있을 때, 클래스의 버전을 수동으로 관리하려면 다음과 같이 `serialVersinoUID`를 추가로 정의해야 한다.

``` java
class MyData implements java.io.Serializable {
    static final long serialVersinoUID = 3518731767529258119L;
}
```

이렇게 클래스 내에 `serialVersinoUID`를 정의해주면, 클래스의 내용이 바뀌어도 클래스의 버전이 자동생성된 값으로 변경되지 않는다.

`serialVersinoUID`의 값은 정수값이면 어떠한 값으로도 지정할 수 있지만 서로 다른 클래스간의 같은 값을 갖지 않도록 serialver.exe를 사용해서 생성된 값을 사용하는 것이 보통이다.

```
C:\jdk1.8\work\ch15>serialver MyData
MyData:     static final long serialVersionUID = 3518731767529258119L;
```

serialver.exe 뒤에 `serialVersionUID`를 얻고자 하는 클래스의 이름만 적어주면 클래스의 `serialVersinoUID`를 알아낼 수 있다. serialver.exe 는 클래스에 `serialVersionUID`가 정의되어 있으면 그 값을 출력하고 정의되어 있지 않으면 자동 생성한 값을 출력한다.

serialver.exe 에 의해서 생성되는 `serialVersionUID`값은 클래스의 멤버들에 대한 정보를 바탕으로 하기 때문에 이 정보가 변경되지 않는 한 항상 같은 값을 생성한다.