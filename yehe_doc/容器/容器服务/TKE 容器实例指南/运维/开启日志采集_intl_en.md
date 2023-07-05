## Scenarios

EKSCI provides log collection capability and supports sending the standard output logs and file logs of the containers in the cluster to [CLS](https://www.tencentcloud.com/products/cls). It is applicable for uses who want to store and analyze the service logs in EKSCI.

## Prerequisites
 Prepare a log topic of CLS to be used as the log reporting terminal. You can view and search the logs under the log topic after reporting the logs. If there is no appropriate log topic, see [Creating a log topic](https://intl.cloud.tencent.com/document/product/614/31592).

## How It Works

### Enabling log collection when creating a container instance

>?You need to enable log collection when creating the container instance.

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2/eksci). Click **Create Instance**.
2. Configure the parameters of the container instance based on actual needs. For more information, see [Creating a Container Instance](https://intl.cloud.tencent.com/document/product/457/47857). After configuration, click **Next**.
3. Enable log collection on the**Other Configurations** page.
Authorization is required when the log collection feature is enabled for the first time. The role TKE_QCSLinkedRoleInEKSLog will be bound to your account by default, and the default policy configured for this role is QcloudAccessForTKELinkedRoleInEKSLog. The role will have permissions such as log uploading. Select the following parameters after the feature is enabled:

	- Select the logset and log topic.
	- Select the container and configure the collection path. It supports "stdout" (indicating standard output) and absolute path, and supports `*`. If there are more than one collection path, separate them with `,`.
<dx-alert infotype="notice" title="">
If role authorization capability is required when enabling log collection, the role bound to the instance must have the write permission on "cls:pushLog". For more information, see [here](https://intl.cloud.tencent.com/document/product/457/47857). Only one role can be bound to a container instance.
</dx-alert>

		


### Viewing the collected logs

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls) and click **Search and Analysis** in the left sidebar.
2. On the **Search and Analysis** page, select the region, logset, and log topic to view logs.
3. Click **Index Configuration** and enable full-text index for the cluster in the basic configuration window that pops up.
4. Enter the search syntax, select a time range, and then click **Search Analysis** to search for logs.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/3YR7537_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221226163615.png)

## FAQs

### What can I do if logs are not displayed?

If you confirm that you have reported logs but they are not displayed, please check the following:
1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/role) to check if there is a TKE_QCSLinkedRoleInEKSLog role.
2. Check if full-text index has been enabled for the log topic.
3. If role authorization has been enabled, check if the role bound to the container instance has the permission to report logs. For specific configuration, see "Role Authorization".
4. Check if the entity selected for the role bound to the instance is CVM.

If the problem persists, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) to contact us.
