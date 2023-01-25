## Insert
1. **Just copy data from gener table 
to new _generes but not the				 constrained and create a table;**
```
select * into new_geners from gener;
```
2. **insert data from other table**
```
inset into new_geners 
select * from geners where id in (1,2)
```
## Delete

1. **delete from table**
```
delete from new_gener;
```
drop table new_geners ---> delete the whole table

truncate table new_geners----> will delete the data and free the space but 
	will not let you delete if there is a foriegn key constraint

truncate table new_geners cascade ---> will delete the data from the both 
side on main table and reference table


truncate table geners restart identity cascade;---> will also restart or 
delete the data of sequence and restart the sequence
 
insert into geners(name) select name from new_geners2 where id in (1,2);
--->insert values into table from diff table with the help of select
 statetment

In---> it is used to enter multiple values or get multiple values
from sub query

select distinct title,release_date,language from movies ---> will get 
distinct data

###IMP 
cascade will not run with delete command
----------------------------------------

delete from movies where movie_id = 2;----> wil delete the data from table
					    acc to cond.

alter table geners 
add constraint unq_geners_name unique(column_name)----> will add constraint
on column For ex we add unique constraints on column name 

alter table geners
drop constraint costraint name ---> will drop the constraint

select mv.title,g.name from movies mv inner join movie_geners mg on mv.id = mg.movie_id inner join 
geners g on mg.gener_id = g.id 
where mv.title = 'Sholay'; 

///Union will give unique column
select name from geners
union
select name from movies;

//Union all will give all values even duplicate
select name from geners
union all
select name from movies;

//except will perform minus
select name from geners
except
select name from movies;

//intersect will give intersection between two column
select name from geners
intersect
select name from movies;


## IMP
By using select we get records
but by using agg func we get sumary of records
##


## IMP
whenever you are using aggregate function with a column , you need to 
add the group by and need add that column in grp by

ex--> select year,count(*) from movies group by year;
##


## Order By
Order by is used to order the set
ex--> select year,count(*) from movies group by year order by year;
##

## for getting null
ex--> select * from movies where title is null;
##


## for getting not null
ex--> select * from movies where title is not null;
##

## self  join
ex-->
##

##with query,inner query ,sequence,view ---> To be continued...
##like and ilike

ilike is used for ignoring case

//wild card character
%-->
_-->

like
##

##Having 
it is used to when we need to implement the conditions on group by
##

##View
It is used to create For security purpose for giving access to specific columns
ex -->

**command
create view v_top_rated_movies
as
<Query>

-----

## Explain 
It will Give a Query Plan
It is used to Optimize and debug the query 

for example when the sequential search is applied

**command**

>```explain <Query>```

**example**

```
explain select mv.id, mv.title, mv.release_date from movies mv
where mv.id in (select movie_id from ratings group by movie_id having count(*) > 1)
```
-------

## Triggers
Trigger Type

insted of 

----------

## Role

### Create 

Creating a role

**comand**
>`create role "UserName" with password = 'password'`

**example**
```
create role mvName with password='password'
```
### Grant

**command**
>`GRANT {Permission} ON {SOMETING} TO "USERNAME";`

**example**
```
GRANT INSERT ON films TO PUBLIC;
```
### Alter
ALTER ROLE — change a database role

**command**
>`ALTER ROLE "USER" WITH {OPTIONS}[....];`

**example**

1. **Change a role's password:** 
```
ALTER ROLE davide WITH PASSWORD 'hu8jmn3';
```
2. **Give Acces to Login:** 
```
ALTER ROLE davide WITH LOGIN;
```


## SEQUENCE 
```
create sequence  sequence_name increment 5 start 20 maxvalue 30 cycle;
```
>[start,increment,minvalue,maxvalue,cycle]*

## DATA TYPE
**BOOL**
>y,t,1,yes for true

>n,f,0,no for false

>space for null

**TEXT**
>char --> padding is done

>varChar --> padding is not done

>text --> unlimited length

**INTEGER**
>**SMALLINT** --> range -32,768 to 32,767 has size of 2 byte

>**INT** --> range -2,147,483,648 to 2,147,483,647 has size of 4 byte

>**SERIAL** --> integer except these are automatically generated

**FLOATING POINT**
>**FLOAT(N)** --> float with n precision and have max of 8 byte

`Example`
```Postgres
prd float(5);
```

>**REAL** --> 4 byte floating point numbers

`Example`
```Postgres
prd real;
```
>**N(d,p)** --> These are generally precise.

`Example`
```Postgres
prd numeric(5,4);
```

**TEMPORAL DATA TYPE**
>**DATE** --> It is used to store date

>**TIME** --> It is used to stores the time of day values

>**TIMESTAMP** --> used to store both date and time values

>**TIMESTAMPZ** --> timestamp with time zones


**ARRAY**

`SYNTAX`
```Postgres
CREATE TABLE sal_emp (
    name            text,
    pay_by_quarter  integer[],
    schedule        text[][]
);

CREATE TABLE tictactoe (
    squares   integer[3][3]
);

pay_by_quarter  integer ARRAY;

pay_by_quarter  integer ARRAY[4];
```


`EXAMPLE`
```Postgres
INSERT INTO sal_emp
    VALUES ('Bill',
    '{10000, 10000, 10000, 10000}',
    '{{"meeting", "lunch"}, {"training", "presentation"}}'),
	('Bill',
    '{10000, 10000, 10000, 10000}',
    '{{"meeting", "lunch"}, {"training", "presentation"}}');
```	
### TIMEZONE
`Examples`
>Set the timezone
```Postgres
SET timezone = "ASIA/KOLKATA"
```
>Show current timezone
```Postgres
SELECT NOW();
```
>To get the time of day in the string format, you use the timeofday() function.
```Postgres
SELECT TIMEOFDAY();
```

>To convert 2016-06-01 00:00 to America/New_York timezone, you use the timezone() function as follows:
```Postgres
SELECT timezone('America/New_York','2016-06-01 00:00');
```
### ENUM
**CREATING ENUM**

`Tip:`Naming convention should be in plural like days,genders...etc.

>Creating Enum

`Syntax`
```Postgres
create type genders as enum ('FEMALE','MALE');
```
> Alter table for Enum 

`Syntax`
```Postgres
alter table actors alter COLUMN gender type genders using gender::genders;
```

> Find Values of enum


`Syntax`
```Postgres
select enum_range(null::genders);
```
>list all the data types

`Syntax`
```Postgres
\dT
```
>Add Values to Enum

`Syntax`
```Postgres
Alter type genders add value 'NOT_SPECIFIED';
```
>Rename Values of Enum

`Syntax`
## **OPERATORS**
### CONDITION OPERATORS
`And:` both condition must be satisfied.

`OR:` either condition must be satisfied.

`NOT:` except that condition.

`ORDER OF EXECUTION`

>IN -> BETWEEN -> LIKE -> NOT EQUALITY(<>) -> EQUALITY(=) -> NOT -> AND ->OR


