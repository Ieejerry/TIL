# 스키마의 사용

</br>

## 스키마(데이터베이스) 생성

`CREATE DATABASE opentutorials;`라는 sql문을 통해 "opentutorials"라는 스키마(데이터베이스)를 생성한다.

</br>

```
mysql [(none)]> CREATE DATABASE opentutorials;
Query OK, 1 row affected (0.002 sec)
```

</br>

## 스키마(데이터베이스) 삭제

`Drop DATABASE opentutorials;`라는 sql문을 통해 "opentutorials"라는 스키마(데이터베이스)를 삭제한다.

</br>

```
mysql [(none)]> DROP DATABASE opentutorials;
Query OK, 0 rows affected (0.019 sec)
```

</br>

### 커맨드라인 리플레이

커맨드라인에서 위쪽 방향키 `↑`를 누르면 이전에 사용했던 문구를 리플레이할 수 있다.

</br>

```
mysql [(none)]> CREATE DATABASE opentutorials;
Query OK, 1 row affected (0.002 sec)
```

</br>

## 스키마(데이터베이스) 조회

`SHOW DATABASES;`라는 sql문을 통해 스키마(데이터베이스)를 조회할 수 있다.

</br>

```
mysql [(none)]> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| opentutorials      |
| performance_schema |
| test               |
+--------------------+
5 rows in set (0.011 sec)
```

</br>

## 스키마(데이터베이스) 사용

`USE opentutorials`라는 sql문을 통해 이후부터 내리는 명령을 "opentutorials" 스키마에 있는 표(table)를 대상으로 명령을 실행하게 된다.

</br>

```
mysql [(none)]> USE opentutorials;
Database changed
mysql [opentutorials]>
```