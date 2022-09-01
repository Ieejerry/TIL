Chapter 5. 배열 array

# 1. 배열(array)

</br>

## 1.1 배열(array)이란?

같은 타입의 여러 변수를 하나의 묶음으로 다루는 것을 '배열(array)'라고 한다.

배열을 사용하면 많은 양의 데이터를 손쉽게 다룰 수 있다.

> **"배열은 같은 타입의 여러 변수를 하나의 묶음으로 다루는 것"**

여기서 중요한 것은 '같은 타입'이어야 한다는 것이며, 서로 다른 타입의 변수들로 구성된 배열은 만들 수 없다. 한 학급의 시험점수를 저장하고자 할 때가 배열을 사용하기 좋은 예이다. 만일 배열을 사용하지 않는다면 학생 5명의 점수를 저장하기 위해서 아래와 같이 5개의 변수를 선언해야 한다.

![image](https://ifh.cc/g/ddVpOM.png)

변수 대신 배열을 이용하면 다음과 같이 간단히 처리할 수 있따. 변수의 선언과 달리 다뤄야할 데이터의 수가 아무리 많아도 단지 배열의 길이만 바꾸면 된다.

``` java
int[] score = new int[5];   // 5개의 int 값을 저장할 수 있는 배열을 생성한다.
```

아래의 그림은 위의 코드가 실행되어 생성된 배열을 그림으로 나타낸 것이다. 값을 저장할 수 있는 공간은 `score[0]`부터 `score[4]`까지 모두 5개이며, 변수 `score`는 배열을 다루는데 필요한 참조변수일 뿐 값을 저장하기 위한 공간은 아니다.

![image](https://ifh.cc/g/OSn6dn.png)

변수와 달리 배열은 각 저장공간이 연속적으로 배치되어 있다는 특징이 있다.

</br>

## 1.2 배열의 선언과 생성

원하는 타입의 변수를 선언하고, 변수 또는 타입에 배열임을 의미하는 대괄호[]를 붙이면 된다. 대괄호[]는 타입 뒤에 붙여도 되고, 변수이름 뒤에 붙여도 된다.

![image](https://ifh.cc/g/ZydYj2.png)

### 배열의 생성

배열을 선언한 다음에는 배열을 생성해야 한다. 배열을 선언하는 것은 단지 생성된 배열을 다루기 위한 참조변수를 위한 공간이 만들어질 뿐이고, 배열을 생성해야만 비로소 값을 저장할 수 있는 공간이 만들어지는 것이다. 배열을 생성하기 위해서는 연산자 `new`와 함께 배열의 타입과 길이를 지정해 주어야 한다.

``` java
타입[] 변수이름;    // 배열을 선언 (배열을 다루기 위한 참조변수 선언)
변수이름 = new 타입[길이];  // 배열을 생성 (실제 저장공간을 생성)
```

아래의 코드는 '길이가 5인 int배열'을 생성한다.

``` java
int[] score;    // int타입의 배열을 다루기 위한 참조변수 score선언
score = new int[5]; // int타입의 값 5개를 저장할 수 있는 배열
```

다음과 같이 배열의 선언과 생성을 동시에 하면 간략히 한 줄로 할 수 있다.

``` java
타입[] 변수이름 = new 타입[길이];   // 배열의 선언과 생성을 동시에.
int[] score = new int[5];   // 길이가 5인 int배열
```

이제 배열의 선언과 생성과정을 단계별로 살펴보겠다.

1. int[] score;

int형 배열 참조변수 `score`를 선언한다. 데이터를 저장할 수 있는 공간은 아직 마련되지 않았다.

![image](https://ifh.cc/g/SVr5p2.png)

2. score = new int[5];

연산자 `new`에 의해서 메모리의 빈 공간에 5개의 `int`형 데이터를 저장할 수 있는 공간이 마련된다.

![image](https://ifh.cc/g/q3RBts.png)

그리고 각 배열요소는 자동적으로 `int`의 기본값(default)인 0으로 초괴화 된다.

![image](https://ifh.cc/g/8tbBfr.png)

끝으로 대입 연산자 `=`에 의해 배열의 주소가 `int`형 배열 참조변수 `score`에 저장된다.

![image](https://ifh.cc/g/OSn6dn.png)

이제 참조변수 `score`를 통해서 생성된 배열에 값을 저장하거나 읽어 올 수 있다. 이 배열은 '길이가 5인 `int`배열'이며, 참조변수의 이름을 따서 '배열 score'라고 부르면 된다.

</br>

## 1.3 배열의 길이와 인덱스

생성된 배열의 각 저장공간을 '배열의 요소(element)'라고 하며, '배열이름[인덱스]'의 형식으로 배열의 요소에 접근한다. **인덱스(index)는 배열의 요소마다 붙여진 일련번호** 로 각 요소를 구별하는데 사용된다.

인덱스는 1이 아닌 0부터 시작한다.

> "인덱스(index)의 범위는 **0부터 '배열길이 - 1'까지.**"

배열에 값을 저장하고 읽어오는 방법은 변수와 같다. 단지 변수이름 대신 '배열이름[인덱스]'를 사용한다는 점만 다르다.

``` java
score[3] = 100; // 배열 score의 4번째 요소에 100을 저장한다.
int value = score[3];   // 배열 score의 4번째 요소에 젖아된 값을 읽어서 value에 저장
```

배열의 또 다른 장점은 index로 상수 대신 변수나 수식도 사용할 수 있다는 것이다. 그래서 왼쪽의 코드를 오른쪽과 같이 `for`문을 이용해서 간단히 할 수 있다. 오른쪽 코드는 index로 상수대신 변수 `i`를 사용하고, `for`문으로 변수 `i`의 값을 0부터 4까지 증가시킨다.

![image](https://ifh.cc/g/O82G75.png)

`for`문의 제어변수 `i`는 배열의 index로 사용하기에 딱 알맞아서, 배열을 다룰 때 `for`문은 거의 필수적이다. 만일 아래와 같이 괄호[]안에 수식이 포함된 경우, 이 수식이 먼저 계산된다. 그래야만 배열의 몇 번째 요소인지 알 수 있기 때문이다.

``` java
int tmp = score[i + 1];
```

배열을 다룰 떄 한 가지 주의할 점은 index의 범위를 벗어난 값을 index로 사용하지 않아야 한다. 예를 들어 다음과 같이 길이가 5인 배열이 선언되어 있을 때, index의 범위는 0~4이다. 이 때, 이 범위를 벗어나는 값인 5를 index로 사용하면 안된다는 얘기다.

``` java
int[] score = new int[5];   // 길이가 5인 int배열, index의 범위는 0~4
    ...
score[5] = 100; // index의 범위를 벗어난 값을 index로 사용
```

유효한 범위를 벗어난 값을 index로 사용하는 것은 배열을 다룰 때 하는 가장 흔한 실수이다. 그러나 컴파일러는 이러한 실수를 걸러주지 못한다. 왜냐하면 배열의 index로 변수를 많이 사용하는데, 변수의 값은 실행 시에 대입되므로 컴파일러는 이 값의 범위를 확인할 수 없다.

그래서 유효한 범위의 값을 index로 사용하는 것은 전적으로 프로그래머의 책임이며, 유효하지 않은 값을 index로 사용하면, 무사히 컴파일을 마쳤더라도 실행 시에 에러(ArrayIndexOutOfBoundsException)가 발생한다.

예제 5-1 / ch5 / ArrayEx1.java
``` java
public class ArrayEx1 {

	public static void main(String[] args) {
		int[] score = new int[5];
		int k = 1;
		
		score[0] = 50;
		score[1] = 60;
		score[k + 1] = 70;	// score[2] = 70
		score[3] = 80;
		score[4] = 90;
		
		int tmp = score[k + 2] + score[4];	// int tmp = score[3] + score[4]
		
		// for문으로 배열의 모든 요소를 출력한다.
		for (int i = 0; i < 5; i++) {
			System.out.printf("score[%d]: %d%n", i, score[i]);
		}
		
		System.out.printf("tmp: %d%n", tmp);
	System.out.printf("score[%d]: %d%n", 7, score[7]);	// index의 범위를 벗어난 값
	}	// main

}
```

```
score[0]: 50
score[1]: 60
score[2]: 70
score[3]: 80
score[4]: 90
tmp: 170
Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: Index 7 out of bounds for length 5
	at ArrayEx1.main(ArrayEx1.java:22)
```

앞서 배운 내용을 직접 확인할 수 있는 간단한 예제이다. 배열 `score`는 길이가 5이므로 index의 범위가 0~4이지만, 일부러 이 범위에 속하지 않는 7을 배열의 index로 해서 값을 출력해보았다. 컴파일 시에는 아물너 문제가 없지만, 실행 시에는 아래와 같은 에러가 발생하였다.

```
Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: Index 7 out of bounds for length 5
	at ArrayEx1.main(ArrayEx1.java:22)
```

위 메세지는 배열의 인덱스가 유효한 범위를 넘었다는 뜻이다.

### 배열의 길이

배열을 생성할 떄 괄호[]안에 배열의 길이를 적어줘야 하는데, 배열의 길이는 배열의 요소의 개수, 즉 값을 저장할 수 있는 공간의 개수이다.

배열의 길이는 양의 정수이어야 하며 최대값은 `int`타입의 최대값, 약 20억이다.

``` java
타입[] 배열이름 = new 타입[갈이];
int[] arr = new int[5]; // 길이가 5인 int배열
```

그런데 길이가 0인 배열도 생성이 가능하다. 길이가 0이라는 얘기는 값을 저장할 수 있는 공간이 하나도 없다는 뜻이다.

``` java
int[] arr = new int[0]; // 길이가 0인 배열도 생성이 가능하다. 
```

> **배열의 길이는 int범위의 양의 정수(0도 포함)이어야 한다.**

### 배열이름.length

자바에서는 JVM이 모든 배열의 길이를 별도로 관리하며, '배열이름.length'를 통해서 배열의 길이에 대한 정보를 얻을 수 있다.

아래의 코드에서 배열 arr의 길이가 5이므로 `arr.length`의 값 역시 5가 된다.

``` java
int[] arr = new int[5]; // 길이가 5인 int배열
int tmp = arr.length;   // arr.length의 값은 5이고 tmp에 5가 저장된다.
```

배열은 한번 생성하면 길이를 변경할 수 없기 때문에, 이미 생성된 배열의 길이는 변하지 않는다. 따라서 '배열이름.length'는 상수다. 즉, 값을 읽을 수만 있을 뿐 변경할 수 없다.

``` java
int[] arr = new int[5];
arr.length = 10;    // 에러. 배열의 길이는 변경할 수 없음.
```

아래의 코드는 배열의 각 요소를 for문을 이용해서 출력한다. 여기서 배열 `score`의 길이는 6이며, 인덱스의 범위는 0\~5이다.

``` java
int[] score = new int[6];

for (int i = 0; i < 6; i++) {
    System.out.println(score[i]);
}
```

이 때 코드를 다음과 같이 변경하여 배열의 길이를 줄인다면, 유효한 인덱스의 범위는 0~4가 된다.

``` java
int[] score = new int[5];   // 배열의 길이를 6에서 5로 변경

for (int i = 0; i < 6; i++) {   // 실수로 조건식을 변경하지 않음
    System.out.println(score[i]);   // 에러발생
}
```

배열이 길이가 변경되었으니 for문에 사용되는 조건의 범위도 변경해주어야 하는데, 만일 이것을 잊고 실행한다면 for문은 배열의 유효한 인덱스 범위인 0~4를 넘어 0부터 5까지 반복하기 때문에 5번째 반복에서 `ArrayIndexOutOfBoundsException`이라는 예외(배열의 index가 유효한 범위를 벗어났다는 에러)가 발생하여 비정상적으로 종료된다.

그래서 for문의 조건식에 배여르이 길이를 직접 적어주는 것보다 '배열이름.length'를 사용하는 것이 좋다. 위의 for문을 '배열이름.length'를 사용해서 변경하면 다음과 같다.

``` java
int[] score = new int[5];   // 배열의 길이를 6에서 5로 변경

for (int i = 0; i < score.length; i++) {    // 조건식을 변경하지 않아도 됨
    System.out.println(score[i]);
}
```

'배열이름.length'는 배열의 길이가 변경되면 자동적으로 변경된 배열의 길이를 값으로 갖기 때문에, 배열과 함께 사용되는 for문의 조건식을 일일이 변경해주지 않아도 된다.

![image](https://ifh.cc/g/9DHcPN.png)

여기서는 for문을 예로 들었지만, 모든 경우에 배열의 길이를 직접 적어주는 것보다 '배열이름.length'를 하는 것이 코드의 관리가 쉽고 에러가 발생할 확률이 적어진다.

</br>

## 1.4 배열의 초기화

배열은 생성과 동시에 자도엊긍로 자신의 타입에 해당하는 기본값으로 초기화되므로 배열을 사용하기 전에 따로 초기화를 해주지 않아도 되지만, 원하는 값을 저장하려면 아래와 같이 각 요소마다 값을 지정해 줘야한다.

``` java
int[] score = new int[5];	// 길이가 5인 int형 배열을 생성한다.
score[0] = 50;	// 각 요소에 직접 값을 저장한다.
score[1] = 60;
score[2] = 70;
score[3] = 80;
score[4] = 90;
```

배열의 길이가 큰 경우에는 이렇게 요소 하나하나에 값을 지정하기 보다는 for문을 사용하는 것이 좋다. 위의 코드를 for문을 이용해서 바꾸면 다음과 같다.

``` java
int[] score = new int[5];	// 길이가 5인 int형 배열을 생성한다.

for (int i = 0; i < score.length; i++) {
	score[i] = i * 10 + 50;
}
```

그러나 for문을으로 배열을 초기화하려면, 저장하려는 값에 일정한 규칙이 있어야만 가능하기 때문에 자바에서는 다음과 같이 배열을 간단히 초기화 할 수 있는 방법을 제공한다.

``` java
int[] score = new int[] { 50, 60, 70, 80, 90 };	// 배열의 생성과 초기화를 동시에
```

저장할 값들을 괄호[] 안에 쉼표로 구분해서 나열하면 되며, 괄호[] 안의 값의 개수에 의해 배열의 길이가 자동으로 결정되기 때문에 괄호[] 안에 배열의 길이는 안적어도 된다.

``` java
int[] score = new int[] { 50, 60, 70, 80, 90 };
int[] score = { 50, 60, 70, 80, 90 };	// new int[]를 생략할 수 있음
```

심지어는 위와 같이 'new 타입[]'을 생략하여 코드를 더 간단히 할 수도 있다. 다만 다음과 같이 배열의 선언과 생성을 따로 하는 경우에는 생략할 수 없다.

``` java
int[] score;
score = new int[] { 50, 60, 70, 80, 90 };	// OK
score = { 50, 60, 70 80, 90 };	// 에러. new int[]를 생략할 수 없음
```

또 다른 예로, 아래와 같이 매개변수 int배열을 받는 `add`메소드가 정의되어 있고, 이 메소드를 호출해야할 경우 역시 'new 타입[]'을 생략할 수 없다.

``` java
int add(int[] arr) { /* 내용 생략 */ }	// add 메소드

int result = add(new int[] { 100, 90, 80, 70, 60 });	// OK
int result = add({ 100, 90, 80, 70, 60 });	// 에러. new int[]를 생략할 수 없음
```

그리고 괄호[] 안에 아무 것도 넣지 않으면, 길이가 0인 배열이 생성된다. 참조변수의 기본 값은 `null`이지만, 배열을 가르키는 참조변수는 `null` 대신 길이가 0인 배열로 초기화하기도 한다. 아래의 세 문장은 모두 길이가 0인 배열을 생성한다.

``` java
int[] score = new int[0];	// 길이가 0인 배열
int[] score = new int[];	// 길이가 0인 배열
int[] score = {};			// 길이가 0인 배열, new int[]가 생략됨
```

### 배열의 출력

배열을 초기화할 때 for문을 사용하듯이, 배열에 저장된 값을 확인할 때도 다음과 같이 for문을 사용하면 된다.

``` java
int[] iArr = { 100, 90, 80, 70, 60 };

// 배열의 요소를 순서대로 하나씩 출력
for (int i = 0; i < iArr.length; i++) {
	System.out.println(iArr[i]);
}
```

`println`메소드는 출력 후에 줄 바꿈을 하므로, 여러 줄에 출력되어 보기 불편할 때가 있다. 그럴 때는 다음과 같이 출력 후에 줄 바꿈을 하지 않는 `print`메소드를 사용하면 된다.

``` java
int[] iArr = { 100, 90, 80, 70, 60 };

for (int i = 0; i < iArr.length; i++) {
	System.out.print(iArr[i] + ",");	// 각 요소간의 구별을 위해 쉼표를 넣는다.
}
System.out.println();	// 다음 출력이 바로 이어지지 않도록 줄 바꿈을 한다.
```

더 간단한 방법은 `Arrays.toStirng(배열이름)`메소드를 사용하는 것이다. 이 메소드는 배열의 모든 요소를 '[첫번째 요소, 두번째 요소, ...]'와 같은 형식의 문자열로 만들어서 반환한다.

``` java
int[] iArr = { 100, 90, 80, 70, 60 };
// 배열 iArr의 모든 요소를 출력한다. [100, 90, 80, 70, 60]이 출력된다.
System.out.println(Arrays.toString(iArr));
```

만일 `iArr`의 값을 바로 출력하면 **'타입@주소'** 의 형식으로 출력된다. '[I'는 1차원 int배열이라는 의미이고, '@'뒤에 나오는 16진수는 배열의 주소인데 실제 주소가 이닌 내부 주소이다.

``` java
// 배열을 가리키는 참조변수 iArr의 값을 출력한다.
System.out.println(iArr);	// [I@1c4af82c]와 같은 형식의 문자열이 출력된다.
```

예외적으로 char배열은 `println`메소드로 출력하면 각 요소가 구분자없이 그대로 출력되는데, 이것은 `println`메소드가 char배열일 때만 이렇게 동작하도록 작성되었기 때문이다.

``` java
char[] chArr = { 'a', 'b', 'c', 'd' };
System.out.println(chArr);	// abcd가 출력된다. 
```

예제 5-2 / ch5 / ArrayEx2.java
``` java
import java.util.Arrays;

public class ArrayEx2 {

	public static void main(String[] args) {
		int[] iArr1 = new int[10];
		int[] iArr2 = new int[10];
		int[] iArr3 = new int[] { 100, 95, 80, 70, 60 };
//		int[] iArr3 = { 100, 95, 80, 70, 60 };
		char[] chArr = { 'a', 'b', 'c', 'd' };
		
		for (int i = 0; i < iArr1.length; i++) {
			iArr1[i] = i + 1;	// 1~10의 숫자를 순서대로 배열에 넣는다.
		}
		
		for (int i = 0; i < iArr2.length; i++) {
			iArr2[i] = (int)(Math.random() * 10) + 1;	// 1~10의 값을 배열에 저장
		}
		
		// 배열에 저장된 값들을 출력한다.
		for (int i = 0; i < iArr1.length; i++) {
			System.out.print(iArr1[i] + ",");
		}
		System.out.println();
		System.out.println(Arrays.toString(iArr2));
		System.out.println(Arrays.toString(iArr3));
		System.out.println(Arrays.toString(chArr));
		System.out.println(iArr3);
		System.out.println(chArr);
	}

}
```

```
1,2,3,4,5,6,7,8,9,10,
[9, 4, 8, 9, 2, 10, 5, 9, 8, 9]
[100, 95, 80, 70, 60]
[a, b, c, d]
[I@1c4af82c	← 실행할 때 마다 달라질 수 있다.
abcd
```

</br>

## 1.5 배열의 복사

배열은 한번 생성하면 그 길이를 변경할 수 없기 때문에 더 많은 저장공간이 필요하다면 보다 큰 배열을 새로 만들고 이전 배열로부터 내용을 복사해야한다.

배열을 복사하는 방법은 두 가지가 있는데, 먼저 for문을 이용해서 배열을 복사하는 방법은 다음과 같다.

``` java
int[] arr = new int[5];
	...
int[] tmp = new int[arr.length * 2];	// 기존 배열보다 길이가 2배인 배열 생성

for (int i = 0; i < arr.length; i++) {
	tmp[i] = arr[i];	// arr[i]의 값을 tmp[i]에 저장
}
arr = tmp;	// 참조변수 arr이 새로운 배열을 가르키게 한다.
```

이러한 작업들은 꽤나 비용이 많이 들기 때문에, 처음부터 배열의 길이를 넉넉하게 잡아줘서 새로 배열을 생성해야하는 상황이 가능한 적게 발생하도록 해야 한다. 그렇다고 배열의 길이를 너무 크게 잡으면 메모리를 낭비하기 되므로, 위의 코드에서처럼 기존의 2배정도의 길이로 배열을 생성하는 것이 좋다.

예제 5-3 / ch5 / ArrayEx3.java
``` java
public class ArrayEx3 {

	public static void main(String[] args) {
		int[] arr = new int[5];
		
		// 배열 arr에 1~5를 저장한다.
		for (int i = 0; i < arr.length; i++) {
			arr[i] = i + 1; 
		}
		
		System.out.println("[변경전]");
		System.out.println("arr.length: " + arr.length);
		for (int i = 0; i < arr.length; i++) {
			System.out.println("arr[" + i + "]: " + arr[i]);
		}
		
		int[] tmp = new int[arr.length * 2];
		
		// 배열 arr에 저장된 값들을 배열 tmp에 복사한다.
		for (int i = 0; i < arr.length; i++) {
			tmp[i]= arr[i]; 
		}
		
		arr = tmp;	// tmp에 저장된 값을 arr에 저장한다.
		
		System.out.println("[변경후]");
		System.out.println("arr.length: " + arr.length);
		for (int i = 0; i < arr.length; i++) {
			System.out.println("arr[" + i + "]: " + arr[i]);
		}
	}

}
```

```
[변경전]
arr.length: 5
arr[0]: 1
arr[1]: 2
arr[2]: 3
arr[3]: 4
arr[4]: 5
[변경후]
arr.length: 10
arr[0]: 1
arr[1]: 2
arr[2]: 3
arr[3]: 4
arr[4]: 5
arr[5]: 0
arr[6]: 0
arr[7]: 0
arr[8]: 0
arr[9]: 0
```

### System.arraycooy()를 이용한 배열의 복사

for문 대신 System클래스의 `arraycopy()`를 사용하면 보다 간단하고 빠르게 배열을 복사할 수 있다. for문은 배열의 요소 하나하나에 접근해서 복사하지만, `arraycopy()`는 지정된 범위의 값들을 한 번에 통째로 복사한다. 각 요소들이 연속적으로 저장되어 있다는 배열의 특성 때문에 이렇게 처리하는 것이 가능하다.

> **배열의 복사는 for문보다 System.arraycopy()를 사용하는 것이 효율적이다.**

이전 예제에서 배열의 복사에 사용된 for문을 `arraycopy()`로 바꾸면 다음과 같다.

``` java
for (int i = 0; i < num.length; i++) { newNum[i] = num[i]; }

System.arraycopy(num, 0, newNum, 0, num.length);
```

`arraycopy()`를 호출할 때는 어느 배열의 몇 번째 요소에서 어느 배열로 몇 번째 요소로 몇 개의 값을 복사할 것인지 지정해줘야 하는데, 다음과 같이 생각하면 이해하기 쉽다.

![image](https://ifh.cc/g/WpTP4J.png)

배열 `num`의 내용을 배열 `newNum`으로, 배열 `num`의 첫 번째 요소(`num[0]`)부터 시작해서 `num.length`개의 데이터를 `newNum`의 첫 번째 요소(`newNum[0]`)에 복사한다.

이 때 복사하려는 배열의 위치가 적절하지 못하여 복사하려는 내용보다 여유 공간이 적으면 에러(ArrayIndexOutOfBoundsException)가 발생한다.

예제 5-4 / ch5 / ArrayEx5.java
``` java
public class ArrayEx4 {

	public static void main(String[] args) {
		char[] abc = { 'A', 'B', 'C', 'D' };
		char[] num = { '0', '1', '2', '3', '4', '5', '6', '7', '8','9' };
		System.out.println(abc);
		System.out.println(num);
		
		// 배열 abc와 num을 붙여서 하나의 배열(result)로 만든다.
		char[] result = new char[abc.length + num.length];
		System.arraycopy(abc, 0, result, 0, abc.length);
		System.arraycopy(num, 0, result, abc.length, num.length);
		System.out.println(result);
		
		// 배열 abc을 배열 num의 첫 번째 위치부터 배열 abc의 길이만큼 복사
		System.arraycopy(abc, 0, num, 0, abc.length);
		System.out.println(num);
		
		// number의 인덱스 6 위치에 3개를 복사
		System.arraycopy(abc, 0, num, 6, 3);
		System.out.println(num);
	}

}
```

```
ABCD
0123456789
ABCD0123456789
ABCD456789
ABCD45ABC9
```

다른 배열과 달리 char배열은 for문을 사용하지 않고도 `print()`나 `println()`으로 배열에 저장된 모든 문자를 출력할 수 있다.

</br>

## 배열의 활용

예제 5-5 / ch5 / ArrayEx5.java
``` java
public class ArrayEx5 {

	public static void main(String[] args) {
		int sum = 0;	// 총점을 저장하기 위한 변수
		float average = 0f;	// 평균을 저장하기 위한 변수
		
		int[] score = { 100, 88, 100, 100, 90 };
		
		for (int i = 0; i < score.length; i++) {
			sum += score[i];	// 반복문을 이용해서 배열에 저장되어 있는 값들을 모두 더한다.
		}
		average = sum / (float)score.length;	// 계산결과를 float로 얻기 위해서 형변환
		
		System.out.println("총점 : " + sum);
		System.out.println("평균 : " + average);
	}

}
```

```
총점 : 478
평균 : 95.6
```

for문을 이용해서 배열에 저장된 값을 모두 더한 결과를 배열의 개수로 나누어서 평균을 구하는 예제이다. 평균을 구하기 위해 전체 합을 배열의 길이인 `score.length`로 나누었다.

이 때 int와 int 간의 연산은 int를 결과를 얻기 때문에 정확한 평균을 얻지 못하므로 `score.length`를 float로 변환하여 나눗셈을 하였다.

478 / 5 → **95**
478 / (float)5 → 478 / 5.0f → 478.0f / 5.0f → **95.6f**

예제 5-6 / ch5 / ArrayEx6.java
``` java
public class ArrayEx6 {

	public static void main(String[] args) {
		int[] score = { 79, 88, 91, 33, 100, 55, 95 };
		
		int max = score[0];	// 배열의 첫 번재 값으로 최대값을 초기화한다.
		int min = score[0];	// 배열의 첫 번재 값으로 최소값을 초기화한다.
		
		for (int i = 0; i < score.length; i++) {
			if (score[i] > max) {
				max = score[i];
			} else if (score[i] < min ) {
				min = score[i];
			}
		}	// end of for
		
		System.out.println("최대값 : " + max);
		System.out.println("최소값 : " + min);
	}

}
```

```
최대값 : 100
최소값 : 33
```

배열에 저장된 값 중에서 최대값과 최소값을 구하는 예제이다. 배열의 첫 번째 요소 `score[0]`의 값으로 최대값을 의미하는 변수 `max`와 최소값을 의미하는 변수 `min`을 초기화 하였다.

그 다음 반복문을 통해서 배열의 두 번째 요소 `socre[1]`부터 `max`와 비교하기 시작한다. 만일 배열에 담긴 값이 `max`에 저장된 값보다 크다면, 이 값을 `max`에 저장한다.

이런 식으로 배열의 마지막 요소까지 비교하고 나면 `max`에는 배열에 담긴 값 중에서 최대값이 저장된다. 최소값 `min`도 같은 방식으로 얻을 수 있다.

예제 5-7 / ch5 / ArrayEx7.java
``` java
public class ArrayEx7 {

	public static void main(String[] args) {
		int[] numArr = new int[10];
		
		for (int i = 0; i < numArr.length; i++) {
			numArr[i] = i;	// 배열을 0~9의 숫자로 초기화한다.
			System.out.print(numArr[i]);
		}
		System.out.println();
		
		for (int i = 0; i < 100; i++) {
			int n = (int)(Math.random() * 10);	// 0~9중의 한 값을 임의로 얻는다.
			int tmp = numArr[0];
			numArr[0] = numArr[n];
			numArr[n] = tmp;
		}
		
		for (int i = 0; i < numArr.length; i++) {
			System.out.print(numArr[i]);
		}
	}	// main의 끝

}
```

```
0123456789
6453871290
```

길이가 10인 배열 `numArr`을 생성하고 0~9의 숫자로 차례대로 초기화화여 출력한다. 그 다음 `random()`을 이용해서 배열의 임의의 위치에 있는 값과 배열의 첫 번째 요소인 `numArr[0]`의 값을 교환하는 일을 100번 반복한다.

만일 `random()`을 통해 얻은 값 `n`이 3이라면, 왼쪽의 코드는 오른쪽처럼 될 것이다.

![image](https://ifh.cc/g/LszZHx.png)

오른쪽의 코드는 `numArr[0]`과 `numArr[3]`에 저장된 값을 서로 바꾸는 일을 한다. 두 변수에 저장된 값을 서로 바꾸려면, 별도의 저장공간이 하나 더 필요하다.

예제 5-8 / ch5 / ArrayEx8.java
``` java
public class ArrayEx8 {

	public static void main(String[] args) {
		int[] ball = new int[45];	//  45개의 정수값을 저장하기 위한 배열 생성
		
		// 배열의 각 요소에 1~45의 값을 저장한다.
		for (int i = 0; i < ball.length; i++) {
			ball[i] = i + 1;	// ball[0]에 1이 저장된다.
		}
		
		int temp = 0;	// 두 값을 바꾸는데 사용할 임시변수
		int j = 0;	// 임의의 값을 얻어서 저장할 변수
		
		// 배열의 i번째 요소와 임의의 요소에 저장된 값을 서로 바꿔서 값을 섞는다.
		// 0번째부터 5번째 요소까지 모두 6개만 바꾼다.
		for (int i = 0; i < 6; i++) {
			j= (int)(Math.random() * 45);	// 0~44범위의 임의의 값을 얻는다.
			temp = ball[i];
			ball[i] = ball[j];
			ball[j] = temp;
		}
		
		// 배열 ball의 앞에서부터 6개의 요소를 출력한다.
		for (int i = 0; i < 6; i++) {
			System.out.printf("ball[%d] = %d%n", i, ball[i]);
		}
	}

}
```

```
ball[0] = 9
ball[1] = 35
ball[2] = 6
ball[3] = 40
ball[4] = 45
ball[5] = 15
```

로또번호를 생성하는 예제이다. 길이가 45인 배열에 1부터 45까지의 값을 담은 다음 반복문을 이용해서 배열의 인덱스가 `i`인 값(`ball[i]`)과 `random()`에 의해서 결정된 임의의 위치에 있는 값과 자리를 바꾸는 것을 6번 반복한다. 이것은 마치 1부터 45까지의 번호가 쓰인 카드를 잘 썩은 다음 맨 위의 6장을 꺼내는 것과 같다고 할 수 있다.

45개의 요소 중에서 앞에 6개의 요소만 임의의 위치에 있는 요소와 자리를 바꾸면 된다.

``` java
// 배열의 인덱스가 i인 요소와 임의이 요소에 저장된 값을 서로 바꿔서 값을 섞는다.
// 0번째부터 5번째 요소까지 모두 6개만 바꾼다.
for (int i = 0; i < 6; i++) {
	j = (int)(Math.random() * 45);	// 0~44범위의 임의의 값을 얻는다.
	temp = ball[i];
	ball[i] = ball[j];
	ball[j] = temp;
}
```

### 임의의 값으로 배열 채우기

배열을 연속적인 범위의 임의의 값으로 채우는 것은 다음과 같이 `random()`만 사용하면 쉽게 할 수 있다.

``` java
for (i = 0; i < arr.length; i++) {
	arr[i] = (int)(Math.random() * 5);	// 0~4범위의 임의의 값을 저장
}
```

그러면, 불연속적인 범위의 값들로 배열을 채우는 것은 배열을 하나 더 사용하면 된다. 먼저 배열 `code`에 불연속적인 값들을 담고, 임의로 선택된 index에 저장된 값으로 배열 `arr`의 요소들을 하나씩 채우면 되는 것이다. 저장된 값에 상관없이 배열의 index는 항상 연속적이기 때문이다.

예제 5-9 / ch5 / ArrayEx9.java
``` java
import java.util.Arrays;

public class ArrayEx9 {

	public static void main(String[] args) {
		int[] code = { -4, -1, 3, 6, 11 };	// 불연속적인 값들로 구성된 배열
		int[] arr = new int[10];
		
		for (int i = 0; i < arr.length; i++) {
			int tmp = (int)(Math.random() * code.length);
			arr[i] = code[tmp];
		}
		
		System.out.println(Arrays.toString(arr));
	}	// main의 끝

}
```

```
[-1, 6, 6, 6, -4, -4, 6, 11, 11, 3]	← 실행할 때마다 달라진다.
```

배열 `code`의 길이가 5이므로 `code.length`의 값은 5가 된다. 따라서 변수 `tmp`에는 0~4범위에 속한 임의의 정수가 저장되는데, 이 범위의 배열 `code`의 index의 범위와 일치한다.

``` java
	int tmp = (int)(Math.random() * code.length);
→	int tmp = (int)(Math.random() * 5);	// tmp에 0, 1, 2, 3, 4중의 하나가 저장된다.
```

만일 `i`의 값이 0이고, `tmp`의 값이 4라면 다음과 같이 계산되어 `arr[0]`에는 `code[4]`의 값인 11이 저장된다.

``` java
	arr[i] = code[tmp];
→	arr[0] = code[4];	// code[4]는 배열 code의 5번째 요소이므로 11이다.
→	arr[0] = 11;	// arr[0]에 11이 저장된다.
```

예제 5-10 / ch5 / ArrayEx10.java
``` java
public class ArrayEx10 {

	public static void main(String[] args) {
		int[] numArr = new int[10];
		
		for (int i = 0; i < numArr.length; i++) {
			System.out.print(numArr[i]= (int)(Math.random() * 10) );
		}
		System.out.println();
		
		for (int i = 0; i < numArr.length - 1; i++) {
			boolean changed = false;	// 줄바꿈이 발생했는지를 체크한다.
			
			for (int j = 0; j < numArr.length - 1- i; j++) {
				if (numArr[j] > numArr[j + 1]) {	// 옆의 값이 작으면 서로 바꾼다.
					int temp = numArr[j];
					numArr[j] = numArr[j + 1];
					numArr[j + 1] = temp;
					changed = true;	// 자리바꿈이 발생했으니 changed를 true로
				}
			}	// end for j
			
			if (!changed) break;	// 자리바꿈이 없으면 반복문을 벗어난다.
			
			for (int k = 0; k < numArr.length; k++)
				System.out.print(numArr[k]);	// 정렬된 결과를 출력한다.
			System.out.println();
		}	// end 
	}	// main의 끝

}
```

```
9151421120
1514211209
1142112059
1121120459
1111202459
1111022459
1110122459
1101122459
1011122459
0111122459
```

길이가 10인 배열에 0고 9 사이에 임의의 값으로 채운 다음, 버블정렬 알고리즘을 통해서 크기순으로 정렬하는 예제이다. 이 알고리즘의 정렬방법은 아주 간단하다. 배열의 길이가 n일 때, 배열의 첫 번째부터 n-1까지의 요소에 대해, 근접한 값과 크기를 비교하여 자리바꿈을 반복하는 것이다.

``` java
for (int j = 0; j < numArr.length; j++) {
	// numArr[j]와 바로 옆의 요소 numArr[j + 1]을 비교한다.
	if (numArr[j] > numArr[j + 1]) {	// 왼쪽의 값이 크면 서로 바꾼다.
		int tmp = numArr[j];
		numArr[j] = numArr[j + 1];
		numArr[j + 1] = tmp;
	}
}
```

예를 들어 다음과 같이 길이가 5인 int배열이 있을 때, 첫 번째와 두 번째 요소의 값을 비교해서 왼쪽 요소의 값이 크면 두 값의 위치를 바꾸고, 그렇지 않으면 바꾸지 않는다.

![image](https://ifh.cc/g/2hZxPp.png)

위의 그림에서 왼쪽의 값이 크므로 두 값의 자리를 바꾼다.

![image](https://ifh.cc/g/FVJrvK.png)

두 번째 비교에서는 왼족의 값이 작으므로 두 값의 자리를 바꾸지 않는다. 이러한 작업을 배열의 끝에 도달할 때까지 반복하면 배열에서 제일 큰 값이 배열의 마지막 값이 된다.

![image](https://ifh.cc/g/0O4QPo.png)

비교횟수는 모두 4번이며, 이 값은 배열의 길이보다 1이 작은 값(`numArr.length - 1`)이다. 즉, 배열의 길이가 5라면, 4번만 비교하면 된다는 뜻이다. 나머지 값들이 아직 정렬되지 않았으므로 비교작업을 배열의 첫 번째 요소부터 다시 해야 한다.

그러나 처음과 달리 이번엔 세 번만 비교하면 된다. 배열의 마지막 요소는 최대값이므로 비교할 필요가 없기 때문이다.

![image](https://ifh.cc/g/344FXq.png)

이처럼 비교작업(아래의 for문)을 반복할수록 비교해야하는 범위는 하나씩 줄어든다. 그래서 원래는 배열의 길이에서 1이 작은 `numArr.length - 1`번을 비교해야 하는데, 매 반복마다 비교횟수가 1씩 줄어들기 때문에 바깥쪽 for문의 제어변수 `i`를 빼주는 것이다.

``` java
for (int j = 0; j < numArr.length; j++) {
	// numArr[j]와 바로 옆의 요소 numArr[j + 1]을 비교한다.
	if (numArr[j] > numArr[j + 1]) {	// 왼쪽의 값이 크면 서로 바꾼다.
		int tmp = numArr[j];
		numArr[j] = numArr[j + 1];
		numArr[j + 1] = tmp;
	}
}
```

위의 작업이 한번 수행되는 것만으로는 정렬이 되지 않기 때문에 비교작업(위의 for문)을 모두 4번, 즉, '배열의 길이 - 1'번 만큼 반복해서 비교해야 한다.

그래서 바깥쪽 for문의 조건식이 `numArr.length - 1`이어야 하는 것이다.

``` java
for (int i = 0; i < numArr.length; i++) {
	changed = false;	// 매 반복마다 changed를 false로 초기화한다.

	for (int j = 0; j < numArr.legnth; j++) {
		if (numArr[j] > numArr[j + 1]) {	// 옆의 값이 작으면 서로 바꾼다.
			int tmp = numArr[j];
			numArr[j] = numArr[j + 1];
			numArr[j + 1] = tmp;

			changed = true;	// 자리바꿈이 발생했으니 changed를 true로 바꾼다.
		}
	}	// end for j

	if (!changed) break;	// 자리바꿈이 없으면 반복문을 벗어난다.

	for (int k = 0; k < numArr.length; k++) {
		System.out.print(numArr[k]);	// 정렬된 결과를 출력한다.
	}
	System.out.println();
}	// end of for i
```

보다 효율적인 작업을 위해 `changed`라는 boolean형 변수를 두어서 자리바꿈이 없으면 break문을 수행하여 정렬을 미치도록 했다. 자리바꿈이 없다는 것은 정렬이 완료되었음을 뜻하기 때문이다.

이 정렬 방법을 '버블 정렬(bubble sor)'라고 하는데, 비효율적이지만 가장 간단하다.

``` java
System.out.print(numArr[i] = (int)(Math.random() * 10));
```

그리고 위의 문장은 아래의 두 문장을 하나로 합친 것이다.

``` java
numArr[i] = (int)(Math.random() * 10);
System.out.print(numArr[i]);
```

예제 5-11 / ch5 / ArrayEx11.java
``` java
public class ArrayEx11 {

	public static void main(String[] args) {
		int[] numArr = new int[10];
		int[] counter = new int[10];
		
		for (int i = 0; i < numArr.length; i++) {
			numArr[i] = (int)(Math.random() * 10);	// 0~9의 임의의 수를 배열에 저장
			System.out.print(numArr[i]);
		}
		System.out.println();
		
		for (int i = 0; i < numArr.length; i++) {
			counter[numArr[i]]++;
		}
		
		for (int i = 0; i < numArr.length; i++) {
			System.out.println(i + "의 개수 : " + counter[i]);
		}
	}	// main의 끝

}
```

```
5707149805
0의 개수 : 2
1의 개수 : 1
2의 개수 : 0
3의 개수 : 0
4의 개수 : 1
5의 개수 : 2
6의 개수 : 0
7의 개수 : 2
8의 개수 : 1
9의 개수 : 1
```

길이가 10인 배열을 만들고 0과 9 사이의 임의의 값으로 초기화 한다. 그리고 이 배열에 저장된 각 숫자가 몇 번 반복해서 나타나는지를 세어서 배열 `counter`에 담은 다음 화면에 출력한다.

``` java
for (int i = 0; i < numArr.length; i++) {
	counter[numArr[i]]++;
}
```

``` java
	counter[numArr[i]]++;	// i의 값이 0인 경우를 가정하면,
→	counter[numArr[0]]++;	// numArr[0]의 값은 4이다.
→	counter[4]++;			// counter[4]의 값을 1증가시킨다.
```

![image](https://ifh.cc/g/CBtVRv.png)

배열 `counter`에서, 배열 `numArr`에 저장된 값과 일치하는 인덱스와 요소에 저장된 값을 1증가시킨다. 위의 그림에서는 `numArr[0]`에 4가 저장되어있으므로 배열 `counter`의 인덱스가 4인 요소에 저장된 값이 0에서 1로 증가되었다. 이 과정이 반복되고 나면, 배열 `counter`의 각 요소에는 해당 인덱스의 값이 몇 번 나타났는지 알 수 있는 값이 저장된다.