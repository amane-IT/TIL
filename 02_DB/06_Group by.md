
## 집계함수
- 하나 이상의 행을 그룹으로 묶어 연산
- sum: 그룹의 누적합계 반환
- avg: 그룹의 평균 반환
- count: 그룹의 총 개수 반환
  + null값은 제외하고 counting 됨
- max: 그룹의 최대값 반환
- min: 그룹의 최소값 반환

     
## Group by
- 쿼리된 테이블의 행을 그룹으로 묶음
- 선택 목록의 집계함수를 각 행 그룹에 적용 -> 그룹의 단일 결과 행 반환
- Group by 생략 시, **전체 행**을 대상으로 집계함수 결과 반환

### 실행 순서
> from -> where -> group by -> having -> select -> order by

    
## Having 절
- group by한 결과의 조건을 추가하는 것
- 집계 함수의 조건을 작성
  + where 절이 group by 절보다 먼저 실행되기 때문

## Set (집합 연산자)
- 모든 집합 연산자는 동일한 우선 순위를 가짐
- select 절에 있는 column의 개수와 type 일치해야 함

|연산자|설명|set|
|:---:|:-------:|:----:|
|UNION|두 쿼리에서 선택된 모든 행 반환 **(중복불가)**|합집합|
|UNION ALL|두 쿼리에서 선택된 모든 행 반환 **(중복 포함)**|합집합|
|INTERSECT|두 쿼리에서 선택된 모든 중복행 반환 ***MySQL 지원 X***|교집합|
|MINUS|첫번째 쿼리에서 선택한 행 반환 (중복 불가) ***MySQL 지원 X***|차집합|

```MySQL
select employee_id, first_name, salary
from employees
where department_id in (10, 20, 30)
UNION
select employee_id, first_name, salary
from employees
where salary > (
                  select sum(salary)
                  from employees
                  where department_id = 70
                );
```
