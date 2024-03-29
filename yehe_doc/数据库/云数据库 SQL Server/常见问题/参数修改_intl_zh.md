### 云数据库 SQL Server 如何修改时区？
云数据库 SQL Server 默认采用 China Standard Time 时区，由于**修改系统时区需要单独配置机器资源**，如需修改，请在购买实例前 [提交工单](https://console.cloud.tencent.com/workorder/category) 获取解决方案，并给出要调整的系统时区。关于系统时区和介绍和详细修改方法，请参见 [修改系统时区](https://intl.cloud.tencent.com/document/product/238/50257)。

### 云数据库 SQL Server 如何修改字符集排序规则？
云数据库 SQL Server 有实例维度及数据库维度两个维度的字符集排序规则：
- 实例维度的字符集排序规则默认是：Chinese_PRC_CI_AS，如需修改，请在购买前 [提交工单](https://console.cloud.tencent.com/workorder/category) 获取解决方案，并给出要调整的目标字符集，关于字符集的详细介绍请参见 [修改实例级字符集规则](https://intl.cloud.tencent.com/document/product/238/50258)。
- 数据库维度的字符集排序规则可以在数据库创建时指定，详见 [创建数据库](https://intl.cloud.tencent.com/document/product/238/35780)，如果不特别指定，则该数据库字符集默认采用 Chinese_PRC_CI_AS。

### 如何修改云数据库 SQL Server 的配置参数？
您可以登录 [SQL Server 控制台](https://console.cloud.tencent.com/sqlserver)，在实例列表，单击实例 ID，选择**参数配置** > **参数设置**页，修改实例的参数，详情请参见 [设置实例参数](https://intl.cloud.tencent.com/document/product/238/41609)。

### 云数据库 SQL Server 控制台支持快捷修改哪些参数？
您可以登录 [SQL Server 控制台](https://console.cloud.tencent.com/sqlserver)，在实例列表，单击实例 ID，选择**参数配置** > **参数设置**页，修改实例的参数，当前已支持如下参数修改。
- fill factor(%)
- max worker threads
- cost threshold for parallelism
- max degree of parallelism
- optimize for ad hoc workloads
- min server memory(MB)
- blocked process threshold(s)

[](id:CSXGLS)
### 如何查看云数据库 SQL Server 的参数修改历史？
您可以登录 [SQL Server 控制台](https://console.cloud.tencent.com/sqlserver)，在实例列表，单击实例 ID，选择**参数配置** > **修改历史**页，查看参数修改历史，详情请参见 [查看参数修改历史](https://intl.cloud.tencent.com/document/product/238/41610)。
