1. Log in to the [COS console](https://console.cloud.tencent.com/cos5/bucket) and go to the **Bucket list** page.
2. Click **Create a bucket**.
3. In the **Create a bucket** window that pops up, enter the following information and click **OK**.
 - Name: "test-scf".
 - Region: Select "Guangzhou (South China)".
 - Access permissions: Select "Private read and write".
4. Switch to the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1) and enter the **Functions** page.
5. Select **Guangzhou** region and click **Create** to enter the function creating page.
6. Enter the following parameter information and click **Next**. See the figure below:
![](https://main.qcloudimg.com/raw/2fa61bd4c599d0798b48e1faee5e2e9e.png)
 - Creation method: Select "Template function".
 - Function name: "DownloadImage".
 - Filter: Select "Python2.7" and choose " Get_COS_Object".
7. Keep the default configuration and click **Finish** to complete the function creation.
After the function is created, SCF will automatically populate the information such as function configuration and execution method based on the template function information.
8. On the details page of the created function, select the **Function code** tab.
9. Modify and save the code snippet as shown below.
![](https://main.qcloudimg.com/raw/b106350bff4feb54e41785458fea6f66.png)
Main parameters include:
 - Execution is set to "Get_COS_Object.main_handler", indicating that the SCF console will automatically save this snippet of code as a `Get_COS_Object.py` file, compress, and upload it to SCF for creating the function.
 - Modify the following parameters to your actual values:
    - appid: You can check it in [**Account information**](https://console.cloud.tencent.com/developer).
    - secret_id and secret_key: You can check them in [**TencentCloud API key**](https://console.cloud.tencent.com/cam/capi).
    - region: Set to the region of the COS bucket, i.e., "ap-guangzhou".
    >! The function and the COS bucket must be in the same region.
10. Select the **Triggers** tab and click **Add a trigger**.
11. On the **Add a trigger** page, enter the following information and click **Save**. See the figure below:
![](https://main.qcloudimg.com/raw/0a52a905922ee1c150c203d88df721d1.png)
 - Trigger type: Select "COS trigger".
 - COS bucket: Select the created "test-scf".
 - Event type: Select "All creation events".

