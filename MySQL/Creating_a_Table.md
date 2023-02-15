# 테이블의 생성

**커맨드라인에서 sql문을 작성할 때 뒤에 `;`을 안붙이고 Enter를 치게 되면 줄바꿈을 해준다.(`;`을 붙이고 Enter를 치면 문구를 실행한다.)**

스프레드시트 column에는 어떠한 데이터 타입이든 넣을 수 있다. 반면 데이터베이스 column에는 지정된 타입의 데이터만 넣을 수 있게 규제할 수 있다.

그로인해 데이터를 꺼낼 경우, 반드시 column에 지정된 타입의 데이터만 꺼내지기 때문에 확신할 수 있다.

**column에 데이터 타입을 강제할 수 있다.**

</br>

## 표(Table) 만들기

</br>

```
CREATE TABLE [테이블 이름](
    [칼럼이름] [데이터 타입(길이)] [데이터 유무] [자동 증가],
    PRIMARY KEY([칼럼 이름])
);
```

</br>

[테이블 이름]에는 생성하는 테이블이 사용할 이름을 지정한다.

[칼럼 이름]에는 생성하는 칼럼이 사용할 이름을 지정한다.

[데이터 타입(길이)]에는 해당 칼럼에 저장될 데이터들의 타입을 지정하고, 길이에는 저장될 데이터의 길이를 지정한다.

[데이터 유무]에는 해당 칼럼에 데이터가 없어도 될 때는 NULL을, 데이터가 반드시 있어야 할 경우에는 NOT NULL을 입력한다.

[자동 장가]에는 id와 같이 중복된 값이 없어야 하고, 데이터가 생성될 때마다 1씩 값을 증가시켜야 할 경우 AUTO_INCREAMENT를 입력한다.

PRIMARY KEY([칼럼 이름])에는 중복되지 말아야 할 column, 중요한 칼럼을 지정한다.



</br>

```
mysql [opentutorials]> CREATE TABLE topic(
                         id INT(11) NOT NULL AUTO_INCREMENT,
                         title VARCHAR(100) NOT NULL,
                         description TEXT NULL,
                         created DATETIME NOT NULL,
                         author VARCHAR(30) NULL,
                         profile VARCHAR(100) NULL,
                         PRIMARY KEY(id)
                       );

Query OK, 0 rows affected (0.022 sec)
```