## Overview
You can log in to the [CSG Console](https://console.cloud.tencent.com/csg) and click **File Sharing** > **File System**. On this page, you can view all the file systems that have been created.

## Viewing File System
Click an "ID/Name (Mount Directory)" in the list to enter the file system details page where you can view detailed information, lifecycle, sharing settings, accessing information, and file metadata.


### Basic information
On the basic information page, you can view the gateway and bucket (by redirecting to the COS Console) associated with the file system, state, and mount path.


### Lifecycle
File gateway supports the configuration of lifecycle rules for the files stored in COS. You can set to transfer the objects in a specified bucket (i.e., the entire file system) or with a specified prefix to Standard_IA or Archive storage after a specified period of time.

>As the lifecycle configured on the gateway will be eventually stored in the configuration information of the corresponding bucket in COS and take effect, if you have multiple file gateways associated with the same bucket, or if you edit the configuration information of the bucket in the COS Console, the last edited lifecycle rule will be saved and take effect for the bucket.

Lifecycle rules can be added, edited, or deleted in the lifecycle settings as shown below:
- Rule name: set a rule name with no more than 64 characters.
- State: the rule can be "enabled" or "disabled" (i.e., not effective).
- Scope of Application: this indicates the objects for which the rule takes effect. It can be the entire bucket or one or more objects (files) with the specified prefix.
- Transition Rule: you can check whether you want to transition the data to "Standard_IA" storage or "Archive" and set the transition time separately.
>The minimum storage period in Standard_IA storage is 30 days. If it is less than 30 days, the storage fee will still be charged for 30 days. In order to reduce storage costs, the interval between "transition to Archive storage" and "transition to Standard_IA storage" must be at least 30 days.

### Sharing settings
For an NFS file system, you can set the read and write permissions of a visiting user in the sharing settings.
 - **Squash**: set the permissions of a visiting user and a root account.
- All_Squash: any visiting user will be mapped to an anonymous user or user group;
- No_All_Squash: a visiting user will be first matched with a local user, and if the match fails, it will be mapped to an anonymous user or user group;
- Root_Squash: a visiting root user will be mapped to an anonymous user or user group;
- No_Root_Squash: a visiting root user will be allowed to maintain root account permissions;
 - **Write State**: set whether a visiting user's access to the file system is "read/write" or "read-only". 


### Accessing information
If the network environment is complex, you can limit the visiting clients by setting an allowlist.
**Allowed Accessing Address**: this can be an IP or IP range (one item per line).

### File Metadata
If the metadata value of a bucket file or directory is not set, the file gateway will set the file or directory permissions according to the default metadata value in the "File Metadata" settings. The meanings of the fields are as follows:
- **Directory Permission**: access permission for the directory, which is a 4-digit integer. The default value is 0777, indicating that the directory allows reads and writes by everyone.
- **File Permission**: access permission for the file, which is a 4-digit integer. The default value is 0666, indicating that the file allows reads and writes by everyone.
- **User ID**: ID of the default owner of the file system (UID). The default value is 65534 (nfsnobody).
- **Group ID**: ID of the default group of the file system (GID). The default value is 65534 (nfsnobody).
For more information on file permissions and user/group ID, please see [Linux File Permissions](https://www.linux.org/threads/file-permissions-chmod.4124/).


## Deleting File System
As needed by your business, you may want to migrate data. In this case, you need to delete the file system. In order to ensure the proper operations of your business, you are strongly recommended to stop reading from and writing to the file system and unmount it before deleting it.

Find the file system you want to delete in the file system list and select **Delete** in the "Operation" column. Or, if you need to delete file systems in batches, select the ones you want to delete and click **Delete** at the top of the list.
