After logging in to the console, select the "File Sharing -> File System" tab. On this page, you can see all the file systems.

## Viewing a File System
Click an "ID/name (mount directory)" in the list to go to the file system details page where you can view detailed information, modify storage type, lifecycle, sharing settings and accessing information and view file metadata information.


### Basic Information
On the basic information page, you can view the gateway and bucket (jumping to the COS Console for viewing supported) associated with the file system, state and mount path.
![](https://mc.qcloudimg.com/static/img/427c850d61745f04d34e0e4f96f0a9b7/image.png)

### Storage Type
You can set the default storage type (standard or low-frequency) for the files uploaded through the gateway here. If you need to modify the storage type of files in COS, you can do so in the COS Console or through the APIs/SDK provided by COS.
![](https://mc.qcloudimg.com/static/img/5af6daf40d0bec2286f04558a79ab944/image.png)

### Lifecycle
File gateway supports the configuration of the lifecycle rules for the files stored in COS. You can set to transfer the objects in a specified bucket (i.e., the entire file system) or with a specified prefix to low-frequency or archive storage after a specified period of time.

**Note: As the lifecycle configured on the gateway will be eventually stored in the configuration information of the corresponding bucket in COS and take effect, if you have multiple file gateways associated with the same bucket, or if you edit the configuration information of the bucket in the COS Console, the lifecycle rules for the bucket will be saved and take effect for the last edited content.**

Lifecycle rules can be added, edited or deleted in the lifecycle settings as shown below:

Rule name: Set a rule name with no more than 64 characters.
State: The rule can be "enabled" or "disabled" (i.e., not effective).
Scope of application: This indicates the objects for which the rule takes effect. It can be the entire bucket or one or more objects (files) with the specified prefix.
Relegation rule: You can check whether you want to relegate the data to "low-frequency" storage or "archive" and set the relegation time separately. **Note: The shortest storage period of low-frequency storage is 30 days. If it is less than 30 days, the storage fee will still be charged for 30 days. In order to reduce storage cost, the interval between "relegation to archive" and "relegation to low-frequency storage" must be at least 30 days.**

![](https://mc.qcloudimg.com/static/img/4e63c7d1546379fb555e94e8548e6e4c/image.png)
 
### Sharing Settings
For an NFS file system, you can set the read and write permissions of a visiting user in the sharing settings.

* Squash: Set the permissions of a visiting user and a root account. Where:
				All_Squash: Any visiting user will be mapped to an anonymous user or user group;
				No_All_Squash: A visiting user will be first matched with a local user, and if the match fails, it will be mapped to an anonymous user or user group;
				Root_Squash: A visiting root user will be mapped to an anonymous user or user group;
				No_Root_Squash: A visiting root user will be allowed to maintain root account permissions;

* Write state: Set whether a visiting user's access to the file system is "read-only" or "read-and-write".

![](https://mc.qcloudimg.com/static/img/94c37fbfabe4eb20e7031c99333e687a/image.png)  


### Accessing Information
If the network environment is complex, you can limit the visiting clients by setting a whitelist.

* Allowed accessing address: This can be an IP or IP address range; one item per line.

![](https://mc.qcloudimg.com/static/img/8cd9ed270b0a8b9f2846e539dc70928e/image.png)

### File Metadata Information
If the metadata value of the bucket file or directory is not set, the file gateway will set the file or directory permissions according to the default metadata value in the "File metadata" settings. The meanings of the fields are as follows:

Directory permission: Access permission for the directory; 4-digit integer; the default value is 0777 which indicates that the directory allows reads and writes by everyone.

File permission: Access permission for the file; 4-digit integer; the default value is 0666 which indicates that the file allows reads and writes by everyone.

User ID: ID of the default owner of the file system (UID); the default value is 65534 (nfsnobody).

Group ID: ID of the default group of the file system (GID); the default value is 65534 (nfsnobody).

For more information on file permissions and user/group ID, see [Linux File Permissions](https://www.linux.org/threads/file-permissions-chmod.4124/), 

![](https://mc.qcloudimg.com/static/img/31a78ebd8698c35ada24e368834f17ca/image.png)



## Deleting a File System
Depending on the needs of your business, you may want to migrate data. In this case, you need to delete the file system. In order to ensure the proper operations of your business, it is strongly recommended that you stop reading and writing to the file system and unmount it before deleting it.

Find the file system you want to delete in the file system list and select the **Delete** button in the "Operation" column. Or, if you need to batch delete file systems, select the ones you want to delete and click the **Delete** button at the top of the list.

![](https://mc.qcloudimg.com/static/img/da12618eba120de24422170337e79c69/image.png)




