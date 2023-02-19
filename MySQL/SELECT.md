# SELECT

데이터를 추가, 수정, 삭제는 명령이 아주 간단하다. 하지만 읽기는 아주 복잡해질 수 가 있다.

</br>

## 모든 데이터 출력

</br>

```
mysql [opentutorials]> SELECT * FROM topic;
+----+------------+-------------------+---------------------+--------+---------------------------+
| id | title      | description       | created             | author | profile                   |
+----+------------+-------------------+---------------------+--------+---------------------------+
|  1 | MySQL      | MySQL is ...      | 2023-02-14 22:44:49 | egoing | developer                 |
|  2 | ORACLE     | ORACLE is ...     | 2023-02-14 22:53:49 | egoing | developer                 |
|  3 | SQL Server | SQL Server is ... | 2023-02-14 22:56:49 | duru   | data administrator        |
|  4 | PostgreSQL | PostgreSQL is ... | 2023-02-14 22:58:14 | taeho  | data scientist, developer |
|  5 | MongoDB    | MongoDB is ...    | 2023-02-14 22:58:51 | egoing | developer                 |
+----+------------+-------------------+---------------------+--------+---------------------------+
5 rows in set (0.002 sec)
```

</br>

`SELECT * FROM topic;`을 입력하게 되면 `topic` 테이블에 있는 모든 데이터를 출력한다.

</br>

## 원하는 칼럼만 출력

</br>

```
mysql [opentutorials]> SELECT id, title, created, author FROM topic;
+----+------------+---------------------+--------+
| id | title      | created             | author |
+----+------------+---------------------+--------+
|  1 | MySQL      | 2023-02-14 22:44:49 | egoing |
|  2 | ORACLE     | 2023-02-14 22:53:49 | egoing |
|  3 | SQL Server | 2023-02-14 22:56:49 | duru   |
|  4 | PostgreSQL | 2023-02-14 22:58:14 | taeho  |
|  5 | MongoDB    | 2023-02-14 22:58:51 | egoing |
+----+------------+---------------------+--------+
5 rows in set (0.009 sec)
```

</br>

`SELECT`와 `FROM` 사이를 프로젝션이라고 하는데, 여기에는 출력하고 싶은 컬럼의 목록이 나온다. 이 부분에 `id`, `title`, `created`, `author`의 칼럼을 입력해주면 입력한 칼럼에 대한 데이터만 출력된다.

</br>

## SELECT 문법

</br>

### SELECT

</br>

```
mysql [opentutorials]> SELECT 'egoing';
+--------+
| egoing |
+--------+
| egoing |
+--------+
1 row in set (0.001 sec)

mysql [opentutorials]> SELECT 'egoing', 1+1;
+--------+-----+
| egoing | 1+1 |
+--------+-----+
| egoing |   2 |
+--------+-----+
1 row in set (0.009 sec)
```

</br>

`SELECT` 뒤에는 컬럼의 목록이 나온다.

</br>

### WHERE

</br>

```
mysql [opentutorials]> SELECT id, title, created, author FROM topic WHERE author='egoing';
+----+---------+---------------------+--------+
| id | title   | created             | author |
+----+---------+---------------------+--------+
|  1 | MySQL   | 2023-02-14 22:44:49 | egoing |
|  2 | ORACLE  | 2023-02-14 22:53:49 | egoing |
|  5 | MongoDB | 2023-02-14 22:58:51 | egoing |
+----+---------+---------------------+--------+
3 rows in set (0.001 sec)
```
</br>

`WHRER`은 스프레드시트의 필터 기능이라고 생각하면 된다. `WHERE` 뒤에 필터를 걸고 싶은 칼럼의 데이터를 `author='egoing'`와 같이 입력을 해주면 egoing이 들어간 데이터만을 필터링하여 출력해준다.

> WHERE은 FROM 뒤에 입력되어야 한다. FROM 앞에 입력될 경우, 문법적인 오류가 발생한다.

</br>

### ORDER BY

</br>

```
mysql [opentutorials]> SELECT id, title, created, author FROM topic WHERE author='egoing' ORDER BY id DESC;
+----+---------+---------------------+--------+
| id | title   | created             | author |
+----+---------+---------------------+--------+
|  5 | MongoDB | 2023-02-14 22:58:51 | egoing |
|  2 | ORACLE  | 2023-02-14 22:53:49 | egoing |
|  1 | MySQL   | 2023-02-14 22:44:49 | egoing |
+----+---------+---------------------+--------+
3 rows in set (0.001 sec)
```

</br>

`ORDER BY`는 정렬기능이다. `ORDER BY id DESC`는 id를 기준으로 내림차순으로 정렬해준다. `DESC`는 내림차순 정렬을 뜻한다.

</br>

### LIMIT

</br>

```
mysql [opentutorials]> SELECT id, title, created, author FROM topic WHERE author='egoing' ORDER BY id DESC LIMIT 2;
+----+---------+---------------------+--------+
| id | title   | created             | author |
+----+---------+---------------------+--------+
|  5 | MongoDB | 2023-02-14 22:58:51 | egoing |
|  2 | ORACLE  | 2023-02-14 22:53:49 | egoing |
+----+---------+---------------------+--------+
2 rows in set (0.001 sec)
```

</br>

스프레드시트 같은 경우, 최대 저장할 수 있는 데이터를 65000개 정도로 제한이 있지만, 데이터베이스 경우 1억건, 10억 그 이상의 데이터도 저장할 수 있다. 만약 10억건의 데이터를 `SELECT * FROM`을 통해 전부 출력한다고 하면, 컴퓨터가 부하가 생겨 멈출 수도 있기 때문에, 출력할 데이터를 제한해야 한다. 그 때 사용하는 것이 `LIMIT`이며, `LIMIT` 뒤에 숫자만큼만 잘라서 출력한다.