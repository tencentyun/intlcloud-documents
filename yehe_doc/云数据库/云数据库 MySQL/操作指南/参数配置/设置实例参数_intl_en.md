You can view and modify certain parameters and query parameter modification logs in [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb).

## Notes
- To ensure instance stability, only some parameters can be modified in the console. These parameters are displayed in the **Parameter Settings** page.
- If the modified parameter requires instance restart to take effect, the system will ask you if you wish to restart. We recommend that you do so during off-peak hours and ensure that your application has a reconnection mechanism.

## Modifying Parameters in the Parameter List

<span id = "plxgcs"></span>
### Modifying parameters in batches
1. Log in to the [MySQL Console](https://console.cloud.tencent.com/cdb). In the instance list, click the instance ID/name or **Manage** in the "Operation" column to access the instance management page.
2. Select **Database Management** > **Parameter Settings** and click **Batch modify parameters**.
![](https://main.qcloudimg.com/raw/82c535bd50543645831988ca2e9b688e.png)
3. Locate the desired parameters, and modify their values in the "Current Value" column. After confirming that everything is correct, click **Confirm Modification**.
![](https://main.qcloudimg.com/raw/5307fbeef4b1fccef478ab7fd57b3167.png)
4. In the pop-up dialog box, select the "Execution Mode" and click **OK**.
>?
>- If you select **Immediate execution**, the parameter modification task will be executed and take effect immediately.
>- If you select **During maintenance window**, the parameter modification task will be executed and take effect during the [instance maintenance period](https://intl.cloud.tencent.com/document/product/236/10929).
>

<span id = "xgdgcs"></span>
### Modifying a single parameter
1. Log in to the [MySQL Console](https://console.cloud.tencent.com/cdb). In the instance list, click the instance ID/name or **Manage** in the "Operation" column to access the instance management page.
2. Select **Database Management** > **Parameter Settings**. In the parameter list, locate the desired parameter and click <img src="https://main.qcloudimg.com/raw/788902e3f8c335cf17de420f7181c2a8.png"  style="margin:0;"> in the "Current Value" column.
![](https://main.qcloudimg.com/raw/4687ed705274b76ec92c43b7f9d448ab.png)
3. Modify the value within the restrictions stated in the "Acceptable Values" column and click <img src="https://main.qcloudimg.com/raw/1f4c7f2e0744bc601efb5d9fb04a7a04.png"  style="margin:0;"> to save the modification. You can click <img src="https://main.qcloudimg.com/raw/2106cb4b9337a1a2fff5908581d2a908.png"  style="margin:0;"> to cancel the operation.
![](https://main.qcloudimg.com/raw/41c7d73d4c5d404a112f54c3a63da726.png)
4. In the pop-up dialog box, select the "Execution Mode" and click **OK**.
>?
>- If you select **Immediate execution**, the parameter modification task will be executed and take effect immediately.
>- If you select **During maintenance window**, the parameter modification task will be executed and take effect during the [instance maintenance period](https://intl.cloud.tencent.com/document/product/236/10929).
>


## Modifying Parameters by Importing a Parameter Template
### Method 1. Importing a parameter template on the "Parameter Settings" page
1. Log in to the [MySQL Console](https://console.cloud.tencent.com/cdb). In the instance list, click the instance ID/name or **Manage** in the "Operation" column to access the instance management page.
2. Select **Database Management** > **Parameter Settings** and click **Import from Templates**.
![](https://main.qcloudimg.com/raw/bd7a2fd3dc89895f1a3bd779d0fe8bbc.png)
3. In the pop-up dialog box, select a parameter template and click **Import and Overwrite Original Parameters**.
![](https://main.qcloudimg.com/raw/2f649840f16befabea6259f9b4c7f47c.png)
4. After confirming that everything is correct, click **Confirm Modification**.
![](https://main.qcloudimg.com/raw/1673166256bc4d122f5a72c3c703ffab.png)
5. In the pop-up dialog box, select the "Execution Mode" and click **OK**.
>?
>- If you select **Immediate execution**, the parameter modification task will be executed and take effect immediately.
>- If you select **During maintenance window**, the parameter modification task will be executed and take effect during the [instance maintenance period](https://intl.cloud.tencent.com/document/product/236/10929).
>


### Method 2. Importing a parameter template on the "Parameter Templates" page
For more information, please see [Managing Parameter Template > Applying a Parameter Template to a Database](https://intl.cloud.tencent.com/document/product/236/31906#.E5.BA.94.E7.94.A8.E5.8F.82.E6.95.B0.E6.A8.A1.E6.9D.BF.E4.BA.8E.E5.AE.9E.E4.BE.8B).

## Modifying Parameters by Importing a Parameter Configuration File
1. Log in to the [MySQL Console](https://console.cloud.tencent.com/cdb). In the instance list, click the instance ID/name or **Manage** in the "Operation" column to access the instance management page.
2. Select **Database Management** > **Parameter Settings** and click **Import Parameters**.
![](https://main.qcloudimg.com/raw/52d6f069bbce29c933254593d59c0236.png)
3. In the pop-up dialog box, select a file to upload and click **Import and Overwrite Original Parameters**.
![](https://main.qcloudimg.com/raw/42fb6ef8936131a3bc776e492478e745.png)
4. After confirming that everything is correct, click **Confirm Modification**.
![](https://main.qcloudimg.com/raw/1673166256bc4d122f5a72c3c703ffab.png)
5. In the pop-up dialog box, select the "Execution Mode" and click **OK**.
>?
>- If you select **Immediate execution**, the parameter modification task will be executed and take effect immediately.
>- If you select **During maintenance window**, the parameter modification task will be executed and take effect during the [instance maintenance period](https://intl.cloud.tencent.com/document/product/236/10929).
>


## Exporting Parameter Configuration as a File
1. Log in to the [MySQL Console](https://console.cloud.tencent.com/cdb). In the instance list, click the instance ID/name or **Manage** in the "Operation" column to access the instance management page.
2. Select **Database Management** > **Parameter Settings** and click **Export Parameters**.
![](https://main.qcloudimg.com/raw/6885ffbc45f3154ed203551a309e1848.png)

## Exporting Parameter Configuration as a Template
1. Log in to the [MySQL Console](https://console.cloud.tencent.com/cdb). In the instance list, click the instance ID/name or **Manage** in the "Operation" column to access the instance management page.
2. Select **Database Management** > **Parameter Settings** and click **Save as Template**.
![](https://main.qcloudimg.com/raw/fca4ec16b316948af812db9988d0c92c.png)

## Modifying Parameters during a Custom Time Window
Before you confirm the parameter modification, the "Modify Parameters" dialog box will pop up for you to select a custom time window for the modification to take effect.
>?If you select **During maintenance window** as the effective time, the parameter modification task will be executed and take effect during the [instance maintenance period](https://intl.cloud.tencent.com/document/product/236/10929).
>
![](https://main.qcloudimg.com/raw/00d4892fb614dd285cdec91a4a74cf2d.png)


## Canceling a Parameter Modification Task
If a parameter modification or batch modification task has been submitted but you want to cancel it, you can select **[Task List](https://console.cloud.tencent.com/mysql/task)** in the left sidebar in the console, locate the task, and click **Cancel** in the "Operation" column. You can cancel a task only before it is executed. The task state should be "Waiting for execution".



## Viewing Parameter Modification Logs
1. Log in to the [MySQL Console](https://console.cloud.tencent.com/cdb). In the instance list, click the instance ID/name or **Manage** in the "Operation" column to access the instance management page.
2. Select **Database Management** > **Parameter Settings** and click **Recent modifications**.
![](https://main.qcloudimg.com/raw/93494ebb3b80a6547f1c6fe7bcbf9c8a.png)
3. You can view the recent parameter modification records here.

## Subsequent Operations
- You can use templates to manage database parameters in batches. For more information, please see [Managing Parameter Template](https://intl.cloud.tencent.com/document/product/236/31906).
- For suggestions for configuration of key parameters, please see [Suggestions on Parameter Settings](https://intl.cloud.tencent.com/document/product/236/38056).
