# DELETE

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
5 rows in set (0.041 sec)
```

</br>

현재 테이블의 저장되어있는 데이터들의 목록이다. 여기서 제일 끝에 있는 `id`가 5인 `MongoDB`를 삭제하겠다.

</br>

```
mysql [opentutorials]> DELETE FROM topic WHERE id = 5;
Query OK, 1 row affected (0.024 sec)
```

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
+----+------------+-------------------+---------------------+--------+---------------------------+
4 rows in set (0.000 sec)
```

다시 `SELECT` sql문으로 데이터 목록을 확인해보니 `id`가 5인 `MongoDB` 데이터가 삭제된 것을 확인할 수가 있다.

</br>

## 주의 사항

`DELETE` sql문을 사용할 때의 주의할 점은 **`WHERE`을 꼭 넣어줘야 한다. `WHERE`을 넣지 않고 `DELETE`할 경우 모든 데이터가 삭제된다.**