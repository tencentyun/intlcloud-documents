
Parameters in TDSQL-C for MySQL have been optimized on the basis of official default values in MySQL. We recommend you configure the following parameters for your TDSQL-C for MySQL instance after purchase based on your business scenarios.

### character_set_server
- Default value: UTF8
- Whether restart is required: yes
- Role: it is used to configure the default character set of the TDSQL-C for MySQL server. TDSQL-C for MySQL provides four character sets: LATIN1, UTF8, GBK, and UTF8MB4.
 - LATIN1 supports English letters. Each character in it occupies 1 byte.
 - UTF8 contains the characters used by all countries/regions in the world and is an international encoding with a high universality. Each character in it occupies 3 bytes.
 - GBK uses 2 bytes to encode any character, that is, no matter whether it is a Chinese or English character, it is represented by 2 bytes.
 - As a superset of UTF8, UTF8MB4 is completely compatible with UTF8. Each character in it occupies 4 bytes, and emojis are supported.
- Recommendation: after purchasing an instance, you need to select the appropriate character set based on the data format required in your business to ensure that the client and the server use the same character set, preventing garbled text and unnecessary restarts.

### lower_case_table_names
- Default value: 0
- Whether restart is required: yes
- Role: when creating a database or table, you can set whether storage and query operations are case-sensitive. This parameter can be set to 0 (case-sensitive) or 1 (case-insensitive). The default value is 0.
- Recommendation: TencentDB for MySQL is case-sensitive by default. We recommend that you configure this parameter based on your business needs and usage habits.

### sql_mode
- Default values:
```
NO_ENGINE_SUBSTITUTION (v5.6); ONLY_FULL_GROUP_BY, STRICT_TRANS_TABLES, NO_ZERO_IN_DATE, NO_ZERO_DATE, ERROR_FOR_DIVISION_BY_ZERO, NO_AUTO_CREATE_USER, NO_ENGINE_SUBSTITUTION (v5.7)
```
- Whether restart is required: no
- Role: TencentDB for MySQL can operate in different SQL modes, which define the SQL syntax and data check that it should support.
 - The default value of this parameter on v5.6 is `NO_ENGINE_SUBSTITUTION`, indicating that if the used storage engine is disabled or not compiled, an error will be reported.
 - On v5.7 and v8.0, the default values are `ONLY_FULL_GROUP_BY, STRICT_TRANS_TABLES`, `NO_ZERO_IN_DATE, NO_ZERO_DATE`, `ERROR_FOR_DIVISION_BY_ZERO`, `NO_AUTO_CREATE_USER`, and `NO_ENGINE_SUBSTITUTION`.
Where:
   - If `ONLY_FULL_GROUP_BY` is enabled, MySQL rejects queries for which the select list, `HAVING` condition, or `ORDER BY` list refer to nonaggregated columns that are neither named in the `GROUP BY` clause nor are functionally dependent on `GROUP BY` columns.
   - `STRICT_TRANS_TABLES` enables strict SQL mode. `NO_ZERO_IN_DATE` controls whether the server permits dates in which the year part is nonzero but the month or day part is zero. The effect of `NO_ZERO_IN_DATE` depends on whether strict SQL mode is enabled.
   - `NO_ZERO_DATE` controls whether the server permits a zero date as valid. Its effect depends on whether strict SQL mode is enabled.
   - `ERROR_FOR_DIVISION_BY_ZERO` means that in strict SQL mode, if data is divided by zero during the INSERT or UPDATE process, an error rather than a warning will be generated, while in non-strict SQL mode, NULL will be returned.
   - `NO_AUTO_CREATE_USER` prohibits the GRANT statement from creating a user whose password is empty.
   - `NO_ENGINE_SUBSTITUTION` means that if the storage engine is disabled or not compiled, an error will be thrown.
- Recommendation: as different SQL modes support different SQL syntax, we recommend that you configure them based on your business needs and development habits.

### long_query_time
- Default value: 10
- Whether restart is required: no
- Role: used to define the time threshold for slow queries, with the default value as 10s. If a query execution takes 10s or longer, the execution details will be recorded in the slow log for future analysis.
- Recommendation: as business scenarios and performance sensitivity may vary, we recommend that you set the value in consideration of future performance analysis.


