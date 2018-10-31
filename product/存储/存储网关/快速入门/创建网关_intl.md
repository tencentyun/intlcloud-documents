## Precautions Before Installation

1. The server where the gateway is installed can be a **CVM instance** or a **VMware virtual machine** in your local environment. The server configuration needs to meet the following requirements:

Gateway type | Minimum Server Specs | Recommended Server Specs | Disk Configuration
------- | ------- | -------  | -------
Volume gateway | 4-core CPU / 8 GB MEM / 4 Mbps bandwidth | 8-core CPU / 16 GB MEM / 10 Mbps bandwidth | At least two 10+ GB disks
File gateway | 4-core CPU / 4 GB MEM / 8 Mbps bandwidth | 8-core CPU / 16 GB MEM / 120 Mbps bandwidth | At least two 10+ GB disks
Tape gateway | 4-core CPU / 8 GB MEM / 4 Mbps bandwidth | 8-core CPU / 16 GB MEM / 10 Mbps bandwidth | At least two 10+ GB disks
High-IO gateway (high-speed upload, suitable for Direct Connect lines) | 8-core CPU / 64 GB MEM / 400 Mbps bandwidth | - | No disk required

**Note: CSG may not function properly if the system is below the minimum requirements.** For more information on server configuration and disk and memory limitations, see [System Limitations and Precautions](https://cloud.tencent.com/document/product/581/9775).

2. The server on which you log in to the CSG Console (for initiating activation) must interconnect with the server (activated) on which CSG is installed (through either a private network or a public network); **if you are using CVM to deploy CSG, please use the public IP of CVM for activation.**

3. In order to activate and ensure CSG communication, please open the following required ports of the server on which CSG is installed.

Port | Protocol | Use | Suggestion
------- | ------- | ------- | -------
22 | TCP | Used to access and manage CSG server via SSH | It can be selectively opened to servers on the internal network 
80 | TCP | Used to activate the gateway | It needs to be opened to servers that log in to the Tencent Cloud Console to activate CSG (if Tencent Cloud CVM is used, it is okay to use an external IP address to activate) 
3260 | TCP | Used to connect to a volume | It needs to be opened to clients that require volume mounting
111, 662, 892, 2049, 8082, 32803 | TCP | Used to connect to a file system | They need to be opened to clients that require file system mounting 
111, 662, 892, 2049, 32769 | UDP | Used to connect to a file system | They need to be opened to clients that require file system mounting 

4. Network bandwidth settings

The bandwidth settings of CSG must meet the requirement of **"daily uploadable data volume" > "daily written data volume"**. Please set the egress bandwidth and speed limit for CSG based on the amount of data written by your business per day. For example, if 500 GB of data is written to CSG A and the speed is unlimited for all day (i.e., upload time is 24 hours x 60 minutes x 60 seconds), then the minimum egress bandwidth should be set to 50 Mbps.

5. Configure upload buffer and cache disks

a. Upload buffer and cache (for volume and tape gateways)

To ensure proper read/write operation, the system requires that the ratio of the cache to the upload buffer be *3:2*.

- If **cache:upload buffer < 3:2**, the system will not work properly. At this point, you need to increase the cache space.
- If **cache:upload buffer >= 3:2**, the system will automatically adjust the actual usage ratio of the two parts to 3:2. Therefore, if the ratio is greater than 3:2, there will be idle cache space. At this point, you can increase the upload buffer space to take advantage of the idle cache space.

*Note: The local disk cannot be changed once its purpose is set (it can only be added or deleted). If you don't see your disk in the local disk list, click the **Refresh** button.* 

b. Cache and metadata disks configuration (for file gateway)

Both must be over 10 GB.

## Starting to Deploying a Gateway 

After entering the CSG Console, click the **Create a gateway** button in the upper left corner of the list to enter the creation wizard.
![](https://mc.qcloudimg.com/static/img/3295699467ef5535cda16c00be82c812/image.png)	


## Selecting a Region

Since gateways in different regions cannot interconnect with CVM servers, it is recommended that you select the region where your business is mainly located as the region for the gateway. Click **Next**.
*Note: When creating the gateway, the region cannot be modified once set.*
![](https://mc.qcloudimg.com/static/img/8736746c1bbf9f3e10e3d1ca3247db47/image.png)

## Choosing Gateway Type and Performance

Choose "Volume gateway", "File gateway" or "Tape gateway" on the page based on your business scenario.

- Volume gateway: It provides an iSCSI access interface, which caches frequently accessed hot data locally and stores all data in COS.
- File gateway: It provides an NFS v3.0 / v4.0 access protocol which accesses files stored in COS through the file gateway.
- Tape gateway: It provides an iSCSI access interface which stimulates a virtual tape library (VTL) and uses archive storage as the final backend storage to provide more durable and cost-effective storage service.

![](https://mc.qcloudimg.com/static/img/0f52c02a79f58c1135172cf6ddda8e1c/image.png)

## Select the Platform on Which the Gateway Runs

The gateway supports VMware and Linux under CVM for running. If you need to create a gateway in your local environment, please first download and deploy a gateway VM and then activate the gateway. If you need to create a gateway on a CVM instance, please select a VM image containing a gateway in CVM Image Marketplace, execute it and then activate the gateway.

![](https://mc.qcloudimg.com/static/img/54779ae228dbc53e2480262c06fcc1a7/image.png)


### Deploying CSG on VMware
Download the package containing the VM image on the current page.
![](https://mc.qcloudimg.com/static/img/d02d40b2e99351111f2c4bf4fc3059c9/image.png)

#### Deploying a Gateway VM to a VMware Host
  
- Connect to your host
	Open VMware vSphere Client on Windows and log in by entering the host's IP and password.
	![](https://mc.qcloudimg.com/static/img/a19a562c204e25069182276b3adb6931/image.png)
	
- Open the OVF template deployment wizard
	On the "File" menu of vSphere Client, click **Deploy OVF Template**.
	![](https://mc.qcloudimg.com/static/img/b937e1adc501d883799963e7540dc308/image.png)
	
- Select the gateway image file
	In the "Source" pane, select the path of the CSG.ova file just decompressed and click **Next**.
	![](https://mc.qcloudimg.com/static/img/a0c8389fbf39c3c231beb922ecdb9752/image.png)

- Enter a name
	In the "Name and Location" window, enter the name of the VM and click **Next**.
	![](https://mc.qcloudimg.com/static/img/21058d668eec84f00a56a03c6e9412f5/image.png)

- Set up data storage 
	If your host has only one data store, go directly to the next step.
	If it has multiple data stores, you need to choose the one where you want to deploy the VM in the list and click **Next**.
	![](https://mc.qcloudimg.com/static/img/17f78509150cd43543ac8947f24df245/image.png)
	
- Set the disk format 
In the Disk Format window, choose "Thick Provision Lazy Zeroed" or "Thick Provision Eager Zeroed" and click **Next**.	
	Note: Setting the thick provision format can provide enough disk space for the gateway to function properly.
	![](https://mc.qcloudimg.com/static/img/86c76c3f0c01a7ab03ca3c84917ba1fa/image.png)
	
- Complete the setup 
	Follow the setup steps above to complete the VM configuration.
	![](https://mc.qcloudimg.com/static/img/e18dba4da68619e611e8c17c5012e373/image.png)	
	
**Note: In order to block iSCSI connection requests from the Internet, it is recommended to open the ports 22 and 80 on the server where the gateway is located to everyone and open port 3260 only to private IPs.**	
	
	
#### Syncing VM Time with Host	

- Select **Edit Settings** in vSphere Client and then "VMware Tools" in the "Options" tab. Select the "Sync guest time with host" option.
	![](https://mc.qcloudimg.com/static/img/253856bf215be43d5c882c02a5e44ac7/image.png)
	![](https://mc.qcloudimg.com/static/img/cc7744baf1e40d70f30affc2a6cc9555/image.png)

- Sync host time with NTP server.
  Select **Properties** in **Time Settings**.
  ![](https://mc.qcloudimg.com/static/img/34ebfd4dfb03630ac2e4ccccf1356750/image.png)
  
  Set the time and date in the time settings pop-up window.
  ![](https://mc.qcloudimg.com/static/img/81ee7d4b67d8b9d85d5dacc940e5bc77/image.png)
  
  Click the **Options** button in the window above and click "Add" in the pop-up window to add the NTP server's IP or full domain name. You can enter pool.ntp.org as the domain name.
  ![](https://mc.qcloudimg.com/static/img/4021ee87b962df50eaf76846f5da1142/image.png)
  
  Click the **Start** button in the **General** page to start the service and then click **OK**.
  ![](https://mc.qcloudimg.com/static/img/9dbdf6b3b03a7a452551138edf8ad19a/image.png)

#### Pre-configuring Local Disk Storage for Gateway VM	

If you are creating a volume or tape gateway, you need to allocate an "upload buffer" disk and a "cache" disk to the gateway VM in your local disk, DAS or SAN storage. **Cache:upload buffer must be at least 3:2; otherwise, the gateway cannot work properly.**

- **Upload buffer**: Used to store the data to be uploaded. The recommended space is 120% of the "amount of data written per day" of the business. For example, if the daily written data is 300 GB, the upload buffer capacity should be at least 360 GB. *Note: The upload network bandwidth assigned for CSG should be able to at least allow for smoothly uploading the data written per day to the cloud.*

- **Cache**: Used to cache frequently read hot data. Its capacity depends on the amount of data the business needs to read frequently. For example, if 100 GB of data is generated per day and frequently read within one month, while data older than one month is rarely read, then you need to prepare 100*30 GB (about 3 TB) of space as the cache.

The cache is larger than the upload buffer which is 2/3 of the cache, namely: 

*Cache  = 3 TB*
*Upload buffer = cache (3 TB) / 1.5 = 2 TB*


If you are creating a file gateway, you need to allocate a "cache" disk and a "metadata" disk to the gateway VM in your local disk, DAS or SAN storage.

- **Cache**: Used to store the data to be uploaded and frequently accessed hot data. The recommended space for the upload part is 120% of the amount of data written per day of the business. For example, if the daily written data is 300 GB, the minimum space should be 360 GB. The cache space reserved for hot data can be any value. If you want to improve the performance of data read, it is recommended to reserve as much space as possible. *Note: The upload network bandwidth assigned for CSG should be able to at least allow for smoothly uploading the data written per day to the cloud.*

- **Metadata**: Used to store metadata information of files so that you can locally query and search for file information faster. Each 1 GB storage space can store the metadata information of 100,000 files, and 512 MB of space in each metadata disk is reserved for the system. It is recommended to configure the metadata disk space based on 1.2 times the number of files expected in the file system. Please evaluate the number of business files and select the appropriate storage capacity. *Note: After the metadata disk is full, the files cannot be accessed properly. If the storage usage reaches 90%, please increase disk capacity in time.*

Follow the steps below to pre-configure local disk for the gateway VM.

- Click the **Edit Settings** button.
	![](https://mc.qcloudimg.com/static/img/c543d185cce324d9bd78ba91fde45c24/image.png)	
	
- In the pop-up window, click the **Add** button and select "Hard Disk".
	![](https://mc.qcloudimg.com/static/img/ddba7eb592d7e6a6e8fd4f6545a0b1ae/image.png)

- In the pop-up window, select "Create a new virtual disk".
	![](https://mc.qcloudimg.com/static/img/30e9f45df99906c35348b6e6cd6f1104/image.png)
	
- Set the disk capacity (at least 10 GB) and select "Thick Provision Lazy Zeroed" or "Thick Provision Eager Zeroed" for disk provisioning.
	![](https://mc.qcloudimg.com/static/img/4e18ebc34b0b96b351e5afa918405f84/image.png)
	
- Complete disk creation.
	![](https://mc.qcloudimg.com/static/img/ce566e05137128e2d60a68d1e450db81/image.png)


#### Configuring a Disk ID
Since the gateway needs to be mounted through the disk ID, you also need to add ID information for the disk created in the steps above.
	
- Select "General" in the "Options" tab. Click the **Configuration Parameters** button.

![](https://mc.qcloudimg.com/static/img/d47ce35e66d0583d0da3a2c4caae75ea/image.png)
	
- In the pop-up window, click the **Add Row** button. Then in the added row, enter "disk.EnableUUID" for the name field and "true" for the value field. Click the **OK** button and exit.

![](https://mc.qcloudimg.com/static/img/e05d02f29ccef723753bba137496a2c2/image.png)
	
### Deploying CSG on CVM
In the third step of creating a gateway, select "Go to CVM for deployment". Jump from the CSG Console page to the CVM purchase page. You can also create an instance directly in CVM.

![](https://mc.qcloudimg.com/static/img/8aa870b2527a0d51d281f99fd6d8a05f/image.png)

#### Selecting CVM Region and Model
After jumping to the CVM purchase page, select the billing method, region, availability zone, series and model.
**Note: The CVM instance where the gateway is deployed can be in a different region from CSG, but cross-region access incurs corresponding network traffic. In order to ensure proper operation of the gateway, please select the appropriate instance configuration according to the requirements described earlier in this document. If you select an instance below the minimum requirements, CSG cannot start properly.** 

![](https://mc.qcloudimg.com/static/img/b744953d0eeb21f02ba8666a0716958c/image.png)
 
#### Selecting a CSG Image
If you are jumping from the CSG Console to the CVM purchase page, you only need to confirm that the image is a CSG image.
![](https://mc.qcloudimg.com/static/img/f37783fc72d541b7e7e7f63d6434cf2f/image.png)

If you are purchasing a CVM instance directly, you need to select the "Service Marketplace" option, search for "CSG" in the pop-up window and select the desired gateway type.
Note: The system included in the CSG image is CentOS 7.2.
![](https://mc.qcloudimg.com/static/img/d87443a2452c4ee76f05bea4b0d491df/image.png)

#### Selecting Storage and Network
Configure storage and network for CSG. In the CVM instance purchase process, **do not select the data disk (data disk set to 0 GB).** 
![](https://mc.qcloudimg.com/static/img/4e1de73e91cb3b4eab390e142d09af59/image.png)



#### Setting Instance Information and Purchasing
Set the instance name and security group for the gateway. For port opening requirements, see [CSG Security Group Requirements]](https://cloud.tencent.com/document/product/581/9775#.E7.BD.91.E7.BB.9C.E5.8F.8A.E7.BD.91.E5.85.B3.E5.AE.89.E5.85.A8.E7.BB.84). After completing the setup, confirm the purchase.
![](https://mc.qcloudimg.com/static/img/4cf0544a1d410861d032f05ba61b464e/image.png)

**Note: For security reasons, the CVM instance running CSG does not provide root permission for the time being (even if root is configured here). Please use the following username/password to log in to the CSG server for maintenance. <p>

```
Username: csguser
Password: csg123
```

#### Adding a Disk to the Server

After purchasing the CVM instance, you need to go back to the [CVM Console](https://console.cloud.tencent.com/cvm). Create at least two 10+ GB cloud disks in the CVM Console and mount them to the instance. (The gateway needs at least two disks to run properly. Please select the cache/upload buffer/metadata disk capacity according to your business needs, which also can be added later as needed). **Note: In order to guarantee the read/write performance of volume and tape gateways, the capacity of the cache disk must be over 1.5 times that of the upload buffer disk.**

![](https://mc.qcloudimg.com/static/img/fdec74fc8ef0b0481eb14ef91c44f89a/image.png)
![](https://mc.qcloudimg.com/static/img/92c386037e4aeff1dfcf91a1d6fc6994/image.png)

## Connecting to a Gateway

Enter the IP address of the instance where the gateway is located in the CSG Console and click **Connect to gateway**. The activation process associates the gateway with your Tencent Cloud account. Your gateway VM must be running for successful activate.
 
- The gateway runs on the local sever
	Get the IP address from the gateway VM's local console or manager client.
	
- The gateway runs on a CVM instance
  Get the IP address from the CVM Console.
  
 	![](https://mc.qcloudimg.com/static/img/0900a37d4650a2a6d8c0bd4ead88f356/image.png)
 
 *Note: If the activation fails, please check whether the IP address entered is correct. If the IP address is correct, verify whether the network is set to "Allow browser access".*
 

## Activating a Gateway

Configure the time zone and name of the gateway to activate it. 

For a volume gateway, you can select the data write mode here, namely:

- High-speed mode: Data is first written to the memory and then written to the disk from the memory. **Note: Data write is faster, but if exceptions such as unexpected power failure happen before the data is written to the disk, the data cached in the memory may be lost.**

- Stable mode: Data is written directly to the disk. **Note: The stability of data written in this mode is high, and data can be restored in the event of exceptions such as unexpected power failure.**
![](https://mc.qcloudimg.com/static/img/4012fdd301ee6ed62a30a92ec54f12b7/image.png)

If you are creating a tape gateway, you can select the media converter and tape drive in this step. Note: Only STK-L700 and IBM-UTL3580 are supported for the time being.	
![](https://mc.qcloudimg.com/static/img/c87edd7610fae8c3cb0d0ce68fcf38a8/image.png)

  
## Configuring a Local Disk and Completing the Creation  

### Disk Configuration for Volume and Tape Gateways

After obtaining the local disk information, set the disk as "upload buffer" or "cache" according to your business conditions. After setting, click **Finish** and exit the gateway creation wizard. *Note: The local disk cannot be changed once its purpose is set (it can only be added or deleted). If you don't see your disk in the local disk list, click the **Refresh** button.* 

- Upload buffer: Used to store the data to be uploaded. The recommended space is 120% of the "amount of data written per day" of the business. For example, if the daily written data is 300 GB, the upload buffer capacity should be 360 GB. *Note: The upload network bandwidth assigned for CSG should be able to at least allow for smoothly uploading the data written per day to the cloud.*

- Cache: Used to cache frequently read hot data. Its capacity depends on the amount of data the business needs to read frequently. For example, if 100 GB of data is generated per day and frequently read within one month, while data older than one month is rarely read, then you need to prepare at least 100*30 GB (about 3 TB) of space as the cache.

The cache is larger than the upload buffer which is 2/3 of the cache or smaller, namely: 

*Cache  = 3 TB*
*Upload buffer = cache (3 TB) / 1.5 = 2 TB*


![](https://mc.qcloudimg.com/static/img/74499026483883fb7244b8bf391cefdc/image.png)

**Note: To enable the gateway to work properly, **at least one "upload buffer" disk and one "cache" disk need to be configured, and the capacity of the cache disk must be at least 1.5 times that of the upload buffer.** If you don't allocate a local disk to the gateway when creating it, the gateway will be in "to be configured" state and can work properly only after a local disk is configured. For details, see [Managing Disk Configuration](https://cloud.tencent.com/document/product/581/9485#.E7.AE.A1.E7.90.86.E6.9C.AC.E5.9C.B0.E7.A3.81.E7.9B.985).** 

### Disk Configuration for File Gateway

After obtaining the local disk information, set the disk as "cache" or "metadata" according to your business conditions. After setting, click **Finish** and exit the gateway creation wizard. *Note: The local disk cannot be changed once its purpose is set (it can only be added or deleted). If you don't see your disk in the local disk list, click the **Refresh** button.* 

- Cache: Used to store the data to be uploaded and frequently accessed hot data. The recommended space for the upload part is 120% of the amount of data written per day of the business. For example, if the daily written data is 300 GB, the minimum space should be 360 GB. The cache space reserved for hot data can be any value. If you want to improve the performance of data read, it is recommended to reserve as much space as possible. *Note: The upload network bandwidth assigned for CSG should be able to at least allow for smoothly uploading the data written per day to the cloud.*

- Metadata: Used to store metadata information of files so that you can locally query and search for file information faster. Each 1 GB storage space can store the metadata information of 100,000 files, and 512 MB of space in each metadata disk is reserved for the system. It is recommended to configure the metadata disk space based on 1.2 times the number of files expected in the file system. Please evaluate the number of business files and select the appropriate storage capacity. *Note: After the metadata disk is full, the files cannot be accessed properly. If the storage usage reaches 90%, please increase disk capacity in time.*


**Note: To enable the gateway to work properly, **at least one "cache" disk and one "metadata" disk need to be configured.** If you don't allocate a local disk to the gateway when creating it, the gateway will be in "to be configured" state and can work properly only after a local disk is configured. For details, see [Managing Disk Configuration](https://cloud.tencent.com/document/product/581/9485#.E7.AE.A1.E7.90.86.E6.9C.AC.E5.9C.B0.E7.A3.81.E7.9B.985).** 



