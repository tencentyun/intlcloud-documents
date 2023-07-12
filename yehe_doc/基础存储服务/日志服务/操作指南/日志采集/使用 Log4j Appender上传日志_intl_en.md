## Overview
CLS allows you to upload logs to CLS by using Log4j Appender.

## Background

Log4j Appender is an open source project of Apache. It allows you to deliver logs to various destinations, including consoles, files, GUI components, and even socket servers, NT event loggers, and UNIX Syslog daemons. You can control the output format of each log. By defining the level of each log, you can further control the log generation process. In addition, you can have the flexibility to configure the logging behavior by editing a configuration file without modifying the application code.

Log4j Appender consists of the following components:
- **Log information priority**
From high to low, log message priorities are ERROR, WARN, INFO, and DEBUG, which specify the importance of log messages.
- **Log information output destination**
The output destination of a log specifies whether the log will be printed to the console or to a file.
- **Log information output format**
The output format determines how log information is displayed.

## Advantages

- Logs are not stored on disks: generated log data is delivered to servers via the network.
- No reconstruction is required: for applications that are using Log4j Appender, you only need to perform simple configuration to enable log collection.
- Logs are delivered in async non-blocking mode: the high concurrency and backend async delivery design make Logback ideal for high write concurrency.
- Resources are controllable: you can use parameters to control the size of the memory used by the producer to cache data to be sent and the number of threads used to execute data sending tasks.
- Automatic retries: you can configure the number of retries for exceptions that allow retries.
- Graceful shutdown: Log4j Appender will deliver logs in full mode before exiting.
- Log reporting result response: exceptions that occur during running are recorded via `org.apache.log4j.helpers.LogLog` and, by default, will be output to the console.

## Using Tencent CLS Log4j Appender

With Tencent CLS Log4j Appender, you can specify that logs are output to Tencent Cloud CLS in the format as shown in the figure below.
![](https://qcloudimg.tencent-cloud.cn/raw/06fdc826031941433b89c64e7fd505c9.png)

| Field | Description |
|---------|---------|
| \_\_SOURCE\_\_ | Source IP |
| \_\_FILENAME\_\_ | File name |
| level | Log level |
| location | Code location of the log print statement |
| message | Log content |
| throwable | Log exception information (This field exists only when exception information is logged.) |
| thread | Thread name |
| time | Log print time (You can print the format and time zone via `timeFormat` and `timeZone` respectively.) |
| log | Custom log format |

	
## Project Introduction and Configuration

### Introducing dependencies into a Maven project

```
<dependency>
    <groupId>com.tencentcloudapi.cls</groupId>
    <artifactId>tencentcloud-cls-log4j-appender</artifactId>
    <version>1.0.2</version>
</dependency>
```

### Modifying the Log4j configuration file

```
#loghubAppender
log4j.appender.loghubAppender=com.tencentcloudapi.cls.LoghubAppender
# CLS HTTP address. Required.
log4j.appender.loghubAppender.endpoint=ap-guangzhou.cls.tencentcs.com
# User ID. Required.
log4j.appender.loghubAppender.accessKeyId=
log4j.appender.loghubAppender.accessKeySecret=
# `log` field format. Required.
log4j.appender.loghubAppender.layout=org.apache.log4j.PatternLayout
log4j.appender.loghubAppender.layout.ConversionPattern=%-4r [%t] %-5p %c %x - %m%n
# Log topic. Required.
log4j.appender.loghubAppender.topicID =
# Log source. Optional.
log4j.appender.loghubAppender.source =
# Maximum size of logs cached by a single Producer instance. The default value is 100 MB.
log4j.appender.loghubAppender.totalSizeInBytes=104857600
# Maximum time for blocking a caller from using the `send` method if the Producer has insufficient free space. The default value is 60 seconds. It is strongly recommended that this value be set to 0 in order not to block the log print thread.
log4j.appender.loghubAppender.maxBlockMs=0
# Size of the thread pool for executing log sending tasks. The default value is the number of available processors.
log4j.appender.loghubAppender.sendThreadCount=8
# When the size of logs cached in ProducerBatch is greater than or equal to `batchSizeThresholdInBytes`, the batch will be sent. The default value is 512 KB, and the maximum value can be set to 5 MB.
log4j.appender.loghubAppender.batchSizeThresholdInBytes=524288
# When the number of logs cached in ProducerBatch is greater than or equal to `batchCountThreshold`, the batch will be sent. The default value is 4096, and the maximum value allowed is 40960.
log4j.appender.loghubAppender.batchCountThreshold=4096
# Linger time of a ProducerBatch from creation to sending. The default value is 2 seconds, and the minimum value allowed is 100 milliseconds.
log4j.appender.loghubAppender.lingerMs=2000
# Number of retries that a ProducerBatch can be retries if it fails to be sent for the first time. The default value is 10 retries.
# If `retries` is less than or equal to 0, the ProducerBatch directly enters the failure queue when it fails to be sent for the first time.
log4j.appender.loghubAppender.retries=10
# A larger parameter value allows you to trace more information, but it also consumes more memory.
log4j.appender.loghubAppender.maxReservedAttempts=11
# Backoff time for the first retry. The default value is 100 milliseconds.
# The Producer adopts an exponential backoff algorithm. The scheduled wait time for the Nth retry is baseRetryBackoffMs * 2^(N-1).
log4j.appender.loghubAppender.baseRetryBackoffMs=100
# Maximum backoff time for retries. The default value is 50 seconds.
log4j.appender.loghubAppender.maxRetryBackoffMs=50000
# Time format. Optional.
log4j.appender.loghubAppender.timeFormat=yyyy-MM-dd'T'HH:mm:ssZ
# Set the time zone to the UTC+08:00 time zone. Optional.
log4j.appender.loghubAppender.timeZone=Asia/Shanghai
# Output DEBUG and higher level messages
log4j.appender.loghubAppender.Threshold=DEBUG
```

## Log4j Appender SDK

- Log4j 1.x: please use [tencentcloud-cls-log4j-appender](https://github.com/TencentCloud/tencentcloud-cls-log4j-appender).
- Log4j 2.x: please use [tencentcloud-cls-log4j2-appender](https://github.com/TencentCloud/tencentcloud-cls-log4j2-appender).


