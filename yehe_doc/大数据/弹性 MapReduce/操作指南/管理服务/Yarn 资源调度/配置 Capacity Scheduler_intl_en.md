## Overview
Capacity Scheduler organizes resources in a hierarchical manner, allowing multiple users to share cluster resources based on multi-level resource restrictions.
## Directions
### Creating a resource pool
1. Log in to the [EMR console](https://console.cloud.tencent.com/emr) and click **Details** of the target Hadoop cluster in the cluster list to enter the cluster details page.
2. On the cluster details page, select **Cluster Service** and click **Operation** > **Resource Scheduling** in the top-right corner of the YARN component block to enter the **Resource Scheduling** page.
![](https://qcloudimg.tencent-cloud.cn/raw/4905f191ea23cca1404bc0535661343b.png)
3. Toggle on **Resource Scheduler** and configure the scheduler.
4. Create a resource pool for Capacity Scheduler.
Select **Capacity Scheduler**. On the displayed page, click **Create Resource Pool**. You can edit and clone an existing resource pool as well as create a subpool for it. You can also click **Default Settings** to set the number of times of delayed scheduling for Capacity Scheduler.
![](https://qcloudimg.tencent-cloud.cn/raw/86d66b1e7dbd36ef7db534180aa4884a.png)
<img src="https://qcloudimg.tencent-cloud.cn/raw/1c9248022f9d3b718353db69b787b985.png" style="zoom:67%;" />

**Fields and parameters**:
<table>
<thead>
<tr>
<th>Field Name</th>
<th>Parameter</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Resource Pool Name</td>
<td>yarn.scheduler.capacity.&lt;queue-path>.queues&lt;/queue-path></td>
<td>Name of the resource pool or queue</td>
</tr>
<tr>
<td>Label Settings</td>
<td>N/A</td>
<td>Set the specified label that can be accessed by the queue.</td>
</tr>
<tr>
<td>Capacity</td>
<td>yarn.scheduler.capacity.&lt;queue-path>.capacity&lt;/queue-path></td>
<td>Available resource amount. The total capacity of the subpools of a parent pool is 100. Available resource amount = resource amount of the parent pool * percentage set here. The queue can consume more resources than the queue's capacity if there are idle resources in other queues.</td>
</tr>
<tr>
<td>Max Capacity</td>
<td>yarn.scheduler.capacity.&lt;queue-path>.maximum-capacity&lt;/queue-path></td>
<td>Maximum queue capacity in percentage. Because of resource sharing, the amount of resources used by a queue may exceed its capacity, and this field specifies the maximum amount of resources that can be used by the queue.</td>
</tr>
<tr>
<td>Default Label Expression</td>
<td>yarn.scheduler.capacity.&lt;queue-path>.default-node-label-expression&lt;/queue-path></td>
<td>If a resource request does not have a node label specified, the application will be submitted to the corresponding partition specified by this configuration item. By default, the value is empty, i.e., applications will be allocated to containers on nodes with no label.</td>
</tr>
<tr>
<td>Min User Capacity</td>
<td>yarn.scheduler.capacity.&lt;queue-path>.minimum-user-limit-percent&lt;/queue-path></td>
<td>Minimum resources in percentage guaranteed for each user. Each queue enforces a limit on the percentage of resources allocated to a user at any given time. When multiple users' applications are running in a queue concurrently, the amount of resources used by each user varies between a minimum and maximum value. The minimum value depends on the number of running applications, and the maximum value is determined by `minimum-user-limit-percent`.</td>
</tr>
<tr>
<td>User Resource Factor</td>
<td>yarn.scheduler.capacity.&lt;queue-path>.user-limit-factor&lt;/queue-path></td>
<td>Maximum amount of resources in percentage that can be used by each user. For example, if the value is `30`, the amount of resources for each user cannot exceed 30% of the queue capacity at any given time.</td>
</tr>
<tr>
<td>Max Memory per Container</td>
<td>yarn.scheduler.capacity.&lt;queue-path>.maximum-allocation-mb&lt;/queue-path></td>
<td>Maximum memory that can be allocated to each container. The value will overwrite and cannot be greater than that of the system's `yarn.scheduler.maximum-allocation-mb`.</td>
</tr>
<tr>
<td>Max vCores per Container</td>
<td>yarn.scheduler.capacity.&lt;queue-path>.maximum-allocation-vcores&lt;/queue-path></td>
<td>Maximum number of cores that can be allocated to each container. The value will overwrite and cannot be greater than that of the system's `yarn.scheduler.maximum-allocation-vcores`.</td>
</tr>
<tr>
<td>Resource Pool Status</td>
<td>yarn.scheduler.capacity.&lt;queue-path>.state&lt;/queue-path></td>
<td>Status of the queue. The value can be `Running` or `Stopped`. If a queue is in the `Stopped` status, new applications cannot be submitted to it or any of its subqueues.</td>
</tr>
<tr>
<td>Max Apps</td>
<td>yarn.scheduler.capacity.&lt;queue-path>.maximum-applications&lt;/queue-path></td>
<td>Maximum number of concurrent active (both running and pending) applications allowed in the system </td>
</tr>
<tr>
<td>Max Resources for AM</td>
<td>yarn.scheduler.capacity.&lt;queue-path>.maximum-am-resource-percent&lt;/queue-path></td>
<td>Maximum percentage of resources in the cluster which can be used to run application masters. It controls the number of concurrent active applications. </td>
</tr>
<tr>
<td>Resource Pool Priority</td>
<td>yarn.scheduler.capacity.root.&lt;leaf-queue-path>.default-application-priority&lt;/leaf-queue-path></td>
<td>Configure the priority of the resource queue, which is `0` by default. The larger the value, the higher the priority.</td>
</tr>
<tr>
<td>Submission</td>
<td>yarn.scheduler.capacity.root.&lt;queue-path>.acl_submit_applications</queue-path></td>
<td>List of users that can submit apps to the queue</td>
</tr>
<tr>
<td>Management</td>
<td>yarn.scheduler.capacity.root.&lt;queue-path>.acl_administer_queue</queue-path></td>
<td>List of users that can manage the queue</td>
</tr>
<tr>
<td>Delayed Scheduling</td>
<td>yarn.scheduler.capacity.node-locality-delay</td>
<td>Set the allowed number of times of delayed scheduling to ensure the local execution of tasks. If the value is `-1`, delayed scheduling will be disabled.</td>
</tr>
</tbody></table>

### Configuring resource pool mappings
1. In the **Policy Settings** section, click **Resource Pool Mappings**. On the displayed page, click **Create Resource Pool Mapping**.
![](https://qcloudimg.tencent-cloud.cn/raw/a53afa531d55fc9a9ed0d13806f9c269.png)
![](https://qcloudimg.tencent-cloud.cn/raw/885fc900c0d98953418291fa68303905.png)
2. Configure **Overwrite Specified Queues**.
This feature is disabled by default. For example, you have defined a mapped queue in **Resource Pool Mappings** and specified a queue other than the mapped queue when submitting a task; if the specified queue is `default` and **Overwrite Specified Queues** is enabled, the mapped queue will be used; otherwise, the specified queue will be used.

### Sample label-based scheduling
1. Log in to the [EMR console](https://console.cloud.tencent.com/emr) and click **Details** of the target Hadoop cluster in the cluster list to enter the cluster details page.
2. On the cluster details page, select **Cluster Service** and click **Operation** > **Resource Scheduling** in the top-right corner of the YARN component block to enter the **Resource Scheduling** page.
3. Toggle on **Resource scheduler** and select **Capacity Scheduler**.
4. Toggle on **Label-based scheduling** and click **Label Management** to enter the **Label Management** page.
![](https://qcloudimg.tencent-cloud.cn/raw/13fd863cc3eb5acd4f8ffedf7f3c0cc3.png)
5. Click **Create Label**, enter the label name, and set the label type and node to be bound to as needed.
<img src="https://qcloudimg.tencent-cloud.cn/raw/9c4b32d2147ff06371acea3c76be8115.png" style="zoom:67%;" />
6. After the label is set, click **Apply**. Then, you can view and edit the resource queue of the label in the resource pool.
![](https://qcloudimg.tencent-cloud.cn/raw/f81987efdc00cc01113a5af9710d14e1.png)
7. On the **Resource Scheduling** page, click **Create Resource Pool** and set **Label**, **Capacity**, **Max Capacity**, and other parameters as needed.
>? The capacity and maximum capacity of a resource pool can be configured by label.

![](https://qcloudimg.tencent-cloud.cn/raw/824235abc226885fd6ea2d741510390f.png)
![](https://qcloudimg.tencent-cloud.cn/raw/fdb9d5f056738f63a78208ac68de7a09.png)

8. After the resource pool is set, click **Apply** to submit the task to the backend.
>! Proceed with caution when restarting the ResourceManager. If you are prompted that the ResourceManager will be restarted after clicking **Apply**, check whether the operation is successful in **Scheduling History** and whether the ResourceManager is healthy in **Role Management**.