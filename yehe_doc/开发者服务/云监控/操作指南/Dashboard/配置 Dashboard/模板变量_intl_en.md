
This document describes how to configure and use template variables.



## Configuring a Template Variable

1. Log in to the [CM console](https://console.cloud.tencent.com/monitor).
2. On the left sidebar, click **Dashboard List** to enter the dashboard list page.
3. In the top-left corner of the dashboard list, click **Create** to enter the dashboard creation page.
4. Click ![](https://main.qcloudimg.com/raw/8e26fe2eacdd794457a53a745bd48f3c.png) or click **Set** on the dashboard list page to enter the global dashboard configuration page.
5. Click **Template Variable**. You can customize dashboard filters and use template variables on the dashboard management page as instructed in [Using a Template Variable](#step1). Currently, filtering by tags of CVM - basic monitoring, storage monitoring, and TencentDB for MySQL source/replica server monitoring is supported.
6. Click **Create** on the dashboard management page, configure parameters, and click **OK** to create a template variable.
   ![](https://main.qcloudimg.com/raw/a21d393bbb522c419de4711e118f1774.png)		 

## Editing/Deleting a Template Variable

You can delete and edit template variables in the template variable list.
![](https://main.qcloudimg.com/raw/6b0b000cc5956e2e9c8356927582705e.png)

[](id:step1)

## Using a Template Variable

1. Log in to the [CM console](https://console.cloud.tencent.com/monitor).
2. On the left sidebar, click **Dashboard List** to enter the dashboard list page.
3. Find the target dashboard and click its name.
4. After creating a template variable, you can use it as a quick selector of dashboards and monitoring charts.
 i. Select the template variable and corresponding template in the **Create Monitoring Chart** or **Edit Monitoring Chart** column.
    ![](https://qcloudimg.tencent-cloud.cn/raw/10094cb1694fe58d6b2a4193a5b0f240.png)
    ii. After successfully binding the template variable, you can use the instance filter in the dashboard for the chart to quickly filter instances as shown below:
    The chart bound to the template variable can be linked with the instance filter for you to quickly filter instances and view the instance monitoring data under the product type.
    ![](https://qcloudimg.tencent-cloud.cn/raw/6f710c4909e1a0d0d1ad470dd48ef962.png)
