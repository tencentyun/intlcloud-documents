### What is Cloud Log Service?

Cloud Log Service (CLS) is Tencent Cloud’s one-stop log data service platform with the following features:

- Log collection: supports multiple access methods like LogListener, API, etc.
- Log storage: stores and manages log data centrally
- Search analysis: provides log query and filtering features
- Shipping and consumption: provides the log shipping/consumption features for further log data processing
- CLS integrates seamlessly with Tencent Cloud services.

### How does CLS define a log?

A complete CLS log contains mainly the log timestamp, the log content and the metadata:
- Log timestamp: the basic time attribute of logs
- Log content: contents in the format of key-value pairs
- Metadata: basic metadata such as the log source IP address, log source file path, etc.

### How long can logs be kept?

CLS provides log lifecycle management. When you create a logset, you may configure a storage cycle, beyond which the data will be cleared without incurring storage fees. If you need to extend the storage cycle, [submit a ticket](https://console.cloud.tencent.com/workorder/category).

After you ship logs to Cloud Object Storage (COS), the lifecycle management of the destination bucket, and the COS billing rules will be used.


### What are the differences between logset and log topic?

CLS provides two levels of conceptual logic: logset and log topic. A logset contains multiple log topics, similar to a project containing multiple application services. Generally, each service has different log formats. Therefore, a log topic is the smallest unit of configuration management such as collection and search.


### What are the differences between full-text index and key-value index?

- Full-text index: breaks a full log into segments by delimiter, and executes keyword query based on the segments.
- Key-value index: breaks a full log into key-value pairs according to the specifications, and executes field query based on the key-value pairs.


### Is CLS available for services not on Tencent Cloud?

Yes. CLS does not restrict log sources. Logs are collected to CLS provided that the log source is reachable to our server over the network.


### Can LogListener upload data to multiple log topics?

Yes, provided that these log topics are in the same region.

### 服务器更换 IP 地址后，Loglistener 应该如何适配？
- 若服务器通过机器标识绑定机器组，用户无需变更 Loglistener 配置。若服务器 IP 需要频繁变更，建议用户使用机器标识配置机器组。单击 [了解详情](https://intl.cloud.tencent.com/document/product/614/17412)。
- 若服务器通过 IP 地址绑定机器组，用户需要完成以下配置变更：
 2. Log in to the target server and modify the `/etc/loglistener.conf` file in the Loglistener installation directory (`/user/local` in this example):
```go
vi /usr/local/loglistener-2.3.0/etc/loglistener.conf
```
 2. Press **i** to enter the edit mode.
 3. 修改配置文件中 group_ip 部分，填入变更后的 IP 地址。
 5. Press **Esc**, enter **:wq** and press **Enter** to save and close the file.
 In the installation directory, run the following command to restart LogListener.
```go
 /etc/init.d/loglistenerd restart
```
 6. 登录 [日志服务控制台](https://console.cloud.tencent.com/cls/overview?region=ap-guangzhou)，在左侧导航栏中，单击【机器组管理】，修改该服务器绑定的机器组配置，使用新 IP 替换原机器 IP 地址，单机【确定】。
