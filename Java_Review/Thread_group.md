Chapter 13. 쓰레드 Thread

# 6. 쓰레드 그룹(thread group)

쓰레드 그룹은 서로 관련된 쓰레드를 그룹으로 다루기 위한 것으로, 폴더를 생성해서 관련된 파일들을 함께 넣어서 관리하는 것처럼 쓰레드 그룹을 생성해서 쓰레드를 그룹으로 묶어서 관리할 수 있다.

또한 폴더 안에 폴더를 생성할 수 있듯이 쓰레드 그룹에 다른 쓰레드 그룹을 포함시킬 수 있다. 사실 쓰레드 그룹은 보안상의 이유로 도입된 개념으로, 자신이 속한 쓰레드 그룹이나 하위 쓰레드 그룹은 변경할 수 있지만 다른 쓰레드 그룹의 쓰레드를 변경할 수는 없다. `ThreadGroup`을 사용해서 생성할 수 있으며, 주요 생성자와 메소드는 다음과 같다.

![image](https://ifh.cc/g/bkzorM.png)

쓰레드를 쓰레드 그룹에 포함시키려면 `Thread`의 생성자를 이용해야 한다.

``` java
Thread(ThreadGroup group, String name)
Thread(ThreadGroup group, Runnable target)
Thread(ThreadGroup group, Runnable target, String name)
Thread(ThreadGroup group, Runnable target, String name, long stackSize)
```

모든 쓰레드는 반드시 쓰레드 그룹에 포함되어 있어야 하기 때문에, 위와 같이 쓰레드 그룹을 지정하는 생성자를 사용하지 않은 쓰레드는 기본적으로 자신을 생성한 쓰레드와 같은 쓰레드 그룹에 속하게 된다.

자바 어플리케이션이 실해되면, JVM은 `main`과 `system`이라는 쓰레드 그룹을 만들고 JVM운영에 필요한 쓰레드들을 생성해서 이 쓰레드 그룹에 포함시킨다. 예를 들어 `main`메소드를 수행하는 `main`이라는 이름의 쓰레드는 `main`쓰레드 그룹에 속하고, 가비지컬렉션을 수행하는 `Finalizer`쓰레드는 `system`쓰레드 그룹에 속한다.

우리가 생성하는 모든 쓰레드 그룹은 `main`쓰레드 그룹의 하위 쓰레드 그룹이 되며, 쓰레드 그룹을 지정하지 않고 생성한 쓰레드는 자동적으로 `main`쓰레드 그룹에 속하게 된다.

그 외에 `Thread`의 쓰레드 그룹과 관련된 메소드는 다음과 같다.

``` java
ThreaGroup getThreadGroup() // 쓰레드 자신이 속한 쓰레드 그룹을 반환한다.
void uncaughtException(Thread t, Throwable e)   // 쓰레드 그룹의 쓰레드가 처리되지 않은 예외에 의해 실행이 종료되었을 때, JVM에 의해 이 메소드가 자동적으로 호출된다.
```

</br>

예제 13-9 / ch13 / ThreadEx9.java

``` java
public class ThreadEx9 {
	public static void main(String[] args) {
		ThreadGroup main = Thread.currentThread().getThreadGroup();
		ThreadGroup grp1 = new ThreadGroup("Group1");
		ThreadGroup grp2 = new ThreadGroup("Group2");
		
		// ThreadGroup(ThreadGroup parent, String name)
		ThreadGroup subGrp1 = new ThreadGroup(grp1, "subGroup1");
		
		grp1.setMaxPriority(3);	// 쓰레드 그룹 grp1의 최대우선순위를 3으로 변경.
		
		Runnable r = new Runnable() {
			public void run() {
				try {
					Thread.sleep(1000);	// 쓰레드를 1초간 멈추게 한다.
				} catch (InterruptedException e) {}
			}
		};
		
		// Thread(ThreadGroup tg, Runnable r, String name)
		new Thread(grp1, r, "th1").start();
		new Thread(subGrp1, r, "th2").start();
		new Thread(grp2, r, "th3").start();
		
		System.out.println(">>List of ThreadGroup : " + main.getName() + ", Active ThreadGroup : " + main.activeGroupCount() + ", Active Thread : " + main.activeCount());
		main.list();
	}
}
```

```
>>List of ThreadGroup : main, Active ThreadGroup : 3, Active Thread : 4
java.lang.ThreadGroup[name=main,maxpri=10]
    Thread[main,5,main]
    java.lang.ThreadGroup[name=Group1,maxpri=3]
        Thread[th1,3,Group1]
        java.lang.ThreadGroup[name=subGroup1,maxpri=3]
            Thread[th2,3,subGroup1]
    java.lang.ThreadGroup[name=Group2,maxpri=10]
        Thread[th3,5,Group2]
```

쓰레드 그룹과 쓰레드를 생성하고 `main.list()`를 호출해서 `main`쓰레드 그룹의 정보를 출력하는 예제이다. 쓰레드 그룹에 대한 정보를 출력하기도 전에 쓰레드가 종료될 수 있으므로, `sleep()`을 호출하여 1초간 멈추게 하였다.

``` java
Runnable r = new Runnable() {
    public void run() {
        try {
            Thread.sleep(1000);	// 쓰레드를 1초간 멈추게 한다.
        } catch (InterruptedException e) {}
    }
};

new Thread(grp1, r, "th1").start();
```

결과르 ㄹ보면 쓰레드 그룹에 포함된 하위 쓰레드 그룹이나 쓰레드는 들여쓰기를 이용해서 구별되도록 하였음을 알 수 있다.

새로 생성한 모든 쓰레드 그룹은 `main`쓰레드 그룹의 하위 쓰레드 그룹으로 포함되어 있다는 것과 `setMaxPriority()`는 쓰레드가 쓰레드 그룹에 추가되기 이전에 호출되어야 하며, 쓰레드 그룹 `grp1`의 최대우선순위를 3으로 했기 때문에, 후에 여기에 속하게 된 쓰레드 그룹과 쓰레드가 영향을 받았다.

그리고 참조변수 없이 쓰레드를 생성해서 바로 실행시켰는데, 그렇다고 해서 이 쓰레드가 가비지 컬렉션의 제거 대상이 되지는 않는다. 이 쓰레드의 참조가 `ThreadGroup`에 저장되어 있기 때문이다.

![image](https://ifh.cc/g/POOqOl.png)

> 쓰레드 그룹을 지정하지 않은 쓰레드는 자동적으로 main쓰레드 그룹에 속하게 된다.