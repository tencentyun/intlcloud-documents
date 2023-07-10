## Overview

This document describes how to use Winlogbeat or Filebeat to collect and upload Windows logs to CLS.

## Prerequisites

- You have activated CLS and created relevant resources such as logset and log topic.
- You have obtained the `SecretId` and `SecretKey` in the [Tencent Cloud console](https://console.cloud.tencent.com/cam/capi).

## Directions


### Using Winlogbeat to collect and upload Windows event logs to CLS

#### Installing Winlogbeat

1. Download the target Winlogbeat version at the official website.
This document takes Winlogbeat 7.6.2 as an example, which can be downloaded [here](https://www.elastic.co/cn/downloads/past-releases/winlogbeat-7-6-2).
2. Decompress the downloaded package to the C drive.
We recommend you create a `winlogbeat` folder under the `Program Files` directory for decompression.
3. Open PowerShell as the admin and run the following command:
```
cd C:\Program Files
cd .\winlogbeat-7.6.2-windows-x86_64
.\install-service-winlogbeat.ps1
```
During execution, if an error is reported, enter the `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned` command and select `y`. Then, enter the above command again.

![](https://qcloudimg.tencent-cloud.cn/raw/68fa77d15c4198ce73f3b68bc543f041.png)
4. Run the following command to test whether the environment is normal.
```
.\winlogbeat.exe test config -c .\winlogbeat.yml -e
```
If `config OK` is returned, the environment is normal.
5. Run the following command to start the program.
```
Start-Service winlogbeat
```

#### Uploading logs to CLS

In the `winlogbeat.yml` file in `C:\Program Files\Winlogbeat`, change `output.kafka` to the following to send logs to CLS.
```
output.kafka:
  enabled: true
  hosts: ["${region}-producer.cls.tencentyun.com:9095"] # TODO: Service address. The public network port is 9096, and the private network port is 9095.
  topic: "${topicID}" #  TODO: Topic ID
  version: "0.11.0.2"
  compression: "${compress}"   # Configure the compression method. Valid values: `gzip`, `snappy`, `lz4`.
  username: "${logsetID}"
  password: "${SecurityId}#${SecurityKey}"
```

| Parameter | Description |
|---------|---------|
| LinkType | Currently, SASL_PLAINTEXT is supported. |
| hosts | Address of the initially connected cluster. For more information, see [Service Entries](#hosts). |
| topic | Log topic ID, such as 76c63473-c496-466b-XXXX-XXXXXXXXXXXX. |
| username | Logset ID, such as 0f8e4b82-8adb-47b1-XXXX-XXXXXXXXXXXX. |
| password | Password in the format of `${SecurityId}#${SecurityKey}`, such as XXXXXXXXXXXXXX#YYYYYYYY. |

### Using Filebeat to collect Windows file logs

#### Installing Filebeat

1. Download the target version [here](https://www.elastic.co/cn/downloads/past-releases#filebeat).
2. Upload and decompress the installation package to the root directory of a drive on the Windows server.
3. Edit the `filebeat.yml` file.
>? Use "/" rather than "\" in paths.
>
4. Find the target log path and edit the module configuration file (with mssql as an example below).
```
# Module: mssql
# Docs: https://www.elastic.co/guide/en/beats/filebeat/7.3/filebeat-module-mssql.html

- module: mssql
  # Fileset for native deployment
  log:
    enabled: true

    # Set custom paths for the log files. If left empty,
    # Filebeat will choose the paths depending on your OS.
    var.paths: ["D:/Program Files/Microsoft SQL Server/MSSQL10_50.MSSQLSERVER/MSSQL/Log/ERROR*"]
```
5. Open PowerShell as the admin and run the following command:
```
# Enter the specific Filebeat path
cd c:/filebeat

# Run the installation script to install Filebeat
.\install-service-filebeat.ps1

# Start the mssql module
.\filebeat.exe modules enable mssql

# Install the template file
.\filebeat.exe setup -e

# Start Filebeat
start-service filebeat
```

#### Uploading logs to CLS

In the `filebeat.yml` file, change `output.kafka` to the following to send logs to CLS:

```
output.kafka:
  enabled: true
  hosts: ["${region}-producer.cls.tencentyun.com:9095"] # TODO: Service address. The public network port is 9096, and the private network port is 9095.
  topic: "${topicID}" #  TODO: Topic ID
  version: "0.11.0.2"
  compression: "${compress}"   # Configure the compression method. Valid values: `gzip`, `snappy`, `lz4`.
  username: "${logsetID}"
  password: "${SecurityId}#${SecurityKey}"
```

| Parameter | Description |
|---------|---------|
| LinkType | Currently, SASL_PLAINTEXT is supported. |
| hosts | Address of the initially connected cluster. For more information, see [Service Entries](#hosts). |
| topic | Log topic ID, such as 76c63473-c496-466b-XXXX-XXXXXXXXXXXX. |
| username | Logset ID, such as 0f8e4b82-8adb-47b1-XXXX-XXXXXXXXXXXX. |
| password | Password in the format of `${SecurityId}#${SecurityKey}`, such as XXXXXXXXXXXXXX#YYYYYYYY. |

<span id="hosts"></span>
## Service Entries 

<table>
	<tr><th>Region</th><th>Network Type</th><th>Port Number</th><th>Service Entry</th></tr>
	<tr><td rowspan=2>Guangzhou</td><td>Private network</td><td>9095</td><td>gz-producer.cls.tencentyun.com:<b>9095</b></td></tr>
	<tr><td>Public network</td><td>9096</td><td>gz-producer.cls.tencentcs.com:<b>9096</b></td></tr>
</table>

>! This document uses the Guangzhou region as an example. The private and public domain names are identified by different ports. For other regions, replace the address prefixes. For more information, see [here](https://intl.cloud.tencent.com/document/product/614/18940).
>
