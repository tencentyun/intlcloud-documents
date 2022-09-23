
## Overview
In EKS, you can [use environment variables to configure log collection](https://intl.cloud.tencent.com/document/product/457/37907), or use custom resource definitions (CRD) to configure log collection.

CRD is non-intrusive to Pod and supports single-line, multi-line, separator, full regex, JSON and other log parsing methods. It sends standard output and file logs in the container to [Tencent Cloud CLS](https://intl.cloud.tencent.com/product/cls), which provides various services such as search and analysis, visualization applications, log download and consumption. **It is recommended to use CRD to configure log collection.**


<dx-alert infotype="notice" title="">
<li>Using CRD to configure log collection is currently only valid for Pods created after May 25, 2021. If you need to use CRD to configure log collection for the Pods created before, please terminate the Pod and recreate one.</li>
<li>If the Pods are configured with environment variables and CRD to collect logs at the same time, it will cause repeated collection and repeated billing. Therefore, when using CRD to configure log collection, please delete the relevant environment variables.</li>
</dx-alert>


## Concepts

- **Log rule**: users can use log rules to specify the log collection source, log consumer end, and log parsing method, configure filters, and upload the log that failed to parse etc. The log collector will monitor the changes of the log collection rules, and the changed rules will take effect within 10 seconds.
- **Log source**: includes the standard output of the specified container and the files in the container.
  - When collecting container standard output logs, users can select TKE logs in all containers or specified workloads and specified Pod labels as the log collection source.
  - When collecting container file path logs, users can specify container file path logs in workloads or Pod labels as the collection source.
- **Consumer**: users can select the logsets and log topics of the CLS as the consumer end.
- **Extraction mode**: the log collection agent supports the delivery of collected logs to the user-specified log topic in the format of single-line text, JSON, separator-based text, multi-line text, or full regex.
- **Filter**: after filter is enabled, logs will be collected according to the specified rules. "key" supports full matching and the rule supports regex matching. For example, you can set to collect logs containing "ErrorCode = 404".
- **Upload the log that failed to parse**: after this feature is enabled, all logs that failed to parse (as the “Key”), and the original log content (as the “Value”) are uploaded. When this feature is disabled, the logs that failed to parse will be discarded.




## Directions



### Authorization on first use[](id:role)
When using the log collection feature of the EKS cluster for the first time, you need to authorize the CLS and other related permissions to ensure that the logs are normally uploaded to the CLS.
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2/cluster?rid=4), and select **Cluster OPS** > **[Feature Management](https://console.cloud.tencent.com/tke2/ops/list?rid=1)** in the left sidebar.
2. At the top of the **Feature Management** page, select the region and **Elastic Cluster**. On the right side of the cluster for which you want to enable log collection, click **Set**, as shown in the figure below:
![](https://main.qcloudimg.com/raw/3f0743029e71e20e4f3b3bfdd7045bab.png)
3. On the **Configure Features** page, click **CAM** to complete authorization.
After authorization is completed, the role TKE_QCSLinkedRoleInEKSLog will be bound to your account by default, and the default policy configured for this role is QcloudAccessForTKELinkedRoleInEKSLog.

>?You only need to authorize when you use the log collection feature for the first time. If you delete the above roles, you need to authorize again.



### Enabling log collection[](id:open)

After completing the authorization, you can enable the log collection.

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2/cluster?rid=4), and select **Cluster OPS** > **[Feature Management](https://console.cloud.tencent.com/tke2/ops/list?rid=1)** in the left sidebar.
2. At the top of the **Feature Management** page, select the region and **Elastic Cluster**. On the right side of the cluster for which you want to enable log collection, click **Set**, as shown in the figure below:
![](https://main.qcloudimg.com/raw/3f0743029e71e20e4f3b3bfdd7045bab.png)
3. On the "Configure Features" page, click **Edit** for log collection, enable log collection, and confirm this operation, as shown in the figure below:
![](https://main.qcloudimg.com/raw/9c1a88b996982ab6112f9032bfa15040.png)




## Subsequent Operations
After enabling the log collection feature, you can refer to the following operations to use the CDR to configure the log collection for the EKS cluster:
- [Configuring Log Collection via the Console](https://intl.cloud.tencent.com/document/product/457/40585)
- [Configuring Log Collection via Yaml](https://intl.cloud.tencent.com/document/product/457/40951)



## FAQ
If you have problems, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=350&source=0&data_title=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1TKE&step=1) to contact us.




