# 집합연산자

> 두 쿼리를 비교하는 연산자를 통해 값을 조회하는 것

 

#### UNION

* 두 쿼리의 결과를 행으로 합치는 것

```sql
SELECT 사번, 이름 FROM 사원
UNION
SELECT 아이디, 이름 FROM 회원; 
```

```sql
//재난 지원금 50번 부서나 급여 5000이하 급여 받는 사원에게 지급
SELECT first_name, department_id, salary FROM employees WHERE department_id = 50 or salary <= 5000;

// UNION 활용한 코드 다른테이블이 존재할 때 사용
SELECT first_name, department_id, salary FROM employees1 WHERE department_id  = 50
UNION
SELECT first_name, department_id, salary FROM employees2 WHERE salary <= 5000;
```



#### UNION ALL

* 두 쿼리의 중복된 값도 행으로 조회

```sql
// employees1 테이블과 employee2 테이블의 중복된 값까지 출력
SELECT first_name, department_id, salary FROM employees WHERE department_id  = 50
UNION ALL
SELECT first_name, department_id, salary FROM employees WHERE salary <= 5000;
```



#### MINUS

* 두 쿼리 중에 선행 쿼리를 만족하지만 후행 쿼리를 만족하지 못하는 값 조회

```sql
// 재난 지원금 50번 부서나 급여 5000 이하 급여 받는 사람에게 지급
//
SELECT first_name, department_id, salary FROM employees1 WHERE department_id  = 50
MINUS
SELECT first_name, department_id, salary FROM employees2 WHERE salary <= 5000;
```



#### INTERSECT

* 두 쿼리를 모두 만족하는 값만 조회

```sql
SELECT first_name, department_id, salary FROM employees1 WHERE department_id  = 50
INTERSECT
SELECT first_name, department_id, salary FROM employees2 WHERE salary <= 5000;
```



### 요약

UNION :  합집합 (중복을 제거한)

UNION ALL : 합집합 (중복을 포함한)

MINUS : 차집합(첫 번째 검색 결과에서 두 번째 검색 결과를 제외한 나머지를 검색)

INTERSECT : 교집합 (양쪽 모두에서 포함된 행을 검색)