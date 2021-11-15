

## Check Details 
- Check requirements: if the source database is Alibaba Cloud RDS, tables in it must have a primary key or non-null unique key.
- Check description: there are hidden columns in RDS tables. During migration without locks, tables without a primary key or non-null unique key may have the risk of data inconsistency.

## Fix
Modify the tables without a primary key or non-null unique key as prompted on the page and run the verification task again.

