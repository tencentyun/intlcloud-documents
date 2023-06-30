
## Log Collection FAQs
### Why can’t I view the logs in CLS console after configuring log collection for the cluster?

If the log cannot be viewed or is missing, please check whether the following problems exist:
- **Check whether you have enabled the index for the selected log topic**. Index configuration is required for CLS log search and analysis. If it is not enabled, you cannot view the logs. For how to configure index, see [Configuring Index](https://intl.cloud.tencent.com/document/product/614/39594).
![](https://main.qcloudimg.com/raw/24657347b0f56ae264228bd8a84d70e6.png)
- **Whether the log, audit, and event use the same topic**. If they use the same topic, the logs will be overwritten, resulting in log missing.
- **Whether the selected topic uses two extraction modes**. The new extraction mode will overwrite the legacy one.
- **Whether there is a soft link**. If the collection type is selected as "Container File Path", the corresponding path cannot be a soft link. Otherwise, the actual path of the soft link will not exist in the collector's container, resulting in log collection failure.
- If you use environment variables to enable EKS log collection and select role as the authorization method, **you need to select the CVM as the role entity when creating a role**. For more information, see [EKS Log Collection](https://intl.cloud.tencent.com/document/product/457/37907).

If the problem persists, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=350&source=0&data_title=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1TKE&step=1) to contact us.



### Where can I view the logs after configuring the log rules?
1. Log in to the [CLS console](https://console.cloud.tencent.com/cls/overview?region=ap-guangzhou) and select **Search and Analysis** in the left sidebar.
2. In the **Search and Analysis** page, select the region, log set, and log topic to view logs, enable full-text index to search and analyze logs, as shown below:
![](https://main.qcloudimg.com/raw/9f55654545252904f81d5e6c2060f045.png)


## Using Environment Variables to Enable EKS Log Collection

### How do Java applications implement multi-line log merging?

When the log data of the application occupies multiple lines (such as the Java program log), the line break `\n` cannot be used to mark the end of a log. To help the CLS to clearly distinguish each log, it is necessary to configure a configmap with the first-line regular expression. When a log in a line matches the preset regular expression, it is considered as the beginning of a log, and the next matching line will be the end mark of the log. For more information, see [Implementing Multi-line Log Merging for EKS Log Collection](https://intl.cloud.tencent.com/document/product/457/40216).


### How to adjust the log collection configuration to adapt to different log output rates?

When you use environment variables to enable EKS log collection, EKS will start up a log collection component in the Pod sandbox to collect and report logs. Since EKS limits the memory usage of the log collection component, when the log output rate is too high, the log collection component may be Out of Memory (OOM). At this time, you can adjust the log collection configuration as needed. The specific method is to manually modify the following Pod annotation to reduce the memory buffer used by the log collection component to reduce the memory usage.
```
internal.eks.tke.cloud.tencent.com/tail-buffer-chunk-size: "2M"
internal.eks.tke.cloud.tencent.com/tail-buffer-max-size: "2M"
```

The descriptions of the annotations are shown in the following table. For more information, see [Fluent Bit](https://docs.fluentbit.io/manual/administration/configuring-fluent-bit/unit-sizes).

| Parameter | Description | Default Value |
|---------|---------|---------|
| Buffer_Chunk_Size | It is used to set the initial buffer size to collect container file logs. It can also be used to increase buffer size. | 2M |
| Buffer_Max_Size | It is used to set the limit of the buffer size of each monitored file. When the buffer needs to be increased (such as long logs), this value can limit the amount of buffer increased. If the read file exceeds this limit, the file will be deleted from the monitoring list. | 2M |


### What is the standard for outputting the logs of the application in the container of the EKS cluster?

When the application outputs logs, the logs should be output to stdout. If the program logs are output to the container file, you need to clean up the log file regularly, or mount the volume for persistent storage; otherwise, the 20G temporary storage will be used up. For more information, see [Pod Temporary Storage](https://intl.cloud.tencent.com/document/product/457/34050).

If you do not know how to clean up the log files, we recommend the following methods:
- Mount volume for persistent storage. For more information, see [Storage Management](https://intl.cloud.tencent.com/document/product/457/37769).
- Enable EKS log collection. For more information, see [EKS Log Collection](https://intl.cloud.tencent.com/document/product/457/37907).
