Chapter 13. 쓰레드 thread

# 3. start()와 run()

`start()`와 `run()`의 차이와 쓰레드가 실행되는 과정에 대해서 자세히 살펴보겠다.

`main`메소드에서 `run()`을 호출하는 것은 생성된 쓰레드를 실행시키는 것이 아니라 단순히 클래스에 선언된 메소드를 호출하는 것아다.

![image](https://ifh.cc/g/qjdJ58.png)

반면에 `start()`는 새로운 쓰레드가 작업을 실행하는데 필요한 호출스택(call stack)을 생성한 다음에 `run()`을 호출해서, 생성된 호출스택에 `run()`이 첫 번째로 올라가게 된다.

모든 쓰레드는 독립적인 작업을 수행하기 위해 자신만의 호출스택을 필요로 하기 때문에, 새로운 쓰레드를 생성하고 실행시킬 때마다 새로운 호출스택이 생성되고 쓰레드가 종료되면 작업에 사용된 호출스택은 소멸된다.

![image](https://ifh.cc/g/vAhfTF.png)

① main메소드에서 쓰레드의 start()를 호출한다.   
② start()는 새로운 쓰레드르를 생성하고, 쓰레드가 작업하는데 사용될 호출스택을 생성한다.   
③ 새로 생성된 호출스택에 run()이 호출되어, 쓰레드가 독립된 공간에서 작업을 수행한다.   
④ 이제는 호출스택이 2개이므로 스케줄러가 정한 순서에 의해서 번갈아 가면서 실행된다.    

호출스택에서는 가장 위에 있는 메소드가 현재 실행중인 메소드이고 나머지 메소드들은 대기상태에 있다. 그러나 쓰레드가 둘 이상일 때는 호출스택의 최상위에 있는 메소드일지라도 대기상태에 있을 수 있다.

스케줄러는 실행대기중인 쓰레드들의 우선순위를 고려하여 실행순서와 실행시간을 잘 정하고, 각 쓰레드들은 작성된 스케줄에 따라 자신의 순서가 되면 지정된 시간동안 작업을 수행한다.

이 때 주어진 시간동안 작업을 마치지 못한 쓰레드는 다시 자신의 차례가 돌아올 때까지 대기상태로 있게 되며, 자겅ㅂ을 마친 쓰레드, 즉 `run()`의 수행이 종료된 쓰레드는 호출스택이 모두 비워지면서 이 쓰레드가 사용하던 호출스택은 사라진다.

</br>

### main쓰레드

`main`메소드의 작업을 수행하는 것도 쓰레드이며, 이를 `main`쓰레드라고 한다. 프로그램을 실행하면 기본적으로 하나의 쓰레드(일꾼)를 생성하고, 그 쓰레드가 `main`메소드를 호출해서 작업이 수행되도록 한다.

![image](https://ifh.cc/g/QF5DRM.png)

`main`메소드가 수행을 마치면 프로그램이 종료되었으나, 위의 그림에서와 같이 `main`메소드가 수행을 마쳤다하더라도 다른 쓰레드가 아직 작업을 마치지 않은 상태라면 프로그램의 종료되지 않는다.

> **실행 중인 사용자 쓰레드가 하나도 없을 때 프로그램은 종료된다.**

쓰레드는 '사용자 쓰레드(user thread)'와 '데몬 쓰레드(daemon thread)', 두 종류가 있다.

</br>

예제 13-2 / ch13 / ThreadEx2.java

``` java
public class ThreadEx2 {
	public static void main(String[] args) {
		ThreadEx2_1 t1 = new ThreadEx2_1();
		t1.start();
	}
}

class ThreadEx2_1 extends Thread {
	public void run() {
		throwException();
	}
	
	public void throwException() {
		try {
			throw new Exception();
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}
```

```
java.lang.Exception
	at ThreadEx2_1.throwException(ThreadEx2.java:15)
	at ThreadEx2_1.run(ThreadEx2.java:10)
```

새로 생성한 쓰레드에서 고의로 예외를 발생시키고 `printStackTrace()`를 이용해서 예외가 발생한 당시의 호출스택을 출력하는 예제이다. 호출스택의 첫 번째 메소드가 `main`메소드가 아니라 `run`메소드이다.

한 쓰레드가 예외가 발생해서 종료되어도 다른 쓰레드의 실행에는 영향을 미치지 않는다. 아래의 그림에 `main`쓰레드의 호출스택이 없는 이유는 `main`쓰레드가 이미 종료되었기 때문이다.

![image](https://ifh.cc/g/VOrBBD.png)

</br>

예제 13-3 / ch13 / ThreadEx3.java

``` java
public class ThreadEx3 {
	public static void main(String[] args) {
		ThreadEx3_1 t1 = new ThreadEx3_1();
		t1.run();
	}
}

class ThreadEx3_1 extends Thread {
	public void run() {
		throwException();
	}
	
	public void throwException() {
		try {
			throw new Exception();
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}
```

```
java.lang.Exception
	at ThreadEx3_1.throwException(ThreadEx3.java:15)
	at ThreadEx3_1.run(ThreadEx3.java:10)
	at ThreadEx3.main(ThreadEx3.java:4)
```

이전 예제와 달리 쓰레드가 새로 생성되지 않았다. 그저 `ThreadEx3_1`클래스의 `run()`이 호출되었을 뿐이다. 아래 그림은 `main`쓰레드의 호출스택이며, `main`메소드가 포함되어 있다.

![image](https://ifh.cc/g/bNRQtl.png)