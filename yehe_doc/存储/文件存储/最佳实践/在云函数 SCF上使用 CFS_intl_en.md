## Overview

[Tencent Cloud's Serverless Cloud Function](https://intl.cloud.tencent.com/product/scf) (SCF) is a serverless execution environment that enables you to build and run applications without having to purchase and manage servers. Simply code in a supported language and set the execution conditions, and your code can be run on the Tencent Cloud infrastructure elastically and securely. SCF is an ideal computing platform for use cases such as real-time file processing and data processing.

SCF function is a service-level computing resource that features fast iteration and super-fast deployment. As a result, it requires the separation of storage and computing, and that’s what makes CFS, a  high-performance shared storage service, the best storage solution for SCF. With only a few easy steps, your function can easily access files stored in CFS. The benefits of using CFS on SCF are as follows:

- The execution space of functions is unlimited.
- Multiple functions can share the same file system so as to share files.

## Directions

### Associating SCF with a CFS access policy

>!To use the CFS service, SCF needs permission to operate on your CFS resources.

Follow the steps below to grant the permission to your account:

1. Associate the `SCF_QcsRole` role with the `QcloudCFSReadOnlyAccess` policy as instructed in [Modifying a Role](https://intl.cloud.tencent.com/document/product/598/19389). 
   If you don't perform this operation for your currently used account, problems such as failures in saving functions and unavailability of CFS features may occur.
2. If the currently used account is a sub-account, please request the root account to associate the sub-account with the `QcloudCFSReadOnlyAccess` policy as instructed in [Setting Sub-user Permissions](https://intl.cloud.tencent.com/document/product/598/32650). 
   If you don't perform this operation for your currently used sub-account, problems such as unavailability of CFS features may occur.


### Creating a VPC

Build a VPC as instructed in [Building Up a IPv4 VPC](https://intl.cloud.tencent.com/document/product/215/31891).

### Creating CFS resources

Create a CFS file system as instructed in [Creating File Systems and Mount Targets](https://intl.cloud.tencent.com/document/product/582/9132).

>!Currently, SCF allows only CFS file systems whose network type is VPC to be added as mount targets. When creating a CFS file system, please select the same VPC as that of the target function, so as to enable communication.

### Mounting and using CFS file system on SCF

1. Log in to the [SCF console](https://console.cloud.tencent.com/scf/list) and click **Function Service** in the left sidebar.
2. On the **Function Service** page, select the name of the function to be configured.
3. On the **Function configuration** tab of the **Function Management** page, click **Edit** in the top-right corner.
4. Check **Enable** for **VPC**, and select the VPC where your CFS file system resides.
5. Check **Enable** for **File System**, and enter the following information to mount the file system as shown below:
 - **User ID** and **User Group ID**: IDs of the user and user group in CFS file system. SCF uses “10000” for both the user ID and user group ID by default to manipulate your CFS file system. Please set the file owner and corresponding group permission as needed and ensure that your CFS file system has the required permission. For more information, please see [Permission Settings](https://intl.cloud.tencent.com/document/product/582/10951).
 - **Remote Directory**: remote directory in the CFS file system to be accessed by the function, which consists of a file system and remote directory.
 - **Local Directory**: mount target of the local file system. You can use a subdirectory in the `/mnt/` directory to mount the CFS file system.
 - **File System ID**: select the file system to be mounted in the drop-down list.
 - **Mount Point ID**: select the ID of the mount target corresponding to the file system in the drop-down list.
6. Click **Save** at the bottom to complete the configuration.
    You can edit the function code to start using the CFS file system as shown below:

```plaintext
'use strict';
var fs = require('fs');

exports.main_handler = async (event, context) => {
await fs.promises.writeFile('/mnt/file.txt', JSON.stringify(event));
return event
}
```

### Performance test on using CFS file system on SCF

You can use this [Demo](https://github.com/tencentyun/scf_cfs_demo) to test how well CFS performs on SCF.
