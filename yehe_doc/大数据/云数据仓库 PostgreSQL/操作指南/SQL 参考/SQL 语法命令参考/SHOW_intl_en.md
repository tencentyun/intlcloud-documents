It shows the value of a runtime parameter.

## Synopsis
```sql
SHOW configuration_parameter
SHOW ALL
```

## Description
`SHOW` displays the current settings of the database system configuration parameters. You can set these parameters with the `SET` statement, or by editing the `postgresql.conf` configuration file of the database master.
>!Note that some parameters viewable by `SHOW` are read-only — their values can be viewed but not set. See the Database Reference Guide for details.

## Parameters
configuration_parameter
The name of a system configuration parameter.

ALL
Shows the current value of all configuration parameters.

## Examples
Show the current setting of the parameter `search_path`:
```sql
SHOW search_path;
```
Shows the current value of all configuration parameters:
```sql
SHOW ALL;
```

## Compatibility
`SHOW` is a database extension.

## See Also
SET, RESET
