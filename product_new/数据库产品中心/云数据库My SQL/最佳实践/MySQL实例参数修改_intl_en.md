For TencentDB for MySQL, you can modify the parameters of a master instance in the [console](https://console.cloud.tencent.com/cdb). Modifying some crucial parameters in an improper way will lead to exceptions in disaster recovery instances and data inconsistency. This document describes the consequences of modifying the following crucial parameters.


### lower_case_table_names
**Default value:** 0
**Role:** When creating a database or table, you can set whether storage and query operations are case-sensitive. This parameter can be set to 0 (case-sensitive) or 1 (case-insensitive), and the default value is 0.
**Impact:** After the parameters of the master instance are modified, the parameters of the disaster recovery instance cannot be modified accordingly, as the master instance is set as case-sensitive, but the disaster recovery instance is not; for example, if two tables named "Test" and "TEst" are created in the master instance, then data sync will fail when the disaster recovery instance uses the corresponding logs, because the table name "TEst" already exists.


### auto_increment_increment
**Default value:** 1
**Role:** It is used as the increment value of the auto-increment column AUTO_INCREMENT. Its value can range from 1 (default value) to 65,535.
**Impact:** After the parameters of the master instance are modified, the parameters of the disaster recovery instance cannot be modified accordingly. When the increment value is modified for the master instance but not for the disaster recovery instance, master-slave data inconsistency will occur.

#### auto_increment_offset
**Default value:** 1
**Role:** It is used as the start value (offset) of the auto-increment column AUTO_INCREMENT. Its value can range from 1 (default value) to 65,535.
**Impact:** After the parameters of the master instance are modified, the parameters of the disaster recovery instance cannot be modified accordingly. When the offset value is modified for the master instance but not for the disaster recovery instance, master-slave data inconsistency will occur.


### sql_mode
**Default value:** NO_ENGINE_SUBSTITUTION
**Role:** TencentDB for MySQL can operate in different SQL modes, which define the SQL syntax and data check that it should support. The default value of this parameter in v5.6 is NO_ENGINE_SUBSTITUTION, which means that if the used storage engine is disabled or not compiled, an error will be thrown; in v5.7, the default value is `ONLY_FULL_GROUP_BY`,`STRICT_TRANS_TABLES`,`NO_ZERO_IN_DATE`,`NO_ZERO_DATE`.
,`ERROR_FOR_DIVISION_BY_ZERO`,`NO_AUTO_CREATE_USER`,`NO_ENGINE_SUBSTITUTION`.
Here:
- `ONLY_FULL_GROUP_BY` means that in a GROUP BY operation, the column in SELECT or the HAVING or ORDER BY subquery must be a function column that appears in or relies on GROUP BY;
- `STRICT_TRANS_TABLES` enables strict mode;
- `NO_ZERO_IN_DATE` indicates whether the month and day of a date can contain 0 and is subject to the status of the strict mode;
- `NO_ZERO_DATE` means that dates in the database cannot contain zero date and is subject to the status of the strict mode;
- `ERROR_FOR_DIVISION_BY_ZERO` means that in strict mode, if data is divided by 0 during the INSERT or UPDATE process, an error rather than a warning will be thrown, while in non-strict mode, NULL will be returned;
- `NO_AUTO_CREATE_USER` prohibits GRANT from creating a user whose password is empty;
- `NO_ENGINE_SUBSTITUTION` means that if the used storage engine is disabled or not compiled, an error will be thrown.

**Impact:** After the parameters of the master instance are modified, the parameters of the disaster recovery instance cannot be modified accordingly. When the SQL mode is changed for the master instance but not for the disaster recovery instance, for example, if the SQL mode limit of the master instance is smaller than that of the disaster recovery instance, the SQL statements that are successfully executed in the master instance may trigger errors when synced to the disaster recovery instance and thus lead to master-slave data inconsistency.  













