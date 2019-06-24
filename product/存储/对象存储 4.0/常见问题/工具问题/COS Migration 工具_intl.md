### What should I do if the migration tool exit abnormally?

The migration tool supports resuming upload from breakpoint. If the upload of a large file is interrupted due to the tool error or service failure, you can run the tool again and resume the upload from the breakpoint.

### If the files that have been migrated successfully to COS are deleted through the console or other methods, will the migration tool upload them again?

No. All the migrated files are recorded in db. The migration tool scans db directory before each migration and the files recorded in db will not be uploaded again. For more information, see [Migration Mechanism and Process](https://intl.cloud.tencent.com/document/product/436/15392#.E8.BF.81.E7.A7.BB.E6.9C.BA.E5.88.B6.E5.8F.8A.E6.B5.81.E7.A8.8B).

### What should I do if the migration fails with an message “403 Access Deny” shown in the log?

Check whether your key, Bucket and Region information is correct and ensure you have the operation permission. If you're using a sub-account, it needs to be authorized by the parent account. If you migrate data locally or from other cloud storages, write/read access to the bucket is required. For the "Bucket copy" operation, read access to the source bucket is also required.

### What should I do if the migration to COS from another cloud storage fails with an error message "Read timed out"?

This error occurs when the data download from other cloud storages times out due to insufficient bandwidth. For example, when you migrate overseas data from AWS to COS, "read time out" may occur due to network latency caused by insufficient bandwidth. To solve this problem, you can increase the network bandwidth and test download speed with wget before migration.

### What should I do if the migration fails with a message "503 Slow Down" shown in the log?

This error occurs when frequency control is triggered. A limit of 800 QPS is imposed on an account in COS. You are recommended to decrease the concurrency for small files in configuration. Then run the tool again to resume the migration.

### What should I do if the migration fails with the message "404 NoSuchBucket" shown in the log?

Check whether your key, Bucket and Region information is correct.

### What should I do if an exception occurs with the following message?

![img](https://main.qcloudimg.com/raw/9fdac231af66c991c13fe0440e8d7366.png)
The possible reason is that the tool is using rocksdb which requires 64-bit JDK. Check whether your JDK version is X64.

### What should I do if the message "rocksdb's jni library cannot be found" is displayed in Windows environment?
In Windows environment, the tool needs to be compiled in the Microsoft Visual Studio 2015. In case of the above error message, you need to install [Visual C++ Redistributable for Visual Studio 2015](https://www.microsoft.com/zh-CN/download/details.aspx?id=48145).

### How do I modify the log level?
Modify the file src/main/resources/log4j.properties by replacing the value of log4j.rootLogger with the log level, such as DEBUG, INFO, and ERROR.

In case of other problems, try running the migration tool again. If the failure persists, [submit a ticket](https://console.cloud.tencent.com/workorder/category) attached with a compressed file containing the configuration information (with key information hidden) and the log directory.

