It changes the value of a database configuration parameter.

## Synopsis
```sql
SET [SESSION | LOCAL] configuration_parameter {TO | =} value | 
    'value' | DEFAULT}
 
SET [SESSION | LOCAL] TIME ZONE {timezone | LOCAL | DEFAULT}
```

## Description
The `SET` command changes server configuration parameters. Any configuration parameter classified as a session parameter can be changed on-the-fly with `SET`. `SET` affects only the value used by the current session.

If `SET` or `SET SESSION` is issued within a transaction that is later aborted, the effects of the `SET` command disappear when the transaction is rolled back. Once the surrounding transaction is committed, the effects will persist until the end of the session, unless overridden by another `SET`.

The effects of `SET LOCAL` last only till the end of the current transaction, whether committed or not. A special case is `SET` followed by `SET LOCAL` within a single transaction: the SET LOCAL value will be seen until the end of the transaction, but afterwards (if the transaction is committed) the `SET` value will take effect.

If `SET LOCAL` is used within a function that includes a `SET` option for the same configuration parameter (see **CREATE FUNCTION**), the effects of the `SET LOCAL` command disappear at function exit; the value in effect when the function was called is restored anyway. This allows `SET LOCAL` to be used for dynamic or repeated changes of a parameter within a function, while retaining the convenience of using the `SET` option to save and restore the caller's value. Note that a regular `SET` command overrides any surrounding function's `SET` option; its effects persist unless rolled back.

If you create a cursor with the `DECLARE` command in a transaction, you cannot use the `SET` command in the transaction until you close the cursor with the `CLOSE` command.

## Parameters
SESSION
Specifies that the command takes effect for the current session. This is the default.

LOCAL
Specifies that the command takes effect for only the current transaction. After `COMMIT` or `ROLLBACK`, the session-level setting takes effect again. Note that `SET LOCAL` will appear to have no effect if it is executed outside of a transaction.

configuration_parameter
The name of a configuration parameter. Only parameters classified as *session* can be changed with `SET`. 

value
New value of parameter. Values can be specified as string constants, identifiers, numbers, or comma-separated lists of these. `DEFAULT` can be used to specify resetting the parameter to its default value. If specifying memory sizing or time units, enclose the value in single quotes.

TIME ZONE
`SET TIME ZONE value` is an alias for `SET timezone TO value`. The syntax `SET TIME ZONE` allows special syntax for the time zone specification. Here are examples of valid values:
```
'PST8PDT'
'Europe/Rome'
-7 (time zone 7 hours west from UTC)
INTERVAL '-08:00' HOUR TO MINUTE (time zone eight hours west from UTC).
	LOCAL
DEFAULT
```
Set the time zone to your local time zone (the one that the server's `timezone` defaults to).

## Examples
Set the schema search path:
```sql
SET search_path TO my_schema, public;
```
Increase the segment host memory per query to 200 MB:
```sql
SET statement_mem TO '200MB';
```
Set the style of date to traditional POSTGRES with "day before month" input convention:
```sql
SET datestyle TO postgres, dmy;
```
Set the time zone for Berkeley, California
```sql
SET TIME ZONE 'PST8PDT';
```
Set the time zone for Italy:
```sql
SET TIME ZONE 'Europe/Rome'; 
```

## Compatibility
`SET TIME ZONE` extends syntax defined in the SQL standard.

## See Also
RESET, SHOW
