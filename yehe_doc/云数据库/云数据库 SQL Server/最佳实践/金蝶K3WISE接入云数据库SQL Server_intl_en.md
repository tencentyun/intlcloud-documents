This document describes how to connect Kingdee K/3 WISE 15.0/15.1 to TencentDB for SQL Server so as to execute distributed transactions between the TencentDB for SQL Server and Windows CVM instances.

This solution consists of the following three steps:
1. Migrate data to TencentDB for SQL Server, i.e., restoring the full data backup of the account set database in a local Kingdee K/3 WISE instance to TencentDB for SQL Server.
2. Enable distributed transaction execution, i.e., adjusting the access settings of the TencentDB for SQL Server and Windows CVM instances to ensure that the relevant ports are open for distributed transaction execution.
3. Replace the account set management tool to make it compatible with TencentDB for SQL Server.

>?
>- To support distributed transactions, additional resources are required for configuration; therefore, you can configure High-Availability Edition instances only in specification higher than "1-core 8 GB MEM". Please upgrade the instances that do not meet the minimum requirement before connection.
>- Adjust the TencentDB for SQL Server access settings to ensure that distributed transaction can be executed. You can [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance. To improve the ticket processing efficiency, make sure that you have already read this document and completed data migration to TencentDB for SQL Server before submitting the ticket.


## Step 1. Migrate data to TencentDB for SQL Server
Prerequisites: you have backed up the full data of the account set database files in your local Kingdee K/3 WISE instance.

1. [Log in to the Windows CVM instance](https://intl.cloud.tencent.com/document/product/213/10516#.E6.AD.A5.E9.AA.A43.EF.BC.9A.E7.99.BB.E5.BD.95.E4.BA.91.E6.9C.8D.E5.8A.A1.E5.99.A8) and install Kingdee K/3 WISE.
>?The CVM instance where Kingdee is installed and the TencentDB for SQL Server instance must be in the same VPC in the same region.
2. [Create a TencentDB for SQL Server instance](https://intl.cloud.tencent.com/document/product/238/31571).
3. Upload the full backup file and restore the data. For detailed directions, please see [Uploading Backup File to COS](https://intl.cloud.tencent.com/document/product/238/32558) and [Migrating Data Through Source File in COS](https://intl.cloud.tencent.com/document/product/238/32558).
4. Create a TencentDB for SQL Server account and authorize it. For more information, please see [Creating Account](https://intl.cloud.tencent.com/document/product/238/7521).

## Step 2. Enable distributed transaction execution
### Setting TencentDB for SQL Server
Adjust the TencentDB for SQL Server access settings to ensure that distributed transactions can be executed. You can [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

### Setting CVM instance
#### Setting security group
1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/instance), select the region where the instance resides, and click the instance ID to enter the management page.
2. Select the **Security Group** tab and modify the rules as follows:
 - "Source" IP information, which can be obtained by [submitting a ticket](https://console.cloud.tencent.com/workorder/category).
 - "Protocol ports" of inbound and outbound rules. You need to open the ports 1433, 135, and 1024–65535.


#### Setting Windows OS
1. [Log in to the Windows CVM instance](https://intl.cloud.tencent.com/document/product/213/10516#.E6.AD.A5.E9.AA.A43.EF.BC.9A.E7.99.BB.E5.BD.95.E4.BA.91.E6.9C.8D.E5.8A.A1.E5.99.A8).
2. Open the `hosts` file located at `C:\Windows\System32\drivers\etc\hosts`.
3. Add the VIP and host information (which can be obtained by [submitting a ticket](https://console.cloud.tencent.com/workorder/category)) provided by TencentDB for SQL Server to the end of the `hosts` file and save the change.

4. Open "Component Services" in "Control Panel" > "System and Security" > "Administrative Tools".
5. Select "Component Services" > "Computers" > "My Computer" > "Distributed Transaction Coordinator".
6. Right-click the local DTC on the right and select "Properties".

7. Select the "Security" tab, set as follows, and click **OK**.

8. In the pop-up MSDTC service dialog box, click **Yes** and wait for the MSDTC service to restart.
 

## Step 3. Initialize account set management
1. Download the account set management tool: Kingdee K/3 WISE 15.1 or 15.0.
>?The required account set management tool varies by Kingdee K/3 WISE version.
2. Decompress the package and replace the files in the Kingdee installation directory `K3ERP\KDSYSTEM\KDCOM` with the extracted files.
3. Open Kingdee K/3 WISE.
4. On the pop-up account set management database settings page, set relevant identity verification information and data server.
>?Enter the private network address of the TencentDB for SQL Server instance as the data server, which can be viewed in the [console](https://console.cloud.tencent.com/sqlserver).
>

5. In the "System" drop-down list, click **Preset Connection** and set the preset connection for easier use.

6. In the database drop-down list, click **Register Account Set**.

7. Select the corresponding database and click **All**.

 
## Step 4. Log in to and use Kingdee K/3 WISE
After you complete all the settings above, distributed transactions can be supported between the CVM and TencentDB for SQL Server instances, and you can log in to and use Kingdee K/3 WISE normally.

If the following error message is displayed during login:
`Failed to create the transaction at the intermediate layer. Please contact the system administrator. Advanced display: error code: 5(5H)`
Please troubleshoot the error as instructed in [Kingdee's official documentation](https://club.kingdee.com/club/newclub/helpDetail?product_id=3&id=366259). 


