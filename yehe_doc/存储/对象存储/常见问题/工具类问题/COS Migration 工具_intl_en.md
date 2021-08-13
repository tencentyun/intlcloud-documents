### What should I do if the migration tool exits abnormally?

The migration tool supports checkpoint restart. If the upload of a large file is interrupted due to the tool error or service failure, you can run the tool again and restart the upload from the checkpoint.

### If the files that have been migrated successfully to COS are deleted through the console or other methods, will the migration tool upload them again?

No. All successfully uploaded files will be recorded in the `db` directory. Before the migration tool runs, the `db` directory will be scanned first, and the files recorded in it will not be uploaded again. For more information, please see [Migration mechanism and process](https://intl.cloud.tencent.com/document/product/436/15392).

### What should I do if the migration fails with the message "403 Access Deny" displayed in the log?

Check whether your key, bucket, and region information is correct and ensure that you have the operation permission. If you're using a sub-account, it needs to be authorized by the root account. If you migrate data from a local file system or other cloud storage, write/read permission on the bucket is required. For the "Bucket copy" operation, read permission on the source bucket is also required.

### What should I do if the migration to COS from another cloud storage fails with an error message "Read timed out"?

This error occurs when the data download from other cloud storage times out due to insufficient bandwidth. For example, when you migrate overseas data from AWS to COS, "read time out" may occur due to network latency caused by insufficient bandwidth. To solve this problem, you can increase the network bandwidth and test download speed with `wget` before migration.

### What should I do if the migration fails with a message "503 Slow Down" shown in the log?

This error occurs when frequency control is triggered. A limit of 30,000 QPS is imposed on an account in COS. You are advised to decrease the concurrency for small files in configuration. Then run the tool again to resume the migration.

### What should I do if the migration fails with the message "404 NoSuchBucket" shown in the log?

Check whether your key, bucket, and region information is correct.

### What should I do if an exception occurs with the following message?

![img](https://main.qcloudimg.com/raw/9fdac231af66c991c13fe0440e8d7366.png)
The possible reason is that the tool uses rocksdb which requires 64-bit JDK. Check whether your JDK version is X64.

### What should I do if the message "rocksdb's jni library cannot be found" is displayed in a Windows environment?
In a Windows environment, the tool needs to be compiled in Microsoft Visual Studio 2015. In case of the above error message, you need to install [Visual C++ Redistributable for Visual Studio 2015](https://www.microsoft.com/zh-CN/download/details.aspx?id=48145).

### How do I modify the log level?
Modify the file `src/main/resources/log4j.properties` by replacing the value of log4j.rootLogger with the log level, such as DEBUG, INFO, and ERROR.

### What do I do if the `/tmp/librocksdbjnixxx.so: ELF file OS ABI invalid` error is reported in the Linux environment?
IFUNC needs to be supported on Linux and the binutils version in the running environment should be later than 2.20.

If other problems occur, try to run the migration tool again. If the problem persists, please compress the configuration (with the key hidden) as well as the log directory and [contact us](https://intl.cloud.tencent.com/contact-sales).


### Does it need to pull data locally when I use COS Migration to migrate third-party data to Tencent Cloud?

COS Migration can directly and quickly migrate data from third-party source addresses into COS without the need to pull data locally. For more information, see [COS Migration](https://intl.cloud.tencent.com/document/product/436/15392).

Currently, the following migration types are supported:

| Migration Type       | Description                          |
| :---------------- | :---------------------------- |
| migrateLocal      | From local system to COS              |
| migrateAws        | From AWS S3 to COS          |
| migrateAli        | From Alibaba Cloud OSS to COS         |
| migrateQiniu      | From Qiniu to COS              |
| migrateUrl        | From download URL to COS           |
| migrateBucketCopy | From source bucket to destination bucket |
| migrateUpyun      | From UpYun to COS            |


