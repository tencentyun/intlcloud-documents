## Operation Scenarios

[Tencent Cloud File Storage (CFS)](https://intl.cloud.tencent.com/product/cfs) provides a scalable shared file storage service that can be used with various Tencent Cloud services such as CVM, TKE, and batch operations. The standard NFS file system access protocol used by CFS offers shared data sources for multiple computing nodes. It supports elastic capacity and performance scaling. Your existing applications can be mounted for use without modification required. As a highly available and reliable distributed file system, CFS is suitable for various scenarios such as big data analysis, media processing, and content management.
CFS is very cost-effective and pay-as-you-go on an hourly basis, so you only need to pay for the actually used storage space. For more information on CFS billing, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/582/9553).

Tencent Cloud SCF can be seamlessly integrated with CFS. After proper configuration, your functions can easily access files stored in CFS. You can enjoy the following advantages of CFS:
- The execution space of functions is unlimited.
- Multiple functions can share the same file system so as to share files.

## Directions

### Associating authorization policy
>! To use the CFS service, you need to grant SCF the operation permission to your CFS resources.

To use CFS features, please authorize your account in the following steps:
1. Associate the `SCF_QcsRole` role with the `QcloudCFSReadOnlyAccess` policy as instructed in [Modifying Role](https://intl.cloud.tencent.com/document/product/598/19389).
If you don't perform this operation for your currently used account, problems such as failures in saving functions and unavailability of CFS features may occur.

2. If the currently used account is a sub-account, please request the root account to associate the sub-account with the `QcloudCFSReadOnlyAccess` policy as instructed in [Setting Sub-user Permission](https://intl.cloud.tencent.com/document/product/598/32650). 
If you don't perform this operation for your currently used sub-account, problems such as unavailability of CFS features may occur.





### Creating VPC
Please create a VPC as instructed in [Quickly Building IPv4 VPC](https://intl.cloud.tencent.com/document/product/215/31891).

### Creating CFS resource
Please create a CFS resource as instructed in [Creating CFS File System](https://intl.cloud.tencent.com/document/product/582/9132).
>!Currently, SCF allows only CFS file systems whose network type is VPC to be added as mount targets. When creating a CFS file system, please select the same VPC as that of the target function, so as to enable communication.

### Mounting and using CFS file system
1. Log in to the SCF Console and select **[Function Service](https://console.cloud.tencent.com/scf/list)** on the left sidebar.
2. On the **Function Service** page, select the name of the function to be configured.
3. On the **Function Configuration** tab of the **Function Management** page, click **Edit** in the top-right corner.
4. In **VPC"** section, check **Enable** and select the VPC where the CFS file system resides.
5. In **File System** section, check **Enable** and enter the following information to mount the file system.

 - **User ID** and **User Group ID**: IDs of the user and user group in CFS file system. SCF uses “10000” for both the user ID and user group ID by default to manipulate your CFS file system. Please set the file owner and corresponding group permission as needed and ensure that your CFS file system has the required permission. For more information, please see [Permission Settings](https://intl.cloud.tencent.com/document/product/582/10951).
 - **Remote Directory**: remote directory in the CFS file system to be accessed by the function, which consists of a file system and remote directory.
 -  **Local Directory**: mount target of the local file system. You can use a subdirectory in the `/mnt/` directory to mount the CFS file system.
 -  **File System ID**: select the file system to be mounted in the drop-down list.
 -  **Mount Target ID**: select the ID of the mount target corresponding to the file system in the drop-down list.
6. Click **Save** at the bottom to complete the configuration.
You can use the following function code to start using CFS.
```
'use strict';
var fs = requiret('fs');
exports.main_handler = async (event, context) => {
      await fs.promises.writeFile('/mnt/myfolder/filel.txt', JSON.stringify(event)); 
      return event;
};
```
### Testing the CFS Use Performance of SCF
You can use this [script](https://github.com/tencentyun/scf_cfs_demo) to test the performance of SCF when using CFS.
