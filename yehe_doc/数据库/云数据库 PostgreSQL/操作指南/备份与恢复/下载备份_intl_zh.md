本文为您介绍通过 PostgreSQL 控制台下载备份的操作。

## 注意事项
- 内网地址与本地下载地址有效期均为15分钟，过期后请主动刷新页面重新获取。
- 使用 wget 下载时需要对 URL 添加英文引号。

## 操作步骤
### 数据备份下载
1. 登录 [PostgreSQL 控制台](https://console.cloud.tencent.com/pgsql)，选择地域，单击实例 ID，进入实例管理页面。
2. 在实例管理页面，选择**备份恢复**页，单击**备份列表**。
![](https://qcloudimg.tencent-cloud.cn/raw/25a170dc36f74ac1a00ec3e8f422fa8e.png)
3. 在备份列表下选择需要下载的备份，在其**操作**列单击**下载**。
4. 在下载窗口，提供内网 VPC 网络地址和本地下载两种下载方式。
>?推荐您复制下载地址，并 [登录到云数据库所在 VPC 下的 CVM（Linux 系统） ](https://intl.cloud.tencent.com/document/product/213/10517#.E6.AD.A5.E9.AA.A43.EF.BC.9A.E7.99.BB.E5.BD.95.E4.BA.91.E6.9C.8D.E5.8A.A1.E5.99.A8)中，运用 wget 命令进行内网高速下载，更高效。
>
![](https://qcloudimg.tencent-cloud.cn/raw/0af2893a802f8c4ce291ac05d9f45a98.png)

### 日志备份下载
1. 登录 [PostgreSQL 控制台](https://console.cloud.tencent.com/pgsql)，选择地域，单击实例 ID，进入实例管理页面。
2. 在实例管理页面，选择**备份恢复**页，单击**日志备份列表**。
![](https://qcloudimg.tencent-cloud.cn/raw/a07f4c7f9a53b837f8dc8ecad117d1f2.png)
3. 在日志备份列表下选择需要下载的备份，在其**操作**列单击**下载**。
4. 在下载窗口，提供内网 VPC 网络地址和本地下载两种下载方式。
![](https://qcloudimg.tencent-cloud.cn/raw/0af2893a802f8c4ce291ac05d9f45a98.png)
