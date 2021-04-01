# SQL_JOIN



다음과 같은 테이블 종류를 가지고 조인 실습을 진행

#### topic

| tid  | title    | description     | author_id |
| ---- | -------- | --------------- | --------- |
| 1    | HTML     | html is...      | 1         |
| 2    | CSS      | css is ...      | 2         |
| 3    | Database | database is ... | 1         |
| 4    | oracle   | oracle is ...   | NULL      |



#### author

| aid  | name     | city   | profile_id |
| ---- | -------- | ------ | ---------- |
| 1    | egoing   | seoul  | 1          |
| 2    | leezche  | jeju   | 2          |
| 3    | blackdew | namhae | 3          |



#### profile

| pid  | title     | descruption     |
| ---- | --------- | --------------- |
| 1    | developer | developer is .. |
| 2    | designer  | designer is ..  |
| 3    | DBA       | DNA is ...      |



### LEFT OUTER JOIN

* 다음과 같은 형태로 조인을 하는 방법

![스크린샷 2021-04-01 오후 11.13.48](../md-images/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-01%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%2011.13.48.png)

```sql
SELECT * FROM topic LEFT JOIN author ON topic.author_id = author.aid
```

출력결과 











### 요약



![img](../md-images/img.png)