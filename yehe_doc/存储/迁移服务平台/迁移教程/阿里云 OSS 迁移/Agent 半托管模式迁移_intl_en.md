

## Overview
In Agent semi-managed migration mode, you need to manually deploy the Agent on the service of the cloud vendor that hosts your source data, so that the Agent can pull the source data through the private network and push it to Tencent Cloud COS.
Traffic is not billed during Agent semi-managed migration if a direct connection is established between the source-data cloud vendor and Tencent Cloud COS. Therefore, we recommend you perform Agent semi-managed migration if Direct Connect is available.

The following describes how to configure an Agent semi-managed migration task to migrate data from Alibaba Cloud OSS to Tencent Cloud COS.


## Preparations
#### Alibaba Cloud OSS
1. Prepare a direct connection (if there is no Direct Connect environment, and the migration is made over the public network, then you can ignore this step):
If you want to perform Agent semi-managed migration through Direct Connect, before migration, confirm with your sales rep that the COS SDK used by the server in Alibaba Cloud can access COS through Direct Connect.
2. Create a RAM sub-account and grant the required permissions:
	1. Log in to the RAM console.
	2. Select **People Management** > **Users** > **Create User**.
	3. Select console password login and programming access, and then enter the user account information.
	4. Save the generated account, password, `AccessKeyID`, and `AccessKeySecret`.
	5. Select the user login name and click **Add Permissions** to grant the sub-account read and write permissions (AliyunOSSFullAccess).

#### Tencent Cloud COS
1. Create a bucket to store the migrated data. For more information, please see [Creating Buckets](https://intl.cloud.tencent.com/document/product/436/13309).
2. Create a sub-user for migration and grant the required permissions:
	1. 	Log in to the [CAM console](https://console.cloud.tencent.com/cam/overview).
	2. 	On the left sidebar, select **Users** > **User List** to enter the user list page.
	3. 	Create a sub-user and select **Programming access** and **Tencent Cloud console access**.
	4. 	Search for and select the `QcloudCOSAccessForMSPRole` and `QcloudCOSFullAccess` policies.
	5. 	Finish creating the sub-user and save the sub-username, login password, `SecretId`, and `SecretKey`.
- Click [here](https://migrate-1256125716.cos.ap-guangzhou.myqcloud.com/agent/agent.zip) to download the Agent.

>?You can use Migration Service Platform (MSP) with your root account. However, for security reasons, we recommend you create a sub-account, use the sub-account's API key for migration, and delete the sub-user after migration.

## Migration Speed Limit
MSP provides a QPS limit for object storage mode and a bandwidth limit for URL list mode. During Agent-based migration, you can set a speed limit on the migration server and select **No Speed Limit** when creating a task on MSP.
1. 	Run the following command to view the serial number of the ENI.
```
[root@VM_10_12_centos ~]# ifconfig
```
2. Run the following command to test the download speed before applying speed limit.
```
[root@VM_10_12_centos ~]# wget https://msp-test-src-1200000000.cos.ap-guangzhou.myqcloud.com/bkce_src-5.0.2.tar.gz
```
3. 	Run the following command to install the iproute tool. It is installed on CentOS 7.x by default. If this is the case, you can skip this step.
```
[root@VM_10_12_centos ~]# yum -y install iproute
```
4. Run the following command to limit the speed of eth0 to 50 Kbit/s.
```
[root@VM_10_12_centos ~]# /sbin/tc qdisc add dev eth0 root tbf rate 50kbit latency 50ms burst 1000
```
>?
>- eth0 is the serial number of the ENI, which is obtained in Step 1.
>- If you need to limit the speed to 10 Mbit/s, change `50kbit` to `10Mbit`.
5. 	Run the following command to check whether the download speed is limited.
```
[root@VM_10_12_centos ~]# wget https://msp-test-src-1200000000.cos.ap-guangzhou.myqcloud.com/bkce_src-5.0.2.tar.gz
```
6. 	Run the following command to remove the speed limit when needed.
```
[root@VM_10_12_centos ~]# /sbin/tc qdisc del dev eth0 root tbf
```

## Migration Implementation
1. 	Create a temporary server (master server) for migration.
You need to enter the IP address of the Agent master server when creating a migration task. This IP address is a private IP address for communicating with the worker server in the migration cluster. Therefore, prepare a virtual machine with the CentOS 7.x 64-bit operating system before creating the migration task.
>?
>- If you migrate over Direct Connect, we recommend you configure the server on the migration source side.
>- If you migrate over the public network, we recommend you use Tencent Cloud [CVM](https://intl.cloud.tencent.com/zh/document/product/213) as the server.
2. 	Create a migration task on Tencent Cloud MSP.
i. 	In the **Mode Selection** section under **Select migration mode**, select **Create a migration task and download the Agent manually to start migration**.
ii. In the **Master Node Private IP** section, enter the private IP address of the server created on Alibaba Cloud, such as `172.XXX.XXX.94`.
iii. 	In the **OSS Private Network EndPoint** section, enter the **EndPoint** (region node) of the OSS bucket.
![](https://main.qcloudimg.com/raw/aacc6697dd8a170f0fb946a6be42bb2f.png)
>!
>- If the files with the same name exist in both the migration source and destination, we recommend you select **Skip (keep the file with the same name in the destination bucket)** for **File with the same name**. By default, **Overwrite (the file in the source bucket replaces the file with the same name in the destination bucket)** is selected.
>- Perform secondary migration if the object (file) content is changed during migration.
3. 	Click **Create and Start** after setting all the parameters. In Agent mode, the task does not automatically run after creation. Instead, you need to manually start the Agent on the Alibaba Cloud master server as follows:
4. 	Deploy and start the Agent on the master server.
i. 	Decompress the Agent toolkit (there are no special requirements on the directory).
ii. 	Modify the configuration file.
```
./agent/conf/agent.toml
# Enter the Tencent Cloud API key pair for migration
secret_id = 'Enter the Tencent Cloud API AccessKey here'
secret_key = 'Enter the Tencent Cloud API SecretKey here'
```
iii. 	Start the Agent.
```
# chmod +x ./agent/bin/agent
# cd agent/bin  // Start the Agent from the bin directory. Otherwise, you may not be able to find the configuration file
#./agent
The Agent periodically retrieves detailed task configurations from MSP. You do not have to start the Agent repeatedly for multiple created migration tasks.
```
5. 	Scale out the migration cluster by adding worker servers.
The Agent mode supports distributed migration (multi-server collaboration). To increase the migration speed, add worker servers to the migration cluster when the available bandwidth allows.
 - Ensure that the added worker servers can communicate with the master server.
 - If migration is performed through Direct Connect, ensure that the worker servers can directly access COS with Direct Connect.
You can configure the worker servers as needed, but we recommend you configure them in the same way as the master server. The Agent is deployed and started in the same way as the master server, and you need to change `secret_id` and `secret_key` in `agent.toml`. Because the master server is designated when the task is created, the newly added Agent works as a worker node to communicate with the master server and receive the task.
You can add worker servers to the migration cluster at any time. However, we recommend you create all worker servers and the master server and configure and start the Agent before creating a task. In this way, the master server can effectively schedule segments during task startup.

## Migration Status and Progress
You can view the status and progress of all file migration tasks on the file migration tool homepage:
 - For the "task completed" status, green indicates that the migration task was completed and all files were successfully migrated, while yellow indicates that the migration task was completed but some files failed to be migrated.
 - After you click the "Retry failed task" link, files that failed in the task will be retried for migration, while files that have been successfully migrated will not be transferred again.
 - You can click the "Export" link to export the list of files that failed to be migrated.




