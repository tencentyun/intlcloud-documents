## Text Search Operators
| **Operator** | **Return Type** | **Description**                      |
| ---------- | ------------ | ----------------------------- |
| @@         | bool         | Does `tsvector` match `tsquery`? |
| @@@        | bool         | Same as `@@`                          |
| \|\|       | tsvector     | Concatenates tsvector                |
| &&         | tsquery      | AND `tsquery` values together    |
| \|\|       | tsquery      | OR `tsquery` values together     |
| !!         | tsquery      | Negates a `tsquery`           |
| <->        | tsquery      | `tsquery` followed by `tsquery`    |
| @>         | bool         | Does `tsquery` contain another?    |
| <@         | bool         | Is `tsquery` contained in?         |

Sample code:
```
postgres=# SELECT to_tsvector('fat cats ate rats') @@ to_tsquery('cat & rat');
 ?column? 
----------
 f
(1 row)
 
postgres=# SELECT 'a:1 b:2'::tsvector || 'c:1 d:2 b:3'::tsvector;
     ?column?     
---------------------------
 'a':1 'b':2,5 'c':3 'd':4
(1 row)
 
postgres=# SELECT 'fat | rat'::tsquery && 'cat'::tsquery;
     ?column?     
---------------------------
 ( 'fat' | 'rat' ) & 'cat'
(1 row)
 
postgres=# SELECT !! 'cat'::tsquery;
 ?column? 
----------
 !'cat'
(1 row)
 
postgres=# SELECT to_tsquery('fat') <-> to_tsquery('rat');
  ?column?  
-----------------
 'fat' <-> 'rat'
(1 row)
 
postgres=# SELECT 'cat'::tsquery @> 'cat & rat'::tsquery;
 ?column? 
----------
 f
(1 row)
```

## Text Search Function
| **Function**                                                     | **Return Type** | **Description**                                    |
| -------------------------------------------------- | ------------ | ------------------------------------ |
| array_to_tsvector(text[])                                  | tsvector     | Converts the array of lexemes to `tsvector`                  |
| get_current_ts_config()                                      | regconfig    | Gets default text search configuration                        |
| length(tsvector)                                           | integer      | Specifies the number of lexemes in `tsvector`                        |
| numnode(tsquery)                                           | integer      | Specifies the number of lexemes plus operators in `tsquery`             |
| querytree(query tsquery)                                 | text         | Gets the indexable part of a `tsquery`               |
| setweight(tsvector, "char")                              | tsvector     | Assigns weight to each element in `tsvector`            |
| to_tsquery([ config regconfig , ]   query text)      | tsvector     | Normalizes words and converts to `tsquery`                  |
| to_tsvector([ config regconfig, ]   document text)  | tsvector     | Reduces document text to `tsvector`                    |
| ts_delete(vector tsvector,   lexeme text)            | tsvector     | Removes given `lexeme` from `vector`         |
| ts_filter(vector tsvector,   weights "char"[])       | tsvector     | Selects only elements with given weights from `vector` |
| ts_rewrite(query tsquery,   targettsquery,   substitute tsquery) | tsquery      | Replaces `target` with `substitute` within query     |
| ts_rewrite(query tsquery,   selecttext)                | tsquery      | Replaces by using targets and substitutes from a `SELECT` command  |
| tsvector_to_array(tsvector)                         | text[]       | Converts `tsvector` to array of lexemes                  |

Sample code:
```
postgres=# SELECT array_to_tsvector('{fat,cat,rat}'::text[]);
array_to_tsvector
-------------------
 'cat' 'fat' 'rat'
(1 row)
 
postgres=# SELECT get_current_ts_config();
 get_current_ts_config 
-----------------------
 simple
(1 row)
 
postgres=# SELECT length('fat:2,4 cat:3 rat:5A'::tsvector);
 length 
--------
   3
(1 row)
 
postgres=# SELECT querytree('foo & ! bar'::tsquery);
 querytree 
-----------
 'foo'
(1 row)
 
postgres=# SELECT to_tsquery('english', 'The & Fat & Rats');
 to_tsquery 
---------------
 'fat' & 'rat'
(1 row)
 
postgres=# SELECT ts_delete('fat:2,4 cat:3 rat:5A'::tsvector, 'fat');
  ts_delete   
------------------
 'cat':3 'rat':5A
(1 row)
 
postgres=# SELECT tsvector_to_array('fat:2,4 cat:3 rat:5A'::tsvector);
 tsvector_to_array 
-------------------
 {cat,fat,rat}
(1 row)
```
Above are some text search functions supported by TDSQL-A for PostgreSQL. For more information, please see [Text Search Functions and Operators](http://www.postgres.cn/docs/10/functions-textsearch.html).
