

## Overview

This document describes how to configure the scheduled update plan for auto-scaling policy after you deploy the server fleet successfully.

## Prerequisites

You have [created a server fleet](https://intl.cloud.tencent.com/document/product/1055/36675).

## Directions

 1. Log in to the [GSE console](https://console.cloud.tencent.com/gse/asset) and click **Fleet** on the left sidebar.  
 2. Click the **ID** of the created server fleet to enter the fleet details page. Click the **Scaling** tab to enter the scaling page.  
 3. Click **Add** in the **Scheduled Update Plan for Scaling Policy** section.
<img src="https://main.qcloudimg.com/raw/a10d330f8878dc8b7160a6867b4636a7.png" style="width: 75%;"></img>

**The scheduled update plan for scaling policy includes the setting of auto scaling policy and repeat cycle.**

### Auto scaling policy

The adjustment mode of the auto scaling policy includes automatic adjustment and manual adjustment.

#### Manual adjustment

![](https://main.qcloudimg.com/raw/0398e4e0179c34df462f9f741bd56b95.png)
- **Instance Range**: it is in the format of minimum number of instances – maximum number of instances and is in integer type. The desired quantity should not exceed the specified instance range. If the first deployment of asset package fails, you can set this field to 0–1 only.
- **Desired Quantity**: it takes effect for manual adjustment. After being configured, it will become the only metric based on which the instance quantity will be adjusted.
- **Scaling Cooldown Time**: indicates the time interval between two scaling operations. It can be set from 1 to 30 minutes, which is determined by the duration of the server's process launch.


#### Automatic adjustment

![](https://main.qcloudimg.com/raw/15659ee5abe5b8f1777869c20380dfe8.png)
- **Instance Range**: it is in the format of minimum number of instances – maximum number of instances and is in integer type. Automatic adjustment cannot exceed the specified instance range. You cannot set this field if the first deployment of asset package fails.
- **Desired Quantity**: generally, this metric does not take effect in automatic adjustment. However, if the game server session buffer and other automatic adjustment policies are not configured, GSE will adjust the number of instances with this metric.
- **Game Server Session Buffer**: represents the proportion of reserved idle instance resources for game server sessions, and automatic adjustment will scale with it.  
- **Scaling Cooldown Time**: indicates the time interval between two scaling operations. It can be set from 1 to 30 minutes, which is determined by the duration of the server's process launch.


>? The sum of max instance range in a single region of an account cannot exceed the highest quota of each region. You can view the regional quotas in [Resource Limits](https://intl.cloud.tencent.com/document/product/1055/36672). To increase the CVM instance quota, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).

### Repeat cycle

- __Repeat Cycle__: the scaling policy can be executed once, or can be repeated daily, weekly, and monthly.
- __Execution Start Time__: the start time of the scheduled update plan for scaling policy.
  1. If you select **Once** for the **Repeat Cycle**, the scaling policy will be executed once based on the specific time that you choose.
![](https://main.qcloudimg.com/raw/dca9ef7012e0a1dbdc8a76f24742205b.png)
  As shown in the figure below, the scaling policy will be executed once at 2021-06-17 15:31.
  ![](https://main.qcloudimg.com/raw/ff98720b4f84815e87532e1fd9b7411a.png)
  2. If you select **By Day** for the **Repeat Cycle**, the scaling policy will be executed every N days based on the execution period that you choose.
![](https://main.qcloudimg.com/raw/efb25c897db636319fdf0af4a8ca1070.png)
  As shown in the figure below, the scaling policy will be executed every other day from 2021-06-17 15:36 to 2022-06-17 15:36.
![](https://main.qcloudimg.com/raw/f304847d5fa18c7ca919110a0aaba72c.png)
  3. If you select **By Week** for the **Repeat Cycle**, the scaling policy will be executed every week (based on the selected days) in the execution period that you choose.
![](https://main.qcloudimg.com/raw/17cf7487f13fc8635178a43265b69e9d.png)
  As shown in the figure below, the scaling policy will be executed every Monday and Wednesday from 2021-06-17 15:38 to 2022-06-17 15:38.
  ![](https://main.qcloudimg.com/raw/ee160284a9293ef2b2d9b5a7619699b1.png)
  4. If you select **By Month** for the **Repeat Cycle**, the scaling policy will be executed on the day N to the day M of each month in the execution period that you choose.
![](https://main.qcloudimg.com/raw/9f2601e167af0d41f7bed19e69798300.png)
  As shown in the figure below, the scaling policy will be executed on the 3rd to 5th day of each month from 2021-06-17 15:39 to 2022-06-17 15:39.
![](https://main.qcloudimg.com/raw/f2e5326ec530d4319492c312ca7baae1.png)


 4. Click **Confirm**. After creating the policy, you can view, modify or delete it or perform other operations in the **Server Fleet Details** > **Scaling** page.
![](https://main.qcloudimg.com/raw/3350e721c9795333d4819216760fbaa1.png)















