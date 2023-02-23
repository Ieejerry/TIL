# 테이블 분리하기

관계형 데이터베이스를 구성하기 위해 테이블을 분리하여야 한다. 그러면 기존 `topic` 테이블을 분리하여 두 개의 테이블로 구성해보겠다.

</br>

## 기존 테이블 이름 바꾸기

</br>

```
mysql [opentutorials]> RENAME TABLE topic TO topic_backup;
Query OK, 0 rows affected (0.049 sec)

mysql [opentutorials]> SHOW TABLES;
+-------------------------+
| Tables_in_opentutorials |
+-------------------------+
| topic_backup            |
+-------------------------+
1 row in set (0.001 sec)

mysql [opentutorials]> SELECT * FROM topic_backup;
+----+------------+-------------------+---------------------+--------+---------------------------+
| id | title      | description       | created             | author | profile                   |
+----+------------+-------------------+---------------------+--------+---------------------------+
|  1 | MySQL      | MySQL is ...      | 2023-02-14 22:44:49 | egoing | developer                 |
|  2 | Oracle     | Oracle is ...     | 2023-02-14 22:53:49 | egoing | developer                 |
|  3 | SQL Server | SQL Server is ... | 2023-02-14 22:56:49 | duru   | data administrator        |
|  4 | PostgreSQL | PostgreSQL is ... | 2023-02-14 22:58:14 | taeho  | data scientist, developer |
+----+------------+-------------------+---------------------+--------+---------------------------+
4 rows in set (0.018 sec)
```

</br>

기존 테이블의 이름을 `topic_backup`으로 바꾸고, `SHOW TABLES;`를 통해 바뀐 테이블 이름을 확인하고, `SELECT` sql문을 통해 이름 바뀐 테이블의 데이터들도 잘 있는지 확인하였다.

</br>

## 새로운 두 개의 테이블 만들기

</br>

```
mysql [opentutorials]> CREATE TABLE `topic` (
    ->   `id` int(11) NOT NULL AUTO_INCREMENT,
    ->   `title` varchar(30) NOT NULL,
    ->   `description` text,
    ->   `created` datetime NOT NULL,
    ->   `author_id` int(11) DEFAULT NULL,
    ->   PRIMARY KEY (`id`)
    -> );
Query OK, 0 rows affected (0.042 sec)

mysql [opentutorials]> DESC topic;
+-------------+-------------+------+-----+---------+----------------+
| Field       | Type        | Null | Key | Default | Extra          |
+-------------+-------------+------+-----+---------+----------------+
| id          | int(11)     | NO   | PRI | NULL    | auto_increment |
| title       | varchar(30) | NO   |     | NULL    |                |
| description | text        | YES  |     | NULL    |                |
| created     | datetime    | NO   |     | NULL    |                |
| author_id   | int(11)     | YES  |     | NULL    |                |
+-------------+-------------+------+-----+---------+----------------+
5 rows in set (0.024 sec)
```

</br>

기존 테이블과 이름이 같은 `topic`이라는 테이블을 새로 만들어주었다. 이 테이블에는 `author`와 `profile` 대신 `author_id`라는 칼럼을 만들어주었다.

</br>

```
mysql [opentutorials]> CREATE TABLE `author` (
    ->   `id` int(11) NOT NULL AUTO_INCREMENT,
    ->   `name` varchar(20) NOT NULL,
    ->   `profile` varchar(200) DEFAULT NULL,
    ->   PRIMARY KEY (`id`)
    -> );
Query OK, 0 rows affected (0.021 sec)

mysql [opentutorials]> DESC author;
+---------+--------------+------+-----+---------+----------------+
| Field   | Type         | Null | Key | Default | Extra          |
+---------+--------------+------+-----+---------+----------------+
| id      | int(11)      | NO   | PRI | NULL    | auto_increment |
| name    | varchar(20)  | NO   |     | NULL    |                |
| profile | varchar(200) | YES  |     | NULL    |                |
+---------+--------------+------+-----+---------+----------------+
3 rows in set (0.016 sec)
```

</br>

그리고 추가적으로 `author`라는 새로운 테이블을 만들어주었다. 이 테이블에는 `id`, `name`, `profile` 칼럼이 있고, `name`에는 기존 `topic`테이블의 `author`, `profile`에는 기존 테이블의 `profile` 데이터를 넣어줄 것이다.

</br>

```
mysql [opentutorials]> INSERT INTO `author` VALUES (1,'egoing','developer');
Query OK, 1 row affected (0.012 sec)

mysql [opentutorials]> INSERT INTO `author` VALUES (2,'duru','database administrator');
Query OK, 1 row affected (0.009 sec)

mysql [opentutorials]> INSERT INTO `author` VALUES (3,'taeho','data scientist, developer');
Query OK, 1 row affected (0.009 sec)

MariaDB [opentutorials]> SELECT * FROM author;
+----+--------+---------------------------+
| id | name   | profile                   |
+----+--------+---------------------------+
|  1 | egoing | developer                 |
|  2 | duru   | database administrator    |
|  3 | taeho  | data scientist, developer |
+----+--------+---------------------------+
3 rows in set (0.001 sec)
```

</br>

`author` 테이블에 기존 `author`와 `profile`데이터를 `INSERT` sql문으로 생성하고, `SELECT` sql문으로 조회하였다.

</br>

```
mysql [opentutorials]> INSERT INTO `topic` VALUES (1,'MySQL','MySQL is...',NOW(),1);
Query OK, 1 row affected (0.012 sec)

mysql [opentutorials]> INSERT INTO `topic` VALUES (2,'Oracle','Oracle is...',NOW(),1);
Query OK, 1 row affected (0.009 sec)

mysql [opentutorials]> INSERT INTO `topic` VALUES (3,'SQL Server','SQL Server is...',NOW(),2);
Query OK, 1 row affected (0.009 sec)

mysql [opentutorials]> INSERT INTO `topic` VALUES (4,'PostgreSQL','PostgreSQL is...',NOW(),3);
Query OK, 1 row affected (0.009 sec)

mysql [opentutorials]> INSERT INTO `topic` VALUES (5,'MongoDB','MongoDB is...',NOW(),1);
Query OK, 1 row affected (0.009 sec)

mysql [opentutorials]> SELECT * FROM topic;
+----+------------+------------------+---------------------+-----------+
| id | title      | description      | created             | author_id |
+----+------------+------------------+---------------------+-----------+
|  1 | MySQL      | MySQL is...      | 2023-02-22 19:13:27 |         1 |
|  2 | Oracle     | Oracle is...     | 2023-02-22 19:14:00 |         1 |
|  3 | SQL Server | SQL Server is... | 2023-02-22 19:14:37 |         2 |
|  4 | PostgreSQL | PostgreSQL is... | 2023-02-22 19:15:12 |         3 |
|  5 | MongoDB    | MongoDB is...    | 2023-02-22 19:15:31 |         1 |
+----+------------+------------------+---------------------+-----------+
5 rows in set (0.000 sec)
```

</br>

`topic` 테이블에 기존 `title`와 `description`데이터를 `INSERT` sql문으로 생성하고, `author_id`라는 새로운 칼럼에 `author` 테이블의 `id` 값을 넣어주고, `SELECT` sql문으로 조회하였다.