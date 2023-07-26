This document describes the TencentDB for MySQL audit rules.
>? The current audit rule capability is under reconstruction and does not support adding new rules.

## Rule Content
The following types are supported:
Client IP, database account, and database name. Supported operators are **Include/ Exclude**.

The full audit rule is a special rule, and all statements will be audited after it is enabled.

## Rule Operation
- The different fields in each rule add the conditions; that is, the relationship between field and condition is "AND" (&&).
- The relationship between rules is "OR" (||).
You can specify one or more audit rules for an instance, and as long as any one of them is met, the instance should be audited. For example, if rule A specifies that only operations of user1 with an execution time >= 1 second need to be audited, and rule B audits the statements of user1 with an execution time < 1 second, then all statements of user1 need to be audited eventually.

## Rule Description
Client IP, database account, and database name support **Include/Exclude** operators, and only one operator can be set at a time.

#### Database name description
If a statement is of the following table object type:
```
SQLCOM_SELECT, SQLCOM_CREATE_TABLE, SQLCOM_CREATE_INDEX, SQLCOM_ALTER_TABLE,
SQLCOM_UPDATE, SQLCOM_INSERT, SQLCOM_INSERT_SELECT, SQLCOM_DELETE, SQLCOM_TRUNCATE, SQLCOM_DROP_TABLE
```
Then, for this type of operation, the name of the database actually manipulated by the statement shall prevail. For example, if the currently used database is "db3", and the statement is:
```
select *from db1.test,db2.test;
```
Then, "db1" and "db2" will be used as the target database for rule judgment. If the rule is configured to audit "db1", "db1" will be audited, and if the rule is configured to audit "db3", "db3" will not be audited.
For statements not of the above table object type, the currently used database will be used as the target database for rule judgment. For example, if the currently used database is "db1", and the executed statement is `show databases`, then "db1" will be used as the target database for judgment. If the rule is configured to audit "db1", "db1" will be audited.

## Note
You can write only one value for "Include" and "Exclude" operator. If you write multiple values, they will be treated as a string, resulting in incorrect matching.

