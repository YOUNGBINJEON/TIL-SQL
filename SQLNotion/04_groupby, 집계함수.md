수잔과 같거나 많은 급여는 받는 사원 부서코드, 이름조회

select department_id, first_name from employees where salary >= all () 여러 조건에서 제일 큰조건 이상 조회



select department_id, first_name from employees where salary >= any () 여러 조건에서 제일 작은조건 이상 조회



### 집계함수 

```sql
select sum(department_id) from employees;

select count(department_id), count(salary), count(*)  from employees;
```



```sql
MAX(), MIN() 은 숫자, 문자, 날짜 사용 가능

select max(salary), min(salary) from employees;

select max(first_name), min(salary) from employees;

select max(first_name), min(salary), max(hire_date) from employees;

select first_name,  salary from employees where salary = (select max(salary) from employees) or salary = (select min(salary) from employees);
```



### group by

```sql
// 그룹함수 쓸때는 
부서별로 급여 총합 조회( 부서 배정 안된 사람 제외)
SELECT department_id, sum(salary) from employees where department_id is not null group by department_id;


그룹바이 뒤로 여러개를 쓰면 대중소 순으로 분류 기준
SELECT department_id, job_id, sum(salary) from employees where department_id is not null group by department_id, job_id order by department_id desc;


부서별로 급여 총합 조회하되 부서별로 급여 총합이 10000 미만인 부서의 결과만 조회 
select department_id, sum(salary) from employees where sum(salary) < 10000 group by department_id; => 에러
```



#### Having 절

> 우선순위 
>
> (1. from > 2. where(일반조건식) > 3. group by > 4. having(그룹함수한정 조건식) > 5. select)

```sql
개선
select department_id, sum(salary) from employees group by department_id having sum(salary) >= 50000;


부서별로 급여 총합 조회하되 사원의 급여가 5000은 제외하고 부서별로 급여 총합이 10000 미만인 부서의 결과만 조회 
select department_id, sum(salary) from employees where salary >= 5000 group by department_id having sum(salary) >= 50000;
```



#### rollup()

```sql
select department_id, job_id, sum(salary) from employees where department_id is not null group by rollup(department_id, job_id);
```

#### cube()

```sql
select department_id, job_id, sum(salary) from employees where department_id is not null group by cube(department_id, job_id);
```

