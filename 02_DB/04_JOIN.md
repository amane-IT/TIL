# Join
## 정의
- 둘 이상의 테이블에서 데이터가 필요한 경우 join
- join의 조건은 **on** 절에 작성
- 조건은 일반적으로 PK와 FK로 구성

## 종류
### Inner Join
- 가장 일반적인 종류
- 동등 조인
- N - 1개의 조건 필요
- 연결 조건절
  + **ON** 키워드
    * on **T1.PK 컬럼 = T2.FK 컬럼**의 형식으로 join조건 지정
  + **using**키워드
    * using(공통 칼럼명)
    * using의 경우, 사용자가 직접 연결하는 것이 아니라서 조건이 꼬일 수 있음

### NATURAL JOIN
- 권장 X
- 일일이 테이블 구조를 살펴봐야 함
- 테이블의 공통적인 필드를 가지고 join

### Outer Join
- 어느 한 쪽 테이블에서는 데이터가 존재하는데 다른 쪽 테이블에서는 존재하지 않는 경우, 해당 데이터가 검색되지 않는 문제점 해결
- 기준에 따라 **LEFT JOIN / RIGHT JOIN / FULL JOIN**으로 구분
  + FULL OUTER JOIN은 MYSQL에서 제공하지 않음

![image](https://user-images.githubusercontent.com/48676089/151801757-b17a7531-0c1b-4351-a052-7923adeea264.png)

### SELF JOIN
- 같은 테이블끼리 JOIN
- 같은 테이블 내의 다른 칼럼의 데이터와 비교하여 결과 출력 시 사용

### Non-Equi JOIN
- 테이블의 PK, FK가 아닌 일반 칼럼을 join 조건으로 지정
- 두 테이블 간에 칼럼 값들이 서로 정확하게 일치하지 않는 경우 사용
- **Between, >, >=, <, <=** 등 연산자로 JOIN 수행
