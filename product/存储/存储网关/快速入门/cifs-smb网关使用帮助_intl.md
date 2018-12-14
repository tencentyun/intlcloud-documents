After deploying a CIFS/SMB gateway in your local network environment or in a public cloud environment, you can use the CIFS/SMB protocol to read and write massive amounts of cloud data and expand local storage. The gateway not only maintains low latency for hot data access, but also significantly reduces primary data storage costs while minimizing the need for local storage expansion.

## Creating a Gateway

### Precautions Before Installation
1) The server where the gateway is installed can be a **CVM instance** or a **VMware virtual machine** in your local environment. The server configuration needs to meet the following requirements:

| Gateway type | Minimum Server Specs | Recommended Server Specs | Disk Configuration |
| :-----------------------------------------: | :--------------------------------------: | :--------------------------------------: | :--------------------: |
|             NFS gateway, CIFS/SMB gateway              | 4-core CPU, <br />16 GB MEM, <br />4 Mbps bandwidth | 8-core CPU, <br />32 GB MEM, <br />10 Mbps bandwidth | At least two 10+ GB disks |
| High-IO gateway (high-speed upload, suitable for Direct Connect lines) | 8-core CPU, <br /> 64 GB MEM, <br />400 Mbps bandwidth | - | No disk required |
> **Note:**
> **CSG may not function properly if the system is below the minimum requirements.**
> For more information on server configuration and disk and memory limitations, see [System Limitations and Precautions](https://cloud.tencent.com/document/product/581/9775).

2) The server on which you log in to the CSG Console (for initiating activation) must interconnect with the server (activated) on which CSG is installed (through either a private network or a public network); **if you are using CVM to deploy CSG, please use the public IP of CVM for activation.**

3) In order to activate and ensure CSG communication, please open the following required ports of the server on which CSG is installed:

| Port                                  | Protocol | Use                                   | Suggestion                                                     |
| ------------------------------------- | ---- | -------------------------------------- | ------------------------------------------------------------ |
| 22 | TCP | Used to access and manage CSG server via SSH | It can be selectively opened to servers on the internal network |
| 80 | TCP | Used to activate the gateway | It needs to be opened to servers that log in to the Tencent Cloud Console to activate CSG (if Tencent Cloud CVM is used, it is okay to use an external IP address to activate) |
| 111, 662, 892, 2049, 8082, 32803 | TCP | Used to connect to a file system | They need to be opened to clients that require file system mounting |
| 111, 662, 892, 2049, 32769 | UDP | Used to connect to a file system | They need to be opened to clients that require file system mounting |

4) Network bandwidth settings
The bandwidth settings of CSG must meet the requirement of **"daily uploadable data volume" > "daily written data volume"**. Please set the egress bandwidth and speed limit for CSG based on the amount of data written by your business per day. For example, if 500 GB of data is written to CSG A and the speed is unlimited for all day (i.e., upload time is 24 hours \* 60 minutes \* 60 seconds), then the minimum egress bandwidth should be set to 50 Mbps.

5) Configure upload buffer and cache disks
To ensure proper read/write operation, the system requires that the ratio of the cache to the upload buffer be **3:2**.
- If **cache:upload buffer < 3:2**, the system will not work properly. At this point, you need to increase the cache space.
- If **cache:upload buffer >= 3:2**, the system will automatically adjust the actual usage ratio of the two parts to 3:2. Therefore, if the ratio is greater than 3:2, there will be idle cache space. At this point, you can increase the upload buffer space to take advantage of the idle cache space.

>**Note:**
The local disk cannot be changed once its purpose is set (it can only be added or deleted). If you don't see your disk in the local disk list, click the **Refresh** button.


### Starting to Deploying a Gateway 
After entering the CSG Console, click the **Create a gateway** button in the upper left corner of the list to enter the creation wizard.
![](https://mc.qcloudimg.com/static/img/3295699467ef5535cda16c00be82c812/image.png)	


### Selecting a Region
Since gateways in different regions cannot interconnect with CVM servers, it is recommended that you select the region where your business is mainly located as the region for the gateway. Click **Next**.
![](https://mc.qcloudimg.com/static/img/8736746c1bbf9f3e10e3d1ca3247db47/image.png)
> **Note:**
> When creating the gateway, the region cannot be modified once set.

### Choosing Gateway Type and Performance
Choose "NFS gateway" or "CIFS/SMB gateway" on the page based on your business scenario.
- NFS gateway: It provides an NFS v3.0 / v4.0 access protocol where data can be read/written through CSG.
- CIFS/SMB gateway: It provides a CIFS/SMB access protocol where data can be read/written through CSG.


### Select the Platform on Which the Gateway Runs
The gateway supports VMware and Linux under CVM for running. If you need to create a gateway in your local environment, please first download and deploy a gateway VM and then activate the gateway. If you need to create a gateway on a CVM instance, please select a VM image containing a gateway in CVM Image Marketplace, execute it and then activate the gateway.
![](https://mc.qcloudimg.com/static/img/54779ae228dbc53e2480262c06fcc1a7/image.png)

> **Note: "NFS gateway", "CIFS/SMB gateway" and "volume gateway" share the image of "[Tencent Cloud CSG Image - Volume Gateway](https://market.cloud.tencent.com/products/4276?productId=4276&_ga=1.138077944.992563734.1509872671#)".**

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

> **Note:**
> **In order to block iSCSI connection requests from the Internet, it is recommended to open the ports 22 and 80 on the server where the gateway is located to everyone and open port 3260 only to private IPs.** 

### Syncing VM Time with Host	
- Select **Edit Settings** in vSphere Client.
![](https://mc.qcloudimg.com/static/img/253856bf215be43d5c882c02a5e44ac7/image.png)
- Select "VMware Tools" in the "Options" tab. Select the "Sync guest time with host" option.
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

### Pre-configuring Local Disk Storage for Gateway VM	

After finishing, you need to allocate an "upload buffer" disk and a "cache" disk to the gateway VM in your local disk, DAS or SAN storage. **Cache:upload buffer must be at least 3:2; otherwise, the gateway cannot work properly.**

- **Upload buffer**: Used to store the data to be uploaded. The recommended space is 120% of the "amount of data written per day" of the business. For example, if the daily written data is 300 GB, the upload buffer capacity should be at least 360 GB. *Note: The upload network bandwidth assigned for CSG should be able to at least allow for smoothly uploading the data written per day to the cloud.*

- **Cache**: Used to cache frequently read hot data. Its capacity depends on the amount of data the business needs to read frequently. For example, if 100 GB of data is generated per day and frequently read within one month, while data older than one month is rarely read, then you need to prepare 100*30 GB (about 3 TB) of space as the cache.

The cache is larger than the upload buffer which is 2/3 of the cache, namely: 
**Cache = 3 TB**
**Upload buffer = cache (3 TB) / 1.5 = 2 TB**

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
> **Note:**
> **The CVM instance where the gateway is deployed can be in a different region from CSG, but cross-region access incurs corresponding network traffic. In order to ensure proper operation of the gateway, please select the appropriate instance configuration according to the requirements described earlier in this document. If you select an instance below the minimum requirements, CSG cannot start properly.** 

![](https://mc.qcloudimg.com/static/img/b744953d0eeb21f02ba8666a0716958c/image.png)

#### Selecting a CSG Image
If you are jumping from the CSG Console to the CVM purchase page, you only need to confirm that the image is a CSG image.
![](https://mc.qcloudimg.com/static/img/f37783fc72d541b7e7e7f63d6434cf2f/image.png)

If you are purchasing a CVM instance directly, you need to select the "Service Marketplace" option, search for "CSG" in the pop-up window and select the desired gateway type. **Note: "NFS gateway", "CIFS/SMB gateway" and "volume gateway" share the image of "[Tencent Cloud CSG Image - Volume Gateway](https://market.cloud.tencent.com/products/4276?productId=4276&_ga=1.138077944.992563734.1509872671#)".**
![](https://mc.qcloudimg.com/static/img/d87443a2452c4ee76f05bea4b0d491df/image.png)
Note: The system included in the CSG image is CentOS 7.2.

#### Selecting Storage and Network
Configure storage and network for CSG. In the CVM instance purchase process, **do not select the data disk (data disk set to 0 GB).** 
![](https://mc.qcloudimg.com/static/img/4e1de73e91cb3b4eab390e142d09af59/image.png)

#### Setting Instance Information and Purchasing
Set the instance name and security group for the gateway. For port opening requirements, see [CSG Security Group Requirements](https://cloud.tencent.com/document/product/581/9775#.E7.BD.91.E7.BB.9C.E5.8F.8A.E7.BD.91.E5.85.B3.E5.AE.89.E5.85.A8.E7.BB.84). After completing the setup, confirm the purchase.
![](https://mc.qcloudimg.com/static/img/4cf0544a1d410861d032f05ba61b464e/image.png)
> **Note:**
> **For security reasons, the CVM instance running CSG does not provide root permission for the time being (even if root is configured here). Please use the following username/password to log in to the CSG server for maintenance.**

```
Username: csguser
Password: csg123
```

#### Adding a Disk to the Server
After purchasing the CVM instance, you need to go back to the [CVM Console](https://console.cloud.tencent.com/cvm). Create at least two 10+ GB cloud disks in the CVM Console and mount them to the instance. (The gateway needs at least two disks to run properly. Please select the cache/upload buffer/metadata disk capacity according to your business needs, which also can be added later as needed).
![](https://mc.qcloudimg.com/static/img/92c386037e4aeff1dfcf91a1d6fc6994/image.png)
> **Note:**
> **In order to guarantee the read/write performance of volume and tape gateways, the capacity of the cache disk must be over 1.5 times that of the upload buffer disk.**

### Connecting to a Gateway
Enter the IP address of the instance where the gateway is located in the CSG Console and click **Connect to gateway**. The activation process associates the gateway with your Tencent Cloud account. Your gateway VM must be running for successful activate.
- The gateway runs on the local sever
  Get the IP address from the gateway VM's local console or manager client.

- The gateway runs on a CVM instance
  Get the IP address from the CVM Console.

![](https://mc.qcloudimg.com/static/img/0900a37d4650a2a6d8c0bd4ead88f356/image.png)

> Note:
> If the activation fails, please check whether the IP address entered is correct. If the IP address is correct, verify whether the network is set to "Allow browser access".

### Activating a Gateway
Configure the time zone and name of the gateway to activate it. You can select the data write mode here, namely:
- High-speed mode: Data is first written to the memory and then written to the disk from the memory. **Note: Data write is faster, but if exceptions such as unexpected power failure happen before the data is written to the disk, the data cached in the memory may be lost.**

- Stable mode: Data is written directly to the disk. **Note: The stability of data written in this mode is high, and data can be restored in the event of exceptions such as unexpected power failure.**

![](https://mc.qcloudimg.com/static/img/4012fdd301ee6ed62a30a92ec54f12b7/image.png)

### Configuring a Local Disk and Completing the Creation  
After obtaining the local disk information, set the disk as "upload buffer" or "cache" according to your business conditions. After setting, click **Finish** and exit the gateway creation wizard. *Note: The local disk cannot be changed once its purpose is set (it can only be added or deleted). If you don't see your disk in the local disk list, click the **Refresh** button.* 

- Upload buffer: Used to store the data to be uploaded. The recommended space is 120% of the "amount of data written per day" of the business. For example, if the daily written data is 300 GB, the upload buffer capacity should be 360 GB. *Note: The upload network bandwidth assigned for CSG should be able to at least allow for smoothly uploading the data written per day to the cloud.*

- Cache: Used to cache frequently read hot data. Its capacity depends on the amount of data the business needs to read frequently. For example, if 100 GB of data is generated per day and frequently read within one month, while data older than one month is rarely read, then you need to prepare at least 100*30 GB (about 3 TB) of space as the cache.

The cache is larger than the upload buffer which is 2/3 of the cache or smaller, namely: 
- Cache = 3 TB
- Upload buffer = cache (3 TB) / 1.5 = 2 TB

![](https://mc.qcloudimg.com/static/img/74499026483883fb7244b8bf391cefdc/image.png)
> **Note:**
> **To enable the gateway to work properly, at least one "upload buffer" disk and one "cache" disk need to be configured, and the capacity of the cache disk must be at least 1.5 times that of the upload buffer. If you don't allocate a local disk to the gateway when creating it, the gateway will be in "to be configured" state and can work properly only after a local disk is configured. For details, see [Managing Disk Configuration](https://cloud.tencent.com/document/product/581/9485#.E7.AE.A1.E7.90.86.E6.9C.AC.E5.9C.B0.E7.A3.81.E7.9B.985).** 

## Creating a CIFS/SMB File System
After a gateway is created, you need to allocate the cloud storage space (i.e., file system) for the gateway to store user-uploaded data.
On the "CSG Console - Gateway" page or "File Sharing -> File system" page, click **Create a file system** or **New**.
![](https://mc.qcloudimg.com/static/img/1d5c0529709738e1a6527e6a63e77d11/image.png)
![](https://mc.qcloudimg.com/static/img/63321f86e1e25578a3b55e1c349bfa04/image.png)

Enter corresponding information in the pop-up:

* Select gateway: Select the gateway for which to create the file system. After creation, this cannot be modified.
* File protocol: According to the gateway type, the access protocol supported by the file system is automatically displayed as NFS or CIFS/SMB.
* Name (mount directory): This name and gateway IP are part of the file system's mount target name (for example, 10.10.10.19:/filesysname).
  Note: The name must be 1-64 digits or English letters and unique under the same gateway. The name cannot be modified once set.
* Allowed addresses: Set the whitelist of visiting IPs or IP address range to allow these clients to mount and access the file system. If this field is left blank, access is allowed for all clients. Meanwhile, if it is a multi-IP server, please enter the private IP of the server. **Note: The access whitelist is shared by multiple file systems on the same SMB gateway. Therefore, the whitelist information of the gateway will be displayed here, and modifying the list of allowed addresses here will affect the access information of other file systems on the gateway.**

 ![](https://mc.qcloudimg.com/static/img/0dfe1fb6f83853ec41c25d547e5e41cf/image.png) 

## Using a CIFS/SMB File System
After creating a file system, configure a server or client as follows and then mount the file system to it for use. An SMB gateway supports CIFS, SMB2.0 and SMB 3.0.

**Note: If you are using a gateway on CVM, it is recommended to deploy the gateway under the VPC of each visiting client; if the clients are on different VPCs, please use [Peering Connection](https://cloud.tencent.com/document/product/215/5000) to achieve network interconnection.**

### Using an SMB File System on Windows
#### Creating an SMB User and Granting Permissions
Create a user in the CSG Console for accessing the file system, set the username and password and grant file system permissions to the user.
![](https://mc.qcloudimg.com/static/img/26b6ad3bfa669ad01dc0852cd810df26/image.png)

#### Adding an Access Whitelist
In the file system, add the IPs of the visiting clients to "Allowed addresses" to grant them access. If you use CVM to access, it is recommended to add both the private and public IPs to the allowed addresses (you can get the private and public IPs in the CVM Console).
![](https://mc.qcloudimg.com/static/img/ba1f23f1ceaec7a46e47a25594960b39/image.png)


#### Opening "Map Network Drive"
Log in to Windows where you need to mount the file system, find "Computer" in the "Start" menu, right-click it and then click "Map network drive" in the menu that appears. 
![](https://mc.qcloudimg.com/static/img/5696d66a83d4e9b35196274f89e07dfc/image.png)
![](https://mc.qcloudimg.com/static/img/6eeb1c0838e6aab185ed8b76dc736912/image.png)

#### Entering the Access Path
In the pop-up settings window, set the drive letter for "Drive" and folder (i.e., the mount directory you see in the SMB file system).
![](https://mc.qcloudimg.com/static/img/004ef32b0b934ed6d666405a38fff999/image.png)

#### Entering Username and Password
After clicking the **Finish** button, enter the username and password created in the first step in the pop-up window and click "OK" to complete the mount.
![](https://mc.qcloudimg.com/static/img/27f2f6fdcb2f75ea974ef96bdb90ef28/image.png)

**Note: Do not use the same username and password to access the same file system from multiple clients. This operation will be automatically recognized as invalid (and the file system will be locked).**


#### Verifying Read/write
After confirmation, the page goes directly to the file system that has been mounted. You can right click to create a file to verify the correctness of read/write.
![](https://mc.qcloudimg.com/static/img/60b9388885536ec7d81b1cf7f76c39d5/image.png)

#### Disconnecting the File System
To disconnect a mounted file system, simply right-click the disk and click **Disconnect** in the menu that appears.
![](https://mc.qcloudimg.com/static/img/376cd0547aa64f4d519e5444c5a58f93/image.png)


## Managing a CIFS/SMB User

After logging in to the console, you can manage users of the CIFS/SMB gateway in the "File sharing -> CIFS/SMB users" menu.
![](https://mc.qcloudimg.com/static/img/1844afdea6b5c428eb5e5cb204e52025/image.png)

### Viewing User Information

Click a "Username" in the list to enter the user details page where you can view the user details.
![](https://mc.qcloudimg.com/static/img/eb6ea81fd40aec4aed6a056846467e1b/image.png)


### Editing User Information

On the user details page, click the "Edit" icon to modify user details and file system permissions. **Note: If a client is using the user to mount or access the file system, changing the password or file system permissions may cause unavailability of the file system due to loss of permissions. In addition, if you use Linux to mount the SMB file system, due to the protocol restrictions, you need to restart the client to make the new user permissions or password take effect.**
![](https://mc.qcloudimg.com/static/img/aaf0bd8aa9ace5c98df757ca7f792ff9/image.png)
![](https://mc.qcloudimg.com/static/img/188df01176ce3697658675abf43e2ea1/image.png)

### Disabling/Enabling a User

When you need to disable a user, you can find the **Disable** or **Enable** button in the "Operation" column of the CIFS/SMB user list. Click the **Disable now** or **Enable now** button in the pop-up to change the user status. **Note: If a client is using the user to mount or access the file system, changing the password or file system permissions may cause unavailability of the file system due to loss of permissions. In addition, if you use Linux to mount the SMB file system, due to the protocol restrictions, you need to restart the client to make the new user permissions or password take effect.**
![](https://mc.qcloudimg.com/static/img/00ccf74c97a308ca95f7eef325f2ebd6/image.png)
![](https://mc.qcloudimg.com/static/img/55a2f0e5cd77217355f00fd845e27665/image.png)

### Deleting a User

If you need to delete a user, you can find the **Delete** button in the "Operation" column in the CIFS/SMB user list. Click the **Delete now** button in the pop-up to delete the user.
![](https://mc.qcloudimg.com/static/img/3e79cdb1989efa6d68c86b0151cda0c5/image.png)


## FAQs for CIFS/SMB Gateway

### What If the Directory Is Locked When CIFS/SMB File System Is Mounted?

If multiple servers access the same file system using the same username/password, the system will treat this type of operations as invalid and then deny access. If necessary, please use different usernames/passwords to log in to different servers to access the same file system.
