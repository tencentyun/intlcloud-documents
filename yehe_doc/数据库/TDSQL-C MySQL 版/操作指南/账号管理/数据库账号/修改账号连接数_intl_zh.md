TDSQL-C MySQL 版支持修改账号连接数限制（每个账号到数据库的最大连接数）。您可以在控制台修改账号的连接数限制，防止单个账号耗尽所有 TDSQL-C MySQL 版的连接。

本文为您介绍如何通过控制台修改数据库账号连接数。

## 操作步骤
1. 登录 [TDSQL-C MySQL 版控制台](https://console.cloud.tencent.com/cynosdb)。
2. 选择地域，在集群列表，找到需要的集群，单击集群 ID 或**操作**列的**管理**，进入集群管理页面。
3. 单击**账号管理**，在账号列表找到需要修改连接数的账号，在其**操作**列选择**更多** > **修改连接数**。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/kdPL311_9.png)
4. 在修改连接数弹窗里，输入**新连接数限制**，单击**确定**。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/zsBZ495_10.png)
>?连接数取值范围：1 - 10240，若不填写连接数，会受到最大连接数10240的限制。
