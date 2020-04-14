### On what platforms can CSG run?
Local servers and Tencent Cloud CVM.

### How do I connect CSG with Tencent Cloud?
You can use the internet, VPN or Direct Connect for connection based on the actual upload and download needs.

### What should I do if a CSG-deployed server is shut down exceptionally?
If the gateway is shut down exceptionally (such as unexpected power failure or direct restart or shut-down of the server where it is installed; to shut it down properly, you need to initiate a "stop gateway" operation in the console), it may not start properly or data may be lost. In this case, to ensure the security of cache data that has not bee uploaded, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance as soon as possible.

### What should I do if the gateway is in "to be configured" state and cannot start?
If the gateway is in "to be configured" state in the list, you can click "Start" to start it. If it cannot start properly, please check the following configuration items:

* If the specification of the gateway server is below 4-core CPU and 4 GB memory, the gateway cannot be started. In this case, please scale up the server. 
* If the cache disk and the upload buffer disk are not configured, the gateway cannot be started. In this case, please add two 10+ GB disks to the server and set the cache space to 1.5 times the upload buffer space.

### Why does a disk of the gateway server not appear in the local disk list?
The local disk list only displays disks larger than or equal to 10 GB, and disks below 10 GB will not appear in this list.

### How do I mount a cloud disk selected when I purchased a CVM instance?
Because the server running CSG does not provide root permissions, the cloud disk purchased when a CVM instance is purchased cannot be mounted directly (instead, it needs to be mounted in the CVM system). Instead of purchasing a data disk when creating a CVM instance, you are recommended to create a disk and mount it on the "Cloud Disk" page in the CVM Console after creating the CVM instance. 

### What should I do if the directory is locked when a CIFS or SMB file system is mounted?
If multiple servers access the same file system by using the same account/password, the system will treat this type of operations as invalid and then deny access. If necessary, please use different accounts/passwords to log in to different servers to access the same file system.

### What are the CSG client and network environment requirements?
1. Because volume/tape gateways use the ISCSI protocol, the following requirements should be met by the network environment where CSG is deployed and visiting clients:
  a. The client and volume gateway must be both on the public network or both on the private network (the IP must be bound to an ENI).
  b. The client and gateway must be both in Tencent Cloud (the public IP of the CVM instance is not bound to an ENI).
2. Because a file gateway uses the NFS protocol, a client can use the NFS protocol to mount and access it over the public network. However, as data transfer over the NFS protocol is not encrypted, for security reasons, it is not recommended that your client and file gateway be connected through the public network.
