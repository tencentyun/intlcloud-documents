
### Step 1. Enable slow query logging for a self-built database
Check whether slow query logging is enabled first by logging in to the self-built database instance with the root account and running the following commands:
```
mysql> show variables like 'slow%';
+---------------------+----------------------------------------+
| Variable_name       | Value                                  |
+---------------------+----------------------------------------+
| slow_launch_time    | 2                                      |
| slow_query_log      | ON                                     |
| slow_query_log_file | /data/mysql/VM_83_217_centos-slow.log  |
+---------------------+----------------------------------------+
```

As shown above, if the value of `slow_query_log` is `ON`, slow query logging has been enabled; if it is `OFF`, you need to run the following command to enable the feature:
```
mysql> set global slow_query_log='ON';
```
>?The start command will become invalidated after the instance restarts. If you need to persist this configuration, you can modify the configuration file of the database instance (which is `/etc/my.cnf` by default) by adding the following content under `mysqld`:
>```
>root@xxx ~ # vim /etc/my.cnf
>[mysqld]
>slow_query_log=ON
>```
```

### Step 2. Modify the access permissions of the slow log file
After slow query logging is enabled, you can use the slow SQL analysis feature only when the agent is able to read the slow log file.
Run the `show variables like 'slow%'` command on the database instance to view the location of the slow log file:
```
mysql> show variables like 'slow%';
+----------------------+----------------------------------------+
| Variable_name        | Value                                  |
+----------------------+----------------------------------------+
| slow_launch_time     | 2                                      |
| slow_query_log       | ON                                     |
| slow_query_log_file  | /data/mysql/VM_83_217_centos-slow.log  |
+----------------------+----------------------------------------+
```

The value of `slow_query_log_file` is the location of the slow log file. It needs to be set to readable, and its upper directories need to be set to accessible:

```
root@xxx ~ # chmod 755 /data
For the above slow log file, the upper directories are `/data/mysql` and `/data`, and their access permissions need to be set in turn:
root@xxx ~ # chmod 755 /data/mysql
Then, set the log file to readable
root@xxx ~ # chmod 644 /data/mysql/VM_83_217_centos-slow.log
```

### Step 3. Enable slow log collection
1. Log in to the [DBbrain console](https://console.cloud.tencent.com/dbbrain/instance?product=mysql) and select **Instance Management** on the left sidebar. On the displayed page, select a database type at the top.
2. On the **Instance Management** page, enable slow log collection for the database instance. If it can be enabled normally without error, the slow log analysis feature is successfully configured.

```