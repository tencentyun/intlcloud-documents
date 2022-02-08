Parameters in TencentDB for MySQL have been optimized on the basis of official default values in MySQL. We recommend that you configure the following parameters for the TencentDB for MySQL instance after purchase based on your business scenarios.

### character_set_server
- Default value: UTF8
- Restart required: yes
- Description: configure the default character set for the MySQL server. TencentDB for MySQL offers four character sets: LATIN1, UTF8, GBK, and UTF8MB4. Among them, LATIN1 supports English characters, with one character having one byte; UTF8 is generally used for international encoding that contains all characters used by all countries, with one character having three bytes; in GBK, every character has two bytes; and UTF8MB4 (a superset of UTF8) is completely backward compatible and supports emojis, with one character having four bytes.
- Recommendation: after purchasing an instance, you need to select the appropriate character set based on the data format required in your business to ensure that the client and the server use the same character set, preventing garbled text and unnecessary restarts.

### lower_case_table_names
- Default value: 0
- Restart required: yes
- Description: when creating a database or table, you can set whether storage and query operations are case-sensitive. This parameter can be set to 0 (case-sensitive) or 1 (case-insensitive). The default value is 0.
- Recommendation: TencentDB for MySQL is case-sensitive by default. We recommend that you configure this parameter based on your business needs and usage habits.

### sql_mode
- Default values:
```
NO_ENGINE_SUBSTITUTION (v5.6); ONLY_FULL_GROUP_BY, STRICT_TRANS_TABLES, NO_ZERO_IN_DATE, NO_ZERO_DATE, ERROR_FOR_DIVISION_BY_ZERO, NO_AUTO_CREATE_USER, NO_ENGINE_SUBSTITUTION (v5.7)
```
- Restart required: no
- Description: TencentDB for MySQL can operate in different SQL modes, which define the SQL syntax and data check that it should support.
The default value of this parameter in v5.6 is `NO_ENGINE_SUBSTITUTION`, which means that if the used storage engine is disabled or not compiled, an error will be thrown; in v5.7, the default values are `ONLY_FULL_GROUP_BY, STRICT_TRANS_TABLES, NO_ZERO_IN_DATE, NO_ZERO_DATE, ERROR_FOR_DIVISION_BY_ZERO, NO_AUTO_CREATE_USER, NO_ENGINE_SUBSTITUTION`.
Notes:
 - If `ONLY_FULL_GROUP_BY` is enabled, MySQL rejects queries for which the select list, `HAVING` condition, or `ORDER BY` list refer to nonaggregated columns that are neither named in the `GROUP BY` clause nor are functionally dependent on `GROUP BY` columns.
 - `STRICT_TRANS_TABLES` enables strict SQL mode. `NO_ZERO_IN_DATE` controls whether the server permits dates in which the year part is nonzero but the month or day part is zero. The effect of `NO_ZERO_IN_DATE` depends on whether strict SQL mode is enabled.
 - `NO_ZERO_DATE` controls whether the server permits a zero date as valid. Its effect depends on whether strict SQL mode is enabled.
 - `ERROR_FOR_DIVISION_BY_ZERO` means that in strict SQL mode, if data is divided by zero during the INSERT or UPDATE process, an error rather than a warning will be generated, while in non-strict SQL mode, NULL will be returned.
 - `NO_AUTO_CREATE_USER` prohibits the GRANT statement from creating a user whose password is empty.
 - `NO_ENGINE_SUBSTITUTION` means that if the storage engine is disabled or not compiled, an error will be thrown.
- Recommendation: as different SQL modes support different SQL syntax, we recommend that you configure them based on your business needs and development habits.

### long_query_time
- Default value: 10
- Restart required: no
- Description: used to define the time threshold for slow queries, with the default value as 10s. If a query execution takes 10s or longer, the execution details will be recorded in the slow log for future analysis.
- Recommendation: as business scenarios and performance sensitivity may vary, we recommend that you set the value in consideration of future performance analysis.

