chapter 4. 조건문과 반복문

# 2. 반복문 - for, while, do-while

반복문은 어떤 작업이 반복적으로 수행되도록 할 때 사용되며, 반복문의 종류로는 `for`문과 `while`문, 그리고 `while`문의 변형인 `do-while`문이 있다.

`for`문이나 `while`문에 속한 문장은 조건에 따라 한 번도 수행되지 않을 수도 있지만 `do-while`문에 속한 문장은 무조건 최소한 한 번은 수행될 것이 보장된다. 반복문은 주어진 조건을 만족하는 동안 주어진 문장들을 반복적으로 수행하므로 조건식을 포함하여, `if`문과 마찬가지로 조건식의 결과가 `true`이면 참이고, `false`면 거짓으로 간주된다.

`for`문과 `while`문은 구조와 기능이 유사하여 어느 경우에나 서로 변환이 가능하기 때문에 반복문을 작성해야할 때 `for`문과 `while`문 중 어느 쪽을 선택해도 좋으나 `for`문은 주로 반복횟수를 알고 있을 때 사용한다.

</br>

## 2.1 for문

`for`문은 반복 횟수를 알고 있을 때 적합하다. 구조가 조금 복잡하지만 직관적이라 오히려 이해하기 쉽다.

### for문의 구조와 수행순서

`for`문은 아래와 같이 '초기화', '조건식', '증감식', '블럭{}', 모두 4부분으로 이루어져 있으며, 조건식이 참인 동안 블럭{} 내의 문장들을 반복하다 거짓이 되면 반복문을 벗어난다.

``` java
for (초기화; 조건식; 증감식) {
    // 조건식이 참일 때 수행될 문장들을 적는다.
}
```

제일 먼저 '① 초기화'가 수행되고, 그 이후부터는 조건식이 참인 동안 '② 조건식 → ③ 수행될 문장 → ④ 증감식'의 순서로 계속 반복된다. 그러다가 조건식이 거짓이 되면, `for`문 전체를 빠져나가게 된다.

![image](https://ifh.cc/g/v8LV9F.png)

### 초기화

반복문에 사용될 변수를 초기화하는 부분이며 처음에 한 번만 수행된다. 보통 변수 하나로 `for`문을 제어하지만, 둘 이상의 변수가 필요할 때는 아래와 같이 콤마 ','를 구분자로 변수를 초기화하면 된다. 단, 두 변수의 타입은 같아야 한다.

``` java
for (int i = 1; i <= 10; i++) { ... }   // 변수 i의 값을 1로 초기화 한다.   
for (int i = 1, j = 0; i <= 10; i++) { ... }   // int타입의 변수 i와 j를 선언하고 초기화
```

### 조건식

조건식의 값이 참(true)이면 반복을 계속하고, 거짓(false)이면 반복을 중단하고 `for`문을 벗어난다.

``` java
for (int i = 1; i <= 10; i++) { ... }   // 'i <= 10'가 참인 동안 블럭{}안의 문장들을 반복   
```

조건식을 잘못 작성하면 블럭{} 내의 문장이 한 번도 수행되지 않거나 영원히 반복되는 무한반복에 빠질 수 있다.

### 증감식

반복문을 제어하는 변수의 값을 증가 또는 감소시키는 식이다. 매 반복마다 변수의 값이 증감식에 의해서 점진적으로 변하다가 결국 조건식이 거짓이 되어 `for`문을 벗어나게 된다. 변수의 값을 1씩 증가시키는 연산자 `++`이 증감식에 주로 사용되지만, 다음과 같이 다양한 연산자들로 증감식을 작성할 수도 있다.

``` java
for (int i = 1; i <= 10; i++) { ... }   // 1부터 10까지 1씩 증가
for (int i = 10; i >= 1; i--) { ... }   // 10부터 1까지 1씩 감소 
for (int i = 1; i <= 10; i += 2) { ... }   // 1부터 10까지 2씩 증가  
for (int i = 1; i <= 10; i \*= 3) { ... }   // 1부터 10까지 3배씩 증가
```

증감식도 쉼표 ','를 이용해서 두 문장 이상을 하나로 연결해서 쓸 수 있다.

``` java
for (int i = 1, j = 10; i <=10; i++, j--) { ... }   // i는 1부터 10까지 1씩 증가하고
                                                    // j는 10부터 1까지 1씩 감소한다.
```

지금까지 살펴본 이 세 가지 요소는 필요하지 않으면 생략할 수 있으며, 심지어 모두 생략하는 것도 가능하다.

``` java
for (;;) { ... }    // 초기화, 조건식, 증감식 모두 생략. 조건식은 참이 된다.
```

조건식이 생략된 경우, 참(true)으로 간주되어 무한 반복문이 된다. 대신 블럭{} 안에 `if`문을 넣어서 특정 조건을 만족하면 `for`문을 빠져 나오게 해야 한다.

예제 4-12 / ch4 / FlowEx12.java
``` java
public class FlowEx12 {

	public static void main(String[] args) {
		for (int i = 1; i <= 5; i++)
			System.out.println(i);	// i의 값을 출력한다.
		
		for (int i = 1; i <= 5; i++)
			System.out.print(i);	// print()를 쓰면 가로로 출력된다.
		
		System.out.println();
	}

}
```

```
1
2
3
4
5
12345
```

1부터 5까지 세로로 한번, 가로로 한번 출려갛는 간단한 예제이다. 아래의 표를 보면 i의 값이 변화함에 따라 조건식의 결과가 어떻게 되는지 알 수 있다.

![image](https://ifh.cc/g/fHGmtb.png)

사실 `i`의 값은 1부터 6까지 변하지만, `i`값이 6일 때 조건식이 `6 <= 5`가 되고, 이 식의 결과는 거짓(false)이므로 `for`문을 벗어나기 때문에 6은 출력되지 않는다.

예제 4-13 / ch4 / FlowEx13.java
``` java
public class FlowEx13 {

	public static void main(String[] args) {
		int sum = 0;	// 합계를 저장하기 위한 변수.
		
		for (int i = 1; i <= 10; i++) {
			sum += i;	// sum = sum + i;
			System.out.printf("1부터 %2d 까지의 합: %2d%n", i, sum);
		}
	}	// main의 끝

}
```

```
1부터  1 까지의 합:  1
1부터  2 까지의 합:  3
1부터  3 까지의 합:  6
1부터  4 까지의 합: 10
1부터  5 까지의 합: 15
1부터  6 까지의 합: 21
1부터  7 까지의 합: 28
1부터  8 까지의 합: 36
1부터  9 까지의 합: 45
1부터 10 까지의 합: 55
```

1부터 10까지의 합을 구하는 예제이다. 변수 `i`를 1부터 10까지 변화시키면서 `i`를 `sum`에 계속 더해서 누적시킨다.

![image](https://ifh.cc/g/OCrLkX.png)

예제 4-14/ ch4 / FlowEx14.java
``` java
public class FlowEx14 {

	public static void main(String[] args) {
		for (int i = 1, j = 10; i <= 10; i++, j--) {
			System.out.printf("%d \t %d%n", i, j);
		}
	}

}
```

```
1 	 10
2 	 9
3 	 8
4 	 7
5 	 6
6 	 5
7 	 4
8 	 3
9 	 2
10 	 1
```

`for`문에 `i`와 `j`, 두 개의 변수를 사용해서 `i`는 1부터 10까지 증가시키는 동시에 `j`는 10부터 1까지 감소시키면서 출력한다. 하나의 `for`문에 두 개의 변수를 이용해서 출력하는 예를 보여준 것인데, 사실 다음과 같이 하나의 변수만으로도 같은 결과를 얻을 수 있다.

``` java
for (int i = 1; i <= 10; i++) {
    System.out.printf("%d \t %d%n", i, 11 - i);
}
```

실행결과에서 `i`와 `j`의 관계를 살펴보면 `i`와 `j`를 더한 값이 11로 일정하다는 것을 알 수 있다. 이 사실을 이용하면 `j`는 `11 - i`가 된다. 그래서 `j`대신 `11 - i`라는 식을 사용할 수 있는 것이다.

``` java
i + j = 11
j = 11 = i
```

예제 4-15 / ch4 / FlowEx15.java
``` java
public class FlowEx15 {
	
	public static void main(String[] args) {
		System.out.println("i \t 2*i \t 2*i-1 \t i*i \t 11-i \t i%3 \t i/3");
		System.out.println("----------------------------------------------------");
		
		for (int i = 1; i <= 10; i++) {
			System.out.printf("%d \t %d \t %d \t %d \t %d \t %d \t %d%n", i, 2 * i, 2 * i - 1, i * i, 11 - i, i % 3, i / 3);
		}
	}
}
```

```
i 	 2*i 	 2*i-1 	 i*i 	 11-i 	 i%3 	 i/3
----------------------------------------------------
1 	 2 	     1 	     1 	     10 	 1 	     0
2 	 4 	     3 	     4       9 	     2 	     0
3 	 6 	     5 	     9 	     8 	     0 	     1
4 	 8 	     7 	     16 	 7 	     1 	     1
5 	 10 	 9 	     25 	 6 	     2 	     1
6 	 12 	 11 	 36 	 5 	     0 	     2
7 	 14 	 13 	 49 	 4 	     1 	     2
8 	 16 	 15 	 64 	 3 	     2 	     2
9 	 18 	 17 	 81 	 2 	     0 	     3
10 	 20 	 19 	 100 	 1 	     1 	     3
```

변수 `i`의 값이 1부터 10까지 변하는 동안, 다양한 연산자를 이용해서 짝수(2 * i), 홀수(2 * i + 1), 제곱(i * i), 역순(11 - i), 순환(i % 3), 반복(i / 3)을 구하는 방법을 보여준다.

나머지 연산자 `%`를 사용하면 특정 범위의 값들이 순환하면서 반복되는 결과를 얻을 수 있다는 것과 나누기 연산자 `/`는 같은 값이 연속적으로 반복되게 할 수 있다.

### 중첩 for문

`if`문 안에 또 다른 `if`문을 넣을 수 있는 것처럼, `for`문 안에 또 다른 `for`문을 포함시키는 것도 가능하다.

\**********   
\**********   
\**********   
\**********   
\**********   

다음과 같이 5행 10열의 별 `*`을 찍으려면 다음과 같이 간단히 할 수 있다.

``` java
for (int i = 1; i <= 5; i++) {
    System.out.println("**********");   // 10개의 별을 출력한다.
}
```

`System.out.println("**********");` 역시 반복적인 일을 하는 문장이니 `for`문으로 바꿀 수 있다. 이 문장을 `for`문으로 바꾸면 다음과 같다.

![image](https://ifh.cc/g/m4Nj1c.png)

왼쪽의 문장 대신 오른쪽의 `for`문을 이전의 `for`문에 넣으면 다음과 같이 두 개의 `for`문이 중첩된 형태가 된다.

![image](https://ifh.cc/g/DWVhqq.png)

예제 4-16 / ch4 / FlowEx16.java
``` java
public class FlowEx16 {

	public static void main(String[] args) {
		for (int i = 1; i <= 5; i++) {
			for (int j = 1; j <= 10; j++) {
				System.out.print("*");
			}
			System.out.println();
		}
	}	// main의 끝

}
```

```
**********
**********
**********
**********
**********
```

이번엔 다음과 같은 삼각형 모양의 별을 출력해보자

\*   
\**   
\***   
\****   
\*****   

가로로 출력하려면, `println` 메소드 대신 `print`메소드로 출력하면 된다.

``` java
for (int j = 1; j <= 5; j++) {
    System.out.print("*");  // *****을 출력한다.
}
System.out.println();   // 줄 바꿈을 한다.
```

따라서 다음과 같이 코드를 작성하면, 우리가 원하는 결과를 얻을 수 있다.

``` java
for (int j = 1; j <= 1; j++) {System.out.print("*");} System.out.println(); // *
for (int j = 1; j <= 2; j++) {System.out.print("*");} System.out.println(); // **
for (int j = 1; j <= 3; j++) {System.out.print("*");} System.out.println(); // ***
for (int j = 1; j <= 4; j++) {System.out.print("*");} System.out.println(); // ****
for (int j = 1; j <= 5; j++) {System.out.print("*");} System.out.println(); // *****
```

위 문장들을 잘 보면 조건식의 숫자만 변할 뿐 나머지는 같다.

이럴 떄는 한 문장의 조건식에 숫자 대신 변수 `i`를 넣고, 이 문장을 `i`의 값이 1부터 5까지 증가하는 `for`문 안에 넣으면 된다.

``` java
for (int i = 1; i <= 5; i++) {
    for(int j = 1; j <= i; j++) { System.out.print("*");} System.out.println();
}
```

예제 4-17 / ch4 / FlowEx17.java
``` java
import java.util.Scanner;

public class FlowEx17 {

	public static void main(String[] args) {
		int num = 0;
		
		System.out.print("*을 출력할 라인의 수를 입력하세요.>");
		
		Scanner scanner = new Scanner(System.in);
		String tmp = scanner.nextLine();	// 화면을 통해 입력받은 내용을 tmp에 저장
		num = Integer.parseInt(tmp);	// 입력받은 문자열(tmp)를 숫자로 변환
		
		for (int i = 0; i < num; i++) {
			for (int j = 0; j <= i; j++) {
				System.out.print("*");
			}
			System.out.println();
		}
	}	// main의 끝

}
```

```
*을 출력할 라인의 수를 입력하세요.>10
*
**
***
****
*****
******
*******
********
*********
**********
```

다음은 구구단을 출력하는 예제이다.

예제 4-18 / ch4 / FlowEx18.java
``` java
public class FlowEx18 {

	public static void main(String[] args) {
		for (int i = 2; i <= 9; i++) {
			for (int j = 1; j <= 9; j++) {
				System.out.printf("%d x %d = %d%n", i, j, i * j);
			}
		}
	}	// main의 끝

}
```

```
2 x 1 = 2
2 x 2 = 4
2 x 3 = 6
2 x 4 = 8
2 x 5 = 10
2 x 6 = 12
2 x 7 = 14
2 x 8 = 16
2 x 9 = 18
3 x 1 = 3
3 x 2 = 6
3 x 3 = 9
3 x 4 = 12
3 x 5 = 15
3 x 6 = 18
3 x 7 = 21
3 x 8 = 24
3 x 9 = 27
4 x 1 = 4
4 x 2 = 8
4 x 3 = 12
4 x 4 = 16
4 x 5 = 20
4 x 6 = 24
4 x 7 = 28
4 x 8 = 32
4 x 9 = 36
5 x 1 = 5
5 x 2 = 10
5 x 3 = 15
5 x 4 = 20
5 x 5 = 25
5 x 6 = 30
5 x 7 = 35
5 x 8 = 40
5 x 9 = 45
6 x 1 = 6
6 x 2 = 12
6 x 3 = 18
6 x 4 = 24
6 x 5 = 30
6 x 6 = 36
6 x 7 = 42
6 x 8 = 48
6 x 9 = 54
7 x 1 = 7
7 x 2 = 14
7 x 3 = 21
7 x 4 = 28
7 x 5 = 35
7 x 6 = 42
7 x 7 = 49
7 x 8 = 56
7 x 9 = 63
8 x 1 = 8
8 x 2 = 16
8 x 3 = 24
8 x 4 = 32
8 x 5 = 40
8 x 6 = 48
8 x 7 = 56
8 x 8 = 64
8 x 9 = 72
9 x 1 = 9
9 x 2 = 18
9 x 3 = 27
9 x 4 = 36
9 x 5 = 45
9 x 6 = 54
9 x 7 = 63
9 x 8 = 72
9 x 9 = 81
```

안쪽 `for`문은 하나의 단을 출력하는데, 바깥쪽 `for`문은 안쪽 `for`문을 8번(2단부터 9단까지) 반복해서 출력한다.

바깥쪽 `for`문이 한번 반복될 때마다 안쪽 `for`문의 모든 반복이 끝나고서야 바깥쪽 `for`문의 다음 반복으로 넘어간다.

예제 4-19 / ch4 / FlowEx19.java
``` java
public class FlowEx19 {

	public static void main(String[] args) {
		for (int i = 1; i <= 3; i++) {
		    for (int j = 1; j <= 3; j++) {
		        for (int k = 1; k <= 3; k++) {
		            System.out.println("" + i + j + k);
		        }
		    }
		}
	}	// main의 끝

}
```

```
111
112
113
121
122
123
131
132
133
211
212
213
221
222
223
231
232
233
311
312
313
321
322
323
331
332
333
```

각 반복문이 3번씩 반복하므로 모두 27번(3 * 3 * 3 = 27)이 반복된다.

예제 4-20 / ch4 / FlowEx20.java
``` java
public class FlowEx20 {

	public static void main(String[] args) {
		for (int i = 1; i <= 5; i++) {
			for (int j = 1; j <= 5; j++) {
				System.out.printf("[%d, %d]", i, j);
			}
			System.out.println();
		}
	}	// main의 끝

}
```

```
[1, 1][1, 2][1, 3][1, 4][1, 5]
[2, 1][2, 2][2, 3][2, 4][2, 5]
[3, 1][3, 2][3, 3][3, 4][3, 5]
[4, 1][4, 2][4, 3][4, 4][4, 5]
[5, 1][5, 2][5, 3][5, 4][5, 5]
```

예제 4-21 / ch4 / FlowEx21.java
``` java
public class FlowEx21 {

	public static void main(String[] args) {
		for (int i = 1; i <= 5; i++) {
			for (int j = 1; j <= 5; j++) {
				if (i == j) {
					System.out.printf("[%d, %d]", i, j);
				} else {
					System.out.printf("%5c", ' ');
				}
			}
			System.out.println();
		}
	}	// main의 끝

}
```

```
[1, 1]                    
     [2, 2]               
          [3, 3]          
               [4, 4]     
                    [5, 5]
```

바로 전 예제의 2중 `for`문에 `if`문을 넣어서 조건식 `i == j`를 만족하는 경우에만 `i`와 `j`의 값을 출력하고 나머지는 공백을 출력하였다.

`if`문의 조건식을 다르게 하면, 다양한 모양의 출력결과를 얻어낼 수 있다.

### 향상된 for문(enhanced for statement)

JDK1.5부터 배열과 컬렉션에 저장된 요소에 접근할 때 기존보다 편리한 방법으로 처리할 수 있도록 `for`문의 새로운 문법이 추가되었다.

``` java
for (타입 변수명 : 배열 또는 컬렉션) {
    // 반복할 문장
}
```

위의 문장에서 타입은 배열 또는 컬렉션의 요소의 타입이어야 한다. 배열 또는 컬렉션에 저장된 값이 매 반복마다 하나씩 순서대로 읽혀서 변수에 저장된다. 그리고 반복문의 괄호{}내에서는 이 변수를 사용해서 코드를 작성한다.

``` java
int[] arr = {10, 20, 30, 40, 50};
```

배열 `arr`을 위와 같이 선언했을 때, 이 배열의 모든 요소를 출력하는 `for`문은 아래와 같다.

![image](https://ifh.cc/g/0AG6B5.png)

위의 왼쪽은 일반적인 `for`문으로, 그리고 오른쪽은 향상된 `for`문으로 작성되었다. 두 `for`문은 동등하며, 향상된 `for`문이 더 간결하다는 것을 알 수 있다. 그러나 향상된 `for`문은 일반적인 `for`문과 달리 배열이나 컬렉션에 저장된 요소들을 읽어오는 용도로만 사용할 수 있다는 제약이 있다.

예제 4-22 / ch4 / FlowEx22.java
``` java
public class FlowEx22 {

	public static void main(String[] args) {
		int[] arr = {10, 20, 30, 40, 50};
		int sum = 0;
		
		for (int i = 0; i < arr.length; i++)
			System.out.printf("%d ", arr[i]);
		System.out.println();
		
		for (int tmp : arr) {
			System.out.printf("%d ", tmp);
			sum += tmp;
		}
		System.out.println();
		System.out.println("sum = " + sum);
	}	// main의 끝

}
```

```
10 20 30 40 50 
10 20 30 40 50 
sum = 150
```

</br>

## 2.2 while문

`for`문에 비해 `while`문은 구조가 간단하다. `if`문처럼 조건식과 블럭{}만으로 이루어져 있다. 다만 `if`문과 달리 `while`문은 조건식이 '참(true)'인 동안', 즉 조건식이 거짓이 될 때까지 블럭{} 내의 문장을 반복한다.

``` java
while (조건식) {
    // 조건식의 연산결과가 참(true)인 동안, 반복될 문장들을 적는다.
}
```

`while`문은 먼저 조건식을 평가해서 조건식이 거짓이면 문장 전체를 벗어나고, 참이면 블럭{} 내의 문장을 수행하고 다시 조건식으로 돌아간다. 조건식이 거짓이 될 때까지 이 과정이 계속 반복된다.

![image](https://ifh.cc/g/7q30wz.png)

1. 조건식이 참(true)이면 블럭{}안으로 들어가고, 거짓(false)이면 while문을 벗어난다.
2. 블럭{}의 문장을 수행하고 다시 조건식으로 돌아간다.

### for문과 while문의 비교

1부터 10까지의 정수를 순서대로 출력하는 `for`문을 `while`문으로 변경하면 아래 오른쪽과 같다.

![image](https://ifh.cc/g/4QvQNQ.png)

`for`문은 초기화, 조건식, 증감식을 한 곳에 모아 놓은 것일 뿐, `while`문과 다르지 않다. 그래서 `for`문과 `while`문은 항상 서로 변환이 가능하다.

그래도 이 경우 `while`문 보다 `for`문이 더 간결하고 알아보기 쉽다. 만일 초기화나 증감식이 필요하지 않은 경우라면, `while`문이 더 적합하다.

### while문의 조건식은 생략불가

한 가지 주의할 점은 `for`문과 달리 `while`문의 조건식은 생략할 수 없다는 것이다.

``` java
while ( ) { // 에러. 조건식이 없음
    ...
}
```

그래서 `while`문의 조건식이 항상 참이 되도록 하려면 반드시 `true`를 넣어야 한다.

예제 4-23 / ch4 / FlowEx23.java
``` java
public class FlowEx23 {
	public static void main(String[] args) {
		int i = 5;
		
		while (i-- != 0) {
			System.out.println(i + " - I can do it.");
		}
	}	// main의 끝
}
```

```
4 - I can do it.
3 - I can do it.
2 - I can do it.
1 - I can do it.
0 - I can do it.
```

변수 `i`의 값만큼 블럭{}을 반복하는 예제이다. `i`의 값이 5이므로 'I can do it.'이 모두 5번(4~0) 출력되었다. `while`문의 조건식 `i-- != 0`는 `i`의 값이 0이 아닌 동안만 참이 되고, `i`의 값이 매 반복마다 1씩 감소하다 0이 되면 조건식은 거짓이 되어 `while`문을 벗어난다.

`i--`가 후위형이므로 조건식이 평가된 후에 `i`의 값이 감소된다.

예제 4-24 / ch4 / FlowEx24.java
``` java
public class FlowEx24 {

	public static void main(String[] args) {
		int i = 11;
		
		System.out.println("카운트 다운을 시작합니다.");
		
		while (i-- != 0) {
			System.out.println(i);
			
			for (int j = 0; j < 2_000_000_000; j++) {
				    ;
			}
		}
		System.out.println("GAME OVER");
	}

}
```

```
카운트 다운을 시작합니다.
10
9
8
7
6
5
4
3
2
1
0
GAME OVER
```

10부터 0까지 1씩 감소시켜가면서 출력을 하되, `for`문으로 매 출력마다 약간의 시간이 지연되도록 했다.

``` java
for (int j = 0; j < 2_000_000_000; j++) {
        ;   // 아무런 내용도 없는 빈 문장
}
```

이 `for`문의 블럭{}내에는 아무 일도 하지 않는 빈 문장 `;` 하나만 있을 뿐 그 외에는 아무것도 없다. 그저 조건식과 증감식을 2,000,000,000번 반복하면서 시간을 보낼 뿐이다.

블럭 내에 문장이 하나뿐일 때 괄호{}를 생략할 수 있으므로 위의 `for`문을 다음과 같이 바꿀 수 있다.

``` java
for (int j = 0; j < 2_000_000_000; j++);
```

또는 아래와 같이 괄호{}를 써주고 빈 문장 `;`을 없앨 수 있다. 괄호{} 안에는 문장을 넣지 않아도 되기 때문이다.

``` java
for (int j = 0; j < 2_000_000_000; j++) {}
```

간혹 실수로 다음과 같이 코드를 작성하는 경우가 있는데, 이럴 때는 빈 문장 `;`만 `for`문에 속한 것으로 간주되어 블럭{}은 반복되지 않는다. 단 한 번만 수행된다.

``` java
for (i = 1; i <= 10; i++);  // 빈 문장 ';'을 10번 반복한다.
{
    System.out.println("i =" + i);  // i = 11이 출력된다.
}
```

예제 4-25 / ch4 / FlowEx25.java
``` java
import java.util.Scanner;

public class FlowEx25 {

	public static void main(String[] args) {
		int num = 0, sum = 0;
		System.out.print("숫자를 입력하세요.(예:12345)>");
		
		Scanner scanner = new Scanner(System.in);
		String tmp = scanner.nextLine();	// 화면을 통해 입력받은 내용을 tmp에 저장
		num = Integer.parseInt(tmp);	// 입력받은 문자열(tmp)을 숫자로 변환
		
		while (num != 0) {
			// num을 10으로 나눈 나머지를 sum에 더함
			sum += num % 10;	// sum = sum + num % 10;
			System.out.printf("sum = %3d num = %d%n", sum, num);
			
			num /= 10;	// num = num / 10;	num을 10으로 나눈 값을 다시 num에 저장
		}
		
		System.out.println("각 자리수의 합: " + sum);
	}

}
```

```
숫자를 입력하세요.(예:12345)>12345
sum =   5 num = 12345
sum =   9 num = 1234
sum =  12 num = 123
sum =  14 num = 12
sum =  15 num = 1
각 자리수의 합: 15
```

사용자로부터 숫자를 입력받고, 이 숫자의 각 자리의 합을 구하는 예제이다. 실행결과에서 알 수 있듯이 12345를 입력하면, 결과는 15(1 + 2 + 3 + 4 + 5)이다.

어떤 수를 10으로 나머지 연산하면 마지막 자리를 얻을 수 있다. 그리고 10으로 나누면 마지막 한자리가 제거된다.

``` java
12345 % 10 → 5
12345 / 10 → 1234
```

예제 4-26 / ch4 / FlowEx26.java
``` java
public class FlowEx26 {

	public static void main(String[] args) {
		int sum = 0;
		int i = 0;
		
		// i를 1씩 증가시켜서 sum에 계속 더해나간다.
		while ((sum += ++i) <= 100) {
			System.out.printf("%d - %d%n", i, sum);
		}
	}	// main의 끝

}
```

```
1 - 1
2 - 3
3 - 6
4 - 10
5 - 15
6 - 21
7 - 28
8 - 36
9 - 45
10 - 55
11 - 66
12 - 78
13 - 91
```

1부터 몇까지 더하면 누적합계가 100을 넘지 않는 제일 큰 수가 되는지 알아내는 예제이다.

예제 4-27 / ch4 / FlowEx27.java
``` java
import java.util.Scanner;

public class FlowEx27 {

	public static void main(String[] args) {
		int num;
		int sum = 0;
		boolean flag = true;	// while문의 조건식으로 사용될 변수
		Scanner scanner = new Scanner(System.in);
		
		System.out.println("합계를 구할 숫자를 입력하세요.(끝내려면 0을 입력)");
		
		while(flag) {	// flag의 값이 true이므로 조건식은 참이 된다.
			System.out.print(">>");
			
			String tmp = scanner.nextLine();
			num = Integer.parseInt(tmp);
			
			if (num != 0) {
				sum += num;	// num이 0이 아니면, sum에 더한다.
			} else {
				flag = false;	// num이 0이면, flag의 값을 false로 변경.
			}
		}	// while문의 끝
		System.out.println("합계 : " + sum);
	}

}
```

```
합계를 구할 숫자를 입력하세요.(끝내려면 0을 입력)
>>100
>>200
>>300
>>400
>>0
합계 : 1000
```

사용자로부터 반복해서 숫자를 입력받다가 0을 입력하면 입력을 마치고 총 합을 출력하는 예제이다. `while`문의 조건식으로 변수 `flag`를 사용했는데, 처음엔 `flag`에 `true`를 저장해서 계속 반복을 하다가 사용자가 0을 입력하면 `flag`의 값도 `false`로 바꿔서 반복을 멈추게 한다.

``` java
while(flag) {	// flag의 값이 true이므로 조건식은 참이 된다.
    System.out.print(">>");
    
    String tmp = scanner.nextLine();
    num = Integer.parseInt(tmp);
    
    if (num != 0) {
        sum += num;	// num이 0이 아니면, sum에 더한다.
    } else {
        flag = false;	// num이 0이면, flag의 값을 false로 변경.
    }
}
```

`while`문의 조건식이 상수는 아니지만, 변수가 고정된 값을 유지하므로 무한반복문과 다름 없다. 그래서 특정조건을 만족할 때 반복을 멈추게 하는 `if`문이 반복문 안에 꼭 필요하다.

</br>

## 2.3 do-while문

`do-while`문은 `while`문의 변형으로 기본적인 구조는 `while`문과 같으나 조건식과 블럭{}의 순서를 바꿔놓은 것이다. 그래서 `while`문과 반대로 블럭{}을 먼저 수행한 후에 조건식을 평가한다. `while`문은 조건식의 결과에 따라 블럭{}이 한 번도 수행되지 않을 수 있지만, `do-while`문은 최소한 한 번은 수행될 것을 보장한다.

``` java
do {
    // 조건식의 연산결과가 참일 때 수행될 문장들을 적는다.
} while (조건식);   ← 끝에 ';'을 잊지 않도록 주의
```

예제 4-28 / ch4 / FlowEx28.java
``` java
import java.util.Scanner;

public class FlowEx28 {

	public static void main(String[] args) {
		int input = 0, answer = 0;
		
		answer = (int)(Math.random() * 100) + 1;	// 1~100사이의 임의의 수를 저장
		Scanner scanner = new Scanner(System.in);
		
		do {
			System.out.print("1과 100사이의 정수를 입력하세요.>");
			input = scanner.nextInt();
			
			if (input > answer) {
				System.out.println("더 작은 수로 다시 시도해보세요.");
			} else if(input < answer) {
				System.out.println("더 큰 수로 다시 시도해보세요.");
			}
		} while (input != answer);
		
		System.out.println("정답입니다.");
	}

}
```

```
1과 100사이의 정수를 입력하세요.>50
더 큰 수로 다시 시도해보세요.
1과 100사이의 정수를 입력하세요.>75
더 작은 수로 다시 시도해보세요.
1과 100사이의 정수를 입력하세요.>60
더 작은 수로 다시 시도해보세요.
1과 100사이의 정수를 입력하세요.>55
정답입니다.
```

`Math.random()`을 이용해서 1과 100사이의 임의의 수를 변수 `answer`에 저장하고, 이 값을 맞출 때까지 반복하는 예제이다. 사용자 입력인 `input`이 변수 `answer`의 값과 다른 동안 반복하다가 두 값이 같으면 반복을 벗어난다.

예제 4-29 / ch4 / FlowEx29.java
``` java
public class FlowEx29 {

	public static void main(String[] args) {
		for (int i = 1; i <= 100; i++) {
			System.out.printf("i = %d", i);
			
			int tmp = i;
			
			do {
				// tmp % 10이 3의 배수인지 확인(0 제외)
				if (tmp % 10 % 3 == 0 && tmp % 10 != 0)
					System.out.print("짝");
			// tmp /= 10은 tmp = tmp / 10과 동일
			} while ((tmp /= 10) != 0);
			
			System.out.println();
		}
	}	// main의 끝

}
```

```
i = 1
i = 2
i = 3짝
i = 4
i = 5
i = 6짝
...
i = 97짝
i = 98짝
i = 99짝짝
i = 100
```

숫자 중에 3의 배수(3, 6, 9)가 포함되어 있으면, 포함된 개수만큼 박수를 치는 369게임을 1부터 100까지 출력하는 예제이다. 숫자의 각 자리를 확인해야하기 때문에 10으로 나누고 10으로 나머지 연산을 한다. 그러나 이 작업은 변수 `i`에 직접 하면 안 되고 다른 변수에 저장해서 처리해야 한다. 변수 `i`는 `for`문의 제어에 사용되는 변수이기 때문이다.

``` java
int tmp = i;
			
do {
    // tmp % 10이 3의 배수인지 확인(0 제외)
    if (tmp % 10 % 3 == 0 && tmp % 10 != 0)
        System.out.print("짝");
} while ((tmp /= 10) != 0);
```

예를 들어 `i`의 값이 97일 때, `do-while`문이 반복되는 동안 변수 `tmp`의 값은 식 `tmp /= 10`에 의해 다음과 같이 변화된다.

![image](https://ifh.cc/g/WkX3ov.png)

두 번째 반복에서만 `if`문의 조건식 `tmp % 10 % 3 == 0 && tmp % 10 != 0`을 만족시키므로 '짝'이 한 번 출력된다는 것을 알 수 있다. 위의 표에서 알 수 있듯이 `tmp % 10`은 `tmp`의 끝자리이다. 식 `tmp % 10 % 3 == 0`은 `tmp`의 끝자리가 3의 배수인지 확인하기 위한 것이다. 이 식은 `tmp % 10`의 값이 0일 때도 참이므로, 식 `tmp % 10 != 0`을 `&&`로 연결해서 `tmp % 10`의 값이 0이 아닌 경우를 제외해야 한다.

</br>

## 2.4 break문

반복문에서도 `break`문을 사용할 수 있는데, `break`문은 자신이 포함된 가장 가까운 반복문을 벗어난다. 주로 `if`문과 함꼐 사용되어 특정 조건을 만족하면 반복문을 벗어나도록 한다.

예제 4-30 / ch4 / FlowEx30.java
``` java
public class FlowEx30 {

	public static void main(String[] args) {
		int sum = 0;
		int i = 0;
		
		while (true) {
			if (sum > 100)
				break;
			++i;
			sum += i;
		}	// end of while
		
		System.out.println("i = " + i);
		System.out.println("sum = " + sum);
	}

}
```

```
i = 14
sum = 105
```

숫자를 1부터 계속 더해 나가서 몇까지 더하면 합이 100을 넘는지 알아내는 예제이다. `i`의 값을 1부터 1씩 계속 증가시켜가며 더해서 `sum`에 저장한다. `sum`의 값이 100을 넘으면 `if`문의 조건식이 참이므로 `break`문이 수행되어 자신이 속한 반복문을 즉시 벗어난다.

이처럼 무한 반복문에는 조건문과 `break`문이 항상 같이 사용된다.

</br>

## 2.5 continue문

`continue`문은 반복문 내에서만 사용될 수 있으며, 반복이 진행되는 도중에 `continue`문을 만나면 반복문의 끝으로 이동하여 다음 반복으로 넘어간다. `for`문의 경우 증감식으로 이동하며, `while`문과 `do-while`문의 경우 조건식으로 이동한다.

`continue`문은 반복문 전체를 벗어나지 않고 다음 반복을 계속 수행한다는 점이 `break`문과 다르다. 주로 `if`문과 함께 사용되어 특정 조건을 만족하는 경우에 `continue`문 이후의 문장들을 수행하지 않고 다음 반복으로 넘어가서 계속 진행하도록 한다.

전체 반복 중에 특정조건을 만족하는 경우를 제외하고자 할 때 유용하다.

예제 4-31 / ch4 / FlowEx31.java
``` java
public class FlowEx31 {

	public static void main(String[] args) {
		for (int i = 0; i <= 10; i++) {
			if (i % 3 == 0)
				continue;
			System.out.println(i);
		}
	}

}
```

```
1
2
4
5
7
8
10
```

1과 10사이의 숫자를 출력하되 그 중에서 3의 배수인 것은 제외하도록 하였다. `i`의 값이 3의 배수인 경우, `if`문의 조건식 `i % 3 == 0`은 참이 되어 `continue`문에 의해 반복문의 블럭끝 '}'으로 이동한다. 즉 `continue`문과 반복문 블럭의 끝'}' 사이의 문장들을 건너뛰고 반복을 이어가는 것이다.

예제 4-32 / ch4 / FlowEx32.java
``` java
import java.util.Scanner;

public class FlowEx32 {

	public static void main(String[] args) {
		int menu = 0;
		int num = 0;
		
		Scanner scanner = new Scanner(System.in);
		
		while (true) {
			System.out.println("(1) squre");
			System.out.println("(2) squre root");
			System.out.println("(1) log");
			System.out.print("원하는 메뉴(1~3)를 선택하세요.(종료: 0)>");
			
			String tmp = scanner.nextLine();	// 화면에서 입력받은 내용을 tmp에 저장
			menu = Integer.parseInt(tmp);
			
			if (menu == 0) {
				System.out.println("프로그램을 종료합니다.");
				break;
			} else if (!(1 <= menu && menu <= 3)) {
				System.out.println("메뉴를 잘못 선택하셨습니다.(종료는 0)");
				continue;
			}
			
			System.out.println("선택하신 메뉴는 " + menu + "번입니다.");
		}
	}	// main의 끝

}
```

```
(1) squre
(2) squre root
(1) log
원하는 메뉴(1~3)를 선택하세요.(종료: 0)>4
메뉴를 잘못 선택하셨습니다.(종료는 0)
(1) squre
(2) squre root
(1) log
원하는 메뉴(1~3)를 선택하세요.(종료: 0)>1
선택하신 메뉴는 1번입니다.
(1) squre
(2) squre root
(1) log
원하는 메뉴(1~3)를 선택하세요.(종료: 0)>0
프로그램을 종료합니다.
```

메뉴를 보여주고 선택하게 하는 예제이다. 메뉴를 잘못 선택한 경우, `continue`문으로 다시 메뉴를 보여주고, 종료(0)를 선택한 경우 `break`문으로 반복을 벗어나 프로그램이 종료되도록 했다.

</br>

## 2.6 이름 붙은 반복문

`break`문은 근접한 단 하나의 반복문만 벗어날 수 있기 때문에, 여러 개의 반복문이 중첩된 경우에는 `break`문으로 중첩 반복문을 완전히 벗어날 수 없다. 이 때는 중첩 반복문 앞에 이름을 붙이고 `break`문과 `continue`문에 이름을 지정해 줌으로써 하나 이상의 반복문을 벗어나거나 반복을 건너뛸 수 있다.

예제 4-33 / ch4 / FlowEx33.java
``` java
public class FlowEx33 {

	public static void main(String[] args) {
		// for문에 Loop1이라는 이름을 붙였다.
		Loop1 : for (int i = 2; i <= 9; i++) {
			for (int j = 1; j <= 9; j++) {
				if (j == 5)
					break Loop1;
//					break;
//					continue Loop1;
//					continue;
				System.out.println(i + " * " + j + " = " + i * j);
			}	// end of for i
			System.out.println();
		}	// end of Loop
	}

}
```

```
2 * 1 = 2
2 * 2 = 4
2 * 3 = 6
2 * 4 = 8
```

구구단을 출력하는 예제이다. 제일 바깥에 있는 `for`문에 `Loop1`이라는 이름을 붙였다. 그리고 `j`가 5일 때 `break`문을 수행하도록 했다. 반복문의 이름이 지정되지 않은 `break`문은 자신이 속한 하나의 반복문만 벗어날 수있지만, 지금처럼 반복문에 이름을 붙여 주고 `break`문에 반복문 이름을 지정해주면 하나 이상의 반복문도 벗어날 수 있다.

`j`가 5일 때 반복문 `Loop1`을 벗어나도록 했으므로 2단의 4번째 줄까지 밖에 출력되지 않았다. 만일 반복문의 이름이 지정되지 않은 `break`문이었다면 2단부터 9단까지 모두 네줄씩 출력되었을 것이다.

예제 4-34 / ch4 / FlowEx34.java
``` java
import java.util.Scanner;

public class FlowEx34 {

	public static void main(String[] args) {
		int menu = 0, num = 0;
		
		Scanner scanner = new Scanner(System.in);
		
		outer:
			while (true) {
				System.out.println("(1) squre");
				System.out.println("(2) squre root");
				System.out.println("(3) log");
				System.out.print("원하는 메뉴(1~3)를 선택하세요.(종료: 0)>");
				
				String tmp = scanner.nextLine();	// 화면을 통해 입력받은 내용을 tmp에 저장
				menu = Integer.parseInt(tmp);	// 입력받은 문자열(tmp)을 숫자로 변환
				
				if (menu == 0) {
					System.out.println("프로그램을 종료합니다.");
					break;
				} else if (!(1 <= menu && menu <= 3)) {
					System.out.println("메뉴를 잘못 선택하셨습니다.(종료는 0)");
					continue;
				}
				
				for (;;) {
					System.out.print("계산할 값을 입력하세요.(계산 종료: 0, 전체 종료: 99)>");
					tmp = scanner.nextLine();	// 화면에서 입력받은 내용을 tmp에 저장
					num = Integer.parseInt(tmp);	// 입력받은 문자열(tmp)을 숫자로 변환
					
					if (num == 0)
						break;	// 계산 종료. for문을 벗어난다.
					
					if (num == 99)
						break outer;	// 전체 종료. for문과 while문을 모두 벗어난다.
					
					switch (menu) {
					case 1: 
						System.out.println("result = " + num * num);
						break;
					case 2:
						System.out.println("result = " + Math.sqrt(num));
						break;
					case 3:
						System.out.println("result = " + Math.log(num));
					}
				}	// for (;;)
			}	// while의 끝
	}	// main의 끝

}
```

```
(1) squre
(2) squre root
(3) log
원하는 메뉴(1~3)를 선택하세요.(종료: 0)>1
계산할 값을 입력하세요.(계산 종료: 0, 전체 종료: 99)>2
result = 4
계산할 값을 입력하세요.(계산 종료: 0, 전체 종료: 99)>3
result = 9
계산할 값을 입력하세요.(계산 종료: 0, 전체 종료: 99)>0
(1) squre
(2) squre root
(3) log
원하는 메뉴(1~3)를 선택하세요.(종료: 0)>2
계산할 값을 입력하세요.(계산 종료: 0, 전체 종료: 99)>4
result = 2.0
계산할 값을 입력하세요.(계산 종료: 0, 전체 종료: 99)>99
```

이 예제는 예제 4-32를 발전시킨 것으로 메뉴를 선택하면 해당 연산을 반복적으로 수행할 수 있게 `for`문을 추가하였다.

아래와 같이 반복문만 떼어놓고 보면, 무한 반복문인 `while`문 안에 또 다른 무한 반복문인 `for`문이 중첩된 구조라는 것을 알 수 있다. `while`문은 메뉴를 반복해서 선택할 수 있게 해주고, `for`문은 선택된 메뉴의 작업을 반복해서 할 수 있게 해준다.

``` java
outer:
while (true) {
    ...
    for (;;) {
        ...
        if (num == 0)   // 계산 종료. for문을 벗어난다.
            break;
        if (num == 99)  // 전체 종료. for문과 while문 모두 벗어난다.
            break outer;
        ...
    }   // for (;;)
}   // while (true)
```

선택된 메뉴에서 0을 입력하면 `break`문으로 `for`문을 벗어나서 다른 메뉴를 선택할 수 있게 되고, 99를 입력하면 `break outer;`에 의해 `for`문과 `while`문 모두를 벗어나 프로그램이 종료된다.