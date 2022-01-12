## connect 

\> sqlplus

\> sqlplus /"as sysdba"

\> alter user {user} identified by {pwd};

\> conn {user}/{pwd}

\> desc {table};

\> column {column} format a{%d};

## select

>AND / OR / (NOT) BETWEEN .. AND / =, '<>, !=, ^=' / (NOT) IN

>round({num}, 2)

\> select * from user_objects where object_type = 'view';

\> select {column} as {nick} from {table} where {condition};

<br/>

>(NOT) LIKE

\> select {column} from {table} where {column} like '2020%'/'___s_';

<br/>

>ORDER BY, GROUP BY

\> select * from {table} order by {column}, {column} desc;

\> select * from {table} where {condition} group by {column}, {column} having {group condition};

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

\> select substr('20200112', 1, 4) from dual;

\> select '2020-'||rownum from dual connect by level<=3;

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


