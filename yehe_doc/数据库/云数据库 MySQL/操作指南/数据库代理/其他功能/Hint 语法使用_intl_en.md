This document describes how to use the hint syntax on the database proxy.

The hint syntax can be used to forcibly execute SQL requests on the specified instance. A hint has the highest routing priority. For example, it is not subject to consistency and transaction constraints.You need to reasonably evaluate whether it is required in your business scenario before using it.
>!
>- When using the MySQL command line tool to connect and use the `HINT` statement, you need to add the `-c` option in the command; otherwise, the hint will be filtered by the tool.
>- The database proxy kernel version greater than or equal to version 1.1.3 supports `PREPARE` statement when the hint syntax is used through the database proxy.

Currently, three types of hints are supported:

- Assign to the source instance for execution:
```
/* to master */
or
/*FORCE_MASTER*/   
``` 
- Assign to a read-only instance for execution:
```
/* to slave */
or
/*FORCE_SLAVE*/  
```  
- Specify an instance for execution: 
```
/* to server server_name*/
```
`server_name` can be a short ID, such as `/* to server test_ro_1 */`.
