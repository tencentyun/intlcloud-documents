## Overview
Tencent Cloud can analyze your CVM instance load based on the monitoring metrics including CPU and memory utilization collected by CM in the past three days and give suggestions on how to adjust the instance configuration. You can determine whether to adjust the instance configuration based on the actual conditions.


## Notes
- The instance configuration adjustment suggestions are made based on the average load data (collected once every 5 minutes) for the last three days and are applicable to instances with a stable load rather than those with CPU or memory utilization spikes.
- This feature isn't supported for heterogeneous models such as GPU and FPGA as well as CPM. You can [create alarms](https://intl.cloud.tencent.com/document/product/213/5179) to actively monitor the instance usage.
- The suggestions are for reference only. If you have high requirements for instance usage monitoring, we recommend you use [CM](https://intl.cloud.tencent.com/document/product/248/32799) for active monitoring.

## Directions
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/instance/index?rid=1) and enter the instance list page.
2. On the instance list page, if the <img src="https://main.qcloudimg.com/raw/b966dd0b540ed2caa752be60c0f99230.png" style="margin:-6px 0px" width="20px"> warning icon is displayed in the monitoring column of an instance, configuration adjustment suggestions have been given for it.
3. Click the <img src="https://main.qcloudimg.com/raw/b966dd0b540ed2caa752be60c0f99230.png" style="margin:-6px 0px" width="20px"> warning icon, and the **Configuration Adjustment Suggestion** window pops up.
4. In the **Configuration Adjustment Suggestions** window, you can view the target model recommended based on the current instance usage and select **Show More** to view other recommended models.
5. If you want to adjust the instance configuration according to the suggestions, select **I have read and agree to the description of instance configuration fees** and click **Start Adjustment**.

