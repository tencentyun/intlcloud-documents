This document describes how to use the hint syntax on the database proxy.

The hint syntax can be used to forcibly execute SQL requests on the specified instance. A hint has the highest routing priority, and it is not subject to consistency and transaction constraints. You need to evaluate whether it is required in your business scenario before using it.
>!
>- When using the TDSQL-C for MySQL command line tool to connect and use the `HINT` statement, you need to add the `-c` option in the command; otherwise, the hint will be filtered out by the tool.
>- If you use the hint syntax through the database proxy, `PREPARE` is currently not supported but will be in future versions.

Currently, three types of hints are supported:

- Assign to the read-write instance for execution:
```
/* to master */
Or
/*FORCE_MASTER*/   
``` 
- Assign to a read-only instance for execution:
```
/* to slave */
Or
/*FORCE_SLAVE*/  
```  
- Assign to a specified instance for execution:
```
/* to server server_name*/
```
`server_name` can be a short ID, such as `/* to server test_ro_1 */`.
