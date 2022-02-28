
This document describes the extensions supported by TencentDB for PostgreSQL.

## Extension Overview
TencentDB for PostgreSQL supports multiple open-source and proprietary extensions. They help you perform instance OPS easier and improve the query and write performance as well as various capabilities such as token query, data retrieval, and incremental data migration.

## Using Extension
Currently, TencentDB for PostgreSQL supports most common extensions for direct use. However, to enable certain extensions, you need to use specified versions or get special permissions. In this case, [submit a ticket](https://console.cloud.tencent.com/workorder/category) and provide the instance ID and extension name to enable it.

## Creating Extension
When creating an extension, the `pg_tencentdb_superuser` is temporarily escalated to superuser and passes all permission checks.
TencentDB for PostgreSQL extensions are managed at the database level. You can create different extensions for different databases, but databases cannot use extensions in other databases.
To create an extension, access the database with the client tool and run the following statements:
```
CREATE EXTENSION [ IF NOT EXISTS ] extension_name
[ WITH ]
[ SCHEMA schema_name ]
[ VERSION version ]
[ FROM old_version ]
```

## Viewing Created Extension
If you have installed extensions, you can run the following command to view the list of extensions installed in the current database:
- You can run the `\dx` command if you use the psql client.
```
\dx
                                        List of installed extensions
     Name      | Version |   Schema   |                             Description                             
---------------+---------+------------+---------------------------------------------------------------------
 amcheck       | 1.2     | public     | functions for verifying relation integrity
 bloom         | 1.0     | public     | bloom access method - signature file based index
 hstore        | 1.6     | public     | data type for storing sets of (key, value) pairs
 hstore_plperl | 1.0     | public     | transform between hstore and plperl
 jsonb_plperl  | 1.0     | public     | transform between jsonb and plperl
 plperl        | 1.0     | pg_catalog | PL/Perl procedural language
 plpgsql       | 1.0     | pg_catalog | PL/pgSQL procedural language
 postgis       | 3.0.2   | public     | PostGIS geometry, geography, and raster spatial types and functions
(8 rows)
```
- If you want to use SQL statements to view the extensions, run the `select * from pg_available_extensions where installed_version is not null;` statement to view the list of installed extensions.
```
        name      | default_version | installed_version |                               comment                               
---------------+-----------------+-------------------+---------------------------------------------------------------------
 plperl        | 1.0             | 1.0               | PL/Perl procedural language
 amcheck       | 1.2             | 1.2               | functions for verifying relation integrity
 hstore_plperl | 1.0             | 1.0               | transform between hstore and plperl
 plpgsql       | 1.0             | 1.0               | PL/pgSQL procedural language
 jsonb_plperl  | 1.0             | 1.0               | transform between jsonb and plperl
 hstore        | 1.6             | 1.6               | data type for storing sets of (key, value) pairs
 bloom         | 1.0             | 1.0               | bloom access method - signature file based index
 postgis       | 3.0.2           | 3.0.2             | PostGIS geometry, geography, and raster spatial types and functions
(8 rows)
```

## List of Supported Extensions
TencentDB for PostgreSQL supports multiple powerful and high-performance extensions. For the list of extensions supported by each database version, see [Supported Extensions](https://intl.cloud.tencent.com/document/product/409/7567).
