Chapter 13. 쓰레드 thread

# 2. 쓰레드의 구현과 실행

쓰레드를 구현하는 방법은 `Thread`클래스를 상속받는 방법과 `Runnable`인터페이스를 구현하는 방법, 모두 두 가지가 있다. 어느 쪽을 선택해도 별 차이는 없지만 `Thread`클래스를 상속받으면 다른 클래스를 상속받을 수 없기 때문에, `Runnable`인터페이스를 구현하는 방법이 일반적이다.

`Runnable`인터페이스를 구현하는 방법은 재사용성(reusability)이 높고 코드의 일관성(consistency)을 유지할 수 있기 때문에 보다 객체지향적인 방법이라 할 수 있겠다.

![image](https://ifh.cc/g/tVmLR7.png)

`Runnable`인터페이스는 오로지 `run()`만 정의되어 있는 간단한 인터페이스이다. `Runnable`인터페이스를 구현하기 위해서 해야 할 일은 추상메소드인 `run()`의 몸통{}을 만들어 주는 것이다.

``` java
public interface Runnable {
    public abstract void run();
}
```

쓰레드를 구현한다는 것은, 위의 두 방법 중 어떤 것을 선택하든지, 그저 쓰레드를 통해 작업하고자 하는 내용으로 `run()`의 몸통{}을 채우는 것이다.

</br>

예제 13-1 / ch13 / ThreadEx1.java

``` java
public class ThreadEx1 {
	public static void main(String[] args) {
		ThreadEx1_1 t1 = new ThreadEx1_1();
		
		Runnable r = new ThreadEx1_2();
		Thread t2 = new Thread(r);	// 생성자 Thread(Runnable target)
		
		t1.start();
		t2.start();
	}
}

class ThreadEx1_1 extends Thread {
	public void run() {
		for(int i = 0; i < 5; i++) {
			System.out.println(getName());	// 조상인 Thread의 getName()을 호출
		}
	}
}

class ThreadEx1_2 implements Runnable {
	public void run() {
		for(int i = 0; i < 5; i++) {
			// Thread.currentThread() - 현재 실행중인 Thread를 반환한다.
			System.out.println(Thread.currentThread().getName());
		}
	}
}
```

```
Thread-0
Thread-0
Thread-0
Thread-0
Thread-0
Thread-1
Thread-1
Thread-1
Thread-1
Thread-1
```

`Thread`클래스를 상속받은 경우와 `Runnable`인터페이스를 구현한 경우의 인스턴스 생성 방법이 다르다.

``` java
ThreadEx1_1 t1 = new ThreadEx1_1(); // Thread의 자손 클래스의 인스턴스를 생성

Runnable r = new ThreadEx1_2(); // Runnable을 구현한 클래스의 인스턴스를 생성
Thread t2 = new Thread(r);   // 생성자 Thread(Runnable target)

Thread t2 = new Thread(new ThreadEx1_2());  // 위의 두 줄을 한 줄로 간단히
```

`Runnable`인터페이스를 구현한 경우, `Runnable`인터페이스를 구현한 클래스의 인스턴스를 생성한 다으므, 이 인스턴스를 `Thread`클래스의 생성자의 매개변수로 제공해야 한다.

아래의 코드는 실제 `Thread`클래스의 소스코드(Thread.java)를 이해하기 쉽게 수정한 것인데, 인스턴스변수로 `Runnable`타입의 변수 `r`을 선언해 놓고 생성자를 통해서 `Runnable`인터페이스를 구현한 인스턴스를 참조하도록 되어 있는 것을 확인할 수 있다.

그리고 `run()`을 호출하면 참조변수 `r`을 통해서 `Runnable`인터페이스를 구현한 인스턴스의 `run()`이 호출된다. 이렇게 함으로써 상속을 통해 `run()`을 오버라이딩하지 않고도 외부로부터 `run()`을 제공받을 수 있다.

``` java
public class Thread {
    private Runnable r; // Runnable을 구현한 클래스의 인스턴스를 참조하기 위한 변수

    public Thread(Runnable r) {
        this.r = r;
    }

    public void run() {
        if(r != null)
            r.run();    // Runnable인터페이스를 구현한 인스턴스의 run()을 호출
    }
    ...
}
```

`Thread`클래스를 상속받으면, 자손 클래스에서 조상인 `Thread`클래스의 메소드를 직접 호출할 수 있지만, `Runnable`을 구현하면 `Thread`클래스의 static메소드인 `currentThread()`를 호출하여 쓰레드의 대한 참조를 얻어 와야만 호출이 가능하다.

> **static Thread currentThread()** 현재 실행중인 쓰레드의 참조를 반환한다.   
> **String getName()** 쓰레드의 이름을 반환한다.

그래서 `Thread`를 상속받은 `ThreadEx1_1`에서는 간단히 `getName()`을 호출하면 되지만, `Runnable`을 구현한 `ThreadEx1_2`에는 멤버라고는 `run()`밖에 없기 때문에 `Thread`클래스의 `getName()`을 호출하려면, `Thread.currentThread().getName()`와 같이 해야 한다.

``` java
class ThreadEx1_1 extends Thread {
	public void run() {
		for(int i = 0; i < 5; i++) {
			System.out.println(getName());	// 조상인 Thread의 getName()을 호출
		}
	}
}

class ThreadEx1_2 implements Runnable {
	public void run() {
		for(int i = 0; i < 5; i++) {
			// Thread.currentThread() - 현재 실행중인 Thread를 반환한다.
			System.out.println(Thread.currentThread().getName());
		}
	}
}
```

참고로 쓰레드의 이름은 다음과 같이 생성자나 메소드를 통해서 지정 또는 변경할 수 있다.

``` java
Thread(Runnable target, String name)
Thread(String name)
void setName(String name)
```

쓰레드의 이름을 지정하지 않으면 `Thread-번호`의 형식으로 이름이 정해진다.

그리고 `System.out.println(Thread.currentThread().getName())`는 아래의 코드를 한 줄로 줄여 쓴 것이다.

``` java
Thread t = Thread.currentThread();
String name = t.getName();
System.out.println(name);
```

</br>

### 쓰레드의 실행 - start()

쓰레드를 생성했다고 해서 자동으로 실행되는 것은 아니다. `start()` 호출해야만 쓰레드가 실행된다.

``` java
t1.start(); // 쓰레드 t1을 실행시킨다.
t2.start(); // 쓰레드 t2을 실행시킨다.
```

사실은 `start()`가 호출되었다고 해서 바로 실행되는 것이 아니라, 일단 실행대기 상태에 있다가 자신의 차례가 되어야 실행된다. 물론 실행대기중인 쓰레드가 하나도 없으면 곧바로 실행상태가 된다.

> 쓰레드의 실행순서는 OS의 스케줄러가 작성한 스케줄에 의해 결정된다.

한 번 실행이 종료된 쓰레드는 다시 실행할 수 없다. 즉, 하나의 쓰레드에 대해 `start()`가 한 번만 호출될 수 있다.

그래서 만일 쓰레드의 작업을 한 번 더 수행해야 한다면 아래의 오른쪽 코드와 같이 새로운 쓰레드를 생성한 다음에 `start()`를 호출해야 한다. 만일 아래의 왼쪽 코드처럼 하나의 쓰레드에 대해 `start()`를 두 번 이상 호출하면 실행시에 `IllegalThreadStateException`이 발생한다.

![image](https://ifh.cc/g/29NwNN.png)