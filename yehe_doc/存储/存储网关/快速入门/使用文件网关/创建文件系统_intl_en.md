## Overview

After a file gateway is created, you can bind the storage capacity of a bucket in COS to the file gateway as a file system and then read and write the files stored in COS through the NFS protocol provided by the gateway.

>Before creating the file system, please make sure that a usable file gateway has been created. For detailed directions, please see [Creating Gateways](https://intl.cloud.tencent.com/document/product/581/35697).

## Directions

1. Log in to the [CSG Console](https://console.cloud.tencent.com/csg).
2. On the left sidebar, click **File Sharing** > **File System** to enter the **File System** page and click **Create** to create a file system.

Or, on the left sidebar, click **Gateway List**. Then, on the **Gateway List** page, click **Create File System** to create a file system.

2. In the pop-up window, configure the file system as follows:
 - **Select Gateway**: select the gateway for which to create a file system. After creation, this cannot be modified.
 - **Bucket**: the buckets in COS in the region where the gateway resides will be listed here. If there is no bucket in the region, please go to the COS Console to create one. **Note: the bucket name is the mounting path of the file system.**
 - **File Protocol**: according to the gateway type, the access protocol supported by the file system is automatically displayed as NFS.
 - **Storage Class**: files uploaded through the gateway will be stored into **standard** storage by default. If you want to change the storage class, you can set a lifecycle transition rule in the COS Console.
 - **Allowed Accessing Address**: set the allowlist of visiting IPs or IP ranges to allow these clients to mount and access the file system. If this field is left empty, access will be allowed for all clients. In addition, if it is a multi-IP server, please enter the private IP of the server.
 - **Authorization**: as the files stored in COS belong to the user account, only after authorization is granted can the gateway have the permission to access such files when reading and writing them. Specific permissions include those for configuring the bucket, reading, writing, and deleting all files in the bucket and managing the bucket lifecycle. (The gateway itself does not initiate any operations to the files in COS. Instead, all operations have to be initiated by user and then executed by the gateway.)
