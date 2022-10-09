云数据库 SQL Server 控制台提供备份的文件列表，并可以通过内网和外网地址下载备份文件，通过下载的备份文件可将数据库恢复到其他数据库（如自建数据库）。
本文为您介绍如何通过控制台下载备份（包含本地备份及跨地域备份）。

## 操作步骤
### 运行中实例备份下载
1. 登录 [SQL Server 控制台](https://console.cloud.tencent.com/sqlserver)。
2. 在上方选择地域，找到所需实例，单击实例 ID 或**操作**列的**管理**，进入实例管理页。
![](https://qcloudimg.tencent-cloud.cn/raw/1b41988a3ab435f3aa4154f293c1558a.png)
3. 在实例管理页，选择**备份管理**页，可通过选择数据备份列表或日志备份列表查看对应备份文件。
   - 若备份文件形式设置为打包备份，则在备份列表的**操作**列，单击**下载**，进入下载页，选择与实例同地域的备份即下载的备份为本地备份，选择与实例不同地域的备份即下载的备份为跨地域备份。![](https://main.qcloudimg.com/raw/30fb714fc7a8751b2833f50a2c0de654.png)
   - 若备份文件形式设置为单库备份，则在备份列表的**操作**列，选择**查看详情** > **下载**，进入下载页，下载该实例中每一个数据库的备份文件。
![](https://qcloudimg.tencent-cloud.cn/raw/1c00e970360331b3cd7f530f2ba4dcfb.png)
4. 在弹出的对话框，获取文件的下载地址，运用 wget 命令进行内网高速下载或单击**本地下载**。
>?
>- 推荐您复制内网下载地址，并 [登录到云数据库所在 VPC 下的 CVM（Linux 系统）](https://intl.cloud.tencent.com/document/product/213/10517)中，运用 wget 命令进行内网高速下载，更高效。
>- 下载地址的有效期为15分钟，超过15分钟后，需要重新进入下载页面获取新生成的下载地址。
>- 使用 wget 下载时需要对 URL 添加英文引号。
>
![](https://main.qcloudimg.com/raw/b7a7289733af5100008952ed1ba3b589.png)


### 已隔离实例备份下载
已隔离状态下的实例，也支持备份下载。
1. 登录 [SQL Server 控制台](https://console.cloud.tencent.com/sqlserver)。
2. 在上方选择地域，找到需要下载备份的实例，在其**操作**列选择**更多** > **备份下载**，进入备份下载页进行下载。
![](https://qcloudimg.tencent-cloud.cn/raw/5fd26f42851c161815be3cc5e24a1ccc.png)
   - 若备份文件形式设置为打包备份，则在备份列表的**操作**列，单击**下载**，进入下载页，下载该实例的备份文件。
   - 若备份文件形式设置为单库备份，则在备份列表的**操作**列，选择**查看详情** > **下载**，进入下载页，下载该实例中每一个数据库的备份文件。
   ![](https://qcloudimg.tencent-cloud.cn/raw/a96d2310328e0aa4adede1f57d2e7886.png)
   <img src="https://qcloudimg.tencent-cloud.cn/raw/1377fedd4f9384c50dfe27066a43a958.png"  style="zoom:80%;">
