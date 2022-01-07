
You can view and modify certain parameters and query parameter modification logs in [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb).

## Notes
- To ensure instance stability, only some parameters can be modified in the console. These parameters are displayed on the **Parameter Settings** page.
- If the modified parameter requires instance restart to take effect, the system will ask you if you wish to restart. We recommend you do so during off-peak hours and ensure that your application has a reconnection mechanism.
- If you want to return to the default formula, clear the entered parameters and apply.

## Modifying Parameters in Parameter List
### [Modifying parameters in batches](id:plxgcs)
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). In the instance list, click an instance ID or **Manage** in the **Operation** column to access the instance management page.
2. Select **Database Management** > **Parameter Settings** and click **Batch Modify Parameters**.
![](https://main.qcloudimg.com/raw/82c535bd50543645831988ca2e9b688e.png)
3. Locate the desired parameters, and modify their values in the **Current Value** column. After confirming that everything is correct, click **Confirm Modification**.
![](https://main.qcloudimg.com/raw/5307fbeef4b1fccef478ab7fd57b3167.png)
4. In the pop-up window, select the **execution mode** and click **OK**.
>?
>- If you select **Immediate execution**, the parameter modification task will be executed and take effect immediately.
>- If you select **During maintenance time**, the parameter modification task will be executed and take effect during the [instance maintenance time](https://intl.cloud.tencent.com/document/product/236/10929).
>

### [Modifying one parameter](id:xgdgcs)
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), click an instance ID in the instance list, and enter the instance management page.
2. On the **Database Management** > **Parameter Settings** tab, locate the desired parameter in the parameter list and click <img src="https://main.qcloudimg.com/raw/788902e3f8c335cf17de420f7181c2a8.png"  style="margin:0;"> in the **Current Value** column.
![](https://main.qcloudimg.com/raw/4687ed705274b76ec92c43b7f9d448ab.png)
3. Modify the value within the restrictions stated in the **Acceptable Values** column and click <img src="https://main.qcloudimg.com/raw/1f4c7f2e0744bc601efb5d9fb04a7a04.png"  style="margin:0;"> to save the modification. You can click <img src="https://main.qcloudimg.com/raw/2106cb4b9337a1a2fff5908581d2a908.png"  style="margin:0;"> to cancel the operation.
![](https://main.qcloudimg.com/raw/41c7d73d4c5d404a112f54c3a63da726.png)
4. In the pop-up window, select the **execution mode** and click **OK**.
>?
>- If you select **Immediate execution**, the parameter modification task will be executed and take effect immediately.
>- If you select **During maintenance time**, the parameter modification task will be executed and take effect during the [instance maintenance time](https://intl.cloud.tencent.com/document/product/236/10929).
>

## Modifying Parameters by Importing Parameter Template
### Method 1. Importing a parameter template on the "Parameter Settings" page
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), click an instance ID in the instance list, and enter the instance management page.
2. Select **Database Management** > **Parameter Settings** and click **Custom Template**. (If you haven't configured a commonly used custom template yet, you can select **Custom Template** on the left sidebar in the TencentDB for MySQL console, click **Create Template** to configure a parameter template, and then import it from the custom template as described in step 2.)
![](https://main.qcloudimg.com/raw/bd7a2fd3dc89895f1a3bd779d0fe8bbc.png)
3. In the pop-up window, select a parameter template and click **Import and Overwrite Original Parameters**.
![](https://main.qcloudimg.com/raw/2f649840f16befabea6259f9b4c7f47c.png)
4. After confirming that everything is correct, click **Confirm Modification**.
![](https://main.qcloudimg.com/raw/1673166256bc4d122f5a72c3c703ffab.png)
5. In the pop-up window, select the **execution mode** and click **OK**.
>?
>- If you select **Immediate execution**, the parameter modification task will be executed and take effect immediately.
>- If you select **During maintenance time**, the parameter modification task will be executed and take effect during the [instance maintenance time](https://intl.cloud.tencent.com/document/product/236/10929).
>

### Method 2. Modifying parameters by importing a parameter configuration file
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), click an instance ID in the instance list, and enter the instance management page.
2. Select **Database Management** > **Parameter Settings** and click **Import Parameters**.
![](https://main.qcloudimg.com/raw/52d6f069bbce29c933254593d59c0236.png)
3. Click **Select File** to locate the desired parameter file and click **Import and Overwrite Original Parameters**.
![](https://main.qcloudimg.com/raw/42fb6ef8936131a3bc776e492478e745.png)
4. After confirming that everything is correct, click **Confirm Modification**.
5. In the pop-up window, select the **execution mode** and click **OK**.
>?
>- If you select **Immediate execution**, the parameter modification task will be executed and take effect immediately.
>- If you select **During maintenance time**, the parameter modification task will be executed and take effect during the [instance maintenance time](https://intl.cloud.tencent.com/document/product/236/10929).


### Method 3. Importing a parameter template on the "Parameter Template" page
For more information, see [Managing Parameter Template > Applying a Parameter Template to a Database](https://intl.cloud.tencent.com/document/product/236/31906).

## Restoring to Default Template
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), click an instance ID in the instance list, and enter the instance management page.
2. Select **Database Management** > **Parameter Settings**, click **Default Template**, select **High-Stability Template** or **High-Performance Template**, and click **Import and Overwrite Original Parameters**.
![](https://qcloudimg.tencent-cloud.cn/raw/030f986ea488796d5c084cb97aec5d6b.png)
3. Click **Confirm Modification** to redirect to the parameter modification confirmation window.
![](https://qcloudimg.tencent-cloud.cn/raw/5ba2e9ba71f33211db43637e0aed8f37.png)
4. In the pop-up window, select the **execution mode**, read and indicate your consent to the **restart rules**, and click **OK**.
>?
>- If you select **Immediate execution**, the parameter modification task will be executed and take effect immediately.
>- If you select **During maintenance time**, the parameter modification task will be executed and take effect during the [instance maintenance time](https://intl.cloud.tencent.com/document/product/236/10929).
>

## Parameter Formula
You can use a formula to set the instance parameters. To do so, set the parameters related to the instance specification as a formula, and when the instance specification is changed, the parameter values in the formula will be dynamically changed accordingly and still take effect after the specification change. In this way, the instance is always in the optimal state required by smooth business operations.

Taking the `{DBinitMemory\*786432}` value of the parameter `innodb_buffer_pool_size` as an example, when the `DBinitMemory` in the instance specification is changed, the parameter configuration here doesn't need to be modified, and the value of `innodb_buffer_pool_size` will be changed automatically.
![](https://qcloudimg.tencent-cloud.cn/raw/696a0d3be52c058124f7c678a18e6b27.png)

Expression syntax is supported as follows:

| Supported Type | Description | Sample |
| -------- | ------------------------------------------------------------ | --------------------- |
| Variable   | <li>DBinitMemory: memory size of instance specification, which is an integer. For example, if the memory size of the instance specification is 4,000 MB, the value of `DBinitMemory` will be 4000.<li>DBInitCpu: number of CPU cores of instance specification, which is an integer. The value of the `innodb_buffer_pool_size` parameter in TencentDB for MySQL must be between 50% and 90% of the memory size. If the configured value is above 90% or below 50%, it will be automatically configured to 90% or 50% respectively. | {DBinitMemory*786432} |
| Operator | Formula syntax: it should be enclosed in braces (`{}`).  <li>Division operator (/): it divides the dividend by the divisor and returns an integer quotient. If the calculation result is a decimal number, only the integer part will be retained. Decimal numbers are not supported; for example, `{MIN(DBInitMemory/4+500,1000000)}` instead of `{MIN(DBInitMemory\*0.25+500,1000000)}` is supported.<li>Multiplication operator (*): it multiplies two numbers and returns an integer product. If the calculation result is a decimal number, only the integer part will be retained. Decimal number calculation is not supported. |  -                     |
| Function   | <li>MAX(): it returns the greatest value in an integer or parameter formula list. <li>MIN(): it returns the smallest value in an integer or parameter formula list.</li> | {MAX(DBInitCpu/2,4)}  |


## Exporting Parameter Configuration as File
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), click an instance ID in the instance list, and enter the instance management page.
2. Select **Database Management** > **Parameter Settings** and click **Export Parameters** to export the parameter configuration file.
![](https://main.qcloudimg.com/raw/6885ffbc45f3154ed203551a309e1848.png)

## Exporting Parameter Configuration as Template
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), click an instance ID in the instance list, and enter the instance management page.
2. Select **Database Management** > **Parameter Settings** and click **Save as Template** to save the existing parameter configuration as a parameter template.
![](https://main.qcloudimg.com/raw/fca4ec16b316948af812db9988d0c92c.png)

## Modifying Parameters During Custom Time Window
Before you confirm the parameter modification, the "Modify Parameters" dialog box will pop up for you to select a custom time window for the modification to take effect.
>?If you select **During maintenance time**, the parameter modification task will be executed and take effect during the [instance maintenance time](https://intl.cloud.tencent.com/document/product/236/10929).
>
![](https://main.qcloudimg.com/raw/00d4892fb614dd285cdec91a4a74cf2d.png)

## Canceling Parameter Modification Task
If a parameter modification or batch modification task has been submitted but you want to cancel it, you can select **[Task List](https://console.cloud.tencent.com/mysql/task)** on the left sidebar in the console, locate the task, and click **Cancel** in the **Operation** column. You can cancel a task only before it is executed. The task state should be **Waiting for execution**.
![](https://main.qcloudimg.com/raw/566fd9374d0d59b38ceb99d310b782a9.png)

## Viewing Parameter Modification Logs
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), click an instance ID in the instance list, and enter the instance management page.
2. On the **Database Management** > **Parameter Settings** tab, click **Recent Modifications** on the right.
![](https://main.qcloudimg.com/raw/93494ebb3b80a6547f1c6fe7bcbf9c8a.png)
3. You can view the recent parameter modification records here.

## Subsequent Operations
- You can use templates to manage database parameters in batches. For more information, see [Managing Parameter Template](https://intl.cloud.tencent.com/document/product/236/31906).
- For suggestions for configuration of key parameters, see [Suggestions on Parameter Settings](https://intl.cloud.tencent.com/document/product/236/38056).

