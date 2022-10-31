
## 操作场景
用户可通过 TDSQL MySQL版 控制台下载云数据库的冷备数据、binlog。

## 操作步骤
1. 登录 [TDSQL MySQL版 控制台](https://console.cloud.tencent.com/dcdb)，单击实例 ID 或**操作**列的**管理**，进入实例管理页面。
2. 选择**备份与恢复** > **冷备列表**或 **Binlog 列表**。
3. 选择对应的分片 ID 及时间，在**操作**列单击**下载**。
4. 在弹出的对话框，提供了在 VPC 内网中下载此备份的地址，单击**获取下载链接**。
5. [登录到云数据库所在 VPC 下的 CVM（Linux 系统） ](https://www.tencentcloud.com/document/product/213/10517)中，运用 wget 命令进行下载。
>?
>- 外网下载：请在左侧导航**数据库备份**页的**下载设置**中开启外网下载，下载链接可直接复制到浏览器进行下载。
>- 内网下载：请在 VPC 网络中进行访问，使用 wget 命令下载：`wget -O <自定义名称.log> '<文件下载地址>'`。
>- 地址有效期为15分钟，过期后请重新刷新页面获取。
>
![](https://qcloudimg.tencent-cloud.cn/raw/0a00a20c0e13ffb3168026ca600bb151.png)
