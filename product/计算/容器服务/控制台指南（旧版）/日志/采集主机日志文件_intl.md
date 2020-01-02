## File Log Collection

Log collection feature allows you to collect logs under the specified CVM paths on all nodes in the Kubernetes cluster. You can configure required paths in a flexible manner based on your own needs. Log collection Agent collects the file logs under the paths that meet the specified path rules on all nodes in the cluster. Collected log information is output to the specified output end in the format of json, and attached with specified metadata, including the path of source file and user-defined metadata.


## How to Configure

1. Create log collection rule
![](https://main.qcloudimg.com/raw/14a4a61458c68a2c36a0fcc0216404b0.png)

2. Specify source path and add custom Metadata (optional)
![][2]

3. Specify log receiver
![][3]

4. View received logs
![][4]

## Log Collection Path

Users can specify the path of a log file to collect the log file under the corresponding path on the node in the cluster. A file path or a path that contains wildcard is supported, for example, `/var/log/nginx.log` or `/var/lib/docker/containers/*/*.log`.


## Metadata 

Users can attach a specified Metadata in Key-Value format to collected logs as the Metadata tag for log information. Attached Metadata is added to the log record in the format of json field.

![][5]

For example, when no Metadata is attached, the collected data is
![][6]

When users attach a specified Metadata, the collected data is
![][7]

[1]:https://main.qcloudimg.com/raw/52dedcd3afa1713f42d4441c5261181c.png
[2]:https://main.qcloudimg.com/raw/b32ecb7a41a1e041d7f459e44c874f64.png
[3]:https://main.qcloudimg.com/raw/419f1eba946744cfa9c7b188e8877683.png
[4]:https://mc.qcloudimg.com/static/img/32f72a65f46f33d67a93d1a9a3f3e3d1/image.jpeg
[5]:https://main.qcloudimg.com/raw/0fd6c36b248acf0cdaf11ddfb21861aa.png
[6]:https://mc.qcloudimg.com/static/img/5386281fc3ed14c4f41ba723a23dc3ec/host-log-without-metadata.png
[7]:https://mc.qcloudimg.com/static/img/c571be8fbc995ab083c2676e3b10861f/host-log-with-metadata.png

Compared to the logs with no specified Metadata, json logs attached with Metadata have an additional key `service`.

## What is Log Metadata
Field Name | Meaning
--- | ---
path | Source file
message | Log information
Custom key | Custom value



