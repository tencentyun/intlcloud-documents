## Check Details
Check whether the target database user conflicts with the source database user.

## Fix
In full database migration, if the target database has the same account as that in the source database, you need to delete it.
- If the account in the target database is the initial account, use it to log in to the database and run the following statements:
```
create user new user with password 'password';
grant pg_tencentdb_superuser to new username;
alter user new user with CREATEDB;
alter user new user with CREATEROLE;
```
- If the account in the target database is a new user, use it to log in to the database and delete the conflicting user.
```
drop user conflicting user;
# If the conflicting user has resource dependencies, run the following statement to modify the owner of the resources first (with a table as an example below):
alter table table name owner to new user;
```
After the conflicting user is deleted, run the verification task again.

