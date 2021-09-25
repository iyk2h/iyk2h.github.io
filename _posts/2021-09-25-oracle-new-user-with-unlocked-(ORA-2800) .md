sql 접속

SQL> conn sys /Oradoc_db1 as sysdba



오라클 12C부터는 공통 사용자 생성시 계정명 앞에 접두사로 `c##`을 붙여주어야 한다.

오라클 11버전처럼 생성하고 싶은경우 아래 명령어 입력 (dba권한 계정으로)

SQL> alter session set "_ORACLE_SCRIPT"=true;



user 생성

SQL> create user test identified by test;



user 권한 부여

SQL> grant connect, resource, dba to test;



rock상태도 해제 권한을 부여

SQL> alter user test identified by test account unlock;

