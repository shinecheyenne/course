## SQL의 분류

### DML(Data Manipulation Language: 데이터 조작 언어)

* 데이터를 조작하는 데 사용되는 sql문
* select, insert, update, delete
* 트랜잭션이 발생하는 sql도 dml에 해당

### DDL(Data Definition Language: 데이터 정의 언어)

* 데이터베이스, 테이블, 뷰, 인덱스 등의 데이터베이스 객체를 생성/삭제/변경하는 sql문 
* create, drop, alter
* DDL은 트랜잭션을 발생시키지 않아 rollback, commit 시킬 수 없다. 즉, 실행 즉시 oracle에 적용됨

### DCL(Data Control Language: 데이터 제어 언어)

* 사용자에게 권한을 부여하거나 빼앗을 때 사용하는 구문
* grant, revoke, deny 

## connect

\> sqlplus

\> sqlplus /"as sysdba"

\> conn {user}/{pwd}

## create 

\> create user {user} identified by {pwd}
      default tablespace users temporary tablespace temp;
      
\> create table {table} (... , {column} {type} defalt {value});

\> create table {table} as (select ....);

\> create sequence {name} start with {%d} increment by {%d}; -> {name}.nextval: 1,2,3,...

\> create sequence {name} start with {%d} increment by {%d} minvalue {%d} maxvalue {%d} cycle nocache;

\> grant connect, resource, dba to {user};

\> alter user {user} identified by {pwd};

\> desc {table};

\> column {column} format a{%d};

\> column {column} format 0000;

## select

>AND / OR / (NOT) BETWEEN .. AND / =, '<>, !=, ^=' / (NOT) IN / ANY, ALL, SOME

>round({num}, 2)

\> select * from user_objects where object_type = 'view';

\> select {column} as {nick} from {table} where {condition};

<br/>

>(NOT) LIKE

\> select {column} from {table} where {column} like '2020%'/'___s_';

<br/>

>ORDER BY, GROUP BY, ROULLUP(), GROUPING_ID(), CUBE()

\> select * from {table} order by {column}, {column} desc;

\> select * from {table} where {condition} group by {column}, {column} having {group condition};

\> select {colum}, grouping_id({column}) from {table} group by rollup ({column});

\> select {column} from {table} group by cube({column}, {column});


<br/>

>DISTINCT

\> select distict {column} from {table};

<br/>

>JOIN / LEFT JOIN / RIGHT JOIN / FULL OUTER JOIN

\> select {table1 nick}.{column} from {table1} {nick} join {table2} {nick} on {table1 nick}.{column} = {table2 nick}.{column} where {condition};

\> select {table1 nick}.{column} from {table1} {nick}, {table2} {nick} where {table1 nick}.{column} = {table2 nick}.{column};

<br/>

>CASE

\> select {column} 
   case {column} when {value} then {newValue}
                 when {value} then {newValue}
                 else {newValue}
   end as {new column name}
   from {table};
   
<br/>
   
>DUAL

\> select rownum from dual connect by level<=10;

\> select to_char(sysdate, 'YYYY-MM-DD') from dual;

\> select {sequence}.currval from dual;

\> select substr('20200112', 1, 4) from dual;

\> select '2020-'||rownum from dual connect by level<=3;

\> select * from {table} where rownum<=5;

cf. select * from {table} sample({percent});

<br/>

>NULL

\> select {column} from {table} where {column} is not null; 

## update

\> update {table} set {column} = {newValue} where {condition};

\> commit;

## insert

\> insert into {table} values ({value1}, {value2}, ...);

\> insert into {table} ({column1} {column2}) ({value1}, {value2});

\> insert into {table} select {column1}, {column2} from {table} where {condition};

\> insert (all|first) when {condition1} then into {table1}
                      when {condition2} then into {table2}
                      else into {table}
   select {column} from {table} where {condition};

## delete

\> delete from {table} where {condition};

\> delete from {table} where {condition} and rownum <=2;

\> delete from {table}; commit; //트랜잭션 로그를 기록하는 작업 때문에 시간이 오래 걸림

\> drop table {table}; //테이블 자체를 삭제

\> truncate table {table}; //트랜잭션 로그를 기록하지 않아 속도가 
