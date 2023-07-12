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
>! It may take a period of time for CLS to clear expired data, during which no charges will apply.

### What are the differences between logset and log topic?

CLS provides two levels of conceptual logic: logset and log topic. A logset contains multiple log topics, similar to a project containing multiple application services. Generally, each service has different log formats. Therefore, a log topic is the smallest unit of configuration management such as collection and search.


### What are the differences between full-text index and key-value index?

- Full-text index: breaks a full log into segments by delimiter, and executes keyword query based on the segments.
- Key-value index: breaks a full log into key-value pairs according to the specifications, and executes field query based on the key-value pairs.


### Is CLS available for services not on Tencent Cloud?

Yes. CLS does not restrict log sources. Logs are collected to CLS provided that the log source is reachable to our server over the network.


### How do I modify the LogListener configuration after the server IP address is changed?
 - If the server is bound to the machine group by machine ID, there is no need to modify the LogListener configuration. This method is recommended when the server IP frequently changes. For more information, see [Machine Group Management]( https://intl.cloud.tencent.com/document/product/614/17412).
 - If the server is bound to the machine group by IP address, modify the configuration as follows:
i. Modify the /etc/loglistener.conf file in the LogListener installation directory (/user/local in this example).
vi /usr/local/loglistener-2.3.0/etc/loglistener.conf
ii. Press **i** to enter the edit mode.
iii. Enter the new IP address in the group_ip section of the configuration file.
iv. Press **Esc**, enter **:wq**, and press **Enter** to save and exit the editor.
v. Run the following command to restart LogListener.
/etc/init.d/loglistenerd restart
vi. Log in to the [CLS console](https://console.cloud.tencent.com/cls) and click **Machine Group Management** on the left sidebar. Locate the machine group to which the server binds and click **Edit**. In the pop-up window, replace the old IP address with the new one, and click **OK**.
