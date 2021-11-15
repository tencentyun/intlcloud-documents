
## MySQL/TDSQL-C Check Details
- Check requirements: when exporting a view structure, DTS will check whether `user1` corresponding to `DEFINER` (`[DEFINER = user1]`) in the source database is the same as `user2` in the migration target.
   - If they are the same, do not modify the settings after migration.
   - If they are different, change the `SQL SECURITY` attribute of `user1` in the target database after migration from `DEFINER` to `INVOKER` (`[INVOKER = user1]`), and set the `DEFINER` in the target database to `user2` of the migration target (`[DEFINER = migration target user2]`).

- Check description: the `SQL SECURITY` parameter indicates according to whose permissions the system runs the command when a user accesses the specified view. 
  - `DEFINER`: only the definer can run the command.
  - `INVOKER`: only invokers with the invocation permissions can run the command.
By default, `DEFINER` is specified by the system.

## TDSQL for MySQL Check Details
Only a definer that is the same as the migration target's `user@host` is allowed; that is, when a view structure is exported, DTS will check whether the `user1` corresponding to the definer in the source database (`[DEFINER = user1]`) is the same with the `user2` in the migration target's `user@host`, and if yes, the view can be migrated; otherwise, it cannot.

For a definer different from that of the migration target's `user@host`, if you want to migrate it, you need to modify the definer in the source database view to the migration target's user, or do not select it during the migration/sync task and then manually sync the view after the task is completed.

