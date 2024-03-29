本文为您介绍 TDSQL-C MySQL 版支持上报告警的事件类型。

| 事件中文名 | 事件英文名 | 事件描述 |
|---------|---------|---------|
| 内存 OOM | GuestOom | 系统内存使用过载|
| 实例只读（存储超限） | DiskOverQuota | 存储空间容量超过限制，无法写入，只能读取|
| 数据库代理挂载节点剔除 | ProxyNodeFaultEliminated |因故障导致数据库代理挂载节点剔除 |
| 数据库代理异常 | ProxyUnHealthy | 数据库代理出现异常|
| HA（实例高可用） | HA | 实例发生 HA|
| 版本升级事件 | UpgradeVersion | 集群执行小版本升级|
| 跨可用区延迟 | CrossAzReplicationLag | 跨可用区主备延迟过高 |
| 云 API 操作事件（基于云审计投递） | ApiCall | 用户调用云 API 的操作|
| 控制台操作事件（基于云审计投递） | ConsoleCall | 用户使用控制台的操作|
