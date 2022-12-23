## Overview

msp-agent is a data migration tool. You can deploy it on a server in your data center or Tencent Cloud. Then, it can execute semi-managed migration tasks created in the MSP console to migrate cloud storage data to COS with ease.

## Features

- Migration from all the source vendors supported in the console.
- Easy-to-deploy distributed master-worker architecture for efficient migration of a high volume of data.
- Checkpoint restart.
- Traffic control.

## Runtime Environment
Linux

## System Deployment Method

### Installation
Download and decompress the [msp-agent installation package](https://msp-agent-1258344699.cos.ap-beijing.myqcloud.com/msp-agent-latest.zip). Below is the directory structure after decompression:
![](https://qcloudimg.tencent-cloud.cn/raw/f208f788bb8d20cbc192e02b73460ead.png)
>?
>- msp-agent adopts the distributed master-worker architecture, where one master can connect to one or multiple workers.
>- The master directory is `master`, and the worker directory is `worker`.
>- To deploy multiple workers, copy the entire `worker` directory, modify relevant parameters, and start the workers as follows:
>- You can start multiple worker processes on a single server. However, you need to modify relevant parameters as detailed below to avoid port conflicts.

### Startup

- Start the master:
cd {path-to-msp-agent}/master && ./bin/start.sh

- Start a worker:
cd {path-to-msp-agent}/worker && ./bin/start.sh

### Configuration parameter description

Both the `master` and `worker` directories have the same `configs` structure:
![](https://qcloudimg.tencent-cloud.cn/raw/6e6e0a1baf256531101e627e491cf8df.png)

Here, `pl_config.yaml` configures main parameters for process execution, `app_logger_config.yaml` configures the application execution log format, and `query_logger_config.yaml` configures the master-worker RPC communication log format.

#### Log configuration

You can basically use the default log parameter settings. However, be careful about the log rotation configuration: if the disk space is limited but the task size is large, you need to adjust the log configuration to reduce the disk usage (during migration, the disk is used to store only storage logs but not migrated files).

![](https://staticintl.cloudcachetci.com/yehe/backend-news/CYQa700_28.png)             

#### Master configuration

| Parameter | Definition | Description |
| ------------------ | -------------------------------- | ------------------------------------------------------------ |
| "*.*.*.*.gRPCPort" | gRPC port for listening on the master               | This parameter specifies the port used to receive the information reported by workers. This port must be opened to worker servers on the master server. |
| failFilePartSize   | Part size of a failed file       | This parameter specifies the part size of a failed file, which is 10,485,760 bytes by default. The product of this value multiplied by 10,000 is the maximum size of failed files, i.e., 100 GB. If there are both high numbers of files to be migrated and failed files, for example, more than 200 million files, you can increase this value appropriately. |
| fragMaxSize        | Fragment size of an assigned task     | To reduce the pressure on master-worker communication, the master packages multiple file paths into a **fragment** and assigns it to a worker as a subtask. `fragMaxSize` is the maximum size of files in each fragment in bytes. If the value is too small, the pressure on master-worker communication will get higher, and server resources will be wasted; if it is too large, workers will become too slow to report the completion of fragment migration and have imbalanced loads. The default value is 10737418240, i.e., 100 GB. When `fragMaxSize` or `fragMaxNum` reaches the limit during packaging, the system will stop adding more files. |
| fragMaxNum         | Maximum number of files of an assigned task fragment     | To reduce the pressure on master-worker communication, the master packages multiple file paths into a **fragment** and assigns it to a worker as a subtask. `fragMaxNum` is the maximum number of files in each fragment. If the value is too small, the pressure on master-worker communication will get higher, and server resources will be wasted; if it is too large, workers will become too slow to report the completion of fragment migration and have imbalanced loads. The default value is 1,000. When `fragMaxSize` or `fragMaxNum` reaches the limit during packaging, the system will stop adding more files. |
| secretId           | The `SecretId` used to request TencentCloud APIs for MSP   | As the master process needs to request TencentCloud APIs for MSP to get the tasks created in the console, you need to enter the `secretId` of your key. **Note that the key here refers to your key used to create MSP tasks, not the keys of source and target buckets.** |
| secretKey          | The `SecretKey` used to request TencentCloud APIs for MSP   | As the master process needs to request TencentCloud APIs for MSP to get the tasks created in the console, you need to enter the `secretKey` of your key. **Note that the key here refers to your key used to create MSP tasks, not the keys of source and target buckets.** |
| listerIp           | Private IP of the server where the master process is deployed     | You may create multiple tasks and want to run them in different clusters. In this case, you need to enter the private IP of the server where the master process is deployed, so that the master will run only tasks whose **master node private IP** is set to this IP during task creation in the console.  |



#### Worker configuration

| Parameter | Definition | Description |
| ------------------------------ | ------------------------ | ------------------------------------------------------------ |
| "*.*.*.*.gRPCPort"             | gRPC port for listening on the worker       | This parameter specifies the port used to receive the scheduling information from the master. This port must be opened to the master server on the worker server. If multiple worker processes run on a single server, you need to change this parameter to a value different from that of other workers, so as to avoid process startup failure due to port conflicts. |
| fileMigrateTryTimes            | Number of retries                 | This parameter specifies the maximum number of retries after a file fails.                                     |
| goroutineConcurrentNum         | Number of concurrent coroutines               | This parameter specifies the number of concurrent coroutines, i.e., the number of files to be migrated concurrently. The value is subject to two factors: server configuration and average file size. The more the server CPU cores, the greater the value can be set. The larger the average file size, the smaller the value can be set. As a small number of concurrent coroutines can lead to a high bandwidth usage, if the average file size is small, you should add more concurrent coroutines to increase the overall bandwidth.   |
| baseWorkerMaxConcurrentFileNum | Queue of cached files to be migrated     | To improve the assignment efficiency of distributed tasks, each worker caches a certain number of file fragments to be migrated. If the files to be migrated are small ( that is, the migration QPS is high), you can increase this value to make workers less hungry during consumption. However, the larger the cache, the more the status data that the master needs to store, which will increase the master load and instability. Therefore, you should choose an appropriate value. |
| partSize                       | Part size                 | This parameter specifies the default part size for multipart upload during large file migration.                         |
| downloadPartTimeout            | Download timeout period             | This parameter specifies the file download timeout period in seconds.                                 |
| uploadPartTimeout              | Upload timeout period             | This parameter specifies the file upload timeout period in seconds.                                 |
| perHostMaxIdle                 | HTTP client concurrency      | This parameter specifies the connection pool size per host and generally should be set to the same value as `goroutineConcurrentNum`. |
| addr                           | Private network communication address of the master | This parameter specifies the master communication address of workers, so that workers will register with the master to form a cluster. For example, if the master's `listerIp` is `10.0.0.1`, and the gRPC port to be listened on in the master configuration is `22011`, then set `addr` to `10.0.0.1:22011`. |
| sample                         | Whether to perform spot check           | The overview section describes the cases of data consistency check after migration. If source files don't have a Content-MD5 or CRC-64 checksum, they cannot be directly checked for data consistency. In this case, you can only perform spot check to reduce their probability of inconsistency. If this parameter is set to `true`, spot check will be performed on such files. |
| sampleTimes                    | Number of sampled fragments per file       | This parameter specifies the number of sampled fragments of a single file. Each sampled fragment will add one download request and increase the download traffic usage.  |
| sampleByte                     | Sampled fragment size in bytes           | This parameter specifies the size of each sampled fragment. The greater the value, the higher the sampling bandwidth.           |

