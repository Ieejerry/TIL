# INSERT

`INSERT`는 MySQL에서 CRUD중 Create 즉, 데이터를 생성할 때 쓴다.

</br>

```
mysql [opentutorials]> INSERT INTO topic (title, description, created, author, profile) VALUES ('MySQL', 'MySQL is ...', NOW(), 'egoing', 'developer');
Query OK, 1 row affected (0.021 sec)
```

</br>

위의 sql문을 통해서 topic에 MySQL이라는 데이터를 생성하였다.

</br>

```
mysql [opentutorials]> SELECT * FROM topic;
+----+-------+--------------+---------------------+--------+-----------+
| id | title | description  | created             | author | profile   |
+----+-------+--------------+---------------------+--------+-----------+
|  1 | MySQL | MySQL is ... | 2023-02-14 22:44:49 | egoing | developer |
+----+-------+--------------+---------------------+--------+-----------+
1 row in set (0.001 sec)
```

</br>

MySQL에서 CRUD중 Read 즉, 저장된 데이터를 읽을 때는 `Select`를 사용한다. 위의 코드는 앞서 생성하였던 MySQL 데이터를 읽는 sql문이다.

</br>

```
mysql [opentutorials]> INSERT INTO topic (title, description, created, author, profile) VALUES ('ORACLE', 'ORACLE is ...', NOW(), 'egoing', 'developer');
Query OK, 1 row affected (0.009 sec)
```

</br>

이어서 ORACLE이라는 데이터를 추가로 생성하였다.

</br>

```
mysql [opentutorials]> SELECT * FROM topic;
+----+--------+---------------+---------------------+--------+-----------+
| id | title  | description   | created             | author | profile   |
+----+--------+---------------+---------------------+--------+-----------+
|  1 | MySQL  | MySQL is ...  | 2023-02-14 22:44:49 | egoing | developer |
|  2 | ORACLE | ORACLE is ... | 2023-02-14 22:53:49 | egoing | developer |
+----+--------+---------------+---------------------+--------+-----------+
2 rows in set (0.000 sec)
```

</br>

`SELECT` sql문을 통해 ORACLE 데이터가 잘 생성되었는지 확인하였다.

</br>

```
mysql [opentutorials]> INSERT INTO topic (title, description, created, author, profile) VALUES ('SQL Server', 'SQL Server is ...', NOW(), 'duru', 'data administrator');
Query OK, 1 row affected (0.009 sec)

mysql [opentutorials]> INSERT INTO topic (title, description, created, author, profile) VALUES ('PostgreSQL', 'PostgreSQL is ...', NOW(), 'taeho', 'data scientist, developer');
Query OK, 1 row affected (0.009 sec)

mysql [opentutorials]> INSERT INTO topic (title, description, created, author, profile) VALUES ('MongoDB', 'MongoDB is ...', NOW(), 'egoing', 'developer');
Query OK, 1 row affected (0.009 sec)
```

</br>

총 3개의 데이터를 추가적으로 생성하여 총 5개의 데이터를 저장하였다.

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
5 rows in set (0.001 sec)
```

</br>

`SELECT` sql문을 사용하여 5개의 데이터가 잘 저장되었는지 확인하였다.

스키마(데이터베이스)를 생성, 삭제하는 일은 매우 드물지만, **`SELECT`는 데이터베이스를 사용하면서 가장 많이 사용하는 sql문이다.** 그 다음으로는 `INSERT` sql문을 많이 사용한다.