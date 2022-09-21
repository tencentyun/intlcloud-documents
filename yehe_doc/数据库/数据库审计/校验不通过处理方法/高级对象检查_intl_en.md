
## MySQL/MariaDB/Percona check details
If you select to migrate/sync advanced objects, DTS will verify the following content. You must fix errors to continue the task. For warnings, you can ignore them based on business risk assessment and continue the task.

- Error: The target instance parameter `log_bin_trust_function_creators` must be `ON`.

- Warnings:
   - The advanced object migration/sync feature conflicts with the database/table renaming feature. After selecting advanced objects, you must cancel database/table renaming.
   - If you select functions or stored procedures as advanced objects, DTS will check whether `user1` corresponding to `DEFINER` (`[DEFINER = user1]`) in the source database is the same as the task execution account `user2`.
     - If they are the same, do not modify the settings after migration/sync.
     - If they are different, change the `SQL SECURITY` attribute of `user1` in the target database after migration/sync from `DEFINER` to `INVOKER` (`[INVOKER = user1]`), and set the `DEFINER` in the target database to the task execution account `user2` (`[DEFINER = task execution account user2]`).
     
   - Migration/Sync time of advanced objects:  
     - Stored procedures and functions: They will be migrated/synced during **source database export**. 
     - Triggers and events: If there are no incremental migration/sync tasks, they will be migrated/synced when the task stops; otherwise, they will be migrated/synced after you click **Done**, in which case the transition will take a longer time.

## Troubleshooting

Modify the `log_bin_trust_function_creators` parameter.

`log_bin_trust_function_creators` controls whether to allow users to write stored functions to the binlog. If it is set to `OFF`, only users with `SUPER` permissions can write stored function creation operations to the binlog. If it is set to `ON`, users with no `SUPER` permissions can also do this.

If an error occurs, troubleshoot as follows:

1. Log in to the source database.
2. Run the following command to modify the `log_bin_trust_function_creators` parameter:
```
set global log_bin_trust_function_creators = ON;
```
3. Run the following command to check whether the parameter modification takes effect:
```
show variables like '%log_bin_trust_function_creators%';
```
The system should display a result similar to the following:
```
mysql>  show variables like '%log_bin_trust_function_creators%';
+---------------------------------+-------+
| Variable_name                   | Value |
+---------------------------------+-------+
| log_bin_trust_function_creators | ON    |
```
4. Run the verification task again.


