Generally, data is stored in many different data storage systems, and you need to extract data from these data sources, transform it, and load it into one or multiple objects. The SSIS feature of TencentDB for SQL Server supports flat files. If your SSIS project involves a flat file, you need to deploy it to a business intelligence server first before deploying the project.

>! If your SSIS project doesn't involve flat files, you can skip this step.

This document describes how to use the SSIS management feature to add and deploy a flat file for easier data use and management.

## Directions
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver).
2. In the instance list, find the target business intelligence server and click its ID or **Manage** in the **Operation** column to enter the instance management page.
![](https://qcloudimg.tencent-cloud.cn/raw/4c327375039c12c58c29e58619ef48d2.png)
3. On the instance management page, select **SSIS Management** > **Add File**.
![](https://qcloudimg.tencent-cloud.cn/raw/96ec8842a5c17e931d4b9881c499e4ad.png)
4. In the **Add File** window, paste the **COS File URL** and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/c98692fa08f4717bdf7c5ad2b7e9eafd.png)
>?
>- You can get the **COS File URL** for file upload and deploy the flat file to the business intelligence server only after uploading the flat file to COS.
>- You can use COS as instructed in [Downloading Objects](https://intl.cloud.tencent.com/document/product/436/13322). The **COS File URL** can be obtained during file download. Note that the access permission of the COS object must be set to **public read/private write**; otherwise, the flat file will fail to be deployed.
>- Only flat files in .txt, .csv, .xlsx, or .xls format are supported. The filename must start with a letter and can contain only digits, letters, underscores, and hyphens.
5. After adding the flat file successfully, you can query the file information in the list, including the file name, file size, file path, and status. You can also perform operations (**Delete** and **Copy MD5**) on the file.
 - File Name: Name of the flat file.
 - File Size: Size of the flat file. A flat file uses the disk space of the business intelligence server.
 - File Path: Path of the flat file , which is fixed at `D:\SSIS\flat file name` and is required during SSIS project deployment.
 - Status: Deployment status of the flat file, including **Deployment successful**, **Deploying**, and **Deployment failed**. If the status is **Deployment successful**, the flat file has been deployed to the business intelligence server successfully, and then you can deploy SSIS projects containing the file. If the status is **Deployment failed**, check whether the access permission of the COS object is set to **public read/private write**.
 - Operation (Delete): You can delete the flat file uploaded to the business intelligence server.
 - Operation (Copy MD5): You can verify whether the flat file uploaded to the business intelligence server has the same content as the local flat file. To do so, click **Copy MD5** to get the file's MD5 value and compare it with that of the local file.

