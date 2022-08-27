Chapter 4. 조건문과 반복문

# 조건문 - if, switch

조건문은 조건식과 문장을 포함하는 블럭{}으로 구성되어 있으며, 조건식의 연산결과에 따라 실행할 문장이 달라져서 프로글매의 실행흐름을 변경할 수 있다.

조건문은 `if`문과 `switch`문, 두 가지가 있으며 주로 `if`문이 많이 사용된다. 처리할 경우의 수가 많을 때는 `if`문보다 `switch`문이 효율적이지만, `switch`문은 `if`문보다 제약이 많다.

</br>

## 1.1 if문

`if`문은 가장 기본적인 조건문이며, 다음과 같이 '조건식'과 '괄호{}'로 이루어져 있다. `if`의 뜻이 '만일 ~이라면...'이므로 **'만일(if) 조건식이 참(true)이면 괄호{} 안의 문장들을 수행하라.'** 라는 의미이다.

``` java
if (조건식) {
    // 조건식이 참(true)일 때 수행될 문장들을 적는다.
}
```

### 조건식

`if`문에 사용되는 조건식은 일반적으로 비교연산자와 논리연산자로 구성된다.

![image](https://ifh.cc/g/20dQ7m.png)

조건식을 작성할 때 실수하기 쉬운 것이, 등가비교 연산자 `==`대신 대입 연산자 `=`를 사용하는 것이다.

예제 4-1 / ch4 / FlowEx1.java
``` java
public class FlowEx1 {

	public static void main(String[] args) {
		int x = 0;
		System.out.printf("x = %d 일 때, 참인 것은%n", x);
		
		if (x == 0) System.out.println("x == 0");
		if (x != 0) System.out.println("x != 0");
		if (!(x == 0)) System.out.println("!(x == 0)");
		if (!(x != 0)) System.out.println("!(x != 0)");
		
		x = 1;
		System.out.printf("x = %d 일 때, 참인 것은%n", x);
		
		if (x == 0) System.out.println("x == 0");
		if (x != 0) System.out.println("x != 0");
		if (!(x == 0)) System.out.println("!(x == 0)");
		if (!(x != 0)) System.out.println("!(x != 0)");
	}

}
```

```
x = 0 일 때, 참인 것은
x == 0
!(x != 0)
x = 1 일 때, 참인 것은
x != 0
!(x == 0)
```

### 블럭

괄호{}를 이용해서 여러 문장을 하나의 단위로 묶을 수 있는데, 이것을 '블럭(block)'이라고 한다. 블럭은 `{`로 시작해서, `}` 다음에 문장의 끝을 의미하는 `;`을 붙이지 않는다.

블럭 내의 문장들은 탭(tab)으로 들여쓰기(indentation)를 해서 블럭 안에 속한 문장이라는 것을 알기 쉽게 해주는 것이 좋다.

![image](https://ifh.cc/g/G7aggL.png)

블럭의 시작을 의미하는 `{`의 위치는 아래와 같이 두 가지 스탕리이 있는데, 각 스타일마다 장단점이 있으므로 본인의 취향에 맞는 것으로 선택해서 사용하면 된다. 왼쪽이 스타일은 라인의 수가 짧아진다는 장점이, 오른쪽의 스타일은 블러그이 시작과 끝을 찾기 쉽다는 장점이 있다.

![image](https://ifh.cc/g/qMP4V3.png)

블럭 안에는 보통 여러 문장을 넣지만, 한 문장만 넣거나 아무런 문장도 넣지 않을 수도 있다. 만일 블럭 내의 문장이 하나뿐 일 때는 아래와 같이 괄호{}를 생략할 수 있다.

``` java
if (score > 60)
    System.out.println("합격입니다.");
```

또는 아래와 같이 한 줄로 쓸 수도 있다.

``` java
if (score > 60) System.out.println("합격입니다.");
```

이처럼 블럭 내의 문장이 하나뿐인 경우 괄호{}를 생략할 수 있지만 가능하면 생략하지 않고 사용하는 것이 바람직하다. 나중에 새로운 문장들이 추가되면 괄호{}로 문장들을 감싸 주어야 하는데, 이 때 괄호{}를 추가하는 것을 잊기 쉽기 때문이다.

예제 4-2 / ch4 / FlowEx2.java
``` java
import java.util.Scanner;

public class FlowEx2 {

	public static void main(String[] args) {
		int input;
		
		System.out.print("숫자를 하나 입력하세요.>");
		
		Scanner scanner = new Scanner(System.in);
		String tmp = scanner.nextLine();	// 화면을 통해 입력받은 내용을 tmp에 저장
		input = Integer.parseInt(tmp);
		
		if (input == 0) {
			System.out.println("입력하신 숫자는 0입니다.");
		}
		
		if (input != 0)
			System.out.println("입력하신 숫자는 0이 아닙니다.");
			System.out.printf("입력하신 숫자는 %d입니다.", input);
	}	// main의 끝

}
```

```
숫자를 하나 입력하세요.>3
입력하신 숫자는 0이 아닙니다.
입력하신 숫자는 3입니다.
```

```
숫자를 하나 입력하세요.>0
입력하신 숫자는 0입니다.
입력하신 숫자는 0입니다.
```

두 번째 `if`문은 괄호{}를 생략했기 때문에, 조건식 바로 다음에 오는 하나의 문장만 `if`문에 속하게 된다. 그래서 실행결과를 보면 세 번째 출력문이 항상 출력된다.

``` java
if (input != 0)
    System.out.println("입력하신 숫자는 0이 아닙니다.");
    System.out.printf("입력하신 숫자는 %d입니다.", input);  // if문 밖의 문장
```

만일 두 문장 모두 `if`문에 속하게 하려면 괄호{}로 묶으면 된다.

```
숫자를 하나 입력하세요.>0
입력하신 숫자는 0입니다.
```

</br>

## 1.2 if-else문

`else`의 뜻이 '그 밖의 다른'이므로 조건식의 결과가 참이 아닐 때, 즉 거짓일 때 `else`블럭의 문장을 수행하라는 뜻이다.

``` java
if (조건식) {
    // 조건식이 참(true)일 때 수행될 문장들을 적는다.
} else {
    // 조건식이 거짓(false)일 때 수행될 문장들을 적는다.
}
```

조건식의 결과에 따라 이 두 개의 블럭{} 중 어느 한 블럭{}의 내용이 수행되고 전체 `if`문을 벗어나게 된다. 두 블럭{}의 내용이 모두 수행되거나, 모두 수행되지 않는 경우는 있을 수 없다. 아래 왼쪽의 두 갱의 `if`문을 `if-else`문으로 바꾸면 오른쪽과 같다.

![image](https://ifh.cc/g/WopkPq.png)

왼쪽 코드의 두 조건식은 어느 한 쪽이 참이면 다른 한 쪽이 거짓인 상반된 관계에 있기 때문에 오른 쪽과 같이 `if-else`문으로 바꿀 수 있는 것이지. 두 개의 `if`문을 항상 `if-else`문으로 바꿀 수 있는 것은 아니다.

그리고 왼쪽의 코드는 두 개의 조건식을 계산해야하지만, `if-else`문을 사용한 오른쪽의 코드는 하나의 조건식만 계산하면 되므로 더 효율적이고 간단하다.

예제 4-3 / ch4 / FlowEx3.java
``` java
import java.util.Scanner;

public class FlowEx3 {

	public static void main(String[] args) {
		System.out.print("숫자를 하나 입력하세요.>");
		
		Scanner scanner = new Scanner(System.in);
		int input = scanner.nextInt();	// 화면을 통해 입력받은 숫자를 input에 저장
		
		if (input == 0) {
			System.out.println("입력하신 숫자는 0입니다.");
		} else {	// input != 0인 경우
			System.out.println("입력하신 숫자는 0이 아닙니다.");
		}
	}	// main의 끝

}
```

```
숫자를 하나 입력하세요.>5
입력하신 숫자는 0이 아닙니다.
```

```
숫자를 하나 입력하세요.>0
입력하신 숫자는 0입니다.
```

`if-else`문 역시 블럭 내의 문장이 하나뿐인 경우 아래와 같이 괄호{}를 생략할 수 있다.

``` java
if (input == 0)
    System.out.println("입력하신 숫자는 0입니다.");
else 
    System.out.println("입력하신 숫자는 0이 아닙니다.");
```

</br>

## 1.3 if-else if문

처리해야할 경우의 수가 셋 이상인 경우에는 한 문장에 여러 개의 조건식을 쑬 수 있는 `if-else if`문을 사용하면 된다.

``` java
if (조건식1) {
    // 조건식1의 연산결과가 참일 때 수행될 문장들을 적는다.
} else if (조건식2) {
    // 조건식2의 연산결과가 참일 때 수행될 문장들을 적는다.
} else if (조건식3) {   // 여러 개의 else if를 사용할 수 있다.
    // 조건식3의 연산결과가 참일 때 수행될 문장들을 적는다.
} else {    // 마지막에는 보통 else블럭으로 끝나며, else블럭은 생략가능하다.
    // 위의 어느 조건식도 만족하지 않을 때 수행될 문장들을 적는다.
}
```

첫 번째 조건식부터 순서대로 평가해서 겨로가가 참인 조건식을 만나면, 해당 블럭{}만 수행하고 `if-else if`문 전체를 벗어난다.

만일 결과가 참인 조건식이 하나도 없으면, 마지막에 있는 `else`블럭의 문장들이 수행된다. 그리고 `else`블럭은 생략이 가능하다. `else`블럭이 생략되었을 때는 `if-else if`문의 어떤 블럭도 수행되지 않을 수 있다.

예제 4-4 / ch4 / FlowEx4.java
``` java
import java.util.Scanner;

public class FlowEx4 {

	public static void main(String[] args) {
		int score = 0;	// 점수를 저장하기 위한 변수
		char grade = ' ';	// 학점을 저장하기 위한 변수, 공백으로 초기화한다.
		
		System.out.print("점수를 입력하세요.>");
		Scanner scanner = new Scanner(System.in);
		score = scanner.nextInt();	// 화면을 통해 입력받은 숫자를 score에 저장
		
		if (score >= 90) {	// score가 90점 보다 같거나 크면 A학점
			grade = 'A';
		} else if (score >= 80) {	// score가 80점 보다 같거나 크면 B학점
			grade = 'B';
		} else if (score >= 70) {	// score가 70점 보다 같거나 크면 C학점
			grade = 'C';
		} else {	// 나머지는 D학점
			grade = 'D';
		}
		System.out.println("당신의 학점은 " + grade + "입니다.");
	}

}
```

```
점수를 입력하세요.>70
당신의 학점은 C입니다.
```

```
점수를 입력하세요.>63
당신의 학점은 D입니다.
```

점수를 입력하면, 그에 해당하는 학점을 출력하는 간단한 예제이다. 여기서 한 가지 눈여겨봐야할 것은 두 번째와 세 번째 조건식이다.

``` java
if (score >= 90) {
			grade = 'A';
} else if (80 <= score && score < 90) {	// 80 <= score < 90
    grade = 'B';
} else if (70 <= score && score < 80) {	// 70 <= score < 80
    grade = 'C';
} else {	// score < 70
    grade = 'D';
}
```

점수가 90점 미만이고, 80점 이상인 사람에게 'B'학점을 주는 조건이라면, 위의 코드에서처럼 조건식이 `80 <= score && < 90`이 되어야 하는데 두 번째 조건식을 `score >= 90`이라고 쓸 수 있는 것은 첫 번째 조건식인 `score >= 90`이 거짓이기 때문이다. `score >= 90`이 거짓이라는 것은 `score < 90`이 참이라는 뜻이므로 두 번째 조건식에서 `score < 90`이라는 조건을 중복해서 확인할 필요가 없다. 세 번째 조건식도 같은 이유로, `70 <= score && <br 80`이 아닌, `score >= 70`과 같이 간단히 쓸 수 있다.

![image](https://ifh.cc/g/blHPKO.png)

</br>

## 1.4 중첩 if문

`if`문의 블럭 내에 또 다른 `if`문을 포함시키는 것이 가능한데 이것을 중첩 `if`문이라고 부르며 중첩의 횟수에는 거의 제한이 없다.

``` java
if (조건식1) {
    // 조건식1의 연산결과가 true일 때 수행될 문장들을 적는다.
    if (조건식2) {
        // 조건식1과 조건식2가 모두 true일 때 수행될 문장들
    } else {
        // 조건식1이 true이고, 조건식2가 false일 때 수행될 문장들
    }
} else {
    // 조건식1이 false일 떄 수행되는 문장들
}
```

위와 같이 내부의 `if`문은 외부의 `if`문보다 안쪽으로 들여쓰기를 해서 두 `if`문의 범위가 명확히 구분될 수 있도록 작성해야 한다.

중첩 `if`문에서는 괄호{}의 생략에 더욱 조심해야 한다. 바깥쪽의 `if`문과 안쪽의 `if`문이 서로 엉켜서 `if`문과 `else`블럭의 관계가 의도한 바와 다르게 형성될 수도 있기 때문이다.

![image](https://ifh.cc/g/MJy9oq.png)

왼족의 코드는 언뜻 보기에 `else`블럭이 바깥쪽의 `if`문에 속한 것처럼 보이지만, 괄호가 생략되었을 때 `else`블럭은 가까운 `if`문에 속한 것으로 간주되기 때문에 실제로는 오른쪽과 같이 안쪽 `if`문의 `else`블럭이 되어버린다. 이제 `else`블럭은 어떤 경우에도 수행될 수 없다. 아래와 같이 괄호{}를 넣어서 `if`블럭과 `else`블럭의 관계를 확실히 해주는 것이 좋다.

``` java
if (num >= 0) {
    if (num != 0) {
        sign = '+';
    }
} else {
    sign = '-';
}
```

예제 4-5 / ch4 / FlowEx5.java
``` java
import java.util.Scanner;

public class FlowEx5 {

	public static void main(String[] args) {
		int score = 0;
		char grade = ' ', opt = '0';
		
		System.out.print("점수를 입력해주세요.>");
		
		Scanner scanner = new Scanner(System.in);
		score = scanner.nextInt();	// 화면을 통해 입력받은 점수르 score에 저장
		
		System.out.printf("당신의 점수는 %d입니다.%n", score);
		
		if (score >= 90) {	// score가 90점 보다 같거나 크면 A학점(grade)
			grade = 'A';
			if (score >= 98) {	// 90점 이상 중에서도 98점 이상은 A+
				opt = '+';
			} else if (score < 94) {	// 90점 이상 94점 미만 A-
				opt = '-';
			}
		} else if (score >= 80) {
			grade = 'B';
			if (score >= 88) {
				opt = '+';
			} else if (score < 84) {
				opt = '-';
			}
		} else {	// 나머지는 C학점(grade)
			grade = 'C';
		}
		System.out.printf("당신의 학점은 %c%c입니다.%n", grade, opt);
	}

}
```

```
점수를 입력해주세요.>100
당신의 점수는 100입니다.
당신의 학점은 A+입니다.
```

```
점수를 입력해주세요.>81
당신의 점수는 81입니다.
당신의 학점은 B-입니다.
```

```
점수를 입력해주세요.>85
당신의 점수는 85입니다.
당신의 학점은 B0입니다.
```

위 예제는 모두 3개의 `if`문으로 이루어져 있으며 `if`문 안에 또 다른 2개의 `if`문을 포함하고 있다. 제일 바깥쪽에 있는 `if`문에서 점수에 따라 학점(grade)을 결정하고, 내부의 `if`문에서는 학점을 더 세부적으로 나누어서 평가를 하고 그 결과를 출력한다. 외부 `if`문의 조건식에 의해 한번 걸러졌기 때문에 내부 `if`문의 조건식은 더 간단해질 수 있다.

아래 오른쪽 `if-else if`문은 `else`블럭이 생략되었는데, 만일 생략되지 않았다면 왼쪽과 같은 코드가 될 것이다. 변수 `opt`를 선언할 때 이미 '0'으로 초기화했기 때문에 굳이 `else`블럭을 쓸 필요가 없다.

![image](https://ifh.cc/g/Fsgp3z.png)

</br>

## 1.5 switch문

`if`문은 조건식의 결과가 참과 거짓, 두 가지 밖에 없기 때문에 경우의 수가 많이질수록 `else-if`를 계속 추가해야하므로 조건식이 많아져서 복잡해지고, 여러 개의 조건식을 계산해야하므로 처리시간도 많이 걸린다.

이러한 `if`문과 달리 `switch`문은 단 하나의 조건식으로 많은 경우의 수를 처리할 수 있고, 표현도 간결하므로 알아보기 쉽다. 그래서 처리할 경우의 수가 많은 경우에는 `if`문 보다 `switch`문으로 작성하는 것이 좋다. 다만 `switch`문은 제약조건이 있기 때문에, 경우의 수가 많아도 어쩔 수 없이 `if`문으로 작성해야 하는 경우도 있다.

`switch`문은 조건식을 먼저 계산한 다음, 그 결과와 일치하는 `case`문으로 이동한다. 이동한 `case`문 아래에 있는 문장들을 수행하며, `break`문을 만나면 전체 `switch`문을 빠져나가게 된다.

1. 조건식을 계산한다.
2. 조건식의 결과와 일치하는 case문으로 이동한다.
3. 이후의 문장들을 수행한다.
4. break문이나 switch문의 끝을 만나면 switch문 전체를 빠져나간다.

![image](https://ifh.cc/g/KxKMTP.png)

만일 조건식의 결과와 일치하는 `case`문이 하나도 없는 경우에는 `default`문으로 이동한다. `default`문은 `if`문의 `else`블럭과 같은 역할을 한다. `default`문의 위치는 어디라도 상관없으나 보통 마지막에 놓기 때문에 `break`문을 쓰지 않아도 된다.

`switch`문에서 `break`문을 각 `case`문의 영역을 구분하는 역할을 하는데, 만일 `break`문을 생략하면 `case`문 사이의 구분이 없어지므로 다른 `break`문을 만나거나 `switch`문 블럭 {}의 끝을 만날 때까지 나오는 모든 문장들을 수행한다. 이러한 이유로 각 `case`문의 마지막에 `break`문을 빼먹는 실수를 하지 않도로고 주의해야 한다.

### switch문의 제약조건

`switch`문의 조건식은 결과값이 반드시 정수 및 문자열이어야 하며, 이 값과 일치하는 `case`문으로 이동하기 때문에 `case`문의 값 역시 정수 및 문자열이어야 한다. 그리고 중복되지 않아야 한다.

게다가 `case`문의 값은 반드시 상수이어야 한다. 변수나 실수는 `case`문의 값으로 사용할 수 없다.

> **switch문의 제약조건**   
> 1. switch문의 조건식 결과는 정수 또는 문자열이어야 한다.   
> 2. case문의 값은 정수 상수만 가능하며, 종복되지 않아야 한다.

> JDK1.7이전에는 switch문의 조건식에 문자열이 허용되지 않았다.

``` java
public static void main(String[] args) {
    int num, result;
    final int ONE = 1;
        ...
    switch (result) {
        case '1' :      // OK. 문자 리터럴(정수 상수 49와 동일)
        case ONE :      // OK. 정수 상수
        case "YES" :    // OK. 문자열 리터럴. JDK1.7부터 허용
        case num :      // 에러. 변수는 불가
        case 1.0:       // 에러. 실수도 불가
            ...
    }
}
```

문자 '1'은 정수 49와 동등하므로 문제가 없고, `ONE`은 정수가 아닌 것처럼 보이지만, `final`이 붙은 정수 상수이므로 `case`문의 값으로 적합하다. 그러나 변수나 실수 리터럴은 `case`문의 값으로 적합하지 않다.

예제 4-6 / ch4 / FlowEx6.java
``` java
import java.util.Scanner;

public class FlowEx6 {

	public static void main(String[] args) {
		System.out.print("현재 월을 입력하세요.>");
		
		Scanner scanner = new Scanner(System.in);
		int month = scanner.nextInt();	// 화면을 통해 입력받은 숫자를 month에 저장
		
		switch (month) {
		case 3:
		case 4:
		case 5:
			System.out.println("현재의 계절은 봄입니다.");
			break;
		case 6: case 7: case 8:
			System.out.println("현재의 계절은 여름입니다.");
			break;
		case 9: case 10: case 11:
			System.out.println("현재의 계절은 가을입니다.");
			break;
		default:
//		case 12: case 1: case 2:
			System.out.println("현재의 계절은 겨울입니다.");
		}
	}	// main의 끝

}
```

```
현재 월을 입력하세요.>3
현재의 계절은 봄입니다.
```

`case`문은 한 줄에 하나씩 쓰던, 한 줄에 붙여서 쓰던 상관없다.

![image](https://ifh.cc/g/PCk1ca.png)

예제 4-7 / ch4 / FlowEx7.java
``` java
import java.util.Scanner;

public class FlowEx7 {

	public static void main(String[] args) {
		System.out.print("가위(1), 바위(2), 보(3) 중 하나를 입력하세요.>");
		
		Scanner scanner = new Scanner(System.in);
		int user = scanner.nextInt();	// 화면을 통해 입력받은 숫자를 user에 저장
		int com = (int)(Math.random() * 3) + 1;	// 1, 2, 3중 하나가 com에 저장됨
		
		System.out.println("당신은 " + user + "입니다.");
		System.out.println("컴은 " + com + "입니다.");
		
		switch (user - com) {
		case 2: case -1:
			System.out.println("당신이 졌습니다.");
			break;
		case 1: case -2:
			System.out.println("당신이 이겼습니다.");
			break;
		case 0:
			System.out.println("비겼습니다.");
			break;	// 마지막 문장이므로 break를 사용할 필요가 없다.
	
		}
	}	// main의 끝
}
```

```
가위(1), 바위(2), 보(3) 중 하나를 입력하세요.>1
당신은 1입니다.
컴은 1입니다.
비겼습니다.
```

```
가위(1), 바위(2), 보(3) 중 하나를 입력하세요.>3
당신은 3입니다.
컴은 2입니다.
당신이 이겼습니다.
```

이 예제는 컴퓨터와 사용자가 가위바위보를 하는 간단한 게임이다. 사용자로부터 1(가위), 2(바위), 3(보) 중의 하나를 입력받고, 컴퓨터는 1, 2, 3 중에서 하나를 임의로 선택한다.

난수(임의의 수)를 얻기 위해서는 `Math.random()`을 사용해야 하는데, 이 메소드는 0.0과 1.0사이의 범위에 속하는 하나의 `double`값을 반환한다. 0.0은 범위에 포함되고 1.0은 포함되지 않는다.

```
0.0 <= Math.random < 1.0
```

만일 1과 3 사이의 정수를 구하기 원한다면, 다음과 같은 과정으로 난수를 구하는 식을 얻을 수 있다.

1. 각 변에 3을 곱한다.

``` java
0.0 * 3 <= Math.random() * 3 < 1.0 * 3
0.0 <= Math.random() * 3 < 3.0
```

2. 각 변을 int형으로 변환한다.

``` java
(int)0.0 <= (int)(Math.random() * 3) < (int)3.0
0 <= (int)(Math.random() * 3) < 3
```

3. 각 변에 1을 더한다.

``` java
0 + 1 <= (int)(Math.random() * 3) + 1 < 3 + 1
1 <= (int)(Math.random() * 3) + 1 < 4
```

이제는 1과 3사이의 정수 중 하나를 얻을 수 있다. 1은 포함되고 4는 포함되지 않는다.

사용자가 입력한 값(user)하고 컴퓨터가 생성한 난수(com)하고 비교해서 가위바위보의 승부결과를 판단해야 한다. 두 값 모두 3가지 값이 가능하므로, 아래의 표와 같이 모두 9가지의 경우의 수를 처리해야 한다.

![image](https://ifh.cc/g/G8cLG6.png)

`user`에서 `com`의 값을 빼면, 아래의 표와 같은 결과를 얻는다. 무승부는 0, 컴퓨터 승리는 -1과 2, 사용자의 승리는 1, -2이다.

![image](https://ifh.cc/g/ra2Shc.png)

경우의 수가 9개에서 5개로 줄었다. 그리고 이 값들은 모두 정수이므로 `switch`문으로 처리가 가능하다.

``` java
switch (user - com) {
		case 2: case -1:
			System.out.println("당신이 졌습니다.");
			break;
		case 1: case -2:
			System.out.println("당신이 이겼습니다.");
			break;
		case 0:
			System.out.println("비겼습니다.");
			break;	// 마지막 문장이므로 break를 사용할 필요가 없다.
}
```

예제 4-8 / ch4 / FlowEx8.java
``` java
import java.util.Scanner;

public class FlowEx8 {

	public static void main(String[] args) {
		System.out.print("당신의 주민번호를 입력하세요.(011231-1111222)>");
		
		Scanner scanner = new Scanner(System.in);
		String regNo = scanner.nextLine();
		
		char gender = regNo.charAt(7);	// 입력받은 번호의 8번째 문자를 gender에 저장
		
		switch (gender) {
		case '1': case '3':
			System.out.println("당신은 남자입니다.");
			break;
		case '2': case '4':
			System.out.println("당신은 여자입니다.");
			break;
		default:
			System.out.println("유효하지 않은 주민등록번호입니다.");
		}
	}	// main의 끝

}
```

```
당신의 주민번호를 입력하세요.(011231-1111222)>110101-2111222
당신은 여자입니다.
```

주민등록번호를 입력받아서 성별을 확인해서 출력하는 예제이다. 주민등록번호 뒷번호의 첫 번째 자리의 값은 성별을 의미하는데, 그 값이 1, 3이면 남자, 2, 4이면 여자를 의미한다. 입력받은 주민등록번호는 `char`배열 `regNo`에 저장되며, 이 배열에서 성별을 의미하는 값은 8번째에 저장되어 있다.

``` java
gender = regNo.charAt(7);   // 입력받은 번호의 8번째 문자를 gender에 저장
```

문자열에 젖아된 문자는 `문자열.charAt(index)`로 가져올 수 있는데, index는 연속된 정수값으로 1이 아닌 0부터 시작한다. 그래서 8번째 문자는 `regNo.charAt(8)`이 아닌 `regNo.charAt(7)`이다.

![image](https://ifh.cc/g/OZVmB2.png)

`char`타입은 하나의 문자를 다루기 위한 것이지만, `char`타입의 값은 사실 문자가 아닌 정수(유니코드)로 저장되기 때문에 이처럼 `char`타입의 값도 `switch`문의 조건식과 `case`문에 사용할 수 있다.

예제 4-9 / ch4 / FlowEx9.java
``` java
import java.util.Scanner;

public class FlowEx9 {

	public static void main(String[] args) {
		char grade = ' ';
		
		System.out.print("당신의 점수를 입력하세요.(1~100)>");
		
		Scanner scanner = new Scanner(System.in);
		int score = scanner.nextInt();	// 화면을 통해 입력받은 숫자를 score에 저장
		
		switch (score) {
		case 100: case 99: case 98: case 97: case 96:
		case 95:  case 94: case 93: case 92: case 91: case 90:
			grade = 'A';
			break;
		case 89: case 88: case 87: case 86: case 85:
		case 84: case 83: case 82: case 81: case 80:
			grade = 'B';
			break;
		case 79: case 78: case 77: case 76: case 75:
		case 74: case 73: case 72: case 71: case 70:
			grade = 'C';
			break;
		default:
			grade = 'F';
		}	// end of switch
		System.out.println("당신의 학점은 " + grade + "입니다.");
	}

}
```

```
당신의 점수를 입력하세요.(1~100)>82
당신의 학점은 B입니다.
```

```
당신의 점수를 입력하세요.(1~100)>69
당신의 학점은 F입니다.
```

이 예제는 예제 4-4의 `if`문을 `switch`문을 이용해서 변경한 것이다. 이 예제를 `if`문을 이용해서 구현하려면, 조건식이 4개가 필요하며, 최대 4번의 조건식을 계산해야한다.

반면에 `switch`문은 조건식 1번만 계산하면 되므로 더 빠르다. 그러나 `case`문이 너무 많아져서 좋지 않은 코드가 되었다. 반드시 속도를 더 향상시켜야 한다면 복잡하더라도 `switch`문을 선택해야겠지만, 그렇지 않다면 이런 경우 `if`문이 더 적합하다.

예제 4-10 / ch4 / FlowEx10.java
``` java
import java.util.Scanner;

public class FlowEx10 {

	public static void main(String[] args) {
		int score = 0;
		char grade = ' ';
		
		System.out.print("당신의 점수를 입력하세요.(1~100)>");
		
		Scanner scanner = new Scanner(System.in);
		String tmp = scanner.nextLine();	// 화면을 통해 입력받은 내용을 tmp에 저장
		score = Integer.parseInt(tmp);	// 입력받은 문자열(tmp)를 숫자로 변환
		
		switch (score / 10) {
		case 10:
		case 9:
			grade = 'A';
			break;
		case 8:
			grade = 'B';
			break;
		case 7:
			grade = 'C';
			break;
		default:
			grade = 'F';
		}	// end of switch
		System.out.println("당신의 학점은 " + grade + "입니다.");
	}	// main의 끝

}
```

```
당신의 점수를 입력하세요.(1~100)>82
당신의 학점은 B입니다.
```

`score`를 10으로 나누면, 전에 배운 것과 같이 `int / int`의 결과는 `int`이기 때문에, 예를 들어 '88 / 10'은 8.8이 아니라 8을 얻는다. 따라서 80과 89 사이의 숫자들은 10으로 나누면 결과가 8이 된다. 마찬가지로 70과 79사이의 숫자들은 10으로 나누면 7이 된다.

이처럼 `switch`문에서는 조건식을 잘 만들어서 `case`문의 객수를 줄이는 것이 중요하다.

### switch문의 중첩

예제 4-11 / ch4 / FlowEx11.java
``` java
import java.util.Scanner;

public class FlowEx11 {

	public static void main(String[] args) {
		System.out.print("당신의 주민번호를 입력하세요.(011231-1111222)>");
		
		Scanner scanner = new Scanner(System.in);
		String regNo = scanner.nextLine();
		char gender = regNo.charAt(7);	// 입력받은 번호의 8번째 문자를 gender에 저장
		
		switch (gender) {
		case '1': case '3':
			switch (gender) {
			case '1':
				System.out.println("당신은 2000년 이전에 출생한 남자입니다.");
				break;
			case '3':
				System.out.println("당신은 2000년 이후에 출생한 남자입니다.");
			}
			break;
		case '2': case '4':
			switch (gender) {
			case '2':
				System.out.println("당신은 2000년 이전에 출생한 여자입니다.");
				break;
			case '4':
				System.out.println("당신은 2000년 이후에 출생한 여자입니다.");
				break;
			}
			break;
		default:
			System.out.println("유효하지 않은 주민등록번호입니다.");
		}
	}	// main의 끝

}
```

```
당신의 주민번호를 입력하세요.(011231-1111222)>010101-4111222
당신은 2000년 이후에 출생한 여자입니다.
```