尊敬的客户，您好：

​      近日，腾讯云监测到外部安全机构 Wiz 披露了一个第三方 PostgreSQL 数据库开源插件的权限提升漏洞，该漏洞允许具备数据库登录权限且可操作插件的攻击者执行任意函数，从而达到系统命令执行的目的。

## 【影响范围】

  当前已知受影响的云数据库 PostgreSQL 插件包括但不限于：

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

## 【修复建议】

​       腾讯云已具备该攻击利用的监测能力，当前暂未发现该漏洞实际利用行为，考虑到插件风险，我们正在对受影响产品进行修复。将于2023年4月20日19:00之后停止对这些插件的创建和升级，已创建插件可以正常使用，同时不影响数据库实例其他功能的正常使用。预计2023年4月27日之后您可以在 [云数据库 PostgreSQL 控制台](https://console.tencentcloud.com/postgres) 进行自助小版本升级，恢复插件的使用，升级时会有系统重启，请做好业务重连，如您有需求使用该类插件，请 [提工单](https://console.cloud.tencent.com/workorder/category) 联系我们。
