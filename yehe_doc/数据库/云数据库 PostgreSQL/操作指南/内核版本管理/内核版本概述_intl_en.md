This document describes the background and strengths of TencentDB for PostgreSQL kernel versions.

## Background
PostgreSQL (PG) is a globally popular enterprise-grade open-source database. It won the DB-Engines DBMS of the Year awards for two consecutive years in 2017–2018 and again in 2020. It also won the O'Reilly Open Source Convention (OSCON) Lifetime Achievement Award in 2019.

Built on top of the community version of PostgreSQL, TencentDB for PostgreSQL offers specific features and optimized kernels based on its many years of business expertise. It not only optimizes the PostgreSQL database engine, permission management, and replication performance, but also improves the database usability and maintainability in the cloud.

## Kernel Version Number
The kernel version number consists of two parts: **community version number** and **internal version number**.
```
v{community major version number.community minor version number}_r{incompatible version number.compatible version number}
Example: v12.7_r1.1
```
v stands for version, and r stands for release; for example, v12.7_r1.1 corresponds to the community version 12.7, where r1.1 indicates Tencent Cloud's iteration version composed of `r{incompatible version number}.{compatible version number}`.

>?
>- Version: it is the PostgreSQL community version number composed of two numbers: major version and minor version. The former starts from 10 (9.3, 9.4, 9.5, 9.6, and so on), and the latter starts from 1. When a >community minor version is released, Tencent Cloud will regularly follow the community to update the version.
>- Release: it is the version number used for TencentDB for PostgreSQL iteration and represents the modifications made by TencentDB for PostgreSQL. It consists of two numbers: incompatible version (starting from 1) and >compatible version (starting from 0).
> - Incompatible version number
>Definition of "incompatible": when a new database kernel program is used to start a database instance, if the start fails or some features cannot be used normally, the modification is incompatible.
>When the kernel contains incompatible features, the incompatible version number needs to be increased by 1. It will be used to determine whether the minor version upgrade can be performed directly.
> - Compatible version number
>When a compatible modification is added, the compatible version number needs to be increased by 1.

## Supported Versions
- PostgreSQL 10
- PostgreSQL 11
- PostgreSQL 12
- PostgreSQL 13

You can view the database version of TencentDB for PostgreSQL in the instance list in the [console](https://console.cloud.tencent.com/postgres). Different version numbers represent different compatible community versions; for example, TencentDB for PostgreSQL 12 is compatible with all subversions of open-source PostgreSQL 12.x, 12.1, 12.2, 12.3, etc.

| Kernel Version Number | Release Date | Compatible Community Version | Release Notes | Support Status |
|---------|---------|---------|---------|---------|
| v9.3.5_r1.0 |2017-07-24| PostgreSQL 9.3.x | [Release Notes](https://www.postgresql.org/docs/release/9.3.5/) | No longer supported for purchase |
| v9.5.4_r1.0 |2017-07-24| PostgreSQL 9.5.x | [Release Notes](https://www.postgresql.org/docs/release/9.5.4/) | No longer supported for purchase |
| v9.3.25_r1.1 |2021-12-09| PostgreSQL 9.3.x | [Release Notes](https://www.postgresql.org/docs/release/9.3.25/) | No longer supported for purchase |
| v9.5.25_r1.1 |2021-12-09| PostgreSQL 9.5.x | [Release Notes](https://www.postgresql.org/docs/release/9.5.25/) | No longer supported for purchase |
| v10.4_r1.0 |2018-11-24| PostgreSQL 10.x | [Release Notes](https://www.postgresql.org/docs/release/10.4/) | Supported |
| v10.17_r1.1 |2021-12-09| PostgreSQL 10.x | [Release Notes](https://www.postgresql.org/docs/release/10.17/) | Supported |
| v11.8_r1.0 |2020-05-12| PostgreSQL 11.x | [Release Notes](https://www.postgresql.org/docs/release/11.8/) | Supported |
| v11.12_r1.1 |2021-12-09| PostgreSQL 11.x | [Release Notes](https://www.postgresql.org/docs/release/11.12/) | Supported |
| v12.4_r1.0 |2020-12-24| PostgreSQL 12.x | [Release Notes](https://www.postgresql.org/docs/release/12.4/) | Supported |
| v12.7_r1.1 |2021-12-09| PostgreSQL 12.x | [Release Notes](https://www.postgresql.org/docs/release/12.7/) | Supported |
| v13.3_r1.0 |2021-12-09| PostgreSQL 13.x | [Release Notes](https://www.postgresql.org/docs/release/13.3/) | Supported |


## Version Rules
- Version and release together form a complete version called database kernel version.
- A major version corresponds to a community evolution branch iterated separately, such as 10, 11, and 12, who have their own respective version number sequence.
- When the community announces that a major version will no longer be maintained, the version will become unavailable for purchase. However, Tencent Cloud will continue to support database instances running on this version until they are actively terminated or migrated.
- The minor version follows the changes in the community, while the release changes according to the feature changes made by the kernel of TencentDB.

## Strengths
Compared with open-source PostgreSQL, TencentDB for PostgreSQL has the following strengths:
- Greater stability
On the basis of open-source PostgreSQL, TencentDB for PostgreSQL further optimizes some underlying implementations of the database service, substantially reducing the problem of database crashes due to external factors and improving the database stability.
- Enhanced primary-standby sync performance
The primary-standby sync performance of open-source PostgreSQL is severely compromised when a high number of DDL statements are processed. TencentDB for PostgreSQL is greatly optimized in this regard, with an overall improvement of up to 100,000 times.
- Shorter access latency
TencentDB for PostgreSQL features special optimization for connection establishment in scenarios with a large number of non-persistent connections. This reduces the database connection performance loss by 80% and greatly improves the non-persistent connection performance.
