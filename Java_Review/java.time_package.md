Chapter 10. 날짜와 시간 & 형식화 date, time and formatting

# 3. java.time패키지

Java의 탄생붜 지금까지 날짜와 시간을 다루는데 사용해왔던, `Date`와 `Calendar`가 가지고 있던 단점들을 해소하기 위해 드디어 JDK1.8부터 `java.time`패키지가 추가되었다. 이 패키지는 다음과 같이 4개의 하위 패키지를 가지고 있다.

![image](https://ifh.cc/g/MLBMrh.png)

위의 패키지들에 속한 클래스들의 가장 큰 특징은 `String`클래스처럼 '불변(immutable)'이라는 것이다. 그래서 날짜나 시간을 변경하는 메소드들은 기존의 객체를 변경하는 대신 항상 변경된 새로운 객체를 반환한다. 기존 `Calendar`클래스는 변경 가능하므로, 멀티 쓰레드 환경에서 안전하지 못한다.

멀티 쓰레드 환경에서는 동시에 여러 쓰레드가 같은 객체에 접근할 수 있기 때문에. 변경 가능한 객체는 데이터가 잘못될 가능성이 있으며, 이를 쓰레드에 안전(thread-safe)하지 않다고 한다.

</br>

## 3.1 java.time패키지의 핵심 클래스

날짜와 시간을 하나로 표현하는 `Calendar`와 달리, `java.time`패키지에서는 날짜와 시간을 별도의 클래스로 분리해 놓았다. 시간을 표현할 때는 `LocalTime`클래스를 사용하고, 날짜를 표현할 때는 `LocalDate`클래스를 사용한다. 그리고 날짜와 시간이 모두 필요할 때는 `LocalDateTime`클래스를 사용하면 된다.

![image](https://ifh.cc/g/6fvCwO.png)

여기에 시간대(time-zone)까지 다뤄야 한다면, `ZonedDateTime`클래스를 사용하면 된다.

![image](https://ifh.cc/g/QM5590.png)

`Calendar`는 `ZonedDateTime`처럼, 날짜와 시간 그리고 시간대까지 모두 가지고 있다. `Date`와 유사한 클래스로는 `Instant`가 있는데, 이 클래스는 날짜와 시간을 초 단위(정확히는 나노초)로 표현한다. 날짜와 시간을 초단위로 표현한 값을 타입스탬프(time-stamp)라고 부르는데, 이 값은 날짜와 시간을 하나의 정수로 표현할 수 있으므로 날짜와 시간의 차이를 계산하거나 순서를 비교하는데 유리해서 데이터베이스에 많이 사용된다.

이외에도 날짜를 더 세부적으로 다룰 수 있는 `Year`, `YearMonth`, `MonthDay`와 같은 클래스도 있다.

</br>

### Period와 Duration

날짜와 시간의 간격을 표현하기 위한 클래스도 있는데, `Period`는 두 날짜간의 차이를 표현하기 위한 것이고, `Duration`은 시간의 차이를 표현하기 위한 것이다.

![image](https://ifh.cc/g/POj4y0.png)

</br>

### 객체 생성하기 - now(), of()

`java.time`패키지에 속한 클래스의 객체를 생성하는 가장 기본적인 방법은 `now()`와 `of()`를 사용하는 것이고, `now()`는 현재 날짜와 시간을 저장하는 객체를 생성한다.

``` java
LocalDate date = LocalDate.now();   // 2022-10-27
LocalTime time = LocalTIme.now();   // 19:25:01.875
LocalDateTime dateTime = LocalDateTime.now();   // 2022-10-27T19:25:01.875
ZonedDateTime dateTimeInKr = ZonedDateTime.now();   // 2022-10-27T19:25:01.875+09:00[Asia/Seoul]
```

</br>

### Temporal과 TemporalAmount

`LocalDate`, `LocalTime`, `LocalDateTime`, `ZonedDateTime`등 날짜와 시간을 표현하기 위한 클래스들은 모두 `Temporal`, `TemporalAccessor`, `TemporalAdjuster`인터페이스를 구현했고, `Duration`과 `Period`는 `TemporalAmount`인터페이스를 구현하였다. 매개변수의 타입이 Temporal로 시작하는 것들이 자주 등장하는데 대부분 날짜와 시간을 위한 것이므로, `TemporalAmount`인지 아닌지만 확인하면 된다.

> 'temporal'과 'chrono'의 의미가 모두 시간(time)인데도, 'time'대신 굳이 이런 어려운 용어를 쓴 이유는 시간(시분초)과 더 큰 개념의 시간(년월일시분초)을 구분하기 위해서이다.

![image](https://ifh.cc/g/G6Ah9T.png)

</br>

### TemporalUnit과 TemporalField

날짜와 시간의 단위를 정의해 놓은 것이 `TemporalUnit`인터페이스이고, 이 인터페이스를 구현한 것이 열거형 `ChronoUnit`이다. 그리고 `TemporalField`는 년, 월, 일 등 날짜와 시간의 필드를 정의해 놓은 것으로, 열거형 `ChronoField`가 이 인터페이스를 구현하였다.

> 열거형(enumeration)은 서로 관련된 상수를 묶어서 정의해 놓은 것이다.

``` java
    LocalTime now = LocalTime.now();    // 현재 시간
    int minute = new.getMinute();   // 현재 시간에서 분(minute)만 뽑아낸다.
//  int minute = now.get(ChronoField.MINUTE_OF_HOUR);   // 위의 문장과 동일
```

날짜와 시간에서 특정 필드의 값만을 얻을 때는 `get()`이나 get으로 시작하는 이름의 메소드를 이용한다. 그리고 아래와 같이 특정 날짜와 시간에서 지정된 단위의 값을 더하거나 뺄 때는 `plus()` 또는 `minus()`에 값과 함께 열거형 `ChronoUnit`을 사용한다.

``` java
LocalDate today = LocalDate.now();  // 오늘
LocalDate tomorrow = today.plus(1, ChronoUnit.DAYS);    // 오늘에 1일을 더한다.
LocalDate tomorrow = today.plusDays(1); // 위의 문장과 동일
```

참고로 `get()`과 `plus()`의 정의는 아래와 같다.

``` java
int get(TemporalField field)
LocalDate plus(long amountToAdd, TemporalUnit unit)
```

특정 `TemporalField`나 `TemporalUnit`을 사용할 수 있는지 확인하는 메소드는 다음과 같다. 이 메소드들은 날짜와 시간을 표현하는 데 사용하는 모든 클래스에 포함되어 있다.

``` java
boolean isSupported(TemporalUnit unit)  // Temporal에 정의
boolean isSupported(TemporalField field)    // TemporalAccessor에 정의
```

</br>

## 3.2 LocalDate와 LocalTime

`LocalDate`와 `LocalTime`은 `java.time`패키지의 가장 기본이 되는 클래스이다.

객체를 생성하는 방법은 현재의 날짜와 시간을 `LocalDate`와 `LocalTime`으로 각각 반환하는 `now()`와 지정된 날짜와 시간으로 `LocalDate`와 `LocalTime`객체를 생성하는 `of()`가 있다. 둘 다 static메소드이다.

``` java
LocalDate today = LocalDate.now();  // 오늘의 날짜
LocalTime now = LocalTime.now();    // 현재 시간

LocalDate birthDate = LocalDate.of(1996, 03, 07);   // 1996년 03월 07일
LocalTime birthTime = LocalTime.of(16, 30, 30);     // 16시 30분 30초
```

`of()`는 다음과 같이 여러 가지 버전이 제공된다.

``` java
static LocalDate of(int year, Month month, int dayOfMonth)
static LocalDate of(int year, int month, int dayOfMonth)

static LocalTime of(int hour, int min)
static LocalTime of(int hour, int min, int sec)
static LocalTime of(int hour, int min, int sec, int nanoOfSecond)
```

참고로 다음과 같이 일 단위나 초 단위로도 지정할 수 있다. 아래의 첫 번째 문장은 1999년의 365번째 날, 즉 마지막 날을 의미하며, 두 번째 문장은 그 날의 0시 0분 0초부터 86399초(하루는 86400초)가 지난 시간, 즉 23시 59분 59초를 의미한다.

``` java
LocalDate birthDate = LocalDate.ofYearDay(1999, 365);   // 1999년 12월 31일
LocalTime birthTime = LocalTime.ofSecondDay(86399);     // 23시 59분 59초
```

또는 `parse()`를 이용하면 문자열을 날짜와 시간으로 변환할 수도 있다.

``` java
LocalDate birthDate = LocalDate.parse("199912-31");   // 1999년 12월 31일
LocalTime birthTime = LocalTime.parse("23:59:59");     // 23시 59분 59초
```

</br>

### 특정 필드의 값 가져오기 - get(), getXXX()

`LocalDate`와 `LocalTime`의 객체에서 특정 필드의 값을 가져올 때는 아래의 표에 있는 메소드를 사용한다. 주의할 점은 `Calendar`와 달리 월(month)의 범위가 1~12이고, 요일은 월요일이 1, 화요일이 2, ..., 일요일은 7이라는 것이다.

> Calendar는 1월을 0으로 표현하고, 일요일은 1, 월요일은 2, ..., 토요일은 7로 표현한다.

![image](https://ifh.cc/g/FTgwdk.png)

위의 표에 소개된 메소드 외에도 `get()`과 `getLong()`이 있는데, 원하는 필드를 직접 지정할 수 있다. 대부분의 필드는 int타입의 범위에 속하지만, 몇몇 필드는 int타입의 범위를 넘을 수 있다. 그럴 때 `get()`대신 `getLong()`을 사용해야 한다. `getLong()`을 사용해야 하는 필드는 아래의 표에서 이름 옆에 '*'표시가 되어 있다.

``` java
int get(TemporalField field)
int getLong(TemporalField field)
```

이 메소드들의 매개변수로 사용할 수 있는 필드의 목록은 아래와 같다.

![image](https://ifh.cc/g/DmXcVm.png)

이 목록은 `ChronoField`에 정의된 모든 상수를 나열한 것일 뿐, 사용할 수 있는 필드는 클래스마다 다르다. 예를 들어 `LocalDate`는 날짜를 표현하기 위한 것이므로, `MINUTE_OF_HOUR`와 같이 시간에 과녈ㄴ된 필드는 사용할 수 없다.

> 만일 해당 클래스가 지원하지 않는 필드를 사용하면, UnsupportedTemporalTypeException이 발생한다.

``` java
LocalDate today = LocalDate.now();  // 오늘의 날짜
System.out.println(today.get(ChronoField.MINUTE_OF_HOUR));  // 예외 발생
```

참고로 특정 필드가 가질 수 있는 값의 범위를 알고 싶으면, 다음과 같이 하면 된다.

``` java
System.out.println(ChronoField.CLOCK_HOUR_OF_DAY.range());  // 1 ~ 24
System.out.println(ChronoField.HOUR_OF_DAY.range());  // 0 ~ 23
```

`HOUR_OF_DAY`는 밤 12시를 0으로 표현하고, `CLOCK_HOUR_OF_DAY`는 24로 표현한다.

</br>

### 필드의 값 변경하기 - with(), plus(), minus()

날짜와 시간에서 특정 필드 값을 변경하려면, 다음과 같이 with로 시작하는 메소드를 사용하면 된다.

``` java
LocalDate withYear(int year)
LocalDate withMonth(int month)
LocalDate withDayOfMonth(int dayOfmonth)
LocalDate withDayOfYear(int dayOfYear)

LocalTime withHour(int hour)
LocalTime withMinute(int minute)
LocalTime withSecond(int second)
LocalTime withNano(int nanoOfSecond)
```

`with()`를 사용하면, 원하는 필드를 직접 지정할 수 있다. 위의 메소드들은 모두 `with()`로 작성된 것이라는 것을 알 수 있다.

``` java
LocalDate with(TemporalField field, long newValue)
```

필드를 변경하는 메소드들은 항상 새로운 객체를 생성해서 반환하므로 아래와 같이 대입 연산자를 같이 사용해야 한다.

``` java
date = date.withYear(2000); // 년도를 2000년으로 변경
time = time.withHour(12);   // 시간을 12시로 변경
```

이 외에도 특정 필드에 값을 더하거나 빼는 `plus()`와 `minus()`가 있는데, 아래에는 `plus()`만 표시하였다.

``` java
LocalTime plus(TemporalAmount amountToAdd)
LocalTime plus(long amountToAdd, TemporalUnit unit)

LocalDate plus(TemporalAmount amountToAdd)
LocalDate plus(long amountToAdd, TemporalUnit unit)
```

`plus()`로 만든 다음과 같은 메소드들도 있다.

``` java
LocalDate plusYears(long yearsToAdd)
LocalDate plusMonths(long monthsToAdd)
LocalDate plusDays(long daysToAdd)
LocalDate plusWeeks(long weeksToAdd)

LocalTime plusHours(long hoursToAdd)
LocalTime plusMinutes(long minutesToAdd)
LocalTime plusSeconds(long secondsToAdd)
LocalTime plusNanos(long nanosToAdd)
```

그리고 `LocalTime`의 `truncatedTo()`는 지정된 것보다 작은 단위의 필드를 0으로 만든다.

``` java
LocalTime time = LocalTime.of(12, 34, 56);  // 12시 34분 56초
time = time.truncatedTo(ChronoUnit.HOURS);  // 시(hour)보다 작은 단위를 0으로.
System.out.println(time);   // 12:00
```

`LocalTime`과 달리 `LocalDate`에는 `truncatedTo()`가 없는데, 그 이유는 `LocalDate`의 필드인 년, 월, 일은 0이 될 수 없기 때문이다. 그리고 이 메소드의 매개변수로는 아래의 표중에서 시간과 관련된 필드만 사용가능하다.

![image](https://ifh.cc/g/H81QcW.png)

</br>

### 날짜와 시간의 비교 - isAfter(), isBefore(), isEqual()

`LocalDate`와 `LocalTime`도 `compareTo()`가 적절히 오버라이딩되어 있어서, 아래와 같이 `compareTo()`로 비교할 수 있다.

``` java
int result = date1.compareTo(date2);    // 같으면 0, date1이 이전이면 -1, 아후면 1
```

그런데도 보다 편리하게 비교할 수 있는 메소드들이 추가로 제공된다.

``` java
boolean isAfter(ChronoLocalDate other)
boolean isBefore(ChronoLocalDate other)
boolean isEqual(ChronoLocalDate other)  // LocalDate에만 있음
```

`equals()`가 있는데도, `isEqual()`을 제공하는 이유는 연표(chronology)가 다른 두 날짜를 비교하기 위해서이다. 모든 필드가 일치해야하는 `equals()`와 달리 `isEqual()`은 오직 날짜만 비교한다. 그래서 대부분의 경우 `equals()`와 `isEqual()`의 결과는 같ㄴ다.

``` java
LocalDate kDate = LocalDate.of(1999, 12, 31);
JapaneseDate jDate = JapaneseDate.of(1999, 12, 31);

System.out.println(kDate.equals(jDate));    // false YEAR_OF_ERA가 다름
System.out.println(kDate.isEqual(jDate));   // true
```

</br>

예제 10-22 / ch10 / NewTimeEx1.java

``` java
import java.time.*;
import java.time.temporal.*;

public class NewTimeEx1 {
	public static void main(String[] args) {
		LocalDate today = LocalDate.now();	// 오늘의 날짜
		LocalTime now = LocalTime.now();	// 현재 시간
		
		LocalDate birthDate = LocalDate.of(1999, 12, 31);	// 1999년 12월 31일
		LocalTime birthTime = LocalTime.of(23, 59, 59);	// 23시 59분 59초
		
		System.out.println("today = " + today);
		System.out.println("now = " + now);
		System.out.println("birthDate = " + birthDate);	// 1999-12-31
		System.out.println("birthTime = " + birthTime);	// 23:59:59
		
		System.out.println(birthDate.withYear(2000));	// 2000-12-31
		System.out.println(birthDate.plusDays(1));	// 2000-01-01
		System.out.println(birthDate.plus(1, ChronoUnit.DAYS));	// 2000-01-01
		
		// 23:59:59 -> 23:00
		System.out.println(birthTime.truncatedTo(ChronoUnit.HOURS));
		
		// 특정 ChronoField의 범위를 알아내는 방법
		System.out.println(ChronoField.CLOCK_HOUR_OF_DAY.range());	// 1-24
		System.out.println(ChronoField.HOUR_OF_DAY.range());	// 0-23
	}
}
```

```
today = 2022-10-27
now = 22:54:33.065453500
birthDate = 1999-12-31
birthTime = 23:59:59
2000-12-31
2000-01-01
2000-01-01
23:00
1 - 24
0 - 23
```

</br>

## 3.3 Instant

`Instant`는 에포크 타입(EPOCH TIME, 1970-01-01 00:00:00 UTC)부터 경과된 시간을 나노초 단위로 표현한다. 사람에겐 불편하지만, 단일 진법으로만 다루기 때문에 계산하기 쉽다. 사람이 사용하는 날짜와 시간은 여러 진법이 섞여있어서 계산하기 어렵다.

``` java
Instant now = Instant.now();
Instant now2 = Instant.ofEpochSecond(now.getEpochSecond());
Instant now3 = Instant.ofEpochSecond(now.getEpochSecond(), now.getNano());
```

`Instant`를 생성할 때는 위와 같이 `now()`와 `ofEpochSecond()`를 사용한다. 그리고 필드에 저장된 값을 가져올 때는 다음과 같이 한다.

``` java
long epochSec = now.getEpochSecond();
int nano = now.getNano();
```

`Instant`는 시간을 초 단위와 나노초 단위로 나누어 저장한다. 오라크 데이터베이스의 타임스탬프(timestamp)처럼 밀리초 단위의 EPOCH TIME이 필요로 하는 경우를 위해 `toEpochMilli()`가 정의되어 있다.

``` java
long toEpochMilli()
```

`Instant`는 항상 UTC(+00:00)를 기준으로 하기 때문에, `LocalTime`과 차이가 있을 수 있다. 예를 들어 한국은 시간대가 '+09:00'이므로 `Instant`와 `LocalTime`간에는 9시간의 차이가 있다. 시간대를 고려해야 하는 경우 `OffsetDateTime`을 사용하는 것이 더 나은 선택일 수도 있다.

UTC는 'Coordinated Universal Time'의 약어로 '세계 협정시'이라고 하며, 1972년 1월 1일부터 시행된 국제 표준서이다. 이전에 사용되던 GMT(Greenwich Mean Time)와 UTC는 거의 같지만, UTC가 좀 더 정확하다.

</br>

### Instant와 Date간의 변환

`Instant`는 기존의 `java.util.Date`를 대체하기 위한 것이며, JDK1.8부터 `Date`에 `Instant`로 변환할 수 있는 새로운 메소드가 추가되었다.

``` java
static Date from(Instant instant)   // Instant → Date
Instant toInstant() // Date → Instant
```

</br>

## 3.4 LocalDateTime과 ZonedDateTime

`LocalDate`와 `LocalTime`을 합쳐 놓은 것이 `LocalDateTime`이고, `LocalDateTime`에 시간대(time zone)를 추가한 것이 `ZonedDateTime`이다.

![image](https://ifh.cc/g/KrxRRT.png)

</br>

### LocalDate와 LocalTime으로 LocalDateTime만들기

`LocalDate`와 `LocalTime`으로 합쳐서 하나의 `LocalDateTime`을 만들 수 있다. 다음은 `LocalDateTime`을 만들 수 있는 다양한 방법을 보여준다.

``` java
LocalDate date = LocalDate.of(2015, 12, 31);
LocalTime time = LocalTime.of(12, 34, 56);

LocalDateTime dt = LocalDateTime.of(date, time);
LocalDateTime dt2 = date.atTime(time);
LocalDateTime dt3 = time.atDate(date);
LocalDateTime dt4 = date.atTime(12, 34, 56);
LocalDateTime dt5 = time.atDate(LocalDate.of(2015, 12, 31));
LocalDateTime dt6 = date.atStartOfDay();    // dt6 = date.atTime(0, 0, 0);
```

`LocalDateTime`에도 날짜와 시간을 직접 작성할 수 있는 다양한 버전의 `of()`와 `now()`가 정의되어 있다.

``` java
// 2015년 12월 31일 12시 34분 56초
LocalDateTime dateTime = LocalDateTime.of(2015, 12, 31, 12, 34, 56);
LocalDateTime today = LocalDateTime.now();
```

</br>

### LocalDateTime의 변환

반대로 `LocalDateTime`을 `LocalDate` 또는 `LocalTime`으로 변환할 수 있다.

``` java
LocalDateTime dt = LocalDateTime.of(2015, 12, 31, 12, 34, 56);
LocalDate date = dt.toLocalDate();  // LocalDateTime → LocalDate
LocalTime time = dt.toLocalTime();  // LocalDateTime → LoaclTime
```

</br>

### LocalDateTime으로 ZonedDateTime만들기

`LocalDateTime`에 시간대(time-zone)를 추가하면, `ZonedDateTime`이 된다. 기존에는 `TimeZone`클래스로 시간대를 다뤘지만 새로운 시간 패키지에서는 `ZoneId`라는 클래스를 사용한다. `ZoneId`는 일광 절약시간(DST, Daylight Saving Time)을 자동적으로 처리해주므로 더 편리하다.

`LocalDate`에 시간 정보를 추가하는 `atTime()`을 쓰면 `LocalDateTime`을 얻을 수 있는 것처럼, `LocalDateTime`에 `atZone()`으로 시간대 정보를 추가하면, `ZonedDateTime`을 얻을 수 있다.

> 사용가능한 ZoneId의 목록은 ZoneId.getAvailableZoneIds()로 얻을 수 있다.

``` java
ZoneId zid = ZoneId.of("Asia/Seoul");
ZonedDateTime zdt = dateTime.atZone(zid);
System.out.println(zdt);    // 2022-10-27T23:18:23.451+09:00[Asia/Seoul]
```

`LocalDate`에 `atStratOfDay()`라는 메소드가 있는데, 이 메소드에 매개변수로 `ZoneId`를 지정해도 `ZonedDateTime`을 얻을 수 있다.

``` java
ZonedDateTime zdt = LocalDate.now().atStartOfDay(zid);
System.out.println(zdt);    // 2022-10-27T00:00+9:00[Aisa/Seoul]
```

메소드의 이름(atStartOfDay)에서 알 수 있듯이 시간이 0시 0분 0초로 되어 있는 것을 확인할 수 있다.

만일 현재 특정 시간대의 시간, 예를 들어 뉴욕을 알고 싶다면 다음과 같이 하면 된다.

``` java
ZoneId nyId = ZoneId.of("America/New York");
ZonedDateTime nyTime = ZonedDateTime.now().withZoneSameInstant(nyId);
```

위의 코드에서 `now()` 대신 `of()`를 사용하면 날짜와 시간을 지정할 수 있다.

</br>

### ZoneOffset

UTC로부터 얼마만큼 떨어져 있는지를 `ZoneOffset`으로 표현한다. 위의 결과에서 알 수 있듯이 서울은 '+9'이다. 즉, UTC보다 9시간(32400초=60*60*9초)이 빠르다.

``` java
    ZoneOffset krOffset = ZoneIdDateTime.now().getOffset();
//  ZoneOFfset krOffset = ZoneOffset.of("+9");  // ±h, ±hh, ±hhmm, ±hh:mm
    int krOffsetInSec = krOffset.get(ChronoField.OFFSET_SECONDS);   // 32400초
```

</br>

### OffsetDateTime

`ZonedDateTime`은 `ZoneId`로 구역을 표현하는데, `ZoneId`가 아닌 `ZoneOffset`을 사용하는 것이 `OffsetDateTime`이다. `ZoneId`는 일광절약시간처럼 시간대와 관련된 규칙들을 포함하고 있는데, `ZoneOffset`은 단지 시간대를 시간의 차이로만 구분한다.

같은 지역내의 컴퓨터간에 데이터를 주고받을 때, 전송시간을 표현하기에 `LocalDateTime`이면, 충분하겠지만, 서로 다른 시간대에 존재하는 컴퓨터간의 통신에는 `OffsetDateTime`이 필요하다.

``` java
ZonedDateTime zdt = ZonedDateTime.of(date, time, zid);
OffsetDateTime odt = OffsetDateTime.of(date, time, krOffset);

// ZonedDateTime → OffsetDateTime
OffsetDateTime odt = zdt.toOffsetDateTime();
```

`OffsetDateTime`은 `ZonedDateTime`처럼, `LocalDate`와 `LocalTime`에 `ZoneOffset`을 더하거나, `ZonedDateTime`에 `toOffsetDateTime()`을 호출해서 얻을 수도 있다.

</br>

### ZoneDateTime의 변환

`ZonedDateTime`도 `LocalDateTime`처럼 날짜와 시간에 관련된 다른 클래스로 변환하는 메소드들을 가지고 있다.

``` java
LocalDate toLocalDate()
LocalTime toLocalTime()
LocalDateTime toLocalDateTime()
OffsetDateTime toOffsetDateTime()
long toEpochSecond()
Instant toInstant()
```

`GregorianCalendar`와 가장 유사한 것이 `ZonedDateTime`이다. `GregorianCalendar`와 `ZonedDateTime`간의 변환방법만 알면, 그 다음엔 위에 나열한 메소드를 이용해서 다른 날짜와 시간 클래스들로 변환할 수 있다.

``` java
// ZoneDateTime → GregorianCalendar
GregorianCalendar from(ZonedDateTime zdt)

// GregorianCalendar → ZonedDateTime
ZonedDatetime = toZonedDateTime()
```

</br>

예제 10-23 / ch10 / NewTimeEx2.java

``` java
import java.time.*;

public class NewTimeEx2 {
	public static void main(String[] args) {
		LocalDate date = LocalDate.of(2015, 12, 31);	// 2015년 12월 31일
		LocalTime time = LocalTime.of(12, 34, 56);	// 12시 34분 56초
		
		// 2015년 12월 31일 12시 34분 56초
		LocalDateTime dt = LocalDateTime.of(date, time);
		
		ZoneId zid = ZoneId.of("Asia/Seoul");
		ZonedDateTime zdt = dt.atZone(zid);
//		String strZid = zdt.getZone().getId();
		
		ZonedDateTime seoulTime = ZonedDateTime.now();
		ZoneId nyId = ZoneId.of("America/New_York");
		ZonedDateTime nyTime = ZonedDateTime.now().withZoneSameInstant(nyId);
		
		// ZoneDateTime -> OffsetDateTime
		OffsetDateTime odt = zdt.toOffsetDateTime();
		
		System.out.println(dt);
		System.out.println(zid);
		System.out.println(zdt);
		System.out.println(seoulTime);
		System.out.println(nyTime);
		System.out.println(odt);
	}
}
```

```
2015-12-31T12:34:56
Asia/Seoul
2015-12-31T12:34:56+09:00[Asia/Seoul]
2022-10-27T23:37:20.631395700+09:00[Asia/Seoul]
2022-10-27T10:37:20.636278300-04:00[America/New_York]
2015-12-31T12:34:56+09:00
```

</br>

## 3.5 TemporalAdjusters

자주 쓰일만한 날짜 계산들을 대신 해주는 메소드를 정의해 놓은 것이 `TemporalAdjusters`클래스이다.

``` java
LocalDate today = LocalDate.now();
LocalDate nextMonday = today.with(TemporalAdjusters.next(DayOfWeek.MONDAY));
```

위의 코드는 다음 주 월요일의 날짜를 계산할 때 `TemporalAdjusters`에 정의된 `next()`를 사용하였다. 이 외에도 다음 과 같이 더 많은 유용한 메소드들이 `TemporalAdjusters`에 정의되어 있다.

![image](https://ifh.cc/g/yJCRZ5.png)

</br>

### TemporalAdjuster직접 구현하기

`LocalDate`의 `with()`는 다음과 같이 정의되어있으며, `TemporalAdjuster`인터페이스를 구현한 클래스의 객체를 매개변수로 제공해야한다.

``` java
LocalDate with(TemporalAdjuster adjuster)
```

`with()`는 `LocalTime`, `LocalDateTime`, `ZonedDateTime`, `Instant` 등 대부분의 날짜와 시간에 관련된 클래스에 포함되어 있다.

`TemporalAdjuster`인터페이스는 다음과 같이 추상 메소드 하나만 정의되어 있으며, 이 메소드만 구현하면 된다.

``` java
@FunctionInterface
public interface TemporalAdjuster {
	Temporal adjustInto(Temporal temporal);
}
```

실제로 구현해야하는 것은 `adjustInto()`지만, 우리가 `TemporalAdjuster`와 같이 사용해야 하는 메소드는 `with()`이다. `with()`와 `adjustInto()`중에서 어느 쪽을 사용해도 되지만, `adjustInto()`는 내부적으로만 사용할 의도로 작성된 것이기 때문에, `with()`를 사용해야 한다.

날짜와 시간에 관련된 대부분의 클래스는 `Temporal`인터페이스를 구현하였으므로 `adjustInto()`의 매개변수가 될 수 있다.

예를 들어, 특정 날짜로부터 2일 후의 날짜를 계산하는 `DayAfterTomorrow`는 다음과 같이 작성할 수 있다.

``` java
class DayAfterTomorrow implements TemporalAdjuster {
	@Override
	public Temporal adjustInto(Temporal temporal) {
		return temporal.plus(2, ChronoUnit.DAYS);	// 2일을 더한다.
	}
}
```

</br>

예제 10-24 / ch10 / NewTimeEx3.java

``` java
import java.time.*;
import java.time.temporal.*;
import static java.time.DayOfWeek.*;
import static java.time.temporal.TemporalAdjusters.*;

class DayAfterTomorrow implements TemporalAdjuster {
	@Override
	public Temporal adjustInto(Temporal temporal) {
		return temporal.plus(2, ChronoUnit.DAYS);
	}
}

public class NewTimeEx3 {
	public static void main(String[] args) {
		LocalDate today = LocalDate.now();
		LocalDate date = today.with(new DayAfterTomorrow());
		
		p(today);	// System.out.println(today);
		p(date);
		p(today.with(firstDayOfNextMonth()));	// 다음 달의 첫 날
		p(today.with(firstDayOfMonth()));	// 이 달의 첫 날
		p(today.with(lastDayOfMonth()));	// 이 달의 마지막 날
		p(today.with(firstInMonth(TUESDAY)));	// 이 달의 첫번째 화요일
		p(today.with(lastInMonth(TUESDAY)));	// 이 달의 첫번째 화요일
		p(today.with(previous(TUESDAY)));	// 지난주 화요일
		p(today.with(previousOrSame(TUESDAY)));	// 지난주 화요일(오늘 포함)
		p(today.with(next(TUESDAY)));	// 다음 주 화요일
		p(today.with(nextOrSame(TUESDAY)));	// 다음 주 화요일(오늘 포함)
		p(today.with(dayOfWeekInMonth(4, TUESDAY)));	// 이 달의 4번째 화요일
	}
	
	static void p(Object obj) {	// 라인의 길이를 줄이기 위해 새로 정의한 메소드
		System.out.println(obj);
	}
}
```

```
2022-10-28
2022-10-30
2022-11-01
2022-10-01
2022-10-31
2022-10-04
2022-10-25
2022-10-25
2022-10-25
2022-11-01
2022-11-01
2022-10-25
```

</br>

## 3.6 Period와 Duration

`Period`는 날짜의 차이를, `Duration`은 시간의 차이를 계산하기 위한 것이다.

![image](https://ifh.cc/g/wL0HYa.png)

</br>

### between()

두 날짜 `date1`와 `date2`의 차이를 나타내는 `Period`는 `between()`으로 얻을 수 있다.

``` java
LocalDate date1 = LocalDate.of(2014, 1, 1);
LocalDate date2 = LocalDate.of(2015, 12, 31);

Period pe = Period.between(date1, date2);
```

`date1`이 `date2`보다 날짜 상으로 이전이면 양수로, 이후면 음수로 `Period`에 저장된다. 그리고 시간차이를 구할 때는 `Duration`을 사용한다는 것을 제외하고는 `Period`와 똑같다.

``` java
LocalTime time1 = LocalTime.of(00, 00, 00);
LocalTime time2 = LocalTime.of(12, 34, 56);	// 12시 34분 56초

Duration du = Duration.between(time1, time2);
```

`Period`, `Duration`에서 특정 필드의 값을 얻을 때는 `get()`을 사용한다.

``` java
long year = pe.get(ChronoUnit.YEARS);	// int getYears()
long month = pe.get(ChronoUnit.MONTHS);	// int getMonths()
long day = pe.get(ChronoUnit.DAYS);		// int getDays()

long sec = du.get(ChronoUnit.SECONDS);	// long getSeconds()
int nano = du.get(ChronoUnit.NANOS);	// int getNano()	
```

그런데, `Period`와 달리 `Duration`에는 `getHours()`, `getMinutes()` 같은 메소드가 없다. `getUnits()`라는 메소드로 `get()`에 사용할 수 있는 `ChronoUnit`의 종류를 확인할 수 있다.

``` java
System.out.println(pe.getUnits());	// [Years, Months, Days]
System.out.println(du.getUnits());	// [Seconds, Nanos]
```

`Duration`에는 `Chrono.SECONDS`와 `Chrono.NANOS`밖에 사용할 수 없다. 다음과 같이 직접 계산해 보았다.

``` java
long hour = du.getSeconds() / 3600;
long min = (du.getSeconds() - hour*3600) / 60;
long sec = (du.getSeconds() - hour*3600 - min * 60) % 60;
int nano = du.getNano();
```

`Duration`을 `LocalTime`으로 변환한 다음에, `LocalTime`이 가지고 있는 `get`메소드들을 사용하면 더 간단하다.

``` java
LocalTime tmpTIme = LocalTime.of(0, 0).plusSeconds(du.getSeconds());

int hour = tmpTime.getHour();
int min = tmpTime.getMinute();
int sec = tmpTime.getSecond();
int nano = du.getNano();
```

</br>

### between()과 until()

`until()`은 `between()`과 거의 같은 일을 한다. `between()`은 static메소드이고, `until()`은 인스턴스 메소드라는 차이가 있다.

``` java
//	Period pe = Period.between(today, byBirthDay);
	Period pe = today.until(myBirthDay);
	long dday = today.until(myBirthDay, ChronoUnit.DAYS);
```

`Period`는 년월일을 분리해서 저장하기 때문에, D-day를 구하려는 경우에는 두 개의 매개변수를 받는 `until()`을 사용하는 것이 낫다. 날짜가 아닌 시간에도 `until()`을 사용할 수 있지만, `Duration`을 반환하는 `until()`은 없다.

``` java
long sec = LocalTime.now().until(endTime, ChronoUnit.SECONDS);
```

</br>

### of(), with()

`Period`에는 `of()`, `ofYears()`, `ofMonths()`, `ofWeeks()`, `ofDays()`가 있고, `Duration`에는 `of()`, `ofHours()`, `ofMinutes()`, `ofSeconds()` 등이 있다.

``` java
	Period pe = Period.of(1, 12, 31);	// 1년 12개월 31일
	Duration du = Duration.of(60, ChronoUnit.SECONDS);	// 60초
//	Duration du = Duration.ofSeconds(60);	// 위의 문장과 동일.
```

특정 필드의 값을 변경하는 `with()`도 있다.

``` java
pe = pe.withYears(2);	// 1년에서 2년으로 변경. withMonths(), withDays()
du = du.withSeconds(120);	// 60초에서 120초로 변경. withNanos()
```

</br>

### 사칙연산, 비교연산, 기타 메소드

`plus()`, `minus()`외에 곱셈과 나눗셈을 위한 메소드도 있다.

``` java
pe = pe.minusYears(1).multipliedBy(2);	// 1년을 빼고, 2배를 곱한다.
du = du.plusHours(1).divideBy(60);	// 1시간을 더하고 60으로 나눈다.
```

`Period`에 나눗셈을 위한 메소드가 없는데, `Period`는 날짜와 기간을 표현하기 위한 것이므로 나눗셈을 위한 메소드가 별로 유용하지 않기 때문에 넣지 않은 것이다.

그리고 음수인지 확인하는 `isNegative()`와 0인지 확인하는 `isZero()`가 있다. 두 날짜 또는 시간을 비교할 때, 사용하면 어느 쪽이 앞인지 또는 같은지 알아낼 수 있다.

``` java
boolean sameDate = Period.between(date1, date2).isZero();
boolean isBefore = Duration.between(time1, time2).isNegative();
```

부호를 반대로 변경하는 `negate()`와 부호를 없애는 `abs()`가 있다. 아래 양쪽의 코드는 동일하다. `Period`에는 `abs()`가 없어서 대신 아래의 오른쪽과 같은 코드를 사용해야 한다.

![image](https://ifh.cc/g/rQ9oMf.png)

`Period`에 `normalized()`라는 메소드가 있는데, 이 메소드는 월(month)의 값이 12를 넘지 않게, 즉 1년 13개월을 2년 1개월로 바꿔준다. 일(day)의 길이는 일정하지 않으므로 그대로 놔둔다.

``` java
pe = Period.of(1, 13, 32).normalized();	// 1년 13개월 32일 → 2년 1개월 32일
```

</br>

### 다른 단위로 변환 - toTotalMonths(), toDays(), toHours(), toMinutes()

이름이 'to'로 시작하는 메소드들이 있는데, 이 들은 `Period`와 `Duration`을 다른 단위의 값으로 변환하는데 사용된다. `get()`은 특정 필드의 값을 그대로 가져오는 것이지만, 아래의 메소드들은 특정 단위로 변환한 결과를 반환한다는 차이가 있다.

> 이 메소드들의 반환타입은 모두 정수(long타입)인데, 이것은 지정된 단위 이하의 값들은 버려진다는 뜻이다.

![image](https://ifh.cc/g/FAh10l.png)

참고로 `LocalDate`의 `toEpochDay()`라는 메소드는 Epoch Day인 '1970-01-01'부터 날짜를 세어서 반환한다. 이 메소드를 이용하면 `Period`를 사용하지 않고도 두 날짜간의 일수를 편리하게 계산할 수 있다. 단, 두 날짜 모두 Epoch Day이후의 것이어야 한다.

``` java
LocalDate date1 = LocalDate.of(2015, 11, 28);
LocalDate date2 = LocalDate.of(2015, 11, 29);

long period = date2.toEpochDay() - date1.toEpochDay();	// 1
```

`LocalTime`에도 다음과 같은 메소드가 있어서, `Duration`을 사용하지 않고도 위와 같이 뺄셈으로 시간차이를 계산할 수 있다.

``` java
int toSecondOfDay()
long toNanoOfDay()
```

</br>

예제 10-25 / ch10 / NewTiimeEx4.java

``` java
import java.time.*;
import java.time.temporal.*;

public class NewTimeEx4 {
	public static void main(String[] args) {
		LocalDate date1 = LocalDate.of(2014, 1, 1);
		LocalDate date2 = LocalDate.of(2015, 12, 31);
		
		Period pe = Period.between(date1, date2);
		
		System.out.println("date1 = " + date1);
		System.out.println("date2 = " + date2);
		System.out.println("pe = " + pe);
		
		System.out.println("YEAR = " + pe.get(ChronoUnit.YEARS));
		System.out.println("MONTH = " + pe.get(ChronoUnit.MONTHS));
		System.out.println("DAY = " + pe.get(ChronoUnit.DAYS));
		
		LocalTime time1 = LocalTime.of(0, 0, 0);
		LocalTime time2 = LocalTime.of(12, 34, 56);	// 12시간 34분 56초
		
		Duration du = Duration.between(time1, time2);
		
		System.out.println("time1 = " + time1);
		System.out.println("time2 = " + time2);
		System.out.println("du = " + du);
		
		LocalTime tmpTime = LocalTime.of(0, 0).plusSeconds(du.getSeconds());
		
		System.out.println("HOUR = " + tmpTime.getHour());
		System.out.println("MINUTE = " + tmpTime.getMinute());
		System.out.println("SECOND = " + tmpTime.getSecond());
		System.out.println("NANO = " + tmpTime.getNano());
	}
}
```

```
date1 = 2014-01-01
date2 = 2015-12-31
pe = P1Y11M30D
YEAR = 1
MONTH = 11
DAY = 30
time1 = 00:00
time2 = 12:34:56
du = PT12H34M56S
HOUR = 12
MINUTE = 34
SECOND = 56
NANO = 0
```

</br>

## 3.7 파싱과 포맷

형식화(formatting)와 관련된 클래스들은 `java.time.format`패키지에 들어있는데, 이 중에서 `DateTimeFormatter`가 핵심이다. 이 클래스에는 자주 쓰이는 다양한 형식들을 기본적으로 정의하고 있으며, 그 외의 형식이 필요하다면 직접 정의해서 사용할 수도 있다.

``` java
LocalDate date = LocalDate.of(2016, 1, 2);
String yyyymmdd = DateTimeFormatter.ISO_LOCAL_DATE.format(date);	// "2022-10-28"
String yyyymmdd = date.format(DateTimeFormatter.ISO_LOCAL_DATE);	// "2022-10-28"
```

날짜와 시간의 형식화에는 위와 같은 `format()`이 사용되는데, 이 메소드는 `DateTimeFormatter`뿐만 아니라 `LocalDate`나 `LocalTime`같은 클래스에도 있다. 같은 기능을 하니까 상황에 따라 편한 쪽을 선택해서 사용하면 된다.

아래의 표는 `DateTimeFormatter`에 상수로 정의된 형식들의 목록이다.

![image](https://ifh.cc/g/PFcxaX.png)

</br>

### 로케일에 종속된 형식화

`DateTimeFormatter`의 static메소드 `ofLocalizedDate()`, `ofLocalizedTime()`, `ofLocalized DateTime()`은 로케일(locale)에 종속적인 포맷터를 생성한다.

``` java
DateTimeFormatter formatter = DateTimeFormatter.ofLocalizedDate(FormatStyle.SHORT);
String shortFormat = formatter.format(LocalDate.now());
```

`FormatSytle`의 종류에 따른 출력 형태는 다음과 같다.

![image](https://ifh.cc/g/hnzpsO.png)

</br>

### 출력형식 직접 정의하기

`DateTimeFormatter`의 `ofPattern()`으로 원하는 출력형식을 직접 작성할 수도 있다.

``` java
DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy/MM/dd");
```

출력형식에 사용되는 기호의 목록은 다음과 같다.

![image](https://ifh.cc/g/lvvDbk.png)

아래의 예제는 자주 사용될만한 패턴의 예를 보여준다.

</br>

예제 10-26 / ch10 / DateFormatterEx1.java

``` java
import java.time.*;
import java.time.format.*;

public class DateFormatterEx1 {
	public static void main(String[] args) {
		ZonedDateTime zdateTime = ZonedDateTime.now();
		
		String[] patternArr = {
				"yyyy-MM-dd HH:mm:ss",
				"''yy년 MMM dd일 E요일",
				"yyyy-MM-dd HH:mm:ss.SSS Z VV",
				"yyyy-MM-dd hh:mm:ss a",
				"오늘은 올 해의 D번째 날입니다.",
				"오늘은 이 달의 d번째 날입니다.",
				"오늘은 올 해의 w번째 날입니다.",
				"오늘은 이 달의 W번째 주입니다.",
				"오늘은 이 달의 W번째 E요일입니다."
		};
		
		for(String p : patternArr) {
			DateTimeFormatter formatter = DateTimeFormatter.ofPattern(p);
			System.out.println(zdateTime.format(formatter));
		}
	}	// main의 끝
}
```

```
2022-10-28 22:36:21
'22년 10월 28일 금요일
2022-10-28 22:36:21.084 +0900 Asia/Seoul
2022-10-28 10:36:21 오후
오늘은 올 해의 301번째 날입니다.
오늘은 이 달의 28번째 날입니다.
오늘은 올 해의 44번째 날입니다.
오늘은 이 달의 5번째 주입니다.
오늘은 이 달의 5번째 금요일입니다.
```

</br>

### 문자열을 날짜와 시간으로 파싱하기

문자열을 날짜 또는 시간으로 변환하려면 static메소드 `parse()`를 사용하면 된다. 날짜와 시간을 표현하는데 사용되는 클래스에는 이 메소드가 거의 다 포함되어 있다. `parse()`는 오버로딩된 메소드가 여러 개 있는데, 그중에서 다음의 2개가 자주 쓰인다.

``` java
static LocalDateTime parse(CharSequence text)
static LocalDateTime parse(CharSequence text, DateTimeFormatter formatter)
```

`DateTimeFormatter`에 상수로 정의된 형식을 사용할 때는 다음과 같다.

``` java
LocalDate date = LocalDate.parse("2016-01-02", DateTimeFormatter.ISO_LOCAL_DATE);
```

자주 사용되는 기본적인 형식의 문자열은 `ISO_LOCAL_DATE`와 같은 형식화 상수를 사용하지 않고도 파싱이 가능하다.

``` java
LocalDate newDate = LocalDate.parse("2001-01-01");
LocalTime newTime = LocalTime.parse("23:59:59");
LocalDateTime newDateTime = LocalDateTime.parse("2001-01-01T23:59:59");
```

다음과 같이 `ofPattern()`을 이용해서 파싱을 할 수도 있다.

``` java
DateTimeFormatter pattern = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");
LocalDateTime endOfYear = LocalDateTime.parse("2015-12-31 23:59:59", pattern);
```

</br>

예제 10-27 / ch10 / DateFormatterEx2.java

``` java
import java.time.*;
import java.time.format.*;

public class DateFormatterEx2 {
	public static void main(String[] args) {
		LocalDate newYear = LocalDate.parse("2016-01-01", DateTimeFormatter.ISO_LOCAL_DATE);
		
		LocalDate date = LocalDate.parse("2001-01-01");
		LocalTime time = LocalTime.parse("23:59:59");
		LocalDateTime dateTime = LocalDateTime.parse("2001-01-01T23:59:59");
		
		DateTimeFormatter pattern = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");
		LocalDateTime endOfYear = LocalDateTime.parse("2015-12-31 23:59:59", pattern);
		
		System.out.println(newYear);
		System.out.println(date);
		System.out.println(time);
		System.out.println(dateTime);
		System.out.println(endOfYear);
	}	// main의 끝
}
```

```
2016-01-01
2001-01-01
23:59:59
2001-01-01T23:59:59
2015-12-31T23:59:59
```