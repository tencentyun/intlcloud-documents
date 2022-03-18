本文为您介绍如何设置会话级连接池功能。

## 背景条件
- [数据库代理版本大于等于1.1.2](https://intl.cloud.tencent.com/document/product/236/45627)。
- 主实例数据库版本为 MySQL 5.7，数据库内核小版本大于或等于20211031，如不满足，可先 [升级数据库内核小版本](https://intl.cloud.tencent.com/document/product/236/36816)。

## 未开启数据库代理
1. 登录 [MySQL 控制台](https://console.cloud.tencent.com/cdb)。
2. 在上方选择地域，单击实例 ID 或**操作**列的**管理**，进入实例管理页。
3. 在实例管理页的**数据库代理**页，单击**立即开启**。
4. 在弹出的对话框，可开启连接池功能。
![](https://qcloudimg.tencent-cloud.cn/raw/ae2436546dfc7c8f0f8b6c6d6f154482.png)

## 已开启数据库代理
1. 登录 [MySQL 控制台](https://console.cloud.tencent.com/cdb)。
2. 在上方选择地域，单击实例 ID 或**操作**列的**管理**，进入实例管理页。
3. 在实例管理页的**数据库代理**页，在概览下方的连接池后单击**开启**。
![](https://qcloudimg.tencent-cloud.cn/raw/9524cadfc5fe0d67a8a050f44ea5fada.png)
4. 在弹出的对话框，选择相关配置，单击**确定**。
   - **连接池状态**：设置开启连接池。
   - **连接池类型**：支持会话级别连接池。
   - **连接保留阈值**：闲置连接放到代理的连接池中保留的时间阈值，设置范围为：1秒 - 300秒。
>!连接池配置调整完成时，会有秒级别闪断，请确保业务具备重连机制。
>
![](https://qcloudimg.tencent-cloud.cn/raw/f354aa701758d2823c67468392e37617.png)
5. 连接池开启成功后，可在数据库代理页的**概览** > **基本信息**，查看详情和编辑配置。

## 关闭连接池功能
1. 登录 [MySQL 控制台](https://console.cloud.tencent.com/cdb)。
2. 在上方选择地域，单击实例 ID 或**操作**列的**管理**，进入实例管理页。
3. 在实例管理页的**数据库代理**页，在概览下方的连接池后单击**详情 / 编辑**。
4. 在弹出的对话框，选择相关配置，单击**确定**。
![](https://qcloudimg.tencent-cloud.cn/raw/6367f83dd1aaacc0dae91e9ec1085955.png)

