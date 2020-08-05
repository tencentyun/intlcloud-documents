You can view and modify certain parameters in the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb) or through [API](https://intl.cloud.tencent.com/document/product/236/15860) and query parameter modification logs in the console.

## Modifying Parameter Value
>
>- If the modified parameter requires instance restart for it to take effect, the system will ask you whether to restart. You are recommended to do so during off-peak hours and ensure that your application has a reconnection mechanism.
>- Before the parameter modification is submitted, you can click <img src="https://main.qcloudimg.com/raw/81fc2494e8b61ff36a63d23cccb61cd1.png"  style="margin:0;"> next to the parameter or **Cancel** on the modification page to cancel the modification.

### Modifying parameters in batches
1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb). In the instance list, click an instance name or **Manage** in the "Operation" column to enter the instance management page.
2. Select **Database Management** > **Parameter Settings** and click **Batch modify parameters**.
![](https://main.qcloudimg.com/raw/3ec389dafa09276ae66b00a71445d9d3.png)
3. In the "Current Value" column, select the parameters to be modified. After confirming that everything is correct, click **Confirm Modification**.
![](https://main.qcloudimg.com/raw/5307fbeef4b1fccef478ab7fd57b3167.png)
4. In the pop-up dialog box, indicate your consent and click **OK**.

### Modifying a single parameter
1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb). In the instance list, click an instance name or **Manage** in the "Operation" column to enter the instance management page.
2. Select **Database Management** > **Parameter Settings**, select the row of the target parameter, and click <img src="https://main.qcloudimg.com/raw/788902e3f8c335cf17de420f7181c2a8.png"  style="margin:0;"> in the "Current Value" column to modify the parameter value.
![](https://main.qcloudimg.com/raw/4687ed705274b76ec92c43b7f9d448ab.png)
3. Enter the target parameter value as prompted in the "Acceptable Values" column and click <img src="https://main.qcloudimg.com/raw/1f4c7f2e0744bc601efb5d9fb04a7a04.png"  style="margin:0;"> to save the change. You can click <img src="https://main.qcloudimg.com/raw/2106cb4b9337a1a2fff5908581d2a908.png"  style="margin:0;"> to cancel the operation.
![](https://main.qcloudimg.com/raw/41c7d73d4c5d404a112f54c3a63da726.png)
4. In the pop-up dialog box, select an "Execution Mode" and click **OK**.

### Importing from parameter template
1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb). In the instance list, click an instance name or **Manage** in the "Operation" column to enter the instance management page.
2. Select **Database Management** > **Parameter Settings** and click **Import from Templates**.
![](https://main.qcloudimg.com/raw/bd7a2fd3dc89895f1a3bd779d0fe8bbc.png)
3. In the pop-up dialog box, select the parameter template and click **Import and Overwrite Original Parameters**.
![](https://main.qcloudimg.com/raw/2f649840f16befabea6259f9b4c7f47c.png)

### Importing parameters
1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb). In the instance list, click an instance name or **Manage** in the "Operation" column to enter the instance management page.
2. Select **Database Management** > **Parameter Settings** and click **Import Parameters**.
![](https://main.qcloudimg.com/raw/52d6f069bbce29c933254593d59c0236.png)
3. In the pop-up dialog box, select the file for upload, and click **Import and Overwrite Original Parameters**.
![](https://main.qcloudimg.com/raw/42fb6ef8936131a3bc776e492478e745.png)
	
## Viewing Parameter Modification Record
1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb). In the instance list, click an instance name or **Manage** in the "Operation" column to enter the instance management page.
2. Select **Database Management** > **Parameter Settings** and click **Recent modifications**.
![](https://main.qcloudimg.com/raw/6d6318fce61fc78c6ff3611479ae5714.png)
3. On the record of recent modifications page, you can view the recent parameter modification records.
![](https://main.qcloudimg.com/raw/4c616b40d058f114e8f75c4021c02648.png)

