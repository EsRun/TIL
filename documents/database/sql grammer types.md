# sql 문법

## 종류

- DDL : Data Definition Language
- DML : Data Manipulation Language
- DCL : DATA Control Language
- DQL : Data Query Language(DML에 포함)
- TCL : Transaction Control Language(DCL에 포함)

## DDL
- 데이터베이스 구조 정의에 사용되는 언어
- 테이블 작업을 할 때 사용
- Create(생성), Alter(구조 변경), Drop(삭제), Truncate(초기화), Rename(이름 변경)

## DML
- 데이터 조작에 사용되는 언어
- 저장된 데이터를 다루는 작업을 할 때 사용
- Select(DQL, 조회), Insert(삽입), Update(수정), Delete(삭제)

## DCL
- 데이터베이스 접근 권한에 사용되는 언어
- 각종 권한의 부여 및 회수에 사용
- Grant(권한 부여), Revoke(권한 회수)

## TCL
- DCL 중 트랜잭션을 컨트롤하는 명령어
- Commit(반영), RollBack(되돌림), SavePoint(저장점 지정)