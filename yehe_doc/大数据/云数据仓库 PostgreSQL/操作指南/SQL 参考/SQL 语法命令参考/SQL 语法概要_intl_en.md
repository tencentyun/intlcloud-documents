### ABORT
Aborts the current transaction.

```sql
ABORT [WORK | TRANSACTION]
```

### ALTER AGGREGATE
Changes the definition of an aggregate function.

```sql
ALTER AGGREGATE name ( type [ , ... ] ) RENAME TO new_name
 
ALTER AGGREGATE name ( type [ , ... ] ) OWNER TO new_owner
 
ALTER AGGREGATE name ( type [ , ... ] ) SET SCHEMA new_schema
```

### ALTER CONVERSION
Changes the definition of a conversion.

```sql
ALTER CONVERSION name RENAME TO newname
 
ALTER CONVERSION name OWNER TO newowner
```

### ALTER DATABASE
Changes the attributes of a database.

```sql
ALTER DATABASE name [ WITH CONNECTION LIMIT connlimit ]
 
ALTER DATABASE name SET parameter { TO | = } { value | DEFAULT }
 
ALTER DATABASE name RESET parameter
 
ALTER DATABASE name RENAME TO newname
 
ALTER DATABASE name OWNER TO new_owner
```

### ALTER DOMAIN
Changes the definition of a domain.

```sql
ALTER DOMAIN name { SET DEFAULT expression | DROP DEFAULT }
 
ALTER DOMAIN name { SET | DROP } NOT NULL
 
ALTER DOMAIN name ADD domain_constraint
 
ALTER DOMAIN name DROP CONSTRAINT constraint_name [RESTRICT | CASCADE]
 
ALTER DOMAIN name OWNER TO new_owner
 
ALTER DOMAIN name SET SCHEMA new_schema
```

### ALTER EXTENSION
Change the definition of an extension that is registered in a database.

```sql
ALTER EXTENSION name UPDATE [ TO new_version ]
ALTER EXTENSION name SET SCHEMA new_schema
ALTER EXTENSION name ADD member_object
ALTER EXTENSION name DROP member_object
 
where `member_object` is:
 
  ACCESS METHOD object_name |
  AGGREGATE aggregate_name ( aggregate_signature ) |
  CAST (source_type AS target_type) |
  COLLATION object_name |
  CONVERSION object_name |
  DOMAIN object_name |
  EVENT TRIGGER object_name |
  FOREIGN DATA WRAPPER object_name |
  FOREIGN TABLE object_name |
  FUNCTION function_name ( [ [ argmode ] [ argname ] argtype [, ...] ] ) |
  MATERIALIZED VIEW object_name |
  OPERATOR operator_name (left_type, right_type) |
  OPERATOR CLASS object_name USING index_method |
  OPERATOR FAMILY object_name USING index_method |
  [ PROCEDURAL ] LANGUAGE object_name |
  SCHEMA object_name |
  SEQUENCE object_name |
  SERVER object_name |
  TABLE object_name |
  TEXT SEARCH CONFIGURATION object_name |
  TEXT SEARCH DICTIONARY object_name |
  TEXT SEARCH PARSER object_name |
  TEXT SEARCH TEMPLATE object_name |
  TRANSFORM FOR type_name LANGUAGE lang_name |
  TYPE object_name |
  VIEW object_name
 
and `aggregate_signature` is:
 
* | [ argmode ] [ argname ] argtype [ , ... ] |
  [ [ argmode ] [ argname ] argtype [ , ... ] ] 
    ORDER BY [ argmode ] [ argname ] argtype [ , ... ]
```

### ALTER EXTERNAL TABLE
Changes the definition of an external table.

```sql
ALTER EXTERNAL TABLE name RENAME [COLUMN] column TO new_column
 
ALTER EXTERNAL TABLE name RENAME TO new_name
 
ALTER EXTERNAL TABLE name SET SCHEMA new_schema
 
ALTER EXTERNAL TABLE name action [, ... ]
```

### ALTER FILESPACE
Changes the definition of a filespace.

```sql
ALTER FILESPACE name RENAME TO newname
 
ALTER FILESPACE name OWNER TO newowner
```

### ALTER FUNCTION
Changes the definition of a function.

```sql
ALTER FUNCTION name ( [ [argmode] [argname] argtype [, ...] ] ) 
   action [, ... ] [RESTRICT]
 
ALTER FUNCTION name ( [ [argmode] [argname] argtype [, ...] ] )
   RENAME TO new_name
 
ALTER FUNCTION name ( [ [argmode] [argname] argtype [, ...] ] ) 
   OWNER TO new_owner
 
ALTER FUNCTION name ( [ [argmode] [argname] argtype [, ...] ] ) 
   SET SCHEMA new_schema
```

### ALTER GROUP
Changes a role name or membership.

```sql
ALTER GROUP groupname ADD USER username [, ... ]
 
ALTER GROUP groupname DROP USER username [, ... ]
 
ALTER GROUP groupname RENAME TO newname
```

### ALTER INDEX
Changes the definition of an index.

```sql
ALTER INDEX name RENAME TO new_name
 
ALTER INDEX name SET TABLESPACE tablespace_name
 
ALTER INDEX name SET ( FILLFACTOR = value )
 
ALTER INDEX name RESET ( FILLFACTOR )
```

### ALTER LANGUAGE
Changes the name of a procedural language.

```sql
ALTER LANGUAGE name RENAME TO newname
ALTER LANGUAGE name OWNER TO new_owner
```

### ALTER OPERATOR
Changes the definition of an operator.

```sql
ALTER OPERATOR name ( {lefttype | NONE} , {righttype | NONE} ) 
   OWNER TO newowner
```

### ALTER OPERATOR CLASS
Changes the definition of an operator class.

```sql
ALTER OPERATOR CLASS name USING index_method RENAME TO newname
 
ALTER OPERATOR CLASS name USING index_method OWNER TO newowner
```

### ALTER OPERATOR FAMILY
Changes the definition of an operator family.

```sql
ALTER OPERATOR FAMILY name USING index_method ADD
  {  OPERATOR strategy_number operator_name ( op_type, op_type ) [ RECHECK ]
    | FUNCTION support_number [ ( op_type [ , op_type ] ) ] funcname ( argument_type [, ...] )
  } [, ... ]
ALTER OPERATOR FAMILY name USING index_method DROP
  {  OPERATOR strategy_number ( op_type, op_type ) 
    | FUNCTION support_number [ ( op_type [ , op_type ] ) 
  } [, ... ]
 
ALTER OPERATOR FAMILY name USING index_method RENAME TO newname
 
ALTER OPERATOR FAMILY name USING index_method OWNER TO newowner
```

### ALTER PROTOCOL
Changes the definition of a protocol.

```sql
ALTER PROTOCOL name RENAME TO newname
 
ALTER PROTOCOL name OWNER TO newowner
```

### ALTER RESOURCE QUEUE
Changes the limits of a resource queue.

```sql
ALTER RESOURCE QUEUE name WITH ( queue_attribute=value [, ... ] ) 
```

### ALTER ROLE
Changes a database role (user or group).

```sql
ALTER ROLE name RENAME TO newname
 
ALTER ROLE name SET config_parameter {TO | =} {value | DEFAULT}
 
ALTER ROLE name RESET config_parameter
 
ALTER ROLE name RESOURCE QUEUE {queue_name | NONE}
 
ALTER ROLE name [ [WITH] option [ ... ] ]
```

### ALTER SCHEMA
Changes the definition of a schema.

```sql
ALTER SCHEMA name RENAME TO newname
 
ALTER SCHEMA name OWNER TO newowner
```

### ALTER SEQUENCE
Changes the definition of a sequence generator.

```sql
ALTER SEQUENCE name [INCREMENT [ BY ] increment] 
     [MINVALUE minvalue | NO MINVALUE] 
     [MAXVALUE maxvalue | NO MAXVALUE] 
     [RESTART [ WITH ] start] 
     [CACHE cache] [[ NO ] CYCLE] 
     [OWNED BY {table.column | NONE}]
 
ALTER SEQUENCE name RENAME TO new_name
 
ALTER SEQUENCE name SET SCHEMA new_schema
```

### ALTER TABLE
Changes the definition of a table.

```sql
ALTER TABLE [ONLY] name RENAME [COLUMN] column TO new_column
 
ALTER TABLE name RENAME TO new_name
 
ALTER TABLE name SET SCHEMA new_schema
 
ALTER TABLE [ONLY] name SET 
     DISTRIBUTED BY (column, [ ... ] ) 
   | DISTRIBUTED RANDOMLY 
   | WITH (REORGANIZE=true|false)
 
ALTER TABLE [ONLY] name action [, ... ]
 
ALTER TABLE name
   [ ALTER PARTITION { partition_name | FOR (RANK(number)) 
   | FOR (value) } partition_action [...] ] 
   partition_action
```

### ALTER TABLESPACE
Changes the definition of a tablespace.

```sql
ALTER TABLESPACE name RENAME TO newname
 
ALTER TABLESPACE name OWNER TO newowner
```

### ALTER TYPE
Changes the definition of a data type.

```sql
ALTER TYPE name
   OWNER TO new_owner | SET SCHEMA new_schema
```

### ALTER USER
Changes the definition of a database role (user).

```sql
ALTER USER name RENAME TO newname
 
ALTER USER name SET config_parameter {TO | =} {value | DEFAULT}
 
ALTER USER name RESET config_parameter
 
ALTER USER name [ [WITH] option [ ... ] ]
```

### ALTER VIEW
Changes the definition of a view.

```sql
ALTER VIEW name RENAME TO newname
```

### ANALYZE
Collects statistics about a database.

```sql
ANALYZE [VERBOSE] [ROOTPARTITION [ALL] ] 
   [table [ (column [, ...] ) ]]
```

### BEGIN
Starts a transaction block.

```sql
BEGIN [WORK | TRANSACTION] [transaction_mode]
      [READ ONLY | READ WRITE]
```

### CHECKPOINT
Forces a transaction log checkpoint.

```sql
CHECKPOINT
```

### CLOSE
Closes a cursor.

```sql
CLOSE cursor_name
```

### CLUSTER
Physically reorders a heap storage table on disk according to an index. Not a recommended operation in a database.

```sql
CLUSTER indexname ON tablename
 
CLUSTER tablename
 
CLUSTER
```

### COMMENT
Defines or change the comment of an object.

```sql
COMMENT ON
{ TABLE object_name |
  COLUMN table_name.column_name |
  AGGREGATE agg_name (agg_type [, ...]) |
  CAST (sourcetype AS targettype) |
  CONSTRAINT constraint_name ON table_name |
  CONVERSION object_name |
  DATABASE object_name |
  DOMAIN object_name |
  FILESPACE object_name |
  FUNCTION func_name ([[argmode] [argname] argtype [, ...]]) |
  INDEX object_name |
  LARGE OBJECT large_object_oid |
  OPERATOR op (leftoperand_type, rightoperand_type) |
  OPERATOR CLASS object_name USING index_method |
  [PROCEDURAL] LANGUAGE object_name |
  RESOURCE QUEUE object_name |
  ROLE object_name |
  RULE rule_name ON table_name |
  SCHEMA object_name |
  SEQUENCE object_name |
  TABLESPACE object_name |
  TRIGGER trigger_name ON table_name |
  TYPE object_name |
  VIEW object_name } 
IS 'text'
```

### COMMIT
Commits the current transaction.

```sql
COMMIT [WORK | TRANSACTION]
```

### COPY
Copies data between a file and a table.

```sql
COPY table [(column [, ...])] FROM {'file' | STDIN}
     [ [WITH] 
       [BINARY]
       [OIDS]
       [HEADER]
       [DELIMITER [ AS ] 'delimiter']
       [NULL [ AS ] 'null string']
       [ESCAPE [ AS ] 'escape' | 'OFF']
       [NEWLINE [ AS ] 'LF' | 'CR' | 'CRLF']
       [CSV [QUOTE [ AS ] 'quote'] 
            [FORCE NOT NULL column [, ...]]
       [FILL MISSING FIELDS]
       [[LOG ERRORS]  
       SEGMENT REJECT LIMIT count [ROWS | PERCENT] ]
 
COPY {table [(column [, ...])] | (query)} TO {'file' | STDOUT}
      [ [WITH] 
        [ON SEGMENT]
        [BINARY]
        [OIDS]
        [HEADER]
        [DELIMITER [ AS ] 'delimiter']
        [NULL [ AS ] 'null string']
        [ESCAPE [ AS ] 'escape' | 'OFF']
        [CSV [QUOTE [ AS ] 'quote'] 
             [FORCE QUOTE column [, ...]] ]
      [IGNORE EXTERNAL PARTITIONS ]
```

### CREATE AGGREGATE
Defines a new aggregate function.

```sql
CREATE [ORDERED] AGGREGATE name (input_data_type [ , ... ]) 
      ( SFUNC = sfunc,
        STYPE = state_data_type
        [, PREFUNC = prefunc]
        [, FINALFUNC = ffunc]
        [, INITCOND = initial_condition]
        [, SORTOP = sort_operator] )
```

### CREATE CAST
Defines a new cast.

```sql
CREATE CAST (sourcetype AS targettype) 
       WITH FUNCTION funcname (argtypes) 
       [AS ASSIGNMENT | AS IMPLICIT]
 
CREATE CAST (sourcetype AS targettype) WITHOUT FUNCTION 
       [AS ASSIGNMENT | AS IMPLICIT]
```

### CREATE CONVERSION
Defines a new encoding conversion.

```sql
CREATE [DEFAULT] CONVERSION name FOR source_encoding TO 
     dest_encoding FROM funcname
```

### CREATE DATABASE
Creates a new database.

```sql
CREATE DATABASE name [ [WITH] [OWNER [=] dbowner]
                     [TEMPLATE [=] template]
                     [ENCODING [=] encoding]
                     [TABLESPACE [=] tablespace]
                     [CONNECTION LIMIT [=] connlimit ] ]
```

### CREATE DOMAIN
Defines a new domain.

```sql
CREATE DOMAIN name [AS] data_type [DEFAULT expression] 
       [CONSTRAINT constraint_name
       | NOT NULL | NULL 
       | CHECK (expression) [...]]
```

### CREATE EXTENSION
Registers an extension in a database.

```sql
CREATE EXTENSION [ IF NOT EXISTS ] extension_name
  [ WITH ] [ SCHEMA schema_name ]
           [ VERSION version ]
           [ FROM old_version ]
           [ CASCADE ]
```

### CREATE EXTERNAL TABLE
Defines a new external table.

```sql
CREATE [READABLE] EXTERNAL TABLE table_name     
    ( column_name data_type [, ...] | LIKE other_table )
     LOCATION ('file://seghost[:port]/path/file' [, ...])
       | ('gpfdist://filehost[:port]/file_pattern[#transform=trans_name]'
           [, ...]
       | ('gpfdists://filehost[:port]/file_pattern[#transform=trans_name]'
           [, ...])
       | ('gphdfs://hdfs_host[:port]/path/file')
       | ('s3://S3_endpoint[:port]/bucket_name/[S3_prefix]
             [region=S3-region]
            [config=config_file]')
     [ON MASTER]
     FORMAT 'TEXT' 
           [( [HEADER]
              [DELIMITER [AS] 'delimiter' | 'OFF']
              [NULL [AS] 'null string']
              [ESCAPE [AS] 'escape' | 'OFF']
              [NEWLINE [ AS ] 'LF' | 'CR' | 'CRLF']
              [FILL MISSING FIELDS] )]
          | 'CSV'
           [( [HEADER]
              [QUOTE [AS] 'quote'] 
              [DELIMITER [AS] 'delimiter']
              [NULL [AS] 'null string']
              [FORCE NOT NULL column [, ...]]
              [ESCAPE [AS] 'escape']
              [NEWLINE [ AS ] 'LF' | 'CR' | 'CRLF']
              [FILL MISSING FIELDS] )]
          | 'AVRO' 
          | 'PARQUET'
          | 'CUSTOM' (Formatter=<formatter_specifications>)
    [ ENCODING 'encoding' ]
      [ [LOG ERRORS] SEGMENT REJECT LIMIT count
      [ROWS | PERCENT] ]
 
CREATE [READABLE] EXTERNAL WEB TABLE table_name     
   ( column_name data_type [, ...] | LIKE other_table )
      LOCATION ('http://webhost[:port]/path/file' [, ...])
    | EXECUTE 'command' [ON ALL 
                          | MASTER
                          | number_of_segments
                          | HOST ['segment_hostname'] 
                          | SEGMENT segment_id ]
      FORMAT 'TEXT' 
            [( [HEADER]
               [DELIMITER [AS] 'delimiter' | 'OFF']
               [NULL [AS] 'null string']
               [ESCAPE [AS] 'escape' | 'OFF']
               [NEWLINE [ AS ] 'LF' | 'CR' | 'CRLF']
               [FILL MISSING FIELDS] )]
           | 'CSV'
            [( [HEADER]
               [QUOTE [AS] 'quote'] 
               [DELIMITER [AS] 'delimiter']
               [NULL [AS] 'null string']
               [FORCE NOT NULL column [, ...]]
               [ESCAPE [AS] 'escape']
               [NEWLINE [ AS ] 'LF' | 'CR' | 'CRLF']
               [FILL MISSING FIELDS] )]
           | 'CUSTOM' (Formatter=<formatter specifications>)
     [ ENCODING 'encoding' ]
     [ [LOG ERRORS] SEGMENT REJECT LIMIT count
       [ROWS | PERCENT] ]
 
CREATE WRITABLE EXTERNAL TABLE table_name
    ( column_name data_type [, ...] | LIKE other_table )
     LOCATION('gpfdist://outputhost[:port]/filename[#transform=trans_name]'
          [, ...])
      | ('gpfdists://outputhost[:port]/file_pattern[#transform=trans_name]'
          [, ...])
      | ('gphdfs://hdfs_host[:port]/path')
      FORMAT 'TEXT' 
               [( [DELIMITER [AS] 'delimiter']
               [NULL [AS] 'null string']
               [ESCAPE [AS] 'escape' | 'OFF'] )]
          | 'CSV'
               [([QUOTE [AS] 'quote'] 
               [DELIMITER [AS] 'delimiter']
               [NULL [AS] 'null string']
               [FORCE QUOTE column [, ...]] ]
               [ESCAPE [AS] 'escape'] )]
           | 'AVRO' 
           | 'PARQUET'
 
           | 'CUSTOM' (Formatter=<formatter specifications>)
    [ ENCODING 'write_encoding' ]
    [ DISTRIBUTED BY (column, [ ... ] ) | DISTRIBUTED RANDOMLY ]
 
CREATE WRITABLE EXTERNAL TABLE table_name
    ( column_name data_type [, ...] | LIKE other_table )
     LOCATION('s3://S3_endpoint[:port]/bucket_name/[S3_prefix]
            [region=S3-region]
            [config=config_file]')
      [ON MASTER]
      FORMAT 'TEXT' 
               [( [DELIMITER [AS] 'delimiter']
               [NULL [AS] 'null string']
               [ESCAPE [AS] 'escape' | 'OFF'] )]
          | 'CSV'
               [([QUOTE [AS] 'quote'] 
               [DELIMITER [AS] 'delimiter']
               [NULL [AS] 'null string']
               [FORCE QUOTE column [, ...]] ]
               [ESCAPE [AS] 'escape'] )]
 
CREATE WRITABLE EXTERNAL WEB TABLE table_name
    ( column_name data_type [, ...] | LIKE other_table )
    EXECUTE 'command' [ON ALL]
    FORMAT 'TEXT' 
               [( [DELIMITER [AS] 'delimiter']
               [NULL [AS] 'null string']
               [ESCAPE [AS] 'escape' | 'OFF'] )]
          | 'CSV'
               [([QUOTE [AS] 'quote'] 
               [DELIMITER [AS] 'delimiter']
               [NULL [AS] 'null string']
               [FORCE QUOTE column [, ...]] ]
               [ESCAPE [AS] 'escape'] )]
           | 'CUSTOM' (Formatter=<formatter specifications>)
    [ ENCODING 'write_encoding' ]
    [ DISTRIBUTED BY (column, [ ... ] ) | DISTRIBUTED RANDOMLY ]
```

### CREATE FUNCTION
Defines a new function.

```sql
CREATE [OR REPLACE] FUNCTION name    
    ( [ [argmode] [argname] argtype [ { DEFAULT | = } defexpr ] [, ...] ] )
      [ RETURNS { [ SETOF ] rettype 
        | TABLE ([{ argname argtype | LIKE other table }
          [, ...]])
        } ]
    { LANGUAGE langname
    | IMMUTABLE | STABLE | VOLATILE
    | CALLED ON NULL INPUT | RETURNS NULL ON NULL INPUT | STRICT
    | [EXTERNAL] SECURITY INVOKER | [EXTERNAL] SECURITY DEFINE
    | COST execution_cost
    | SET configuration_parameter { TO value | = value | FROM CURRENT }
    | AS 'definition'
    | AS 'obj_file', 'link_symbol' } ...
    [ WITH ({ DESCRIBE = describe_function
           } [, ...] ) ]
```

### CREATE GROUP
Defines a new database role.

```sql
CREATE GROUP name [ [WITH] option [ ... ] ]
```

### CREATE INDEX
Defines a new index.

```sql
CREATE [UNIQUE] INDEX name ON table
       [USING btree|bitmap|gist]
       ( {column | (expression)} [opclass] [, ...] )
       [ WITH ( FILLFACTOR = value ) ]
       [TABLESPACE tablespace]
       [WHERE predicate]
```

### CREATE LANGUAGE
Defines a new procedural language.

```sql
CREATE [PROCEDURAL] LANGUAGE name
 
CREATE [TRUSTED] [PROCEDURAL] LANGUAGE name
       HANDLER call_handler [ INLINE inline_handler ] [VALIDATOR valfunction]
```

### CREATE OPERATOR
Defines a new operator.

```sql
CREATE OPERATOR name ( 
       PROCEDURE = funcname
       [, LEFTARG = lefttype] [, RIGHTARG = righttype]
       [, COMMUTATOR = com_op] [, NEGATOR = neg_op]
       [, RESTRICT = res_proc] [, JOIN = join_proc]
       [, HASHES] [, MERGES]
       [, SORT1 = left_sort_op] [, SORT2 = right_sort_op]
       [, LTCMP = less_than_op] [, GTCMP = greater_than_op] )
```

### CREATE OPERATOR CLASS
Defines a new operator class.

```sql
CREATE OPERATOR CLASS name [DEFAULT] FOR TYPE data_type  
  USING index_method AS 
  { 
  OPERATOR strategy_number op_name [(op_type, op_type)] [RECHECK]
  | FUNCTION support_number funcname (argument_type [, ...] )
  | STORAGE storage_type
  } [, ... ]
```

### CREATE OPERATOR FAMILY
Defines a new operator family.

```sql
CREATE OPERATOR FAMILY name  USING index_method  
```

### CREATE PROTOCOL
Registers a custom data access protocol that can be specified when defining a database external table.

```sql
CREATE [TRUSTED] PROTOCOL name (
   [readfunc='read_call_handler'] [, writefunc='write_call_handler']
   [, validatorfunc='validate_handler' ])
```

### CREATE RESOURCE QUEUE
Defines a new resource queue.

```sql
CREATE RESOURCE QUEUE name WITH (queue_attribute=value [, ... ])
```

### CREATE ROLE
Defines a new database role (user or group).

```sql
CREATE ROLE name [[WITH] option [ ... ]]
```

### CREATE RULE
Defines a new rewrite rule.

```sql
CREATE [OR REPLACE] RULE name AS ON event
  TO table [WHERE condition] 
  DO [ALSO | INSTEAD] { NOTHING | command | (command; command 
  ...) }
```

### CREATE SCHEMA
Defines a new schema.

```sql
CREATE SCHEMA schema_name [AUTHORIZATION username] 
   [schema_element [ ... ]]
 
CREATE SCHEMA AUTHORIZATION rolename [schema_element [ ... ]]
```

### CREATE SEQUENCE
Defines a new sequence generator.

```sql
CREATE [TEMPORARY | TEMP] SEQUENCE name
       [INCREMENT [BY] value] 
       [MINVALUE minvalue | NO MINVALUE] 
       [MAXVALUE maxvalue | NO MAXVALUE] 
       [START [ WITH ] start] 
       [CACHE cache] 
       [[NO] CYCLE] 
       [OWNED BY { table.column | NONE }]
```

### CREATE TABLE
Defines a new table.

```sql
CREATE [[GLOBAL | LOCAL] {TEMPORARY | TEMP}] TABLE table_name ( 
[ { column_name data_type [ DEFAULT default_expr ] 
   [column_constraint [ ... ]
[ ENCODING ( storage_directive [,...] ) ]
] 
   | table_constraint
   | LIKE other_table [{INCLUDING | EXCLUDING} 
                      {DEFAULTS | CONSTRAINTS}] ...}
   [, ... ] ]
   )
   [ INHERITS ( parent_table [, ... ] ) ]
   [ WITH ( storage_parameter=value [, ... ] )
   [ ON COMMIT {PRESERVE ROWS | DELETE ROWS | DROP} ]
   [ TABLESPACE tablespace ]
   [ DISTRIBUTED BY (column, [ ... ] ) | DISTRIBUTED RANDOMLY ]
   [ PARTITION BY partition_type (column)
       [ SUBPARTITION BY partition_type (column) ] 
          [ SUBPARTITION TEMPLATE ( template_spec ) ]
       [...]
    ( partition_spec ) 
        | [ SUBPARTITION BY partition_type (column) ]
          [...]
    ( partition_spec
      [ ( subpartition_spec
           [(...)] 
         ) ] 
    )
```

### CREATE TABLE AS
Defines a new table from the results of a query.

```sql
CREATE [ [GLOBAL | LOCAL] {TEMPORARY | TEMP} ] TABLE table_name
   [(column_name [, ...] )]
   [ WITH ( storage_parameter=value [, ... ] ) ]
   [ON COMMIT {PRESERVE ROWS | DELETE ROWS | DROP}]
   [TABLESPACE tablespace]
   AS query
   [DISTRIBUTED BY (column, [ ... ] ) | DISTRIBUTED RANDOMLY]
```

### CREATE TABLESPACE
Defines a new tablespace.

```sql
CREATE TABLESPACE tablespace_name [OWNER username] 
       FILESPACE filespace_name
```

### CREATE TYPE
Defines a new data type.

```sql
CREATE TYPE name AS ( attribute_name data_type [, ... ] )
 
CREATE TYPE name AS ENUM ( 'label' [, ... ] )
 
CREATE TYPE name (
    INPUT = input_function,
    OUTPUT = output_function
    [, RECEIVE = receive_function]
    [, SEND = send_function]
    [, TYPMOD_IN = type_modifier_input_function ]
    [, TYPMOD_OUT = type_modifier_output_function ]
    [, INTERNALLENGTH = {internallength | VARIABLE}]
    [, PASSEDBYVALUE]
    [, ALIGNMENT = alignment]
    [, STORAGE = storage]
    [, DEFAULT = default]
    [, ELEMENT = element]
    [, DELIMITER = delimiter] )
 
CREATE TYPE name
```

### CREATE USER
Defines a new database role with the LOGIN privilege by default.

```sql
CREATE USER name [ [WITH] option [ ... ] ]
```

### CREATE VIEW
Defines a new view.

```sql
CREATE [OR REPLACE] [TEMP | TEMPORARY] VIEW name
       [ ( column_name [, ...] ) ]
       AS query
```

### DEALLOCATE
Deallocates a prepared (precompiled) statement.

```sql
DEALLOCATE [PREPARE] name
```

##### DECLARE
Defines a cursor.

```sql
DECLARE name [BINARY] [INSENSITIVE] [NO SCROLL] CURSOR 
     [{WITH | WITHOUT} HOLD] 
     FOR query [FOR READ ONLY]
```

### DELETE
Deletes rows from a table.

```sql
DELETE FROM [ONLY] table [[AS] alias]
      [USING usinglist]
      [WHERE condition | WHERE CURRENT OF cursor_name ]
```

### DISCARD
Discards the session state.

```sql
DISCARD { ALL | PLANS | TEMPORARY | TEMP }
```

### DROP AGGREGATE
Removes an aggregate function.

```sql
DROP AGGREGATE [IF EXISTS] name ( type [, ...] ) [CASCADE | RESTRICT]
```

### DO
Executes an anonymous code block as a transient anonymous function.

```sql
DO [ LANGUAGE lang_name ] code
```

### DROP CAST
Removes a cast.

```sql
DROP CAST [IF EXISTS] (sourcetype AS targettype) [CASCADE | RESTRICT]
```

### DROP CONVERSION
Removes a conversion.

```sql
DROP CONVERSION [IF EXISTS] name [CASCADE | RESTRICT]
```

### DROP DATABASE
Removes a database.

```sql
DROP DATABASE [IF EXISTS] name
```

### DROP DOMAIN
Removes a domain.

```sql
DROP DOMAIN [IF EXISTS] name [, ...]  [CASCADE | RESTRICT]
```

### DROP EXTENSION
Removes an extension from a database.

```sql
DROP EXTENSION [ IF EXISTS ] name [, ...] [ CASCADE | RESTRICT ]
```

### DROP EXTERNAL TABLE
Removes an external table definition.

```sql
DROP EXTERNAL [WEB] TABLE [IF EXISTS] name [CASCADE | RESTRICT]
```

### DROP FILESPACE
Removes a filespace.

```sql
DROP FILESPACE [IF EXISTS] filespacename
```

### DROP FUNCTION
Removes a function.

```sql
DROP FUNCTION [IF EXISTS] name ( [ [argmode] [argname] argtype 
    [, ...] ] ) [CASCADE | RESTRICT]
```

### DROP GROUP
Removes a database role.

```sql
DROP GROUP [IF EXISTS] name [, ...]
```

### DROP INDEX
Removes an index.

```sql
DROP INDEX [IF EXISTS] name [, ...] [CASCADE | RESTRICT]
```

### DROP LANGUAGE
Removes a procedural language.

```sql
DROP [PROCEDURAL] LANGUAGE [IF EXISTS] name [CASCADE | RESTRICT]
```

### DROP OPERATOR
Removes an operator.

```sql
DROP OPERATOR [IF EXISTS] name ( {lefttype | NONE} , 
    {righttype | NONE} ) [CASCADE | RESTRICT]
```

### DROP OPERATOR CLASS
Removes an operator class.

```sql
DROP OPERATOR CLASS [IF EXISTS] name USING index_method [CASCADE | RESTRICT]
```

### DROP OPERATOR FAMILY
Removes an operator family.

```sql
DROP OPERATOR FAMILY [IF EXISTS] name USING index_method [CASCADE | RESTRICT]
```

### DROP OWNED
Removes database objects owned by a database role.

```sql
DROP OWNED BY name [, ...] [CASCADE | RESTRICT]
```

### DROP PROTOCOL
Removes a external table data access protocol from a database.

```sql
DROP PROTOCOL [IF EXISTS] name
```

### DROP RESOURCE QUEUE
Removes a resource queue.

```sql
DROP RESOURCE QUEUE queue_name
```

### DROP ROLE
Removes a database role.

```sql
DROP ROLE [IF EXISTS] name [, ...]
```

### DROP RULE
Removes a rewrite rule.

```sql
DROP RULE [IF EXISTS] name ON relation [CASCADE | RESTRICT]
```

### DROP SCHEMA
Removes a schema.

```sql
DROP SCHEMA [IF EXISTS] name [, ...] [CASCADE | RESTRICT]
```

### DROP SEQUENCE
Removes a sequence.

```sql
DROP SEQUENCE [IF EXISTS] name [, ...] [CASCADE | RESTRICT]
```

### DROP TABLE
Removes a table.

```sql
DROP TABLE [IF EXISTS] name [, ...] [CASCADE | RESTRICT]
```

### DROP TABLESPACE
Removes a tablespace.

```sql
DROP TABLESPACE [IF EXISTS] tablespacename
```

### DROP TYPE
Removes a data type.

```sql
DROP TYPE [IF EXISTS] name [, ...] [CASCADE | RESTRICT]
```

### DROP USER
Removes a database role.

```sql
DROP USER [IF EXISTS] name [, ...]
```

### DROP VIEW
Removes a view.

```sql
DROP VIEW [IF EXISTS] name [, ...] [CASCADE | RESTRICT]
```

### END
Commits the current transaction.

```sql
END [WORK | TRANSACTION]
```

### EXECUTE
Executes a prepared SQL statement.

```sql
EXECUTE name [ (parameter [, ...] ) ]
```

### EXPLAIN
Shows the query plan of a statement.

```sql
EXPLAIN [ANALYZE] [VERBOSE] statement
```

### FETCH
Retrieves rows from a query using a cursor.

```sql
FETCH [ forward_direction { FROM | IN } ] cursorname
```

### GRANT
Defines access privileges.

```sql
GRANT { {SELECT | INSERT | UPDATE | DELETE | REFERENCES | 
TRIGGER | TRUNCATE } [,...] | ALL [PRIVILEGES] }
    ON [TABLE] tablename [, ...]
    TO {rolename | PUBLIC} [, ...] [WITH GRANT OPTION]
 
GRANT { {USAGE | SELECT | UPDATE} [,...] | ALL [PRIVILEGES] }
    ON SEQUENCE sequencename [, ...]
    TO { rolename | PUBLIC } [, ...] [WITH GRANT OPTION]
 
GRANT { {CREATE | CONNECT | TEMPORARY | TEMP} [,...] | ALL 
[PRIVILEGES] }
    ON DATABASE dbname [, ...]
    TO {rolename | PUBLIC} [, ...] [WITH GRANT OPTION]
 
GRANT { EXECUTE | ALL [PRIVILEGES] }
    ON FUNCTION funcname ( [ [argmode] [argname] argtype [, ...] 
] ) [, ...]
    TO {rolename | PUBLIC} [, ...] [WITH GRANT OPTION]
 
GRANT { USAGE | ALL [PRIVILEGES] }
    ON LANGUAGE langname [, ...]
    TO {rolename | PUBLIC} [, ...] [WITH GRANT OPTION]
 
GRANT { {CREATE | USAGE} [,...] | ALL [PRIVILEGES] }
    ON SCHEMA schemaname [, ...]
    TO {rolename | PUBLIC} [, ...] [WITH GRANT OPTION]
 
GRANT { CREATE | ALL [PRIVILEGES] }
    ON TABLESPACE tablespacename [, ...]
    TO {rolename | PUBLIC} [, ...] [WITH GRANT OPTION]
 
GRANT parent_role [, ...] 
    TO member_role [, ...] [WITH ADMIN OPTION]
 
GRANT { SELECT | INSERT | ALL [PRIVILEGES] } 
    ON PROTOCOL protocolname
    TO username
```

### INSERT
Creates new rows in a table.

```sql
INSERT INTO table [( column [, ...] )]
   {DEFAULT VALUES | VALUES ( {expression | DEFAULT} [, ...] ) 
   [, ...] | query}
```

### LOAD
Loads or reloads a shared library file.

```sql
LOAD 'filename'
```

### LOCK
Locks a table.

```sql
LOCK [TABLE] name [, ...] [IN lockmode MODE] [NOWAIT]
```

### MOVE
Positions a cursor.

```sql
MOVE [ forward_direction {FROM | IN} ] cursorname
```

### PREPARE
Prepare a statement for execution.

```sql
PREPARE name [ (datatype [, ...] ) ] AS statement
```

### REASSIGN OWNED
Changes the ownership of database objects owned by a database role.

```sql
REASSIGN OWNED BY old_role [, ...] TO new_role
```

### REINDEX
Rebuilds indexes.

```sql
REINDEX {INDEX | TABLE | DATABASE | SYSTEM} name
```

### RELEASE SAVEPOINT
Destroys a previously defined savepoint.

```sql
RELEASE [SAVEPOINT] savepoint_name
```

### RESET
Restores the value of a system configuration parameter to the default value.

```sql
RESET configuration_parameter
 
RESET ALL
```

### REVOKE
Removes access privileges.

```sql
REVOKE [GRANT OPTION FOR] { {SELECT | INSERT | UPDATE | DELETE 
       | REFERENCES | TRIGGER | TRUNCATE } [,...] | ALL [PRIVILEGES] }
       ON [TABLE] tablename [, ...]
       FROM {rolename | PUBLIC} [, ...]
       [CASCADE | RESTRICT]
 
REVOKE [GRANT OPTION FOR] { {USAGE | SELECT | UPDATE} [,...] 
       | ALL [PRIVILEGES] }
       ON SEQUENCE sequencename [, ...]
       FROM { rolename | PUBLIC } [, ...]
       [CASCADE | RESTRICT]
 
REVOKE [GRANT OPTION FOR] { {CREATE | CONNECT 
       | TEMPORARY | TEMP} [,...] | ALL [PRIVILEGES] }
       ON DATABASE dbname [, ...]
       FROM {rolename | PUBLIC} [, ...]
       [CASCADE | RESTRICT]
 
REVOKE [GRANT OPTION FOR] {EXECUTE | ALL [PRIVILEGES]}
       ON FUNCTION funcname ( [[argmode] [argname] argtype
                              [, ...]] ) [, ...]
       FROM {rolename | PUBLIC} [, ...]
       [CASCADE | RESTRICT]
 
REVOKE [GRANT OPTION FOR] {USAGE | ALL [PRIVILEGES]}
       ON LANGUAGE langname [, ...]
       FROM {rolename | PUBLIC} [, ...]
       [ CASCADE | RESTRICT ]
 
REVOKE [GRANT OPTION FOR] { {CREATE | USAGE} [,...] 
       | ALL [PRIVILEGES] }
       ON SCHEMA schemaname [, ...]
       FROM {rolename | PUBLIC} [, ...]
       [CASCADE | RESTRICT]
 
REVOKE [GRANT OPTION FOR] { CREATE | ALL [PRIVILEGES] }
       ON TABLESPACE tablespacename [, ...]
       FROM { rolename | PUBLIC } [, ...]
       [CASCADE | RESTRICT]
 
REVOKE [ADMIN OPTION FOR] parent_role [, ...] 
       FROM member_role [, ...]
       [CASCADE | RESTRICT]
```

### ROLLBACK
Aborts the current transaction.

```sql
ROLLBACK [WORK | TRANSACTION]
```

### ROLLBACK TO SAVEPOINT
Rolls back the current transaction to a savepoint.

```sql
ROLLBACK [WORK | TRANSACTION] TO [SAVEPOINT] savepoint_name
```

### SAVEPOINT
Defines a new savepoint within the current transaction.

```sql
SAVEPOINT savepoint_name
```

### SELECT
Retrieves rows from a table or view.

```sql
[ WITH with_query [, ...] ]
SELECT [ALL | DISTINCT [ON (expression [, ...])]]
  * | expression [[AS] output_name] [, ...]
  [FROM from_item [, ...]]
  [WHERE condition]
  [GROUP BY grouping_element [, ...]]
  [HAVING condition [, ...]]
  [WINDOW window_name AS (window_specification)]
  [{UNION | INTERSECT | EXCEPT} [ALL] select]
  [ORDER BY expression [ASC | DESC | USING operator] [NULLS {FIRST | LAST}] [, ...]]
  [LIMIT {count | ALL}]
  [OFFSET start]
  [FOR {UPDATE | SHARE} [OF table_name [, ...]] [NOWAIT] [...]]
```

### SELECT INTO
Defines a new table from the results of a query.

```sql
[ WITH with_query [, ...] ]
SELECT [ALL | DISTINCT [ON ( expression [, ...] )]]
    * | expression [AS output_name] [, ...]
    INTO [TEMPORARY | TEMP] [TABLE] new_table
    [FROM from_item [, ...]]
    [WHERE condition]
    [GROUP BY expression [, ...]]
    [HAVING condition [, ...]]
    [{UNION | INTERSECT | EXCEPT} [ALL] select]
    [ORDER BY expression [ASC | DESC | USING operator] [NULLS {FIRST | LAST}] [, ...]]
    [LIMIT {count | ALL}]
    [OFFSET start]
    [FOR {UPDATE | SHARE} [OF table_name [, ...]] [NOWAIT] 
    [...]]
```

### SET
Changes the value of a database configuration parameter.

```sql
SET [SESSION | LOCAL] configuration_parameter {TO | =} value | 
    'value' | DEFAULT}
 
SET [SESSION | LOCAL] TIME ZONE {timezone | LOCAL | DEFAULT}
```

### SET ROLE
Sets the current role identifier of the current session.

```sql
SET [SESSION | LOCAL] ROLE rolename
 
SET [SESSION | LOCAL] ROLE NONE
 
RESET ROLE
```

### SET SESSION AUTHORIZATION
Sets the session role identifier and the current role identifier of the current session.

```sql
SET [SESSION | LOCAL] SESSION AUTHORIZATION rolename
 
SET [SESSION | LOCAL] SESSION AUTHORIZATION DEFAULT
 
RESET SESSION AUTHORIZATION
```

### SET TRANSACTION
Sets the characteristics of the current transaction.

```sql
SET TRANSACTION [transaction_mode] [READ ONLY | READ WRITE]
 
SET SESSION CHARACTERISTICS AS TRANSACTION transaction_mode 
     [READ ONLY | READ WRITE]
```

### SHOW
Shows the value of a system configuration parameter.

```sql
SHOW configuration_parameter
 
SHOW ALL
```

### START TRANSACTION
Starts a transaction block.

```sql
START TRANSACTION [SERIALIZABLE | READ COMMITTED | READ UNCOMMITTED]
                  [READ WRITE | READ ONLY]
```

### TRUNCATE
Empties a table of all rows.

```sql
TRUNCATE [TABLE] name [, ...] [CASCADE | RESTRICT]
```

### UPDATE
Updates rows of a table.

```sql
UPDATE [ONLY] table [[AS] alias]
   SET {column = {expression | DEFAULT} |
   (column [, ...]) = ({expression | DEFAULT} [, ...])} [, ...]
   [FROM fromlist]
   [WHERE condition | WHERE CURRENT OF cursor_name ]
```

### VACUUM
Garbage-collects and optionally analyzes a database.

```sql
VACUUM [FULL] [FREEZE] [VERBOSE] [table]
 
VACUUM [FULL] [FREEZE] [VERBOSE] ANALYZE
              [table [(column [, ...] )]]
```

### VALUES
Computes a set of rows.

```sql
VALUES ( expression [, ...] ) [, ...]
   [ORDER BY sort_expression [ASC | DESC | USING operator] [, ...]]
   [LIMIT {count | ALL}] [OFFSET start]
```

