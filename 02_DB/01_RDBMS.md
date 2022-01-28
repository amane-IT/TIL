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

## DDL
- Database Definition Language
- 데이터베이스 객체의 구조 정의
- Create, Rename, Alter, Drop이 포함
  + **CREATE DATABASE** DB이름 [default character set 값 collate 값]

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
