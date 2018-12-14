## System and Network Bandwidth Requirements of CSG
The following lists the minimum and recommended system requirements for CSG. **Note: CSG may not function properly if the system is below the minimum requirements.**

Gateway type | Minimum Server Specs | Recommended Server Specs | Disk Configuration
------- | ------- | -------  | -------
Volume gateway | 4-core CPU / 8 GB MEM / 4 Mbps bandwidth | 8-core CPU / 16 GB MEM / 10 Mbps bandwidth | At least two 10+ GB disks
File gateway | 4-core CPU / 4 GB MEM / 8 Mbps bandwidth | 8-core CPU / 16 GB MEM / 120 Mbps bandwidth | At least two 10+ GB disks
Tape gateway | 4-core CPU / 8 GB MEM / 4 Mbps bandwidth | 8-core CPU / 16 GB MEM / 10 Mbps bandwidth | At least two 10+ GB disks
High-IO gateway (high-speed upload, suitable for Direct Connect lines) | 8-core CPU / 64 GB MEM / 400 Mbps bandwidth | - | No disk required


## Recommended Local Disk Capacity Settings
In order to get the best performance of your CSG, it is recommended to set the upload network bandwidth of the gateway and the capacity of the local disk used as "upload buffer" based on the amount of data you need to upload each day. Meanwhile, you need to configure the local "cache" disk based on your needs for hot data reads. **Note: Disks below 10 GB cannot be used as "cache", "upload buffer" or "metadata" disks.**

### Volume and Tape Gateways

 Item | Recommended Capacity
------- | -------
Local bandwidth x upload duration | Greater than the amount of data uploaded per day
Upload buffer disk | Greater than the amount of data uploaded per day
Cache disk | Greater than the estimated amount of frequently read data
Cache disk:upload buffer disk | Greater than 1.5:1

For example, if 500 GB of data is generated per day and requires uploading through CSG daily from 20:00 to 06:00, then the recommended bandwidth is at least 120 Mbps, and a disk capacity of at least 500 GB is needed locally as the "upload buffer". If the data that is frequently read is that in the last 7 days, a disk capacity of at least 7 x 500 GB = 3.5 TB is needed as the "cache". 


### File Gateway

Item | Recommended Capacity
------- | -------
Local bandwidth x upload duration | Greater than the amount of data uploaded per day
Cache disk | Used to store data to be uploaded and locally read hot data; capacity > amount of data uploaded per day + estimated amount of frequently read data
Metadata disk | 1 GB capacity can support 100,000 files, and 512 MB of space in each metadata disk is reserved for the system. It is recommended to configure the metadata disk based on 1.2 times the number of files expected in the file system

For example, one billion files are stored in a COS bucket, and you configure CSG for the bucket, so it is recommended that you configure a metadata disk of at least 10 TB. However, in order to reserve space for new files, it is recommended to make the metadata disk 12 TB. If 100 GB of new data is generated per day and the egress bandwidth can upload this 100 GB of data every day, a local disk capacity of 120 GB can be configured as the "upload buffer".



## Restricting Relationship Between Memory and Local Disk
As memory limits the read/write performance of the gateway, please configure the "cache" and "upload buffer" disks according to the memory size of the virtual machine where the gateway resides. The restricting relationship is as follows (not applicable to file gateway):

Memory | Cache Disk Limit (Multiple Disks Supported) | Upload Buffer Disk Limit (Multiple Disks Supported) 
------- | ------- | -------
4 GB (minimum) | 8 TB | 4 TB 
8 GB  | 16 TB |  8 TB 
16 GB | 32 TB |  16 TB 
32 GB | 64 TB |  32 TB 

**Note: Due to VMware version restrictions, the upper capacity limit for a single disk is 2 TB for ESXi versions below 5.5 and 8 TB for ESXi 5.5 or above.**

## Network and Gateway Security Group
To ensure data security and prevent iSCSI/NFS connections from the Internet, it is recommended to configure the following security groups on the server running CSG:

Port | Protocol | Use | Suggestion
------- | ------- | ------- | -------
22 | TCP | Used to access and manage CSG server via SSH | It can be selectively opened to servers on the internal network 
80 | TCP | Used to activate the gateway | It needs to be opened to servers that log in to the Tencent Cloud Console to activate CSG (if Tencent Cloud CVM is used, it is okay to use an external IP address to activate) 
3260 | TCP | Used to connect to a volume | It needs to be opened to clients that require volume mounting
111, 662, 892, 2049, 8082, 32803 | TCP | Used to connect to a file system | They need to be opened to clients that require file system mounting 
111, 662, 892, 2049, 32769 | UDP | Used to connect to a file system | They need to be opened to clients that require file system mounting 

<!--If you are deploying CSG on CVM, you can select **Create a security group** when configuring security groups in step 4 of the purchase process, find the  "CSG security group" in the list and select it.
-->

**Note: When creating a gateway using CVM, it is recommended to give priority to basic network as the gateway may not upload data properly if VPC is used (the gateway needs to upload data to COS, but the network connection between your VPC and COS may not be available).** 

## Precautions
### Precautions for Restart and Shutdown
When stopping a gateway in use, please be sure to stop the service in the CSG Console. After the operation is completed and the gateway enters "stopped" state in the console, restart the CVM instance or physical server running CSG.
**Note: Directly restarting CVM instance or physical server or cutting their power supply may cause data inconsistency for the local upload buffer, resulting in the gateway not working properly after the CVM instance or server restarts.** If this happens and the gateway does not work properly, please submit a ticket as soon as possible.

### CSG Sever Password
In order to ensure that your CSG program can be upgraded and communicate with the cloud, please do not change the password of the CSG server. If the password is changed, the gateway may not work properly.

