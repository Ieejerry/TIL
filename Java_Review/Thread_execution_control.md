Chapter 13. 쓰레드 Thread

# 8. 쓰레드의 실행제어

쓰레드 프로그래밍이 어려운 이유는 동기화(synchronization)와 스케줄링(scheduling) 때문이다. 효율적인 멀티쓰레드 프로그램을 만들기 위해서는 보다 정교한 스케줄링을 통해 프로세스에게 주어진 자원과 시간을 여러 쓰레드가 낭비없이 잘 사용하도록 프로그래밍 해야 한다.

쓰레드의 스케줄링을 잘하기 위해서는 쓰레드의 상태와 관련 메소드를 잘 알아야 하는데, 먼저 쓰레드의 스케줄링과 관련된 메소드는 다음과 같다.

![image](https://ifh.cc/g/TbJfhX.png)

> resume(), stop(), suspend()는 쓰레드를 교착상태(dead-lock)로 만들기 쉽기 때문에 deprecated되었다.

이제 쓰레드의 상태에 대해서 알아보겠다.

![image](https://ifh.cc/g/R9FfCM.png)

> 쓰레드의 상태는 Thread의 getState()메소드를 호출해서 확인할 수 있다. JDK1.5부터 추가되었다.

</br>

### sleep(long millis) - 일정시간동안 쓰레드를 멈추게 한다.

`sleep()`은 지정된 시간동안 쓰레드를 멈추게 한다.

> **static** void sleep(long millis)   
*static** void sleep(long millis, int nanos)

밀리세컨드(millis, 1000분의 일초)와 나노세컨드(nanos, 10억분의 일초)의 시간단위로 세밀하게 값을 지정할 수 있지만 어느 정도의 오차가 발생할 수 있다는 것은 염두에 둬야한다. 예를 들어, 쓰레드가 0.0015초 동안 멈추게 하려면 다음과 같이 한다.

> 나노세컨드(nanos)로 지정할 수 있는 값의 범위는 0~999999이며, 999999나노세컨드는 약 1밀리세컨드이다.

``` java
try {
    Thread.sleep(1, 500000);    // 쓰레드를 0.0015초 동안 멈추게 한다.

} catch(InterruptedException e) {}
```

`sleep()`에 의해 일시정지 상태가 된 쓰레드는 지정된 시간이 다 되거나 `interrupt()`가 호출되면(InterruptedException발생), 잠에서 깨어나 실행대기 상태가 된다.

그래서 `sleep()`을 호출할 때는 항상 try-catch문으로 예외를 처리해줘야 한다. 매번 예외처리를 해주는 것이 번거롭기 때문에, 아래와 같이 try-catch문까지 포함하는 새로운 메소드를 만들어서 사용하기도 한다.

``` java
void delay(long millis) {
    try {
        Thread.sleep(millis);
    } catch(InterruptedException e) {}
}
```

</br>

예제 13-12 / ch13 / ThreadEx12.java

``` java
public class ThreadEx12 {
	public static void main(String[] args) {
		ThreadEx12_1 th1 = new ThreadEx12_1();
		ThreadEx12_2 th2 = new ThreadEx12_2();
		th1.start();
		th2.start();
				
		try {
			th1.sleep(2000);
		} catch (InterruptedException e) {}
		
		System.out.print("<<main 종료>>");
	}	// main
}

class ThreadEx12_1 extends Thread {
	public void run() {
		for(int i = 0; i < 300; i++) {
			System.out.print("-");
		}
		System.out.print("<<th1 종료>>");
	}	// run()
}

class ThreadEx12_2 extends Thread {
	public void run() {
		for(int i = 0; i < 300; i++) {
			System.out.print("|");
		}
		System.out.print("<<th2 종료>>");
	}	// run()
}
```

```
--------|||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||-----------------------------------------------------------|||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||--|||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------<<th1 종료>>|||||||||||||||||||<<th2 종료>><<main 종료>>
```

위의 결과를 보면 쓰레드 `th1`의 작업이 가장 먼저 종료되었고, 그 다음이 `th2`, `main`의 순인 것을 알 수 있다. 그러나 아래의 코드를 생각해보면 이 결과가 뜻밖이라는 생각이 들 것이다.

``` java
th1.start();
th2.start();
        
try {
    th1.sleep(2000);
} catch (InterruptedException e) {}

System.out.print("<<main 종료>>");
```

쓰레드 `th1`과 `th2`에 대해 `start()`를 호출하자마자 `th1.sleep(2000)`을 호출하여 쓰레드 `th1`이 2초 동안 작업을 멈추기 일시정지 상태에 있도록 하였으니까 쓰레드 `th1`이 가장 늦게 종료되어야 하는데 결과에서는 제일 먼저 종료되었다.

그 이유는 `sleep()`이 항상 현재 실행 중인 쓰레드에 대해 작동하기 때문에 `th1.sleep(2000)`과 같이 호출하였어도 실제로 영향을 받는 것은 `main`메소드를 실행하는 `main`쓰레드이다.

그래서 `sleep()`은 static으로 선언되어 있으며 참조변수를 이용해서 호출하기 보다는 `Thread.sleep(2000);`과 같이 해야 한다.

> yield()가 static으로 선언되어 있는 것도 sleep()가 같은 이유이다.

</br>

### interrupt()와 interrupted() - 쓰레드의 작업을 취소한다.

진행 중인 쓰레드의 작업이 끝나기 전에 취소해야할 때가 있다. 예를 들어 큰 파일을 다운로드받을 때 시간이 너무 오래 걸리면 중간에 다운로드를 포기하고 취소할 수 있어야 한다. `interrupt()`는 쓰레드에게 작업을 멈추라고 요청한다. 단지 멈추라고 요청만 하는 것일 뿐 쓰레드를 강제로 종료시키지는 못한다. `interrupt()`는 그저 쓰레드의 `interrupted`상태(인스턴스 변수)를 바꾸는 것일 뿐이다.

그리고 `interrupted()`는 쓰레드에 대해 `interrupt()`가 호출되었는지 알려준다. `interrupt()`가 호출되지 않았다면 false를, `interrupt()`가 호출되었다면 true를 반환한다.

``` java
Thred th = new Thread();
th.start();
    ...
th.interrupt(); // 쓰레드 th에 interrupt()를 호출한다.

class MyThread extends Thread {
    public void run() {
        while(!interrupted()) { // interrupted()의 결과가 false인 동안 반복
            ...
        }
    }
}
```

`interrupt()`가 호출되면, `interrupted()`의 결과가 false에서 true로 바뀌어 while문을 벗어나게 된다. while문의 조건식에 `!`가 포함되어 있다.

`isInterrupted()`도 쓰레드의 `interrupt()`가 호출되었는지 확인하는데 사용할 수 있지만, `interrupted()`와 달리 `isInterrupted()`는 쓰레드의 `interrupted`상태를 false로 초기화하지 않는다.

> **void interrupt()** 쓰레드의 interrupted상태를 false에서 true로 변경   
**boolean isInterrupted()** 쓰레드의 interrupted상태를 반환   
**static boolean interrupted()** 쓰레드의 interrupted상태를 반환 후, false로 변경

쓰레드가 `sleep()`, `wait()`, `join()`에 의해 '일시정지 상태(WAITING)'에 있을 때, 해당 쓰레드에 대해 `interrupt()`를 호출하면, `sleep()`, `wait()`, `join()`에서 `InterruptedException`이 발생하고 쓰레드는 '실행대기 상태(RUNNABLE)'로 바뀐다. 즉, 멈춰있던 쓰레드를 깨워서 실행가능한 상태로 만드는 것이다.

아래는 예제 13- 7을 `interrupt()`와 `interrupted()`를 사용해서 수정한 것으로 카운트다운 도중에 사용자의 입력이 들어오면 카운트다운을 종료한다.

</br>

예제 13-13 / ch13 / ThreadEx13.java

``` java
import javax.swing.JOptionPane;

public class ThreadEx13 {
	public static void main(String[] args) {
		ThreadEx13_1 th1 = new ThreadEx13_1();
		th1.start();
		String input = JOptionPane.showInputDialog("아무 값이나 입력하세요.");
		System.out.println("입력하신 값은 " + input + "입니다.");
		th1.interrupt();	// interrupt()를 호출하면, interrupted상태는 true가 된다.
		System.out.println("isInterrupted() : " + th1.isInterrupted());	// true
	}
}

class ThreadEx13_1 extends Thread {
	public void run() {
		int i = 10;
		
		while(i != 0 && !isInterrupted()) {
			System.out.println(i--);
			for(long x = 0; x < 2500000000L; x++);	// 시간 지연
		}
		System.out.println("카운트가 종료되었습니다.");
	}
}
```

```
10
9
8
7
6
입력하신 값은 abcd입니다.
isInterrupted() : true
카운트가 종료되었습니다.
```

사용자 입력이 끝나자 `interrupt()`에 의해 카운터다운이 중간에 멈추었다.

</br>

예제 13-14 / ch13 / ThreadEx14.java

``` java
import javax.swing.JOptionPane;

public class ThreadEx14 {
	public static void main(String[] args) {
		ThreadEx14_1 th1 = new ThreadEx14_1();
		th1.start();
		
		String input = JOptionPane.showInputDialog("아무 값이나 입력하세요.");
		System.out.println("입력하신 값은 " + input + "입니다.");
		th1.interrupt();	// interrupt()를 호출하면, interrupted상태는 true가 된다.
		System.out.println("isInterrupted() : " + th1.isInterrupted());	// true
	}
}

class ThreadEx14_1 extends Thread {
	public void run() {
		int i = 10;
		
		while(i != 0 && !isInterrupted()) {
			System.out.println(i--);
			try {
				Thread.sleep(1000);	// 1초 지연
			} catch (InterruptedException e) {}
		}
		System.out.println("카운트가 종료되었습니다.");
	}
}
```

```
10
9
8
입력하신 값은 abcd입니다.
isInterrupted() : false ← true일 때도 있음.
7
6
5
4
3
2
1
카운트가 종료되었습니다.
```

이전 예제에서 시간지연을 위해 사용했던 for문 대신 `Thread.sleep(1000)`으로 1초 동안 지연되도록 변경했을 뿐인데, 카운트가 종료되지 않았다.

![image](https://ifh.cc/g/Y2tVRS.png)

그 이유는 `Thread.sleep(1000)`에서 `InterruptedException`이 발생했기 때문이다. `sleep()`에 의해 쓰레드가 잠시 멈춰있을 때, `interrupt()`를 호출하면 `InterruptedException`이 발생되고 쓰레드의 `interrupted`상태는 false로 자동 초기화된다.

![image](https://ifh.cc/g/AN9BMj.png)

그럴 때는 위와 같이 catch블럭에 `interrupt()`를 추가로 넣어줘서 쓰레드의 `interrupted`상태를 true로 다시 바꿔줘야 한다.

</br>

### suspend(), resume(), stop()

`suspend()`는 `sleep()`처럼 쓰레드를 멈추게 한다. `suspend()`에 의해 정지된 쓰레드는 `resume()`을 호출해야 다시 실행대기 상태가 된다. `stop()`은 호출되는 즉시 쓰레드가 종료된다.

`suspend()`, `resume()`, `stop()`은 쓰레드의 실행을 제어하는 가장 손쉬운 방법이지만, `suspend()`와 `stop()`이 교착상태(deadlock)를 일으키기 쉽게 작성되었으므로 사용이 권장되지 않는다. 그래서 이 메소드들은 모두 'deprecated'되었다.

'deprecated'의 의미는 '전에는 사용되었지만, 앞으로 사용하지 않을 것을 권장한다.'이다. 'deprecated'된 메소드는 하위 호환성을 위해서 삭제하지 않는 것일 뿐이므로 사용해서는 안 된다.

</br>

예제 13-15 / ch13 / ThreadEx15.java

``` java
public class ThreadEx15 {
	public static void main(String[] args) {
		RunImplEx15 r = new RunImplEx15();
		Thread th1 = new Thread(r, "*");
		Thread th2 = new Thread(r, "**");
		Thread th3 = new Thread(r, "***");
		th1.start();
		th2.start();
		th3.start();
		
		try {
			Thread.sleep(2000);
			th1.suspend();	// 쓰레드 th1을 잠시 중단시킨다.
			Thread.sleep(2000);
			th2.suspend();
			Thread.sleep(3000);
			th1.resume();	// 쓰레드 th1을 다시 동작하도록 한다.
			Thread.sleep(3000);
			th1.stop();	// 쓰레드 t1을 강제종료시킨다.
			th2.stop();
			Thread.sleep(2000);
			th3.stop();
		} catch (InterruptedException e) {}
	}	// main
}

class RunImplEx15 implements Runnable {
	public void run() {
		while(true) {
			System.out.println(Thread.currentThread().getName());
			try {
				Thread.sleep(1000);
			} catch (InterruptedException e) {}
		}
	}	// run()
}
```

```
*
**
***
*
**
***
**
***
**
***
***
***
***
***
*
***
*
***
*
***
**
```

`suspend()`와 `resume()`, `stop()`의 사용법을 보여주는 예제이다. `sleep(2000)`은 쓰레드를 2초간 멈추게 하지만, 2초 후에 바로 실행상태가 아닌 실행대기상태가 된다.

이 예제는 간단하기 때문에 교착상태가 일어날 일이 없으므로 `suspend()`와 `stop()`을 사용해도 아무런 문제가 없지만, 좀 더 복잡한 경우에는 사용하지 않는 것이 좋다.

그 대신 이 문제를 해결할 다른 방법이 있으니 다음 예제를 보겠다.

</br>

예제 13-16 / ch13 / ThreadEx16.java

``` java
public class ThreadEx16 {
	public static void main(String[] args) {
		RunImplEx16 r1 = new RunImplEx16();
		RunImplEx16 r2 = new RunImplEx16();
		RunImplEx16 r3 = new RunImplEx16();
		Thread th1 = new Thread(r1, "*");
		Thread th2 = new Thread(r2, "**");
		Thread th3 = new Thread(r3, "***");
		th1.start();
		th2.start();
		th3.start();
		
		try {
			Thread.sleep(2000);
			th1.suspend();	// 쓰레드 th1을 잠시 중단시킨다.
			Thread.sleep(2000);
			th2.suspend();
			Thread.sleep(3000);
			th1.resume();	// 쓰레드 th1을 다시 동작하도록 한다.
			Thread.sleep(3000);
			th1.stop();	// 쓰레드 t1을 강제종료시킨다.
			th2.stop();
			Thread.sleep(2000);
			th3.stop();
		} catch (InterruptedException e) {}
	}	// main
}

class RunImplEx16 implements Runnable {
	volatile boolean suspended = false;
	volatile boolean stopped = false;
	
	public void run() {
		while(!stopped) {
			if(!suspended) {
				System.out.println(Thread.currentThread().getName());
				try {
					Thread.sleep(1000);
				} catch (InterruptedException e) {}
			}
		}
		System.out.println(Thread.currentThread().getName() + " - stopped");
	}
	public void suspend() { suspended = true; }
	public void resume() { suspended = false; }
	public void stop() { stopped = true; }
}
```

```
**
*
***
**
*
***
***
*
**
***
**
***
***
***
*
***
*
***
*
***
*
** - stopped
***
* - stopped
***
*** - stopped
```

`stopped`와 `suspended`라는 boolean타입의 두 변수를 인스턴스변수로 선언하고, 이 변수를 사용해서 반복문과 조건문의 조건식을 작성한다. 그리고 이 변수의 값을 변경함으로써 쓰레드의 작업이 중지되었다가 재개되거나 종료되도록 할 수 있다.

``` java
boolean suspended = false;
boolean stopped = false;

public void run() {
	while(!stopped) {	// stopped의 값이 false인 동안 반복한다.
		if(!suspended) {	// suspended의 값이 false일 때만 작업을 수행한다.
			...
```

그리고 각 쓰레드가 다른 실행상태를 가질 수 있어야 하므로, 이전 예제와 달리 하나의 `RunImplEx16`객체를 공유하지 않는다.

만일 이 예제가 잘 동작하지 않는다면, 아래의 오른쪽과 같이 `suspended`와 `stopped`의 선언문 앞에 `volatile`을 붙이면 된다.

![image](https://ifh.cc/g/7vGaK3.png)

</br>

예제 13-17 / ch13 / ThreadEx17.java

``` java
public class ThreadEx17 {
	public static void main(String[] args) {
		ThreadEx17_1 th1 = new ThreadEx17_1("*");
		ThreadEx17_1 th2 = new ThreadEx17_1("**");
		ThreadEx17_1 th3 = new ThreadEx17_1("***");
		th1.start();
		th2.start();
		th3.start();
		
		try {
			Thread.sleep(2000);
			th1.suspend();	// 쓰레드 th1을 잠시 중단시킨다.
			Thread.sleep(2000);
			th2.suspend();
			Thread.sleep(3000);
			th1.resume();	// 쓰레드 th1을 다시 동작하도록 한다.
			Thread.sleep(3000);
			th1.stop();	// 쓰레드 t1을 강제종료시킨다.
			th2.stop();
			Thread.sleep(2000);
			th3.stop();
		} catch (InterruptedException e) {}
	}	// main
}

class ThreadEx17_1 implements Runnable {
	volatile boolean suspended = false;
	volatile boolean stopped = false;
	
	Thread th;
	
	ThreadEx17_1(String name) {
		th = new Thread(this, name);	// Thread(Runnable r, String name)
	}
	
	public void run() {
		while(!stopped) {
			if(!suspended) {
				System.out.println(Thread.currentThread().getName());
				try {
					Thread.sleep(1000);
				} catch (InterruptedException e) {}
			}
		}
		System.out.println(Thread.currentThread().getName() + " - stopped");
	}
	public void suspend() { suspended = true; }
	public void resume() { suspended = false; }
	public void stop() { stopped = true; }
	public void start() { th.start();	}
}
```

이전 예제를 보다 객체지향적으로 코드를 정리하였다.

</br>

### yield() - 다른 쓰레드에게 양보한다.

`yield()`는 쓰레드 자신에게 주어진 실행시간을 다음 차례의 쓰레드에게 양보(yield)한다.

예를 들어 스케줄러에 의해 1초의 실행시간을 할당받은 쓰레드가 0.5초의 시간동안 작업한 상태에서 `yield()`가 호출되면, 나머지 0.5초는 포기하고 다시 실행대기상태가 된다.

`yield()`와 `interrupt()`를 적절히 사용하면, 프로그램의 응답성도 높이고 보다 효율적인 실행이 가능하게 할 수 있다.

</br>

예제 13-18 / ch13 / ThreadEx18.java

``` java
public class ThreadEx18 {
	public static void main(String[] args) {
		ThreadEx18_1 th1 = new ThreadEx18_1("*");
		ThreadEx18_1 th2 = new ThreadEx18_1("**");
		ThreadEx18_1 th3 = new ThreadEx18_1("***");
		th1.start();
		th2.start();
		th3.start();
		
		try {
			Thread.sleep(2000);
			th1.suspend();	// 쓰레드 th1을 잠시 중단시킨다.
			Thread.sleep(2000);
			th2.suspend();
			Thread.sleep(3000);
			th1.resume();	// 쓰레드 th1을 다시 동작하도록 한다.
			Thread.sleep(3000);
			th1.stop();	// 쓰레드 t1을 강제종료시킨다.
			th2.stop();
			Thread.sleep(2000);
			th3.stop();
		} catch (InterruptedException e) {}
	}	// main
}

class ThreadEx18_1 implements Runnable {
	volatile boolean suspended = false;
	volatile boolean stopped = false;
	
	Thread th;
	
	ThreadEx18_1(String name) {
		th = new Thread(this, name);	// Thread(Runnable r, String name)
	}
	
	public void run() {
		String name = th.getName();
		
		while(!stopped) {
			if(!suspended) {
				System.out.println(name);
				try {
					Thread.sleep(1000);
				} catch (InterruptedException e) {
					System.out.println(name + " - interrupted");
				}
			} else {
				Thread.yield();
			}
		}
		System.out.println(name + " - stopped");
	}
	public void suspend() {
		suspended = true;
		th.interrupt();
		System.out.println(th.getName() + " - interrupt() by suspend()");
	}
	public void stop() {
		stopped = true;
		th.interrupt();
		System.out.println(th.getName() + " - interrupt() by stop()");
	}
	public void resume() { suspended = false; }
	public void start() { th.start();	}
}
```

```
*
***
**
**
***
*
* - interrupt() by suspend()
**
* - interrupted
***
**
***
** - interrupt() by suspend()
** - interrupted
***
***
***
*
***
*
***
*
***
* - interrupt() by stop()
** - interrupt() by stop()
* - interrupted
** - stopped
* - stopped
***
***
*** - interrupt() by stop()
*** - interrupted
*** - stopped
```

이 전의 예제에 `yield()`와 `interrupt()`를 추가해서 예제의 효율과 응답성을 향상시켰다. 먼저 아래의 코드를 보면 if문에 `yield()`를 호출하는 else블럭이 추가되었다.

![image](https://ifh.cc/g/G8KRxO.png)

왼쪽 코드에서 만일 `suspended`의 값이 true라면, 즉 잠시 실행을 멈추게 한 상태라면, 쓰레드는 주어진 실행시간을 그저 while문을 의미없이 돌면서 낭비하게 될 것이다. 이런 상황을 '바쁜 대기상태(busy-waiting)'이라고 한다.

그러나 오른쪽 코드는, 같은 경우에 `yield()`를 호출해서 남은 실행시간을 while문에서 낭비하지 않고 다른 쓰레드에게 양보(yield)하게 되므로 더 효율적이다. 또 한 가지 달라진 부분은 `suspend()`와 `stop()`인데, `interrupt()`를 호출하는 코드를 추가했다.

![image](https://ifh.cc/g/MDVyz1.png)

만일 `stop()`이 호출되었을 때 `Thread.sleep(1000)`에 의해 쓰레드가 일시정지 상태에 머물러 있는 상황이라면, `stopped`의 값이 true로 바뀌었어도 쓰레드가 정지될 때까지 최대 1초의 시간지연이 생길 것이다.

``` java
while(!stopped) {
	if(!suspended) {
			...
		try {
			Thread.sleep(1000);	// interrupt()가 호출되면, 예외가 발생된다.
		} catch (InterruptedException e) {
			System.out.println(name + " - interrupted");
		}
	} else {
		Thread.yield();
	}
}
```

그러나 같은 상황에서 `interrupt()`를 호출하면, `sleep()`에서 `interruptedException`이 발생하여 즉시 일시정지 상태에서 벗어나게 되므로 응답성이 좋아진다.

</br>

### join() - 다른 쓰레드의 작업을 기다린다.

쓰레드 자신이 하던 작업을 잠시 멈추고 다른 쓰레드가 지정된 시간동안 작업을 수행하도록 할 때 `jOin()`을 사용한다.

``` java
void join()
void join(long millis)
void join(long millis, int nanos)
```

시간을 지정하지 않으면, 해당 쓰레드가 자겅ㅂ을 모두 마칠 때까지 기다리게 된다. 작업 중에 다른 쓰레드의 작업이 먼저 수행되어야할 필요가 있을 때 `join()`을 사용한다.

``` java
try {
	th1.join();	// 현재 실행중인 쓰레드가 쓰레드 th1의 작업이 끝날때까지 기다린다.
} catch(InterruptedException e) {}
```

`join()`도 `sleep()`처럼 `interrupt()`에 의해 대기상태에서 벗어날 수 있으며, `join()`이 호출되는 부분을 try-catch문으로 감싸야 한다. `join()`은 여러모로 `sleep()`과 유사한 점이 많은데, `sleep()`과 다른 점은 `join()`은 현재 쓰레드가 아닌 특정 쓰레드에 대해 동작하므로 static메소드가 아니다.

> join()은 자신의 작업 중간에 다른 쓰레드와 작업을 참여(join)시킨다는 의미로 이름 지어진 것이다.

</br>

예제 13-19 / ch13 / ThreadEx19.java

``` java
public class ThreadEx19 {
	static long startTime = 0;
	
	public static void main(String[] args) {
		ThreadEx19_1 th1 = new ThreadEx19_1();
		ThreadEx19_2 th2 = new ThreadEx19_2();
		th1.start();
		th2.start();
		startTime = System.currentTimeMillis();
		
		try {
			th1.join();	// main쓰레드가 th1의 작업이 끝날 때까지 기다린다. 
			th2.join();	// main쓰레드가 th1의 작업이 끝날 때까지 기다린다. 
		} catch (InterruptedException e) {}
		
		System.out.print("소요시간 : " + (System.currentTimeMillis() - ThreadEx19.startTime));
	}	// main
}

class ThreadEx19_1 extends Thread {
	public void run() {
		for(int i = 0; i < 300; i++) {
			System.out.print(new String("-"));
		}
	}	// run()
}

class ThreadEx19_2 extends Thread {
	public void run() {
		for(int i = 0; i < 300; i++) {
			System.out.print(new String("|"));
		}
	}	// run()
}
```

```
-------|||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||-------------------------------------------------------||||||||||--------------------------------------------------------------------------------------------------------------------------------------------||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||------------|||||||||||---------------------------------------------------------------------------------||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||-----||||||||||||||||||||||||||||||||||||소요시간 : 28
```

`join()`을 사용하지 않았으면 `main`쓰레드는 바로 종료되었겠지만, `join()`으로 쓰레드 `th1`의 작업을 마칠 때까지 `main`쓰레드가 기다리도록 했다. 그래서 `main`쓰레드가 두 쓰레드의 작업에 소요된 시간을 출력할 수 있다.

</br>

예제 13-20 / ch13 / ThreadEx20.java

``` java
class ThreadEx20 {
	public static void main(String[] args) {
		ThreadEx20_1 gc = new ThreadEx20_1();
		gc.setDaemon(true);
		gc.start();
		
		int requireMemory = 0;
		
		for(int i = 0; i < 20; i++) {
			requireMemory = (int)(Math.random() * 10) * 20;
			
			// 필요한 메모리가 사용할 수 있는 양보다 크거나 전체 메모리의 60%이상을
			// 사용했을 경우 gc를 깨운다.
			if(gc.freeMemory() < requireMemory || gc.freeMemory() < gc.totalMemory() * 0.4) {
				gc.interrupt();	// 잠자고 있는 쓰레드 gc를 깨운다.
			}
			
			gc.usedMemory += requireMemory;
			System.out.println("usedMemory : " + gc.usedMemory);
		}
	}
}

class ThreadEx20_1 extends Thread {
	final static int MAX_MEMORY = 1000;
	int usedMemory = 0;
	
	public void run() {
		while(true) {
			try {
				Thread.sleep(10 * 1000);	// 10초를 기다린다.
			} catch (InterruptedException e) {
				System.out.println("Awaken by interrupt().");
			}
			
			gc();	// garbage collection을 수행한다.
			System.out.println("Garbage Collected. Free Memory : " + freeMemory());
		}
	}
	
	public void gc() {
		usedMemory -= 300;
		if(usedMemory < 0) usedMemory = 0;
	}
	public int totalMemory() { return MAX_MEMORY; }
	public int freeMemory() { return MAX_MEMORY - usedMemory; }
}
```

```
usedMemory : 40
usedMemory : 200
usedMemory : 260
usedMemory : 320
usedMemory : 480
usedMemory : 520
usedMemory : 540
usedMemory : 680
usedMemory : 860
usedMemory : 980
usedMemory : 1040
usedMemory : 1040
usedMemory : 1080
usedMemory : 1100
usedMemory : 1220
Awaken by interrupt().
usedMemory : 1360
Garbage Collected. Free Memory : -60
Awaken by interrupt().
usedMemory : 1220
usedMemory : 1100
Garbage Collected. Free Memory : 80
usedMemory : 1260
Awaken by interrupt().
usedMemory : 1340
Garbage Collected. Free Memory : -40
Awaken by interrupt().
Garbage Collected. Free Memory : 260
```

이 예제는 JVM의 가비지 컬렉터(garbage collector)을 흉내 내어 간단히 구현해 본 것이다. `random()`을 사용했기 때문에 실행할 때마다 결과가 다를 수 있다.

먼저 `sleep()`을 이용해서 10초마다 한 번씩 가비지 컬렉션을 수행하는 쓰레드를 만든 다음, 쓰레드를 생성해서 데몬 쓰레드로 설정하였다.

``` java
public void run() {
	while(true) {
		try {
			Thread.sleep(10 * 1000);	// 10초를 기다린다.
		} catch (InterruptedException e) {
			System.out.println("Awaken by interrupt().");
		}
		
		gc();	// garbage collection을 수행한다.
		System.out.println("Garbage Collected. Free Memory : " + freeMemory());
	}
}
```

반복문을 사용해서 메모리의 양을 계속 감소시키도록 했고, 매 반복마다 if문으로 메모리를 확인해서 남은 메모리가 전체 메모리의 40% 미만일 경우에 `interrupt()`를 호출해서 즉시 가비지 컬렉터 쓰레드를 깨워서 `gc()`를 수행하도록 하였다.

``` java
for(int i = 0; i < 20; i++) {
	requireMemory = (int)(Math.random() * 10) * 20;
	
	// 필요한 메모리가 사용할 수 있는 양보다 크거나 전체 메모리의 60%이상을 사용했을 경우 gc를 깨운다.
	if(gc.freeMemory() < requireMemory || gc.freeMemory() < gc.totalMemory() * 0.4) {
		gc.interrupt();	// 잠자고 있는 쓰레드 gc를 깨운다.
	}
	
	gc.usedMemory += requireMemory;
	System.out.println("usedMemory : " + gc.usedMemory);
}
```

그러나 예제의 실행결과를 보면 `MAX_MEMORY`가 1000임에도 불구하고 `usedMemory`의 값이 1000을 넘는 것을 알 수 있다. 이것은 쓰레드 `gc`가 `interrupt()`에 의해서 깨어났음에도 불구하고 `gc()`가 수행되기 이전에 `main`쓰레드의 작업이 수행되어 메모리를 사용하기 때문이다. 그래서 쓰레드 `gc`를 깨우는 것뿐만 아니라 `join()`을 이용해서 쓰레드 `gc`가 작업할 시간을 어느 정도 주고 `main`쓰레드가 기다리도록 해서, 사용할 수 있는 메모리가 확보된 다음에 작업을 계속 하는 것이 필요하다.

![image](https://ifh.cc/g/zbPQGa.png)

그래서 위의 왼쪽의 코드를 오른쪽과 같이 `join()`을 호출해서 쓰레드 `gc`가 0.1초 동안 수행될 수 있도록 변경해야 한다.

가비지 컬렉터와 같은 데몬 쓰레드의 우선순위를 낮추기 보다는 `sleep()`을 이용해서 주기적으로 실행되도록 하다가 필요할 때마다 `interrupt()`를 호출해서 즉시 가비지 컬렉션이 이루어지도록 하는 것이 좋다. 그리고 필요하다면 `join()`을 함꼐 사용해야한다.