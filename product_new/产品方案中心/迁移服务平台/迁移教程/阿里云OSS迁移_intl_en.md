# Alibaba Cloud OSS Migration Tutorial

## Agent Semi-Managed Migration

## Scenario

In Agent semi-managed migration mode, you need to manually deploy the Agent on the service of the cloud vendor that hosts your source data so that the Agent can pull the source data through a private network and push it to Tencent Cloud COS.
 Outbound traffic is not billed during Agent semi-managed migration if a direct connection is established between the source-data cloud vendor and Tencent Cloud COS. Therefore, we recommend that you perform Agent semi-managed migration if Direct Connect is available.

The following describes how to configure an Agent semi-managed migration task to migrate data from the Alibaba Cloud OSS to Tencent Cloud COS.

## Preparations

### Alibaba Cloud OSS

Direct Connect preparation:

1. If you want to perform Agent semi-managed migration through Direct Connect, before migration, confirm with the business manager that the COS SDK used by the server in Alibaba Cloud can access COS through Direct Connect.

2. Create a RAM sub-account and grant the required permissions:

3. Log in to the RAM console.

4. Click **People Management** -> **Users** -> **Create User**.

5. Check off console password login and programmatic access, and then enter the user account information.

6. Save the generated account, password, AccessKeyID, and AccessKeySecret.

7. Check off the user login name, and click **Add Permissions** to grant read and write permission to the sub-account’s bucket (AliyunOSSFullAccess).

 

### Tencent Cloud COS

Create a destination bucket:

Create a bucket to store the migrated data. For more information, see [Creating a Bucket](https://intl.cloud.tencent.com/document/product/436/13309).

Create a sub-user for migration and grant the required permissions:

1. Log in to the Tencent Cloud Console.

2. Search for **Access Management** or click **Cloud Access Management** in the **Account Information** drop-down menu.

3. In the left sidebar, click **User Management** to go to the **User List** page.

4. Create a sub-user, and select **Programmatic Access** and **Tencent Cloud Console Access**.

5. Search for and select the QcloudCOSAccessForMSPRole and QcloudCOSFullAccess policies.

6. Finish creating the sub-user and save the sub-user name, login password, SecretId, and SecretKey.

Click [here](https://main.qcloudimg.com/raw/7579efd7d2839e0dfbcff6be0ac2e22b/agent.zip) to download the Agent.

 
> You can use Migration Service Platform (MSP) with your root account. However, for security reasons, we recommend that you create a sub-account, use the sub-account’s API key for migration, and delete the sub-account after migration.

 

## Migration Speed Limit

MSP provides a QPS limit for object storage mode and a bandwidth limit for URL list mode. During Agent-based migration, you can set a speed limit on the migration server and select **No Speed Limit** when creating a task on MSP.

1. Run the following command to view the serial number of the ENI.

```
[root@VM_10_12_centos ~]# ifconfig
```

2. Run the following command to test the download speed before applying speed limiting.

```
[root@VM_10_12_centos ~]# wget https://msp-test-src-1200000000.cos.ap-guangzhou.myqcloud.com/bkce_src-5.0.2.tar.gz
```

3. Run the following command to install the iproute tool. It is installed in CentOS 7.x by default. If this is the case, you can skip this step.

```
[root@VM_10_12_centos ~]# yum -y install iproute
```

4. Run the following command to limit the speed of eth0 to 50 Kbit.

`[root@VM_10_12_centos ~]`*# /sbin/tc qdisc add dev eth0 root tbf rate 50kbit latency 50ms burst 1000*


> **Note:**
>- n eth0 is the SN of the ENI, which is obtained in Step 1.
>- n If you need to limit the speed to 10 Mbit, change 50 kbit to 10 Mbit.

5. Run the following command to check whether the download speed is limited.

```
[root@VM_10_12_centos ~]# wget https://msp-test-src-1200000000.cos.ap-guangzhou.myqcloud.com/bkce_src-5.0.2.tar.gz
```

6. Run the following command to remove the speed limit when needed.

```
[root@VM_10_12_centos ~]# /sbin/tc qdisc del dev eth0 root tbf
```

## Implementing migration

1. Create a temporary server (master server) for migration at the migration source.
    You need to enter the IP address of the Agent master server when creating a migration task. This IP address is a private IP address for communicating with the Worker server in the migration cluster. Therefore, prepare a virtual machine with the CentOS 7.x 64-bit operating system in Alibaba Cloud before creating the migration task.

2. Create a migration task on Tencent Cloud MSP.
      i. In the **Mode Selection** section under **Select migration mode**, select **Create a migration task and download the Agent manually to start migration**.
      ii. In the **Master Node Private IP** section, enter the private IP address of the server created on Alibaba Cloud, such as 172.XXX.XXX.94.
      iii. In the **OSS Private Network EndPoint** section, enter the **EndPoint** (region node) of the object storage bucket.

![Image](https://main.qcloudimg.com/raw/aacc6697dd8a170f0fb946a6be42bb2f.png)


> If the migration source and the destination source contain files with the same name but different contents, we recommend that you select **Skip (keep the file with the same name in the destination bucket)** for **File with the same name**. By default, **Overwrite (the file in the source bucket replaces the file with the same name in the destination bucket)** is selected.**

**Perform secondary migration if the object (file) content is changed during migration.**

3. Click **Create and Start** after setting all the parameters. In Agent mode, the task does not automatically run after creation. Instead, you need to manually start the Agent on the Alibaba Cloud master server as follows:

4. Deploy and start the Agent on the master server.
    i. Decompress the Agent toolkit (there are no special requirements on the directory).
    ii. Modify the configuration file.

    ```
    ./agent/conf/agent.toml
    # Entering the Tencent Cloud API AccessKey pair for migration
    secret_id = 'Enter the Tencent Cloud API AccessKey here'
    secret_key = 'Enter the Tencent Cloud API SecretKey here'
    ```

    iii. Launch Agent.

    ```
    # chmod +x ./agent/bin/agent
    # cd agent/bin  //Start the Agent from the **bin** directory. Otherwise, you may not be able to find the configuration  file.
    #./agent
    ```

The Agent periodically retrieves detailed task configurations from MSP. You do not have to start the Agent repeatedly when multiple migration tasks are created.

5. Scale out the migration cluster by adding Worker servers.
    The Agent mode supports distributed migration (multi-server collaboration). To increase the migration speed, add Worker servers to the migration cluster when the available bandwidth allows.
    
- Ensure that the added Worker servers can communicate with the master server.
- If migration is performed through Direct Connect, ensure that the Worker servers can directly access COS with Direct Connect.

You can configure the Worker servers as needed, but it is recommended that you configure them in the same way as the master server. The Agent is deployed and started in the same way as the master server, and you need to change `secret_id` and `secret_key` in agent.toml. Because the master server is designated when the task is created, the newly added Agent works as a Worker node to communicate with the master server and receive the task.

You can add Worker servers to the migration cluster at any time. However, it is recommended that you create all Worker servers and the master server and configure and start the Agent before creating a task. In this way, the master server can effectively schedule segments during task startup.

## Estimating the File Migration Duration

The migration speed is determined by the lowest speed during each stage of the migration process and is affected by factors such as the network transmission speed and the maximum concurrency. The following table describes these factors.

| Influencing Factor | Description |
| ---------------------- | ------------------------------------------------------------ |
| Read speed of the migration source | The read speed of the data source varies depending on different service providers. The transmission speed typically ranges from 50 Mbps to 200 Mbps. The file reading concurrency ranges from 500 to 3000. The transmission of a large number of small files is subject to this concurrency. |
| Direct connect bandwidth | The data transmission speed between access points depends on the available bandwidth of direct connect. |
| Write speed of the migration destination | For Tencent Cloud COS, the write speed is 200 Mbps and the write concurrency ranges from 500 to 800. Generally, the migration speed ranges from 6 MByte to 25 MByte, that is, 21 GB/h to 87 GB/h. |

 
