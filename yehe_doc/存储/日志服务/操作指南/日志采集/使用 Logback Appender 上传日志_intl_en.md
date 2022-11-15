## Overview

Currently, CLS allows you to upload logs to CLS by using Logback Appender.

## Background

Logback is an open source project of Apache. Logback allows you to deliver logs to various destinations, including consoles, files, GUI components, and even socket servers, NT event loggers, and UNIX Syslog daemons. In addition, you can have the flexibility to configure the logging behavior by editing a configuration file without modifying the application code.

## Advantages

- Logs are not stored on disks: generated log data is delivered to servers via the network.
- No reconstruction is required: for applications that are using Logback, you only need to perform simple configuration to enable log collection.
- Logs are delivered in async non-blocking mode: the high concurrency and backend async delivery design make Logback ideal for high write concurrency.
- Resources are controllable: you can use parameters to control the size of the memory used by the producer to cache data to be sent and the number of threads used to execute data sending tasks.
- Automatic retries: you can configure the number of retries for exceptions that allow retries.
- Graceful shutdown: Logback will deliver logs in full mode before exiting.
- Log reporting result response: exceptions that occur during Logback running are output via `addError`.


## Project Introduction and Configuration

### Introducing dependencies into a Maven project

```
<dependency>
    <groupId>com.tencentcloudapi.cls</groupId>
    <artifactId>tencentcloud-cls-logback-appender</artifactId>
    <version>1.0.3</version>
</dependency>
```

### Modifying the Logback configuration file
```
  <appender name="LoghubAppender" class="com.tencentcloudapi.cls.LoghubAppender">
        <!--Required-->
        <endpoint><region>.cls.tencentcs.com</endpoint>
        <accessKeyId>${SecretID}</SecretID>
        <accessKeySecret>${SecretKey}</SecretKey>
        <topicId>${topicId}</topicId>

        <!-- Optional. For details, see 'Parameter description'-->
        <totalSizeInBytes>104857600</totalSizeInBytes>
        <maxBlockMs>0</maxBlockMs>
        <sendThreadCount>8</sendThreadCount>
        <batchSizeThresholdInBytes>524288</batchSizeThresholdInBytes>
        <batchCountThreshold>4096</batchCountThreshold>
        <lingerMs>2000</lingerMs>
        <retries>10</retries>
        <baseRetryBackoffMs>100</baseRetryBackoffMs>
        <maxRetryBackoffMs>50000</maxRetryBackoffMs>

        <!-- Optional. Set the time format -->
        <timeFormat>yyyy-MM-dd'T'HH:mm:ssZ</timeFormat>
        <timeZone>Asia/Shanghai</timeZone>
        <encoder>
            <pattern>%d{HH:mm:ss.SSS} [%thread] %-5level %logger - %msg</pattern>
        </encoder>
        <mdcFields>THREAD_ID,MDC_KEY</mdcFields>
  </appender>
```

## Logback Appender SDK

Please use [tencentcloud-cls-logback-appender](https://github.com/TencentCloud/tencentcloud-cls-logback-appender).



