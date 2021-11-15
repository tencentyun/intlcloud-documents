
## Global Consistency of Distributed Transactions
TDSQL-A for PostgreSQL adopts the global transaction manager (GTM) to dedicatedly ensure the consistency of distributed transactions, that is, it uses two-phase commit and global transaction management policies to guarantee transaction consistency in fully distributed environments. In addition, it provides a distributed transaction reliability guarantee mechanism to avoid problems such as resource blockage, data inconsistency, and CN failures.

## High Compatibility with SQL
TDSQL-A for PostgreSQL is compatible with SQL:2011 specifications and has a great advantage in SQL compatibility. It is compatible with most PostgreSQL syntaxes, such as complex query, foreign key, trigger, view, and stored procedure, meeting the needs of most enterprise users. It is also compatible with most Oracle data types and functions, facilitating business migration from Oracle data warehouses to TDSQL-A for PostgreSQL databases.

## Hybrid Row/Column Storage
On the basis of compatibility with row storage of the PostgreSQL ecosystem, TDSQL-A for PostgreSQL uses a proprietary column storage engine to provide complete column storage capabilities. You can select an appropriate storage format for the data to be written to the database based on your actual business needs.
The column storage of TDSQL-A for PostgreSQL provides powerful compression capabilities, including transparent compression and lightweight compression. The former supports compression algorithms such as zlib and zstd, and the latter supports delta, RLE, and bitpack algorithms. The algorithms can perform efficient compression according to the data characteristics with a compression ratio of up to 400+.

## Efficient Processing of Complex Queries
The proprietary new-generation vectorized execution engine of TDSQL-A for PostgreSQL has efficient processing capabilities for complex queries. It can return results for trillions of correlated subqueries within seconds, with a performance several times to even hundreds of times higher than that of open-source and traditional data warehouses. 

## Multi-Level Security Policies
The superuser privileges in traditional database system are too powerful and difficult to be controlled, which goes against the construction of a database security system. TDSQL-A for PostgreSQL uses a permission separation system where the traditional DBA role is divided into three independent roles: security admin, audit admin, and data admin. The security admin can configure data encryption rules based on the actual business needs to prevent data leakage. In addition, security features such as transparent data encryption and data masking are available.

## Comprehensive Peripheral Ecosystem
- TDSQL-A for PostgreSQL embraces the PostgreSQL ecosystem and keeps up with the community development. It supports a rich variety of ecosystem tools such as the PostGIS extension, JSON unstructured data type, and interconnection with other data sources through foreign data wrapper (FDW).
- Other data sources can be synced to TDSQL-A for PostgreSQL through a data migration service or product.

