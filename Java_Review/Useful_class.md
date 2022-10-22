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

</br>

## 2.3 정규식(Regular Expression) - java.util.regex패키지

정규식이란 텍스트 데이터 중에서 원하는 조건(패턴, pattern)과 일치하는 문자열을 찾아내기 위해 사용하는 것으로 미리 정의된 기호와 문자를 이용해서 작성한 문자열을 말한다.

정규식을 이용하면 많은 양의 텍스트 파일 중에서 원하는 데이터를 손쉽게 뽑아낼 수도 있고 입력된 데이터가 형식에 맞는지를 체크할 수도 있다. 예를 들면 html문서에서 전화번호나 이멩리 주소만을 따로 추출한다던가, 입력한 비밀번호가 숫자와 영문자의 조합으로 되어 있는지 확인할 수도 있다.

예제 9-31 / ch9 / RegularEx1.java

``` java
import java.util.regex.*;	// Pattern과 Matcher가 속한 패키지

public class RegularEx1 {
	public static void main(String[] args) {
		String[] data = {"bat", "baby", "bonus", "cA", "ca", "co", "c.", "c0", "car", "combat", "count", "date", "disc"};
		Pattern p = Pattern.compile("c[a-z]*");	// c로 시작하는 소문자영단어
		
		for(int i = 0; i < data.length; i++) {
			Matcher m = p.matcher(data[i]);
			if(m.matches())
				System.out.print(data[i] + ",");
		}
	}
}
```

```
ca,co,car,combat,count,
```

`data`라는 문자열배열에 담긴 문자열 중에서 지정한 정규식과 일치하는 문자열을 출력하는 예제이다. `Pattern`은 정규식을 정의하는데 사용되고 `Matcher`는 정규식(패턴)을 데이터와 비교하는 역할을 한다. 정규식을 정의하고 데이터를 비교하는 과정을 단계별로 설명하면 다음과 같다.

![image](https://ifh.cc/g/rB8Lsj.png)

> CharSequence는 인터페이스로, 이를 구현한 클래스는 CharBuffer, String, StringBuffer가 있다.

예제 9-32 / ch9 / RegularEx2.java

``` java
import java.util.regex.*;	// Pattern과 Matcher가 속한 패키지

public class RegularEx2 {
	public static void main(String[] args) {
		String[] data = {"bat", "baby", "bonus", "cA", "ca", "co",
				"c.", "c0", "c#", "car", "combat", "count", "date", "disc"};
		
		String[] pattern = {".*", "c[a-z]*", "c[a-z]", "c[a-zA-Z]",
				"c[a-zA-Z0-9]", "c.", "c.*", "c\\.", "c\\w", "c\\d",
				"c.*t", "[b|c].*", ".a.*", ".*a.+", "[b|c].{2}" };
		
		for(int x = 0; x < pattern.length; x++) {
			Pattern p = Pattern.compile(pattern[x]);
			System.out.print("Pattern : " + pattern[x] + " 결과 : ");
			for(int i = 0; i < data.length; i++) {
				Matcher m = p.matcher(data[i]);
				if(m.matches())
					System.out.print(data[i] + ",");
			}
			System.out.println();
		}
	}	// public static void main(String[] args)
}
```

```
Pattern : .* 결과 : bat,baby,bonus,cA,ca,co,c.,c0,c#,car,combat,count,date,disc,
Pattern : c[a-z]* 결과 : ca,co,car,combat,count,
Pattern : c[a-z] 결과 : ca,co,
Pattern : c[a-zA-Z] 결과 : cA,ca,co,
Pattern : c[a-zA-Z0-9] 결과 : cA,ca,co,c0,
Pattern : c. 결과 : cA,ca,co,c.,c0,c#,
Pattern : c.* 결과 : cA,ca,co,c.,c0,c#,car,combat,count,
Pattern : c\. 결과 : c.,
Pattern : c\w 결과 : cA,ca,co,c0,
Pattern : c\d 결과 : c0,
Pattern : c.*t 결과 : combat,count,
Pattern : [b|c].* 결과 : bat,baby,bonus,cA,ca,co,c.,c0,c#,car,combat,count,
Pattern : .a.* 결과 : bat,baby,ca,car,date,
Pattern : .*a.+ 결과 : bat,baby,car,combat,date,
Pattern : [b|c].{2} 결과 : bat,car,
```

자주 쓰일 만한 패턴들을 만들어서 테스트하고 그 결과를 정리하였다. 이 패턴들을 이해하고 나면 정규식에 사용되는 다른 기호를 사용하는 방법도 이해하기 쉽다.

![image](https://ifh.cc/g/jwX3tg.png)

예제 9-33 / ch9 / RegularEx3.java

``` java
import java.util.regex.*;	// Pattern과 Matcher가 속한 패키지

public class RegularEx3 {
	public static void main(String[] args) {
		String source = "HP:011-1111-1111, HOME:02-999-9999 ";
		String pattern = "(0\\d{1,2})-(\\d{3,4})-(\\d{4})";
		
		Pattern p = Pattern.compile(pattern);
		Matcher m = p.matcher(source);
		
		int i = 0;
		while(m.find()) {
			System.out.println( ++i + ": " + m.group() + " -> " + m.group(1)
									+ ", " + m.group(2) + ", " + m.group(3));
		}
	}	// main의 끝
}
```

```
1: 011-1111-1111 -> 011, 1111, 1111
2: 02-999-9999 -> 02, 999, 9999
```

정규식의 일부를 괄호로 나누어 묶어서 그룹화(grouping)할 수 있다. 그룹회된 부분은 하나의 단위로 묶이는 셈이 되어서 한 번 또는 그 이상의 반복을 의미하는 '+'나 '*'가 뒤에 오면 그룹화된 부분이 적용대상이 된다. 그리고 그룹화된 부분은 `group(int i)`를 이용해서 나누어 얻을 수 있다.

위의 예제에서 `(0\\d{1,2})-(\\d{3,4})-(\\d{4})`은 괄호를 이용해서 정규식을 세 부분으로 나누었는데 예제와 결과에서 알 수 있듯이 매칭되는 문자열에서 첫 번째 그룹은 `group(1)`로 두 번째 그룹은 `group(2)`와 같이 호출함으로써 얻을 수 있다. `group()` 또는 `group(0)`은 그룹으로 매칭된 문자열을 전체를 나누어지지 않은 채로 반환한다.

> group(int i)를 호출할 때 i가 실제 그룹의 수보다 많으면 java.lang.IndexOutOfBoundsException이 발생한다.

![image](https://ifh.cc/g/mplh68.png)

`find()`는 주어진 소스 내에서 패턴과 일치하는 부분을 찾아내면 true를 반환하고 찾지 못하면 false를 반환한다. `find()`를 호출해서 패턴과 일치하는 부분을 찾아낸 다음, 다시 `find()`를 호출하면 이전에 발견한 패턴과 일치하는 부분의 다음부터 다시 패턴매칭을 시작한다.

``` java
Matcher m = p.matcher(source);
while(m.find()) {	// find()는 일치하는 패턴이 없으면 false를 반환한다.
	System.out.println(m.group());
}
```

예제 9-34 / ch9 / RegularEx4.java

``` java
import java.util.regex.*;	// Pattern과 Matcher가 속한 패키지

public class RegularEx4 {
	public static void main(String[] args) {
		String source = "A broken hand works, but not a broken heart";
		String pattern = "broken";
		StringBuffer sb = new StringBuffer();
		
		Pattern p = Pattern.compile(pattern);
		Matcher m = p.matcher(source);
		System.out.println("source : " + source);
		
		int i = 0;
		
		while(m.find()) {
			System.out.println(++i + "번째 매칭:" + m.start() + "~" + m.end());
			// broken을 drunken으로 치환하여 sb에 저장한다.
			m.appendReplacement(sb, "drunken");
		}
		
		m.appendTail(sb);
		System.out.println("Replacement count : " + i);
		System.out.println("result : " + sb.toString());		
	}
}
```

```
source : A broken hand works, but not a broken heart
1번째 매칭:2~8
2번째 매칭:31~37
Replacement count : 2
result : A drunken hand works, but not a drunken heart
```

`Matcher`의 `find()`로 정규식과 일치하는 부분을 찾으면, 그 위치를 `start()`와 `end()`로 알아 낼 수 있고 `appendReplacement(StringBuffer sb, String replacement)`를 이용해서 원하는 문자열(replacement)로 치환할 수 있다. 치환된 결과는 `StringBuffer`인 `sb`에 저장되는데, `sb`에 저장되는 내용을 단계별로 살펴보면 이해하기 쉽다.

![image](https://ifh.cc/g/DpZDtZ.png)

</br>

## 2.4 java.util.Scanner클래스

`Scanner`는 화면, 파일, 문자여로가 같은 입력소스로부터 문자데이터를 읽어오는데 도움을 줄 목적으로 JDK1.5부터 추가되었다. `Scanner`에는 다음과 같은 생성자를 지원하기 때문에 다양한 입력소스로부터 데이터를 읽을 수 있다.

``` java
Scanner(String source)
Scanner(File source)
Scanner(InputStream source)
Scanner(Readable source)
Scanner(ReadableByteChannel source)
Scanner(Path source)	// JDK1.7부터 추가
```

또한 `Scanner`는 정규식 표현(Regular expression)을 이용한 라인단위의 검색을 지원하며 구분자(delimiter)에도 정규식 표현을 사용할 수 있어서 복잡한 형태의 구분자도 처리가 가능하다.

``` java
Scanner useDelimiter(Pattern pattern)
Scanner useDelimiter(String pattern)
```

입력받을 값이 숫자라면 `nextLine()`대신 `nextInt()` 또는 `nextLong()`과 같은 메소드를 사용할 수 있다. `Scanner`에서는 이와 같은 메소드를 제공함으로써 입력받은 문자를 다시 변환하는 수고를 덜어 준다.

``` java
boolean nextBoolean()
byte nextByte()
short nextShort()
int nextInt()
long nextLong()
double nextDouble()
float nextFloat()
String nextLine()
```

> 실제 입력된 데이터의 형식에 맞는 메소드를 사용하지 않으면, InputMismatchException이 발생한다.

예제 9-35 / ch9 / ScannerEx1.java

``` java
import java.util.*;

public class ScaanerEx1 {
	public static void main(String[] args) {
		Scanner s = new Scanner(System.in);
		String[] argArr = null;
		
		while(true)	{
			String prompt = ">>";
			System.out.print(prompt);
			
			// 화면으로부터 라인단위로 입력받는다.
			String input = s.nextLine();
			
			input = input.trim();	// 입력받은 값에서 불필요한 앞뒤 공백을 제거한다.
			argArr = input.split(" +");	// 입력받은 내용을 공백을 구분자로 자른다.
			
			String command = argArr[0].trim();
			
			if("".equals(command))	continue;
			
			// 명령어를 소문자로 바꾼다.
			command = command.toLowerCase();
			
			// q 또는 Q를 입력하면 실행종료한다.
			if(command.equals("q")) {
				System.exit(0);
			} else {
				for(int i = 0; i < argArr.length; i++) {
					System.out.println(argArr[i]);
				}
			}
		}	// while(true)
	}	// main
}
```

```
>>hello
hello
>>hello   123
hello
123
>>hello 123 456
hello
123
456
>>
>>q
```

화면으로부터 라인단위로 입력받아서 입력받은 내용을 공백을 구분자로 나눠서 출력하는 예제이다. 입력받은 라인의 단어는 공백이 여러 개 일 수 있으므로 정규식을 " +"로 하였다. 이 정규식의 의미는 하나 이상의 공백을 의미한다.

``` java
argArr = input.split(" +");	// 입력받은 내용을 공백을 구분자로 자른다.
```

예제 9-36 / ch9 / ScannerEx2.java

``` java
import java.util.Scanner;
import java.io.File;

public class ScannerEx2 {
	public static void main(String[] args) throws Exception {
		Scanner sc = new Scanner(new File("data2.txt"));
		int sum = 0;
		int cnt = 0;
		
		while(sc.hasNextInt()) {
			sum += sc.nextInt();
			cnt++;
		}
		
		System.out.println("sum = " + sum);
		System.out.println("average = " + (double)sum / cnt);
	}
}
```

```
c:\jdk1.8\work\ch9>java ScannerEx2
sum = 1500
average = 300.0

c:\jdk1.8\work\ch9>type data2.txt
100
200
300
400
500
```

data2.txt파일로부터 데이터를 읽어서 합과 평균을 계산하는 예제이다. 여기서는 data2.txt파일이 예제소스파일인 ScannerEx2.java와 같은 디렉토리에 있어서 경로없이 파일명만 지정해주었지만 소스파일과 다른 디렉토리에 위치한 파일을 읽기 위해서는 파일명에 경로도 함께 지정해주어야 한다.

예제 9-37 / ch9 / ScannerEx3.java

``` java
import java.util.Scanner;
import java.io.File;

public class ScannerEx3 {
	public static void main(String[] args) throws Exception {
		Scanner sc = new Scanner(new File("data3.txt"));
		int cnt = 0;
		int totalSum = 0;
		
		while(sc.hasNextLine()) {
			String line = sc.nextLine();
			Scanner sc2 = new Scanner(line).useDelimiter(",");
			int sum = 0;
			
			while(sc2.hasNextInt()) {
				sum += sc2.nextInt();
			}
			System.out.println(line + ", sum = " + sum);
			totalSum += sum;
			cnt++;
		}
		System.out.println("Line : " + cnt + ", Total : " + totalSum);
	}
}
```

```
c\:jdk1.8\work\ch9>java ScannerEx3
100,100,100, sum = 300
200,200,200, sum = 600
300,300,300, sum = 900
400,400,400, sum = 1200
500,500,500, sum = 1500
Line : 5, Total : 4500

c:\jdk1.8\work\ch9>type data3.txt
100,100,100
200,200,200
300,300,300
400,400,400
500,500,500
```

이전 예제와 같이 파일로부터 데이터를 읽어서 계산하는 예제인데 이전과는 달리 ','를 구분자로 한 라인에 여러 데이터가 저장되어 있다. 이럴 때는 파일의 내용을 먼저 라인별로 읽은 다음에 다시 ','를 구분자로 하는 `Scanner`를 이용해서 각각의 데이터를 읽어야 한다.

</br>

## 2.5 java.util.StringTokenizer클래스

`StringTokenizer`는 긴 문자열을 지정된 구분자(delimiter)를 기준으로 토큰(token)이라는 여러 개의 문자열로 잘라내는 데 사용한다. 예를 들어 "100,200,300,400"이라는 문자열이 있을 때 ','를 구분자로 잘라내면 "100", "200", "300", "400"이라는 4개의 문자열(토큰)을 얻을 수 있다.

`StringTokenizer`를 이용하는 방법 이외에도 아래와 같이 `String`의 `split(String regex)`이나 `Scanner`의 `useDelimiter(String pattern)`를 사용할 수는 있지만,

``` java
String[] result = "100,200,300,400".split(",");
Scanner sc2 = new Scanner("100,200,300,400").useDelimiter(",");
```

이 두 가지 방법은 정규식 표현(Regular expression)을 사용해야하므로 정규식 표현에 익숙하지 않은 경우 `StringTokenizer`를 사용하는 것이 간단하면서도 명확한 결과를 얻을 수 있다.

그러나 `StringTokenizer`는 구분자로 단 하나의 문자 밖에 사용하지 못하기 때문에 보다 복잡한 형태의 구분자로 문자열을 나누어야 할 때는 어쩔 수 없이 정규식을 사용하는 메소드를 사용해야 한다.

</br>

### StringTokenizer의 생성자와 메소드

`StringTokenizer`의 주로 사용되는 생성자와 메소드는 다음과 같다.

![image](https://ifh.cc/g/JRmPjx.png)

예제 9-38 / ch9 / StringTokenizerEx1.java

``` java
import java.util.*;

public class StringTokenizerEx1 {
	public static void main(String[] args) {
		String source = "100,200,300,400";
		StringTokenizer st = new StringTokenizer(source, ",");
		
		while(st.hasMoreTokens()) {
			System.out.println(st.nextToken());
		}
	} // main의 끝
}
```

```
100
200
300
400
```

','를 구분자로 하는 `StringTokenizer`를 생성해서 문자열(source)을 나누어 출력하는 예제이다.

예제 9-39 / ch9 / StringTokenizerEx2.java

``` java
import java.util.*;

public class StringTokenizerEx2 {
	public static void main(String[] args) {
		String expression = "x=100*(200+300)/2";
		StringTokenizer st = new StringTokenizer(expression, "+-*/=()", true);
		
		while(st.hasMoreTokens()) {
			System.out.println(st.nextToken());
		}
	}	// main의 끝
}
```

```
x
=
100
*
(
200
+
300
)
/
2
```

생성자 `StringTokenizer(String str, String delim, boolean returnDelims)`를 사용해서 구분자도 토큰으로 간주되도록 하였다.

``` java
StringTokenizer st = new StringTokenizer(expression, "+-*/=()", true);
```

`StringTokenizer`는 단 한 문자의 구분자만 사용할 수 있기 때문에, "+-*/=()"가 전체가 하나의 구분자가 아니라 각각의 문자가 모두 구분자라는 것이다.

> 만일 구분자가 두 문자 이상이라면, Scanner나 String클래스의 split메소드를 사용해야 한다.

예제 9-40 / ch9 / StringTokenizerEx3.java

``` java
import java.util.*;

public class StringTokenizerEx3 {
	public static void main(String[] args) {
		String source = "1,김천재,100,100,100|2,박수재,95,80,90|3,이자바,80,90,90";
		StringTokenizer st = new StringTokenizer(source, "|");
		
		while(st.hasMoreTokens()) {
			String token = st.nextToken();
			
			StringTokenizer st2 = new StringTokenizer(token, ",");
			while(st2.hasMoreTokens()) {
				System.out.println(st2.nextToken());
			}
			System.out.println("-------");
		}
	}	// main
}
```

```
1
김천재
100
100
100
-------
2
박수재
95
80
90
-------
3
이자바
80
90
90
-------
```

문자열에 포함된 데이터가 두 가지 종류의 구분자로 나뉘어져 있을 때 두 개의 `StringTokenizer`와 이중 반복문을 사용해서 처리하는 방법을 보여주는 예제이다. 한 학생의 정보를 구분하기위해 "|"를 사용하였고, 학생의 이름과 점수 등을 구분하기 위해 ","를 사용하였다.

예제 9-41 / ch9 / StringTokenizerEx4.java

``` java
import java.util.*;

public class StringTokenizerEx4 {
	public static void main(String[] args) {
		String input = "삼십만삼천백십오";
		System.out.println(input);
		System.out.println(hagulToNum(input));
	}
	
	public static long hagulToNum(String input) {	// 한글을 숫자로 바꾸는 메소드
		long result = 0;	// 최종 변환결과를 저장하기 위한 변수
		long tmpResult = 0;	// 십백천 단위의 값을 저장하기 위한 임시변수
		long num = 0;
		
		final String NUMBER = "영일이삼사오육칠팔구";
		final String UNIT = "십백천만억조";
		final long[] UNIT_NUM = {10,100,1000,10000,(long)1e8,(long)1e12};
		
		StringTokenizer st = new StringTokenizer(input, UNIT, true);
		
		while(st.hasMoreTokens()) {
			String token = st.nextToken();
			int check = NUMBER.indexOf(token);	// 숫자인지, 단위(UNIT)인지 확인한다.
			
			if(check==-1) {	// 단위인 경우
				if("만억조".indexOf(token)==-1) {
					tmpResult += (num!=0 ? num : 1) * UNIT_NUM[UNIT.indexOf(token)];
				} else {
					tmpResult += num;
					result += (tmpResult!=0 ? tmpResult : 1)*UNIT_NUM[UNIT.indexOf(token)];
					tmpResult = 0;
				}
				num = 0;
			} else {	// 숫자인 경우
				num = check;
			}
		}	// end of while
		
		return result + tmpResult + num;
	}
}
```

```
삼십만삼천백십오
303115
```

한글로 된 숫자를 아리비아 숫자로 변환하는 예제이다.

먼저 `tmpResult`는 "만억조"와 같은 큰 단위가 나오기 전까지 "십백천"단위의 값을 저장하는 임시공간이고, `reuslt`는 실제 결과 값을 저장하기 위한 공간이다.

한글로 된 숫자를 구분자(단위)로 잘라서, 토큰이 숫자면 `num`에 저장하고 단위면 `num`에다 단위(UNIT_NUM배열 중의 한 값)를 곱해서 `tmpResult`에 저장한다. 예를 들어 "삼십"이면 '3 * 10 = 30'이 되어 30이 `tmpReuslt`에 저장된다.

그리고 "만삼천"과 같이 숫자 없이 바로 단위로 시작하는 경우에는 `num`의 값이 0이기 때문에 단위의 값을 곱해도 그 결과가 0이 됨으로 삼항 연산자를 이용해서 `num`의 값을 1로 바꾼 후 단위값을 곱하도록 하였다.

``` java
result += (tmpResult!=0 ? tmpResult : 1)*UNIT_NUM[UNIT.indexOf(token)];
```

그 다음에 "만억조"와 같이 큰 단위가 나오면 `tmpResult`에 저장된 값에 큰 단위 값을 곱해서 `result`에 저장하고 `tmpResult`는 0으로 초기화 한다. 예를 들어 "삼십만"은 `tmpResult`에 저장되어 있던 30에 10000을 곱해서 `result`에 저장하고, `tmpResult`는 0으로 초기화 한다.

``` java
tmpResult += num;
result += (tmpResult != 0 ? tmpResult : 1) * UNIT_NUM(UNIT.indexOf(token));
tmpResult = 0;
```

예제 9-42 / ch9 / StringTokenizerEx5.java

``` java
import java.util.*;

public class StringTokenizerEx5 {
	public static void main(String[] args) {
		String data = "100,,,200,300";
		
		String[] result = data.split(",");
		StringTokenizer st = new StringTokenizer(data, ",");
		
		for(int i = 0; i < result.length; i++) {
			System.out.print(result[i] + "|");
		}
		
		System.out.println("개수 : " + result.length);
		
		int i = 0;
		for(; st.hasMoreTokens(); i++) {
			System.out.print(st.nextToken() + "|");
		}
		System.out.println("개수 : " + i);
	}	// main
}
```

```
100|||200|300|개수 : 5
100|200|300|개수 : 3
```

구분자를 ','로 하는 문자열 데이터를 `String`클래스의 `split()`과 `StringTokenizer`로 잘라낸 결과를 비교하는 예제이다. 실행결과를 보면, `split()`은 빈 문자열도 토큰으로 인식하는 반면 `StringTokenizer`는 빈 문자열을 토큰으로 인식하지 않기 때문에 인식하는 토큰의 개수가 서로 다른 것을 알 수 있다.

이 외에도 성능의 차이가 있는데, `split()`은 데이터를 토큰으로 잘라낸 결과를 배열에 담아서 변환하기 때문에 데이터를 토큰으로 바로바로 잘라서 반환하는 `StringTokenizer`보다 성능이 떨어질 수밖에 없다.