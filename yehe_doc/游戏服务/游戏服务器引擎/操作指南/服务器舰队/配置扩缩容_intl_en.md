## Overview

This document describes how to configure a scaling policy after a server fleet is successfully deployed. The size of a server fleet is subject to the number of instances contained in it. You can also set the lower and upper limits based on the actual needs of your game. No matter whether you choose manual or automatic adjustment, the target capacity in any server fleet capacity change requests cannot be out of the current limit range.

## Prerequisites

You have completed the [GSE Application Form](https://intl.cloud.tencent.com/apply/p/k0b6pvbhs6), your application has been approved, and you have created a server fleet.

## Directions
1. Log in to the [GSE Console](https://console.cloud.tencent.com/gse/asset) and create a server fleet. For more information, please see [Creating Server Fleets](https://intl.cloud.tencent.com/document/product/1055/36675).
2. Click the **ID** of the created server fleet to enter the fleet details page. Click the **Scaling** tab to enter the expansion/reduction page.
3. Click **Modify** to enter the scaling policy modification page.
![](https://main.qcloudimg.com/raw/3d8e50656ea65a74ca73e60891476218.png)
   The adjustment modes of a scaling policy include manual adjustment and automatic adjustment.
	
#### Manual adjustment
   - Instance Range: it is in the format of minimum number of instances–maximum number of instances and is in integer type. The desired quantity should not exceed the specified instance range. If the first deployment of asset package fails, you can set this field to 0–1 only.
   - Desired Quantity: it takes effect for manual adjustment. After being configured, it will become the only metric based on which the instance quantity will be adjusted.
![](https://main.qcloudimg.com/raw/b315efc4b2e248211461455befdab5a1.png)

#### Automatic adjustment
   - Instance Range: it is in the format of minimum number of instances–maximum number of instances and is in integer type. Automatic adjustment cannot exceed the specified instance range. In each account, the max number of instances for each fleet combined in a single region cannot exceed the regional quota. You can view regional quotas [here](https://intl.cloud.tencent.com/document/product/1055/36672). To increase the CVM instance quota, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application. You cannot set this field if the first deployment of asset package fails.
   - Desired Quantity: generally, this metric does not take effect in automatic adjustment. However, if the game server session buffer and other automatic adjustment policies are not configured, the system will adjust the number of instances with this metric.
   - Game Server Session Buffer: this metric represents the proportion of reserved idle resources of the game server session, and automatic adjustment will be performed for scaling with it. It is an integer ranging from 1 to 99 in %. For example, if it is configured as 15%, expansion will start when the server resource utilization reaches 85%.
   - Scaling Cooldown Time:  this metric indicates the time interval between two scaling operations. It can be set from 3 to 30 minutes, which is determined by the duration of the server's process launch.
      ![](https://main.qcloudimg.com/raw/0d3d65b91fe5a63857eb2964b215b31e.png)



