A private data engine in Data Lake Compute supports pay-as-you-go and monthly subscription billing modes. For billing details, see [Billing Overview](https://intl.cloud.tencent.com/document/product/1155/48652).

## Private engine purchase
You can purchase on the Data Lake Compute purchase page or in the console as instructed below:
1. Log in to the [Data Lake Compute console](https://console.cloud.tencent.com/dlc) and select the service region. You need to have the Tencent Cloud admin or financial collaborator permission.
2. Click **Data engine** on the left sidebar to enter the data engine management page.
3. Click **Create resource** in the top-left corner to enter the **Resource configuration** page. Configure the resource as needed and view the estimated price.
![]()
4. Confirm the price and make the purchase.
![]()

**Configuration parameter description:**
- Region: Cloud products in different regions are not interconnected over private networks and the region cannot be changed after you purchase the service. Proceed with caution.
- Compute engine: Presto and Spark engines are supported. Note that the engine cannot be changed once purchased. Presto is suitable for faster interactive query and analysis and multi-source federated query, while Spark is suitable for more stable offline tasks with large data volumes.
- Cluster spec: Cluster specification is measured in CU. 1 CU equals to 1 CPU core and 4 GB memory of compute resources. The specification determines the amount of compute resources during task execution and can be purchased as needed.
>! If you need more than 152 CUs, submit a ticket for assistance.
- Min cluster count: Set the minimum number of clusters during cluster start or resident resources in a monthly subscribed cluster. Multiple clusters can deliver a higher concurrency.
- Max cluster count: Set the maximum number of clusters for elastic scaling. If it is the same as the minimum cluster count, elastic scaling is not enabled for the cluster.
- Auto-start: If it is enabled, a suspended data engine will be automatically started after receiving a task request.
>! As pay-as-you-go resources are not reserved, it is possible that they cannot be started right away. If you need resident and stable compute resources, purchase a monthly subscribed data engine instead.
- Suspension policy: Configure the suspension method of a pay-as-you-go data engine. Automatic suspension and scheduled suspension are supported. A suspended pay-as-you-go data engine will not incur fees.
	- Auto-suspension: The data engine will be automatically switched to the **Suspended** status after it has been idle for a certain period of time.
	- Timing policy: You can configure scheduled start and suspension policies by week. The system will start or suspend clusters regularly as configured.
		- Suspension after task end: After the specified time elapses, if a task is running, the system will automatically suspend the data engine within five minutes after the task ends.
		- Suspension after task pause: After the specified time elapses, if a task is running, the system will pause the task and suspend the data engine immediately.
- Advanced configuration: If you need to use federated query, configure the IP range in the advanced configuration.
- Tag: Set tags to categorize purchased resources and allocate costs. For more information, see [Associating Tag with Private Engine Resource](https://intl.cloud.tencent.com/document/product/1155/48685).

## Bill query
You can query bills in the Data Lake Compute console in the following steps:
1. Log in to the [Data Lake Compute console](https://console.cloud.tencent.com/dlc) and select the service region. You need to have the Tencent Cloud admin or financial collaborator permission.
2. Click **Data engine** on the left sidebar to enter the data engine management page.
3. Click **Bill query** to view the detailed bill and settlement information (the financial collaborator permission is required).
![]()

## Renewal management
For a monthly subscribed private data engine, you can perform renewal and other operations in the Data Lake Compute console > Renewal management > Resource management in the following steps:
1. Log in to the [Data Lake Compute console](https://console.cloud.tencent.com/dlc) and select the service region. You need to have the Tencent Cloud admin or financial collaborator permission.
2. Click **Data engine** on the left sidebar to enter the data engine management page.
3. Click **Renewal management** to enter the resource list and renew resources (the financial collaborator permission is required).
![]()
