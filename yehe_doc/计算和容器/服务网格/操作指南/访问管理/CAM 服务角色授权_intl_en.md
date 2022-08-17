The use of Tencent Cloud Mesh involves service mesh-related cloud resources. To use Tencent Cloud Mesh features normally, you need to authorize the service role `TCM_QCSRole` of Tencent Cloud Mesh. The Tencent Cloud Mesh service can use related cloud resources only after authorization.

Scenarios that require service authorization mainly include [Initial Login to the Tencent Cloud Mesh Console](#TCMRole) and [Initial Use of Tencent Cloud Mesh Sample Deployment](#TCMRoleInSample). The two scenarios correspond to two preset policies ` QcloudAccessForTCMRole ` and ` QcloudAccessForTCMRoleInSampleDeployment `, respectively.



## Initial Login to the Tencent Cloud Mesh Console[](id:TCMRole)

### Authorization Scenario

When you log in to the [Tencent Cloud Mesh console](https://console.cloud.tencent.com/tke2/mesh) for the first time after registering and logging in to a Tencent Cloud account, you need to go to the **Cloud access management** page to grant the current account Tencent Cloud Mesh permissions for operating on TKE, SSL certificates, CLS, and other cloud resources. The permissions are granted by associating the preset policy ` QcloudAccessForTCMRole `with the service role `TCM_QCSRole` of Tencent Cloud Mesh. This authorization process also involves the creation of a Tencent Cloud Mesh service role if you have not created a Tencent Cloud Mesh service role yet.

### Authorization Steps

1. Log in to the [Tencent Cloud Mesh console](https://console.cloud.tencent.com/tke2/mesh). For the initial login, the **Service authorization** window automatically pops up.
![](https://qcloudimg.tencent-cloud.cn/raw/960f945bce9253063b8f6ff8d5c32e62.png)
2. Click **Go to cloud access management** to enter the **Service authorization** page.
3. Click **Grant** to complete authentication.
![](https://qcloudimg.tencent-cloud.cn/raw/c064ec50986682f70eacb39b4cd51097.png)

### Permission Content

**TKE**

| Permission | Description | Resource |
| :-------- | :--------| :------ |
| DescribeClusterSecurity | Querying cluster keys | All resources `*` |

 **SSL certificate**

| Permission | Description | Resource |
| :-------- | :--------| :------ |
| DescribeCertificateDetail | Obtaining certificate details | All resources `*` |

 **CLS**

| Permission | Description | Resource |
| :-------- | :--------| :------ |
| getLogset | Obtaining logset details | All resources ` * ` |
| getTopic | Obtaining log topic details | All resources ` * ` |
| createLogset | Creating a logset | All resources ` * ` |
| createTopic | Creating a log topic | All resources ` * ` |
| modifyIndex | Modifying an index | All resources ` * ` |
| listLogset | Obtaining a logset list | All resources ` * ` |
| listTopic | Obtaining a log topic list | All resources ` * ` |


