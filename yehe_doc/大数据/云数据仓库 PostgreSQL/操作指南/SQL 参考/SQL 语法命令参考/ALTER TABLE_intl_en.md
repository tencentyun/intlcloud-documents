It changes the definition of a table.

## Synopsis

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

where `action` is one of:

```sql
  ADD [COLUMN] column_name type
      [column_constraint [ ... ]]
  DROP [COLUMN] column [RESTRICT | CASCADE]
  ALTER [COLUMN] column TYPE type [USING expression]
  ALTER [COLUMN] column SET DEFAULT expression
  ALTER [COLUMN] column DROP DEFAULT
  ALTER [COLUMN] column { SET | DROP } NOT NULL
  ALTER [COLUMN] column SET STATISTICS integer
  ADD table_constraint
  DROP CONSTRAINT constraint_name [RESTRICT | CASCADE]
  DISABLE TRIGGER [trigger_name | ALL | USER]
  ENABLE TRIGGER [trigger_name | ALL | USER]
  CLUSTER ON index_name
  SET WITHOUT CLUSTER
  SET WITHOUT OIDS
  SET (FILLFACTOR = value)
  RESET (FILLFACTOR)
  INHERIT parent_table
  NO INHERIT parent_table
  OWNER TO new_owner
  SET TABLESPACE new_tablespace
```

where `partition_action` is one of:

```sql
  ALTER DEFAULT PARTITION
  DROP DEFAULT PARTITION [IF EXISTS]
  DROP PARTITION [IF EXISTS] { partition_name | 
      FOR (RANK(number)) | FOR (value) } [CASCADE]
  TRUNCATE DEFAULT PARTITION
  TRUNCATE PARTITION { partition_name | FOR (RANK(number)) | 
      FOR (value) }
  RENAME DEFAULT PARTITION TO new_partition_name
  RENAME PARTITION { partition_name | FOR (RANK(number)) | 
      FOR (value) } TO new_partition_name
  ADD DEFAULT PARTITION name [ ( subpartition_spec ) ]
  ADD PARTITION [partition_name] partition_element
     [ ( subpartition_spec ) ]
  EXCHANGE PARTITION { partition_name | FOR (RANK(number)) | 
       FOR (value) } WITH TABLE table_name
        [ WITH | WITHOUT VALIDATION ]
  EXCHANGE DEFAULT PARTITION WITH TABLE table_name
   [ WITH | WITHOUT VALIDATION ]
  SET SUBPARTITION TEMPLATE (subpartition_spec)
  SPLIT DEFAULT PARTITION
    {  AT (list_value)
     | START([datatype] range_value) [INCLUSIVE | EXCLUSIVE] 
        END([datatype] range_value) [INCLUSIVE | EXCLUSIVE] }
    [ INTO ( PARTITION new_partition_name, 
             PARTITION default_partition_name ) ]
  SPLIT PARTITION { partition_name | FOR (RANK(number)) | 
     FOR (value) } AT (value) 
    [ INTO (PARTITION partition_name, PARTITION partition_name)]  
```

where `partition_element` is:

```sql
    VALUES (list_value [,...] )
  | START ([datatype] 'start_value') [INCLUSIVE | EXCLUSIVE]
     [ END ([datatype] 'end_value') [INCLUSIVE | EXCLUSIVE] ]
  | END ([datatype] 'end_value') [INCLUSIVE | EXCLUSIVE]
[ WITH ( partition_storage_parameter=value [, ... ] ) ]
[ TABLESPACE tablespace ]
```

where `subpartition_spec` is:

```sql
subpartition_element [, ...]
```

and `subpartition_element` is:

```sql
   DEFAULT SUBPARTITION subpartition_name
  | [SUBPARTITION subpartition_name] VALUES (list_value [,...] )
  | [SUBPARTITION subpartition_name] 
     START ([datatype] 'start_value') [INCLUSIVE | EXCLUSIVE]
     [ END ([datatype] 'end_value') [INCLUSIVE | EXCLUSIVE] ]
     [ EVERY ( [number | datatype] 'interval_value') ]
  | [SUBPARTITION subpartition_name] 
     END ([datatype] 'end_value') [INCLUSIVE | EXCLUSIVE]
     [ EVERY ( [number | datatype] 'interval_value') ]
[ WITH ( partition_storage_parameter=value [, ... ] ) ]
[ TABLESPACE tablespace ]
```

where `storage_parameter` is:

```sql
   APPENDONLY={TRUE|FALSE}
   BLOCKSIZE={8192-2097152}
   ORIENTATION={COLUMN|ROW}
   COMPRESSTYPE={ZLIB|QUICKLZ|RLE_TYPE|NONE}
   COMPRESSLEVEL={0-9}
   FILLFACTOR={10-100}
   OIDS[=TRUE|FALSE]
```


## Description
`ALTER TABLE` changes the definition of an existing table. There are several subforms:
 
 **ADD COLUMN** 
 Adds a new column to the table, using the same syntax as `CREATE TABLE`. A `DEFAULT` clause is needed when adding a column to an append-optimized table.

**DROP COLUMN** 
Drops a column from a table. Note that if you drop table columns that are being used as the database distribution key, the distribution policy for the table will be changed to `DISTRIBUTED RANDOMLY`. Indexes and table constraints involving the column will be automatically dropped as well. You will need to say `CASCADE` if anything outside the table depends on the column (such as views).

**ALTER COLUMN TYPE** 
Changes the data type of a column of a table. Note that you cannot alter column data types that are being used as distribution or partitioning keys. Indexes and simple table constraints involving the column will be automatically converted to use the new column type by reparsing the originally supplied expression. The optional `USING` clause specifies how to compute the new column value from the old. If omitted, the default conversion is the same as an assignment cast from old data type to new. A `USING` clause must be provided if there is no implicit or assignment cast from old to new type.

**SET/DROP DEFAULT** 
Sets or removes the default value for a column. The default values only apply to subsequent `INSERT` commands. They do not cause rows already in the table to change. Defaults may also be created for views, in which case they are inserted into statements on the view before the view's `ON INSERT` rule is applied.

**SET/DROP NOT NULL** 
Changes whether a column is marked to allow null values or to reject null values. You can only use `SET NOT NULL` when the column contains no null values.

**SET STATISTICS** 
Sets the per-column statistics-gathering target for subsequent `ANALYZE` operations. The target can be set in the range 0 to 1000, or set to -1 to revert to using the system default statistics target (default_statistics_target).

**ADD** table_constraint 
Adds a new constraint to a table (not just a partition) using the same syntax as `CREATE TABLE`.

**DROP CONSTRAINT** 
Drops the specified constraint on a table.

**DISABLE/ENABLE TRIGGER** 
Disables or enables trigger(s) belonging to the table. A disabled trigger is still known to the system, but is not executed when its triggering event occurs. For a deferred trigger, the enable status is checked when the event occurs, not when the trigger function is actually executed. One may disable or enable a single trigger specified by name, or all triggers on the table, or only user-owned triggers. Disabling or enabling constraint triggers requires superuser privileges.

>!Triggers are not supported in the database. Triggers in general have very limited functionality due to the parallelism of the database.

**CLUSTER ON/SET WITHOUT CLUSTER** 
Selects or removes the default index for future `CLUSTER` operations. It does not actually re-cluster the table. Note that `CLUSTER` is not the recommended way to physically reorder a table in the database because it takes so long. It is better to recreate the table with **`CREATE TABLE AS`** and order it by the index column(s).

>!`CLUSTER ON` is not supported on append-optimized tables.

**SET WITHOUT OIDS** 
Removes the OID system column from the table. Note that there is no variant of `ALTER TABLE` that allows OIDs to be restored to a table once they have been removed.

**SET ( FILLFACTOR =** value**) / RESET (FILLFACTOR)** 
Changes the fillfactor for the table. The fillfactor for a table is a percentage between 10 and 100. 100 (complete packing) is the default. When a smaller fillfactor is specified, `INSERT` operations pack table pages only to the indicated percentage; the remaining space on each page is reserved for updating rows on that page. This gives `UPDATE` a chance to place the updated copy of a row on the same page as the original, which is more efficient than placing it on a different page. For a table whose entries are never updated, complete packing is the best choice, but in heavily updated tables smaller fillfactors are appropriate. Note that the table contents will not be modified immediately by this command. You will need to rewrite the table to get the desired effects.

**SET DISTRIBUTED** 
Changes the distribution policy of a table. Changes to a hash distribution policy will cause the table data to be physically redistributed on disk, which can be resource intensive.

**INHERIT** parent_table **/ NO INHERIT** parent_table 
Adds or removes the target table as a child of the specified parent table. Queries against the parent will include records of its child table. To be added as a child, the target table must already contain all the same columns as the parent (it could have additional columns, too). The columns must have matching data types, and if they have `NOTNULL` constraints in the parent then they must also have `NOT NULL` constraints in the child. There must also be matching child-table constraints for all `CHECK` constraints of the parent.

**OWNER** 
Changes the owner of the table, sequence, or view to the specified user.

**SET TABLESPACE** 
Changes the table's tablespace to the specified tablespace and moves the data file(s) associated with the table to the new tablespace. Indexes on the table, if any, are not moved; but they can be moved separately with additional `SET TABLESPACE` commands. See also `CREATE TABLESPACE`. If changing the tablespace of a partitioned table, all child table partitions will also be moved to the new tablespace.

**RENAME** 
Changes the name of a table (or an index, sequence, or view) or the name of an individual column in a table. There is no effect on the stored data. Note that the database distribution key columns cannot be renamed.

**SET SCHEMA** 
Moves the table into another schema. Associated indexes, constraints, and sequences owned by table columns are moved as well.

**ALTER PARTITION | DROP PARTITION | RENAME PARTITION | TRUNCATE PARTITION | ADD PARTITION | SPLIT PARTITION | EXCHANGE PARTITION | SET SUBPARTITION TEMPLATE** 
Changes the structure of a partitioned table. In most cases, you must go through the parent table to alter one of its child table partitions.
>? If you add a partition to a table that has subpartition encodings, the new partition inherits the storage directives for the subpartitions. For more information about the precedence of compression settings, see "Using Compression" in the Database Administrator Guide.

You must own the table to use `ALTER TABLE`. To change the schema of a table, you must also have `CREATE` privilege on the new schema. To add the table as a new child of a parent table, you must own the parent table as well. To alter the owner, you must also be a direct or indirect member of the new owning role, and that role must have `CREATE` privilege on the table's schema. A superuser has these privileges automatically.

>!Memory usage increases significantly when a table has many partitions, if a table has compression, or if the blocksize for a table is large. If the number of relations associated with the table is large, this condition can force an operation on the table to use more memory. For example, if the table is a CO table and has a large number of columns, each column is a relation. An operation like `ALTER TABLE ALTER COLUMN` opens all the columns in the table allocates associated buffers. If a CO table has 40 columns and 100 partitions, and the columns are compressed and the blocksize is 2 MB (with a system factor of 3), the system attempts to allocate 24 GB, that is (40 ×100) × (2 ×3) MB or 24 GB.

## Parameters

ONLY
Only perform the operation on the table name specified. If the `ONLY` keyword is not used, the operation will be performed on the named table and any child table partitions associated with that table.

name
The name (possibly schema-qualified) of an existing table to alter. If `ONLY` is specified, only that table is altered. If `ONLY` is not specified, the table and all its descendant tables (if any) are updated.
>!Constraints can only be added to an entire table, not to a partition. Because of that restriction, the `name` parameter can only contain a table name, not a partition name.

column
Name of a new or existing column. Note that the database distribution key columns must be treated with special care. Altering or dropping these columns can change the distribution policy for the table.

new_column
New name for an existing column.

new_name
New name for the table.

type
Data type of the new column, or new data type for an existing column. If changing the data type of a distribution key column, you are only allowed to change it to a compatible type (for example, `text` to `varchar` is OK, but `text` to `int` is not).

table_constraint
New table constraint for the table. Note that foreign key constraints are currently not supported in the database. Also a table is only allowed one unique constraint and the uniqueness must be within the database distribution key.

constraint_name
Name of an existing constraint to drop.

CASCADE
Automatically drop objects that depend on the dropped column or constraint (for example, views referencing the column).

RESTRICT
Refuse to drop the column or constraint if there are any dependent objects. This is the default behavior.

trigger_name
Name of a single trigger to disable or enable. Note that the database does not support triggers.

ALL
Disable or enable all triggers belonging to the table including constraint related triggers. This requires superuser privilege.

USER
Disable or enable all user-created triggers belonging to the table.

index_name
The index name on which the table should be marked for clustering. Note that `CLUSTER` is not the recommended way to physically reorder a table in the database because it takes so long. It is better to recreate the table with **`CREATE TABLE AS`** and order it by the index column(s).

FILLFACTOR
Set the fillfactor percentage for a table.

value
The new value for the FILLFACTOR parameter, which is a percentage between 10 and 100. 100 is the default.

DISTRIBUTED BY (column) | DISTRIBUTED RANDOMLY
Specifies the distribution policy for a table. Changing a hash distribution policy will cause the table data to be physically redistributed on disk, which can be resource intensive. If you declare the same hash distribution policy or change from hash to random distribution, data will not be redistributed unless you declare `SET WITH(REORGANIZE=true)`.

REORGANIZE=true|false
Use `REORGANIZE=true` when the hash distribution policy has not changed or when you have changed from a hash to a random distribution, and you want to redistribute the data anyways.

parent_table
A parent table to associate or de-associate with this table.

new_owner
The role name of the new owner of the table.

new_tablespace
The name of the tablespace to which the table will be moved.

new_schema
The name of the schema to which the table will be moved.

parent_table_name
When altering a partitioned table, the name of the top-level parent table.

ALTER [DEFAULT] PARTITION
If altering a partition deeper than the first level of partitions, use `ALTER PARTITION` clauses to specify which subpartition in the hierarchy you want to alter.

DROP [DEFAULT] PARTITION
Drops the specified partition. If the partition has subpartitions, the subpartitions are automatically dropped as well.

TRUNCATE [DEFAULT] PARTITION
Truncates the specified partition. If the partition has subpartitions, the subpartitions are automatically truncated as well.

RENAME [DEFAULT] PARTITION
Changes the partition name of a partition (not the relation name). Partitioned tables are created using the naming convention: `<parentname>_<level>_prt_<partition_name>`.

ADD DEFAULT PARTITION
Adds a default partition to an existing partition design. When data does not match to an existing partition, it is inserted into the default partition. Partition designs that do not have a default partition will reject incoming rows that do not match to an existing partition. Default partitions must be given a name.

ADD PARTITION

partition_element
Using the existing partition type of the table (range or list), defines the boundaries of new partition you are adding.

name
A name for this new partition.

**VALUES** 
For list partitions, defines the value(s) that the partition will contain.

**START** 
For range partitions, defines the starting range value for the partition. By default, start values are `INCLUSIVE`. For example, if you declared a start date of '2016-01-01', then the partition would contain all dates greater than or equal to '2016-01-01'. Typically the data type of the `START` expression is the same type as the partition key column. If that is not the case, then you must explicitly cast to the intended data type.

**END** 
For range partitions, defines the ending range value for the partition. By default, end values are `EXCLUSIVE`. For example, if you declared an end date of '2016-02-01', then the partition would contain all dates less than but not equal to '2016-02-01'. Typically the data type of the `END` expression is the same type as the partition key column. If that is not the case, then you must explicitly cast to the intended data type.

**WITH** 
Sets the table storage options for a partition. For example, you may want older partitions to be append-optimized tables and newer partitions to be regular heap tables. See `CREATE TABLE` for a description of the storage options.

**TABLESPACE** 
The name of the tablespace in which the partition is to be created.

subpartition_spec 
Only allowed on partition designs that were created without a subpartition template. Declares a subpartition specification for the new partition you are adding. If the partitioned table was originally defined using a subpartition template, then the template will be used to generate the subpartitions automatically.

EXCHANGE [DEFAULT] PARTITION
Exchanges another table into the partition hierarchy into the place of an existing partition. In a multi-level partition design, you can only exchange the lowest level partitions (those that contain data).

The database server configuration parameter `gp_enable_exchange_default_partition` controls availability of the `EXCHANGE DEFAULT PARTITION` clause. The default value for the parameter is off. The clause is not available and the database returns an error if the clause is specified in an `ALTER TABLE` command.

Warning: Before you exchange the default partition, you must ensure the data in the table to be exchanged, the new default partition, is valid for the default partition. For example, the data in the new default partition must not contain data that would be valid in other leaf child partitions of the partitioned table. Otherwise, queries against the partitioned table with the exchanged default partition that are executed by `GPORCA` might return incorrect results.

**WITH TABLE** table_name
The name of the table you are swapping into the partition design. You can exchange a table where the table data is stored in the database. For example, the table is created with the `CREATE TABLE` command.

With the `EXCHANGE PARTITION` clause, you can also exchange a readable external table (created with the `CREATE EXTERNAL TABLE` command) into the partition hierarchy in the place of an existing leaf child partition. If you specify a readable external table, you must also specify the `WITHOUT VALIDATION` clause to skip table validation against the `CHECK` constraint of the partition you are exchanging.

Exchanging a leaf child partition with an external table is not supported if:
- The partitioned table is created by a `SUBPARTITION` clause or has child partitions.
- The partitioned table contains a column with a check constraint or a NOT NULL constraint.

**WITH** | **WITHOUT VALIDATION** 
Validates that the data in the table matches the `CHECK` constraint of the partition you are exchanging. The default is to validate the data against the `CHECK` constraint.

Warning: If you specify the `WITHOUT VALIDATION` clause, you must ensure that the data in table that you are exchanging for an existing child leaf partition is valid against the `CHECK` constraints on the partition. Otherwise, queries against the partitioned table might return incorrect results.

SET SUBPARTITION TEMPLATE
Modifies the subpartition template for an existing partition. After a new subpartition template is set, all new partitions added will have the new subpartition design (existing partitions are not modified).

SPLIT DEFAULT PARTITION
Splits a default partition. In a multi-level partition, only a range partition can be split, not a list partition, and you can only split the lowest level default partitions (those that contain data). Splitting a default partition creates a new partition containing the values specified and leaves the default partition containing any values that do not match to an existing partition.

**AT** 
For list partitioned tables, specifies a single list value that should be used as the criteria for the split.

**START** 
For range partitioned tables, specifies a starting value for the new partition.

**END** 
For range partitioned tables, specifies an ending value for the new partition.

**INTO** 
Allows you to specify a name for the new partition. When using the `INTO` clause to split a default partition, the second partition name specified should always be that of the existing default partition. If you do not know the name of the default partition, you can look it up using the `pg_partitions` view.

SPLIT PARTITION
Splits an existing partition into two partitions. In a multi-level partition, only a range partition can be split, not a list partition, and you can only split the lowest level partitions (those that contain data).

**AT** 
Specifies a single value that should be used as the criteria for the split. The partition will be divided into two new partitions with the split value specified being the starting range for the latter partition.

**INTO** 
Allows you to specify names for the two new partitions created by the split.

partition_name
The given name of a partition.

FOR (RANK(number))
For range partitions, the rank of the partition in the range.

FOR ('value')
Specifies a partition by declaring a value that falls within the partition boundary specification. If the value declared with `FOR` matches to both a partition and one of its subpartitions (for example, if the value is a date and the table is partitioned by month and then by day), then FOR will operate on the first level where a match is found (for example, the monthly partition). If your intent is to operate on a subpartition, you must declare so as follows:

```
ALTER TABLE name ALTER PARTITION FOR ('2016-10-01') DROP PARTITION FOR ('2016-10-01');
```

## Notes

The table name specified in the `ALTER TABLE` command cannot be the name of a partition within a table.

Take special care when altering or dropping columns that are part of the database distribution key as this can change the distribution policy for the table.

The database does not currently support foreign key constraints. For a unique constraint to be enforced in the database, the table must be hash-distributed (not `DISTRIBUTED RANDOMLY`), and all of the distribution key columns must be the same as the initial columns of the unique constraint columns.

Adding a `CHECK` or `NOT NULL` constraint requires scanning the table to verify that existing rows meet the constraint.

When a column is added with `ADD COLUMN`, all existing rows in the table are initialized with the column's default value, or `NULL` if no `DEFAULT` clause is specified (note that it is not allowed to add columns with no default values specified in append-optimized tables). Adding a column with a non-null default or changing the type of an existing column will require the entire table to be rewritten. This may take a significant amount of time for a large table; and it will temporarily require double the disk space.

You can specify multiple changes in a single `ALTER TABLE` command, which will be done in a single pass over the table.

The `DROP COLUMN` form does not physically remove the column, but simply makes it invisible to SQL operations. Subsequent insert and update operations in the table will store a null value for the column. Thus, dropping a column is quick but it will not immediately reduce the on-disk size of your table, as the space occupied by the dropped column is not reclaimed. The space will be reclaimed over time as existing rows are updated.

The fact that `ALTER TYPE` requires rewriting the whole table is sometimes an advantage, because the rewriting process eliminates any dead space in the table. For example, to reclaim the space occupied by a dropped column immediately, the fastest way is: `ALTER TABLE table ALTER COLUMN anycol TYPE sametype;` where `anycol` is any remaining table column and `sametype` is the same type that column already has. This results in no semantically-visible change in the table, but the command forces rewriting, which gets rid of no-longer-useful data.

If a table is partitioned or has any descendant tables, it is not permitted to add, rename, or change the type of a column in the parent table without doing the same to the descendants. This ensures that the descendants always have columns matching the parent.

To see the structure of a partitioned table, you can use the view `pg_partitions`. This view can help identify the particular partitions you may want to alter.

A recursive `DROP COLUMN` operation will remove a descendant table's column only if the descendant does not inherit that column from any other parents and never had an independent definition of the column. A nonrecursive `DROP COLUMN` (ALTER TABLE ONLY ... DROP COLUMN) never removes any descendant columns, but instead marks them as independently defined rather than inherited.

The `TRIGGER`, `CLUSTER`, `OWNER`, and `TABLESPACE` actions never recurse to descendant tables; that is, they always act as though `ONLY` were specified. Adding a constraint can recurse only for `CHECK` constraints.

These `ALTER PARTITION` operations are supported if no data is changed on a partitioned table that contains a leaf child partition that has been exchanged to use an external table. Otherwise, an error is returned.
- Adding or dropping a column.
- Changing the data type of column.

These `ALTER PARTITION` operations are not supported for a partitioned table that contains a leaf child partition that has been exchanged to use an external table:

- Setting a subpartition template.
- Altering the partition properties.
- Creating a default partition.
- Setting a distribution policy.
- Setting or dropping a `NOT NULL` constraint of column.
- Adding or dropping constraints.
- Splitting an external partition.

Changing any part of a system catalog table is not permitted.

## Examples

Add a column to a table:

```sql
ALTER TABLE distributors ADD COLUMN address varchar(30);
```

Rename an existing column:

```sql
ALTER TABLE distributors RENAME COLUMN address TO city;
```

Rename an existing table:

```sql
ALTER TABLE distributors RENAME TO suppliers;
```

Add a not-null constraint to a column:

```sql
ALTER TABLE distributors ALTER COLUMN street SET NOT NULL;
```

Add a check constraint to a table:

```sql
ALTER TABLE distributors ADD CONSTRAINT zipchk CHECK 
(char_length(zipcode) = 5);
 
-- Add a constraint that the value of the `c1` column must be greater than 5:
alter table table1 ADD CONSTRAINT xxcheck2 check (c1 > 5);
ALTER TABLE
Time: 50.201 ms
-- Insert data and report an error if the value of the inserted column is less than 5:
INSERT INTO table1 VALUES(20190117,'test', 4);
ERROR:  new row for relation "table1" violates check constraint "xxcheck2"  (seg0 10.0.15.16:40000 pid=11071)
 
INSERT INTO table1 VALUES(20190117,'test', 6);
INSERT 0 1
Time: 71.215 ms
 
```

Move a table to a different schema:

```sql
ALTER TABLE myschema.distributors SET SCHEMA yourschema;
```

Add a new partition to a partitioned table:

```sql
ALTER TABLE sales ADD PARTITION 
            START (date '2017-02-01') INCLUSIVE 
            END (date '2017-03-01') EXCLUSIVE;
```

Add a default partition to an existing partition design:

```sql
ALTER TABLE sales ADD DEFAULT PARTITION other;
```

Rename a partition:

```sql
ALTER TABLE sales RENAME PARTITION FOR ('2016-01-01') TO 
jan08;
```

Drop the first (oldest) partition in a range sequence:

```sql
ALTER TABLE sales DROP PARTITION FOR (RANK(1));
```

Exchange a table into your partition design:

```sql
ALTER TABLE sales EXCHANGE PARTITION FOR ('2016-01-01') WITH 
TABLE jan08;
```

Split the default partition (where the existing default partition's name is `other`) to add a new monthly partition for January 2017:

```sql
ALTER TABLE sales SPLIT DEFAULT PARTITION 
START ('2017-01-01') INCLUSIVE 
END ('2017-02-01') EXCLUSIVE 
INTO (PARTITION jan09, PARTITION other);
```

Split a monthly partition into two with the first partition containing dates January 1-15 and the second partition containing dates January 16-31:

```sql
ALTER TABLE sales SPLIT PARTITION FOR ('2016-01-01')
AT ('2016-01-16')
INTO (PARTITION jan081to15, PARTITION jan0816to31);
```

## Compatibility

The `ADD`, `DROP`, and `SET DEFAULT` forms conform with the SQL standard. The other forms are database extensions of the SQL standard. Also, the ability to specify more than one manipulation in a single `ALTER TABLE` command is an extension.

`ALTER TABLE DROP COLUMN` can be used to drop the only column of a table, leaving a zero-column table. This is an extension of SQL, which disallows zero-column tables.

## See Also

CREATE TABLE, DROP TABLE
