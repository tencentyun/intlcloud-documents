>? You don't need to manage the public engine, as it is managed by Data Lake Compute in a unified manner.
## Modifying the private engine configuration
>! Fees may change as the private engine configuration changes. For more information, see [Configuration Adjustment Fees Description](https://intl.cloud.tencent.com/document/product/1155/48655).

Option 1. Data engine list
1. Log in to the [Data Lake Compute console](https://console.cloud.tencent.com/dlc) and select the service region. You need to have the Tencent Cloud admin or financial collaborator permission.
2. Click **Data engine** on the left sidebar to enter the data engine management page.
3. Find the target private engine and click **Configuration** on the right to enter the configuration modification page, where you can modify the cluster specification and elastic scaling policy.
4. After making changes, click **Save** to submit the order and make the payment.
![]()

Option 2. Data engine details
1. Log in to the [Data Lake Compute console](https://console.cloud.tencent.com/dlc) and select the service region. You need to have the Tencent Cloud admin or financial collaborator permission.
2. Click **Data engine** on the left sidebar to enter the data engine management page.
3. Find the target private engine and click the cluster name to enter the cluster details page, where you can modify the cluster specification and elastic scaling policy.
4. Adjust the parameters as needed and click **Save**.
![]()

## Modifying the private engine information
1. Log in to the [Data Lake Compute console](https://console.cloud.tencent.com/dlc) and select the service region. You need to have the Tencent Cloud admin permission.
2. Click **Data engine** on the left sidebar to enter the data engine management page.
3. Find the target private engine and click the cluster name to enter the cluster details page, **where you can modify the cluster description, automatic start policy, and suspension policy**.
4. Adjust the parameters as needed and click **Save**.
![]()
Suspension policy: Configure the suspension method of a pay-as-you-go data engine. Automatic suspension and scheduled suspension are supported. A suspended pay-as-you-go data engine will not incur fees.
	Auto-suspension: The data engine will be automatically switched to the **Suspended** status after it has been idle for 15 minutes.
	- Timing policy: You can configure scheduled start and suspension policies by week. The system will start or suspend clusters regularly as configured.
		- Suspension after task end: After the specified time elapses, if a task is running, the system will automatically suspend the data engine within five minutes after the task ends.
		- Suspension after task pause: After the specified time elapses, if a task is running, the system will pause the task and suspend the data engine immediately.

## Manually suspending/starting a private engine
>! Monthly subscribed resources are resident and cannot be suspended.
>
1. Log in to the [Data Lake Compute console](https://console.cloud.tencent.com/dlc) and select the service region. You need to have the Tencent Cloud admin permission.
2. Click **Data engine** on the left sidebar to enter the data engine management page.
3. Find the target private engine, click **More**, and select **Start** or **Suspend** in the drop-down list.
![]()



## Terminating a private engine
You can terminate a data engine that is no longer needed. A monthly subscribed data engine will be returned automatically after termination. For more information, see [Refund](https://intl.cloud.tencent.com/document/product/1155/48653).
>! Note that a pay-as-you-go data engine cannot be recovered once terminated. Proceed with caution.

1. Log in to the [Data Lake Compute console](https://console.cloud.tencent.com/dlc) and select the service region. You need to have the Tencent Cloud admin permission.
2. Click **Data engine** on the left sidebar to enter the data engine management page.
3. Find the target private engine (only suspended clusters can be terminated), click **More**, and select **Terminate** in the drop-down list.
4. Confirm the termination.
![]()

## Cluster running logs
Data Lake Compute provides running logs within 14 days for private engines to help you stay informed of the start, suspension, and scaling of clusters. Cluster logs mainly include the following content:
- Start time: The time when the cluster starts working.
- Suspension time: The time when the cluster stops working.
- Scale-out record: The time of the cluster scale-out and the number of added clusters.
- Scale-in record: The time of the cluster scale-in and the number of removed clusters.
![]()

## Viewing cluster running logs
1. Log in to the [Data Lake Compute console](https://console.cloud.tencent.com/dlc) and select the service region. You need to have the data engine monitoring permission (for more information, see [Permission Overview](https://intl.cloud.tencent.com/document/product/1155/48665)).
2. Click **Data engine** on the left sidebar to enter the data engine management page.
3. Find the target private engine and click the cluster name to enter the cluster details page.
![]()
