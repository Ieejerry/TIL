Chapter 13. 쓰레드 Thread

# 7. 데몬 쓰레드(daemon thread)

데몬 쓰레드는 다른 일반 쓰레드(데몬 쓰레드가 아닌 쓰레드)의 작업을 돕는 보조적인 역할을 수행하는 쓰레드이다. 일반 쓰레드가 모두 종료되면 데몬 쓰레드는 강제적으로 자동종료되는데, 그 이유는 데몬 쓰레드는 일반 쓰레드의 보조역할을 수행하므로 일반 쓰레드가 모두 종료되고 나면 데몬 쓰레드의 존재의 의미가 없기 때문이다.

이 점을 제외하고는 데몬 쓰레드와 일반 쓰레드는 다르지 않다. 데몬 쓰레드의 예로는 가비지 컬렉터, 위드프로세서의 자동저장, 화면자동갱신 등이 있다.

데몬 쓰레드는 무한루프와 조건문을 이용해서 실행 후 대기하고 있다가 특정 조건이 만족되면 작업을 수행하고 다시 대기하도록 작성한다.

데몬 쓰레드는 일반 쓰레드의 작성방법과 실행방법이 같으며 다만 쓰레드를 생성한 다음 실행하기 전에 `setDaemon(true)`를 호출하기만 하면 된다. 그리고 데몬 쓰레드가 생성한 쓰레드는 자동적으로 데몬 쓰레드가 된다.

> **boolean isDaemon()** 쓰레드가 데몬 쓰레드인지 확인한다. 데몬 쓰레드이면 true를 반환한다.   
> **void setDaemon(boolean on)** 쓰레드를 데몬 쓰레드로 또는 사용자 쓰레드로 변경한다. 매개변수 on의 값을 true로 지정하면 데몬 쓰레드가 된다.

</br>

예제 13-10 / ch13 / ThreadEx10.java

``` java
public class ThreadEx10 implements Runnable {
	static boolean autoSave = false;
	
	public static void main(String[] args) {
		Thread t = new Thread(new ThreadEx10());
		t.setDaemon(true);	// 이 부분이 없으면 종료되지 않는다.
		t.start();
		
		for(int i = 1; i < 10; i++) {
			try {
				Thread.sleep(1000);
			} catch (InterruptedException e) {}
			System.out.println(i);
			
			if(i == 5) autoSave = true;
		}
		
		System.out.println("프로그램을 종료합니다.");
	}
	
	public void run() {
		while(true) {
			try {
				Thread.sleep(3 * 1000);	// 3초마다
			} catch (InterruptedException e) {}
			
			// autoSave의 값이 true이면 autoSave()를 호출한다.
			if(autoSave) autoSave();
		}
	}
	
	public void autoSave() {
		System.out.println("작업파일이 자동저장되었습니다.");
	}
}
```

```
1
2
3
4
5
작업파일이 자동저장되었습니다.
6
7
8
작업파일이 자동저장되었습니다.
9
10
프로그램을 종료합니다.
```

3초마다 변수 `autoSave`의 값을 확인해서 그 값이 true이면, `autoSave()`를 호출하는 일을 무한히 반복하도록 쓰레드를 작성하였다. 만일 이 쓰레드를 데몬 쓰레드로 설정하지 않았다면, 이 프로그램은 강제종료되지 않는 한 영원히 종료되지 않는다.

``` java
Thread t = new Thread(new ThreadEx10());

t.setDaemon(true);	// 이 부분이 없으면 종료되지 않는다.
t.start();
```

`setDaemon`메소드는 반드시 `start()`를 호출하기 전에 실행되어야 한다. 그렇지 않으면 `IllegalThreadStateException`이 발생한다.

</br>

예제 13-11 / ch13 / ThreadEx11.java

``` java
import java.util.*;

public class ThreadEx11 {
	public static void main(String[] args) {
		ThreadEx11_1 t1 = new ThreadEx11_1("Thread1");
		ThreadEx11_2 t2 = new ThreadEx11_2("Thread2");
		t1.start();
		t2.start();
	}
}

class ThreadEx11_1 extends Thread {
	ThreadEx11_1(String name) {
		super(name);
	}
	
	public void run() {
		try {
			sleep(5 * 1000);	// 5초 동안 기다린다.
		} catch (InterruptedException e) {}
	}
}

class ThreadEx11_2 extends Thread {
	ThreadEx11_2(String name) {
		super(name);
	}
	
	public void run() {
		Map map = getAllStackTraces();
		Iterator it = map.keySet().iterator();
		
		int x = 0;
		while(it.hasNext()) {
			Object obj = it.next();
			Thread t = (Thread)obj;
			StackTraceElement[] ste = (StackTraceElement[])(map.get(obj));
			
			System.out.println("[" + ++x + "] name : " + t.getName() + ", group : " + t.getThreadGroup().getName() + ", daemon : " + t.isDaemon());
			
			for(int i = 0; i < ste.length; i++) {
				System.out.println(ste[i]);
			}
			
			System.out.println();
		}
	}
}
```

```
[1] name : Reference Handler, group : system, daemon : true
java.base@17.0.3/java.lang.ref.Reference.waitForReferencePendingList(Native Method)
java.base@17.0.3/java.lang.ref.Reference.processPendingReferences(Reference.java:253)
java.base@17.0.3/java.lang.ref.Reference$ReferenceHandler.run(Reference.java:215)

[2] name : Finalizer, group : system, daemon : true
java.base@17.0.3/java.lang.Object.wait(Native Method)
java.base@17.0.3/java.lang.ref.ReferenceQueue.remove(ReferenceQueue.java:155)
java.base@17.0.3/java.lang.ref.ReferenceQueue.remove(ReferenceQueue.java:176)
java.base@17.0.3/java.lang.ref.Finalizer$FinalizerThread.run(Finalizer.java:172)

[3] name : Signal Dispatcher, group : system, daemon : true

[4] name : Thread1, group : main, daemon : false
java.base@17.0.3/java.lang.Thread.sleep(Native Method)
app//ThreadEx11_1.run(ThreadEx11.java:19)

[5] name : Common-Cleaner, group : InnocuousThreadGroup, daemon : true
java.base@17.0.3/java.lang.Object.wait(Native Method)
java.base@17.0.3/java.lang.ref.ReferenceQueue.remove(ReferenceQueue.java:155)
java.base@17.0.3/jdk.internal.ref.CleanerImpl.run(CleanerImpl.java:140)
java.base@17.0.3/java.lang.Thread.run(Thread.java:833)
java.base@17.0.3/jdk.internal.misc.InnocuousThread.run(InnocuousThread.java:162)

[6] name : Attach Listener, group : system, daemon : true

[7] name : Thread2, group : main, daemon : false
java.base@17.0.3/java.lang.Thread.dumpThreads(Native Method)
java.base@17.0.3/java.lang.Thread.getAllStackTraces(Thread.java:1662)
app//ThreadEx11_2.run(ThreadEx11.java:30)

[8] name : Notification Thread, group : system, daemon : true
```

`getAllStackTraces()`를 이용하면 실행 중 또는 대기상태, 즉 작업이 완료되지 않은 모든 쓰레드의 호출스택을 출력할 수 있다. 결과를 보면 `getAllStackTraces()`가 호출되었을 때, 새로 생성한 `Thread1`, `Thread2`를 포함해서 모두 8개의 쓰레드가 실행 중 또는 대기상태에 있다는 것을 알 수 있다.

프로그램을 실행하면, JVM은 가비지컬렉션, 이벤트처리, 그래픽처리와 같이 프로그램이 실행되는 데 필요한 보조작업을 수행하는 데몬 쓰레드들을 자동적으로 생성해서 실행시킨다. 그리고 이 들은 `system쓰레드 그룹` 또는 `main쓰레드 그룹`에 속한다.

AWT나 Swing과 같이 GUI를 가진 프로그램을 실행하는 경우에는 이벤트와 그래픽처리를 위해 더 많은 수의 데몬 쓰레드가 생성된다.

> main쓰레드는 이미 종료되었기 때문에 결과에 포함되지 않았다.

> GUI는 Graphic User Interface의 약자로 Java에서는 AWT나 Swing을 이용해서 GUI를 가진 프로그램을 작성할 수 있다. JavaFX라는 보다 발전된 GUI기술도 있지만, 실무에서는 거의 사용하지 않는다.