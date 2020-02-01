## Scenario

Tencent Cloud provides cloud monitoring for all users by default, no need for the user to manually turn on. But the user must use Tencent Cloud products before cloud monitoring can begin to collect monitoring data; to view these monitoring data, there are several ways:

## Directions
### Obtain monitoring data from the cloud product console

Some cloud products provide a separate monitoring data reading tab on their own console pages. CVM is used in this example

1. Open [Tencent Cloud Console](https://console.cloud.tencent.com), select **CVM**.

2. Click the CVM Instance ID from the list of CVMs to view the monitoring data, and enter the CVM details page.

3. Click the **Monitor** tab; on this page, you can view the CPU, memory, network bandwidth, disk and monitoring data, etc. of the CVM instance. You can also freely adjust the time range.


### Obtain monitoring data from Cloud Monitor Console
On Cloud Monitoring console, you can view monitoring data for most of the products used. In this case, CVM is used as an example.

1. Open [Tencent Cloud Console](https://console.cloud.tencent.com), select **Basic Cloud Monitor**.

2) On the left navigation bar, select **Cloud Product Monitoring - Cloud Virtual Machine**.

3) Click the CVM Instance ID from the list of CVMs displayed to view the monitoring data, and enter the monitoring details page.

4) On this page, you can view the CPU, memory, network bandwidth, disk and all monitoring data of the CVM instance. You can also freely adjust the time range.

## Obtain monitoring data through the API
Users can use the GetMonitorData API to obtain monitoring data for all products.


