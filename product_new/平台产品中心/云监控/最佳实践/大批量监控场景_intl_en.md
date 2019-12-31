## Overview
As your business continues to develop, your need for underlying resources will also increase. With more and more basic resources, the efficiency of daily monitoring becomes a bottleneck in OPS. Tencent Cloud Cloud Monitoring (CM) provides a solution for large-scale resource monitoring scenarios to customers who have a large number of resources.

## Steps
### Performance view for large-scale resource monitoring

With a large number of resources, it is impossible to view the metric data of all cloud resources one by one. Even if you do, you still cannot compare the data in a global way, nor detect exceptions. There are two key points when monitoring a large number of resources:

- Aggregation: The performance data of a batch of resources is aggregated. With aggregated data, you can easily understand the overall resource operation performance.
- Sorting: The data of a batch of resources is sorted by metric, allowing you to quickly identify abnormal data and corresponding resource objects.

#### Creating an aggregation monitoring view for large-scale resources

Using Cloud Virtual Machine (CVM) as an example:

1. CVM resources are classified and managed by service and cluster in projects. The resources of different services or clusters reside in different projects.
2. Log in to [Cloud Monitoring Console](https://console.cloud.tencent.com/monitor/).
3. In the left sidebar, click **Dashboard** to access the dashboard management page.
4. In the upper-left corner of the page, click **Add Monitoring Dashboard** to add a dashboard.
5. Click **Add Monitoring Chart**. In the pop-up dialog box, configure monitoring items. <!--For more information, see [Configuring the monitoring view]().-->

6. After the configuration is completed, click **OK** to complete the creation.
   * You can create multiple charts with multiple metrics in batches to avoid repeatedly selecting monitoring items.
   * You can create charts in batches in the order of objects in the list to avoid repeatedly configuring new charts when the number of resources to be monitored exceeds the content limit of a chart.
   * You can filter and search for resources, select all resources with one click, or select multiple resources by pressing **Shift**. The user-friendly batch operations facilitate the batch selection of resources, improving configuration efficiency.
7. Sum up the data of all servers to calculate the total bandwidth used by a service or cluster according to bandwidth-related metrics.
   Calculate the `Avg`, `Max`, and `Min` values of the monitoring data of all servers according to performance metrics, such as the CPU utilization, and display them in one chart. You can then obtain the average, maximum, and minimum CPU utilization of a service or cluster. <!--By looking at these calculated data as a graph, you can easily identify abnormal peak values.-->

8. **Detect abnormal data in an aggregation view**. According to the overall trend of resource aggregation curves and their comparisons, you can understand the overall trends and exceptions in the performance data of resources.
   For example, you can determine whether the current bandwidth is abnormal by comparing the inbound and outbound bandwidth curves as well as the overall trend of bandwidth curves. You can also determine the overall status of resources and whether abnormal resources exist by comparing the average, maximum, and minimum CPU utilization.
9. **Locate a specific abnormal object.**
 1. Click the curve at a specific time point to show a list of corresponding instances sorted by performance. You can change the sorting order and metrics, or switch the data displayed in the list by clicking different points in the curve.

 2. Hover over an instance in the sorted list. The monitoring data curve corresponding to this instance is highlighted in the curve above. Compare and analyze the monitoring curve of this instance and the overall aggregated data curve to further determine the current and historical exceptions of the instance.

 3. After confirming the specific abnormal object via the previous two steps, click the name of the abnorml object in the list to open the monitoring details page for further troubleshooting.

So far, you have completed the processes of creating a monitoring view, viewing the monitoring view, detecting an exception, and locating the exception. The chart and the sorting list allow you to intuitively view the running status of all resources, locate the specific abnormal object, and analyze the trend of an exception. This provides an effective solution to solve inefficiency in large-scale resource monitoring and difficulty in detecting exceptions.

> Currently, a maximum of 12 CVM instances can be added to each chart on the dashboard. If this does not meet your needs, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category) to raise the limit.

#### Creating a details monitoring view for large-scale resources

In addition to aggregation views, you can also use a details view to detect and locate exceptions in large-scale resources.

Details view: The curves of all instances are displayed in the same chart.
Aggregation view: The curves of all instances are computed and aggregated into one or more curves by using a custom statistical method.

1. **Create a details view.**
   The process of creating a details view is similar to that of creating an aggregation view. You do not need to select the statistics collection mode when creating a details view.  <!--For detailed process, see [Configuring the monitoring view]().-->
2. **Detect exceptions in a details view.**
 * The more resources are in the same service or cluster, the denser the curves are in the chart. The overall trends and densities of curves in the chart indicate the overall trends and distributions of resource performance data.
 * If some curves deviate from the rest, the performance data of the corresponding instances is abnormal.
3. **Locate a specific abnormal object.**
   You can also use a details view in conjunction with a chart and a sorted list to locate a specific abnormal object. The overall process is similar to that for an aggregation view. For more information, see the sixth item for aggregation views above.
> Currently, a maximum of 12 CVM instances can be added to each chart on the dashboard. If this cannot meet your needs, you can submit a ticket to raise the limit.

### Configuring alarm policies for large-scale resources

1. CVM resources are classified and managed by service and cluster in the project. The resources of different services or clusters reside in different projects.
2. Log in to Cloud Monitor Console and choose **Alarm Configuration** to create alarm policies for resources. After the resources are grouped by project, you can create a default [Alarm Policy](https://intl.cloud.tencent.com/document/product/248/6215) for each project.
   The default alarm policy is automatically bound to all resources in the project. If resource changes occur, such as when new resources are added, project changes, or resources are terminated upon expiration, resource objects bound to the default policy will change accordingly by default, eliminating the need for complex manual maintenance.

