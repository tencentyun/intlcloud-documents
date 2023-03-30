
云数据库 SQL Server 通过收缩所有数据库文件释放未使用的空间，可以减小数据库的大小，您可以通过 SQL Server 控制台直接对数据库进行收缩。

## 单个收缩数据库
1. 登录 [SQL Server 控制台](https://console.cloud.tencent.com/sqlserver)，在实例列表，单击实例 ID 或**操作**列的**管理**，进入实例管理页面。
2. 在实例管理页面，选择**数据库管理**页，选择目标数据库所在行，在**操作**列选择**其它** > **收缩数据库**。
![](https://main.qcloudimg.com/raw/ffc76302b167d3a198ddcb3310125b07.png)
3. 在弹出的对话框，展示了数据库名称及收缩至剩余空间的比例，当前仅支持收缩至剩余空间的10%。
>!收缩数据库后，将仅剩当前剩余空间的10%，若收缩至剩余空间10%后不足2GB，将实际保留2GB空间。
>
<img src="https://main.qcloudimg.com/raw/d778ec0f30dfd19ada706dbd2280a84d.png" style="zoom:50%;" /><br>
您可以通过**数据库管理**页右上角的**当前任务**，查看收缩数据库的任务进度。
<img src="https://main.qcloudimg.com/raw/e31bf0fe34402b71f0cc76e2b3843d73.png" style="zoom:50%;" />

## 批量收缩数据库
1. 登录 [SQL Server 控制台](https://console.cloud.tencent.com/sqlserver) ，在实例列表，单击实例 ID，进入实例管理页面。
2. 在实例管理页面，选择**数据库管理**页，勾选目标数据库行，在列表上方选择**批量管理** > **批量收缩数据库**。
![](https://main.qcloudimg.com/raw/3f2cc7da03c47fdcee08cce3fd804822.png)
3. 在弹出的对话框，展示了数据库名称及收缩至剩余空间的比例，当前仅支持收缩至剩余空间的10%。
>!收缩数据库后，将仅剩当前剩余空间的10%，若收缩至剩余空间10%后不足2GB，将实际保留2GB空间。
>
<img src="https://main.qcloudimg.com/raw/38ddbb2395dd0f1b54dc5e63ca584180.png" style="zoom:50%;" /><br>
您可以通过数据库管理页右上角的**当前任务**，查看收缩数据库的任务进度。
<img src="https://main.qcloudimg.com/raw/e31bf0fe34402b71f0cc76e2b3843d73.png" style="zoom:50%;" />

