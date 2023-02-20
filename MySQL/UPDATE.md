# UPDATE

`UPDATE`는 데이터베이스의 저장된 데이터를 수정을 할 때 사용하는 sql문이다.

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
5 rows in set (0.026 sec)
```

</br>

현재 테이블의 데이터를 보면 두 번째 데이터의 `title`과 `description`의 `ORACLE`을 `Oracle`로 바꾸고 싶다. 이럴 때 `UPDATE` sql문을 사용하면 된다.

</br>

```
mysql [opentutorials]> UPDATE topic SET description='Oracle is ...', title='Oracle' WHERE id=2;
Query OK, 1 row affected (0.011 sec)
Rows matched: 1  Changed: 1  Warnings: 0
```

</br>

위의 코드가 두 번째 데이터의 `title`과 `description`을 수정하는 코드이다. 수정이 잘 되었는지 확인을 해보겠다.

</br>

```
mysql [opentutorials]> SELECT * FROM topic;
+----+------------+-------------------+---------------------+--------+---------------------------+
| id | title      | description       | created             | author | profile                   |
+----+------------+-------------------+---------------------+--------+---------------------------+
|  1 | MySQL      | MySQL is ...      | 2023-02-14 22:44:49 | egoing | developer                 |
|  2 | Oracle     | Oracle is ...     | 2023-02-14 22:53:49 | egoing | developer                 |
|  3 | SQL Server | SQL Server is ... | 2023-02-14 22:56:49 | duru   | data administrator        |
|  4 | PostgreSQL | PostgreSQL is ... | 2023-02-14 22:58:14 | taeho  | data scientist, developer |
|  5 | MongoDB    | MongoDB is ...    | 2023-02-14 22:58:51 | egoing | developer                 |
+----+------------+-------------------+---------------------+--------+---------------------------+
5 rows in set (0.001 sec)
```

</br>

두 번째 데이터를 확인해보면 `Oracle`로 정상적으로 변경이 되었다. `UPDATE` sql문은 `SELECT`, `INSERT` sql문처럼 자주 사용되지는 않는다.

</br>

## 주의 사항

**주의할 점은 `UPDATE` sql문을 사용할 경우, 뒤에 `WHERE`을 꼭 같이 사용해줘야 한다. `WHERE`을 사용하지 않을 경우, 모든 데이터들이 똑같이 수정되기 때문이다.**