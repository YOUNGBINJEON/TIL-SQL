# JOIN

> 두 개이상의 테이블을 서로 묶어서 하나의 결과 집합으로 만들어 내는것을 말함



* 표준 문법과 오라클 문법이 다르다

  ```sql
  //표준 JOIN 문법 - ANSI
  
  SELECT  a1.name, b1.dept_name FROM  A a1 JOIN B b1 ON a1.id = b1.id;
  
  // FROM 뒤 쉼표를 = JOIN으로 씀 / where = ON으로 씀
  
  //오라클 JOIN 문법
  
  SELECT  a1.name, b1.dept_name FROM  A a1, B b1 WHERE a1.id = b1.id;
  ```





#### INNER JOIN

```sql
//employees 테이블과 departments 테이블 조인 
SELECT employee_id, department_name, employees.department_id, department_name FROM employees, departments WHERE employees.department_id = departments.department_id;


//위 코드 간략화
SELECT employee_id, department_name, e.department_id, department_name FROM employees e, departments d WHERE e.department_id = d.department_id;

```

* INNER JOIN 표준문법

  ```sql
  SELECT employee_id, department_name, e.department_id, department_name FROM employees e INNER JOIN departments d ON e.department_id = d.department_id;
  ```

  



#### OUTTER JOIN

* NULL이 존재할 때 where절에서 (+)로 추가해서 추가한 쪽에 부족한 데이터를

   (+)가 없는 쪽의 데이터를 표현하도록 하는것

```sql
// employees에 NULL포함 조인해서 출력하고 싶을때 where 절 department에 (+) 삽입
SELECT employee_id, first_name,department_name, e.department_id, department_name FROM employees e, departments d WHERE e.department_id = d.department_id(+);


// department에 NULL포함 조인해서 출력하고 싶을때 where 절 employees에 (+) 삽입
SELECT employee_id, first_name,department_name, e.department_id, department_name FROM employees e, departments d WHERE e.department_id(+) = d.department_id;


//London 도시에 근무하는 사원명, 부서명, 도시명
//사원명 : employees
//부서명 : departments
//도시명 : locations
SELECT first_name, department_name, city FROM employees e, departments d, locations l WHERE e.department_id = d.department_id AND d.location_id = l.location_id AND lower(city) = 'london';


//부서명에 IT를 포함하는 부서의 사원명, 부서명, 도시명 조회
SELECT first_name, department_name, city FROM employees e, departments d, locations l WHERE e.department_id = d.department_id AND d.location_id = l.location_id AND INSTR(lower(department_name), 'it') > 0;

SELECT first_name, department_name, city FROM employees e, departments d, locations l WHERE e.department_id = d.department_id AND d.location_id = l.location_id AND lower(department_name) LIKE '%it%';
```

* OUTER JOIN 표준 문법

  ```sql
  // employees에 NULL포함 조인해서 출력하고 싶을때 where 절 department에 (+) 삽입을 표준문법으로 작성
  SELECT employee_id, first_name,department_name, e.department_id, department_name FROM employees e LEFT OUTER JOIN departments d ON e.department_id = d.department_id;
  ```





#### SELF JOIN

* 자기 자신의 테이블을 자신과 조인한다는 의미
* 별도의 구문이 있는것은 아님

```sql
SELECT employee_id, manager_id FROM employees;

//employees 테이블에서 스스로 비교했을때 상사가 누구인지 조회
SELECT me.employee_id, me.first_name, me.manager_id, man.employee_id, man.first_name FROM employees me, employees man WHERE me.manager_id = man.employee_id;


//내 상사보다 급여를 많이 받는 사원의 이름 급여 조회
SELECT me.first_name, me.salary, man.first_name, man.salary FROM employees me, employees man WHERE me.manager_id = man.employee_id AND me.salary > man.salary;
```

