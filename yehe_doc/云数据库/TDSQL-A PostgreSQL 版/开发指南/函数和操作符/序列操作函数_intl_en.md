Sequence objects, also called sequence generators or just sequences, are special single-row tables created with `CREATE SEQUENCE`. Sequence objects are commonly used to generate unique identifiers for rows of a table.
As sequences are non-transactional, changes made by `setval` will not be undone if the transaction rolls back.
Common sequence functions are as listed below:

| **Function**                                    | **Return Type** | **Description**                                  |
| ------------------------------------------- | ---------- | ----------------------------------------- |
| currval(regclass)                         | bigint     | Returns value most recently obtained with `nextval` for specified sequence |
| lastval()                                   | bigint     | Returns value most recently obtained with `nextval` for any sequence |
| nextval(regclass)                         | bigint     | Advances sequence and returns new value                        |
| setval(regclass,   bigint)              | bigint     | Sets sequence's current value                          |
| setval(regclass,   bigint,   boolean) | bigint     | Sets sequence's current value and `is_called` flag       |

Sample code:
```
postgres=# CREATE SEQUENCE seq;
CREATE SEQUENCE
postgres=# SELECT nextval('seq');
 nextval 
---------
    1
(1 row)
 
postgres=# SELECT nextval('seq');
 nextval 
---------
    2
(1 row)
 
postgres=# SELECT currval('seq');
 currval 
---------
    2
(1 row)
 
postgres=# SELECT setval('seq',188);
 setval 
--------
  188
(1 row)
 
postgres=# SELECT currval('seq');
 currval 
---------
   188
(1 row)
 
postgres=# SELECT lastval();
 lastval 
---------
   188
(1 row)
```
