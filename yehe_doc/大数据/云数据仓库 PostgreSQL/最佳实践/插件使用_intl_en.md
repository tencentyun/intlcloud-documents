## Background
CDWPG is based on the massively parallel processing (MPP) cluster architecture of PostgreSQL, so it is compatible with certain extensions in the PostgreSQL ecosystem. This document lists such extensions and how to use them. If you need to use other extensions, [contact us](https://intl.cloud.tencent.com/contact-us).

## Extension List
- postgis: v2.5.2, a spatial database extension as detailed in [geospatial](https://github.com/greenplum-db/geospatial).
- hll: v2.14, a HyperLogLog algorithm extension as detailed in [postgresql-hll](https://github.com/citusdata/postgresql-hll).
- roaringbitmap: v0.2.66, a compressed bitmap algorithm extension as detailed in [gpdb-roaringbitmap](https://github.com/zeromax007/gpdb-roaringbitmap).
- orafce: v3.7, an Oracle function compatibility extension as detailed in [orafce](https://github.com/orafce/orafce).
- pgcrypto: v1.1, an encryption extension as detailed in [pgcrypto](https://www.postgresql.org/docs/9.4/pgcrypto.html).
- fuzzystrmatch: v1.0, an extension used to determine similarities and distance between strings as detailed in [fuzzystrmatch](https://www.postgresql.org/docs/9.4/fuzzystrmatch.html).

## Directions

CDWPG does not create the above extensions by default. You can create or delete extensions as needed with the following syntax:
```
CREATE EXTENSION {extension name};
DROP EXTENSION {extension name}
```
>!The scope of extensions is the database, which means that within each database where an extension is needed, you need to first run the `CREATE` statement.

To see the extensions currently installed in the database and their versions, use the following syntax:
```
test_db=> \dx
                                                  List of installed extensions
  Name   | Version |   Schema   |                                          Description
ion                                          
---------+---------+------------+--------------------------------------------------
---------------------------------------------
 hll     | 2.14    | public     | Type for storing hyperloglog data
 orafce  | 3.7     | public     | Functions and operators that emulate a subset of 
functions and packages from the Oracle RDBMS
 plpgsql | 1.0     | pg_catalog | PL/pgSQL procedural language
(3 rows)
```
