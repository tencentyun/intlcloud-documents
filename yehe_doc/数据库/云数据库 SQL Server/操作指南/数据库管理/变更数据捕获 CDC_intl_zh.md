
变更数据捕获（CDC）用于捕获应用到 SQL Server 表中的插入、更新和删除活动，并以方便使用的关系格式来提供这些变更的详细信息。

变更数据捕获所使用的更改表中，包含镜像所跟踪源表列结构的列，同时还包含了解所发生的变更所需的元数据。对表开启了变更数据捕获之后，对该表的所有 DML 和 DDL 操作都会被记录，有助于跟踪表的变化。

## 单库开启/关闭变更数据捕获 CDC
1. 登录 [SQL Server 控制台](https://console.cloud.tencent.com/sqlserver)，在实例列表，单击实例 ID 或**操作**列的**管理**，进入实例管理页面。
2. 在实例管理页面，选择**数据库管理**页，选择目标数据库所在行，在**操作**列选择**其它** > **开启/关闭变更数据捕获**。
![](https://main.qcloudimg.com/raw/b527d8852328d14a7a375dc0ab693d76.png)
3. 在弹出的对话框，展示了数据库的名称及当前 CDC 状态，对 CDC 进行开启或者关闭的操作后，单击**确定**。
<img src="https://main.qcloudimg.com/raw/ea3716dbfcbbd14eec5a84faa057137a.png" style="zoom:40%;" /><br>
您可以通过**数据库管理**页右上角的**当前任务**，查看开启或关闭变更数据捕获 CDC 的任务进度。
<img src="https://main.qcloudimg.com/raw/e31bf0fe34402b71f0cc76e2b3843d73.png" style="zoom:50%;" />

## 批量开启/关闭变更数据捕获 CDC
1. 登录 [SQL Server 控制台](https://console.cloud.tencent.com/sqlserver)，在实例列表，单击实例 ID，进入实例管理页面。
2. 在实例管理页面，选择**数据库管理**页，勾选目标数据库行，在列表上方选择**批量管理** > **批量开启/关闭变更数据捕获**。
![](https://main.qcloudimg.com/raw/492b21e192566c64c17917325160182b.png)
3. 在弹出的对话框，展示了所选数据库的名称及当前 CDC 状态，对 CDC 进行开启或者关闭的操作后，单击**确定**。
<img src="https://main.qcloudimg.com/raw/ea3716dbfcbbd14eec5a84faa057137a.png" style="zoom:40%;" /><br>
您可以通过**数据库管理**页右上角的**当前任务**，查看开启或关闭变更数据捕获 CDC 的任务进度。
<img src="https://main.qcloudimg.com/raw/e31bf0fe34402b71f0cc76e2b3843d73.png" style="zoom:50%;" />
