
## Overview
In Agent semi-managed migration mode, you need to manually deploy the Agent on the service of the cloud vendor that hosts your source data so that the Agent can pull the source data over private network and push it to Tencent Cloud COS.
Outbound traffic is not billed during Agent semi-managed migration if a Direct Connect dedicated connection is established between the source-data cloud vendor and Tencent Cloud COS. Therefore, we recommend that you perform Agent semi-managed migration if Direct Connect is available.

The following describes how to configure an Agent semi-managed migration task to migrate data from the Alibaba Cloud OSS to Tencent Cloud COS.

## Preparations
#### Alibaba Cloud OSS
1. Confirm Direct Connect connection:
To perform Agent semi-managed migration over Direct Connect, first confirm with your sales rep that the COS SDK used by the server in Alibaba Cloud OSS can access COS over Direct Connect.
2. Create a Alibaba Cloud RAM sub-account and grant required permissions:
	1. Log in to the RAM console.
	2. Click **Identities** > **Users** > **Create User**.
	3. In the Access Mode section, select **Console Password Logon** and **Programmatic Access**. Enter other account information.
	4. Save the generated account ID, password, AccessKeyID, and AccessKeySecret.
	5. Select the newly created user name on the Users Management page, and click **Authorize** under **Actions** to grant this sub-account all access to OSS (AliyunOSSFullAccess).

#### Tencent Cloud COS
1. Create a bucket to store your migrated data. For more information, see [Creating Buckets](https://intl.cloud.tencent.com/document/product/436/13309).
2. Create a sub-user for migration and grant required permissions:
	1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam/overview).
	2. In the left sidebar, click **Users** > **User List**.
	3. Select **Create User** > **Custom Create**. In the **Create Sub-user** page, select both **Programming Access** and **Tencent Cloud Console access** for **Access mode**.
	4. Search for and select the QcloudCOSAccessForMSPRole and QcloudCOSFullAccess policies.
	5. Complete the creation steps and save the sub-user name, login password, SecretId, and SecretKey.
- Click [here](https://migrate-1256125716.cos.ap-guangzhou.myqcloud.com/agent/agent.zip) to download Agent.

>?You can also migrate data using your root account. However, for security reasons, we recommend that you instead create a new sub-user, use its API key for migration, and then delete the sub-user.

## Migration Speed Limits
MSP provides a QPS limit for object storage mode and a bandwidth limit for URL list mode. During Agent-based migration, you can set a speed limit on the migration server and select **No Speed Limit** when creating a task on MSP.
1. Run the following command to view the serial number of the ENI.
```
[root@VM_10_12_centos ~]# ifconfig
```
2. Run the following command to test the download speed before applying speed limiting.
```
[root@VM_10_12_centos ~]# wget https://msp-test-src-1200000000.cos.ap-guangzhou.myqcloud.com/bkce_src-5.0.2.tar.gz
```
3. Run the following command to install iproute. It is installed on CentOS 7.x by default, in which case you can skip this step.
```
[root@VM_10_12_centos ~]# yum -y install iproute
```
4. Run the following command to limit the speed of eth0 to 50 Kbit.
```
[root@VM_10_12_centos ~]# /sbin/tc qdisc add dev eth0 root tbf rate 50kbit latency 50ms burst 1000
```
>?
>- eth0 is the SN of the ENI, which is obtained in Step 1.
>- To limit the speed to 10 Mbit, change 50 kbit to 10 Mbit.
5. Run the following command to check whether the download speed is limited.
```
[root@VM_10_12_centos ~]# wget https://msp-test-src-1200000000.cos.ap-guangzhou.myqcloud.com/bkce_src-5.0.2.tar.gz
```
6. Run the following command to remove the speed limit when needed.
```
[root@VM_10_12_centos ~]# /sbin/tc qdisc del dev eth0 root tbf
```

## Migration
1. Create a temporary server (master server) for migration at the migration source.
The creation of a migration task requires the private IP address of your Agent master server for communicating with Worker servers in the migration cluster. Therefore, before the creation, you need to prepare a virtual machine running on CentOS 7.x 64-bit in Alibaba Cloud.
2. Create a migration task on Tencent Cloud MSP.
	i. In the **Mode Selection** section under **Select migration mode**, select **Create a migration task and download the Agent manually to start migration**.
	ii. In the **Master Node Private IP** section, enter the private IP address of the server created on Alibaba Cloud, such as 172.XXX.XXX.94.
	iii. In the **OSS Private Network EndPoint** section, enter the **EndPoint** (region node) of your Alibaba Cloud OSS bucket.
![](https://main.qcloudimg.com/raw/aacc6697dd8a170f0fb946a6be42bb2f.png)
>!
>- If the files with the same name exist in both the migration source and destination, we recommend that you select **Skip (keep the file with the same name in the destination bucket)** for **File with the same name**. By default, **Overwrite (the file in the source bucket replaces the file with the same name in the destination bucket)** is selected.
>- If the object (file) content is changed during migration, you need to migrate again.
3. Click **Create and Start** after setting all the parameters. In Agent mode, the task does not automatically run after creation. Instead, you need to manually start the Agent on the Alibaba Cloud master server as follows:
4. Deploy and start the Agent on the master server.
	i. Decompress the Agent toolkit (no special requirements on the directory).
	ii. Modify the configuration file.
```
./agent/conf/agent.toml
# Enter the Tencent Cloud API AccessKey pair for migration
secret_id = 'Enter the Tencent Cloud API AccessKey here'
secret_key = 'Enter the Tencent Cloud API SecretKey here'
```
iii. Start the Agent.
```
# chmod +x ./agent/bin/agent
# cd agent/bin  //Start the Agent from the **bin** directory. Otherwise, you may not be able to find the configuration file.
#./agent
The Agent periodically retrieves detailed task configurations from MSP. You do not have to start the Agent repeatedly when multiple migration tasks are created.
```
5. Scale out the migration cluster by adding Worker servers.
The Agent mode supports distributed migration (multi-server collaboration). To increase the migration speed, add Worker servers to the migration cluster when the available bandwidth allows.
 - Ensure that the added Worker servers can communicate with the master server.
 - If migration is performed through Direct Connect, ensure that the Worker servers can directly access COS over Direct Connect.
You can configure the Worker servers as needed, but it is recommended that you configure them in the same way as the master server. The Agent is deployed and started in the same way as the master server, and you need to change `secret_id` and `secret_key` in agent.toml. Because the master server is designated when the task is created, the newly added Agent works as a Worker node to communicate with the master server and receive the task.
You can add Worker servers to the migration cluster at any time. However, it is recommended that you create all Worker servers along with the master server and configure and start the Agent before creating a task. In this way, the master server can effectively schedule segments during task startup.

## Viewing Migration Status and Schedule
You can view the status and schedule of all migrated files under **Object Storage Migration** in the MSP console.
 - For tasks with **Status** displayed as **Task completed**, the green bar indicates that all files were migrated successfully while a yellow bar indicates only part of files were so.
 - Click the task retry option under **Operation** to re-migrate only failed files in the task.
 - Click the export option under **Operation** to export the list of failed files during migration.

## Estimating the File Migration Duration
The migration speed is determined by the lowest speed during each migration stage and is affected by factors such as network transfer speed and maximum concurrency as shown below:

| Factor | Description |
| ---------------------- | ------------------------------------------------------------ |
| Read speed of the migration source | The read speed of the data source varies depending on different service providers.<br><li>The transfer speed typically ranges from 50 Mbps to 200 Mbps.<br><li>The number of concurrent reads ranges from 500 to 3,000, a limit put on transfers of a large number of small files. |
| Direct Connect bandwidth | The data transfer speed between access points depends on the available bandwidth of Direct Connect. |
| Write speed of the migration destination | For Tencent Cloud COS, the write speed is 200 Mbps and the number of concurrent writes ranges from 500 to 800.<br>Generally, the migration speed ranges from 6 MByte to 25 MByte, that is, 21 GB/h to 87 GB/h. |



