### How do I view CVMs that are currently in use?

You can log in to the [CVM console](https://console.cloud.tencent.com/cvm/index) to view CVMs that are currently in use.

### Can VM be installed on a CVM?

No.

### How do I shut down an instance?

For more information, see [Shutdown Instances](https://intl.cloud.tencent.com/document/product/213/4929).

### How do I restart an instance?

For more information, see [Restarting Instances](https://intl.cloud.tencent.com/document/product/213/4928).

### How do I terminate an instance?

For more information, see [Terminating Instances](https://intl.cloud.tencent.com/zh/document/product/213/4930).

### How do I query the username and password of a Linux instance?
After you create a CVM instance, its username and password will be delivered to your account through the [Message Center](https://console.cloud.tencent.com/message). The admin account of a Linux instance is `root` by default.

### How do I query, partition, and format the disks of a Linux instance?

You can run the `df -h` command to query the total and used disk capacities and run the `fdisk -l` command to view the disk information. For information about how to partition and format the disks of Linux instances, see [Initializing Cloud Disks (Smaller than 2TB)](https://intl.cloud.tencent.com/document/product/362/31597) and [Initializing Cloud Disks (Larger than 2TB)](https://intl.cloud.tencent.com/document/product/362/31598).

### How do I upload files to a Linux instance?
- You can [use SCP to upload files to a Linux instance](https://intl.cloud.tencent.com/document/product/213/2133).
- You can [use FTP to upload files to a Linux instance](https://intl.cloud.tencent.com/document/product/213/35307).

### How do I change the owners and owner groups of directories and files on a Linux instance?
If the file or directory permissions are incorrectly configured on the Web server, a 403 error will occur when you access a website hosted on the instance. Therefore, before you adjust a file or directory, you must confirm the identity under which the file or directory process is running.
- You can run the `ps` and `grep` commands to query the identities under which the file or directory process is running.
- You can run the `ls –l` command to query the owners and owner groups of files and directories.
- You can run the `chown` command to modify the permissions. For example, you can run the `chown -R www.www /tencentcloud/www/user/` command to change the owners and owner groups of all files and directories under the `/tencentcloud/www/user` directory to account "www".

### Do Linux instances support GUI?
Yes. If you need to build a GUI in a Linux instance, see [Building a Visual Ubuntu Desktop](https://intl.cloud.tencent.com/document/product/213/37500).

### Why can’t I add sound or video cards to CVM instances?
Tencent Cloud CVMs do not provide multimedia servers and sound and video card components by default. Therefore, sound and video cards cannot be added to CVM instances.

### Can I specify a MAC address when purchasing a CVM instance?
No. A MAC address is randomly assigned when a CVM instance is created and cannot be specified.

### Can I transfer the unused time of a CVM instance to another CVM instance?
No. If you want higher flexibility and cost-efficiency, we recommend that you purchase pay-as-you-go instances.

### How do I query the region where the IP address of a CVM instance is located in?
The IP address of a CVM instance is located in the same region where you purchased the CVM instance.

### Do CVM instances provide databases by default?
No. To use database services, you can:
- Deploy your own database. For example, you can [install and build MySQL](https://intl.cloud.tencent.com/document/product/213/10190).
- Purchase [TencentDB for MySQL](https://intl.cloud.tencent.com/products/cdb) separately.
- Configure the environment database using the image marketplace.

### Can I build a database on a CVM instance?
Yes. You can install database software and configure a database environment on a CVM instance as needed. You can also purchase [TencentDB for MySQL](https://intl.cloud.tencent.com/zh/products/cdb) separately.

### Do CVM instances support Oracle databases?
Yes. Before you install an Oracle database, we recommend you perform a performance stress test on the target CVM instance to ensure that the instance can satisfy the read/write requirements of the database.

### When can I forcibly stop a CVM instance? What are the consequences of forcibly stopping a CVM instance?
You can forcibly stop a CVM instance when normal shutdown fails. Please note that forced shutdown is equivalent to a power outage and can result in the loss of unsaved data.
