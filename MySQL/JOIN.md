# JOIN

관게형 데이터베이스의 꽃이라고 할 수 있는 `JOIN`은 각각 분리된 테이블을 하나의 테이블처럼 볼 수가 있다

</br>

```
mysql [opentutorials]> SELECT * FROM topic LEFT JOIN author ON topic.author_id = author.id;
+----+------------+------------------+---------------------+-----------+------+--------+---------------------------+
| id | title      | description      | created             | author_id | id   | name   | profile                   |
+----+------------+------------------+---------------------+-----------+------+--------+---------------------------+
|  1 | MySQL      | MySQL is...      | 2023-02-22 19:13:27 |         1 |    1 | egoing | developer                 |
|  2 | Oracle     | Oracle is...     | 2023-02-22 19:14:00 |         1 |    1 | egoing | developer                 |
|  3 | SQL Server | SQL Server is... | 2023-02-22 19:14:37 |         2 |    2 | duru   | database administrator    |
|  4 | PostgreSQL | PostgreSQL is... | 2023-02-22 19:15:12 |         3 |    3 | taeho  | data scientist, developer |
|  5 | MongoDB    | MongoDB is...    | 2023-02-22 19:15:31 |         1 |    1 | egoing | developer                 |
+----+------------+------------------+---------------------+-----------+------+--------+---------------------------+
5 rows in set (0.014 sec)
```

</br>

`topic`테이블과 `author`테이블을 결합하는데 있어서 Joint 즉, 결합고리는 `topic`테이블에서는 `author_id`의 값이고, `author`테이블에서는 `id`값이다.

위에는 `SELECT` sql문과 `JOIN` sql문을 활용하여 `topic`테이블에 있는 `author_id`와 같은 값을 갖는 `author`테이블의 `id`의 데이터를 붙여서 출력한다.

</br>

```
mysql [opentutorials]> SELECT topic.id,title,description,created,name,profile FROM topic LEFT JOIN author ON topic.author_id = author.id;
+----+------------+------------------+---------------------+--------+---------------------------+
| id | title      | description      | created             | name   | profile                   |
+----+------------+------------------+---------------------+--------+---------------------------+
|  1 | MySQL      | MySQL is...      | 2023-02-22 19:13:27 | egoing | developer                 |
|  2 | Oracle     | Oracle is...     | 2023-02-22 19:14:00 | egoing | developer                 |
|  3 | SQL Server | SQL Server is... | 2023-02-22 19:14:37 | duru   | database administrator    |
|  4 | PostgreSQL | PostgreSQL is... | 2023-02-22 19:15:12 | taeho  | data scientist, developer |
|  5 | MongoDB    | MongoDB is...    | 2023-02-22 19:15:31 | egoing | developer                 |
+----+------------+------------------+---------------------+--------+---------------------------+
5 rows in set (0.001 sec)
```

</br>

첫번째 `SELECT`문 같은 경우, `topic`테이블의 `author_id`와 `author`테이블의 `id`가 함께 출력된다. `topic`테이블의 `author_id`와 `author`테이블의 `id` 같은 경우, 보기도 싫고 굳이 필요한 정보가 아니기 때문에 이 두 칼럼을 제외하고 출력하고 싶다면 sql문의 `SELECT`와 `FROM` 사이에 `*` 대신 출력하고 싶은 칼럼의 이름을 넣어주면 된다. `*`은 전체 칼럼을 의미하기 때문이다. 그래서 `SELECT`와 `FROM` 사이에 `author_id`와 `author`테이블의 `id`를 제외한 칼럼의 이름들을 입력해주면 된다. 하지만 이 때 `tooic`테이블의 `id`와 `author`테이블의 `id`는 같은 이름을 갖는다. MySQL은 둘 중 어느 칼럼을 의미하는지 모르기 때문에 에러가 발생한다. `JOIN` sql문을 사용하는 테이블의 같은 이름의 칼럼이 있다면 `테이블이름.칼럼이름`으로 명확하게 입력해주어야 한다.

위에는 `author_id`와 `author`테이블의 `id`를 제외한 데이터들을 출력한 모습이다.

</br>

```
mysql [opentutorials]> SELECT topic.id AS topic_id,title,description,created,name,profile FROM topic LEFT JOIN author ON topic.author_id = author.id;
+----------+------------+------------------+---------------------+--------+---------------------------+
| topic_id | title      | description      | created             | name   | profile                   |
+----------+------------+------------------+---------------------+--------+---------------------------+
|        1 | MySQL      | MySQL is...      | 2023-02-22 19:13:27 | egoing | developer                 |
|        2 | Oracle     | Oracle is...     | 2023-02-22 19:14:00 | egoing | developer                 |
|        3 | SQL Server | SQL Server is... | 2023-02-22 19:14:37 | duru   | database administrator    |
|        4 | PostgreSQL | PostgreSQL is... | 2023-02-22 19:15:12 | taeho  | data scientist, developer |
|        5 | MongoDB    | MongoDB is...    | 2023-02-22 19:15:31 | egoing | developer                 |
+----------+------------+------------------+---------------------+--------+---------------------------+
5 rows in set (0.001 sec)
```

</br>

출력할 때 그냥 `id`가 아닌 `topic_id`로 칼럼 이름을 출력하고 싶다면, `SELECT`와 `FROM` 사이의 출력할 칼럼들을 입력할 때 `topic.id AS topic_id`라고 입력을 해주면 해당 칼럼의 이름을 `id`가 아닌 `topic_id`로 바뀌어 출력된다.

</br>

만약 `commnet`라는 댓글을 저장하는 또 다른 테이블이 있다고 가정하면, 댓글을 작성한 작성자의 정보 또한 `author`테이블을 사용하여 중복을 제거하고 유지보수를 쉽게 할 수 있다.

**즉, 테이블을 분리함으로써 또 다른 테이블 혹은 새롭게 추가된 테이블들과도 얼마든지 관계를 맺을 수 있게 된다.**