## Overview

Environment management enables you to view and manage environments and runtime environments easily. You can view the configuration, usage, and Ops information of deployed environments at one stop.


## Environment Management Page

1. Log in to the [iPaaS console](https://ipaas.tencentcloud.com/login) and click **Management center** > **Environment management** on the left sidebar.
2. The environment list page displays the basic information of each environment as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/5892936527e7622474240ea69913d7bf.png)
	- **Environment name**: It displays the names of all environments for which you have permissions. 
	- **Status**: It displays the instantaneous status of each environment. Currently, you cannot create, delete, or extend environments in the console. The platform supports the following environment statuses (when an operation is performed on the backend, the status displayed on the frontend will be updated), and the environment availability varies by status:
<table>
<thead>
<tr>
<th>Environment Status</th>
<th>Availability</th>
</tr>
</thead>
<tbody><tr>
<td>Creating</td>
<td>Apps cannot be published</td>
</tr>
<tr>
<td>Running</td>
<td>Apps can be published</td>
</tr>
<tr>
<td>Extending</td>
<td>Apps can be published</td>
</tr>
<tr>
<td>Deleting</td>
<td>Apps cannot be published</td>
</tr>
<tr>
<td>Unavailable</td>
<td>Apps cannot be published</td>
</tr>
<tr>
<td>Creation failed</td>
<td>Apps cannot be published</td>
</tr>
<tr>
<td>Services suspended</td>
<td>Apps cannot be published</td>
</tr>
</tbody></table>
	- **Region - environment type**: It displays the list of exclusive and shared environments. Currently, iPaaS supports two environment types with different environment deployment characteristics and resource capabilities.
		- Shared environment: It is a high-availability iPaaS runtime environment shared by all users for quick app publishing.
		- Exclusive environment: For data and resource security considerations, iPaaS also provides a deployment mode with stronger resource and data isolation, i.e., exclusive environment. You can use an iPaaS runtime environment exclusively to isolate computing resources and data and quickly increase the isolation level at low costs. Currently, you can create an exclusive environment by clicking **Purchase environment**.
	- **Environment plan**: Enterprise (this field is displayed only for Enterprise Edition exclusive environment).
	- **Expiration time**: Expiration time of the environment.
	- **Resource**: The configuration information of CPU, memory, and network bandwidth resources are displayed only for Enterprise Edition environments during purchase or after upgrade but not for the shared environment.
	- **Resource overview**: It displays the actual resource usage for Enterprise Edition environments but not for the shared environment.
	- **Operation**: Currently, operations such as app management, execution overview viewing, and information configuration are supported.


## Environment Management Operations

### Purchasing an environment
>?After being purchased, the environment will be in **Creating** status for one to three minutes. Wait patiently.
>
The **shared environment** is suitable for new users to test the basic product features, while an exclusive environment (Enterprise Edition) is more suitable for deploying businesses.
An **exclusive environment** provides a deployment mode with stronger resource and data isolation for data and resource security considerations. You can use an iPaaS runtime environment exclusively to isolate computing resources and data and quickly increase the isolation level at low costs. It is suitable for deploying businesses.

1. Log in to the [iPaaS console](https://ipaas.tencentcloud.com/login), click **Management center** > **Environment management** on the left sidebar, and click **Purchase Enterprise Edition**.
    ![](https://qcloudimg.tencent-cloud.cn/raw/d8fc24228b57098183d30cd536efd558.png)
2. On the configuration selection page, select an environment configuration based on your business needs. If you are worried that a high configuration may lead to resource waste, you can select the basic environment configuration first and **change the configuration** subsequently. For more information on purchase, see [Purchase Guide](https://www.tencentcloud.com/document/product/1165/51578).
![](https://qcloudimg.tencent-cloud.cn/raw/e22fbed7d16dd9ad67c2ff18269d1969.png)

### Renewal and upgrade
You can renew and upgrade Enterprise Edition environments on the **Environment management** page.
#### Upgrade
Please contact online customer service staff.

#### Renewal
Log in to the [iPaaS console](https://ipaas.tencentcloud.com/login), click **Environment management**, and click *Renew**.
![](https://qcloudimg.tencent-cloud.cn/raw/0696aa385e42f93d7008991f85bc63d7.png)
Select a renewal period.

### Viewing environment details
Click **Details** to view environment details, including overview, app management, and configuration details (available for exclusive environments).
![](https://qcloudimg.tencent-cloud.cn/raw/0b9f8971449d009fa09760960bd1f580.png)
<dx-tabs>
::: Overview
The **Overview** tab centrally displays information such as environment name, status, region, and type and the number of running integration apps, but the displayed fields differ slightly for shared and exclusive environments as shown below (fields marked in red boxes are displayed only for Enterprise Edition (exclusive) environments):
![](https://qcloudimg.tencent-cloud.cn/raw/9a8aa022b48f5a288f7f7e259627893a.png)

- Shared environment: The overview of the shared (Trial Edition) environment displays the basic information, region, status, and other information of the environment as well as the numbers of integration apps and flows running in the environment.
- Exclusive environment: The overview of an exclusive (Enterprise Edition) environment is similar to that of a Trial Edition environment. However, in addition to the basic information, region, status, and other information of the environment as well as the numbers of integration apps and flows running in the environment, it also displays the usage and running status (such as CPU and memory usage) of the current environment.
:::
::: Applications
You can enter the **Applications** tab on the environment details page or by selecting **Environment management** > **Applications**. This tab centrally displays app names, app statuses, project names, deployment time, running/debugging versions, and operations of the current environment for you to further view and manage the apps in the specified environment.
![](https://qcloudimg.tencent-cloud.cn/raw/69d9e28837ac23a7485ee33f40e88d6f.png)
**App management operations**:

- Start: You can start apps in **Stopped** status in the environment.
- Stop: You can stop apps in **Running** status in the environment.
- Remove: You can remove apps in **Stopped** status in the environment. Log query is not supported for removed apps.
  ![](https://qcloudimg.tencent-cloud.cn/raw/81ed73bd794d2e55f93147bfb934e2a1.png)
:::
::: Configuration
>!The **Configuration** tab is displayed only for an exclusive environment. Currently, the configuration parameters cannot be modified on the backend by default for the shared environment.
>
The **Configuration** tab centrally displays parameter configurations, including environment configuration (environment use limits), Dataway configuration, and component configuration. You can modify the upper limits as needed and click **Save**. To restore the default value, click **Reset** as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/4c33ba725cb0b52864f6ec80fd2284b8.png)

- Environment configuration
- Use limits
  - Maximum number of requests per second: The maximum number of requests that can be triggered per second.
  - Maximum number of project requests per second: The maximum number of requests that can be triggered per second for a single project.
  - Maximum number of flow requests per second: The maximum number of requests that can be triggered per second for a single flow.
  - Maximum concurrency: The maximum concurrency supported by the system.
  - Maximum project concurrency: The maximum concurrency for a single project.
  - Maximum flow concurrency: The maximum concurrency for a single flow.
- Execution engine
  - Maximum message size: The maximum size of a message in the memory.
  - Flow execution timeout period: The timeout period for flow execution.
  - Maximum message size in memory: Messages exceeding the size will be stored to COS for processing.
- Environment configuration
- Timeout period: Dataway timeout period. After configuration, you need to restart the corresponding integration app for the configuration to take effect.
- Component configuration
- Database 
  - Fetch Size: The maximum number of database entries that can be queried each time. After configuration, you need to restart the corresponding integration app for the configuration to take effect.
:::
</dx-tabs>
