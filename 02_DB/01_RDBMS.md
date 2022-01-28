# RDBMS
> 관계형 데이터베이스 시스템
> Relational Database System

## Table based DBMS
- 테이블 단위로 데이터 관리
- 중복 데이터 최소화
  + 같은 데이터가 중복으로 존재하는 경우, 데이터 수정 시 문제 발생 가능성 UP -> **정규화**로 중복 데이터 줄임
- 여러 테이블에 분산된 데이터를 테이블 간의 관계(**JOIN**)를 이용해 검색

- - -
# SQL
- DB에 있는 정보를 사용할 수 있도록 지원하는 질의어
- 모든 DBMS에서 사용 가능
- 대소문자 구분X (**데이터 대소문자는 구분**)

## DML
- Database Manipulation Language
- CRUD(Insert, Select, Update, Delete)
  + **INSERT into** 테이블이름(칼럼1, 칼럼2, ... , 칼럼N) **values** ( ?, ?, ... , ? );
  + **SELECT** * from 테이블이름
  + **UPDATE** 테이블이름 **set** 바꿀 내용
  + **DELETE from** 테이블 이름
- 데이터 조작 가능
    
### WHERE 절
- DML에서 조건에 만족하는 레코드만 가져오게 하기 위한 조건절
- 조건 설정 키워드
  + AND / OR / NOT
  + IN
    * 괄호 안에 필터링 하고 싶은 조건을 대입
      -> where 컬럼명 [NOT] IN ( ?, ?, ? )
  + BETWEEN
    * 조건의 범위 설정
      -> where 컬럼명 범위1 BETWEEN 범위2
  + NULL 비교
    * Null값은 = 연산자로는 필터링할 수 없음
    * 그래서 IS NULL과 IS NOT NULL로 필터링
  + LIKE
    * 문자열에 포함한 내용을 검색하고 싶을 때 와일드 카드와 함께 사용
    * |표시|설명|
      |:---:|:----|
      |%x%|문자열 안에 x가 들어있음|
      |x%|x로 시작하는 문자열|
      |%x|x로 끝나는 문자열|
      |_|언더바 하나에 문자 하나를 의미|

### ORDER BY절
- ORDER BY 컬럼명: 컬럼명을 기준으로 오름차순 정렬을 시킨다
- DESC를 붙이면 내림차순 정렬
- 정렬기준은 복수 개도 

## DDL
- Database Definition Language
- 데이터베이스 객체의 구조 정의
- Create, Alter, Drop이 포함
  + **CREATE DATABASE** DB이름 [default character set 값 collate 값]
    * CHARACTER SET: 컴퓨터에 어떤 **코드**로 저장할 것인지에 대한 규칙 집합
    * COLLATE: DB의 데이터 문자들을 서로 **비교**할 때 사용하는 규칙 집합
    * utf8mb3: 다국어 처리
    * utf8mb4: 이모지까지 처리
   
  + **ALTER TABLE** 테이블이름
    * 컬럼 추가: ADD COLUMN 컬럼이름 속성
    * 컬럼 변경: MODIFY COLUMN 컬럼이름 속성
    * 컬럼 이름까지 변경: CHANGE COLUMN 원래이름 바꿀이름 속성
    * 컬럼 삭제: DROP COLUMN 컬럼이름
    * 테이블 이름 변경: RENAME 새로운이름

  + **DROP DATABASE** DB이름
  + **USE** DB이름 
    
- 주요 조건
  + NOT NULL
  + DEFAULT value: 전달된 값이 없을 경우, 해당 값으로 설정
  + UNSIGNED: 숫자 타입인 경우 해당. 0과 양수로 제한
  + AUTO INCREMENT: 새 레코드가 추가될 때마다 자동으로 1씩 증가시켜 저장시킴
  + PRIMARY KEY(컬럼이름): 테이블에서 컬럼을 **고유하게 식별**하기 위해 사용.
  + UNIQUE: 컬럼에 **중복된 값 저장 불가능**. NULL은 가능
  + FORIEGN KEY: 특정 테이블의 **PK 값**만 저장 -> references로 어떤 데이터를 참조하는지 지정

## DCL
- Database Control Language
- 특정 사용자에 대한 접근권한이나 CRUD권한 정의
  + **GRANT**: 권한 부여
  + **REVOKE**: 권한 취소

## TCL
- Transaction Control Language
- 논리적 연산단위 제어
  + **COMMIT**: 실행한 쿼리를 최종적으로 적용
  + **SAVEPOINT**:
    * ROLLBACK시 트랜잭션의 시작이 아닌 savepoint까지 rollback시킬 수 있다.
    * 여러 개 생성 가능
  + **ROLLBACK**: 실행한 쿼리를 마지막 commit (or savepoint) 전으로 취소시켜 데이터 복구
