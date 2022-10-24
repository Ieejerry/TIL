Chapter 10. 날짜와 시간 & 형식화 date, time and formatting

# 1. 날짜와 시간

</br>

## 1.1 Calendar와 Date

`Date`는 날짜와 시간을 다룰 목적으로 JDK1.0부터 제공되어온 클래스이다. `Date`클래스는 기능이 부족했기 때문에, 서둘러 `Calendar`라는 새로운 클래스를 그 다음 버전인 JDK1.1부터 제공하기 시작했다. `Calendar`는 `Date`보다는 훨씬 나았지만 몇 가지 단점들이 발견되었다. 그래서 JDK1.8부터 `java.time패키지`로 기존의 단점들을 개선한 새로운 클래스들이 추가되었다.

</br>

### Calendar와 GregorianCalendar

`Calendar`는 추상클래스이기 때문에 직접 객체를 생성할 수 없고, 메소드를 통해서 완전히 구현된 클래스의 인스턴스를 얻어야 한다.

``` java
Calendar cal = new Calendar();  // 에러. 추상클래스는 인스턴스를 생성할 수 없다.

// OK. getInstance()메소드는 Calendar클래스를 구현한 클래스의 인스턴스를 반환한다.
Calendar cal = Calendar.getInstance();
```

`Calendar`를 상속받아 완전히 구현한 클래스로는 `GregorianCalendar`와 `BuddhistCalendar`가 있는데 `getInstance()`는 시스템의 국가와 지역설정을 확인해서 태국인 경우에는 `BuddhistCalendar`의 인스턴스를 반환하고, 그 외에는 `GregorianCalendar`의 인스턴스를 반환한다.

`GregorianCalendar`는 `Calendar`를 상속받아 오늘날 전세계 공통으로 사용하고 있는 그레고리력에 맞게 구현한 것으로 태국을 제외한 나머지 국가에서는 `GregorianCalendar`를 사용하면 된다.

인스턴스를 직접 생성해서 사용하지 않고 이처럼 메소드를 통해서 인스턴스를 반환받게 하는 이유는 최소한의 변경으로 프로그램이 동작할 수 있도록 하기 위한 것이다.

``` java
class MyApplication {
    public static void main(String[] args) {
        Calendar cal = new GregorianCalendar(); // 경우에 따라 이 부분을 변경해야한다.
            ...
    }
}
```

만일 위와 같이 특정 인스턴스를 생성하도록 프로그램이 작성되어 있다면, 다른 종류의 역법(calendar)을 사용하는 국가에서 실행한다던가, 새로운 역볍이 추가된다던가 하는 경우, 즉 다른 종류의 인스턴스를 필요로 하는 경우에 `MyApplicaiton`을 변경해야 하는데 비해 아래와 같이 메소드를 통해 인스턴스를 얻어오도록 하면 `MyApplication`을 변경하지 않아도 된다.

``` java
class MyApplicaiton {
    public static void main(String[] args) {
        Calendar cal = Calendar.getInstance();
            ...
    }
}
```

대신 `getInstance()`의 내용은 달라져야 하겠지만, `MyApplication`이 변경되지 않아도 된다는 것이 중요하다. `getInstance()`메소드가 static인 이유는 메소드내의 코드에서 인스턴스 변수를 사용하거나 인스턴스 메소드를 호출하지 않기 때문이다. 또 다른 이유는 `getInstance()`가 static이 아니라면 위와 같이 객체를 생성한 다음에 호출해야 하는데 `Calendar`는 추상클래스이기 때문에 객체를 생성할 수 없기 때문이다.

</br>

### Date와 Calendar간의 변환

`Calendar`가 새로 추가되면서 `Date`는 대부분의 메소드가 'deprecated'되었으므로 잘 사용되지 않는다. 그럼에도 불구하고 여전히 `Date`를 필요로 하는 메소드들이 있기 때문에 `Calendar`를 `Date`로 또는 그 반대로 변환할 일이 생긴다.

> java API문서를 보면 더 이상 사용을 권장하지 않는 대상에 'deprecated'가 붙어있다.

![image](https://ifh.cc/g/BQToF1.png)

예제 10-1 / ch10 / CalendarEx1.java

``` java
import java.util.*;

public class CalendarEx1 {
	public static void main(String[] args) {	// 기본적으로 현재날짜와 시간으로 설정된다.
		Calendar today = Calendar.getInstance();
		System.out.println("이 해의 년도 : " + today.get(Calendar.YEAR));
		System.out.println("월(0~11, 0:1월) : " + today.get(Calendar.MONTH));
		System.out.println("이 해의 몇 째 주 : " + today.get(Calendar.WEEK_OF_YEAR));
		System.out.println("이 달의 몇 째 주 : " + today.get(Calendar.WEEK_OF_MONTH));
		// DATE와 DAY_OF_MONTH는 같다.
		System.out.println("이 달의 몇 일 : " + today.get(Calendar.DATE));
		System.out.println("이 달의 몇 일 : " + today.get(Calendar.DAY_OF_MONTH));
		System.out.println("이 해의 몇 일 : " + today.get(Calendar.DAY_OF_YEAR));
		System.out.println("요일(1~7, 1:일요일) : " + today.get(Calendar.DAY_OF_WEEK));	// 1:일요일, 2.월요일, ..., 7:토요일
		System.out.println("이 달의 몇 째 요일 : " + today.get(Calendar.DAY_OF_WEEK_IN_MONTH));
		System.out.println("오전_오후(0:오전, 1:오후) : " + today.get(Calendar.AM_PM));
		System.out.println("시간(0~11) : " + today.get(Calendar.HOUR));
		System.out.println("시간(0~23) : " + today.get(Calendar.HOUR_OF_DAY));
		System.out.println("분(0~59) : " + today.get(Calendar.MINUTE));
		System.out.println("초(0~59) : " + today.get(Calendar.SECOND));				
		System.out.println("100분의 1초(0~999) : " + today.get(Calendar.MILLISECOND));
		// 천분의 1초를 시간으로 표시하기 위해 3600000으로 나누었다.(1시간 = 60 * 60초)
		System.out.println("TimeZone(-12~+12) : " + (today.get(Calendar.ZONE_OFFSET)/(60*60*1000)));
		System.out.println("이 달의 마지막 날 : " + today.getActualMaximum(Calendar.DATE));	// 이 달의 마지막 일을 찾는다.
	}
}
```

```
이 해의 년도 : 2022
월(0~11, 0:1월) : 9
이 해의 몇 째 주 : 44
이 달의 몇 째 주 : 5
이 달의 몇 일 : 23
이 달의 몇 일 : 23
이 해의 몇 일 : 296
요일(1~7, 1:일요일) : 1
이 달의 몇 째 요일 : 4
오전_오후(0:오전, 1:오후) : 1
시간(0~11) : 5
시간(0~23) : 17
분(0~59) : 38
초(0~59) : 25
100분의 1초(0~999) : 954
TimeZone(-12~+12) : 9
이 달의 마지막 날 : 31
```

`getInstance()`를 통해서 얻은 인스턴스는 기본적으로 현재 시스템의 날짜와 시간에 대한 정보를 담고 있다. 원하는 날짜나 시간으로 설정하려면 `set`메소드를 사용하면 된다.

여기서는 `int get(int field)`를 이용해서 원하는 필드의 값을 얻어오는 방법을 보여주기 위한 것이다.

``` java
public final static int YEAR = 1;
```

`get`메소드의 매개변수로 사용되는 int값들은 `Calendar`에 정의된 static상수이다.

``` java
System.out.println("월(0~111, 0:1월): " + today.get(Calendar.MONTH));
```

한 가지 주의해야할 것은 `get(Calendar.MONTH)`로 얻어오는 값의 범위가 1~12가 아닌 0~11이라는 것이다. 그래서 `get(Calendar.MONTH)`로 얻어오는 값이 0이면 1월을 의미하고, 11이면 12월을 의미한다.

예제 10-2 / ch10 / CalendarEx2.java

``` java
import java.util.Calendar;

public class CalendarEx2 {
	public static void main(String[] args) {
		// 요일은 1부터 시작하기 때문에, DAY_OF_WEEK[0]은 비워두었다.
		final String[] DAY_OF_WEEK = {"", "일", "월", "화", "수", "목", "금", "토"};
		
		Calendar date1 = Calendar.getInstance();
		Calendar date2 = Calendar.getInstance();
		
		// month인 경우 0부터 시작하기 때문에 4월인 경우, 3로 지정해야한다.
		// date1.set(2019, Calendar.APRIL, 29);와 같이 할 수도 있다.
		date1.set(2019, 3, 29);	// 2019년 4월 29일로 날짜를 설정한다.
		System.out.println("date1은 " + toString(date1) + DAY_OF_WEEK[date1.get(Calendar.DAY_OF_WEEK)] + "요일이고,");
		System.out.println("오늘(date2)은 " + toString(date2) + DAY_OF_WEEK[date2.get(Calendar.DAY_OF_WEEK)] + "요일입니다.");
		
		// 두 날짜간의 차이를 얻으려면, getTimeInMillis() 천분의 일초 단위로 변환해야 한다.
		long difference = (date2.getTimeInMillis() - date1.getTimeInMillis()) / 1000;
		System.out.println("그 날(date1)부터 지금까지(date2)까지 " + difference + "초가 지났습니다.");
		System.out.println("일(day)로 계산하면 " + difference / (24 * 60 * 60) + "일입니다.");	// 1일 = 24 * 60 * 60
	}
	
	public static String toString(Calendar date) {
		return date.get(Calendar.YEAR) + "년 " + (date.get(Calendar.MONTH) + 1) + "월 " + date.get(Calendar.DATE) + "일 ";
	}
}
```

```
date1은 2019년 4월 29일 월요일이고,
오늘(date2)은 2022년 10월 23일 일요일입니다.
그 날(date1)부터 지금까지(date2)까지 109987200초가 지났습니다.
일(day)로 계산하면 1273일입니다.
```

두 날짜간의 차이를 구하는 예제이다. 날짜와 시간을 원하는 값으로 변경하려면 `set`메소드를 사용하면 된다.

``` java
void set(int field, int value)
void set(int year, int month, int date)
void set(int year, int month, int date, int hourOfDay, int minute)
void set(int year, int month, int date, int hourOfDay, int minute, int second)
```

> clear()는 모든 필드의 값을, clear(int field)는 지정된 필드의 값을 기본값으로 초기화 한다. 각 필드의 기본값은 Java API문서에서 GregorianCalendar를 참고하면 된다.

두 날짜간의 차이를 구하기 위해서는 두 날짜를 최소단위인 초단위로 변경한 다음 그 차이를 구하면 된다. `getTimeInMillis()`는 1/1000초 단위로 값을 반환하기 때문에 초단위로 얻기 위해서는 1000으로 나눠 주어야 하고, 일단위로 얻기 위해서는 '24(시간) * 60(분) * 60(초) * 1000'으로 나누어야 한다.

예제에서는 변수 `difference`에 저장할 때 이미 초단위로 변경하였기 때문에 일단위로 변경할 때 '24(시간) * 60(분) * 60(초)'로만 나누었다.

시간상의 전후를 알고 싶을 때는 두 날짜간의 차이가 양수인지 음수인지를 판단하면 된다. 아니면, 간단히 `boolean after(Object when)`와 `boolean before(Object when)`를 사용해도 된다.

예제 10-3 / ch10 / CalendarEx3.java

``` java
import java.util.Calendar;

public class CalendarEx3 {
	public static void main(String[] args) {
		final int[] TIME_UNIT = {3600, 60, 1};	// 큰 단위를 앞에 놓는다.
		final String[] tIME_UNIT_NAME = {"시간", "분", "초"};
		
		Calendar time1 = Calendar.getInstance();
		Calendar time2 = Calendar.getInstance();
		
		time1.set(Calendar.HOUR_OF_DAY, 10);	// time1을 10시 20분 30초로 설정
		time1.set(Calendar.MINUTE, 20);
		time1.set(Calendar.SECOND, 30);
		
		time2.set(Calendar.HOUR_OF_DAY, 20);	// time2을 20시 30분 10초로 설정
		time2.set(Calendar.MINUTE, 30);
		time2.set(Calendar.SECOND, 10);
		
		System.out.println("time1 : " + time1.get(Calendar.HOUR_OF_DAY) + "시 " + time1.get(Calendar.MINUTE) + "분 " + time1.get(Calendar.SECOND) + "초");
		System.out.println("time2 : " + time2.get(Calendar.HOUR_OF_DAY) + "시 " + time2.get(Calendar.MINUTE) + "분 " + time2.get(Calendar.SECOND) + "초");
		
		long difference = Math.abs(time2.getTimeInMillis() - time1.getTimeInMillis()) / 1000;
		System.out.println("time1과 time2의 차이는 : " + difference + "초 입니다.");
		
		String tmp = "";
		for(int i = 0; i < TIME_UNIT.length; i++) {
			tmp += difference / TIME_UNIT[i] + tIME_UNIT_NAME[i];
			difference %= TIME_UNIT[i];
		}
		System.out.println("시분초로 변환하면 " + tmp + "입니다.");
	}
}
```

```
time1 : 10시 20분 30초
time2 : 20시 30분 10초
time1과 time2의 차이는 : 36580초 입니다.
시분초로 변환하면 10시간9분40초입니다.
```

두 개의 시간 데이터로부터 초 단위로 차이를 구한 다음, 시분초로 바꿔 출력하는 예제이다. 가장 큰 단위인 시간 단위(3600초)로 나누고 남은 나머지를 다시 분 단위(60초)로 나누면 그 나머지는 초 단위의 값이 된다.

``` java
for(int i = 0; i < TIME_UNIT.length; i++) {
    tmp += difference / TIME_UNIT[i] + tIME_UNIT_NAME[i];
    // difference = difference % TIME_UNIT[i];
    difference %= TIME_UNIT[i];
}
```

예제 10-4 / ch10 / CalendarEx4.java

``` java
import java.util.Calendar;

public class CalendarEx4 {
	public static void main(String[] args) {
		Calendar date = Calendar.getInstance();
		date.set(2019, 7, 31);	// 2019년 8월 31일
		
//		System.out.println(date);
		System.out.println(toString(date));
		System.out.println("= 1일 후 =");
		date.add(Calendar.DATE, 1);
		System.out.println(toString(date));
		
		System.out.println("= 6달 전 =");
		date.add(Calendar.MONTH, -6);
		System.out.println(toString(date));
		
		// add()와 달리 roll()은 다른 필드에 영향을 주지 않는다.
		System.out.println("= 31일 후(roll) =");
		date.roll(Calendar.DATE, 31);
		System.out.println(toString(date));
		
		System.out.println("= 31일 후(add) =");
		date.add(Calendar.DATE, 31);
		System.out.println(toString(date));
	}
	
	public static String toString(Calendar date) {
		return date.get(Calendar.YEAR) + "년 " + (date.get(Calendar.MONTH) + 1) + "월 " + date.get(Calendar.DATE) + "일";
	}
}
```

```
2019년 8월 31일
= 1일 후 =
2019년 9월 1일
= 6달 전 =
2019년 3월 1일
= 31일 후(roll) =
2019년 3월 1일
= 31일 후(add) =
2019년 4월 1일
```

`add(int field, int amount)`를 사용하면 지정한 필드의 값을 원하는 만틈 증가 또는 감소시킬 수 있기 때문에 `add`메소드를 이용하면 특정 날짜 또는 시간을 기점으로 해서 일정기간 전후의 날짜와 시간을 알아낼 수 있다.

`roll(int field, int amount)`도 지정한 필드의 값을 증가 또는 감소시킬 수 있는데, `add`메소드와의 차이점은 다른 필드에 영향을 미치지 않는다는 것이다. 예를 들어 `add`메소드로 날짜필드(Calendar.DATE)의 값을 31만큼 증가시켰다면 다음 달로 넘어가므로 월 필드(Calendar.MONTH)의 값도 1 증가하지만, `roll`메소드는 같은 경우에 월 필드의 값은 변하지 않고 일 필드의 값만 바뀐다.

단, 한 가지 예외가 있는데 일 필드(Calendar.DATE)가 만일(end of month)일 때, `roll`메소드를 이용해서 월 필드(Calendar.MONTH)를 변경하면 일 필드(Calendar.DATE)에 영향을 미칠 수 있다.

예제 10-5 / ch10 / CalendarEx5.java

``` java
import java.util.Calendar;

public class CalendarEx5 {
	public static void main(String[] args) {
		Calendar date = Calendar.getInstance();
		
		date.set(2015, 0, 31);	// 2015년 1월 31일
		System.out.println(toString(date));
		date.roll(Calendar.MONTH, 1);
		System.out.println(toString(date));
	}
	
	public static String toString(Calendar date) {
		return date.get(Calendar.YEAR) + "년 " + (date.get(Calendar.MONTH) + 1) + "월 " + date.get(Calendar.DATE) + "일";
	}
}
```

```
2015년 1월 31일
2015년 2월 28일
```

2015년 1월 31일에 대해 `roll()`을 호출해서 월 필드를 1 증가시켰을 때, 우러 필드는 2월이 되는데 2월에는 31일이 없기 때문에 2월의 말일인 28일로 자동 변경되었다. `add()`도 같은 경우에 마찬가지로 자동 변경된다.

예제 10-6 / ch10 / CalendarEx6.java

``` java
import java.util.Calendar;

public class CalendarEx6 {
	public static void main(String[] args) {
		if(args.length != 2) {
			System.out.println("Usage : java CalendarEx6 2022 10");
			return;
		}
		int year = Integer.parseInt(args[0]);
		int month = Integer.parseInt(args[1]);
		int START_DAY_OF_WEEK = 0;	// 1일의 요일
		int END_DAY = 0;	// 마지막날의 요일
		
		Calendar sDay = Calendar.getInstance();	// 시작일
		Calendar eDay = Calendar.getInstance();	// 끝일
		
		// 월의 경우 0부터 11까지의 값을 가지므로 1을 빼주어야 한다.
		// 예를 들어, 2019년 11월 1일은 sDay.set(2019, 10, 1);과 같이 해주어야 한다.
		sDay.set(year, month-1, 1);	// month는 0부터 시작
		eDay.set(year, month, 1);
		
		// 다음달의 첫날(12월 1일)에서 하루를 빼면 현재달의 마지막 날(11월 30일)이 
		eDay.add(Calendar.DATE, -1);
		
		// 첫 번째 요일이 무슨 요일인지 알아낸다.
		START_DAY_OF_WEEK = sDay.get(Calendar.DAY_OF_WEEK);
		
		// eDay에 지정된 날짜를 얻어온다.
		END_DAY = eDay.get(Calendar.DATE);
		
		System.out.println("      " + year + "년 " + month + "월");
		System.out.println(" SU MO TU WE TH FR SA");
		
		// 해당 월의 1일이 어느 요일인지를 따라서 공백을 출력한다.
		// 만일 1일이 수요일이라면 공백을 세 번 찍는다.(일요일부터 시작)
		for(int i = 1; i < START_DAY_OF_WEEK; i++) {
			System.out.print("   ");
		}
		
		for(int i = 1, n = START_DAY_OF_WEEK; i <= END_DAY; i++, n++) {
			System.out.print((i < 10) ? "  " + i : " " + i);
			if(n % 7 == 0) System.out.println();
		}
	}
}
```

```
      2022년 10월
 SU MO TU WE TH FR SA
                    1
  2  3  4  5  6  7  8
  9 10 11 12 13 14 15
 16 17 18 19 20 21 22
 23 24 25 26 27 28 29
 30 31
```

커맨드라인으로 년과 월을 입력하면 달력을 출력하는 예제이다. 다음 달의 1일에서 하루를 빼면 이번 달의 마지막 일을 알 수 있다.

> getActualMaximum(Calendar.DATE)를 사용해도 해당 월의 마지막 날을 알 수 있다.

예제 10-7 / ch10 / CalendarEx7.java

``` java
import java.util.Calendar;

public class CalendarEx7 {
	public static void main(String[] args) {
		if(args.length != 2) {
			System.out.println("Usage : java CalendarEx7 2022 10");
			return;
		}
		
		int year = Integer.parseInt(args[0]);
		int month = Integer.parseInt(args[1]);
		
		Calendar sDay = Calendar.getInstance();	// 시작일
		Calendar eDay = Calendar.getInstance();	// 끝일
		
		// 월의 경우 0부터 11까지의 값을 가지므로 1을 빼주어야 한다.
		// 예를 들어, 2019년 11월 1일은 sDay.set(2019, 10, 1);과 같이 해주어야 한다.
		sDay.set(year, month-1, 1);	// 입력월의 1일로 설정한다.
		// 입력월의 말일로 설정한다.
		eDay.set(year, month-1, sDay.getActualMaximum(Calendar.DATE));
		// 1일이 속한 주의 일요일로 날짜설정
		sDay.add(Calendar.DATE,	-sDay.get(Calendar.DAY_OF_WEEK) + 1);
		// 말일이 속한 주의 토요일로 날짜설정
		eDay.add(Calendar.DATE, 7 - eDay.get(Calendar.DAY_OF_WEEK));
		
		System.out.println("      " + year + "년 " + month + "월");
		System.out.println(" SU MO TU WE TH FR SA");
		
		// 시작 일로부터 마지막 일까지(sDay <= eDay) 1일씩 증가시키면서 일(Calendar.DATE)을 출력
		for(int n=1; sDay.before(eDay) || sDay.equals(eDay); sDay.add(Calendar.DATE, 1)) {
			int day = sDay.get(Calendar.DATE);
			System.out.print((day < 10) ? "  " + day : " " + day);
			if(n++%7==0) System.out.println();	// 7일치를 찍고 나서 줄을 바꾼다.
		}
	}	// main
}
```

```
      2022년 10월
 SU MO TU WE TH FR SA
 25 26 27 28 29 30  1
  2  3  4  5  6  7  8
  9 10 11 12 13 14 15
 16 17 18 19 20 21 22
 23 24 25 26 27 28 29
 30 31  1  2  3  4  5
```

이전 예제를 첫 주와 마지막 주가 이전 달, 이후 달과 연결되도록 변경하였다.

예제 10-8 / ch10 / CalendarEx8.java

``` java
public class CalendarEx8 {
	public static void main(String[] args) {
		String date1 = "201508";
		String date2 = "201405";
		
		// 년과 월을 substring으로 잘라서 정수로 변환한다.
		// 년에 12를 곱해서 월로 변환한 다음에 뺄셈을 하면 개월차를 구할 수 있다.
		int month1 = Integer.parseInt(date1.substring(0, 4)) * 12 + Integer.parseInt(date1.substring(4));
		int month2 = Integer.parseInt(date2.substring(0, 4)) * 12 + Integer.parseInt(date2.substring(4));
		
		System.out.println(date1 + "과 " + date2 + "의 차이는 " + Math.abs(month1 - month2) + "개월 입니다.");
	}
}
```

```
201508과 201405의 차이는 15개월 입니다.
```

년과 월 정도의 계산이라면, 굳이 `Calendar`를 사용하지 않고 이처럼 간단히 처리해도 좋다.

예제 10-9 / ch10 / CalendarEx9.java

``` java
public class CalendarEx9 {
	public static void main(String[] args) {
		System.out.println("2014. 5. 31 : " + getDayOfWeek(2014, 5, 31));
		System.out.println("2012. 6. 1 : " + getDayOfWeek(2012, 6, 1));
		System.out.println("2014. 5. 1 - 2014.4.28 : " + dayDiff(2014, 5, 1, 2014, 4, 28));
		System.out.println("2015. 6. 29 : " + convertDateToDay(2015, 6, 29));
		System.out.println("735778 : " + convertDayToDate(735778));
	}
	
	public static int[] endOfMonth = {31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};	// 각 달의 마지막 일
	
	public static boolean isLeapYear(int year) {
		return ((year % 4 == 0) && (year % 100 != 0) || (year % 400 == 0));
	}
	
	public static int dayDiff(int y1, int m1, int d1, int y2, int m2, int d2) {
		return convertDateToDay(y1, m1, d1) - convertDateToDay(y2, m2, d2);
	}
	
	public static int getDayOfWeek(int year, int month, int day) {
		// 1~7의 값을 반환한다. 결과가 1이면 일요일이다.
		return convertDateToDay(year, month, day)%7 + 1;
	}
	
	public static String convertDayToDate(int day) {
		int year = 1;
		int month = 0;
		
		while(true) {
			int aYear = isLeapYear(year)? 366 : 365;
			if(day > aYear) {
				day -= aYear;
				year++;
			} else {
				break;
			}
		}
		
		while(true) {
			int endDay = endOfMonth[month];
			// 윤년이고 윤달이 포함되어 있으면, 1일을 더한다.
			if(isLeapYear(year) && month == 1) endDay++;
			
			if(day > endDay) {
				day -= endDay;
				month++;
			} else {
				break;
			}
		}
		return year + "-" + (month+1) + "-" + day;
	}
	
	public static int convertDateToDay(int year, int month, int day) {
		int numOfLeapYear = 0;	// 윤년의 수
		
		// 전년도까지의 윤년의 수를 구한다.
		for(int i = 1; i < year; i++) {
			if(isLeapYear(i))
				numOfLeapYear++;
		}
		
		// 전년도까지의 일수를 구한다.
		int toLastYearDaySum = (year - 1) * 365 + numOfLeapYear;
		
		// 올해의 현재 월까지의 일수 계산
		int thisYearDaySum = 0;
		
		for(int i = 0; i < month - 1; i++) {
			thisYearDaySum += endOfMonth[i];
		}
		
		// 윤년이고, 2월이 포함되어 있으면 1일을 증가시킨다.
		if(month > 2 && isLeapYear(year)) {
			thisYearDaySum++;
		}
		thisYearDaySum += day;
		
		return toLastYearDaySum + thisYearDaySum;
	}
}
```

```
2014. 5. 31 : 7
2012. 6. 1 : 6
2014. 5. 1 - 2014.4.28 : 3
2015. 6. 29 : 735778
735778 : 2015-6-29
```

이 예제는 날짜계산을 위한 몇 가지 메소드를 직접 구현해 보았다. 여기서 작성한 메소드의 기능을 요약하면 다음과 같다.

![image](https://ifh.cc/g/X4ZG1w.png)

날짜를 일단위로, 일단위의 값을 날짜로 바꾸는 것을 제외하고는 간단하다. 두 날짜의 차이를 구하려면, 일단위로 변환한 다음 두 값을 서로 빼기만 하면 된다.

요일을 구하는 것은 일단위로 바꾼 다음에 요일의 개수인 7로 나누고, 요일이 1부터 시작하기 위해서 1을 더했다. 1을 더하지 않고 요일의 범위를 0~6으로 해도 되지만, `Calendar`에서의 요일범위가 1~7이기 때문에 동일하게 처리했다.

> 일 단위로 변환할 때 서기 1년 1월 1일부터의 일(日)의 수를 계산하였지만, Calendar의 경우 1970년 1월 1일 기준으로 계산한다. 그래서 1970년 1월 1일 이전의 날짜에 대해 getTimeInMillis()를 호출하면 음수를 결과로 얻는다.