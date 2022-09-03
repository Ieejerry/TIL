Chapter 5. 배열 array

# 3. 다차원 배열

2차원 이사의 배열, 즉 다차원(multi-dimensional) 배열도 선언해서 사용할 수 있다. 메모리의 용량이 허용하는 한, 차원의 제한은 없다.

</br>

## 3.1 2차원 배열의 선언과 인덱스

2차원 배열을 선언하는 방법은 1차원 배열과 같다. 다만 괄호[]가 하나 더 들어갈 뿐이다.

![image](https://ifh.cc/g/AdVRhL.png)

> 3차원이상의 고차원 배열의 선언은 대괄호[]의 개수를 차원의 수만큼 추가해 주기만 하면 된다.

2차원 배열은 주로 테이블 형태의 데이터를 담는데 사용되며, 만일 4행 3열의 데이터를 담기 위한 배열을 생성하려면 다음과 같다.

``` java
int[][] score = new int[4][3];  // 4행 3열의 2차원 배열을 생성한다.
```

위 문장이 수행되면 아래의 그릠처럼 4행 3열의 데이터, 모두 12개의 int값을 저장할 수 있는 공간이 마련된다.

![image](https://ifh.cc/g/kdxnK0.png)

위의 그림에서는 각 요소, 즉 저장공간의 타입을 적어놓은 것이고, 실제로는 배열요소의 타입인 int이 기본값인 0이 저장된다. 배열을 생성하면, 배열의 각 요소에는 배열요소타입의 기본값이 자동적으로 저장된다.

### 2차원 배열의 index

2차원 배열은 행(row)과 열(column)로 구성되어 있기 때문에 index도 행과 열에 각각 하나씩 존재한다. '행index'의 범위는 '0 \~ 행의 길이 - 1'이고, '열의 index'의 범위는 '0 \~ 열의 길이 - 1'이다. 그리고 2차원 배열의 각 요소에 접근하는 방법은 '배열이름[행index][열index]'이다.

만일 다음과 같이 배열 `score`를 생성하면, `score[0][0]`부터 `score[3][2]`까지 모두 12개(4*3=12)의 int값을 저장할 수 있는 공간이 마련되고, 각 배열 요소에 접근할 수 있는 방법은 다음과 같다.

``` java
int[][] score = new int[4][3];  // 4행 3열의 2차원 배열 score를 생성
```

![image](https://ifh.cc/g/1S4WnX.png)

배열 `score`의 1행 1열에 100을 저장하고, 이 값을 출력하려면 다음과 같이 하면 된다.

``` java
score[0][0] = 100;  // 배열 score의 1행 1열에 100을 저장
System.out.println(score[0][0]);    // 배열 score의 1행 1열의 값을 출력
```

</br>

## 3.2 2차원 배열의 초기화

2차원 배열도 괄호{}를 사용해서 생성과 초기화를 동시에 할 수 있다. 다만, 1차원 배열보다 괄호{}를 한번 더 써서 행렬로 구분해 준다.

``` java
int[][] arr = new int[][] { {1, 2, 3}, {4, 5, 6} };
int[][] arr = { {1, 3, 3}, {4, 5, 6} }; // new int[][]가 생략됨
```

크기가 작은 배열은 위와 같이 간단히 한 줄로 써주는 것도 좋지만, 가능하면 다음과 같이 행별로 줄 바꿈을 해주는 것이 보기도 좋고 이해하기 쉽다

``` java
int[][] arr = {
                    {1, 2, 3},
                    {4, 5, 6}
              };
```

만일 아래와 같은 테이블형태의 데이터를 배열에 저장하려면,

![image](https://ifh.cc/g/0sA1zg.png)

다음과 같이 하면 된다.

``` java
int[][] score = {
                    {100, 100, 100},
                    {20, 20, 20},
                    {30, 30, 30},
                    {40, 40, 40},
                    {50, 50, 50}
                }
```

2차원 배열은 '배열의 배열'로 구성되어 있다. 즉, 여러 개의 1차원 배열을 묶어서 또 하나의 배열로 만든 것이다.

`score.length`의 값은 배열 참조변수 `score`가 참조하고 있는 배열의 길이가 얼마인가를 세어보면 될 것이다. 정답은 5이다. 그리고 `score[0].length`은 배열 참조변수 `score[0]`이 참조하고 있는 배열의 길이이므로 3이다.

같은 이유로 `score[1].length`, `score[2].length`, `score[3].length`, `score[4].length`의 값 역시 모두 3이다.

만일 for문을 이용해서 2차원 배열을 초기화한다면 다음과 같다.

``` java
for (int i = 0; i < score.length; i++) {
    for (int j = 0; j < score[i].length; j++) {
        score[i][j] = 10;
    }
}
```

위의 코드는 2차원 배열 `score`의 모든 요소를 10으로 초기화한다.

예제 5-18 / ch5 / ArrayEx18.java
``` java
public class ArrayEx18 {

	public static void main(String[] args) {
		int[][] score = {
							{100, 100, 100},
							{20, 20, 20},
							{30, 30, 30},
							{40, 40, 40},
						};
		int sum = 0;
		
		for (int i = 0; i < score.length; i++) {
			for (int j = 0; j < score[i].length; j++) {
				System.out.printf("score[%d][%d] = %d%n", i, j, score[i][j]);
			}
		}
		
		for (int[] tmp : score) {
			for (int i : tmp) {
				sum += i;
			}
		}
		
		System.out.println("sum = " + sum);
	}

}
```

```
score[0][0] = 100
score[0][1] = 100
score[0][2] = 100
score[1][0] = 20
score[1][1] = 20
score[1][2] = 20
score[2][0] = 30
score[2][1] = 30
score[2][2] = 30
score[3][0] = 40
score[3][1] = 40
score[3][2] = 40
sum = 570
```

2차원 배열 `score`의 모든 요소의 합을 구하고, 출력하는 예제이다. 하나의 이중 for문으로 처리가 가능한 작업이지만, 향상된 for문으로 2차원 배열의 모든 요소를 읽어오는 방법을 보여주기 위해 출력과 합계를 따로 처리하였다.

``` java
for (int i : score) {   // 에러. 2차원 배열 score의 각 요소는 1차원 배열
    sum += i;
}
```

2차원 배열 `score`의 각 요소는 1차원 배열이므로 아래와 같이 for문을 하나 더 추가해야 한다.

``` java
for (int[] tmp : score) {   // score의 각 요소(1차원 배열 주소)를 tmp에 저장
    for (int i : tmp) { // tmp는 1차원 배열을 가리키는 참조변수
        sum += i;
    }
}
```

향샹된 for문으로 배열의 각 요소에 저장된 값들을 순차적으로 읽어올 수는 있지만, 배열에 저장된 값을 변경할 수는 없다.

예제 5-19 / ch5 / ArrayEx19.java
``` java
public class ArrayEx19 {

	public static void main(String[] args) {
		int[][] score = {
				{ 100, 100, 100 },
				{ 20, 20, 20 },
				{ 30, 30, 30 },
				{ 40, 40, 40 },
				{ 50, 50, 50 }
		};
		
		// 과목별 총점
		int korTotal = 0, engTotal = 0, mathTotal = 0;
		
		System.out.println("번호   국어  영어  수학  총점   평균");
		System.out.println("=============================");
		
		for (int i = 0; i < score.length; i++) {
			int sum = 0;	// 개인별 총점
			float avg = 0.0f;	// 개인별 평균
			
			korTotal += score[i][0];
			engTotal += score[i][1];
			mathTotal += score[i][2];
			System.out.printf("%3d", i + 1);
			
			for (int j = 0; j < score[i].length; j++) {
				sum += score[i][j];
				System.out.printf("%5d", score[i][j]);
			}
			
			avg = sum / (float)score[i].length;	// 평균계산
			System.out.printf("%5d %5.1f%n", sum, avg);
		}
		
		System.out.println("=============================");
		System.out.printf("총점: %3d %4d %4d%n", korTotal, engTotal, mathTotal);
	}

}
```

```
번호   국어  영어  수학  총점   평균
=============================
  1  100  100  100  300 100.0
  2   20   20   20   60  20.0
  3   30   30   30   90  30.0
  4   40   40   40  120  40.0
  5   50   50   50  150  50.0
=============================
총점: 240  240  240
```

5명의 학생의 세 과목 점수를 더해서 각 학생의 총점과 평균을 계산하고, 과목별 총점을 계산하는 예제이다.

</br>

## 3.3 가변 배열

자바에서는 2차원 이사의 배열을 '배열의 배열'의 형태로 처리한다는 사실을 이용하면 보다 자유로운 형태의 배열을 구성할 수 있다.

2차우너 이상의 다차원 배열을 생성할 때 전체 배열 차수 중 마지막 차수의 길이를 저장하지 않고, 추후에 각기 다른 길이의 배열을 생성함으로써 고정된 형태가 아닌 보다 유동적인 가변 배열을 구성할 수 있다.

만일 다음과 같이 '5 * 3'길이의 2차원 배열 `score`를 생성하는 코드가 있을 때,

``` java
int[][] = score = new int[5][3];    // 5행 3열의 2차원 배열 생성
```

위 코드를 다음과 같이 표현할 수 있다.

``` java
int[][] score = new int[5][];   // 두 번째 차원의 길이는 저장하지 않는다.
score[0] = new int[3];
score[1] - new int[3];
score[2] - new int[3];
score[3] - new int[3];
score[4] - new int[3];
```

첫 번째 코드와 같이 2차원 배열을 생성하면 직사각형 테이블 형태의 고정적인 배열만 생성할 수 있지만, 두 번째 코드오 같이 2차원 배열을 생성하면 다음과 같이 각 행마다 다른 길이의 배열을 생성하는 것이 가능하다.

``` java
int[][] score = new int[5][];
score[0] = new int[4];
score[1] - new int[3];
score[2] - new int[2];
score[3] - new int[2];
score[4] - new int[3];
```

`score.length`의 값은 여전히 5지만, 일반적인 2차원 배열과 달리 `score[0].length`의 값은 4이고 `score[1].length`의 값은 3으로 서로 다르다.

가변배열 역시 중괄호{}를 이용해서 다음고 같이 생성과 초기화를 동시에 하는 것이 가능하다.

``` java
int[][] score = {
				{ 100, 100, 100, 100 },
				{ 20, 20, 20 },
				{ 30, 30 },
				{ 40, 40 },
				{ 50, 50, 50 }
		};
```

</br>

## 3.4 다차원 배열의 활용

예제 5-20 / ch5 / MultiArrEx1.java
``` java
import java.util.Scanner;

public class MultiArrEx1 {

	public static void main(String[] args) {
		final int SIZE = 10;
		int x = 0, y = 0;
		
		char[][] board = new char[SIZE][SIZE];
		byte[][] shipBoard = {
//				  1  2  3  4  5  6  7  8  9
				{ 0, 0, 0, 0, 0, 0, 1, 0, 0 },	// 1
				{ 1, 1, 1, 1, 0, 0, 1, 0, 0 },	// 2
				{ 0, 0, 0, 0, 0, 0, 1, 0, 0 },	// 3
				{ 0, 0, 0, 0, 0, 0, 1, 0, 0 },	// 4
				{ 0, 0, 0, 0, 0, 0, 0, 0, 0 },	// 5
				{ 1, 1, 0, 1, 0, 0, 0, 0, 0 },	// 6
				{ 0, 0, 0, 1, 0, 0, 0, 0, 0 },	// 7
				{ 0, 0, 0, 1, 0, 0, 0, 0, 0 },	// 8
				{ 0, 0, 0, 0, 0, 1, 1, 1, 0 }	// 9
		};
		
		// 1행에 행번호를, 1열에 열번호를 저장한다.
		for (int i = 0; i < SIZE; i++) {
			board[0][i] = board[i][0] = (char)(i + '0');
		}
		
		Scanner scanner = new Scanner(System.in);
		
		while (true) {
			System.out.printf("좌표를 입력하세요.(종료는 00)>");
			String input = scanner.nextLine();	// 화면을 통해 입력받은 내용을 input에 저장
			
			if (input.length() == 2) {	// 두 글자를 입력한 경우
				x = input.charAt(0) - '0';	// 문자를 숫자로 변환
				y = input.charAt(1) - '0';
				
				if (x == 0 && y == 0) break;	// x와 y가 모두 0인 경우 종료
			}
			
			if (input.length() != 2 || x <= 0 || x >= SIZE || y <= 0 || y >= SIZE) {
				System.out.println("잘못된 입력입니다. 다시 입력해주세요.");
				continue;
			}
			
			// shipBoard[x-1][y-1]의 값이 1이면, 'O'을 borad[x][y]에 저장한다.
			board[x][y] = shipBoard[x-1][y-1] == 1 ? 'O' : 'X';
			
			// 배열 board의 내용을 화면에 출력한다.
			for (int i = 0; i < SIZE; i++) {
				System.out.println(board[i]);	// board[i]는 1차원 배열
			}
			System.out.println();
		}
	}	// main의 끝

}
```

```
좌표를 입력하세요.(종료는 00)>1010
잘못된 입력입니다. 다시 입력해주세요.
좌표를 입력하세요.(종료는 00)>33
 123456789
1
2
3  X
4
5
6
7
8
9

좌표를 입력하세요.(종료는 00)>00
```

둘이 마주 앉아 다양한 크기의 배를 상대방이 알지 못하게 배치한 다음, 번갈아가며 좌표를 불러서 상대방의 배의 위치를 알아내는 게임을 간단히 하여 예제로 만들어 보았다.

2차원 char배열 `board`는 입력한 좌표를 표시하기 위한 것이고, 2차원 byte배열 `shipBoard`에는 상대방의 배의 위치를 저장한다. 0은 바다이고, 1은 배가 있는 것이다.

``` java
char[][] board = new char[SIZE][SIZE];
		byte[][] shipBoard = {
//				  1  2  3  4  5  6  7  8  9
				{ 0, 0, 0, 0, 0, 0, 1, 0, 0 },	// 1
				{ 1, 1, 1, 1, 0, 0, 1, 0, 0 },	// 2
				{ 0, 0, 0, 0, 0, 0, 1, 0, 0 },	// 3
				{ 0, 0, 0, 0, 0, 0, 1, 0, 0 },	// 4
				{ 0, 0, 0, 0, 0, 0, 0, 0, 0 },	// 5
				{ 1, 1, 0, 1, 0, 0, 0, 0, 0 },	// 6
				{ 0, 0, 0, 1, 0, 0, 0, 0, 0 },	// 7
				{ 0, 0, 0, 1, 0, 0, 0, 0, 0 },	// 8
				{ 0, 0, 0, 0, 0, 1, 1, 1, 0 }	// 9
		};
```

배열 `board`는 좌표를 쉽게 입력하기 위한 행번호와 열번호가 필요하다. 그래서 배열 `board`가 배열 `shipBoard`보다 행과 열의 길이가 1씩 큰 것이다.

``` java
// 1행에 행번호를, 1열에 열번호를 저장한다.
		for (int i = 0; i < SIZE; i++) {
			board[0][i] = board[i][0] = (char)(i + '0');    // (char)(1 + '0') → '1' 
		}                                                   // (char)(2 + '0') → '2'
```

`board`는 char배열이므로, 숫자를 문자로 변환하여 저장해야한다. 그래서 변수 `i`에 문자 '0'을 더한다. 숫자 1에 문자 '0'을 더하면 문자 '1'이 된다. 그 다음엔 무한반복문으로 좌표를 반복해서 입력받는다. 입력받은 좌표 x, y에 저장된 값이 1이면, `board[x][y]`에 'O'를 저장하고, 1이 아니면 'X'를 저장한다. 배열 `board`와 `shipBoard`간에는 좌표가 가로, 세로로 각각 1씩 차이가 난다.

``` java
while (true) {
			...
			board[x][y] = shipBoard[x-1][y-1] == 1 ? 'O' : 'X';
```

그리고 2차원 char배열의 각 요소는 1차원 배열이므로 아래의 왼쪽과 같이 간단히 출력할 수 있다. 원래는 오른쪽과 같이 배열의 각 요소를 하나씩 출력해야하는데, `println`메소드로 1차원 char배열의 참조변수를 출력하면, 배열의 모든 요소를 한 줄로 출력한다.

![image](https://ifh.cc/g/oYAQG0.png)

`println()`메소드가 모든 1차원 배열을 이렇게 출력할 수 있는 것은 아니고, char배열인 경우만 가능하다.

예제 5-21 / ch5 / MultiArrEx2.java
``` java
import java.util.Scanner;

public class MultiArrEx2 {

	public static void main(String[] args) {
		final int SIZE = 5;
		int x = 0, y = 0, num = 0;
		
		int[][] bingo = new int[SIZE][SIZE];
		Scanner scanner = new Scanner(System.in);
		
		// 배열의 모든 요소를 1부터 SIZE*SIZE까지의 숫자로 초기화
		for (int i = 0; i < SIZE; i++) {
			for (int j = 0; j < SIZE; j++) {
				bingo[i][j] = i * SIZE + j + 1; 
			}
		}
		
		// 배열에 저장된 값을 뒤섞는다.(shuffle)
		for (int i = 0; i < SIZE; i++) {
			for (int j = 0; j < SIZE; j++) {
				x = (int)(Math.random() * SIZE);
				y = (int)(Math.random() * SIZE);
				
				// bingo[i][j]와 임의로 선택된 값(bingo[x][y])을 바꾼다.
				int tmp = bingo[i][j];
				bingo[i][j]= bingo[x][y];
				bingo[x][y] = tmp; 
			}
		}
		
		do {
			for (int i = 0; i < SIZE; i++) {
				for (int j = 0; j < SIZE; j++) {
					System.out.printf("%2d ", bingo[i][j]);
				}
				System.out.println();
			}
			System.out.println();
			
			System.out.printf("1~%d의 숫자를 입력하세요.(종료:0)>", SIZE*SIZE);
			String tmp = scanner.nextLine();	// 화면에서 입력받은 내용을 tmp에 저장
			num = Integer.parseInt(tmp);	// 입력받은 문자열(tmp)를 숫자로 변환
			
			// 입력받은 숫자와 같은 숫자가 저장된 요소를 찾아서 0을 저장
			outer:
			for (int i = 0; i < SIZE; i++) {
				for (int j = 0; j < SIZE; j++) {
					if (bingo[i][j] == num) {
						bingo[i][j] = 0;
						break outer;	// 2중 반복문을 벗어난다.
					}
				}
			}
		} while (num != 0);
	}	// main의 끝

}
```

```
23 25  1  7  2 
21 11 15 16  3 
13  5 17 22 18 
 9 24  4 14 19 
10  8  6 20 12 

1~25의 숫자를 입력하세요.(종료:0)>1
23 25  0  7  2 
21 11 15 16  3 
13  5 17 22 18 
 9 24  4 14 19 
10  8  6 20 12 

1~25의 숫자를 입력하세요.(종료:0)>9
23 25  0  7  2 
21 11 15 16  3 
13  5 17 22 18 
 0 24  4 14 19 
10  8  6 20 12 

1~25의 숫자를 입력하세요.(종료:0)>0
```

5 X 5크기의 빙고판에 1~25의 숫자를 차례로 저장한 다음에, `Math.random()`을 이용해서 저장된 값의 위치를 섞는다.

그 다음에 사용자로부터 숫자를 입력받아서 일치하는 숫자가 빙고판에 있으면 해당 숫자를 0으로 바꾼다.

``` java
// 입력받은 숫자와 같은 숫자가 저장된 요소를 찾아서 0을 저장
outer:
for (int i = 0; i < SIZE; i++) {
    for (int j = 0; j < SIZE; j++) {
        if (bingo[i][j] == num) {
            bingo[i][j] = 0;    // 일치하는 숫자가 있으면 0으로 변경
            break outer;	// 2중 반복문을 벗어난다.
        }
    }
}
```

입력받은 숫자와 일치하는 숫자를 빙고판에서 찾는 방법은 간단하다. 배열의 첫 번째 요소부터 순서대로 하나씩 비교하다 일치하는 숫자를 찾으면, 값을 0으로 바꾸고 break문으로 반복문을 빠져나오면 된다. 2중 반복문이므로, 이름 붙은 break문을 사용해야 한다.

예제 5-22 / ch5 / MultiArrEx3.java
``` java
public class MultiArrEx3 {

	public static void main(String[] args) {
		int[][] m1 = {
				{1, 2, 3},
				{4, 5, 6}
		};
		
		int[][] m2 = {
				{1, 2},
				{3, 4},
				{5, 6}
		};
		
		final int ROW = m1.length;		// m1의 행 길이
		final int COL = m2[0].length;	// m2의 열 길이
		final int M2_ROW = m2.length;	// m2의 행 길이
		
		int[][] m3 = new int[ROW][COL];
		
		// 행렬곱 m1 x m2의 겨로가를 m3에 저장
		for (int i = 0; i < ROW; i++)
			for (int j = 0; j < COL; j++)
				for (int k = 0; k < M2_ROW; k++)
					m3[i][j] += m1[i][k] * m2[k][j];
		
		// 행렬 m3를 출력
		for (int i = 0; i < ROW; i++) {
			for (int j = 0; j < COL; j++) {
				System.out.printf("%3d ", m3[i][j]);
			}
			System.out.println();
		}
	}	// main의 끝

}
```

```
22  28 
49  64 
```

수학에서 두 개의 행렬(matrix) `m1`과 `m2`가 있을 때, 이 두 행렬을 곱한 결과인 행렬 `m3`는 아래와 같이 정의된다.

![image](https://ifh.cc/g/bC7yRB.png)

두 행렬의 곱셈이 가능하려면, `m1`의 열의 길이와 `m2`의 행의 길이가 같아야 한다는 조건이 있다. 위의 경우에는 `m1`이 2행 **3열**이고, `m2`가 **3행** 2열이므로 곱셈이 가능하다.

그리고 곱셈연산의 결과인 행렬 `m3`의 행의 길이는 `m1`의 행의 길이와 같고, 열의 길이는 `m2`의 길이와 같다. **2행** 3열인 행렬과 3행 **2열**인 행렬을 곱하면 결과는 **2행 2열**의 행렬이 되는 것이다.

위의 행렬의 곱셈공식을 2차원 배열로 표현하면 아래와 같다.

![image](https://ifh.cc/g/wa2jYG.png)

그리고 행렬 곱셈의 결과인 행렬 `m3`의 각 요소들은 아래와 같이 계산된다.

![image](https://ifh.cc/g/YgcdAP.png)

위의 문장들을 자세히 들여다보면, 행렬 `m3`의 **행index**가 행렬 `m1`의 행index와 일치하고, `m3`의 **열index**가 `m2`의 열index와 일치한다는 것을 알 수 있다. 그래서 위의 문장들은 다음과 같이 2중 for문으로 대체할 수 있다.

``` java
for (int i = 0; i < 2; i++) {   // i = 0, 1
    for (int j = 0; j < 2; j++) {   // j = 0, 1
        m3[i][j] = m1[i][0] * m2[0][j]
                 + m1[i][1] * m2[1][j]
                 + m1[i][2] * m2[2][j];
    }
}
```

위의 문장을 잘 보면 여전히 반복되는 부분이 있다. `m1`의 열index와 `m2`의 열index가 동일하게 0부터 2까지 1씩 증가한다. 이 부분을 또 하나의 for문으로 바꾸면 다음과 같이 된다.

``` java
for (int i = 0; i < 2; i++) {
    for (int j = 0; j < 2; j++) {
        for (int k = 0; k < 3; k++) {   k = 0, 1, 2
            m3[i][j] += m1[i][k] * m2[k][j];
        }
    }
}
```

행렬 `m1`과 `m2`의 길이가 달라져도 행렬 `m3`가 계산될 수 있도록, 배열 `m3`의 크기와 for문의 조건식이 동적으로 계산되게 하였다.

``` java
final int ROW = m1.length;  // m1의 행 길이(m3의 행 길이)
final int COL = m2[0].length;   // m2의 열 길이(m3의 열 길이)
final int M2_ROW = m2.length;   // m2의 행 길이

int[][] m3 = new int[ROW][COL];
```

두 행렬의 곱셈이 가능하려면, 배열 `m1`의 열의 길이와 배열 `m2`의 행의 길이가 일치해야 한다

예제 5-23 / ch5 / MultiArrEx4.java
``` java
import java.util.Scanner;

public class MultiArrEx4 {

	public static void main(String[] args) {
		String[][] words = {
				{"chair", "의자"},		// words[0][0], words[0][1]
				{"computer", "컴퓨터"},	// words[1][0], words[1][1]
				{"integer", "정수"}		// words[2][0], words[2][1]
		};
		
		Scanner scanner = new Scanner(System.in);
		
		for (int i = 0; i < words.length; i++) {
			System.out.printf("Q%d. %s의 뜻은?", i + 1, words[i][0]);
			
			String tmp = scanner.nextLine();
			
			if (tmp.equals(words[i][1])) {
				System.out.printf("정답입니다.%n%n");
			} else {
				System.out.printf("틀렸습니다. 정답은 %s입니다.%n%n", words[i][1]);
			}
		}	// for의 끝
	}	// main의 끝

}
```

```
Q1. chair의 뜻은?dmlwk
틀렸습니다. 정답은 의자입니다.

Q2. computer의 뜻은?컴퓨터
정답입니다.

Q3. integer의 뜻은?정수
정답입니다.
```

영단어를 부여주고 단어의 뜻을 맞추는 예제이다. `words[i][0]`은 문제이고, `words[i][1]`은 답이다. `words[i][0]`을 화면에 보여주고, 입력받은 답은 `tmp`에 저장한다.

``` java
System.out.printf("Q%d. %s의 뜻은?", i + 1, words[i][0]);
String tmp = scanner.nextLine();
```

그 다음엔 `equals()`로 `tmp`와 `words[i][1]`을 비교해서 정답인지 확인한다.

``` java
if (tmp.equals(words[i][1])) {
    System.out.printf("정답입니다.%n%n");
} else {
    System.out.printf("틀렸습니다. 정답은 %s입니다.%n%n", words[i][1]);
}
```