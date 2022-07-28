It loads a shared library file.

## Synopsis
```sql
LOAD 'filename'
```

## Description
This command loads a shared library file into the database server address space. If the file had been loaded previously, it is first unloaded. This command is primarily useful to unload and reload a shared library file that has been changed since the server first loaded it. To make use of the shared library, function(s) in it need to be declared using the `CREATE FUNCTION` command.

The file name is specified in the same way as for shared library names in `CREATE FUNCTION`; in particular, one may rely on a search path and automatic addition of the system's standard shared library file name extension.
>!In the database the shared library file (.so file) must reside in the same path location on every host in the database array (masters, segments, and mirrors).

## Parameters
filename
The path and file name of a shared library file. This file must exist in the same location on all hosts in your database array.

## Examples
Load a shared library file:
```sql
LOAD '/usr/local/snova-db/lib/myfuncs.so';
```

## Compatibility
`LOAD` is a database extension.

## See Also
CREATE FUNCTION
