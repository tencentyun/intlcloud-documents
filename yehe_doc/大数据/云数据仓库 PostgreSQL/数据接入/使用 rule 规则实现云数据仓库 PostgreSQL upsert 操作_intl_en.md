## Background
The underlying structure of CDWPG is built on Greenplum 6. The PostgreSQL kernel is v9.4, and its `INSERT .. ON CONFLICT` feature cannot be well supported for now. This document describes how to use a PostgreSQL rule to `UPSERT`, as it requires a different method.

## Rule Overview
The PostgreSQL rule system allows one to define an alternative action to be performed on insertions, updates, or deletions in database tables. Roughly speaking, a rule causes additional commands to be executed when a given command on a given table is executed. Alternatively, an `INSTEAD` rule can replace a given command by another, or cause a command not to be executed at all. Rules are used to implement table views as well. A rule is really a command transformation mechanism, or command macro. The transformation happens before the execution of the command starts.

For more information, see [CREATE RULE](https://www.postgresql.org/docs/9.4/sql-createrule.html).

## `UPSERT` Rule
To implement an `UPSERT` operation, you need a rule that determines whether a corresponding record already exists during `INSERT`, allows for `UPDATE` if yes, and allows for `INSERT` if no.

The following database instance is used as an example:

Create a test database.
```
CREATE TABLE my_test(
   id integer,
   num1 integer,
   num2 decimal,
   str1 varchar(20),
   str2 text,
   PRIMARY KEY(id)
) distributed by (id);
```
Then, add a rule to the table.
```
create rule r1 as on insert to my_test where exists (select 1 from e t1 where t1.id=NEW.id limit 1) do instead update my_test set num1=NEW.num1,num2=NEW.num2,str1=NEW.str1,str2=NEW.str2 where id=NEW.id;
```
This rule is for the `INSERT` operation. If the `id` in the new `INSERT` statement already exists, the original data will be updated with the value inside the new `INSERT`, i.e., the `NEW.XXX` that can be seen after the operation. In this case, no errors will be reported due to the primary key constraint, and the `UPDATE` operation will be performed.
```
\d my_test
                                   Table "public.my_test"
 Column |         Type          | Collation | Nullable |               Default               
--------+-----------------------+-----------+----------+-------------------------------------
 id     | integer               |           | not null | nextval('my_test_id_seq'::regclass)
 num1   | integer               |           |          | 
 num2   | numeric               |           |          | 
 str1   | character varying(20) |           |          | 
 str2   | text                  |           |          | 
Indexes:
    "my_test_pkey" PRIMARY KEY, btree (id)
Rules:
    r1 AS
    ON INSERT TO my_test
   WHERE (EXISTS ( SELECT 1
	 FROM my_test my_test_1
 	WHERE my_test_1.id = new.id
	 LIMIT 1)) DO INSTEAD  UPDATE my_test SET num1 = new.num1, num2 = new.num2, str1 = new.str1, str2 = new.str2
```


## Notes
The rule is subject to the following limits:
1. Bulk insert may not be proper. If the statement does not set a unique constraint or primary key constraint, duplicate data may be generated during bulk insert. Therefore, you should avoid using bulk insert. When using it, avoid determining whether the fields of `UPSERT` are not duplicated or add unique constraints to the fields that need to be determined. As shown in the following example, if there is no primary key constraint on the `id`, there may be duplicate data after execution.
```
insert into my_test (id,num1,num2,str1,str2)values(1,2,1.0,'111','555'),(1,3,2.0,'111','666');
```
2. The rule does not support the `COPY` statement, which may also cause duplicate data just like bulk insert.
3. When you set the `UPDATE` rule, if the rule usage is configured, but the `INSERT` statement does not pass in the `num1` and `num2` fields, these two fields will be null after `UPDATE`, resulting in the loss of the original data.
```
update my_test set num1=NEW.num1,num2=NEW.num2,str1=NEW.str1,str2=NEW.str2
```
