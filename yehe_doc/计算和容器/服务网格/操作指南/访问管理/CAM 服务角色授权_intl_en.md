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


## Initial Use of Tencent Cloud Mesh Sample Deployment[](id:TCMRoleInSample)

### Authorization Scenario

When you use Tencent Cloud Mesh sample deployment for the first time, you need to go to the **Cloud access management** page to grant the current account Tencent Cloud Mesh permissions for operating on VPCs, CCN, TKE, CVMs, and other cloud resources and finance permission for purchasing CVMs. The permissions are granted by associating the preset policy `QcloudAccessForTCMRoleInSampleDeployment` with the service role `TCM_QCSRole` of Tencent Cloud Mesh. This authorization process also involves the creation of a Tencent Cloud Mesh service role if you have not created a Tencent Cloud Mesh service role yet.

### Authorization Steps

1. Log in to the [Tencent Cloud Mesh console](https://console.cloud.tencent.com/tke2/mesh), move the cursor to **Sample deployment** button, and click **Service authorization** to pop up an authorization prompt window.
2. Click **Go to cloud access management** to enter the **Service authorization** page.
3. Click **Grant** to complete authentication.

### Permission Content

 **VPC**

| Permission | Description | Resource |
| :-------- | :--------| :------ |
| CreateSubnet |  Creating a subnet | All resources ` * ` |
| CreateVpc |  Creating a VPC | All resources ` * ` |
| DeleteVpc |  Deleting a VPC | All resources ` * ` |
| DescribeVpcEx | Querying a VPC list | All resources ` * ` |
| DescribeSubnetEx | Querying a subnet list | All resources ` * ` |

**CCN**

| Permission | Description | Resource |
| :-------- | :--------| :------ |
| AttachCcnInstances |  Associating a CCN instance | All resources ` * ` |
| CreateCcn |  Creating a CCN | All resources ` * ` |
| DeleteCcn | Deleting a CCN | All resources ` * ` |
| DescribeCcnAttachedInstances | Querying a list of instances associated with a CCN | All resources ` * ` |
| DescribeCcns |  Querying a CCN list | All resources ` * ` |

 **TKE**

| Permission | Description | Resource |
| :-------- | :--------| :------ |
| CreateCluster |  Creating a cluster | All resources ` * ` |
| CreateClusterEndpointVip |  Enabling a cluster access port (Only external network ports of managed clusters are supported.) | All resources ` * ` |
| DeleteCluster |  Deleting a cluster | All resources ` * ` |
| DeleteClusterEndpoint | Deleting a cluster access port | All resources ` * ` |
| DeleteClusterEndpointVip | Deleting a cluster access port (Only external network ports of managed clusters are supported.) | All resources ` * ` |
| DescribeClusterEndpointVipStatus | Querying the status of enabling the cluster access port (Only external network ports of managed clusters are supported.) | All resources ` * ` |
| DescribeClusters | Obtaining a cluster list | All resources ` * ` | 

 **CVM**

| Permission | Description | Resource |
| :-------- | :--------| :------ |
| CreateSecurityGroup | Creating a security group | All resources ` * ` |
| DeleteSecurityGroup |  Deleting a security group | All resources ` * ` |
| DescribeImages |  Querying images | All resources ` * ` |
| DescribeInstances | Querying instances | All resources ` * ` |
| DescribeSecurityGroups | Querying security groups | All resources ` * ` |
| ModifySecurityGroupPolicys | Modifying a security group rule | All resources ` * ` |
| RunInstances | Creating an instance | All resources ` * ` | 

**Finance permission**

| Permission | Description | Resource |
| :-------- | :--------| :------ |
| `finance:*` |  Finance permission for purchasing CVM | CVM ` qcs::cvm:::* ` |
