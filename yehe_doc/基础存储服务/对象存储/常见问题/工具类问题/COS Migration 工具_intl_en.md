### What should I do if the migration tool exits abnormally?

The migration tool supports checkpoint restart. If the upload of a large file is interrupted due to the tool error or service failure, you can run the tool again and restart the upload from the checkpoint.

### If the files that have been migrated successfully to COS are deleted through the console or other methods, will the migration tool upload them again?

No. All successfully uploaded files will be recorded in the `db` directory. Before the migration tool runs, the `db` directory will be scanned first, and the files recorded in it will not be uploaded again. For more information, see [Migration mechanism and process](https://intl.cloud.tencent.com/document/product/436/15392).

### What should I do if the migration fails with the message "403 Access Deny" displayed in the log?

Check whether your key, bucket, and region information is correct and ensure that you have the operation permission. If you're using a sub-account, it needs to be authorized by the root account. If you migrate data from a local file system or other cloud storage, write/read permission on the bucket is required. For the "Bucket copy" operation, read permission on the source bucket is also required.

### What should I do if the migration to COS from another cloud storage fails with an error message "Read timed out"?

This error occurs when the data download from other cloud storage times out due to insufficient bandwidth. For example, when you migrate overseas data from AWS to COS, "read time out" may occur due to network latency caused by insufficient bandwidth. To solve this problem, you can increase the network bandwidth and test download speed with `wget` before migration.

### What should I do if the migration fails with a message "503 Slow Down" shown in the log?

This error occurs when frequency control is triggered. A limit of 30,000 QPS is imposed on an account in COS. We recommend you decrease the concurrency for small files in configuration. Then run the tool again to resume the migration.

### What should I do if the migration fails with the message "404 NoSuchBucket" shown in the log?

Check whether your key, bucket, and region information is correct.

### What should I do if an exception occurs with the following message?

![img](https://main.qcloudimg.com/raw/9fdac231af66c991c13fe0440e8d7366.png)
The possible reason is that the tool uses RocksDB which requires 64-bit JDK. Check whether your JDK version is x64.

### What should I do if the message "rocksdb's jni library cannot be found" is displayed in a Windows environment?
In a Windows environment, the tool needs to be compiled in Microsoft Visual Studio 2015. In case of the above error message, you need to install [Visual C++ Redistributable for Visual Studio 2015](https://www.microsoft.com/zh-CN/download/details.aspx?id=48145).

### How do I modify the log level?
Modify the file `src/main/resources/log4j.properties` by replacing the value of log4j.rootLogger with the log level, such as DEBUG, INFO, and ERROR.

### What do I do if the `/tmp/librocksdbjnixxx.so: ELF file OS ABI invalid` error is reported in the Linux environment?
IFUNC needs to be supported on Linux and the binutils version in the running environment should be later than 2.20.

### What should I do if a task fails to be fully executed and "java.nio.file.FileSystemLoopException" is reported in `error.log`?
The exception information in `error.log` is similar to:

```
2022-XX-XX XX:XX:XX [ERROR] [main:xxx] [com.qcloud.cos_migrate_tool.task.MigrateLocalTaskExecutor:] [MigrateLocalTaskExecutor.java:183]
walk file tree error
java.nio.file.FileSystemLoopException: /dataseal/xx1/file1
at java.nio.file.FileTreeWalker.visit(FileTreeWalker.java:294)
at java.nio.file.FileTreeWalker.next(FileTreeWalker.java:372)
at java.nio.file.Files.walkFileTree(Files.java:2706)
at com.qcloud.cos_migrate_tool.task.MigrateLocalTaskExecutor.buildTask(MigrateLocalTaskExecutor.java:176)
at com.qcloud.cos_migrate_tool.task.TaskExecutor.run(TaskExecutor.java:244)
at com.qcloud.cos_migrate_tool.app.App.main(App.java:135)
```
The reason is that the file "/dataseal/xx1/file1" to be migrated may be a soft link pointing to a resource in its parent directory. You can check with the following command:

```
[root@TENCENT64 /dataseal/cos_migrate_tool_v5-master/log]# ll /dataseal/xx1/file1
lrwxrwxrwx 1 xx xx xx xx   x xxxx /dataseal/xx1/file1 -> ../xx1/
```

As shown above, the soft link file "/dataseal/xx1/file1" points to "/dataseal/xx1/" in its parent directory, which causes an infinite loop in traversal. Therefore, the migration task is automatically terminated.
We recommend you delete such files in advance (note: the method of excluding such files in the configuration item `excludes` is invalid).

If other problems occur, try to run the migration tool again. If the problem persists, compress the configuration (with the key hidden) as well as the log directory and [contact us](https://intl.cloud.tencent.com/contact-sales).
