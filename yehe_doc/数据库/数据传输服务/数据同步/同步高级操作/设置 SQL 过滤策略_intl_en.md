## Overview
When configuring a sync task, you can set a SQL sync policy, so that only SQL data meeting the set conditions will be synced to the target database. In this way, you can flexibly configure the sync schemes between multiple databases or split data tables as needed.

DTS supports the following SQL filters:
- DML filter: INSERT, UPDATE, and DELETE.

- DDL filter: You can select the specific DDL operation, such as `CREATE TABLE`, `CREATE VIEW`, and `DROP INDEX`.

- WHERE conditional filter: You can customize a filter for a single table.
  
> ?Currently, you can filter by DDL and WHERE condition for the following data sync links:
>
> - MySQL > MySQL/MariaDB/TDSQL-C for MySQL
> - MariaDB > MySQL/MariaDB
> - Percona > MySQL/MariaDB
> - TDSQL-C for MySQL > MySQL/TDSQL-C for MySQL

## Restrictions
You can set a WHERE conditional filter for a single table. To filter multiple tables, set a filter for each of them.

## Directions
1. Select different SQL policies on the **Set sync options and objects** page in [Sync Task](https://console.cloud.tencent.com/dts/replication).
   - DML: INSERT, UPDATE, and DELETE.
   - DDL:
     - If you select **DDL** but not **Custom DDL**, all the DDL operations in the source database will be synced to the target database.
     - If you select both **DDL** and **Custom DDL**, you can select specific DDL policies, and only the selected policies will be synced to the target database.
     - If you don't select **DDL**, all the DDL operations will not be synced to the target database.
<img src="https://qcloudimg.tencent-cloud.cn/raw/6f6e5623c461cd7f810bd281eb87c43d.png" style="zoom:70%;" /> 
2. In **Selected Object** on the right of **Sync Object Option**, select the target table and click the edit button on the right to set the WHERE conditional filter.
>?Rules for setting a WHERE conditional filter:
>- For INSERT operations, the data to be inserted must meet the condition for the filter rule to take effect. For DELETE operations, the data to be deleted must meet the condition for the filter rule to take effect. For UPDATE operations, both the data before and after the update must meet the condition for the filter rule to take effect.
>- The rule entered must be a valid Boolean expression, which is more rigorous than MySQL. Some MySQL-supported syntaxes that may trigger a warning (such as comparing a string with a number, and c1 + c2 < "abc") are not supported here. The rules and priority levels of logical, arithmetic, and comparison operations are the same as those in MySQL. The priority levels of operations can be changed through parentheses. Even if there is a NULL, the operation rules are still the same as those in MySQL. DTS will verify the entered conditional filter rule and issue an alert if the rule is invalid.
>- Basic operation rules are as follows:
> - A column name can be imported as a variable.
>  - Logical operations (NOT, AND, OR, XOR, &&, and ||) are supported.
>  - Numerical types (signed/unsigned integer types TINYINT, SMALLINT, MEDIUMINT, INT, and BIGINT, floating point types FLOAT and DOUBLE, and exact type DECIMAL) and their arithmetic operations (+, -, \*, /, %, DIV, and MOD) and comparison operations (=, !=, >, <, >=, <=, <>, and <=>) are supported.  
>  - String types (CHAR and VARCHAR) and their comparison operations (binary comparison) are supported.  
>  - Data types (DATE, DATETIME, and TIMESTAMP) and their comparison operations are supported. 
>  - Time type (TIME) and its comparison operations are supported. A date/time-type variable can be compared with a string. In this case, the string will be converted into a date/time-type constant for comparison according to the date/time comparison rules.  
>  - The default time zone of the entered `TIMESTAMP` is UTC+0, and it will be converted to a time in UTC+0 for comparison. 
>    Example: If the entered filter rule is 'c1 > "2016-10-01 09:00:00"', where `c1` is a TIMESTAMP-type column, then "2016-10-01 09:00:00" will be parsed as a time in the UTC+0 time zone, i.e., "2016-10-01 09:00:00 +00:00" for comparison, and `c1` will also be converted into a time in UTC+0.
>   
3. Click **OK**.
4. Click **Save and Go Next** to proceed with the subsequent sync task process.

