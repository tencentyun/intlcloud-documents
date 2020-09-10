### How do I upgrade the kernel minor version?
TencentDB for MySQL supports automatic or manual kernel minor version upgrade. Upgrading adds new features, improves performance, and fixes issues.
>?Currently, the kernel minor version of a Basic Edition instance cannot be upgraded.
>
- **Automatic upgrade**:
 - Scenario 1: when a severe bug or security vulnerability occurs in TencentDB for MySQL, the system will perform database kernel minor version upgrade during the maintenance window and send upgrade notifications through the console Message Center and SMS.
 - Scenario 2: when a TencentDB for MySQL instance is migrated due to instance configuration upgrade/downgrade, storage capacity expansion/reduction, or database version upgrade, etc., the system will automatically upgrade the instance’s kernel to the latest minor version.
- **Manual upgrade**:
You can also manually upgrade kernel minor version in the console. For more information, please see [Upgrading Kernel Minor Version](https://intl.cloud.tencent.com/document/product/236/36816).

>!
>- The instance cannot be downgraded once upgraded to the latest kernel minor version.
>- Operations such as database version upgrade and configuration adjustment are accompanied by a momentary disconnection from the TencentDB for MySQL instance. Please make sure that your business has a reconnection mechanism.


### How do I check the kernel minor version?
1. Log in to the [CVM instance](https://intl.cloud.tencent.com/document/product/213/10517) and run the following command to log in to the TencentDB for MySQL instance. For more information, please see [Accessing MySQL Database](https://intl.cloud.tencent.com/document/product/236/3130).
 Private network access:
```
mysql -h hostname -u username -p
```
 Public network access:
```
mysql -h [database IP] -P[database port] -uroot -p
```
2. Run the following command to check the version number of the TencentDB for MySQL instance.
```
show variables like 'version_comment';
```
![](https://main.qcloudimg.com/raw/abea801e026190a0cbfd763c5d4862bd.png)

