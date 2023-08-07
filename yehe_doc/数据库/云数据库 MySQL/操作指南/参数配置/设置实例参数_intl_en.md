
You can view and modify certain parameters and query parameter modification logs in [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb).
>?You can modify the parameters of both source and read-only instances in the console in the same way as detailed below.

## Use Limits
- To ensure instance stability, only some parameters can be modified in the console. These parameters are displayed on the **Parameter Settings** page.
- If the modified parameter requires instance restart to take effect, the system will ask you if you want to restart. We recommend that you do so during off-peak hours and ensure that your application has a reconnection mechanism.
- If you want to return to the default formula, clear the entered parameters and apply.

## Modifying Parameters in Parameter List
### [Batch modifying parameters](id:plxgcs)
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). In the instance list, click an instance ID or **Manage** in the **Operation** column to access the instance management page.
2. Select **Database Management** > **Parameter Settings** and click **Batch Modify Parameters**.
UI for the source instance:
![](https://qcloudimg.tencent-cloud.cn/raw/0236dc88558f16937f71daca3e2d8d0f.png)
UI for the read-only instance:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/fjTY752_61.png)
3. Locate the desired parameters, and modify their values in the **Current Value** column. After confirming that everything is correct, click **Confirm Modification**.
![](https://qcloudimg.tencent-cloud.cn/raw/1f904a228aa0ee6bb28f870f3238396c.png)
4. In the pop-up window, select an option in the **Execution Mode** and click **OK**.
>?
>- If you select **Immediate execution**, the parameter modification task will be executed and take effect immediately.
>- If you select **During maintenance time**, the parameter modification task will be executed and take effect during this time. For more information, see [Setting Instance Maintenance Window](https://intl.cloud.tencent.com/document/product/236/10929).
>

### [Modifying one parameter](id:xgdgcs)
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), click an instance ID in the instance list, and enter the instance management page.
2. On the **Database Management** > **Parameter Settings** tab, locate the desired parameter in the parameter list and click <img src="https://main.qcloudimg.com/raw/788902e3f8c335cf17de420f7181c2a8.png"  style="margin:0;"> in the **Current Value** column.
![](https://qcloudimg.tencent-cloud.cn/raw/d6bce1222a71d69a26bfc85a52feedea.png)
3. Modify the value within the restrictions stated in the **Acceptable Values** column and click <img src="https://main.qcloudimg.com/raw/1f4c7f2e0744bc601efb5d9fb04a7a04.png"  style="margin:0;"> to save the modification. You can click <img src="https://main.qcloudimg.com/raw/2106cb4b9337a1a2fff5908581d2a908.png"  style="margin:0;"> to cancel the operation.
![](https://main.qcloudimg.com/raw/41c7d73d4c5d404a112f54c3a63da726.png)
4. In the pop-up window, select an option in the **Execution Mode** and click **OK**.
>?
>- If you select **Immediate execution**, the parameter modification task will be executed and take effect immediately.
>- If you select **During maintenance time**, the parameter modification task will be executed and take effect during this time. For more information, see [Setting Instance Maintenance Window](https://intl.cloud.tencent.com/document/product/236/10929).
>

## Modifying Parameters by Importing Parameter Template
### Option 1. Importing a parameter template on the **Parameter Settings** page
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), click an instance ID in the instance list, and enter the instance management page.
2. Select **Database Management** > **Parameter Settings** and click **Custom Template**. If you haven't configured a commonly used custom template yet, you can select **Custom Template** on the left sidebar in the TencentDB for MySQL console, click **Create Template** to configure a parameter template, and then import it from the custom template as described in this step.
![](https://qcloudimg.tencent-cloud.cn/raw/4eab1607d41b9bb420135141d68da1b6.png)
3. In the pop-up window, select a parameter template and click **Import and Overwrite Original Parameters**.
![](https://qcloudimg.tencent-cloud.cn/raw/8bb98a9e921f3aae984d12b3dc7909c1.png)
4. After confirming that everything is correct, click **Confirm Modification**.
![](https://qcloudimg.tencent-cloud.cn/raw/1fa0b69eda99b5d4a799082cf8fde7e5.png)
5. In the pop-up window, select an option in the **Execution Mode** and click **OK**.
>?
>- If you select **Immediate execution**, the parameter modification task will be executed and take effect immediately.
>- If you select **During maintenance time**, the parameter modification task will be executed and take effect during this time. For more information, see [Setting Instance Maintenance Window](https://intl.cloud.tencent.com/document/product/236/10929).
>

### Option 2. Modifying parameters by importing a parameter configuration file
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), click an instance ID in the instance list, and enter the instance management page.
2. Select **Database Management** > **Parameter Settings** and click **Import Parameters**.
![](https://qcloudimg.tencent-cloud.cn/raw/81f1a98c44457434e69d9660c084a358.png)
3. Click **Select File** to locate the desired parameter file and click **Import and Overwrite Original Parameters**.
![](https://main.qcloudimg.com/raw/42fb6ef8936131a3bc776e492478e745.png)
4. After confirming that everything is correct, click **Confirm Modification**.
5. In the pop-up window, select the **execution mode** and click **OK**.
>?
>- If you select **Immediate execution**, the parameter modification task will be executed and take effect immediately.
>- If you select **During maintenance time**, the parameter modification task will be executed and take effect during this time. For more information, see [Setting Instance Maintenance Window](https://intl.cloud.tencent.com/document/product/236/10929).


### Option 3. Importing a parameter template on the "Parameter Template" page
For more information, see [Managing Parameter Template > Applying a Parameter Template to a Database](https://intl.cloud.tencent.com/document/product/236/31906).

## Restoring to Default Template
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), click an instance ID in the instance list, and enter the instance management page.
2. Select **Database Management** > **Parameter Settings**, click **Default Template**, select **High-Stability Template** or **High-Performance Template**, and click **Import and Overwrite Original Parameters**.
![](https://qcloudimg.tencent-cloud.cn/raw/030f986ea488796d5c084cb97aec5d6b.png)
3. Click **Confirm Modification** to redirect to the parameter modification confirmation window.
![](https://qcloudimg.tencent-cloud.cn/raw/5ba2e9ba71f33211db43637e0aed8f37.png)
4. In the pop-up window, select an option in **Execution Mode**, read and indicate your consent to the **Restart Rules**, and click **OK**.
>?
>- If you select **Immediate execution**, the parameter modification task will be executed and take effect immediately.
>- If you select **During maintenance time**, the parameter modification task will be executed and take effect during this time. For more information, see [Setting Instance Maintenance Window](https://intl.cloud.tencent.com/document/product/236/10929).
>

## Parameter Formula[](id:CSGSMYSQL)
You can use a formula to set the instance parameters. To do so, set the parameters related to the instance specification as a formula, and when the instance specification is changed, the parameter values in the formula will be dynamically changed accordingly and still take effect after the specification change. In this way, the instance is always in the optimal state for running business smoothly.

Taking the `{DBinitMemory\*786432}` value of the parameter `innodb_buffer_pool_size` as an example, when the `DBinitMemory` in the instance specification is changed, the parameter configuration here doesn't need to be modified, and the value of `innodb_buffer_pool_size` will be changed automatically.
![](https://qcloudimg.tencent-cloud.cn/raw/696a0d3be52c058124f7c678a18e6b27.png)

Expression syntax is supported as follows:

| Supported Type | Description | Sample |
| :------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| Variable |DBinitMemory: Instance memory in MB (integer type). For example, if the memory size of the instance is 4000 MB, the value of DBinitMemory is 4000.  DBInitCpu: The number of CPU cores of the instance (integer type).  For example, if the instance specification is 8 cores, the value of DBInitCpu is 8. | {DBinitMemory * 786432} = memory size (DBinitMemory) * percentage (75% by default) * 1024 * 1024 (unit conversion) |
| Operator | Formula syntax: It should be enclosed in braces (`{}`).  Division operator (/): It divides the dividend by the divisor and returns an integer quotient. If the calculation result is a decimal number, only the integer part will be retained. Decimal numbers are not supported; for example, `{MIN(DBInitMemory/4+500,1000000)}` instead of `{MIN(DBInitMemory0.25+500,1000000)}` is supported. Multiplication operator (\*): It multiplies two numbers and returns an integer product. If the calculation result is a decimal number, only the integer part will be retained. Decimal number calculation is not supported. | -                                                            |
| Function | MAX(): It returns the greatest value in an integer or parameter formula list.  MIN(): It returns the smallest value in an integer or parameter formula list. | {MAX(DBInitCpu/2,4)}                                         |


### Parameters that support parameter formulas
>?TencentDB for MySQL continuously optimizes parameter settings. The following lists only certain parameters that support parameter formula. You can learn more about parameter formulas in the parameter template in the console.

| Parameter | Description | Default Formula |
| :----------------- | :-------------------------------- | :-------------------------------- |
| thread_pool_size | The number of thread groups in the thread pool. The default value means that the number of thread groups is the same as the number of CPU cores. | {MIN(DBInitCpu,64)} |
| table_open_cache_instances | The number of partitions where MySQL caches table handles.                   | {MIN(DBInitMemory/1000,16)} |
| table_open_cache | The size of the table descriptor, which can reduce the file open/close times.                  | {MAX(DBInitMemory\*512/1000,2048)} |
| table_definition_cache | The number of opened table cache instances.                                     | {MAX(DBInitMemory\*512/1000,2048)} |
| max_connections | Max connections.                                                 | {MIN(DBInitMemory/4+500,1000000)} |
| join_buffer_size | The minimum size of the buffer used for normal index scans, range index scans, and table joins that perform full-table scans. | {MIN(DBInitMemory\*128,262144)} |
| innodb_write_io_threads | The number of I/O threads in InnoDB used for write operations.                           | {MAX(DBInitCpu/2,4)} |
| innodb_read_io_threads | The number of I/O threads in InnoDB used for read operations.                           | {MAX(DBInitCpu/2,4)} |
| innodb_buffer_pool_instances | The number of partitions in the InnoDB buffer pool.                                  | {MIN(DBInitMemory/2000,16)} |
| innodb_buffer_pool_size | The size of the buffer pool in bytes, i.e., the memory zone where InnoDB caches tables and index data. | {DBInitMemory\*786432} |


## Exporting Parameter Configuration as File
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), click an instance ID in the instance list, and enter the instance management page.
2. Select **Database Management** > **Parameter Settings** and click **Export Parameters** to export the parameter configuration file.
![](https://qcloudimg.tencent-cloud.cn/raw/5a8357f189cc68ff63ccfe08efecaec4.png)

## Exporting Parameter Configuration as Template
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), click an instance ID in the instance list, and enter the instance management page.
2. Select **Database Management** > **Parameter Settings** and click **Save as Template** to save the existing parameter configuration as a parameter template.
![](https://qcloudimg.tencent-cloud.cn/raw/5e93d4f27f975b7d7adac82ff42d7fae.png)

## Modifying Parameters During Custom Time Window
Before you confirm the parameter modification, the **Modify Parameters** dialog box will pop up for you to select a custom time window for the modification to take effect.
>?If you select **During maintenance time**, the parameter modification task will be executed and take effect during this time. For more information, see [Setting Instance Maintenance Window](https://intl.cloud.tencent.com/document/product/236/10929).
>
![](https://qcloudimg.tencent-cloud.cn/raw/33fb2f56d3fb40db0a6771fa8fb43825.png)

## Canceling Parameter Modification Task
If a parameter modification task (to be executed **During maintenance window**) has been submitted but you want to cancel it, you can select **[Task List](https://console.cloud.tencent.com/mysql/task)** on the left sidebar in the console, locate the task, and click **Cancel** in the **Operation** column. You can cancel a task only before it is executed. The task status should be **Waiting for execution**.
![](https://main.qcloudimg.com/raw/566fd9374d0d59b38ceb99d310b782a9.png)

## Viewing Parameter Modification Log
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), click an instance ID in the instance list, and enter the instance management page.
2. On the **Database Management** > **Parameter Settings** tab, click **Recent Modifications** on the right.
![](https://main.qcloudimg.com/raw/93494ebb3b80a6547f1c6fe7bcbf9c8a.png)
3. You can view the recent parameter modification records here.

## Subsequent Operations
- You can use templates to manage database parameters in batches. For more information, see [Managing Parameter Template](https://intl.cloud.tencent.com/document/product/236/31906).
- For suggestions on the configuration of key parameters, see [Suggestions on Parameter Settings](https://intl.cloud.tencent.com/document/product/236/38056).
