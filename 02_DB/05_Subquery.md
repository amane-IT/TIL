# 서브쿼리
- 다른 쿼리 내부에 포함되어 있는 SELECT문
- 서브쿼리는 비교 연산자의 오른쪽에 기술해야 함

## 주의사항
- 반드시 괄호로 감싸져 있어야 함
- 단일행 or 다중행 비교 연산자와 함께 사용

## 종류
### 1. 중첩 서브 쿼리 (**Nested Subquery**)
- ***where***문에 작성하는 서브 쿼리
- 단일행, 복수행, 다중 컬럼...
  + **IN** 키워드: 조건에 만족하는 서브 쿼리의 결과를 리턴
  + **ANY** 키워드: 적어도 하나의 조건을 만족하면 true
  + **ALL** 키워드: 모든 조건을 만족하면 true
    
### 2. 인라인 뷰 (**Inline View**)
- ***from***문에 작성하는 서브 쿼리
- 뷰(View)처럼 결과가 동적으로 생성된 테이블로 사용 가능
- 임시 뷰이기 때문에 DB에 저장 X
- 컬럼을 자유롭게 참조 가능
- Top N(MSSQL), Limit N(MySQL), RowNum <= N (Oracle)...
    
### 3. 스칼라 서브 쿼리 (**Scalar Subquery**)
- ***select***문에 작성하는 서브 쿼리
- 하나의 행만 반환

## Create
- create table 테이블 명 select (추가할 칼럼) from 테이블 명2 where (추가할 데이터 조건)

## Insert
- Insert into (추가할 칼럼) 테이블 명 select (추가할 칼럼) from 테이블 명2 where(추가할 데이터 조건)

## Update
- Update 테이블 명 set (바꿀 내용) where (조건 (select (조건 칼럼) from 테이블 명2))

## Delete
- Delete from 테이블 명 where (조건(select (조건 칼럼) from 테이블 명2))
