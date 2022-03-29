>!Since the product logic no longer meets the technical development of game industry, Game Player Matching GPM will be deprecated on June 1st, 2022. Please complete service migration before May 31 , 2022.

This document describes how to view GPM's metric monitoring and configure alarms.

## Prerequisites

- You have [created a match](https://intl.cloud.tencent.com/document/product/1072/39203).
- Your account has full access permission to **Cloud Monitor (CM)**. For Cloud Monitor permission configurations, please see [Cloud Access Management](https://intl.cloud.tencent.com/document/product/248/36744).

## Viewing Metric Monitoring

### Step 1: log in to the Cloud Monitor console.

GPM metric data will be reported to **Cloud Monitor**. You need to log in to [Cloud Monitor console](https://console.cloud.tencent.com/monitor/overview) to view the metric data.

### Step 2: Creating a GPM dashboard

In Cloud Monitor console, click **Dashboard** > **Dashboard List** in the left sidebar to go to the **Dashboard List** page. Click **Create Dashboard**.
![](https://main.qcloudimg.com/raw/4d4547948acfe1c8120227a147740d1b.png)

### Step 3: Create a GPM chart.

Click **Create Chart**, select the metrics to monitor, and complete the chart information configuration.
![](https://main.qcloudimg.com/raw/56c530e9f929842eee6aae4111c187e4.png)
As shown in the figure below:

1. Select **Game Player Matchmaking** in the **Metric** drop-down box and select a monitoring metric (Here takes "Matching Success Rate (%)" as an example).
2. Select **Instance** in the **Filter** drop-down box and select the MatchCode to monitor.
>!Before selecting the MatchCode to monitor, you need to make sure that the "region" you select is the same as the "region" where the MatchCode was created. You can only select the MatchCode to which the current account has access permission.
>![](https://main.qcloudimg.com/raw/f874212cc51539e40b78506277108400.png)
3. In **Chart Name**, enter the chart name.
4. Click **Save** on the top-right corner. In the pop-up window, enter the **Dashboard Name**, and select the **Folder**.
![](https://main.qcloudimg.com/raw/89a9feb2bde8e34e357e87ccb9bf11b0.png)
5. Click **OK** to complete the creation of the metric monitoring chart.

### Step 4: View the monitoring data through the created chart.

Go to the directory where the your **Dashboard** is located through the [Dashboard List](https://console.cloud.tencent.com/monitor/dashboard2/dashboards).
- You can select a dashboard and click **Settings** in the **Operation** column to modify the dashboard name.
![](https://main.qcloudimg.com/raw/1f8a06e485817aad0e27e49a70511ed4.png)
- You can click a dashboard name to view all charts configured under the current dashboard. When the MatchCode you are monitoring has request records, the chart will display the corresponding data.
![](https://main.qcloudimg.com/raw/0cdc66c6f5e22468d91ed6477226e0f8.png)




## Configuring Metric Alarms

### Step 1: Enter the **Alarm Policy** page.
1. Log in to the [Cloud Monitor console](https://console.cloud.tencent.com/monitor/overview) and select **Alarm Configuration** > **Alarm Policy** to go to the **Alarm Policy** page.
2. Click **Create** to go to the **Create Alarm Policy** page.
![](https://main.qcloudimg.com/raw/f0277fefee102dbef36a1fcce62ab802.png)

### Step 2: Create an alarm policy.

![](https://main.qcloudimg.com/raw/6b13f5f5aa7fb36f04128c9beba52d04.png)
As shown in the figure below:

1. Enter the alarm policy name in **Policy Name**.
2. Select **Game Play Matchmaking** in the drop-down list of **Policy Type**.
3. Select the MatchCode that needs alarms in the drop-down list of **Alarm Object**.
4. Select the alarm metric in **Metric Alarm**. You can select a single metric or multiple metrics to configure the alarm policy.
5. In **Configure Alarm Notification** section, you can select the existing template or create a template to configure the recipient and receiving channel for the alarm notification.
6. Click **Complete**, and the alarm policy will take effect. When the configured alarm condition is met, an alarm notification will be triggered automatically.

