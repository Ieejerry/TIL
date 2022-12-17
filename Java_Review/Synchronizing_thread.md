Chapter 13. 쓰레드 Thread

# 9. 쓰레드의 동기화

멀티쓰레드 프로세스의 경우 여러 쓰레드가 같은 프로세스 내의 자원을 공유해서 작업을 하기 때문에 서로의 작업에 영향을 주게 된다. 만일 쓰레드A가 작업하던 도중에 다른 쓰레드B에게 제어권이 넘어갔을 때, 쓰레드A가 작업하던 공유데이터를 쓰레드B가 임의로 변경하였다면, 다시 쓰레드A가 제어권을 받아서 나머지 작업을 마쳤을 때 원래 의도했던 것과는 다른 결과를 얻을 수 있다.

이러한 일이 발생하는 것을 방지하기 위해서 한 쓰레드가 특정 작업을 끝마치기 전까지 다른 쓰레드에 의해 방해받지 않도록 하는 것이 필요하다. 그래서 도입된 개념이 바로 '임계 영역(critical section)'과 '잠금(락, lock)'dlek.

공유 데이터를 사용하는 코드 영역을 임계 영역으로 지정해놓고, 공유 데이터(객체)가 가지고 있는 `lock`을 획득한 단 하나의 쓰레드만 이 영역 내의 코드를 수행할 수 있게 한다. 그리고 해당 쓰레드가 임계 영역 내의 모든 코드를 수행하고 벗어나서 `lock`을 반납해야만 다른 쓰레드가 반납된 `lock`을 획득하여 임계 영역의 코드를 수행할 수 있게 된다.

이처럼 **한 쓰레드가 진행 중인 작업을 다른 쓰레드가 간섭하지 못하도록 막는 것을 '쓰레드의 동기화(synchronization)'** 라고 한다.

자바에서는 `synchronized`블럭을 이용해서 쓰레드의 동기화를 지원했지만, JDK1.5부터는 `java.util.concurrent.locks`와 `java.util.concurrent.atomic`패키지를 통해서 다양한 방식으로 동기화를 구현할 수 있도록 지원하고 있다.

</br>

## 9.1 synchronized를 이용한 동기화

먼저 가장 간단한 동기화 방법인 `synchronized` 키워드를 이용한 동기화에 대해서 알아보겠다. 이 키워드는 임계 영역을 설정하는데 사용된다. 아래와 같이 두 가지 방식이 있다.

![image](https://ifh.cc/g/gVsAnY.png)

첫 번째 방법은 메소드 앞에 `synchronized`를 붙이는 것인데, `synchronized`를 붙이면 메소드 전체가 임계 영역으로 설정된다. 쓰레드는 `synchronized`에 메소드가 호출된 시점부터 해당 메소드가 포함된 객체의 `lock`을 얻어 작업을 수행하다가 메소드가 종료되면 `lock`을 반환한다.

두 번째 방법은 메소드 내의 코드 일부를 블럭{}으로 감싸고 블럭 앞에 `synchronized(참조변수)`를 붙이는 것인데, 이때 참조변수는 락을 걸고자하는 객체를 참조하는 것이어야 한다. 이 블럭을 `synchronized`블럭이라고 부르며, 이 블럭의 영역 안으로 들어가면서부터 쓰레드는 지정된 객체의 `lock`을 얻게 되고, 이 블럭을 벗어나면 `lock`을 반납한다.

두 방법 모두 `lock`의 획득과 반납이 모두 자동적으로 이루어지므로 임계 영역만 설정해주면 된다.

모든 객체는 `lock`을 하나씩 가지고 있으며, 해당 객체의 `lock`을 가지고 있는 쓰레드만 임계 영역의 코드를 수행할 수 있다. 그리고 다른 쓰레드들은 `lock`을 얻을 때까지 기다리게 된다.

임계 영역은 멀티쓰레드 프로그램의 성능을 좌우하기 때문에 가능하면 메소드 전체에 락을 거는 것보다 `synchronized`블럭으로 임계 영역을 최소화해서 보다 효율적인 프로그램이 되도록 노력해야 한다.

</br>

예제 13-21 / ch13 / ThreadEx21.java

``` java
public class ThreadEx21 {
	public static void main(String[] args) {
		Runnable r = new RunnableEx21();
		new Thread(r).start();	// ThreadGroup에 의해 참조되므로 gc대상이 아니다.
		new Thread(r).start();	// ThreadGroup에 의해 참조되므로 gc대상이 아니다.
	}
}

class Account {
	private int balance = 1000;
	
	public int getBalance() {
		return balance;
	}
	
	public void withdraw(int money) {
		if(balance >= money) {
			try {
				Thread.sleep(1000);
			} catch (InterruptedException e) {}
			balance -= money;
		}
	}	// withdraw
}

class RunnableEx21 implements Runnable {
	Account acc = new Account();
	
	public void run() {
		while(acc.getBalance() > 0) {
			// 100, 200, 300중의 한 값을 임의로 선택해서 출금(withDraw)
			int money = (int)(Math.random() * 3 + 1) * 100;
			acc.withdraw(money);
			System.out.println("balance : " + acc.getBalance());
		}
	}	// run()
}
```

```
balance : 700
balance : 400
balance : 200
balance : -100
```

은행계좌(account)에서 잔고(balance)를 확인하고 임의의 금액을 출금(withdraw)하는 예제이다. 아래의 코드를 보면 잔고가 출금하려는 금액보다 큰 경우에만 출금하도록 되어 있는 것을 확인할 수 있다.

``` java
public void withdraw(int money) {
    if(balance >= money) {
        try {
            Thread.sleep(1000);
        } catch (InterruptedException e) {}
        balance -= money;
    }
}	// withdraw
```

그러나 실행결과를 보면 잔고(balance)가 음수이다. 그 이유는 한 쓰레드가 if문의 조건식을 통과하고 출금하기 바로 직전에 다른 쓰레드가 끼어들어서 출금을 먼저 했기 때문이다.

예를 들어 한 쓰레드가 if문의 조건식을 계산했을 때는 잔고(balance)가 200이고 출금하려는 금액(money)이 100이라서 조건식(balance >= money)이 true가 되어 출금(balance -= money)을 수행하려는 순간 다른 쓰레드에게 제어권이 넘어가서 다른 쓰레드가 200을 출금하여 잔고가 0이 되었다. 다시 이전의 쓰레드로 제어권이 넘어오면 if문 다음부터 수행하게 되므로 잔고가 0인 상태에서 100을 출금하여 잔고가 결국 -100이 된다. 그래서 잔고를 확인하는 if문과 출금하는 문장은 하나의 임계 영역으로 묶어져야 한다.

예제에서는 상황을 보여주기 위해 일부러 `Thread.sleep(1000)`을 사용해서 if문을 통과하자마자 다른 쓰레드에게 제어권을 넘기도록 하였지만, 굳이 이렇게 하지 않더라도 이처럼 한 쓰레드의 작업이 다른 쓰레드에 의해서 영향을 받는 일이 발생할 수 있기 때문에 동기화가 반드시 필요하다. 아래와 같이 `withDraw`메소드에 `synchronized`키워드를 붙이기만 하면 간단히 동기화가 된다.

``` java
public synchronized void withdraw(int money) {
    if(balance >= money) {
        try {
            Thread.sleep(1000);
        } catch (InterruptedException e) {}
        balance -= money;
    }
}	// withdraw
```

한 쓰레드에 의해서 먼저 `withdraw()`가 호출되면, 이 메소드가 종료되어 `lock`이 반납될 때까지 다른 쓰레드는 `withdraw()`를 호출하더라도 대기상태에 머물게 되낟.

메소드 앞에 `synchronized`를 붙이는 대신, `synchronized`블럭을 사용하면 다음과 같다.

``` java
public void withdraw(int money) {
    synchronized(this) {
        if(balance >= money) {
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {}
            balance -= money;
        }
    }
}	// withdraw
```

이 경우에는 둘 중의 어느 쪽을 선택해도 같으니까 `synchronized`메소드로 하는 것이 낫다.

</br>

예제 13-22/ ch13 / ThreadEx22.java

``` java
public class ThreadEx22 {
	public static void main(String[] args) {
		Runnable r = new RunnableEx22();
		new Thread(r).start();	// ThreadGroup에 의해 참조되므로 gc대상이 아니다.
		new Thread(r).start();	// ThreadGroup에 의해 참조되므로 gc대상이 아니다.
	}
}

class Account {
	private int balance = 1000;
	
	public int getBalance() {
		return balance;
	}
	
	public synchronized void withdraw(int money) {
		if(balance >= money) {
			try {
				Thread.sleep(1000);
			} catch (InterruptedException e) {}
			balance -= money;
		}
	}	// withdraw
}

class RunnableEx22 implements Runnable {
	Account acc = new Account();
	
	public void run() {
		while(acc.getBalance() > 0) {
			// 100, 200, 300중의 한 값을 임의로 선택해서 출금(withDraw)
			int money = (int)(Math.random() * 3 + 1) * 100;
			acc.withdraw(money);
			System.out.println("balance : " + acc.getBalance());
		}
	}	// run()
}
```

```
balance : 700
balance : 400
balance : 200
balance : 0
balance : 0
```

이전 예제의 `withdraw()`에 `synchronized`를 붙이기만 했는데도, 전과 달리 결과에 음수값이 나타나지 않는 것을 확인할 수 있다. 여기서 한 가지 주의할 점은 `Account`클래스의 인스턴스변수인 `balance`의 접근 제어자가 `private`이라는 것이다. 만일 `private`이 아니면, 외부에서 직접 접근할 수 있기 때문에 아무리 동기화를 해도 이 값의 변경을 막을 길이 없다. `synchronized`를 이용한 동기화는 지정된 영역의 코드를 한 번에 하나의 쓰레드가 수행하는 것을 보장하는 것일 뿐이기 때문이다.

</br>

## 9.2 wait()과 notify()

`synchronized`로 동기화해서 공유 데이터를 보호하는 것까지는 좋은데, 특정 쓰레드가 객체의 락을 가진 상태로 오랜 시간을 보내지 않도록 하는 것도 중요하다. 만일 계좌에 출금할 돈이 부족해서 한 쓰레드가 락을 보유한 채로 돈이 입금될 때까지 오랜 시간을 보낸다면, 다른 쓰레드들은 모두 해당 객체의 락을 기다리느라 다른 작업들도 원활히 진행되지 않는다.

이러한 상황을 개선하기 위해 고안된 것이 바로 `wait()`와 `notify()`이다. 동기화된 임계 영역의 코드를 수행하다가 작업을 더 이상 진행할 상황이 아니면, 일단 `wait()`를 호출하여 쓰레드가 락을 반납하고 기다리게 한다. 그러면 다른 쓰레드가 락을 얻어 해당 객체에 대한 작업을 수행할 수 있게 된다. 나중에 작업을 진행할 수 있는 상황이 되면 `notify()`를 호출해서 작업을 중단했던 쓰레드가 다시 락을 얻어 작업을 진행할 수 있게 된다.

`wait()`가 호출되면, 실행 중이던 쓰레드는 해당 객체의 대기실(waiting pool)에서 통지를 기다린다. `notify()`가 호출되면, 해당 객체의 대기실에 있던 모든 쓰레드 중에서 임의의 쓰레드만 통지를 받는다. `notifyAll()`은 기다리고 있는 모든 쓰레드에게 통보를 하지만, 그래도 `lock`을 얻을 수 있는 것은 하나의 쓰레드일 뿐이고 나머지 쓰레드는 통보를 받기 했지만, `lock`을 얻지 못하면 다시 `lock`을 가디라는 신세가 된다.

`wait()`와 `notify()`는 특정 객체에 대한 것이므로 `Object`클래스에 정의되어 있다.

``` java
void wait()
void wait(long timeout)
void wait(long timeout, int nanos)
void notify()
void notifyAll()
```

`wait()`는 `notify()` 또는 `notifyAll()`이 호출될 때까지 기다리지만, 매개변수가 있는 `wait()`은 지정된 시간동안만 기다린다. 즉, 지정된 시간이 지난 후에 자동적으로 `notify()`가 호출되는 것과 같다.

그리고 waiting pool은 객체마다 존재하는 것이므로 `notifyAll()`이 호출된다고 해서 모든 객체의 waiting pool에 있는 쓰레드가 깨워지는 것은 아니다. `notifyAll()`이 호출된 객체의 `waiting pool`에 대기 중인 쓰레드만 해단된다.

> **wait(), notify(), notifyAll()**
> - Object에 정의되어 있다.
> - 동기화 블럭(synchronized블럭)내에서만 사용할 수 있다.
> - 보다 효율적인 동기화를 가능하게 한다.

다음 예제에서는 식당에서 음식(Dish)을 만들어서 테이블(Table)에 추가(add)하는 요리사(Cook)와 테이블의 음식을 소비(remove)하는 손님(Customer)을 쓰레드로 구현했다.

</br>

예제 13-23 / ch13 / ThreadWaitEx1.java

``` java
import java.util.ArrayList;

public class ThreadWaitEx1 {
	public static void main(String[] args) throws Exception {
		Table table = new Table();	// 여러 쓰레드가 공유하는 객체
		
		new Thread(new Cook(table), "COOK1").start();
		new Thread(new Customer(table, "donut"), "CUST1").start();
		new Thread(new Customer(table, "burger"), "CUST2").start();
		
		Thread.sleep(100);	// 0.1초(100 밀리 세컨드) 후에 강제 종료시킨다.
		System.exit(0);	// 프로그램 전체를 종료. (모든 쓰레드가 종료됨.)
	}
}

class Customer implements Runnable {
	private Table table;
	private String food;
	
	Customer(Table table, String food) {
		this.table = table;
		this.food = food;
	}
	
	public void run() {
		while(true) {
			try {
				Thread.sleep(10);
			} catch (InterruptedException e) {}
			
			String name = Thread.currentThread().getName();
			
			if(eatFood())
				System.out.println(name + " ate a " + food);
			else
				System.out.println(name + " failed to eat, : (");
		}	// while
	}
	
	boolean eatFood() { return table.remove(food); }
}

class Cook implements Runnable {
	private Table table;
	
	Cook(Table table) { this.table = table; }
	
	public void run() {
		while(true) {
			// 임의의 요리를 하나 선택해서 table에 추가한다.
			int idx = (int)(Math.random() * table.dishNum());
			table.add(table.dishNames[idx]);
			try { Thread.sleep(1); } catch (InterruptedException e) { }
		}	// while
	}
}

class Table {
	String[] dishNames = { "donut", "donut", "burger" };	// donut이 더 자주 나온다.
	final int MAX_FOOD = 6;	// 테이블에 놓을 수 있는 최대 음식의 개수
	
	private ArrayList<String> dishes = new ArrayList<>();
	
	public void add(String dish)	{
		// 테이블에 음식이 가득찼으면, 테이블에 음식을 추가하지 않는다.
		if(dishes.size() >= MAX_FOOD)
			return;
		dishes.add(dish);
		System.out.println("Dishes : " + dishes.toString());
	}
	
	public boolean remove(String dishName) {
		// 지정된 요리와 일치하는 요리를 테이블에서 제거한다.
		for(int i = 0; i < dishes.size(); i++)
			if(dishName.equals(dishes.get(i))) {
				dishes.remove(i);
				return true;
			}
		
		return false;
	}
	public int dishNum() { return dishNames.length;	}
}
```

```
Dishes : [donut]
Dishes : [donut, donut]
Dishes : [donut, donut, burger]
Dishes : [donut, donut, burger, donut]
CUST2 ate a burger
CUST1 ate a donut
Exception in thread "COOK1" java.util.ConcurrentModificationException
	at java.base/java.util.ArrayList$Itr.checkForComodification(ArrayList.java:1013)
	at java.base/java.util.ArrayList$Itr.next(ArrayList.java:967)
	at java.base/java.util.AbstractCollection.toString(AbstractCollection.java:456)
	at Table.add(ThreadWaitEx1.java:69)
	at Cook.run(ThreadWaitEx1.java:52)
	at java.base/java.lang.Thread.run(Thread.java:833)
CUST1 ate a donut
CUST2 failed to eat, : (
CUST1 ate a donut
CUST2 failed to eat, : (
CUST1 ate a donut
CUST2 failed to eat, : (
CUST1 ate a donut
CUST2 failed to eat, : (
CUST2 failed to eat, : (
CUST1 failed to eat, : (
CUST1 failed to eat, : (
CUST2 failed to eat, : (
CUST1 failed to eat, : (
CUST2 failed to eat, : (
```

실행결과는 실행할 때마다 다른데, 예외가 발생할 수도 있고 발생하지 않을 수도 있다. 위의 실행결과에서는 2가지 종류의 예외가 발생했는데, 요리사(Cook) 쓰레드가 테이블에 음식을 놓는 도중에, 손님(Custommer) 쓰레드가 음식을 가져가려했기 때문에 발생하는 예외(ConcurrentModificationException)이고, 다른 하나는 손님 쓰레드가 테이블의 마지막 남은 음식을 가져가는 도중에 다른 손님 쓰레드가 먼저 음식을 낚아채버려서 있지도 않은 음식을 테이블에서 제거하려했기 때문에 발생하는 예외(IndexOutOfBoundsException)이다.

이런 예외들이 발생하는 이유는 여러 쓰레드가 테이블을 공유하는데도 동기화를 하지 않았기 때문이다.

</br>

예제 13-23/ ch13 / ThreadWaitEx2.java

``` java
import java.util.ArrayList;

class Customer2 implements Runnable {
	private Table2 table;
	private String food;
	
	Customer2(Table2 table, String food) {
		this.table = table;
		this.food = food;
	}
	
	public void run() {
		while(true) {
			try {
				Thread.sleep(10);
			} catch (InterruptedException e) {}
			
			String name = Thread.currentThread().getName();
			
			if(eatFood())
				System.out.println(name + " ate a " + food);
			else
				System.out.println(name + " failed to eat, : (");
		}	// while
	}
	
	boolean eatFood() { return table.remove(food); }
}

class Cook2 implements Runnable {
	private Table2 table;
	
	Cook2(Table2 table) { this.table = table; }
	
	public void run() {
		while(true) {
			// 임의의 요리를 하나 선택해서 table에 추가한다.
			int idx = (int)(Math.random() * table.dishNum());
			table.add(table.dishNames[idx]);
			try { Thread.sleep(100); } catch (InterruptedException e) { }
		}	// while
	}
}

class Table2 {
	String[] dishNames = { "donut", "donut", "burger" };
	final int MAX_FOOD = 6;
	private ArrayList<String> dishes = new ArrayList<>();
	public synchronized void add(String dish)	{	// synchronized를 추가
		if(dishes.size() >= MAX_FOOD)
			return;
		dishes.add(dish);
		System.out.println("Dishes : " + dishes.toString());
	}
	
	public boolean remove(String dishName) {
		synchronized (this) {
			while(dishes.size() == 0) {
				String name = Thread.currentThread().getName();
				System.out.println(name + " is waiting.");
				try { Thread.sleep(500); } catch (InterruptedException e) {}
			}
			
			for(int i = 0; i < dishes.size(); i++)
				if(dishName.equals(dishes.get(i))) {
					dishes.remove(i);
					return true;
				}
		}	// synchronized
		
		return false;
	}
	public int dishNum() { return dishNames.length; }
}

public class ThreadWaitEx2 {
	public static void main(String[] args) throws Exception {
		Table2 table = new Table2();	// 여러 쓰레드가 공유하는 객체
		
		new Thread(new Cook2(table), "COOK1").start();
		new Thread(new Customer2(table, "donut"), "CUST1").start();
		new Thread(new Customer2(table, "burger"), "CUST2").start();
		
		Thread.sleep(5000);
		System.exit(0);
	}
}
```

```
Dishes : [donut]
CUST2 failed to eat, : (    ← burger가 없어서 먹지 못했다.
CUST1 ate a donut
CUST2 is waiting.   ← 음식이 없어서 테이블에 lock을 건 채로 계속 기다리고 있다.
CUST2 is waiting.
CUST2 is waiting.
... 중간 생략 ...
```

여러 쓰레드가 공유하는 객체인 테이블(Table2)의 `add()`와 `remove()`를 동기화하였다. 더 이상 전과 같은 예외는 발생하지 않지만, 뭔가 원활히 진행되지 않는다.

손님 쓰레드가 원하는 음식이 테이블에 없으면, 'failed to eat'을 출력하고, 테이블에 음식이 하나도 없으면, 0.5초마다 음식이 추가되었는지 확인하면서 기다리도록 작성되어 있다.

요리사 쓰레드는 음식을 추가하지 않고 계속 손님 쓰레드를 기다리게 된다.

``` java
synchronized (this) {
    while(dishes.size() == 0) {
        String name = Thread.currentThread().getName();
        System.out.println(name + " is waiting.");
        try { Thread.sleep(500); } catch (InterruptedException e) {}
    }
            ...
}	// synchronized의 끝
```

그 이유는 손님 쓰레드가 테이블 객체의 `lock`을 쥐고 기다리기 때문이다. 요리사 쓰레드가 음식을 새로 추가하려해도 테이블 객체의 `lock`을 얻을 수 없어서 불가능하다. 이럴 때 사용하는 것이 바로 `wait()` & `notify()`이다. 손님 쓰레드가 `lock`을 쥐고 기다리는 게 아니라, `wait()`으로 `lock`을 풀고 기다리다가 음식이 추가되면 `notify()`로 통보를 받고 다시 `lock`을 얻어서 나머지 작업을 진행하게 할 수 있다.

</br>

예제 13-25 / ch13 / ThreadWaitEx3.java

``` java
import java.util.ArrayList;

class Customer3 implements Runnable {
	private Table3 table;
	private String food;
	
	Customer3(Table3 table, String food) {
		this.table = table;
		this.food = food;
	}
	
	public void run() {
		while(true) {
			try {
				Thread.sleep(100);
			} catch (InterruptedException e) {}
			
			String name = Thread.currentThread().getName();
			
			table.remove(food);
			System.out.println(name + " ate a " + food);
		}	// while
	}
}

class Cook3 implements Runnable {
	private Table3 table;
	
	Cook3(Table3 table) { this.table = table; }
	
	public void run() {
		while(true) {
			int idx = (int)(Math.random() * table.dishNum());
			table.add(table.dishNames[idx]);
			try { Thread.sleep(10); } catch (InterruptedException e) { }
		}	// while
	}
}

class Table3 {
	String[] dishNames = { "donut", "donut", "burger" };	// donut의 확률을 높인다.
	final int MAX_FOOD = 6;
	
	private ArrayList<String> dishes = new ArrayList<>();
	
	public synchronized void add(String dish)	{
		while(dishes.size() >= MAX_FOOD) {
			String name = Thread.currentThread().getName();
			System.out.println(name + " is waiting.");
			try {
				wait();	// COOK쓰레드를 기다리게 힌다.
				Thread.sleep(500);
			} catch (InterruptedException e) {}
		}
		dishes.add(dish);
		notify();	// 기다리고 있는 CUST를 깨우기 위함.
		System.out.println("Dishes : " + dishes.toString());
	}
	
	public void remove(String dishName) {
		synchronized (this) {
			String name = Thread.currentThread().getName();
			
			while(dishes.size() == 0) {
				System.out.println(name + " is waiting.");
				try {
					wait();	// CUST쓰레드를 기다리게 한다.
					Thread.sleep(500);
				} catch (InterruptedException e) {}
			}
			
			while(true) {
				for(int i = 0; i < dishes.size(); i++) {
					if(dishName.equals(dishes.get(i))) {
						dishes.remove(i);
						notify();	// 잠자고 있는 COOK을 깨우기 위함
						return;
					}
				}	// for문의 끝
				
				try {
					System.out.println(name + " is waiting.");
					wait();	// 원하는 음식이 없는 CUST쓰레드를 기다리게 한다.
					Thread.sleep(500);
				} catch (InterruptedException e) {}
			}	// while(true)
		}	// synchronized
	}
	
	public int dishNum() {
		return dishNames.length;
	}
}

public class ThreadWaitEx3 {
	public static void main(String[] args) throws Exception {
		Table3 table = new Table3();	// 여러 쓰레드가 공유하는 객체
		
		new Thread(new Cook3(table), "COOK1").start();
		new Thread(new Customer3(table, "donut"), "CUST1").start();
		new Thread(new Customer3(table, "burger"), "CUST2").start();
		
		Thread.sleep(2000);
		System.exit(0);
	}
}
```

```
Dishes : [burger]
Dishes : [burger, donut]
Dishes : [burger, donut, burger]
Dishes : [burger, donut, burger, donut]
Dishes : [burger, donut, burger, donut, donut]
Dishes : [burger, donut, burger, donut, donut, donut]
COOK1 is waiting.
CUST1 ate a donut
CUST2 ate a burger
Dishes : [burger, donut, donut, donut, donut]
CUST1 ate a donut
CUST2 ate a burger
Dishes : [donut, donut, donut, donut]
Dishes : [donut, donut, donut, donut, donut]
Dishes : [donut, donut, donut, donut, donut, donut]
COOK1 is waiting.
CUST2 is waiting.
CUST1 ate a donut
Dishes : [donut, donut, donut, donut, donut, burger]
CUST2 ate a burger
Dishes : [donut, donut, donut, donut, donut, burger]
CUST1 ate a donut
Dishes : [donut, donut, donut, donut, burger, donut]
COOK1 is waiting.
CUST2 ate a burger
CUST1 ate a donut
```

이전 예제에 `wait()`와 `notify()`를 추가하였다. 그리고 테이블에 음식이 없을 때뿐만 아니라, 원하는 음식이 없을 때도 손님이 기다리도록 바꾸었다.

실행결과를 보니 이제 무너가 좀 잘 돌아가는 것 같다. 그런데, 여기에도 한 가지 문제가 있다. 그래서 `notify()`가 호출되었을 때, 요리사 쓰레드와 손님 쓰레드 중에서 누가 통지를 받을지 알 수 없다.

만일 테이블의 음식이 줄어들어서 `notify()`가 호출되었다면, 요리사 쓰레드가 통지를 받아야 한다. 그러나 `notify()`는 그저 waiting pool에서 대기 중인 쓰레드 중에서 하나를 임의로 선택해서 통지할 뿐, 요리사 쓰레드를 선택해서 통지할 수 없다. 운 좋게 요리사 쓰레드가 통지를 받으면 다행인데, 손님 쓰레드가 통지 받으면 lock을 얻어도 여전히 자신이 원하는 음식이 없어서 다시 waiting pool에 들어가게 된다.

</br>

### 기아 현상과 경쟁 상태

지독히 운이 나쁘면 요리사 쓰레드는 계속 통지를 받지 못하고 오랫동안 기다리게 되는데, 이것을 '기아(starvation) 현상'이라고 한다. 이 현상을 막으려면, `notify()`대신 `notifyAll()`을 사용해야 한다. 일단 모든 쓰레드에게 통지를 하면, 손님 쓰레드는 다시 waiting pool에 들어가더라도 요리사 쓰레드는 결국 lock을 얻어서 작업을 진행할 수 있기 때문이다.

`notifyAll()`로 요리사 쓰레드의 기아현상은 막았지만, 손님 쓰레드까지 통지를 받아서 불필요하게 요리사 쓰레드와 lock을 얻기 위해 경쟁하게 된다. 이처럼 여러 쓰레드가 lock을 얻기 위해 서로 경쟁하는 것을 '경쟁 상태(race condition)'라고 하는데, 이 경쟁 상태를 개선하기 위해서는 요리사 쓰레드와 손님 쓰레드를 구별해서 통지하는 것이 필요하다. `Lock`과 `Condition`을 이용하면, `wait()` & `notify()`로는 불가능한 선별적인 통지가 가능하다.

</br>

## 9.3 Lock과 COndition을 이용한 동기화

동기화할 수 있는 방법은 `synchronized`블럭 외에도 `java.util.concurrent.locks`패키지가 제공하는 `lock`클래스들을 이용하는 방법이 있다. 이 패키지는 JDK1.5에 와서야 추가된 것으로 그 전에는 동기화 방법이 `synchronized`블럭뿐이었다.

`synchronized`블럭으로 동기화를 하면 자동적으로 lock이 잠기고 풀리기 때문에 편리하다. 심지어 `synchronized`블럭 내에서 예외가 발생해도 lock은 자동적으로 풀린다. 그러나 때로는 같은 메소드 내에서만 lock을 걸수 있다는 제약이 불편하기도 하다. 그럴 때 이 `lock`클래스를 사용한다. `lock`클래스의 종류는 다음과 같다.

> **ReentrantLock** 재진입이 가능한 lock, 가장 일반적인 베타 lock   
> **ReentrantReadWriteLock** 읽기에는 공유적이고, 쓰기에는 베타적인 lock   
> **StampedLock** ReentrantReadWriteLock에 낙관적인 lock의 기능을 추가

> StampedLock은 JDK1.8부터 추가되었으며, 다른 lock과 달리 Lock인터페이스를 구현하지 않았다.

`ReentrantLock`은 가장 일반적인 `lock`이다. 'reentrant(재진입할 수 있는)'이라는 단어가 앞에 붙은 이유는 특정 조건에서 `lock`을 풀고 나중에 다시 `lock`을 얻고 임계 영역으로 들어와서 이후의 작업을 수행할 수 있기 때문이다.

`ReentrantReadWriteLock`은 읽기를 위한 `lock`과 쓰기를 위한 `lock`을 제공한다. `ReetrantLock`은 베타적인 `lock`이라서 무조건 `lock`이 걸려있으면, 다른 쓰레드가 읽기 `lock`을 중복해서 걸고 읽기를 수행할 수 있다. 읽기는 내용을 변경하지 않으므로 동시에 여러 쓰레드가 읽어도 문제가 되지 않는다. 그러나 읽기 `lock`이 걸린 상태에서 쓰기 `lock`을 거는 것은 허용되지 않는다. 반대의 경우도 마찬가지다. 읽기를 할 때는 읽기 `lock`을 걸고, 쓰기 할 때는 쓰기 `lock`을 거는 것일 뿐 `lock`을 거는 방법은 같다.

`StampedLock`은 `lock`을 걸거나 해지할 때 '스탬프(long타입의 정수값)'를 사용하며, 읽기와 쓰기를 위한 `lock`외에 '낙관적 읽기 lock(optimistic reading lock)'이 추가된 것이다. 읽기 lock이 걸려있으면, 쓰기 lock을 얻기 위해서는 읽기 lock이 풀릴 때까지 기다려야 하는데 비해 '낙관적 읽기 lock'은 쓰기 lock에 의해 바로 풀린다. 그래서 낙관적 읽기에 실패하면, 읽기 lock을 얻어서 다시 읽어와야 한다. **무조건 읽기 lock을 걸지 않고, 쓰기와 읽기가 충돌할 때만 쓰기가 끝난 후에 읽기 lock을 거는 것이다.**

다음의 코드는 가장 일반적인 `StampedLock`을 이용한 낙관적 읽기의 예이다.

``` java
int getBalance() {
    long stamp = lock.tryOptimisticRead();  // 낙관적 읽기 lock을 건다.

    int curBalance = this.balance;  // 공유 데이터인 balance를 읽어온다.

    if(!lock.validate(stamp)) {
        stamp = lock.readLock();    // lock이 풀렸으면, 읽기 lock을 얻으려고 기다린다.

        try {
            curBalance = this.balance;  // 공유 데이터를 다시 읽어온다.
        } finally {
            lock.unlockRead(stamp); // 읽기 lock을 푼다.
        }
    }

    return curBalance;  // 낙관적 읽기 lock이 풀리지 않았으면 곧바로 읽어온 값을 반환
}
```

</br>

### ReeatrantLock의 생성자

ReentrantLock은 다음과 가이 두 개의 생성자를 가지고 있다.

> **ReentrantLock()**   
> **ReentrantLock(boolean fair)**

생성자의 매개변수를 true로 주면, lock이 풀렸을 때 가장 오래 기다린 쓰레드가 lock을 획득할 수 있게, 즉 공정(fair)하게 처리한다. 그러나 공정하게 처리하려면 어떤 쓰레드가 가장 오래 기다렸는지 확인하는 과정을 거칠 수 밖에 없으므로 성능은 떨어진다.

대부분의 경우 굳이 공정하게 처리하지 않아도 문제가 되지 않으므로 공정함보다 성능을 선택한다.

> **void lock()** lock을 잠근다.   
> **void unlock()** lock을 해지한다.   
> **boolean isLocked()** lock이 잠겼는지 확인한다.

자동적으로 lock의 잠금과 해제가 관리되는 `synchronized`블럭과 달리, `ReentrantLock`과 같은 `lock`클래스들은 수동으로 lock을 잠그고 해제해야 한다. 그래도 lock을 잠그고 푸는 것은 간단하다. 그저 메소드를 호출하기만 하면 될 뿐이다. lock을 걸고 나서 푸는 것을 잊어버리는 실수를 하지 않도록 주의를 기울여야 한다.

![image](https://ifh.cc/g/aRolV5.png)

임계 영역 내에서 예외가 발생하거나 return문으로 빠져 나가게 되면 lock이 풀리지 않을 수 있으므로 `unlock()`은 try-finally문으로 감싸는 것이 일반적이다. 참조변수 `lock`은 `ReentrantLock`객체를 참조하도록 가정하였다.

``` java
lock.lock();    // ReentrantLock lock = new ReentrantLock();
try {
    // 임계 영역
} finally {
    lock.unlock();
}
```

이렇게 하면, try블럭 내에서 어떤 일이 발생해도 finally블럭에 있는 `unlock()`이 수행되어 lock이 풀리지 않는 일이 발생하지 않는다.

이외에도 `tryLock()`이라는 메소드가 있는데, 이 메소드는 `lock()`과 달리, 다른 쓰레드에 의해 lock이 걸려 있으면 lock을 얻으려고 기다리지 않는다. 또는 지정된 시간만큼만 기다린다. lock을 얻으려면 true를 반환하고, 얻지 못하면 false를 반환한다.

> **boolean tryLock()**   
> **boolean tryLock(long timeout, TimeUnit unit) throws InterruptedException**

`lock()`은 lock을 얻을 때까지 쓰레드를 블럭(block)시키므로 쓰레드의 응답성이 나빠질 수 있다. 응답성이 중요한 경우, `tryLock()`을 이용해서 지정된 시간동안 lock을 얻지 못하면 다시 작업을 시도할 것인지 포기할 것인지를 사용자가 결정할 수 있게 하는 것이 좋다.

그리고 이 메소드는 `InterruptedException`을 발생시킬 수 있는데, 이것은 지정된 시간동안 lock을 얻으려고 기다리는 중에 `interrupt()`에 의해 작업을 취소될 수 있도록 코드를 작성할 수 있다는 뜻이다.

</br>

### ReentrantLock과 Condition

`wait()` & `notify()` 예제에 요리사 쓰레드와 손님 쓰레드를 구분해서 통지하지 못한다는 단점이 있다. `Condition`은 이 문제점을 해결하기 위한 것이다.

`wait()` & `notify()`로 쓰레드의 종류를 구분하지 않고, 공유 객체의 wating pool에 같이 몰아넣는 대신, 손님 쓰레드를 위한 `Condition`과 요리사 쓰레드를 위한 `Condition`을 만들어서 각각의 waiting pool에서 따로 기다리도록 하면 문제는 해결된다.

`Condition`은 이미 생성된 lock으로부터 `newCondition()`을 호출해서 생성한다.

``` java
private ReentrantLock lock = new ReentrantLock();   // lock을 생성

// lock으로 condition을 생성
private Condition forCook = lock.newCondition();
private Condition forCust = lock.newCondition();
```

위의 코드에서 두 개의 `Condition`을 생성했는데, 하나는 요리사 쓰레드를 위한 것이고 다른 하나는 손님 쓰레드를 위한 것이다. 그 다음엔, `wait()` & `notify()`대신 `Condition`이 `await()` & `signal()`을 사용하면 그걸로 끝이다.

![image](https://ifh.cc/g/tqQKq3.png)

아래의 코드는 예제13-25에서 테이블에 음식을 추가하는 `add()`인데, `wait()`과 `notify()`대신 `await()`과 `signal()`을 사용하였다.

``` java
public void add(String dish) {
    lock.lock();

    try {
        while(dishes.size() >= MAX_FOOD) {
            String name = Thread.currentThread().getName();
            System.out.println(name + " is Waiting.");
            try {
                forCook.await();    // wait();  COOK쓰레드를 기다리게 한다.
            } catch(InterruptedException e) {}
        }

        dishes.add(dish);
        forCust.signal();   // notify();  기다리고 있는 CUST를 깨우기 위함
        System.out.println("Dishes : " + dishes.toString());
    } finally {
        lock.unlock();
    }
}
```

전에는 손님 쓰레드를 기다리게 할 때와 요리사 쓰레드를 기다리게 할 때 모두 `wait()`을 사용했는데, 이제는 `wait()`대신 `forCook.await()`과 `forCust.await()`을 사용함으로써 대기와 통지의 대상이 명확히 구분된다.

</br>

예제 13-26 / ch1 / ThreadWaitEx4.java

``` java
import java.util.ArrayList;
import java.util.concurrent.locks.ReentrantLock;
import java.util.concurrent.locks.Condition;

class Customer4 implements Runnable {
	private Table4 table;
	private String food;
	
	Customer4(Table4 table, String food) {
		this.table = table;
		this.food = food;
	}
	
	public void run() {
		while(true) {
			try { Thread.sleep(100); } catch (InterruptedException e) {}
			String name = Thread.currentThread().getName();
			
			table.remove(food);
			System.out.println(name + " ate a " + food);
		}	// while
	}
}

class Cook4 implements Runnable {
	private Table4 table;
	
	Cook4(Table4 table) { this.table = table; }
	
	public void run() {
		while(true) {
			int idx = (int)(Math.random() * table.dishNum());
			table.add(table.dishNames[idx]);
			try { Thread.sleep(10); } catch (InterruptedException e) {}
		} // while
	}
}

class Table4 {
	String[] dishNames = { "donut", "donut", "burger" };	// donut의 확률을 높인다.
	final int MAX_FOOD = 6;
	private ArrayList<String> dishes = new ArrayList<>();
	
	private ReentrantLock lock = new ReentrantLock();
	private Condition forCook = lock.newCondition();
	private Condition forCust = lock.newCondition();
	
	public void add(String dish) {
		lock.lock();
		
		try {
			while(dishes.size() >= MAX_FOOD) {
				String name = Thread.currentThread().getName();
				System.out.println(name + " is waiting.");
				
				try {
					forCook.await();	// wait();	COOK쓰레드를 기다리게 한다.
					Thread.sleep(500);
				} catch (InterruptedException e) {}
			}
			
			dishes.add(dish);
			forCust.signal();	// notify();  기다리고 있는 CUST를 깨우기 위함.
			System.out.println("Dishes : " + dishes.toString());
		} finally {
			lock.unlock();
		}
	}
	
	public void remove(String dishName) {
		lock.lock();	// synchronized(this) {
		String name = Thread.currentThread().getName();

		try {
			while(dishes.size() == 0) {
				System.out.println(name + " is waiting.");
				try {
					forCust.await();	// wait(); CUST쓰레드를 기다리게 한다.
					Thread.sleep(500);
				} catch (InterruptedException e) {}
			}
			
			while(true) {
				for(int i = 0; i < dishes.size(); i++) {
					if(dishName.equals(dishes.get(i))) {
						dishes.remove(i);
						forCook.signal();	// notify(); 잠자고 있는 COOK을 깨움
						return;
					}
				}	// for문의 끝
				
				try {
					System.out.println(name + " is waiting.");
					forCust.await();	// wait();	// CUST쓰레드를 기다리게 한다.
					Thread.sleep(500);
				} catch (InterruptedException e) {}
			}	// while(true)
				// }	// synchronized
		} finally {
			lock.unlock();
		}
	}
	
	public int dishNum() { return dishNames.length; }
}

public class ThreadWaitEx4 {
	public static void main(String[] args) throws Exception {
		Table4 table = new Table4();
		new Thread(new Cook4(table), "COOK").start();
		new Thread(new Customer4(table, "donut"), "CUST1").start();
		new Thread(new Customer4(table, "burger"), "CUST2").start();
		
		Thread.sleep(2000);
		System.exit(0);
		
	}
}
```

```
Dishes : [donut]
Dishes : [donut, burger]
Dishes : [donut, burger, donut]
Dishes : [donut, burger, donut, burger]
Dishes : [donut, burger, donut, burger, donut]
Dishes : [donut, burger, donut, burger, donut, donut]
COOK is waiting.
CUST2 ate a burger
CUST1 ate a donut
Dishes : [donut, burger, donut, donut, burger]
CUST1 ate a donut
CUST2 ate a burger
Dishes : [donut, donut, burger, donut]
Dishes : [donut, donut, burger, donut, burger]
Dishes : [donut, donut, burger, donut, burger, donut]
COOK is waiting.
CUST1 ate a donut
Dishes : [donut, burger, donut, burger, donut, donut]
CUST2 ate a burger
CUST1 ate a donut
Dishes : [donut, burger, donut, donut, donut]
Dishes : [donut, burger, donut, donut, donut, donut]
COOK is waiting.
CUST1 ate a donut
CUST2 ate a burger
Dishes : [donut, donut, donut, donut, burger]
CUST1 ate a donut
CUST2 ate a burger
Dishes : [donut, donut, donut, donut]
Dishes : [donut, donut, donut, donut, donut]
Dishes : [donut, donut, donut, donut, donut, donut]
COOK is waiting.
CUST2 is waiting.
CUST1 ate a donut
```

예제 13-25와 달리, 요리사 쓰레드가 통지를 받아야하는 상황에서 손님 쓰레드가 통지를 받는 경우가 없어졌다. '기아 현상'이나 '경쟁 상태'가 확실히 개선되었다. 그래도 쓰레드의 종류에 따라 구분하여 통지를 할 수 있게 된 것일 뿐, 여전히 특정 쓰레드를 선택할 수 없기 때문에 같은 종류의 쓰레드간의 '기아 현상'이나 '경쟁 상태'가 발생할 가능성은 남아있다.

손님이 원하는 음식의 종류로 `Condition`을 더 세분화하면 통지를 받고도 원하는 음식이 없어서 다시 가디라는 일이 없도록 할 수 있다.

</br>

## 9.4 volatile

멀티 코어 프로세서에서는 코어마다 별도의 캐시를 가지고 있기 때문에 문제가 발생할 가능성이 있다.

코어는 메모리에서 읽어온 값을 캐시에 저장하고 캐시에서 값을 읽어서 작업한다. 다시 같은 값을 읽어올 때는 먼저 캐시에 있는지 확인하고 없을 때만 메모리에서 읽어온다.

그러다보니 도중에 메모리에 저장된 변수의 값이 변경되었는데도 캐시에 저장된 값이 갱신되지 않아서 메모리에 저장된 값이 다른 경우가 발생한다.

![image](https://ifh.cc/g/x4O93P.png)

그러나 위의 오른쪽과 같이 변수 앞에 `volatile`을 붙이면, 코어가 변수의 값을 읽어올 때 캐시가 아닌 메모리에서 읽어오기 때문에 캐시와 메모리간의 값의 불일치가 해결된다.

변수에 `volatile`를 붙이는 대신에 `synchronized`블럭을 사용해도 같은 효과를 얻을 수 있다. 쓰레드가 `synchronized`블럭으로 들어갈 때와 나올 때, 캐시와 메모리간의 동기화가 이루어지기 때문에 값의 불일치가 해소되기 때문이다.

![image](https://ifh.cc/g/rzXq3y.png)

</br>

### volatile로 long과 double을 원자화

JVM은 데이터를 4byte(=32bit)단위로 처리하기 때문에, int와 int보다 작은 타입들은 한 번에 읽거나 쓰는 것이 가능하다. 즉, 단 하나의 명령어로 읽거나 쓰기가 가능하다는 뜻이다. 하나의 명령어는 더 이상 나눌 수 없는 최소의 작업단위이므로, 작업의 중간에 다른 쓰레드가 끼어들 틈이 없다.

그러나, 크기가 8 byte인 long과 double타입의 변수는 하나의 명령어로 값을 읽거나 쓸 수 없기 때문에, 변수의 값을 읽는 과정에 다른 쓰레드가 끼어들 여지가 있다. 다른 쓰레드가 끼어들지 못하게 하려고 변수를 읽고 쓰는 모든 문장을 `synchronized`블럭으로 감쌀 수도 있지만, 더 간단한 방법이 있다. 변수를 선언할 때 `volatile`를 붙이는 것이다.

> 상수에는 volatile를 붙일 수 없다. 즉, 변수에 final과 volatile을 같이 붙일 수 없다. 사실 상수는 변하지 않는 값이므로 멀티쓰레드에 안전(thread-safe)하다. 그래서 volatile을 붙일 필요가 없다.

``` java
volatile long sharedVal;    // long타입의 변수(8 byte)를 원자화
volatile double shareVal;   // double타입의 변수(8 byte)를 원자화
```

`volatile`은 해당 변수에 대한 읽거나 쓰기가 원자화된다. 원자화라는 것은 작업을 더 이상 나눌 수 없게 한다는 의미인데, `synchronized`블럭도 일종의 원자화라고 할 수 있다. 즉, `synchronized`블럭은 여러 문장을 원자화함으로써 쓰레드의 동기화를 구현한 것이라고 보면 된다.

`volatile`은 변수의 읽거나 쓰기를 원자화 할 뿐, 동기화하는 것은 아니다. 동기화가 필요할 때 `synchronized`블럭 대신 `volatile`를 ㅆㄹ 수 없다.

예를 들어 아래와 같은 코드가 있을 때,

``` java
volatile long balane;   // 인스턴스 변수 balance를 원자화한다.

synchronized int getBalance() { // balance의 값을 반환한다.
    return balance;
}

synchronized void withdraw(int money) { // balance의 값을 변경
    if(balance >= money) {
        balance -= money;
    }
}
```

인스턴스변수 `balance`를 `volatile`로 원자화했으니까, 이 값을 읽어서 반환하는 메소드 `getBalance()`를 동기화할 필요가 없다고 생각할 수 있다. 그러나, `getBalance()`를 `synchronized`로 동기화하지 않으면, `withdraw()`가 호출되어 객체에 lock을 걸고 작업을 수행하는 중인데도 `getBalance()`가 호출되는 것이 가능해진다. 출금이 진행 중일 때는 기다렸다가 출금이 끝난 후에 잔고를 조회할 수 있도록 하려면 `getBalance()`에 `synchronized`를 붙여서 동기화를 해야 한다.

</br>

## 9.5 fork & join 프레임워크

JDK1.7부터 'fork & join 프레임워크'이 추가되었고, 이 프레임워크은 하나의 작업을 작은 단위로 나눠서 여러 쓰레드가 동시에 처리하는 것을 쉽게 만들어 준다.

먼저 수행할 자겁에 따라 `RecursiveAction`과 `RecursiveTask`, 두 클래스 중에서 하나를 상속받아 구현해야한다.

> **RecursiveAction** 반환값이 없는 작업을 구현할 때 사용   
> **RecursiveTask** 반환값이 있는 작업을 구현할 때 사용

두 클래스 모두 `compute()`라는 추상 메소드를 가지고 있는데, 우리는 상속을 통해 이 추상 메소드를 구현하기만 하면 된다.

``` java
public abstract class RecursiveAction extends ForkJoinTask<Void> {
        ...
    protected abstract void compute();      // 상속을 통해 이 메소드를 구현해야 한다.
        ...
}

public abstract class RecursiveTask<V> extends ForkJoinTask<V> {
        ...
    V result;
    protected abstract V compute();     // 상속을 통해 이 메소드를 구현해야한다.
        ...
}
```

예를 들어 1부터 n까지의 합을 계산한 결과를 돌려주는 작업의 구현은 다음과 같이 한다.

``` java
class SumTask extends RecursiveTask<Long> { // RecursiveTask를 상속받는다.
    long from, to;

    SumTask(long from, long to) {
        this.from = from;
        this.to = to;
    }

    public Long compute() {
        // 처리할 작업을 수행하기 위한 문장을 넣는다.
    }
}
```

그 다음에는 쓰레드풀과 수행할 작업을 생성하고, `invoke()`로 작업을 시작한다. 쓰레드를 시작할 때 `run()`이 아니라 `start()`를 호출하는 것처럼, fork&join프레임워크으로 수행할 작업도 `compute()`가 아닌 `invoke()`로 시작한다.

``` java
ForkJoinPool pool = new ForkJoinPool(); // 쓰레드 풀을 생성
SumTask task = new SumTask(from, to);   // 수행할 작업을 생성

Long result = pool.invoke(task);    // invoke()를 호출해서 작업을 시작
```

`ForkJoinPool`은 fork & join 프레임워크에서 제공하는 쓰레드 풀(thread pool)로, 지정된 수의 쓰레드를 생성해서 미리 만들어 놓고 반복해서 재사용할 수 있게 한다. 그리고 쓰레드를 반복해서 생성하지 않아도 된다는 장점과 너무 많은 쓰레드가 생성되어 성능이 저하되는 것을 막아준다는 장점이 있다.

쓰레드 풀은 쓰레드가 수행해야하는 작업이 담긴 큐를 제공하며, 각 쓰레드는 자신의 작업 큐에 담긴 작업을 순서대로 처리한다.

> 쓰레드 풀은 기본적으로 코어의 개수가 동일한 개수의 쓰레드를 생성한다.

</br>

### compute()의 구현

`compute()`를 구현할 때는 수행할 작업 외에도 작업을 어떻게 나눌 것인가에 대해서도 알려줘야 한다.

``` java
public Long compute() {
    long size = to - from + 1;  // from ≤ i ≤ to

    if(size <= 5)   // 더할 숫자가 5개 이하면
        return sum();   // 숫자의 합을 반환. sum()은 from부터 to까지의 수를 더해서 반환

    // 범위를 반으로 나눠서 두 개의 작업을 생성
    long half = (from + to) / 2;

    SumTask leftSum = new SumTask(from, half);
    SumTask rightSum = new SumTask(half + 1, to);

    leftSum.fork(); // 작업(leftSum)을 작업 큐에 넣는다.

    return rightSum.compute() + leftSum.join();
}
```

실제 수행할 작업은 `sum()`뿐이고 나머지는 수행할 작업의 범위를 반으로 나눠서 새로운 작업을 생성해서 실행시키기 위한 것이다. 좀 복잡해 보이지만, 작업의 범위를 어떻게 나눌 것인지만 정의해 주면 나머지는 항상 같은 패턴이다.

여기서는 지정된 범위를 절반으로 나누어서 나눠지 범위의 합을 계산하기 위한 새롱누 `SumTask`를 생성하는데, 이 과정은 작업이 더 이상 나눠질 수 없을 때까지, `size`의 값이 5보다 작거나 같을 때까지, 반복딘다.

> compute()의 구조는 일반적인 재귀호출 메소드와 동일하다.

</br>

### 다른 쓰레드의 작업 훔쳐오기

`fork()`가 호출되어 작업 큐에 추가된 작업 역시, `compute()`에 의해 더 이상 나눌 수 없을 때까지 반복해서 나뉘고, 자신의 작업 큐가 비어있는 쓰레드는 다른 쓰레드의 작업 큐에서 작업을 가져와서 수행한다. 이것을 작업 훔쳐오기(work stealing)라고 하며, 이 과정은 모두 쓰레드풀에 의해 자동적으로 이루어진다.

작업 큐가 비어있는 쓰레드가 다른 쓰레드의 작업을 가져와서 수행하는 과정을 통해 한 쓰레드에 작업이 몰리지 않고, 여러 쓰레드가 골고루 작업을 나누어 처리하게 된다.

> 작업의 크기를 충분히 작게 해야 각 쓰레드가 골고루 작업을 나눠가질 수 있다.

</br>

### fork()와 join()

`fork()`는 작업을 쓰레드의 작업 큐에 넣는 것이고, 작업 큐에 들어간 작업은 더 이상 나눌 수 없을 때까지 나뉜다. 즉 `compute()`로 나누고 `fork()`로 작업 큐에 넣는 작업이 계속해서 반복된다. 그리고 나눠진 작업은 각 쓰레드가 골고루 나눠서 처리하고, 작업의 결과는 `join()`을 호출해서 얻을 수 있다.

> **fork()** 해당 작업을 해당 쓰레드 풀의 작업 큐에 넣는다. 비동기 메소드   
> **join()** 해당 작업의 수행이 끝날 때까지 기다렸다가, 수행이 끝나면 그 결과를 반환한다. 동기 메소드

비동기 메소드는 일반적인 메소드와 달리 메소드를 호출만 할 뿐, 그 결과를 기다리지 않는다. (내부적으로는 다른 쓰레드에게 작업을 수행하도록 지시만 하고 결과를 기다리지 않고 돌아오는 것이다.) 그래서 아래의 코드에서, `fork()`를 호출하면 결과를 기다리지 않고 다음 문장인 return문으로 넘어간다.

return문에서 `coompute()`가 재귀호출될 때, `join()`은 호출되지 않는다. 그러다가 작업을 더 이상 나눌 수 없게 되었을 때, `compute()`의 재귀호출은 끝나고 `join()`의 겨로가를 기다렸다가 더해서 결과를 반환한다. 재귀호출된 `compute()`가 모두 종료될 때, 최종 결과를 얻는다.

``` java
public Long compute() {
        ...
    SumTask leftSum = new SumTask(from, half);
    SumTask rightSum = new SumTask(half + 1, to);
    leftSum.fork(); // 비동기 메소드, 호출 후 결과를 기다리지 않는다.

    return rightSum.compute() + leftSum.join(); // 동기 메소드, 호출결과를 기다린다.
}
```

</br>

예제 13-27 / ch13 / ForkJoinEx1.java

``` java
import java.util.concurrent.*;

public class ForkJoinEx1 {
	static final ForkJoinPool pool = new ForkJoinPool();	// 쓰레드 풀을 생성
	
	public static void main(String[] args) {
		long from = 1L, to = 100_000_000L;
		
		SumTask task = new SumTask(from, to);
		
		long start = System.currentTimeMillis();	// 시작시간 초기화
		Long result = pool.invoke(task);
		System.out.println("Elapsed time(4 Core) : " + (System.currentTimeMillis() - start));
		
		System.out.printf("sum of %d~%d=%d%n", from, to, result);
		System.out.println();
		
		result = 0L;
		start = System.currentTimeMillis();	// 시작시간 초기화
		for(long i = from; i <= to; i++)
			result += i;
		
		System.out.println("Elapsed time(1 Core) : " + (System.currentTimeMillis() - start));
		System.out.printf("sum of %d~%d=%d%n", from, to, result);
	}	// main의 끝
}

class SumTask extends RecursiveTask<Long> {
	long from, to;
	
	SumTask(long from, long to) {
		this.from = from;
		this.to = to;
	}
	
	public Long compute() {
		long size = to - from + 1;	// from ≤ i ≤ to
		
		if(size <= 5)	// 더할 숫자가 5개 이하면
			return sum();	// 숫자의 합을 반환
		
		long half = (from + to) / 2;
		
		// 범위를 반으로 나눠서 두 개의 작업을 생성
		SumTask leftSum = new SumTask(from, half);
		SumTask rightSum = new SumTask(half + 1, to);
		
		leftSum.fork();
		
		return rightSum.compute() + leftSum.join();
	}
	
	long sum() {	// from~to의 모든 숫자를 더한 결과를 반환
		long tmp = 0L;
		
		for(long i = from; i <= to; i++)
			tmp += i;
		
		return tmp;
	}
}
```

```
Elapsed time(4 Core) : 941
sum of 1~100000000=5000000050000000

Elapsed time(1 Core) : 726
sum of 1~100000000=5000000050000000
```

실행결과를 보면, fork & join 프레임워크으로 계산한 결과보다 for문으로 계산한 결과가 시간이 덜 걸린 것을 알 수 있다. 왜냐하면, 작업을 나누고 다시 합치는데 걸리는 시간이 있기 때문이다. 재귀호출보다 for문이 더 빠른 것과 같은 이유인데, 항상 멀티쓰레드로 처리하는 것이 빠르다고 생각해서는 안 된다.