# 주석과 세미콜론
## 주석
주석(comment)은 로직에 대한 설명이나 코드를 비활성화 할 때 사용한다. 주석은 프로그래밍적으로 해석되지 않는다.
### 한줄 주석
``` java
public static void main(String[] args) {
    // 두개의 변수가 같은 데이터 타입 일 때 아래와 같이 코드를 작성한다.
    String a, b;
}
```
### 여러줄 주석
``` java
public static void main(String[] args) {
    String a, b;
    /*
    a = "coding";
    b = "everybody";
    System.out.println(a+b);
    */
}
```
### JavaDoc 주석
/**로 시작하는 주석은 JavaDoc 주석이라고 해서 자바의 문서를 만들 때 사용한다. 아래 예제는 다음 URL의 문서를 생성한다.
http://docs.oracle.com/javase/7/docs/api/java/io/PrintStream.html#println(long)
``` java
/**
 * Prints an integer and then terminate the line.  This method behaves as
 * though it invokes <code>{@link #print(int)}</code> and then
 * <code>{@link #println()}</code>.
 *
 * @param x  The <code>int</code> to be printed.
 */
public void println(int x) {
    synchronized (this) {
        print(x);
        newLine();
    }
}
```

</br>

## 세미콜론
세미콜론은 문장(statement)의 끝을 의미한다. 자바에서는 문장의 끝에 세미콜론을 사용하지 않으면 컴파일 에러가 발생한다. 
``` java
// assignment statement
aValue = 8933.234;
// increment statement
aValue++;
// method invocation statement
System.out.println("Hello World!");
// object creation statement
Bicycle myBike = new Bicycle();
```
세미콜론을 이용하면 여러개의 문장을 한줄에 표현할 수 있다.
``` java
int a = 100; double b = 10.1;
```