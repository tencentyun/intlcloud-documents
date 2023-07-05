
您可以通过 [MySQL 控制台](https://console.cloud.tencent.com/cdb) 查看和修改部分参数，并可以在控制台查询参数修改记录。
>?主实例和只读实例均支持通过控制台修改参数，操作方法一致，可参见下文进行操作。

## 注意事项
- 为保证实例的稳定，控制台仅开放部分参数的修改，控制台的参数配置页面展示的参数即为用户可以修改的参数。
- 如果修改的参数需要重启实例才生效，系统会提示您是否重启，建议您在业务低峰期操作，并确保应用程序具有重连机制。
- 如果希望恢复为默认公式，清空输入的参数内容并应用。

## 通过参数列表修改参数
### [批量修改参数](id:plxgcs)
1. 登录 [MySQL 控制台](https://console.cloud.tencent.com/cdb)，在实例列表，单击实例 ID 或**操作**列的**管理**，进入实例管理页面。
2. 选择**数据库管理** > **参数设置**页，单击**批量修改参数**。
主实例界面如下：
![](https://qcloudimg.tencent-cloud.cn/raw/0236dc88558f16937f71daca3e2d8d0f.png)
只读实例界面如下：
![](https://staticintl.cloudcachetci.com/yehe/backend-news/fjTY752_61.png)
3. 在**参数运行值**列，选择需要修改的参数进行修改，确认无误后，单击**确认修改**。
![](https://qcloudimg.tencent-cloud.cn/raw/1f904a228aa0ee6bb28f870f3238396c.png)
4. 在弹出的对话框，选择参数任务的**执行方式**，单击**确定**。
>?
>- 若选择**立即执行**，所选实例的参数变更任务会立即执行并生效。
>- 若选择**维护时间内**，所选实例的参数变更任务会在实例的 [维护时间](https://intl.cloud.tencent.com/document/product/236/10929) 内执行并生效。
>

### [修改单个参数](id:xgdgcs)
1. 登录 [MySQL 控制台](https://console.cloud.tencent.com/cdb)，在实例列表，单击实例 ID，进入实例管理页面。
2. 选择**数据库管理** > **参数设置**页，选择目标参数所在行，在**参数运行值**列，单击<img src="https://main.qcloudimg.com/raw/788902e3f8c335cf17de420f7181c2a8.png"  style="margin:0;">修改参数值。
![](https://qcloudimg.tencent-cloud.cn/raw/d6bce1222a71d69a26bfc85a52feedea.png)
3. 根据**参数可修改值**列的提示，输入目标参数值，单击<img src="https://main.qcloudimg.com/raw/1f4c7f2e0744bc601efb5d9fb04a7a04.png"  style="margin:0;">保存，单击<img src="https://main.qcloudimg.com/raw/2106cb4b9337a1a2fff5908581d2a908.png"  style="margin:0;">可取消操作。
![](https://main.qcloudimg.com/raw/41c7d73d4c5d404a112f54c3a63da726.png)
4. 在弹出的对话框，选择参数任务的**执行方式**，单击**确定**。
>?
>- 若选择**立即执行**，所选实例的参数变更任务会立即执行并生效。
>- 若选择**维护时间内**，所选实例的参数变更任务会在实例的 [维护时间](https://intl.cloud.tencent.com/document/product/236/10929) 内执行并生效。
>

## 通过导入参数模板修改参数
### 方式一：通过参数设置页面导入
1. 登录 [MySQL 控制台](https://console.cloud.tencent.com/cdb)，在实例列表，单击实例 ID，进入实例管理页面。
2. 选择**数据库管理** > **参数设置**页，单击**自定义模板**（若之前没有设置过常用的自定义模板，可通过 MySQL 控制台，左侧导航栏的参数模板进入找到自定义模板，单击创建模板即可预先设置参数模板，之后即可通过第2步从自定义模板导入）。
![](https://qcloudimg.tencent-cloud.cn/raw/4eab1607d41b9bb420135141d68da1b6.png)
3. 在弹出的对话框，选择参数模板，单击**导入并覆盖原有参数**。
![](https://qcloudimg.tencent-cloud.cn/raw/8bb98a9e921f3aae984d12b3dc7909c1.png)
4. 确认参数后，单击**确认修改**。
![](https://qcloudimg.tencent-cloud.cn/raw/1fa0b69eda99b5d4a799082cf8fde7e5.png)
5. 在弹出的对话框，选择参数任务的**执行方式**，单击**确定**。
>?
>- 若选择**立即执行**，所选实例的参数变更任务会立即执行并生效。
>- 若选择**维护时间内**，所选实例的参数变更任务会在实例的 [维护时间](https://intl.cloud.tencent.com/document/product/236/10929) 内执行并生效。
>

### 方式二：通过导入参数配置文件修改参数
1. 登录 [MySQL 控制台](https://console.cloud.tencent.com/cdb)，在实例列表，单击实例 ID，进入实例管理页面。
2. 选择**数据库管理** >**参数设置**页，单击**导入参数**。
![](https://qcloudimg.tencent-cloud.cn/raw/81f1a98c44457434e69d9660c084a358.png)
3. 单击**选择文件**找到需要的参数文件，然后单击**导入并覆盖原有参数**。
![](https://main.qcloudimg.com/raw/42fb6ef8936131a3bc776e492478e745.png)
4. 确认参数后，单击**确认修改**。
5. 在弹出的对话框，选择参数任务的执行方式，单击**确定**。
>?
>- 若选择**立即执行**，所选实例的参数变更任务会立即执行并生效。
>- 若选择**维护时间内**，所选实例的参数变更任务会在实例的 [维护时间](https://intl.cloud.tencent.com/document/product/236/10929) 内执行并生效。


### 方式三：通过参数模板页面导入
请参见 [应用参数模板于实例](https://intl.cloud.tencent.com/document/product/236/31906)。

## 恢复为默认模板
1. 登录 [MySQL 控制台](https://console.cloud.tencent.com/cdb)，在实例列表，单击实例 ID，进入实例管理页面。
2. 选择**数据库管理** > **参数设置**，单击**默认模板**，可选择**高稳定性模板**或**高性能模板**，之后单击**导入并覆盖原有参数**。
![](https://qcloudimg.tencent-cloud.cn/raw/030f986ea488796d5c084cb97aec5d6b.png)
3. 单击**确认修改**，跳转至参数修改确认窗口。
![](https://qcloudimg.tencent-cloud.cn/raw/5ba2e9ba71f33211db43637e0aed8f37.png)
4. 在弹出的对话框，选择参数任务的执行方式，阅读和勾选**重启规则**，单击**确定**即可。
>?
>- 若选择**立即执行**，所选实例的参数变更任务会立即执行并生效。
>- 若选择**维护时间内**，所选实例的参数变更任务会在实例的 [维护时间](https://intl.cloud.tencent.com/document/product/236/10929) 内执行并生效。
>

## 参数公式[](id:CSGSMYSQL)
实例的参数设置支持使用公式，将与实例规格相关的参数设置为公式，当实例规格发生变更时，此处设置的参数值会动态变化，对于变更后的规格仍然适用，使实例始终保持业务运行所需的最佳状态。

参考参数 innodb_buffer_pool_size 的设置：{DBinitMemory\*786432}，当实例规格中 DBinitMemory 变更时，此处的参数配置无需修改，innodb_buffer_pool_size 的值将会自动变更。
![](https://qcloudimg.tencent-cloud.cn/raw/696a0d3be52c058124f7c678a18e6b27.png)

表达式语法的相关支持详见下表。

| 支持类别 | 支持说明                                                     | 样例                                                         |
| :------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| 变量     | DBinitMemory：实例规格的内存大小，整数型。例如，实例规格的内存大小为4000MB，则 DBinitMemory 的值为4000。 DBInitCpu：实例规格的 CPU 核数，整数型。 例如，实例规格为8核，则 DBInitCpu 的值为8。 | {DBinitMemory * 786432} 即：内存大小（DBinitMemory）* 百分比（系统默认为75%）* 1024 * 1024（单位换算） |
| 运算符   | 公式语法：使用`{}`包裹。 除法运算符（/）：用被除数除以除数，返回整数型商。如果计算结果为小数，会截断取整数部分。不支持小数，例如系统支持 {MIN(DBInitMemory/4+500,1000000)}，不支持 {MIN(DBInitMemory\*0.25+500,1000000)}。 乘法运算符（\*）：两个乘数相乘，返回整数型积。如果计算结果为小数，会截断取整数部分。不支持小数运算。 | -                                                            |
| 函数     | 函数 MAX()，返回整数型或者参数公式列表中最大的值。 函数 MIN()，返回整数型或者参数公式列表中最小的值。 | {MAX(DBInitCpu/2,4)}                                         |


### 支持参数公式的参数
>?云数据库 MySQL 不断优化参数设置，以下仅列举部分支持参数公式的参数，您可在控制台参数模板下了解更多参数公式。

| 参数名称        | 参数描述                           | 默认公式                          |
| :----------------- | :-------------------------------- | :-------------------------------- |
| thread_pool_size             | 该参数设置线程池中线程组的数量，默认值时表示线程组数与 CPU 数量一致。 | {MIN(DBInitCpu,64)}               |
| table_open_cache_instances   | 指的是 MySQL 缓存 table 句柄的分区的个数。                   | {MIN(DBInitMemory/1000,16)}       |
| table_open_cache             | 表描述符缓存大小，可减少文件打开/关闭次数。                  | {MAX(DBInitMemory\*512/1000,2048)} |
| table_definition_cache       | 打开的表缓存实例的数量。                                     | {MAX(DBInitMemory\*512/1000,2048)} |
| max_connections              | 最大连接数。                                                 | {MIN(DBInitMemory/4+500,1000000)} |
| join_buffer_size             | 用于普通索引扫描、范围索引扫描和执行全表扫描的表连接的缓冲区的最小大小。 | {MIN(DBInitMemory\*128,262144)}    |
| innodb_write_io_threads      | InnoDB 中用于写操作的 I/O 线程数。                           | {MAX(DBInitCpu/2,4)}              |
| innodb_read_io_threads       | InnoDB 中用于读操作的 I/O 线程数。                           | {MAX(DBInitCpu/2,4)}              |
| innodb_buffer_pool_instances | InnoDB 缓冲池划分的区域数。                                  | {MIN(DBInitMemory/2000,16)}       |
| innodb_buffer_pool_size      | 缓冲池的大小（以字节为单位），InnoDB 缓存表和索引数据的内存区域。 | {DBInitMemory\*786432}             |


## 导出参数配置文件
1. 登录 [MySQL 控制台](https://console.cloud.tencent.com/cdb)，在实例列表，单击实例 ID，进入实例管理页面。
2. 选择**数据库管理** > **参数设置**页，单击**导出参数**导出参数配置文件。
![](https://qcloudimg.tencent-cloud.cn/raw/5a8357f189cc68ff63ccfe08efecaec4.png)

## 导出参数配置为参数模板
1. 登录 [MySQL 控制台](https://console.cloud.tencent.com/cdb)，在实例列表，单击实例 ID，进入实例管理页面。
2. 选择**数据库管理** > **参数设置**页，单击**另存为模板**，可将现有参数配置存储为参数模板。
![](https://qcloudimg.tencent-cloud.cn/raw/5e93d4f27f975b7d7adac82ff42d7fae.png)

## 自定义时间修改参数
执行参数修改的最后一步时，在弹出的对话框，可自定义参数的修改时间。
>?选择**维护时间内**，所选实例的参数变更任务会在实例的 [维护时间](https://intl.cloud.tencent.com/document/product/236/10929) 内执行并生效。
>
![](https://qcloudimg.tencent-cloud.cn/raw/33fb2f56d3fb40db0a6771fa8fb43825.png)

## 取消参数修改任务
选择**维护时间内**的修改参数任务提交后，如需取消修改参数，可在任务执行前（即任务状态为**等待执行**），在左侧导航 [**任务列表**](https://console.cloud.tencent.com/mysql/task) 页，单击**操作**列的**撤销**，取消参数修改任务。
![](https://main.qcloudimg.com/raw/566fd9374d0d59b38ceb99d310b782a9.png)

## 查看参数修改记录
1. 登录 [MySQL 控制台](https://console.cloud.tencent.com/cdb)，在实例列表，单击实例 ID，进入实例管理页面。
2. 选择**数据库管理** > **参数设置**页，单击右侧的**最近修改记录**。
![](https://main.qcloudimg.com/raw/93494ebb3b80a6547f1c6fe7bcbf9c8a.png)
3. 在最近参数修改记录页，可查看近期参数修改记录。

## 后续操作
- 您可以使用数据库参数模板来批量管理数据库的参数配置，请参见 [使用参数模板](https://intl.cloud.tencent.com/document/product/236/31906)。
- 相关重要参数的配置建议，请参见 [参数配置建议](https://intl.cloud.tencent.com/document/product/236/38056)。
