## 任务相关接口

| 接口名称 | 接口功能 |
|---------|---------|
| [DescribeAsyncRequestInfo](/document/api/236/20410) | 查询异步任务的执行结果 |
| [DescribeTasks](/document/api/236/15848) | 查询云数据库实例任务列表 |

## 参数相关接口

| 接口名称 | 接口功能 |
|---------|---------|
| [CreateParamTemplate](/document/api/236/32663) | 创建参数模板 |
| [DeleteParamTemplate](/document/api/236/32824) | 删除参数模板 |
| [DescribeDefaultParams](/document/api/236/32662) | 查询默认的可设置参数列表 |
| [DescribeInstanceParamRecords](/document/api/236/32661) | 查询实例参数修改历史 |
| [DescribeInstanceParams](/document/api/236/20411) | 查询实例的可设置参数列表 |
| [DescribeParamTemplateInfo](/document/api/236/32660) | 查询参数模板详情 |
| [DescribeParamTemplates](/document/api/236/32659) | 查询参数模板列表 |
| [ModifyInstanceParam](/document/api/236/15860) | 修改实例参数 |
| [ModifyParamTemplate](/document/api/236/32658) | 修改参数模板 |

## 回档相关接口

| 接口名称 | 接口功能 |
|---------|---------|
| [DescribeRollbackRangeTime](/document/api/236/18726) | 查询可回档时间 |
| [StartBatchRollback](/document/api/236/18725) | 回档数据库表 |

## 备份相关接口

| 接口名称 | 接口功能 |
|---------|---------|
| [CreateBackup](/document/api/236/15844) | 创建云数据库备份 |
| [DeleteBackup](/document/api/236/15841) | 删除云数据库备份 |
| [DescribeBackupConfig](/document/api/236/15837) | 查询云数据库备份配置信息 |
| [DescribeBackupDatabases](/document/api/236/15840) | 查询备份数据库列表 |
| [DescribeBackupTables](/document/api/236/15846) | 查询指定数据库的备份数据表 |
| [DescribeBackups](/document/api/236/15842) | 查询备份日志 |
| [DescribeBinlogs](/document/api/236/15843) | 查询二进制日志 |
| [DescribeSlowLogs](/document/api/236/15845) | 查询慢查询日志 |
| [ModifyBackupConfig](/document/api/236/15839) | 修改数据库备份配置 |

## 安全组相关接口

| 接口名称 | 接口功能 |
|---------|---------|
| [AssociateSecurityGroups](/document/api/236/15852) | 安全组批量绑定云资源 |
| [DescribeDBSecurityGroups](/document/api/236/15854) | 查询实例安全组信息 |
| [DescribeProjectSecurityGroups](/document/api/236/15850) | 查询项目安全组信息 |
| [DisassociateSecurityGroups](/document/api/236/15851) | 安全组批量解绑云资源 |
| [ModifyDBInstanceSecurityGroups](/document/api/236/15853) | 修改云数据库安全组 |

## 实例相关接口

| 接口名称 | 接口功能 |
|---------|---------|
| [CloseWanService](/document/api/236/15863) | 关闭实例外网访问 |
| [CreateDBInstance](/document/api/236/15871) | 创建云数据库实例（包年包月） |
| [CreateDBInstanceHour](/document/api/236/15865) | 创建云数据库实例（按量计费） |
| [DescribeDBInstanceCharset](/document/api/236/15866) | 查询云数据库实例的字符集 |
| [DescribeDBInstanceConfig](/document/api/236/17491) | 查询云数据库实例的配置信息 |
| [DescribeDBInstanceGTID](/document/api/236/15862) | 查询云数据实例的GTID是否开通 |
| [DescribeDBInstanceRebootTime](/document/api/236/15874) | 查询云数据库实例的预期重启时间 |
| [DescribeDBInstances](/document/api/236/15872) | 查询实例列表 |
| [DescribeDBPrice](/document/api/236/18566) | 查询数据库价格 |
| [DescribeDBSwitchRecords](/document/api/236/17490) | 查询云数据库切换记录 |
| [DescribeDBZoneConfig](/document/api/236/17229) | 获取云数据库可售卖规格 |
| [DescribeTagsOfInstanceIds](/document/api/236/32666) | 获取实例绑定的tag |
| [InitDBInstances](/document/api/236/15873) | 初始化新实例 |
| [InquiryPriceUpgradeInstances](/document/api/236/32665) | 查询数据库升级价格 |
| [IsolateDBInstance](/document/api/236/15869) | 隔离云数据库实例 |
| [ModifyAutoRenewFlag](/document/api/236/19652) | 修改云数据库实例的自动续费标记 |
| [ModifyDBInstanceName](/document/api/236/15877) | 修改云数据库实例名 |
| [ModifyDBInstanceProject](/document/api/236/15868) | 修改云数据库实例的所属项目 |
| [ModifyDBInstanceVipVport](/document/api/236/15867) | 修改云数据库实例的IP和端口号 |
| [ModifyInstanceTag](/document/api/236/32664) | 修改实例标签 |
| [OpenDBInstanceGTID](/document/api/236/17489) | 开启实例的GTID |
| [OpenWanService](/document/api/236/15875) | 开通实例外网访问 |
| [RenewDBInstance](/document/api/236/30160) | 续费云数据库实例 |
| [RestartDBInstances](/document/api/236/17488) | 重启实例 |
| [SwitchForUpgrade](/document/api/236/15864) | 切换访问新实例 |
| [UpgradeDBInstance](/document/api/236/15876) | 升级云数据库实例 |
| [UpgradeDBInstanceEngineVersion](/document/api/236/15870) | 升级实例版本 |

## 数据导入相关接口

| 接口名称 | 接口功能 |
|---------|---------|
| [CreateDBImportJob](/document/api/236/15858) | 创建数据导入任务 |
| [DescribeDBImportRecords](/document/api/236/15856) | 查询数据库导入任务记录 |
| [DescribeUploadedFiles](/document/api/236/30161) | 查询导入SQL文件列表 |
| [StopDBImportJob](/document/api/236/15857) | 终止数据导入任务 |

## 数据库相关接口

| 接口名称 | 接口功能 |
|---------|---------|
| [DescribeDatabases](/document/api/236/17493) | 查询数据库 |
| [DescribeTables](/document/api/236/18727) | 查询数据库表 |

## 监控相关接口

| 接口名称 | 接口功能 |
|---------|---------|
| [DescribeDeviceMonitorInfo](/document/api/236/32668) | 物理机监控信息 |

## 账号相关接口

| 接口名称 | 接口功能 |
|---------|---------|
| [CreateAccounts](/document/api/236/17502) | 创建云数据库的账户 |
| [DeleteAccounts](/document/api/236/17501) | 删除云数据库的账号 |
| [DescribeAccountPrivileges](/document/api/236/17500) | 查询云数据库账户的权限信息 |
| [DescribeAccounts](/document/api/236/17499) | 查询云数据库的所有账号信息 |
| [DescribeSupportedPrivileges](/document/api/236/32825) | 查询云数据库实例支持的权限信息 |
| [ModifyAccountDescription](/document/api/236/17498) | 修改云数据库实例账号的备注信息 |
| [ModifyAccountPassword](/document/api/236/17497) | 修改云数据库实例账号的密码 |
| [ModifyAccountPrivileges](/document/api/236/17496) | 修改云数据库实例账号的权限 |
| [VerifyRootAccount](/document/api/236/17495) | 验证root账号权限 |

