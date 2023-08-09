## Overview
SQL optimization is a crucial step in improving database performance. To avoid the impact when the optimizer fails to select an appropriate execution plan, TXSQL provides the outline feature for you to bind execution plans. MySQL allows you to use hints to manually bind execution plans. The hint information contains the optimization rule for SQL statements, algorithm to be used, and index for data scan, and an outline relies on hints to specify execution plans. Tencent Cloud provides the `mysql.outline` system table for you to add plan binding rules and the `cdb_opt_outline_enabled` switch for you to enable/disable the outline feature.

## Supported Versions
Kernel version: MySQL 8.0 20201230 and above.

## Use Cases
This feature is suitable for scenarios where an execution plan in the production environment has poor performance (for example, the index in the execution plan is incorrect), but you don't want to modify SQL statements and release a new version to fix this problem.

## Performance Impact
- If `cdb_opt_outline_enabled` is enabled, the execution efficiency of SQL statements missing the outline will not be affected.
- The execution efficiency of SQL statements hitting the outline will be lower than that of general execution, but the performance after outline binding is generally improved by several times.
- To use `cdb_opt_outline_enabled`, you should consult the OPS or kernel engineers to avoid faulty binding and consequential performance compromise.

## Instructions
The outline syntax uses a new syntax form:
- Configure outline information: `outline "sql" set outline_info "outline";`
- Clear outline information: `outline reset ""; outline reset all;`
- Refresh outline information: `outline flush;`

Below are the outline use methods with the following schemas as examples:
```
create table t1(a int, b int, c int, primary key(a));
create table t2(a int, b int, c int, unique key idx2(a));
create table t3(a int, b int, c int, unique key idx3(a));
```

| Parameter                  | Effective Immediately | Type | Default Value  | Valid Values | Description                |
| ----------------------- | ---- | ---- | ----- | ---------- | ------------------- |
| cdb_opt_outline_enabled | Yes  | bool | false | true/false | Whether to enable the outline feature. |

>?Currently, you cannot directly modify the values of the above parameter. If needed, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
>

### Binding outline
To bind an outline, replace the SQL statement with another where the SQL syntax is not changed but some hint information is added to tell the optimizer how to execute the statement.
The syntax is in the format of `outline "sql" set outline_info "OUTLINE";`. Note that the string after `outline_info` must start with `"OUTLINE:"`, which is followed by the SQL statement with the hint information added. For example, you can add the index in column `a` to table `t2` in the SQL statement `select *from t1, t2 where t1.a = t2.a` as follows:
```
outline "select* from t1, t2 where t1.a = t2.a" set outline_info "OUTLINE:select * from t1, t2 use index(idx2) where t1.a = t2.a";
```

### Binding optimizer hint
To make the feature more flexible, TXSQL allows you to add optimizer hints incrementally to SQL statements. You can also implement the same feature by directly binding an outline.
The syntax is in the format of `outline "sql" set outline_info "outline";`. Note that the string after `outline_info` must start with `"OPT:"`, which is followed by the optimizer hint information to be added. For example, you can specify `SEMIJOIN` of `MATERIALIZATION/DUPSWEEDOUT` for the SQL statement `select *from t1 where t1.a in (select b from t2)` as follows:
```
outline "select* from t1 where t1.a in (select b from t2)" set outline_info "OPT:2#qb_name(qb2)";
outline "select * from t1 where t1.a in (select b from t2)" set outline_info "OPT:1#SEMIJOIN(@qb2 MATERIALIZATION, DUPSWEEDOUT)";
```

You can add only one optimizer hint to the original SQL statement at a time and must comply with the following rules:
- The `OPT` keyword must follow ".
- ':' must be placed before the new statement to be bound.
- You must add two fields (query block number#optimizer hint string), which must be separated with "#" (e.g., `"OPT:1#max_execution_time(1000)"`).

### Binding index hint
To make the feature more flexible, TXSQL allows you to add index hints incrementally to SQL statements. You can also implement the same feature by directly binding an outline.
The syntax is in the format of `outline "sql" set outline_info "outline";`. Note that the string after `outline_info` must start with `"INDEX:"`, which is followed by the index hint information to be added.
For example, you can add the index `idx1` of `USE INDEX` in `FOR JOIN` type to the table `t1` in the database `test` in query block 3 for the SQL statement `select *from t1 where t1.a in (select t1.a from t1 where t1.b in (select t1.a from t1 left join t2 on t1.a = t2.a))` as follows:
```
outline "select* from t1 where t1.a in (select t1.a from t1 where t1.b in (select t1.a from t1 left join t2 on t1.a = t2.a))" set outline_info "INDEX:3#test#t1#idx1#1#0";
```

You can add only one index hint to the original SQL statement at a time and must comply with the following rules:
- The `INDEX` keyword must follow ".
- ':' must be placed before the new statement to be bound.
- You must add five fields (query block number#db_name#table_name#index_name#index_type#clause).
- Here, `index_type` has three valid values (0: INDEX_HINT_IGNORE; 1: INDEX_HINT_USE; 2: INDEX_HINT_FORCE), and `clause` also has three valid values (1: FOR JOIN; 2: FOR ORDER BY; 3: FOR GROUP BY), which must be separated by "#" (e.g., `"INDEX:2#test#t2#idx2#1#0"`, indicating to bind the index `idx1` in `USE INDEX FOR JOIN` type to the table `test.t2` in the second query block).

### Deleting the outline information of SQL statement
TXSQL allows you to delete the outline binding information from an SQL statement.
The syntax is in the format of `outline reset "sql";`. For example, to delete the outline information from `select *from t1, t2 where t1.a = t2.a`, run the following statement: `outline reset "select* from t1, t2 where t1.a = t2.a";`.

### Clearing all outline information
TXSQL allows you to clear all outline binding information in the kernel. The syntax is `outline reset all`, and the execution statement is `outline reset all;`.

There may be some specific problems in the production environment where you must bind an index. In this case, you can directly configure an outline for binding.
You should analyze the possible performance compromise after configuring an outline and bind an outline only if the compromised performance is acceptable. You can consult kernel engineers if necessary.

## Parameter Status Description
TXSQL provides multiple methods to view the outline binding of your SQL statements. You can use the `mysql.outline` table to view the information of configured outlines. You can also use the ` show cdb_outline_info` and `select * from information_schema.cdb_outline_info` APIs to view the outline information in the memory. Whether the entered SQL statement is bound to the specified outline is subject to whether the outline information is in the memory. Therefore, you can use the two APIs for debugging.

The `mysql.outline` system table is added to store the records of configured outline information, which has the following fields:

| Field Name       | Description                                   |
| ------------ | -------------------------------------- |
| Id                | Outline number.                    |
| Digest         | Hash value of the original SQL statement.                    |
| Digest_text  | Fingerprint information text of the original SQL statement.              |
| Outline_text | Fingerprint information text of the SQL statement after the outline is bound. |

You can use `show cdb_outline_info` or `select * from information_schema.cdb_outline_info` to view the outline records in the memory, and execution of the corresponding SQL statement will hit the bound plan in the outline. The parameters are as follows:

| Field Name  | Description                         |
| ------- | ---------------------------- |
| origin  | Original SQL statement fingerprint.              |
| outline | SQL statement fingerprint after the outline is bound. |

