## Where can CSG be used?
Local servers and Tencent Cloud CVM.

## How to connect CSG with Tencent Cloud?
You can use the Internet, VPN or Direct Connect for connection based on the actual upload and download needs.

## What if a CSG-deployed server is shut down exceptionally?
If the gateway is shut down exceptionally (such as unexpected power failure or direct restart or shut-down of the server where it is installed; to shut it down properly, you need to initiate a "stop gateway" operation in the console), it may not start properly or data may be lost. If this happens, in order to protect the cached data that has not been uploaded yet, please submit a ticket immediately.

## What if the gateway is in "to be configured" state and cannot start?
If the gateway is in "to be configured" state in the list, you can click the "Start" button to start it. If it cannot start properly, please check:

* Whether the specs of the gateway server are below 4- core CPU and 4 GB MEM (if this is the case, scale up the server). 
* Whether the cache disk and the upload buffer disk are in "not configured" state (if this is the case, add two 10+ GB disks to the server and set the cache space to 1.5 times the upload buffer space).

## What if a disk of the gateway server does not appear in the local disk list?
The local disk list only displays disks larger than or equal to 10 GB, and disks below 10 GB will not appear in this list.

## How to mount a cloud disk purchased when purchasing a CVM instance?
Because the server running CSG does not provide root permissions, the cloud disk purchased when purchasing a CVM instance cannot be mounted directly (instead, it needs to be mounted in the CVM system). Instead of purchasing a data disk when creating a CVM instance, it is recommended to create a disk and mount it on the "Cloud disk" page in the CVM Console after creating the CVM instance. 

## What if the directory is locked when CIFS/SMB file system is mounted?
If multiple servers access the same file system using the same username/password, the system will treat this type of operations as invalid and then deny access. If necessary, please use different usernames/passwords to log in to different servers to access the same file system.




