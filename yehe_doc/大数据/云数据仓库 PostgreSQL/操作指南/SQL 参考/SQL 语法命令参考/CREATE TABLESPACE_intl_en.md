It defines a new tablespace.

## Synopsis
```sql
CREATE TABLESPACE tablespace_name [OWNER username] 
       FILESPACE filespace_name
```

## Description
`CREATE TABLESPACE` registers a new tablespace for your database system. The tablespace name must be distinct from the name of any existing tablespace in the system.

A tablespace allows superusers to define an alternative location on the file system where the data files containing database objects (such as tables and indexes) may reside.

A user with appropriate privileges can pass a tablespace name to `CREATE DATABASE`, `CREATE TABLE`, or `CREATE INDEX` to have the data files for these objects stored within the specified tablespace.

In the database, there must be a file system location defined for the master, each segment, and each mirror segment in order for the tablespace to have a location to store its objects across an entire system. This collection of file system locations is defined in a filespace object. A filespace must be defined before you can create a tablespace. See "gpfilespace" in the Database Utility Guide for more information.

## Parameters
tablespacename
The name of a tablespace to be created. The name cannot begin with `pg\_` or `gp\_`, as such names are reserved for system tablespaces.

OWNER username
The name of the user who will own the tablespace. If omitted, defaults to the user executing the command. Only superusers may create tablespaces, but they can assign ownership of tablespaces to non-superusers.

FILESPACE
The name of a database filespace that was defined using the `gpfilespace` management utility.

## Notes
You must first create a filespace to be used by the tablespace. See "gpfilespace" in the Database Utility Guide for more information. Tablespaces are only supported on systems that support symbolic links. `CREATE TABLESPACE` cannot be executed inside a transaction block.

## Examples
Create a new tablespace by specifying the corresponding filespace to use:
```sql
CREATE TABLESPACE mytblspace FILESPACE myfilespace;
```

## Compatibility
`CREATE TABLESPACE` is a database extension.

## See Also
CREATE DATABASE, CREATE TABLE, CREATE INDEX, DROP TABLESPACE, ALTER TABLESPACE

