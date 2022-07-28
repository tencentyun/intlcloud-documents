
This document describes how to connect to a business intelligence server and deploy a project through a Windows CVM instance.

## Step 1. Create a Windows authentication account with the same account name and password as that on the business intelligence server in a CVM instance
You have created a Windows authentication account on the business intelligence server in [Creating Windows Authentication Account](https://intl.cloud.tencent.com/document/product/238/48058). Then, you need to create a Windows authentication account with the same account name and password as that on the business intelligence server in a CVM instance.

1. [Log in to the CVM instance](https://intl.cloud.tencent.com/document/product/213/10516) and click **Control Panel** in the **Start** menu of Windows Server.
<img src="https://qcloudimg.tencent-cloud.cn/raw/b3c39bf9b76ec355933b55c2cd20b93a.png"  style="zoom:60%;">
2. In the Control Panel, click **Change account type**.
![](https://qcloudimg.tencent-cloud.cn/raw/d47ad2ec0cb0d1121eaaacb2e377f620.png)
3. On the **Manage Accounts** page, click **Add a user account**.
![](https://qcloudimg.tencent-cloud.cn/raw/02b68ca909859d89c293794b9731795d.png)
4. In the **Add a user** pop-up window, enter a Windows authentication account with the same account name and password as that on the business intelligence server in the console, and click **Next**.
![](https://qcloudimg.tencent-cloud.cn/raw/e1c565c9bb8b4de605e419cc88e7a9b2.png)
5. Click **Finish**.
![](https://qcloudimg.tencent-cloud.cn/raw/5c14304020889f907419acb45489b27b.png)
6. Return to the **Manage Accounts** page, and you can see the account just created.
![](https://qcloudimg.tencent-cloud.cn/raw/c2b64ec9af7aa7e8c1e01af9d3ed837f.png)

## Step 2. Use the Windows authentication account created in step 1 to log in to the CVM instance
After creating a Windows authentication account with the same account name and password as that on the business intelligence server, use this account to log in to the CVM instance.
If you are logging in remotely, you need to perform the following operations to add the remote login permission to the account created in the previous step. Otherwise, you can skip this step and directly log in to the CVM instance with this account.
Add the remote login permission to the Windows authentication account created in the CVM instance in the following steps:

1. [Log in to the CVM instance](https://intl.cloud.tencent.com/document/product/213/10516) and click **Control Panel** in the **Start** menu of Windows Server.
2. In the search box in the Control Panel, enter **remote**, refresh the page, and click **Allow remote access to your computer**.
![](https://qcloudimg.tencent-cloud.cn/raw/66e1f5b569cd5cc02033f66cf66b6196.png)
3. On the **Remote** tab in the **System Properties** pop-up window, click **Select Users**.
![](https://qcloudimg.tencent-cloud.cn/raw/ed5d78cf4a7c3a76a6d4988bd3613a96.png)
4. In the **Remote Desktop Users** pop-up window, click **Add**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/0592279aff6ff2bbc948d32f52d77f2f.png"  style="zoom:60%;">
5. In the **Select Users** pop-up window, enter the Windows authentication account with the same account name and password as that on the business intelligence server created in the CVM instance in **Enter the object names to select** and click **OK**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/292544a05433bedad50ed21bac2f39bc.png"  style="zoom:60%;">
6. In the **Remote Desktop Users** window, you can see that the remote login permission is granted to the account. Click **OK**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/133fd71884c06198c4d29b24b797269c.png"  style="zoom:60%;">

## Step 3. Use the Windows authentication account to log in to the business intelligence server
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver#/) and view the private network address of the business intelligence server in the instance list.
2. Download and install [SSMS](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-ver16) in the CVM instance. For more information on SSMS, see [What is SQL Server Management Studio (SSMS)?](https://docs.microsoft.com/en/sql/ssms/sql-server-management-studio-ssms?view=sql-server-ver15).
3. Start SSMS in the Windows CVM instance.
In the **Connect to Server** window, enter the relevant information to connect to the business intelligence server, click **Connect**, and wait a few minutes while SSMS connects to your business intelligence server through Windows authentication.
 - Server type: Select **Database Engine**.
 - Server name: Enter the private IP and port number of the business intelligence server and separate them by a comma. For example, if the private IP of the instance is `10.10.10.10` and the port number is `1433`, then enter `10.10.10.10,1433` here.
 - Authentication: Select **Windows Authentication**.
 - User name and Password: You don't need to enter anything, as the information of the created Windows authentication account will be entered automatically. A prefix will be automatically added to the account name here, so that it can be the same as that displayed in the list on the **Account Management** tab of the instance.
 <img src="https://qcloudimg.tencent-cloud.cn/raw/8833851c148570adf8f043f1de9b7bdd.png"  style="zoom:60%;">
4. After logging in to SSMS, you can see the private IP of the business intelligence server in the **Object Explorer**, indicating that you have successfully logged in to the instance with the Windows authentication account.<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/ec24972d665668e8ccec0e52886e4baa.png"  style="zoom:60%;">

## Step 4. Deploy an SSIS project
1. View the SSISDB.
In the **Object Explorer** of SSMS, expand the **Integration Services Catalogs** directory to view the SSISDB.
![](https://qcloudimg.tencent-cloud.cn/raw/987bbb15c54d95a7011950a38e7ad68f.png)
2. Create a folder.
Right-click **SSISDB** and click **Create Folder**. In the pop-up window, enter the folder name and description and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/039f1431f9c6ed4d75db7e0c4c8c9be7.png)
3. Expand the folder created in the above step, and you can see the **Projects** and **Environments** directories.
![](https://qcloudimg.tencent-cloud.cn/raw/68d48a5c16a5f7217cd7e589f589d59d.png)
4. Deploy the project. Right-click **Projects** and click **Deploy Project**
![](https://qcloudimg.tencent-cloud.cn/raw/4336b8dea73696a6cc7b0fdc9bcf04c6.png)
5. On the **Introduction** page in the **Integration Services Deployment Wizard**, click **Next**.
![](https://qcloudimg.tencent-cloud.cn/raw/7707c8b679304b4c7e3a6123a032d44d.png)
6. Select an SSIS project deployment source.
On the **Select Source** page in the **Integration Services Deployment Wizard**, select **Project Deployment** > **Project deployment file**, click **Browse**, select the path of the prepared SSIS project file to be deployed, i.e., the .ispac file, and click **Next**.
>!SSIS projects only support the project deployment mode.
>
![](https://qcloudimg.tencent-cloud.cn/raw/552bceb4968b2a8bfc2426a271e21505.png)
7. During deployment, the **SQL Server Integration Services** warning window may pop up. If it does, click **OK** to ignore it.
![](https://qcloudimg.tencent-cloud.cn/raw/91139ab770815711e2419494e87788c2.png)
8. Select the deployment target.
On the **Select Deployment Target** page in the **Integration Services Deployment Wizard**, click **SSIS in SQL Server** and **Next**.
![](https://qcloudimg.tencent-cloud.cn/raw/e29483d6c4d9757b8ea13957fb86ecef.png)
9. Select the destination.
On the **Select Destination** page in the **Integration Services Deployment Wizard**, **Server name** is the business intelligence server's private IP and port, and **Authentication** is **Windows Authentication** by default. Leave the settings as-is and click **Connect**.
![](https://qcloudimg.tencent-cloud.cn/raw/a73416d1ba3f8a4afb8dce47ea2de90c.png)
10. After clicking **Connect**, you can see that the **Path** field is activated, and the .ispac SSIS project file is displayed after the path of the folder created previously. At this point, directly click **Next**.
![](https://qcloudimg.tencent-cloud.cn/raw/f1d2bee4b6078af6e87ccbc89cd1edbb.png)
11. Check the SSIS project deployment options. On the **Review** page in the **Integration Services Deployment Wizard**, check whether the source and destination information of the SSIS project to be deployed is correct. After confirming that everything is correct, click **Deploy** to deploy the project in the created folder.
![](https://qcloudimg.tencent-cloud.cn/raw/abbce933ec42673304cb1dd61f4f1c03.png)
12. On the **Results** page in the **Integration Services Deployment Wizard**, if all results are **Passed**, the SSIS service is deployed successfully.
![](https://qcloudimg.tencent-cloud.cn/raw/86897ac0399b4fce567ecc0b4228d83c.png)

## Step 5. Configure the SSIS service
1. After the SSIS project is deployed, configure relevant services.
After deployment, you can view the .ispac SSIS project file in the created **Projects** directory.
<img src="https://qcloudimg.tencent-cloud.cn/raw/6fc6a7645e7c4b8d34269308a69a8638.png"  style="zoom:50%;">
2. Right-click the deployed SSIS project file and click **Configure**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/c1a9d3b3710982cfdbefb613adae14d5.png"  style="zoom:70%;">![img](C:\Users\v_vwslwu\AppData\Local\Microsoft\Windows\INetCache\IE\V3955VCF\c1a9d3b3710982cfdbefb613adae14d5[1].png)
3. In the **Configure** pop-up window, switch to the **Connection Managers** tab.
![](https://qcloudimg.tencent-cloud.cn/raw/1bc4ea082a2f4fd9ab52ccaf71786245.png)
4. Configure the flat file connection.
 1. If the SSIS project file involves a flat file, click **Flat File Connection Manager** on the **Connection Managers** tab, find **ConnectionString** in **Properties** on the right, and click **...** after it.
>!This step configures the connection to the flat file. If the SSIS project file involves a flat file, perform this step; otherwise, skip it.
>
![](https://qcloudimg.tencent-cloud.cn/raw/c447a5e388eba28cca2786cca8c0d77d.png)
 2. In the **Set Parameter Value** pop-up window, click **Edit value** in the **Value** section.<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/7292576fb238d589ac1c494bc97f9345.png"  style="zoom:60%;">
 3. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver#/), click the ID of the business intelligence server in the instance list to enter its SSIS management page, and view and copy the **File Path** of the flat file.
![](https://qcloudimg.tencent-cloud.cn/raw/7c8efa6103162b9fdbb9154d2ddd6c5e.png)
 4. In the **Set Parameter Value** pop-up window, paste the copied flat file path in the input box after **Edit value** and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/b984bbb17baf6bd2abe73dc76215cdcd.png)
 5. Return to **Connection Managers**. You can see that the **ConnectionString** property of the **Flat File Connection Manager** has been changed to the path of the flat file uploaded on the business intelligence server's SSIS management page.
![](https://qcloudimg.tencent-cloud.cn/raw/b3266a07c28b6447968fc95424688907.png)
5. Configure the connection addresses of the source and target TencentDB for SQL Server instances in the SSIS project file.
On the **Connection Managers** tab, you can see the source and target instance connectors named **TencentDB for SQL Server instance's private IP,port.database name.account name**.
 1. Set the connection configuration of the source database first. Click the name of the source database connector, find **ServerName** in **Properties** on the right, and click **...** after it.
![](https://qcloudimg.tencent-cloud.cn/raw/8d2193d7bb5a3c321d23b47375163641.png)
 2. In the **Set Parameter Value** pop-up window, click **Edit value** in the **Value** section.
![](https://qcloudimg.tencent-cloud.cn/raw/5eb534af3dc446fdfd4c66b262fca806.png)
 3. Log in to the TencentDB for SQL Server console. On the **Interworking Group Management** page, find the source TencentDB for SQL Server database instance and copy its interworking IP and port number for business intelligence services.
![](https://qcloudimg.tencent-cloud.cn/raw/e370df16e888625b1b2b7275d2a10c68.png)
 4. In the **Set Parameter Value** pop-up window, paste the copied interworking IP and port number for business intelligence services of the source TencentDB for SQL Server instance in the input box after **Edit value**, separate the IP and port number by a comma, and click **OK**.
 For example, if the interworking IP for business intelligence services is `10.10.10.10` and the port number is `1024`, then enter `10.10.10.10,1024` here.
![](https://qcloudimg.tencent-cloud.cn/raw/9313b09c53665bb10801d14aa7985f8c.png)
 5. Return to **Connection Managers**. You can see that the connection address in the **ServerName** property of the **source TencentDB for SQL Server instance** has been changed to the interworking IP for business intelligence services of the source instance.
![](https://qcloudimg.tencent-cloud.cn/raw/65af1c9ceba4bfc0cdf50b42b9c35e15.png)
 6. On the **Connection Managers** tab, click the name of the source database connector, find the **Passsword** property of the **source TencentDB for SQL Server instance** in **Properties** on the right, and click **...** after it.
![](https://qcloudimg.tencent-cloud.cn/raw/13900b1bc3a4d47a408dc432c89404d3.png)
 7. In the **Set Parameter Value** pop-up window, select **Edit value** in the **Value** section, enter the password of the source database account in the input box after **Edit value**, and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/816fb5395e1d0dca91380cf7e760d81c.png)
 8. Return to **Connection Managers**, configure the connection information of the target database, including the **ConnectionString** and **Password** properties, and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/deafa568f32a0de86dbd82f3b081c52f.png)

## Step 6. Run the SSIS service
1. After configuring relevant services of the SSIS project file, in the created **Projects** directory, you can view the .dtsx SSIS package file in the **Packages** directory of the SSIS project file.
2. Right-click the .dtsx SSIS package file and click **Execute**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/e9021f1206fd0c77967814119c4495df.png"  style="zoom:60%;">
3. In the **Execute Package** pop-up window, check the configuration information on the **Connection Managers** tab and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/5717c7d08c67386504d4ebcdadfa85ce.png)
4. During execution, the **Microsoft SQL Server Management Studio** prompt window may pop up. If it does, click **Yes**.
![](https://qcloudimg.tencent-cloud.cn/raw/60421834e02728bffbf02f3056acff2b.png)
5. View the report. If all results are **Succeeded**, the execution succeeds.
![](https://qcloudimg.tencent-cloud.cn/raw/b2943c53a01045970c800d979d6c99f2.png)

## Step 7. Configure an agent job
1. In the **Object Explorer** of SSMS, expand **SQL Server Agent**, right-click **Jobs**, and click **New Job**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/cdb2c9cef71f58b8cc8e4e8575f9c88f.png"  style="zoom:70%;">
2. In the **New Job** pop-up window, click **...** after **Owner**. In the **Select Login** pop-up window, enter the **business intelligence server's Windows authentication account** in the input box below **Enter the object names to select**, and click **Check Names**.
![](https://qcloudimg.tencent-cloud.cn/raw/d2ae49da6df280da92ec66f023976b18.png)
3. As you cannot directly use the business intelligence server's default Windows authentication account, the **Multiple Objects Found** window will pop up. Select matched object and click **OK**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/c79c921124c1b104c25eddf859eb5f26.png"  style="zoom:60%;">
4. In the **Select Login** pop-up window, you can see that the real domain prefix is added before the account name in the input box below **Enter the object names to select**. Click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/37d57dc7b7d3fe941fe665f985f39872.png)
The displayed account name is the same as that displayed in the list on the **Account Management** tab of the business intelligence server.
![](https://qcloudimg.tencent-cloud.cn/raw/27e7fe4a54fc9adbf86f9bb4371293ec.png)
5. Create a job.
In the **New Job** pop-up window, click **Steps** below **Select a page**. On the **Steps** page, click **Create**, and the **New Job Step** window pops up.
![](https://qcloudimg.tencent-cloud.cn/raw/dbc7b828684b1ddcbad59b85e3ef1e85.png)
6. Create a job step.
In the **New Job Step** pop-up window, enter **Step name**, **Type**, **Run as**, **Server**, and **Package** as follows:
 - Step name: Enter a custom job step name.
 - Type: Select **SQL Server Integration Services Package** in the drop-down list.
 - Run as: Select the corresponding role of the account in the drop-down list.
 - Server: Enter the private IP and port number of the business intelligence server and separate them by a comma.
 - Package: Click **...** after the package. In the **Select an SSIS Package** pop-up window, select the SSIS package to be configured with the agent job and click **OK**.
 ![](https://qcloudimg.tencent-cloud.cn/raw/f7b03b15e0a79b4cb8d024fea82571c7.png)
 >!Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver#/). In the instance list, find the business intelligence server, and you can view its private network address in the **Private Network Address** column.
 >
![](https://qcloudimg.tencent-cloud.cn/raw/0ec0a2cde13744dcd40a7ae32c9c5e44.png)
7. After selecting the SSIS package to be configured with the agent job, return to the **New Job Step** pop-up window.
![](https://qcloudimg.tencent-cloud.cn/raw/b215cef6f3be682e1685077b9d80cc8d.png)
8. In the **New Job Step** pop-up window, set **Server** to the interworking IP and port number for business intelligence services, separate the IP and port number by a comma, and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/d372266a6f203a7d559b91ffca7a301c.png)
>!Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver#/). On the **Interworking Group Management** tab, find the business intelligence server, and you can view its interworking IP for business intelligence services.
>
![](https://qcloudimg.tencent-cloud.cn/raw/a30e5f2e6b811ee9d9aaddc7f70d3a09.png)
9. At this point, if you click **OK**, the program will stop responding temporarily, and the **SSIS Execution Properties** window will pop up to report a connection error. You can click **OK** to ignore this error.
![](https://qcloudimg.tencent-cloud.cn/raw/2c5650b41520cb14f0dbfd0ecf1adad7.png)
10. Set the scheduling cycle.
In the **New Job** pop-up window, click **Schedule** below **Select a page**. On the **Schedule** page, click **Create**, and the **New Job Schedule** window will pop up.
![](https://qcloudimg.tencent-cloud.cn/raw/8a27d251f2fc424f49a0ffe2528bc3b4.png)
11. In the **New Job Schedule** window, set the job scheduling cycle of the SSIS package, including **Name**, **Schedule type**, **Frequency**, **Daily frequency**, and **Duration**, based on your business requirements, and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/73e9b58f073abd7ed6a590f7c0302b8e.png)
12. Return to the **New Job** pop-up window. At this point, you have configured a job step and schedule. Click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/7ee44049c3f2a383d1fe901f1e5c1ab7.png)
13. In the **Object Explorer** of SSMS, expand **SQL Server Agent**, find **Jobs**, and you can see the job just created.
<img src="https://qcloudimg.tencent-cloud.cn/raw/7ebe83293d656102fd444465547ff501.png"  style="zoom:60%;">
14. Right-click the name of the job just created and click **View History**. In the **Log File Viewer** pop-up window, you can view the job execution history.
<img src="https://qcloudimg.tencent-cloud.cn/raw/d879b341ce28f37014d790f1f9d69178.png"  style="zoom:60%;">
15. View job execution logs in the **Log File Viewer**, and you can see that the job is running normally.
![](https://qcloudimg.tencent-cloud.cn/raw/178266df633eee89c58f80aa0819fc15.png)
16. In SSMS, log in to the target instance. You can see that the data is being extracted, transformed, and loaded into the target instance according to the settings in the SSIS project.<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/474714c996f8f5a54fbb8e71c33213d5.png"  style="zoom:60%;">

