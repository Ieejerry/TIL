Chapter 9. java.lang패키지와 유용한 클래스

# 2. 유용한 클래스

</br>

## 2.1 java.util.Objects클래스

`Object`클래스의 보조 클래스로 `Math`클래스처럼 모든 메소드가 `static`이다. 객체의 비교나 널 체크(null check)에 유용하다.

`isNull()`은 해당 객체가 널인지 확인해서 null이면 true를 반환하고 아니면 false를 반환한다. `nonNull()`은 `isNull()`과 정반대의 일을 한다. 즉, `!Objects.isNull(obj)`와 같다.

``` java
static boolean isNull(Object obj)
static boolean nonNull(Object obj)
```

그리고 `requireNonNull()`은 해당 객체가 널이 아니어야 하는 경우에 사용한다. 만일 객체가 널이면, `NullPointException`을 발생시킨다. 두 번째 매개변수로 지정하는 문자열은 예외의 메세지가 된다.

``` java
static <T> T requireNonNull(T obj)
static <T> T requireNonNull(T obj, String message)
static <T> T requireNonNull(T obj, Supplier<String> messageSupplier)
```

예전 같으면, 매개변수의 유효성 검사를 다음과 같이 해야 하는데, 이제는 `requireNonNull()`의 호출만으로 간단히 끝낼 수 있다.

``` java
void setName(String name) {
    if(name==null)
        throw new NullPointException("name must not be null.");

    this.name = name;
}
```

<center>↓</center>

``` java
void setName(String name) {
    this.name = Objects.requireNonNull(name, "name must not be null.");
}
```

`Objects`에 `compare()`는 두 비교대상이 같으면 0, 크면 양수, 작으면 음수를 반환한다.

``` java
static int compare(Object a, Object b, Object c)
```

이 메소드는 `a`와 `b` 두 객체를 비교하는데, 두 객체를 비교하는데 사용할 비교 기준이 필요하다. 그 역할을 하는 것이 Comparator이다.

``` java
static boolean equals(Object a, Obejct b)
static boolean deepEquals(Object a, Object b)
```

`Objects`클래스에도 `equals()`가 있는데, 이 메소드의 장점은 null검사를 하지 않아도 된다.

``` java
if(a!=null&&a.equals(b)) {  // a가 null인지 반드시 확인해야 한다.
    ...
}
```

<center>↓</center>

``` java
if(Objects.equals(a, b)) {  // 매개변수의 값이 null인지 확인할 필요가 없다.
    ...
}
```

`equals()`의 내부에서 `a`와 `b`의 널 검사를 하기 때문에 따로 널 검사를 위한 조건식을 따로 넣지 않아도 된다.

``` java
public static boolean equals(Object a, Object b) {
    return(a == b) || (a != null && a.equals(b));
}
```

`a`와 `b`가 모두 널인 경우에는 참을 반환한다는 점을 빼고는 특별한 것이 없다. `deepEquals()`는 객체를 재귀적으로 비교하기 때문에 다차원 배열의 비교도 가능하다.

``` java
String[][] str2D = new String[][]{{"aaa", "bbb"}, {"AAA", "BBB"}};
String[][] str2D2 = new String[][]{{"aaa", "bbb"}, {"AAA", "BBB"}};

System.out.println(Objects.equals(str2D, str2D2));  // false
System.out.println(Objects.deepEquals(str2D, str2D2));  // true
```

``` java
static String toString(Object o)
static String toString(Object o, String nullDefault)
```

`toString()`도 `equals()`처럼, 내부적으로 널 검사를 한다는 것 빼고는 특별한 것이 없다. 두 번째 메소드는 o가 널일 때, 대신 사용할 값을 지정할 수 있어서 유용하다.

마지막으로 `hashCode()`인데, 이것 역시 내부적으로 널 검사를 한 후에 `Object`클래스의 `hashCode()`를 호출할 뿐이다.

``` java
static int hashCode(Object o)
static int hash(Object... values)
```

보통은 클래스에 선언된 인스턴스의 변수들의 `hashCode()`를 조합해서 반환하도록, `hashCode()`를 오버라이딩하는데, 그 대신 매개변수의 타입이 가변인자인 두 번째 메소드를 사용하면 편리하다.

예제 9-26 / ch9 / ObjectsTest.java

``` java
import java.util.*;
import static java.util.Objects.*;	// Objects클래스의 메소드를 static import

public class ObjectsTest {
	public static void main(String[] args) {
		String[][] str2D = new String[][] {{"aaa", "bbb"}, {"AAA", "BBB"}};
		String[][] str2D_2 = new String[][] {{"aaa", "bbb"}, {"AAA", "BBB"}};
		
		System.out.print("str2D = {");
		for(String[] tmp : str2D)
			System.out.print(Arrays.toString(tmp));
		System.out.println("}");
		
		System.out.print("str2D_2= {");
		for(String[] tmp : str2D_2)
			System.out.print(Arrays.toString(tmp));
		System.out.println("}");
		
		System.out.println("equals(str2D, str2D_2)=" + Objects.equals(str2D, str2D_2));
		System.out.println("deepEquals(str2D, str2D_2)=" + Objects.deepEquals(str2D, str2D_2));
		
		System.out.println("isNull(null) =" + isNull(null));
		System.out.println("nonNull(null) =" + nonNull(null));
		System.out.println("hashCode(null) =" + Objects.hashCode(null));
		System.out.println("toString(null) =" + Objects.toString(null));
		System.out.println("toString(null, \"\") =" + Objects.toString(null, ""));
		
		Comparator c = String.CASE_INSENSITIVE_ORDER;	// 대소문자 구분 안하는 비교
		
		System.out.println("compare(\"aa\", \"bb\")=" + compare("aa", "bb", c));
		System.out.println("compare(\"bb\", \"aa\")=" + compare("bb", "aa", c));
		System.out.println("compare(\"ab\", \"AB\")=" + compare("ab", "AB", c));
	}
}
```

```
str2D = {[aaa, bbb][AAA, BBB]}
str2D_2= {[aaa, bbb][AAA, BBB]}
equals(str2D, str2D_2)=false
deepEquals(str2D, str2D_2)=true
isNull(null) =true
nonNull(null) =false
hashCode(null) =0
toString(null) =null
toString(null, "") =
compare("aa", "bb")=-1
compare("bb", "aa")=1
compare("ab", "AB")=0
```

static import문을 사용했음에도 불구하고 `Object`클래스의 메소드와 일므이 같은 것들은 충돌이 난다. 즉, 컴파일러가 구별을 못한다. 그럴 때는 클래스의 이름을 붙여줄 수밖에 없다. 그리고 `String`클래스에 상수로 정의되어 있는 `Comparator`가 있어서 그걸 사용해서 `compare()`를 호출했다.

``` java
Comparator c = String.CAsE_INSENSITIVE_ORDER;   // 대소문자 구분안하는 비교
    ...
System.out.println("compare(\"ab\", \"AB\")=" + compare("ab", "AB", c));
```

이 `Comparator`는 문자열을 대소문자 구분하지 않고 비교할 때 사용하기 위한 것이다. 그래서 아래와 같이 "ab"와 "AB"를 비교한 결과가 0, 즉 두 문자열이 같다는 결과가 나온다.

</br>

## 2.2 java.util.Random클래스

`Random`클래스를 사용하면 난수를 얻을 수 있다 `Math.random()`은 내부적으로 `Random`클래스의 인스턴스를 생성해서 사용하는 것이므로 둘 중에서 편한 것을 사용하면 된다. 아래의 두 문장은 동등하다.

``` java
double randNum = Math.random();
double randNum = new Random().nextDouble();	// 위의 문장과 동일
```

예를 들어 1~6사이의 정수를 난수로 얻고자 할 때는 다음과 같다.

``` java
int num = (int)(Math.random() * 6) + 1;
int num = new Random().nextInt(6) + 1;	// nextInt(6)은 0~6사이의 정수를 반환
```

`Math.random()`과 `Random`의 가장 큰 차이점이라면, 종가값(seed)을 설정할 수 있다. 종자값이 같은 `Random`인스턴스들은 항상 같은 난수를 같은 순서대로 반환한다. 종자값은 난수를 만드는 공식에 사용되는 값으로 같은 공식에 같은 값을 넣으면 같은 결과를 얻는 것처럼 같은 종자값을 넣으면 같은 난수를 얻게 된다.

</br>

### Random클래스의 생성자와 메소드

생성자 `Random()`은 아래와 같이 종자값을 `System.currentTimeMillis()`로 하기 때문에 실행할 때마다 얻는 난수가 달라진다.

> System.currentTimeMillis()는 현재시간을 천분의 1초단위로 변환해서 반환한다.

``` java
public Random() {
	this(System.currentTimeMillis());	// Random(long seed)를 호출한다.
}
```

`Random`클래스의 메소드 목록인데, 별로 특별한 것은 없다. 각 메소드가 반환하는 값의 범위와 `nextBytes()`는 `BigInteger(int signum, byte[] magnitude)`와 함께 사용하면 int의 범위인 '-2<sup>31</sup>~2<sup>31</sup>-1'보다 넓은 범위의 난수를 얻을 수 있다.

![image](https://ifh.cc/g/zn1ccq.png)

예제 9-27 / ch9 / RandomEx1.java

``` java
import java.util.*;

public class RandomEx1 {
	public static void main(String[] args) {
		Random rand = new Random(1);
		Random rand2 = new Random(1);
		
		System.out.println("= rand =");
		for(int i = 0; i < 5; i++) {
			System.out.println(i + ":" + rand.nextInt());
		}
		
		System.out.println();
		System.out.println("- rand2 =");
		for(int i = 0; i < 5; i++) {
			System.out.println(i + ":" + rand2.nextInt());
		}
	}
}
```

```
= rand =
0:-1155869325
1:431529176
2:1761283695
3:1749940626
4:892128508

- rand2 =
0:-1155869325
1:431529176
2:1761283695
3:1749940626
4:892128508
```

`Random`인스턴스 `rand`와 `rand2`가 같은 종자값(seed)을 사용하기 때문에 같은 값들을 같은 순서로 얻는 것을 확인할 수 있다. 같은 종자값을 갖는 `Random`인스턴스는 시스템이나 실행시간 등에 관계없이 항상 같은 값을 같은 순서로 반환할 것을 보장한다.

예제 9-28 / ch9 / RandomEx2.java

``` java
import java.util.*;

public class RandomEx2 {
	public static void main(String[] args) {
		Random rand = new Random();
		int[] number = new int[100];
		int[] counter = new int[10];
		
		for(int i = 0; i < number.length; i++) {
//			System.out.print(number[i] = (int)(Math.random() * 10));
//			0<=x<10 범위의 정수 x를 반환한다.
			System.out.print(number[i] = rand.nextInt(10));
		}
		System.out.println();
		
		for(int i = 0; i < number.length; i++) {
			counter[number[i]]++;
		}
		
		for(int i = 0; i < counter.length; i++) {
			System.out.println(i + "의 개수 :" + printGraph('#', counter[i]) + " " + counter[i]);
		}
	}
	
	public static String printGraph(char ch, int value) {
		char[] bar = new char[value];
		
		for(int i = 0; i < bar.length; i++) {
			bar[i] = ch;
		}
		
		return new String(bar);
	}
}
```

```
0718101419063444969567290464722815742927705437186649116706349013749021608067471289910750987670175401
0의 개수 :############## 14
1의 개수 :############## 14
2의 개수 :####### 7
3의 개수 :#### 4
4의 개수 :############# 13
5의 개수 :##### 5
6의 개수 :########### 11
7의 개수 :############### 15
8의 개수 :###### 6
9의 개수 :########### 11
```

0~9 사이의 난수를 100개 발생시키고 각 숫자의 빈도수를 센 다음 그래프를 그리는 예제이다. `nextInt(int n)`는 0부터 n사이의 정수를 반환한다. 단, n의 범위에 포함되지 않는다.

예제 9-29 / ch9 / RandomEx3.java

``` java
import java.util.*;

public class RandomEx3 {
	public static void main(String[] args) {
		for(int i = 0; i < 10; i++) {
			System.out.print(getRand(5, 10)+",");
		}
		System.out.println();
		
		int[] result = fillRand(new int[10], new int[] { 2, 3, 7, 5 });
		
		System.out.println(Arrays.toString(result));
	}
	
	public static int[] fillRand(int[] arr, int from, int to) {
		for(int i = 0; i < arr.length; i++) {
			arr[i] = getRand(from, to);
		}
		
		return arr;
	}
	
	public static int[] fillRand(int[] arr, int[] data) {
		for(int i = 0; i < arr.length; i++) {
			arr[i] = data[getRand(0, data.length-1)];
		}
		
		return arr;
	}
	
	public static int getRand(int from, int to) {
		return (int)(Math.random() * (Math.abs(to-from) + 1)) + Math.min(from, to);
	}
}
```

```
7,5,6,6,9,10,8,5,6,10,
[5, 3, 2, 7, 5, 2, 7, 2, 3, 3]
```

![image](https://ifh.cc/g/Mq2ob2.png)

예제 9-30 / ch9 / RandomEx4.java

``` java
import java.util.*;

public class RandomEx4 {
	final static int RECORD_NUM = 10;	// 생성할 레코드의 수를 정한다.
	final static String TABLE_NAME = "TEST_TABLE";
	final static String[] CODE1 = {"010", "011", "017", "018", "019"};
	final static String[] CODE2 = {"남자", "여자"};
	final static String[] CODE3 = {"10대", "20대", "30대", "40대", "50대"};
	
	public static void main(String[] args) {
		for(int i = 0; i < RECORD_NUM; i++) {
			System.out.println(" INSERT INTO " + TABLE_NAME
					+ " VALUES ("
					+ " '" + getRandArr(CODE1) + "'"
					+ ", '" + getRandArr(CODE2) + "'"
					+ ", '" + getRandArr(CODE3) + "'"
					+ ",  " + getRand(100, 200)	// 100~200 사이의 값을 얻는다.
					+ "); ");
		}
	}
	
	public static String getRandArr(String[] arr) {
		return arr[getRand(arr.length-1)];	// 배열에 저장된 값 중 하나를 반환한다.
	}
	
	public static int getRand(int n) { return getRand(0, n); }
	public static int getRand(int from, int to) {
		return (int)(Math.random() * (Math.abs(to-from)+1)) + Math.min(from, to);
	}
}
```

```
 INSERT INTO TEST_TABLE VALUES ( '019', '남자', '30대',  146); 
 INSERT INTO TEST_TABLE VALUES ( '018', '여자', '30대',  134); 
 INSERT INTO TEST_TABLE VALUES ( '019', '남자', '10대',  164); 
 INSERT INTO TEST_TABLE VALUES ( '017', '남자', '30대',  128); 
 INSERT INTO TEST_TABLE VALUES ( '011', '남자', '40대',  176); 
 INSERT INTO TEST_TABLE VALUES ( '011', '남자', '20대',  168); 
 INSERT INTO TEST_TABLE VALUES ( '017', '여자', '50대',  127); 
 INSERT INTO TEST_TABLE VALUES ( '011', '여자', '20대',  147); 
 INSERT INTO TEST_TABLE VALUES ( '010', '여자', '20대',  117); 
 INSERT INTO TEST_TABLE VALUES ( '017', '남자', '50대',  129); 
```

데이터베이스에 넣을 테스트 데이터를 만드는 예제이다. 지금까지는 연속적인 범위 내에서 값을 얻어왔지만, 때로는 이 예제와 같이 불연속적인 범위에 있는 값을 임의로 얻어 와야 하는 경우도 있다.

이런 경우 불연속적인 값을 배열에 저장한 후, 배열의 index를 임의로 얻어서 배열에 저장된 값을 읽어오도록 하면 된다.