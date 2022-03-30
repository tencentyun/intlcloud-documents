## Overview
This document describes how to create a self-service instance detection and view the historical detection reports of an instance in the CVM console. If you encounter any problem when manipulating a CVM instance or want to fully understand the overall instance running status, you can perform a self-service instance detection to discover and solve problems.

## Usage Limits
If you need to perform multiple self-service instance detections on the same instance, the interval between two detections should be 5 minutes.

## Directions

### Creating self-service instance detection
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/instance/index?rid=1).
2. You can create a self-service instance detection in either of the following methods:
<dx-tabs>
::: Method 1
On the instance management page, proceed according to the used view mode:

#### List view
1. On the **Instance** page, select **More** > **OPS and Check** > **Self-Service Instance Detection** on the right of the row of the target instance.
2. In the **Self-Service Instance Detection** pop-up window, click **Start Detection**.


#### Tab view
Select the tab of the target instance and click **Start Detection** on the right.

:::
::: Method 2
1. Select **[Self-Service Instance Detection](https://console.cloud.tencent.com/cvm/diagnosis/index?rid=1)** on the left sidebar and click **Start Detection**.
2. In the **Self-Service Instance Detection** pop-up window, select the target instance and click **Start Detection**.
:::
</dx-tabs>
3. Wait for the detection result to be generated, which may take a while. If the result is displayed as shown below, the detection has been completed:
View the detection result and details as follows:
 - **Detection Result**: there are three types of results: **Normal**, **Risky**, and **Abnormal**. If there is any risk or exception, you can troubleshoot and fix it according to the provided suggestions.
 - **Detection Details**: the detection results of all items are displayed.

### Viewing historical detection report
Log in to the [CVM console](https://console.cloud.tencent.com/cvm/instance/index?rid=1) and click **[Self-Service Instance Detection](https://console.cloud.tencent.com/cvm/diagnosis/)** on the left sidebar to view the historical detection report information as needed.
- **View and filter historical detection reports**: on the **Self-Service Instance Detection** page, you can view historical detection reports. You can also use the search box above the list to filter reports by report or instance ID.
- **View historical detection report details**: click **View Report** on the right of the row of the target report to view the detection details. If there is any risk or exception, you can troubleshoot and fix it according to the provided suggestions.

## References
For more information on this tool, see [Self-Service Instance Detection](https://intl.cloud.tencent.com/document/product/213/45274).
