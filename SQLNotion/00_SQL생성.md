# SQL 사용법





### SQL 실행 





### 계정 생성

```sql
//system 계정에서만 유저 생성 가능
SQL> connect system / oracle
Connected.

//유저 생성
SQL> create user jdbc identified by jdbc;

User created.

//권한 부여
SQL> grant resource, connect to jdbc;

Grant succeeded.
```



오라클 주석 `--`



SQL 흐름 

CREATE TABLE

ALTER TABLE

DROP TALE

INSERT

INSERT한 정보 UPDATE

데이터 베이스로 적용 COMMIT / ROLLBACK

DELETE