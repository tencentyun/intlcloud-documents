
### 如何把本地的 SQL 文件导入到 MySQL 数据库？
>?云数据库 MySQL 仅双节点、三节点实例支持 SQL 文件导入功能。
>
1. 登录 [云数据库 MySQL 控制台](https://console.cloud.tencent.com/cdb)，单击实例 ID 进入管理页。
2. 选择【数据库管理】>【数据库列表】>【数据导入】，选择导入文件，接下来选择目标数据库，最后确定导入。
>?导入的单个 SQL 文件不超过2GB，文件名仅允许英文、数字、下划线。
>
![](https://main.qcloudimg.com/raw/a8854e74caebb9c69d831dc1583c10c0.png)
详情请参见 [导入 SQL 文件](https://intl.cloud.tencent.com/document/product/236/8466)。

### 如何导出数据库数据？
- 如果需要导出备份数据，可通过 [控制台](https://console.cloud.tencent.com/cdb) 单击实例 ID 进入管理页，选择【备份恢复】页进行下载。
- 如果需要导出实时数据，可以购买 [只读实例](https://intl.cloud.tencent.com/document/product/236/7270)，连接实例后，通过 mysqldump 工具获取实时数据。

### 原数据库大概7GB，哪种方式最快迁移至云数据库 MySQL 中？
建议您使用 [数据迁移](https://intl.cloud.tencent.com/zh/document/product/571/34103) 功能，可以直接连到您的源库进行数据同步。

