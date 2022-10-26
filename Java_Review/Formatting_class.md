Chapter 10. 날짜와 시간 & 형식화 date, time and formatting

# 2. 형식화 클래스

형식화 클래스는 `java.text`패키지에 포함되어 있으며 숫자, 날짜, 텍스트 데이터를 일정한 형식에 맞게 표현할 수 있는 방법을 객체지향적으로 설계하여 표준화하였다.

형식화 클래스는 형식화에 사용될 패턴을 정의하는데, 데이터를 정의된 패턴에 맞춰 형식화할 수 있을 뿐만 아니라 역으로 형식화된 데이터에서 원래의 데이터를 얻어낼 수도 있다.

이것은 마치 "123"과 같은 문자열을 `Integer.parseInt()`를 사용해서 123이라는 숫자로 변환하는 것과 같은 일이 가능하다는 것을 의미한다. 즉, 형식화된 데이터의 패턴만 정의해주면 복잡한 문자열에서도 `substring()`을 사용하지 않고도 쉽게 원하는 값을 얻어낼 수 있다.

</br>

## 2.1 DecimalFormat

형식화 클래스 중에서 숫자를 형식화하는데 사용되는 것이 `DecimalFormat`이다. `DecimalFormat`을 이용하면 숫자 데이터를 정수, 부동소수점, 금액 등의 다양한 형식으로 표현할 수 있으며, 반대로 일정한 형식의 텍스트 데이터를 숫자로 쉽게 변환하는 것도 가능하다.

형식화 클래스에서는 원하는 형식으로 표현 또는 변환하기 위해서 패턴을 정의하는데, 형식화 클래스에서는 패턴을 저으이하는 것이 전부라고 해도 과언이 아니다.

아래의 표에 `DecimalFormat`의 패턴의 작성에 사용되는 기호와 설명, 그리고 자주 사용될 만한 패턴들을 예로 들었다.

![image](https://ifh.cc/g/BPPLQP.png)

`DecimalFormat`을 사용하는 방법은 간단하다. 먼저 원하는 출력형식의 패턴을 작성하여 `DecimalFormat`인스턴스를 생성한 다음, 출력하고자 하는 문자여롤 `format`메소드를 호출하면 원하는 패턴에 맞게 변환된 문자열을 얻게 된다.

``` java
double number = 1234567.89;
DecimalFormat df = new DecimalFormat("#.#E0");
String result = df.format(number);
```

</br>

예제 10-10 / ch10 / DecimalFormatEx1.java

``` java
import java.text.DecimalFormat;

public class DecimalFormatEx1 {
	public static void main(String[] args) {
		double number = 1234567.89;
		String[] pattern = {
				"0",
				"#",
				"0.0",
				"#.#",
				"0000000000.0000",
				"##########.####",
				"#.#-",
				"-#.#",
				"#,###.##",
				"#,####.##",
				"#E0",
				"0E0",
				"##E0",
				"00E0",
				"####E0",
				"0000E0",
				"#.#E0",
				"0.0E0",
				"0.000000000E0",
				"00.00000000E0",
				"000.0000000E0",
				"#.#########E0",
				"##.########E0",
				"###.#######E0",
				"#,###.##+;#,###.##-",
				"#.#%",
				"#.#\u2030",
				"\u00A4 #,###",
				"'#'#,###",
				"''#,###",
		};
		
		for(int i = 0; i < pattern.length; i++) {
			DecimalFormat df = new DecimalFormat(pattern[i]);
			System.out.printf("%19s : %s\n", pattern[i], df.format(number));
		}
	}
}
```

```
                  0 : 1234568
                  # : 1234568
                0.0 : 1234567.9
                #.# : 1234567.9
    0000000000.0000 : 0001234567.8900
    ##########.#### : 1234567.89
               #.#- : 1234567.9-
               -#.# : -1234567.9
           #,###.## : 1,234,567.89
          #,####.## : 123,4567.89
                #E0 : .1E7
                0E0 : 1E6
               ##E0 : 1.2E6
               00E0 : 12E5
             ####E0 : 123.5E4
             0000E0 : 1235E3
              #.#E0 : 1.2E6
              0.0E0 : 1.2E6
      0.000000000E0 : 1.234567890E6
      00.00000000E0 : 12.34567890E5
      000.0000000E0 : 123.4567890E4
      #.#########E0 : 1.23456789E6
      ##.########E0 : 1.23456789E6
      ###.#######E0 : 1.23456789E6
#,###.##+;#,###.##- : 1,234,567.89+
               #.#% : 123456789%
               #.#‰ : 1234567890‰
            ¤ #,### : ₩ 1,234,568
           '#'#,### : #1,234,568
            ''#,### : '1,234,568
```

자주 사용될 만한 패턴들을 작성해서 테스트한 예제이다.

</br>

예제 10-11 / ch10 / DecimalFormatEx2.java

``` java
import java.text.DecimalFormat;

public class DecimalFormatEx2 {
	public static void main(String[] args) {
		DecimalFormat df = new DecimalFormat("#,###.##");
		DecimalFormat df2 = new DecimalFormat("#.###E0");
		
		try {
			Number num = df.parse("1,234,567.89");
			System.out.print("1,234,567.89" + " -> ");
			
			double d = num.doubleValue();	// d = 1234567.89
			System.out.print(d + " -> ");
			
			System.out.println(df2.format(num));
		} catch (Exception e) {}
	}	// main
}
```

```
1,234,567.89 -> 1234567.89 -> 1.235E6
```

패턴을 이용해서 숫자를 다르게 변환하는 예제이다. `parse`메소드를 이용하면 기호와 문자가 포함된 문자열을 숫자로 쉽게 변환할 수 있다.

> Integer.parseInt메소드는 콤마(,)가 포함된 문자열을 숫자로 변환하지 못한다.

`parse(String source)`는 `DecimalFormat`의 조상인 `NumberFormat`에 정의된 메소드이며, 이 메소드의 선언부는 다음과 같다.

``` java
public Number parse(String source) throws ParseException
```

`Number`클래스는 `Integer.Double`과 같은 숫자를 저장하는 래퍼 클래스의 조상이며, `doubleValue()`는 `Number`에 저장된 값을 double형의 값으로 변환하여 반환한다. 이 외에도 `intValue()`, `floatValue()`등의 메소드가 `Number`클래스에 정의되어 있다.

</br>

## 2.2 SimpleDateFormat

`Date`와 `Calendar`만으로 날짜 데이터를 원하는 형태로 다양하게 출력하는 것은 불편하고 복잡하다. 그러나 `SimpleDateFormat`을 사용하면 이러한 문제들이 간단히 해결된다.

> DateFormat은 추상클래스로 SimpleDateFormat의 조상이다. DateFormat는 추상클래스이므로 인스턴스를 생성하기 위해서는 getDateInstance()와 같은 static메소드를 이용해야 한다. getDateInstance()에 의해서 반환되는 것은 DateFormat을 상속받아 완전하게 구현한 SimpleDateFormat인스턴스이다.

![image](https://ifh.cc/g/QWMkD3.png)

`SimpleDateFormat`을 사용하는 방법은 간단하다. 먼저 원하는 출력형식의 패턴을 작성하여 `SimpleDateFormat`인스턴스를 생성한 다음, 출력하고자 하는 `Date`인스턴스를 가지고 `format(Date d)`를 호출하면 지정한 출력형식에 맞게 변환된 문자열을 얻게 된다.

``` java
Date today = new Date();
SimpleDateFormat df = new SimpleDateFormat("yyyy-MM-dd");

// 오늘 날짜를 yyyy-MM-dd형태로 변환하여 반환한다.
String result = df.format(today);
```

</br>

예제 10-12 / ch10 / DateFormatEx1.java

``` java
import java.text.SimpleDateFormat;
import java.util.Date;

public class DateFormatEx1 {
	public static void main(String[] args) {
		Date today = new Date();
		
		SimpleDateFormat sdf1, sdf2, sdf3, sdf4;
		SimpleDateFormat sdf5, sdf6, sdf7, sdf8, sdf9;
		
		sdf1 = new SimpleDateFormat("yyyy-MM-dd");
		sdf2 = new SimpleDateFormat("''yy년 MMM dd일 E요일");
		sdf3 = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss.SSS");
		sdf4 = new SimpleDateFormat("yyyy-MM-dd hh:mm:ss a");
		
		sdf5 = new SimpleDateFormat("오늘은 올 해의 D번째 날입니다.");
		sdf6 = new SimpleDateFormat("오늘은 이 달의 d번째 날입니다.");
		sdf7 = new SimpleDateFormat("오늘은 올 해의 w번째 주입니다.");
		sdf8 = new SimpleDateFormat("오늘은 이 달의 W번째 주입니다.");
		sdf9 = new SimpleDateFormat("오늘은 이 달의 F번째 E요일입니다.");
		
		System.out.println(sdf1.format(today));	// format(Date d)
		System.out.println(sdf2.format(today));
		System.out.println(sdf3.format(today));
		System.out.println(sdf4.format(today));
		System.out.println();
		System.out.println(sdf5.format(today));
		System.out.println(sdf6.format(today));
		System.out.println(sdf7.format(today));
		System.out.println(sdf8.format(today));
		System.out.println(sdf9.format(today));
	}
}
```

```
2022-10-24
'22년 10월 24일 월요일
2022-10-24 21:26:31.054
2022-10-24 09:26:31 오후

오늘은 올 해의 297번째 날입니다.
오늘은 이 달의 24번째 날입니다.
오늘은 올 해의 44번째 주입니다.
오늘은 이 달의 5번째 주입니다.
오늘은 이 달의 4번째 월요일입니다.
```

자주 사용될 만한 패턴을 만들어서 다양한 형식으로 예제가 실행된 날짜와 시간을 출력해보았다.

> 홑따옴표(')는 escape기호이기 때문에 패턴 내에서 홑따옴표를 표시하기 위해서는 홑따옴표를 연속적으로 두 번 사용해야 한다.

</br>

예제 10-13 / ch10 / DateFormatEx2.java

``` java
import java.text.*;
import java.util.*;

public class DateFormatEx2 {
	public static void main(String[] args) {
		Calendar cal = Calendar.getInstance();
		cal.set(2005, 9, 3);	// 2005년 10월 3일 - Month는 0~11의 범위를 갖는다.
		
		Date day = cal.getTime();	// Calendar를 Date로 변환
		
		SimpleDateFormat sdf1, sdf2, sdf3, sdf4;
		sdf1 = new SimpleDateFormat("yyyy-MM-dd");
		sdf2 = new SimpleDateFormat("yy-MM-dd E요일");
		sdf3 = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss.SSS");
		sdf4 = new SimpleDateFormat("yyyy-MM-dd hh:mm:ss a");
		
		System.out.println(sdf1.format(day));
		System.out.println(sdf2.format(day));
		System.out.println(sdf3.format(day));
		System.out.println(sdf4.format(day));
	}
}
```

```
2005-10-03
05-10-03 월요일
2005-10-03 21:31:41.667
2005-10-03 09:31:41 오후
```

`Date`인스턴스만 `format`메소드에 사용될 수 있기 때문에 `Calendar`인스턴스를 `Date`인스턴스로 변환하는 방법을 보여주는 예제이다.

> Date인스턴스를 Calendar인스턴스로 변환할 때는 Calendar클래스의 setTime()을 사용하면 된다.

</br>

예제 10-14 / ch10 / DateFormatEx3.java

``` java
import java.text.*;
import java.util.*;

public class DateFormatEx3 {
	public static void main(String[] args) {
		DateFormat df = new SimpleDateFormat("yyyy년 MM월 dd일");
		DateFormat df2 = new SimpleDateFormat("yyyy/MM/dd");
		
		try {
			Date d = df.parse("2019년 11월 23일");
			System.out.println(df2.format(d));
		} catch (Exception e) {}
	}	// main
}
```

```
2019/11/23
```

`parse(String source)`를 사용하여 날짜 데이터의 출력형식을 변환하는 방법을 보여주는 예제이다. `Integer`의 `parseInt()`가 문자열을 정수로 변환하는 것처럼 `SimpleDateFormat`의 `parse(String source)`는 문자열 `source`을 날짜 `Date`인스턴스로 변환해주기 때문에 매우 유용하게 쓰일 수 있다.

예를 들어 사용자로부터 날짜 데이터를 문자열로 입력받을 때, 입력받은 문자열을 날짜로 인식하기 위해서는 `substring`메소드를 이용해서 년, 월, 일을 뽑아내야 하는데 `parse(String source)`은 이러한 수고를 덜어준다.

> parse(String source)는 SimpleDateFormat의 조상인 DateFormat에 정의되어 있다.

> 지정된 형식과 입력된 형식이 일치하지 않는 경우에는 예외가 발생하므로 적절한 예외처리가 필요하다.

</br>

예제 10-15 / ch10 / DateFormatEx4.java

``` java
import java.util.*;
import java.text.*;

public class DateFormatEx4 {
	public static void main(String[] args) {
		String pattern = "yyyy/MM/dd";
		DateFormat df = new SimpleDateFormat(pattern);
		Scanner s = new Scanner(System.in);
		
		Date inDate = null;
		
		System.out.println("날짜를 " + pattern + "의 형태로 입력해주세요.(입력예:2015/12/31)");
		
		while(s.hasNextLine()) {
			try {
				inDate = df.parse(s.nextLine());
				break;
			} catch (Exception e) {
				System.out.println("날짜를 " + pattern + "의 형태로 다시 입력해주세요.(입력예:2015/12/31)");
			}
		}	// while
		
		Calendar cal = Calendar.getInstance();
		cal.setTime(inDate);
		Calendar today = Calendar.getInstance();
		long day = (cal.getTimeInMillis() - today.getTimeInMillis()) / (60 * 60 * 1000);
		System.out.println("입력하신 날짜는 현재와 " + day + "시간 차이가 있습니다.");
	}	// main
}
```

```
날짜를 yyyy/MM/dd의 형태로 입력해주세요.(입력예:2015/12/31)
asdfasdf
날짜를 yyyy/MM/dd의 형태로 다시 입력해주세요.(입력예:2015/12/31)
20221231
날짜를 yyyy/MM/dd의 형태로 다시 입력해주세요.(입력예:2015/12/31)
2022/12/31
입력하신 날짜는 현재와 1610시간 차이가 있습니다.
```

화면으로부터 날짜를 입력받아서 계산결과를 출력하는 예제이다. while과 try-catch문을 이용해서 사용자가 올바른 형식으로 날짜를 입력할 때까지 반복해서 입력받도록 하였다.

지정된 패턴으로 입력되지 않은 경우, `parse`메소드를 호출하는 부분에서 예외(ParseException)가 발생하기 때문에 while문을 벗어나지 못한다.

</br>

## 2.3 ChoiceFormat

`ChoiceFormat`은 특정 범위에 속하는 값을 문자열로 반환해준다. 연속적 또는 불연속적인 범위의 값들을 처리하는 데 있어서 if문이나 switch문은 적절하지 못한 경우가 많다.

이럴 때 `ChoiceFormat`을 잘 사용하면 복잡하게 처리될 수 밖에 없었던 코드를 간단하고 직관적으로 만들 수 있다.

</br>

예제 10-15 / ch10 / ChoiceFormatEx1.java

``` java
import java.text.*;

public class ChoiceFormatEx1 {
	public static void main(String[] args) {
		double[] limits = {60, 70, 80, 90};	// 낮은 값부터 큰 값의 순서대로 적어야한다.
		// limits, grades간의 순서와 개수를 맞추어야 한다.
		String[] grades = {"D", "C", "B", "A"};
		
		int[] scores = { 100, 95, 88, 70, 52, 60, 70 };
		
		ChoiceFormat form = new ChoiceFormat(limits, grades);
		
		for(int i = 0; i < scores.length; i++) {
			System.out.println(scores[i] + ":" + form.format(scores[i]));
		}
	}	// main
}
```

```
100:A
95:A
88:B
70:C
52:D
60:D
70:C
```

두 개의 배열이 사용되었는데 하나(limits)는 범위의 경계값을 저장하는데 사용하였고, 또 하나(grades)는 범위에 포함된 값을 치환할 문자열을 저장하는데 사용되었다.

경계값은 double형으로 반드시 모두 오름차순으로 정렬되어 있어야 하며, 치환 될 문자열의 개수는 경계값에 의해 정의된 범위의 개수와 일치해야한다. 그렇지 않으면 IllegalArgumentException이 발생한다.

예제에서는 4개의 경계값에 의해 '60~69', '70~79', '80~89', '90~'의 범위가 정의되었다.

</br>

예제 10-17 / ch10 / ChoiceFormatEx2.java

``` java
import java.text.*;

public class ChoiceFormatEx2 {
	public static void main(String[] args) {
		String pattern = "60#D|70#C|80<B|90#A";
		int[] scores = { 91, 90, 80, 88, 70, 52, 60 };
		
		ChoiceFormat form = new ChoiceFormat(pattern);
		
		for(int i = 0; i < scores.length; i++) {
			System.out.println(scores[i] + ":" + form.format(scores[i]));
		}
	}	// main
}
```

```
91:A
90:A
80:C
88:B
70:C
52:D
60:D
```

이전 예제를 패턴을 사용하도록 변경한 것이다. 이처럼 배열 대신 패턴을 사용해서 보다 간결하게 처리할 수 있다. 패턴은 구분자로 `#`와 `<` 두 가지를 제공하는데 `limit#value`의 형태로 사용한다. `#`는 경계값을 범위에 포함시키지만, `<`는 포함시키지 않는다. 위의 결과에서 90은 A지만, 80은 B가 아닌, C이다.

> 경계값을 포함하지 않는다고 해서 "61#D|71#C|81#B|91#A"와 같이 하는 것보다는 "60\<D\|70\<C\|80\<B\|90\<A"과 같이 하는 것이 낫다.

</br>

## 2.4 MessageFormat

`MessageFormat`은 데이터를 정해진 양식에 맞게 출력할 수 있도록 도와준다. 데이터가 들어갈 자리를 마련해 놓은 양식을 미리 작성하고 프로그램을 이용해서 다수의 데이터를 같은 양식으로 출력할 때 사용하면 좋다.

예를 들어 고객들에게 보낼 안내문을 출력할 때 같은 안내문 양식에 받는 사람의 이름과 같은 데이터만 달라지도록 출력할 때, 또는 하나의 데이터를 다양한 양식으로 출력할 때 사용한다. 그리고 `SimpleDateFormat`의 `parse`처럼 `MessageFormat`의 `parse`를 이용하면 지정된 양식에서 필요한 데이터만을 손쉽게 추출해 낼 수도 있다.

</br>

예제 10-18 / ch10 / MessageFormatEx1.java

``` java
import java.text.*;

public class MessageFormatEx1 {
	public static void main(String[] args) {
		String msg = "Name: {0} \nTel: {1} \nAge: {2} \nBirthday: {3}";
		
		Object[] arguments = {
				"이자바", "02-123-1234", "27", "07-09"
		};
		
		String result = MessageFormat.format(msg, arguments);
		System.out.println(result);
	}
}
```

```
Name: 이자바 
Tel: 02-123-1234 
Age: 27 
Birthday: 07-09
```

`MessageFormat`에 사용할 양식인 문자열 `msg`를 작성할 때 `{숫자}`로 표시된 부분이 데이터가 출력될 자리이다. 이 자리는 순차적일 필요는 없고 여러 번 반복해서 사용할 수도 있다. 여기에 사용되는 숫자는 배열처럼 인덱스가 0부터 시작하며 양식에 들어갈 데이터는 객체배열인 `arguments`에 지정되어 있음을 알 수 있다.

객체배열이기 때문에 String이외에도 다른 객체들이 지정될 수 있으며, 이 경우 보다 세부적인 옵션들이 사용될 수 있다.

</br>

예제 10-10 / ch10 / MessageFormatEx2.java

``` java
import java.text.*;

public class MessageFormatEx2 {
	public static void main(String[] args) {
		String tableName = "CUST_INFO";
		String msg = "INSERT INTO" + tableName + " VALUES (''{0}'',''{1}'',{2}'',{3}'');";
				
		Object[][] arguments = {
				{"이자바", "02-123-1234", "27", "07-09"},
				{"김프로", "032-333-1234", "33", "10-07"},
		};
		
		for(int i = 0; i < arguments.length; i++) {
			String result = MessageFormat.format(msg, arguments[i]);
			System.out.println(result);
		}
	}
}
```

```
INSERT INTOCUST_INFO VALUES ('이자바','02-123-1234',27',07-09');
INSERT INTOCUST_INFO VALUES ('김프로','032-333-1234',33',10-07');
```

이전 예제를 보다 발전시켜서 반복문으로 하나 이상의 데이터 집합을 출력하는 예제이다. 다수의 데이터를 Database에 저장하기 위한 Insert문으로 변환하는 경우 드엥 사용하면 좋다.

</br>

예제 10-20 / ch10 / MessageFormatEx3.java

``` java
import java.text.*;

public class MessageFormatEx3 {
	public static void main(String[] args) throws Exception {
		String[] data = {
				"INSERT INTO CUST_INFO VALUES ('이자바', '02-123-1234', 27, '07-09');",
				"INSERT INTO CUST_INFO VALUES ('김프로', '032-333-1234', 33, '10-07');"
		};
		
		String pattern = "INSERT INTO CUST_INFO VALUES ({0}, {1}, {2}, {3});";
		MessageFormat mf = new MessageFormat(pattern);
		
		for(int i = 0; i < data.length; i++) {
			Object[] objs = mf.parse(data[i]);
			for(int j = 0; j < objs.length; j++) {
				System.out.print(objs[j] + ",");
			}
			System.out.println();
		}
	}	// main
}
```

```
'이자바','02-123-1234',27,'07-09',
'김프로','032-333-1234',33,'10-07',
```

이전 예제에서는 데이터를 양식에 넣어서 출력했지만 이번에는 `parse(String source)`를 이용해서 출력된 데이터로부터 필요한 데이터만을 뽑아내는 방법을 보여준다.

</br>

예제 10-21 / ch10 / MessageFormatEx4.java

``` java
import java.util.*;
import java.text.*;
import java.io.*;

public class MessageFormatEx4 {
	public static void main(String[] args) throws Exception {
		String tableName = "CUST_INFO";
		String fileName = "data4.txt";
		String msg = "INSERT INTO " + tableName + " VALUES ({0}, {1}, {2}, {3});";
		
		Scanner s = new Scanner(new File(fileName));
		
		String pattern = "{0}, {1}, {2}, {3}";
		MessageFormat mf = new MessageFormat(pattern);
		
		while(s.hasNextLine()) {
			String line = s.nextLine();
			Object[] objs = mf.parse(line);
			System.out.println(MessageFormat.format(msg, objs));
		}
		
		s.close();	// 작업이 끝났으니 Scanner에서 사용한 파일을 닫아 준다.
	}	// main
}
```

```
INSERT INTO CUST_INFO VALUES ('이자바', '02-123-1234', 27, '07-09');
INSERT INTO CUST_INFO VALUES ('김프로', '032-333-1234', 33, '10-07');

c:\jdk1.8\work\ch10>type data4.txt
'이자바', '02-123-1234', 27, '07-09'
'김프로', '032-333-1234', 33, '10-07'
```

이전의 예제에서는 데이터를 객체배열에 직접 초기화하였는데, 이렇게 하면 데이터가 바뀔 때마다 매번 배열을 변경해야하고 그리고는 다시 컴파일을 해줘야하므로 불편하다.

이러한 불편함을 없애기 위해 이번에 `Scanner`를 통해 파일로부터 데이터를 라인별로 읽어서 처리하도록 변경했다. 이렇게 파일로부터 데이터를 제공받으면 데이터가 변경되어도 다시 컴파일을 하지 않아도 된다.

> 실행 시에 입력받을 데이터가 저장된 파일명도 지정하도록 예제를 변경하면, 파일의 이름이 바뀌어도 다시 컴파일 하지 않아도 된다.