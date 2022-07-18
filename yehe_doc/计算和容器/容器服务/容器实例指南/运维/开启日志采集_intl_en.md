## Overview

EKSCI provides log collection capability and supports sending the standard output logs and file logs of the containers in the cluster to [CLS](https://intl.cloud.tencent.com/zh/product/cls). It is applicable for uses who want to store and analyze the service logs in EKSCI.

## Prerequisites

- Prepare a log topic of CLS to be used as the log reporting terminal. You can view and search the logs under the log topic after reporting the logs. If there is no appropriate log topic, see [Creating Logset and Log Topic](https://intl.cloud.tencent.com/document/product/614/31592).
- Enable the **Log Index** for the selected log topic. Index configuration is required for CLS log search and analysis. If it is not enabled, you cannot view and search the logs. For how to configure index, see [Configuring Index](https://intl.cloud.tencent.com/zh/document/product/614/39594). 
  You can go to the **[CLS console](https://console.cloud.tencent.com/cls/topic?region=ap-guangzhou) > Log Topic** page, select a log topic name, and enable the index in the **Index Configuration** tab, as shown in the figure below:
	![](https://qcloudimg.tencent-cloud.cn/raw/b60bf3dae63e22f16154e703f98b0572.png)

## Directions

### Enabling log collection when creating a container instance

>?You need to enable log collection when creating the container instance.

1. Log in to the TKE console. Click **Create Instance**.
2. Set the parameters of the container instance based on actual needs. Click **Next**.
3. Enable log collection on **Other Configurations** page.
	Authorization is required when the log collection feature is enabled for the first time. The role TKE_QCSLinkedRoleInEKSLog will be bound to your account by default, and the default policy configured for this role is QcloudAccessForTKELinkedRoleInEKSLog. The role will have permissions such as log uploading. Select the following parameters after the feature is enabled:
	- Select the logset and log topic.
	- Select the container and configure the collection path. It supports "stdout" (indicating standard output) and absolute path, and supports `*`. If there are more than one collection path, separate them with `,`.


<dx-alert infotype="notice" title="">
If role authorization capability is required when enabling log collection feature, the role bound to the instance must have write permission of "cls:pushLog". For details, see [Creating a Container Instance](https://www.tencentcloud.com/document/product/457/47857#.E5.88.9B.E5.BB.BA.E5.AE.B9.E5.99.A8.E5.AE.9E.E4.BE.8B). Only one role can be bound to the container instance.
</dx-alert>

​		


### Viewing the collected logs

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls) and click **Search and Analysis** in the left sidebar.
2. On the **Search and Analysis** page, select the region, log set, and log topic to view logs, enable full-text index to search and analyze logs, as shown in the figure below:![](https://qcloudimg.tencent-cloud.cn/raw/1c0ff923d5531d8da9a8fa867432c199.png)

## FAQs

### What can I do if logs are not displayed?

If you confirm that you have reported logs but they are not displayed, please check the following:
1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/role) to check if there is a TKE_QCSLinkedRoleInEKSLog role.
2. Check if full-text index has been enabled for the log topic.
3. If role authorization has been enabled, check if the role bound to the container instance has the permission to report logs. For specific configuration, see "Role Authorization".
4. Check if the entity selected for the role bound to the instance is CVM.

If the problem persists, please [submit a ticket](https://console.intl.cloud.tencent.com/workorder) to contact us.
