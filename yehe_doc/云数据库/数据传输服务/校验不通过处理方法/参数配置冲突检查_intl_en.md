## Check Details
- Check requirements: check the following parameter values of the source and target databases. If a parameter has different values in the source database and target database, a verification warning will be reported, which will not block the migration task but will affect the business. You need to assess and determine whether to modify the parameter.
TimeZone, lc_monetary, lc_numeric, array_nulls, server_encoding, DateStyle, extra_float_digits, gin_fuzzy_search_limit, xmlbinary, and constraint_exclusion.

- Impact on the business: if the parameter values are different, data inconsistency between the source and target databases may be caused. Below is the specific impact:
  - TimeZone: sets the instance time zone. If this parameter has different values, data may be incorrect after migration.
  - lc_monetary: sets the instance currency mode. If this parameter has different values, currency numbers may be incorrect after migration.
  - lc_numeric: sets the instance numeric mode. If this parameter has different values, data may be incorrect after migration.
  - array_nulls: sets whether arrays can be empty. If this parameter has different values, data inconsistency may occur, and certain data may fail to be migrated.
  - server_encoding: sets the instance character set. If this parameter has different values, garbled characters may be present in the stored data.
  - DateStyle: sets the date format. If this parameter has different values, data migration may fail.
  - extra_float_digits: sets the floating-point value output precision. If this parameter has values, data precision will be affected. In high-precision database use cases, data inconsistency will occur after migration.
  - gin_fuzzy_search_limit: sets the upper limit of the size of the set returned by the GIN index. If this parameter has different values, data display inconsistency will occur after migration.
  - xmlbinary: sets the XML function conversion result. If this parameter has different values, function execution in the target database may be different from that in the source database.
  - constraint_exclusion: sets whether the restraints take effect. If this parameter has different values, data inconsistency may occur after migration. 


## Fix
1. Log in to the source database with the `superuser` account.
2. Run the following sample statements to modify the corresponding parameters:
   - You can choose to first modify the parameters in the source database. If such parameters cannot be modified, you need to modify them in the target database by [submitting a ticket](https://console.cloud.tencent.com/workorder/category).
   - The `server_encoding` parameter cannot be modified in the source database. If it is exceptional, check whether it has been created in the target database, and if so and it is different from that in the source database, you need to apply for a new instance; and if not, modify it as follows (currently, TencentDB instances only support two character sets: UTF-8 and LATIN):
```
alter system set timezone='parameter value';
alter system set lc_monetary='parameter value';
alter system set lc_numeric='parameter value';
```

