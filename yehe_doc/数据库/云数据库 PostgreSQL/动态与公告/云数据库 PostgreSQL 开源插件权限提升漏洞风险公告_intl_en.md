Dear user,

We have detected that Wiz, an external security organization, disclosed a privilege escalation vulnerability in an open-source PostgreSQL database extension. This vulnerability allows attackers with database login privileges and operable extensions to execute arbitrary functions for system command execution.

## Impacts

  Affected TencentDB for PostgreSQL extensions include but are not limited to the following: 



- pg_cron
- adminpack
- amcheck
- file_fdw
- pageinspect
- pg_surgery
- pg_visibility
- pg_cron
- pg_bigm
- postgis
- postgis_raster
- postgis_sfcgal
- postgis_tiger_geocoder
- postgis_topology
- timescaledb
- zhparser
- tencentdb_stat
- plv8
- babelfishpg_common
- babelfishpg_money
- babelfishpg_tds
- babelfishpg_tsql
- tencentdb_superuser  
- tencentdb_stat

## Suggestions

​       Currently, we haven’t observed the abuse of this vulnerability in TencentDB for PostgreSQL. But considering extension risks, we are fixing the affected products. We will disable the creation and the upgrade of these extensions after 18:00 on April 20, 2023. The created extensions can still be used without affecting the normal use of other features for the instance. You can upgrade minor version in a self-service manner in the TencentDB for PostgreSQL console to restore the use of extensions after April 27, 2023. As the system will be restarted during the upgrade, ensure that your business has a reconnection mechanism. If you have any questions, submit a ticket.
