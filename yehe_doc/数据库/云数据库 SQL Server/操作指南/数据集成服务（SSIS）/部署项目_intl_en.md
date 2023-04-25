
This document describes how to connect to a business intelligence server and deploy a project through a Windows CVM instance.

## Step 1. Create a Windows authentication account with the same account name and password as that on the business intelligence server in a CVM instance
You have created a Windows authentication account on the business intelligence server. Then, you need to create a Windows authentication account with the same account name and password as that on the business intelligence server in a CVM instance. For more information, see [Creating Windows Authentication Account](https://www.tencentcloud.com/document/product/238/48058).

1. [Log in to the CVM instance](https://www.tencentcloud.com/document/product/213/10516) and click **Control Panel** in the **Start** menu of Windows Server.
2. In the Control Panel, click **Change account type**.
3. On the **Manage Accounts** page, click **Add a user account**.
4. In the **Add a user** pop-up window, enter a Windows authentication account with the same account name and password as that on the business intelligence server in the console, and click **Next**.
5. Click **Finish**.
6. Return to the **Manage Accounts** page, and you can see the account just created.

## Step 2. Use the Windows authentication account created in step 1 to log in to the CVM instance
After creating a Windows authentication account with the same account name and password as that on the business intelligence server, use this account to log in to the CVM instance.
If you are logging in remotely, you need to perform the following operations to add the remote login permission to the account created in the previous step. Otherwise, you can skip this step and directly log in to the CVM instance with this account.
Add the remote login permission to the Windows authentication account created in the CVM instance in the following steps:
1. [Log in to the CVM instance](https://www.tencentcloud.com/document/product/213/10516) and click **Control Panel** in the **Start** menu of Windows Server.
2. In the search box in the Control Panel, enter **remote**, refresh the page, and click **Allow remote access to your computer**.
3. On the **Remote** tab in the **System Properties** pop-up window, click **Select Users**.
4. In the **Remote Desktop Users** pop-up window, click **Add**.
5. In the **Select Users** pop-up window, enter the Windows authentication account with the same account name and password as that on the business intelligence server created in the CVM instance in **Enter the object names to select** and click **OK**.
6. In the **Remote Desktop Users** window, you can see that the remote login permission is granted to the account. Click **OK**.

## Step 3. Use the Windows authentication account to log in to the business intelligence server
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver#/) and view the private network address of the business intelligence server in the instance list.
2. Download and install [SSMS](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-ver16) in the CVM instance. For more information on SSMS, see [What is SQL Server Management Studio (SSMS)?](https://docs.microsoft.com/en/sql/ssms/sql-server-management-studio-ssms?view=sql-server-ver15).
3. Start SSMS in the Windows CVM instance.
In the **Connect to Server** window, enter the relevant information to connect to the business intelligence server, click **Connect**, and wait a few minutes while SSMS connects to your business intelligence server through Windows authentication.
 - Server type: Select **Database Engine**.
 - Server name: Enter the private IP and port number of the business intelligence server and separate them by a comma. For example, if the private IP of the instance is `10.10.10.10` and the port number is `1433`, then enter `10.10.10.10,1433` here.
 - Authentication: Select **Windows Authentication**.
 - User name and password: You don't need to enter anything, as the information of the created Windows authentication account will be entered automatically. A prefix will be automatically added to the account name here, so that it can be the same as that displayed in the list on the **Account Management** tab of the instance.
4. After logging in to SSMS, you can see the private IP of the business intelligence server in the **Object Explorer**, indicating that you have successfully logged in to the instance with the Windows authentication account.<br>

## Step 4. Deploy an SSIS project
1. View the SSISDB.
In the **Object Explorer** of SSMS, expand the **Integration Services Catalogs** directory to view the SSISDB.
2. Create a folder.
Right-click **SSISDB** and click **Create Folder**. In the pop-up window, enter the folder name and description and click **OK**.
3. Expand the folder created in the above step, and you can see the **Projects** and **Environments** directories.
4. Deploy the project. Right-click **Projects** and click **Deploy Project**
5. On the **Introduction** page in the **Integration Services Deployment Wizard**, click **Next**.
6. Select an SSIS project deployment source.
On the **Select Source** page in the **Integration Services Deployment Wizard**, select **Project Deployment** > **Project deployment file**, click **Browse**, select the path of the prepared SSIS project file to be deployed, i.e., the .ispac file, and click **Next**.
>!SSIS projects only support the project deployment mode.
>
7. During deployment, the **SQL Server Integration Services** warning window may pop up. If it does, click **OK** to ignore it.
8. Select the deployment target.
On the **Select Deployment Target** page in the **Integration Services Deployment Wizard**, click **SSIS in SQL Server** and **Next**.
9. Select the destination.
On the **Select Destination** page in the **Integration Services Deployment Wizard**, **Server name** is the business intelligence server's private IP and port, and **Authentication** is **Windows Authentication** by default. Leave the settings as-is and click **Connect**.
10. After clicking **Connect**, you can see that the **Path** field is activated, and the .ispac SSIS project file is displayed after the path of the folder created previously. At this point, directly click **Next**.
11. Check the SSIS project deployment options. On the **Review** page in the **Integration Services Deployment Wizard**, check whether the source and destination information of the SSIS project to be deployed is correct. After confirming that everything is correct, click **Deploy** to deploy the project in the created folder.
12. On the **Results** page in the **Integration Services Deployment Wizard**, if all results are **Passed**, the SSIS service is deployed successfully.

## Step 5. Configure the SSIS service
1. After the SSIS project is deployed, configure relevant services.
After deployment, you can view the .ispac SSIS project file in the created **Projects** directory.
2. Right-click the deployed SSIS project file and click **Configure**.
3. In the **Configure** pop-up window, switch to the **Connection Managers** tab.
4. Configure the flat file connection.
 1. If the SSIS project file involves a flat file, click **Flat File Connection Manager** on the **Connection Managers** tab, find **ConnectionString** in **Properties** on the right, and click **...** after it.
>!This step configures the connection to the flat file. If the SSIS project file involves a flat file, perform this step; otherwise, skip it.
>
  2. In the **Set Parameter Value** pop-up window, click **Edit value** in the **Value** section.<br>
  3. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver#/), click the ID of the business intelligence server in the instance list to enter its SSIS management page, and view and copy the **File Path** of the flat file.
  4. In the **Set Parameter Value** pop-up window, paste the copied flat file path in the input box after **Edit value** and click **OK**.
  5. Return to **Connection Managers**. You can see that the **ConnectionString** property of the **Flat File Connection Manager** has been changed to the path of the flat file uploaded on the business intelligence server's SSIS management page.
5. Configure the connection addresses of the source and target TencentDB for SQL Server instances in the SSIS project file.
On the **Connection Managers** tab, you can see the source and target instance connectors named **TencentDB for SQL Server instance's private IP,port.database name.account name**.
  7. Set the connection configuration of the source database first. Click the name of the source database connector, find **ServerName** in **Properties** on the right, and click **...** after it.
  8. In the **Set Parameter Value** pop-up window, click **Edit value** in the **Value** section.
  9. Log in to the TencentDB for SQL Server console. On the **Interworking Group Management** page, find the source TencentDB for SQL Server database instance and copy its interworking IP and port number for business intelligence services.
 4. In the **Set Parameter Value** pop-up window, paste the copied interworking IP and port number for business intelligence services of the source TencentDB for SQL Server instance in the input box after **Edit value**, separate the IP and port number by a comma, and click **OK**.
 For example, if the interworking IP for business intelligence services is `10.10.10.10` and the port number is `1024`, then enter `10.10.10.10,1024` here.
  11. Return to **Connection Managers**. You can see that the connection address in the **ServerName** property of the **source TencentDB for SQL Server instance** has been changed to the interworking IP for business intelligence services of the source instance.
  12. On the **Connection Managers** tab, click the name of the source database connector, find the **Passsword** property of the **source TencentDB for SQL Server instance** in **Properties** on the right, and click **...** after it.
  13. In the **Set Parameter Value** pop-up window, select **Edit value** in the **Value** section, enter the password of the source database account in the input box after **Edit value**, and click **OK**.
  14. Return to **Connection Managers**, configure the connection information of the target database, including the **ConnectionString** and **Password** properties, and click **OK**.

## Step 6. Run the SSIS service
1. After configuring relevant services of the SSIS project file, in the created **Projects** directory, you can view the .dtsx SSIS package file in the **Packages** directory of the SSIS project file.
2. Right-click the .dtsx SSIS package file and click **Execute**.
3. In the **Execute Package** pop-up window, check the configuration information on the **Connection Managers** tab and click **OK**.
4. During execution, the **Microsoft SQL Server Management Studio** prompt window may pop up. If it does, click **Yes**.
5. View the report. If all results are **Succeeded**, the execution succeeds.

## Step 7. Configure an agent job
1. In the **Object Explorer** of SSMS, expand **SQL Server Agent**, right-click **Jobs**, and click **New Job**.
2. In the **New Job** pop-up window, click **...** after **Owner**. In the **Select Login** pop-up window, enter the **business intelligence server's Windows authentication account** in the input box below **Enter the object names to select**, and click **Check Names**.
3. As you cannot directly use the business intelligence server's default Windows authentication account, the **Multiple Objects Found** window will pop up. Select matched object and click **OK**.
4. In the **Select Login** pop-up window, you can see that the real domain prefix is added before the account name in the input box below **Enter the object names to select**. Click **OK**.
The displayed account name is the same as that displayed in the list on the **Account Management** tab of the business intelligence server.
5. Create a job.
In the **New Job** pop-up window, click **Steps** below **Select a page**. On the **Steps** page, click **Create**, and the **New Job Step** window pops up.
6. Create a job step.
In the **New Job Step** pop-up window, enter **Step name**, **Type**, **Run as**, **Server**, and **Package** as follows:
 - Step name: Enter a custom job step name.
 - Type: Select **SQL Server Integration Services Package** in the drop-down list.
 - Run as: Select the corresponding role of the account in the drop-down list.
 - Server: Enter the private IP and port number of the business intelligence server and separate them by a comma.
 - Package: Click **...** after the package. In the **Select an SSIS Package** pop-up window, select the SSIS package to be configured with the agent job and click **OK**.
 >!Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver#/). In the instance list, find the business intelligence server, and you can view its private network address in the **Private Network Address** column.
 >
7. After selecting the SSIS package to be configured with the agent job, return to the **New Job Step** pop-up window.
8. In the **New Job Step** pop-up window, set **Server** to the interworking IP and port number for business intelligence services, separate the IP and port number by comma, and click **OK**.
>!Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver#/). On the **Interworking Group Management** tab, find the business intelligence server, and you can view its interworking IP for business intelligence services.
>
9. At this point, if you click **OK**, the program will stop responding temporarily, and the **SSIS Execution Properties** window will pop up to report a connection error. You can click **OK** to ignore this error.
10. Set the scheduling cycle.
In the **New Job** pop-up window, click **Schedule** below **Select a page**. On the **Schedule** page, click **Create**, and the **New Job Schedule** window will pop up.
11. In the **New Job Schedule** window, set the job scheduling cycle of the SSIS package, including **Name**, **Schedule type**, **Frequency**, **Daily frequency**, and **Duration**, based on your business requirements, and click **OK**.
12. Return to the **New Job** pop-up window. At this point, you have configured a job step and schedule. Click **OK**.
13. In the **Object Explorer** of SSMS, expand **SQL Server Agent**, find **Jobs**, and you can see the job just created.
14. Right-click the name of the job just created and click **View History**. In the **Log File Viewer** pop-up window, you can view the job execution history.
15. View job execution logs in the **Log File Viewer**, and you can see that the job is running normally.
16. In SSMS, log in to the target instance. You can see that the data is being extracted, transformed, and loaded into the target instance according to the settings in the SSIS project.<br>
