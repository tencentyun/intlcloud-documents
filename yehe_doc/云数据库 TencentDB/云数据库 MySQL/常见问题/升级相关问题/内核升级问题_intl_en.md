### How do I upgrade the kernel version?
TencentDB for MySQL supports automatic kernel version upgrade. The upgrade can add new features, improve the performance, and fix issues. It will be triggered automatically in the following scenarios:
- Scenario 1: when a severe bug or security vulnerability occurs in TencentDB for MySQL, the system will upgrade the database kernel version during the maintenance window and send upgrade notifications through Message Center and SMS.
- Scenario 2: when an instance undergoes database version upgrade or configuration adjustment, it will be upgraded to the latest kernel version.
>
>- The instance cannot be downgraded once upgraded to the latest kernel version.
>- Operations such as database version upgrade and configuration adjustment are accompanied by a momentary disconnection from the TencentDB for MySQL instance. Please make sure that your business has a reconnection mechanism.

### How do I check the kernel version?
1. Log in to the [CVM instance](https://intl.cloud.tencent.com/document/product/213/10517) and run the following command to log in to the TencentDB for MySQL instance. For more information, please see [Accessing TencentDB for MySQL from Linux CVM](https://intl.cloud.tencent.com/document/product/236/3130).
 Private network access:
```
mysql -h hostname -u username -p
```
 Public network access:
```
mysql -h [TencentDB IP] -P[TencentDB port number] -uroot -p
```
2. Run the following command to check the version number of the TencentDB for MySQL instance.
```
show variables like 'version_comment';
```
![](https://main.qcloudimg.com/raw/abea801e026190a0cbfd763c5d4862bd.png)

