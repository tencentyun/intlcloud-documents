TDSQL-C MySQL 版的备份包含数据备份和 binlog 备份，备份方式分为自动备份和手动备份，其中自动备份产生的备份文件不支持删除，TDSQL-C MySQL 版支持根据用户业务需求设置备份保留的时间周期，用户可以通过调整备份保留时间缩短或延长此类备份的保存周期，到期后这部分备份将自动删除。

本文为您介绍通过控制台设置备份保留时间。

>?binlog 备份保留时间不得小于数据备份保留时间。

## 操作步骤
1. 登录 [TDSQL-C MySQL 版控制台](https://console.cloud.tencent.com/cynosdb)。
2. 选择地域，在集群列表，找到需要的集群，单击集群 ID 或操作列的**管理**，进入集群管理页面。
3. 在集群管理页面，选择**备份管理**页，单击**自动备份设置**。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/P9eE337_18.png)
4. 在备份设置窗口，分别设置数据备份和 binlog 备份保留时间，单击**确定**。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/XaNV418_19.png)
