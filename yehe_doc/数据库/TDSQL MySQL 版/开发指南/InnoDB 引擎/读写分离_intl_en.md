
TDSQL for MySQL instances support read/write separation in the following modes:
- A replica comment flag such as `/*slave*/` can be added in a SQL statement, and the `-c` parameter is added after `mysql` to parse `mysql -c -e "/*slave*/sql"` to send the SQL statements to the replica server.
>?Comment flags including `/*slave:slaveonly*/`, `/*slave:20*/`, and `/*slave:slaveonly,20*/` are also supported, where their values indicate the delay requirement that the replica server should satisfy, and `slaveonly` indicates that the query will not be sent to the source server if there is no eligible replica server.
>
```
//Read data from source//
select * from emp order by sal, deptno desc;
//Read data from replica//
/*slave*/ select * from emp order by sal, deptno desc;
```
- Requests sent by read-only accounts are sent to the replica server based on the configured attributes.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Bpmr055_10.png)
