本文介绍 Windows 环境如何使用帆软 FineBI 工具搭配云数据仓库 PostgreSQL，进行数据的可视化分析。

## 前提条件
1. 已创建云数据仓库 PostgreSQL 集群，并申请外网 IP，可参考 [申请外网地址](https://intl.cloud.tencent.com/document/product/1138/45132)。
2. 将本机的 IP 添加到云数据仓库 PostgreSQL 的白名单，可参考 [管理 IP 白黑名单](https://intl.cloud.tencent.com/document/product/1138/45133)。
3. 下载并安装帆软，单击下载 [帆软](https://www.finebi.com/product/download)。

## 操作步骤
1. 连接云数据仓库 PostgreSQL，需要下载 JDBC Driver，参见 [Pivotal Greenplum Database 数据连接](https://help.finebi.com/doc-view-289.html)。
从该页面中下载`org.postgresql.Driver`，并将该驱动包放置`%FineBI%\webapps\webroot\WEB-INF\lib`（Windows 下为安装目录）下，重启 FineBI。
2. 打开客户端，设置管理员账号后，选择数据库，单击**内置数据库**中的**直接登录**。

3. 选择**管理系统 > 数据连接 > 数据连接管理**，单击**新建数据连接**，在**所有**选项下选择 **Pivotal Greenplum Database**。
4. 填写数据库连接信息：
 - 驱动：选择`org.postgresql.Driver`。
 - 数据库名称：云数据仓库 PostgreSQL 如果没有创建数据库，默认使用 postgres。
 - 主机：需要提前将本机的 IP 加入云数据仓库 PostgreSQL 的白名单中，否则将会返回带有"no pg_hba.conf entry"的错误信息。
5. 单击**点击连接数据库**，连接成功后，页面会有提示。
6. 保存数据源。这里需要选择正确的模式，默认是拉取第一个，通常是系统模式。
