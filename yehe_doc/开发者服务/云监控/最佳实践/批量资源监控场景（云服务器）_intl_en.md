## Introduction

As business continuously develops, the scale of underlying resources expands. With more basic resources, the efficiency of daily monitoring becomes a bottleneck for OPS. The solution to batch resource monitoring scenarios is provided by Tencent Cloud’s Cloud Monitor and is designed to improve monitoring efficiency when there are massive resources. This document describes the monitoring of a batch of CVMs as an example to provide you with the best practices for monitoring complex business metrics.



## Implementation Notes


#### Key points of the implementation

In cases where you have deployed complex business on Tencent Cloud CVMs, the number of servers involved is large. In such cases, it is impractical to check the monitoring data of all cloud resources one by one. In addition, as no comparison is made between individual resources and the overall condition, it is difficult to detect exceptions. Besides, monitoring in the business or cluster dimension cannot be implemented, and the OPS efficiency and methods lag behind substantially. Therefore, with regard to the batch monitoring of resources, the following key points are concerned:
- **Chart grouping**
- **Dynamic analysis**
- **Day-over-day and week-over-week analysis**
- **Quick chart redirection**
- **Legend configuration and sorting**


#### Implementation background

As shown in the figure below, two businesses run under the Penguin project: the Emperor Penguin business and the Round Penguin business.
- The Emperor Penguin business involves 7 servers, with 3 on the frontend and 4 on the backend.
- The Round Penguin business involves 6 servers, with 3 in Guangzhou and 3 in Shenzhen.
![](https://main.qcloudimg.com/raw/11dc6fa24684cba6e0d9bb2b8a7461de.png)



## Step 1: Create a Dashboard and Chart Groups

1. Create a dashboard. In this case, create a dashboard named `Penguin Project`. For directions, see [Creating a Dashboard](https://intl.cloud.tencent.com/document/product/248/38468).

2. Create chart groups. As shown in the figure below, click the creation icon in the upper-right corner of the dashboard, click **Create a Chart Group** and the settings icon next to the chart group name. Enter the chart group name and click **OK** to create a chart group. In this case, create two chart groups for two businesses, respectively.



## Step 2: Create Monitoring Charts for Different Businesses

In this step, you need to create aggregation and detail monitoring charts, with frontend-backend separation or regional separation for two businesses, respectively. The following uses the monitoring scenario with frontend-backend separation as an example.

1. Click the **Create a Chart** icon > **Create a Chart** and configure the chart as follows:
   - Chart name: in **Basic Info** of **Chart Configuration**, specify the **Chart Name**.
   - Monitoring type: in this example, select **QCEMetric**.
   - Metric: select the Tencent Cloud service type and the metric to be monitored. Here, **Cloud Virtual Machine** and the **Basic CPU Utilization** metric are used as an example.
   - Filter: filter the monitoring data sources. In this example, after selecting **Instance ID**, you can select the instance to be monitored by the chart. In this chart, the 3 frontend servers of the Emperor Penguin business are selected as the objects to be monitored.
   - group by: similar to the Group by feature of SQL, this feature can group data based on specified labels and then aggregate data according to aggregation algorithms. In this example, after selecting **Instance ID**, you can preview three curves, which correspond to the CPU utilization of the three frontend servers, respectively.
   
2. Click **Create a Chart** and configure the content of **Aggregation Chart** as follows:
   - In this example, create the chart **Frontend - Basic CPU Average Utilization** for monitoring the average CPU utilization of the three frontend servers. The methods for configuring the chart name, monitoring type, metric, and filter are the same as those for the detail chart.
   - group by: for the **Aggregation Chart**, instead of selecting a label, you need to select an aggregation method. Currently, four aggregation methods are available: sum, max, min, and avg. In this example, after selecting the avg method, you can preview the average CPU utilization of the three frontend servers.
     
3. In this step, drag the chart to the desired chart group, and adjust its size as needed.
   
4. You have now created the basic charts for monitoring the CPU standalone utilization and average utilization of the three frontend servers of the Emperor Penguin business. Next, perform advanced configuration on the two charts to improve the monitoring efficiency.
	 

## Step 3: Perform Advanced Chart Configuration

1. Configuring the day-over-day and week-over-week curves
   In the created **Frontend - Basic CPU Average Utilization** aggregation chart, a single curve is insufficient to quickly locate issues. By configuring the day-over-day and week-over-week curves, you can compare the current data with the data in the same period yesterday and last week. As shown in the following figure, by comparing and analyzing these three curves after the configuration, you can identify data exceptions more quickly.
   
2. Configuring and sorting the legend
   In the configured **Frontend Server - Basic CPU Utilization** detail chart, by default, the chart displays the maximum values of the curves. If you see multiple fluctuating curves, you can add legends for the summary functions, such as the minimum value, the average value, and the sum to enrich the metric data and better understand and analyze the overall trend in a period. In addition, by sorting legends, you can sort different numerical values of resources to quickly identify data with exceptions and the corresponding resource objects.
   
3. Configuring the link redirection
   Dashboards provide chart configuration with links that redirect to two positions: data and charts. This facilitates the configuration of multiple customized OPS scenarios. The following figure shows two use cases configured for **Frontend - Basic CPU Average Utilization**:
   
   - The chart link to start a one-click group conversation. This link can bring relevant OPS personnel of the current chart into a group via the one click group conversation feature, facilitating collaborative OPS and troubleshooting.
      
4. After completing the preceding three configurations, you can view the configuration effects on the dashboard page.
   

## Step 4: Perform Efficient Chart Analysis

1. Use template variables to dynamically analyze metrics
   Template variables enable you to dynamically switch data sources within the same dashboard. You can dynamically select the tag values bound with template variables to display different data in the same set of charts at any time. For example, you can modify the previous configuration of **Frontend - Basic CPU Average Utilization** to turn it into **Template Variable - Basic CPU Average Utilization**, which can dynamically switch data source instances. The detailed directions are as follows:
   1. Add the template variable `$Emperor Penguin Business Instance ID`, and associate it with the tag `CVM-Basic Monitoring Instance`. For the detailed directions for adding template variables, see [Configuring Template Variables](https://intl.cloud.tencent.com/document/product/248/38473). After completing the configuration, you can see the newly added template variable with a null value in the upper-left corner of the dashboard.
      
   2. Copy the chart **Frontend - Basic CPU Average Utilization** to the current dashboard.
     
   3. Edit the chart **Frontend - Basic CPU Average Utilization**, change its name to **Template Variable - Basic CPU Average Utilization**, and use the template variable `$Emperor Penguin Business Instance ID` as the filter condition. At this time, as the tag value of the template variable has not been selected, the chart preview page displays "No data yet." Then, save the chart.
      
   4. On the dashboard page, select or enter the tag value of the template variable `$Emperor Penguin Business Instance ID`, and the chart data will be dynamically displayed:
      - Selecting two instances
      
      - Selecting three instances
      
2. Adjust the Y-axis baseline to magnify the metric trend
- When a metric shows a significant offset, for example, when an extreme value that differs sharply from other data points is generated due to a sudden increase or decrease, the display of this sudden change in the chart may cause the display of the trends of other data curves in the chart to be less clear.
  
- In the **Chart Configuration** module, manually adjust the maximum or minimum value of the chart to enlarge some curves along the Y axis so that the metric trends will be displayed more clearly.
  

## Step 5: Configure Alarm Policies for Batch Resources

1. CVM resources are classified and managed by services and clusters in the project. The resources of different services or clusters reside in different projects.
2. Log in to the Cloud Monitor console and click **Alarm Configuration** > **Alarm Policy** to create alarm policies for resources. After the resources are grouped by project, you can create a default [alarm policy](https://intl.cloud.tencent.com/document/product/248/38908) for each project.
   The default alarm policy is automatically bound to all resources in the project. If resource changes occur, such as the purchase of resources, project changes, or resource termination upon expiration, by default, resource objects bound to the default policy will change accordingly, eliminating the need for complex manual maintenance.
