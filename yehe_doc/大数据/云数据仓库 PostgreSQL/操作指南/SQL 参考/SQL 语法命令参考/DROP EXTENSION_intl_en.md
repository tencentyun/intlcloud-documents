It removes an extension from a database.

## Synopsis
```sql
DROP EXTENSION [ IF EXISTS ] name [, ...] [ CASCADE | RESTRICT ]
```

## Description
`DROP EXTENSION` removes extensions from the database. Dropping an extension causes its component objects to be dropped as well.
>!The required supporting extension files what were installed to create the extension are not deleted. The files must be manually removed from the database hosts.

You must own the extension to use `DROP EXTENSION`.

This command fails if any of the extension objects are in use in the database. For example, if a table is defined with columns of the extension type. Add the `CASCADE` option to forcibly remove those dependent objects.
>?Before issuing a `DROP EXTENSION` with the `CASCADE` keyword, you should be aware of all object that depend on the extension to avoid unintended consequences.

## Parameters
IF EXISTS
Do not throw an error if the extension does not exist. A notice is issued.

name
The name of an installed extension.

CASCADE
Automatically drop objects that depend on the extension, and in turn all objects that depend on those objects.

RESTRICT
Refuse to drop an extension if any objects depend on it, other than the extension member objects. This is the default.

## Compatibility
`DROP EXTENSION` is a database extension.

## See Also
CREATE EXTENSION, ALTER EXTENSION
