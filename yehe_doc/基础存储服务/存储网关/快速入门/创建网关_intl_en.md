## Precautions Before Installation

1. The server where the gateway is installed can be a **CVM instance** or a **VMware virtual host** in your local environment. The server configuration needs to meet the following requirements:

| Gateway type | Minimum Server Specification | Recommended Server Specification | Disk Configuration |
| ---------------------------------------------- | ------------------------------- | ------------------------------- | ---------------------- |
| Volume gateway | 4-core CPU / 8 GB MEM / 4 Mbps bandwidth | 8-core CPU / 16 GB MEM / 10 Mbps bandwidth | At least two 10+ GB disks |
| File gateway | 4-core CPU / 4 GB MEM / 8 Mbps bandwidth | 8-core CPU / 16 GB MEM / 120 Mbps bandwidth | At least two 10+ GB disks |
| Tape gateway | 4-core CPU / 8 GB MEM / 4 Mbps bandwidth | 8-core CPU / 16 GB MEM / 10 Mbps bandwidth | At least two 10+ GB disks |
| High-IO gateway (high-speed upload, suitable for Direct Connect lines) | 8-core CPU / 64 GB MEM / 400 Mbps bandwidth | - | No disk required |

>CSG may not function properly if the system is below the minimum requirements. For more information on server configuration and disk and memory limits, please see [System Limits and Precautions](https://intl.cloud.tencent.com/document/product/581/35681).

2. The server on which you log in to the CSG Console (for initiating activation) must interconnect with the server (activated) on which CSG is installed (through either a private network or a public network); **if you are using CVM to deploy CSG, please use the public IP of CVM for activation.**

3. In order to activate and ensure CSG communication, please open the following required ports of the server on which CSG is installed.

| Port                       | Protocol | Use                       | Suggestion                                   |
| ------------------------------------- | ---- | -------------------------------------- | ------------------------------------------------------------ |
| 22 | TCP | Used to access and manage CSG server via SSH | It can be selectively opened to servers on the private network |
| 80 | TCP | Used to activate the gateway | It needs to be opened to servers that log in to the Tencent Cloud Console to activate CSG (if Tencent Cloud CVM is used, it is okay to use a public IP address to activate) |
| 3260 | TCP | Used to connect to a volume | It needs to be opened to clients that require volume mounting |
| 111, 662, 892, 2049, 8082, 32803 | TCP | Used to connect to a file system | They need to be opened to clients that require file system mounting |
| 111, 662, 892, 2049, 32769 | UDP | Used to connect to a file system | They need to be opened to clients that require file system mounting |

4. Network bandwidth settings

The bandwidth settings of CSG must meet the requirement of "daily uploadable data volume" > "daily written data volume". Please set the egress bandwidth and speed limit for CSG based on the amount of data written by your business per day. For example, if 500 GB of data is written to CSG instance A and the speed is unlimited for all day (i.e., upload time is 24 hours * 60 minutes * 60 seconds), then the minimum egress bandwidth should be set to 50 Mbps.

5. Configure upload buffer and cache disks

Both cache and metadata disks (for file gateway) must be over 10 GB.

## Starting to Deploy Gateway 

After entering the CSG Console, click **Create Gateway** in the top-left corner of the list to enter the creation wizard.	

## Selecting Region

Since gateways and CVM instances in different regions cannot directly communicate with each other, you are recommended to select the region where your business is mainly located as the region for the gateway. Click **Next**.

>When the gateway is created, the region cannot be modified once set.

## Choosing Gateway Type and Performance

Choose "Volume Gateway", "File Gateway" or "Tape Gateway" on the page based on your business scenario.

- Volume gateway: it provides an iSCSI access interface and caches frequently accessed hot data locally and stores all data in COS.
- File gateway: it provides an NFS v3.0 / v4.0 access protocol, enabling users to access files stored in COS through the file gateway.
- Tape gateway: it provides an iSCSI access interface and stimulates a virtual tape library (VTL). It uses archive storage as the final backend storage to provide more durable and cost-effective storage service.



## Selecting the Platform on Which the Gateway Runs

The gateway can run on VMware and Linux CVM. If you need to create a gateway in your local environment, please first download and deploy a gateway VM and then activate the gateway. If you need to create a gateway on a CVM instance, please select a VM image containing a gateway in CVM Image Marketplace, execute it, and then activate the gateway.

### Deploying CSG on VMware

Download the package containing the VM image on the current page.


#### Deploying gateway VM to VMware host

- Connect to your host
  Open VMware vSphere Client on Windows and log in by entering the host's IP and password.
  
- Open the OVF template deployment wizard
  On the "File" menu of vSphere Client, click **Deploy OVF Template**.
  
- Select the gateway image file
  In the "Source" pane, select the path of the CSG.ova file just decompressed and click **Next**.
  
- Enter a name
  In the "Name and Location" window, enter the name of the VM and click **Next**.
  
- Set up data storage 
  If your host has only one data store, go directly to the next step.
  If it has multiple data stores, you need to choose the one where you want to deploy the VM in the list and click **Next**.
  
- Set the disk format 
  In the Disk Format window, choose "Thick Provision Lazy Zeroed" or "Thick Provision Eager Zeroed" and click **Next**.
  Note: setting the thick provision format can provide enough disk capacity for the gateway to function properly.
  
- Complete the setup 
  Follow the setup steps above to complete the VM configuration.
  	

>In order to block iSCSI connection requests from the internet, you are recommended to open the ports 22 and 80 on the server where the gateway resides to everyone and open port 3260 only to private IPs. 	

#### Syncing VM time with host	

- Select **Edit Settings** in vSphere Client and then "VMware Tools" in the "Options" tab. Select the "Sync guest time with host" option.
  
  
- Sync host time with NTP server.
  Select **Properties** in **Time Settings**.
  
Set the time and date in the time settings pop-up window.
  
  
Click **Options** in the window above and click "Add" in the pop-up window to add the NTP server's IP or full domain name. You can enter pool.ntp.org as the domain name.
  
  
Click **Start** in the **General** page to start the service and then click **OK**.
  

#### Pre-configuring local disk storage for gateway VM	

If you are creating a volume or tape gateway, you need to allocate an "upload buffer" disk and a "cache" disk to the gateway VM in your local disk, DAS or SAN storage. The ratio of cache to upload buffer must be at least 3:2; otherwise, the gateway cannot work properly.

>The upload network bandwidth assigned for CSG should be able to at least allow for smoothly uploading the data written per day to the cloud.

- **Cache**: used to cache frequently read hot data. Its capacity depends on the amount of data the business needs to read frequently. For example, if 100 GB of data is generated per day and frequently read within one month, while data older than one month is rarely read, then you need to prepare 100 \* 30 GB (about 3 TB) of capacity as the cache.

The cache is larger than the upload buffer which is 2/3 of the cache, namely: 

Cache = 3 TB
Upload buffer = cache (3 TB) / 1.5 = 2 TB

If you are creating a file gateway, you need to allocate a "cache" disk and a "metadata" disk to the gateway VM in your local disk, DAS or SAN storage.

- **Cache**: it is used to store the data to be uploaded and frequently accessed hot data. The recommended space for the upload part is 120% of the amount of data written per day by the business. For example, if the daily written data is 300 GB, the minimum space should be 360 GB. The cache space reserved for hot data can be any value. If you want to improve the performance of data read, you are recommended to reserve as much space as possible. >The upload network bandwidth assigned for CSG should be able to at least allow for smoothly uploading the data written per day to the cloud.
- **Metadata**: it is used to store metadata of files so that you can locally query and search for file information faster. Each 1 GB of storage capacity can store the metadata of 100,000 files, and 512 MB of capacity in each metadata disk is reserved for the system. You are recommended to configure the metadata disk capacity based on 1.2 times the number of files expected in the file system. Please evaluate the number of business files and select the appropriate storage capacity. 

>After the metadata disk is full, the files cannot be accessed properly. If the storage utilization reaches 90%, please increase disk capacity in time.

Follow the steps below to pre-configure local disk for the gateway VM.

- Click **Edit Settings**.
  	
- In the pop-up window, click **Add** and select "Hard Disk".
  
- In the pop-up window, select "Create a new virtual disk".
  
- Set the disk capacity (at least 10 GB) and select "Thick Provision Lazy Zeroed" or "Thick Provision Eager Zeroed" for disk provisioning.
  
- Complete disk creation.

#### Configuring disk ID

Since the gateway needs to be mounted through the disk ID, you also need to add ID information for the disk created in the steps above.
	

- Select "General" in the "Options" tab. Click **Configuration Parameters**.

- In the pop-up window, click **Add Row**. Then, in the added row, enter "disk.EnableUUID" for the name field and "true" for the value field.
  	

### Deploying CSG on CVM

In the third step of creating a gateway, select "Go to CVM for deployment" and you will be redirected from the CSG Console to the CVM purchase page. You can also create an instance directly in the CVM Console.

#### Selecting CVM region and model

After you are redirected to the CVM purchase page, select the billing mode, region, availability zone, series, and model.

>The CVM instance where the gateway is deployed can be in a different region from CSG, but cross-region access incurs corresponding network traffic. In order to ensure proper operation of the gateway, please select the appropriate instance configuration according to the requirements described earlier in this document. If you select an instance below the minimum requirements, CSG cannot start properly.

#### Selecting CSG image

If you are going from the CSG Console to the CVM purchase page, you only need to confirm that the image is a CSG image.


If you are purchasing a CVM instance directly, you need to select the "Service Marketplace" option, search for "CSG" in the pop-up window and select the desired gateway type.
Note: the system included in the CSG image is CentOS 7.2.

#### Selecting storage and network

Configure storage and network for CSG. In the CVM instance purchase process, **do not select the data disk (data disk is set to 0 GB).** 




#### Setting instance information and purchasing

Set the instance name and security group for the gateway. For more information on port opening requirements, please see [CSG Security Group Requirements](https://intl.cloud.tencent.com/document/product/581/35681#.E7.BD.91.E7.BB.9C.E5.8F.8A.E7.BD.91.E5.85.B3.E5.AE.89.E5.85.A8.E7.BB.84). After completing the setup, confirm the purchase.


>For security reasons, the CVM instance running CSG does not provide root permission for the time being (even if root is configured here). Please use the following username/password to log in to the CSG server for maintenance.

```
Username: csguser
Password: csg123
```

#### Adding disk to server

After purchasing the CVM instance, you need to go back to the [CVM Console](https://console.cloud.tencent.com/cvm). Create at least two 10+ GB cloud disks in the CVM Console and mount them to the instance. (The gateway needs at least two disks to run properly. Please select the cache/upload buffer/metadata disk capacity according to your business needs, which also can be added later as needed).

>In order to guarantee the read/write performance of volume and tape gateways, the capacity of the cache disk must be over 1.5 times that of the upload buffer disk.

## Connecting to Gateway

Enter the IP address of the instance where the gateway resides in the CSG Console and click **Connect to gateway**. The activation process associates the gateway with your Tencent Cloud account. Your gateway VM must be running for successful activation.

- The gateway runs on the local sever
  Get the IP address from the gateway VM's local console or manager client.
- The gateway runs on a CVM instance
  Get the IP address from the CVM Console.

 	

> If the activation fails, please check whether the IP address entered is correct. If the IP address is correct, verify whether the network is set to "Allow browser access".

## Activating Gateway

Configure the time zone and name of the gateway to activate it. 

For a volume gateway, you can select the data write mode here, namely:

- High-speed mode: data is first written to the memory and then written to the disk from the memory. **Note: data write is faster, but if exceptions such as unexpected power failure happen before the data is written to the disk, the data cached in the memory may be lost.**
- Stable mode: data is written directly to the disk. **Note: the stability of data written in this mode is high, and data can be restored in the event of exceptions such as unexpected power failure.**
  

If you are creating a tape gateway, you can select the media converter and tape drive in this step. Note: only STK-L700 and IBM-UTL3580 are supported for the time being.	


## Configuring Local Disk and Completing Creation  

### Disk configuration for volume and tape gateways

After getting the local disk information, set the disk as "upload buffer" or "cache" according to your business conditions. After the disk is set, click **Finish** and exit the gateway creation wizard.

>Note: the local disk cannot be changed once its purpose is set (it can only be added or deleted). If you don't see your disk in the local disk list, click **Refresh**.

- Upload buffer: used to store the data to be uploaded. The recommended space is 120% of the "amount of data written per day" of the business. For example, if the daily written data is 300 GB, the upload buffer capacity should be 360 GB. 

>The upload network bandwidth assigned for CSG should be able to at least allow for smoothly uploading the data written per day to the cloud.

- Cache: used to cache frequently read hot data. Its capacity depends on the amount of data the business needs to read frequently. For example, if 100 GB of data is generated per day and frequently read within one month, while data older than one month is rarely read, then you need to prepare at least 100 \* 30 GB (about 3 TB) of capacity as the cache.

The cache is larger than the upload buffer which is 2/3 of the cache or smaller, namely: 

Cache = 3 TB
Upload buffer = cache (3 TB) / 1.5 = 2 TB



>To enable the gateway to work properly, at least one "upload buffer" disk and one "cache" disk need to be configured, and the capacity of the cache disk must be at least 1.5 times that of the upload buffer. If you don't allocate a local disk to the gateway when creating it, the gateway will be in "to be configured" state and can work properly only after a local disk is configured. For more information, please see [Managing Disk Configuration](https://intl.cloud.tencent.com/document/product/581/35690).

### Disk configuration for file gateway

After getting the local disk information, set the disk as "buffer" or "metadata" according to your business conditions. After the disk is set, click **Finish** and exit the gateway creation wizard.

>The local disk cannot be changed once its purpose is set (it can only be added or deleted). If you don't see your disk in the local disk list, click **Refresh**.

- Cache: it is used to store the data to be uploaded and frequently accessed hot data. The recommended capacity for the upload part is 120% of the amount of data written per day by the business. For example, if the daily written data is 300 GB, the minimum capacity should be 360 GB. The cache space reserved for hot data can be any value. If you want to improve the performance of data read, you are recommended to reserve as much space as possible. 

>The upload network bandwidth assigned for CSG should be able to at least allow for smoothly uploading the data written per day to the cloud.

- Metadata: it is used to store metadata of files so that you can locally query and search for file information faster. Each 1 GB of storage capacity can store the metadata of 100,000 files, and 512 MB of capacity in each metadata disk is reserved for the system. You are recommended to configure the metadata disk capacity based on 1.2 times the number of files expected in the file system. Please evaluate the number of business files and select the appropriate storage capacity. 

>After the metadata disk is full, the files cannot be accessed properly. If the storage utilization reaches 90%, please increase disk capacity in time.

>To enable the gateway to work properly, at least one "cache" disk and one "metadata" disk need to be configured. If you don't allocate a local disk to the gateway when creating it, the gateway will be in "to be configured" state and can work properly only after a local disk is configured. For more information, please see [Managing Disk Configuration](https://intl.cloud.tencent.com/document/product/581/35690).



