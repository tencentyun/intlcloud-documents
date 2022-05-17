## Overview
This document describes how to change the instance public IP in the Lighthouse console.

## Usage Limits
- You can change the public IP only once for each instance throughout its entire lifecycle.
- You can change instance public IPs only three times per day in each region, and this quota is shared with other Tencent Cloud products using general public IPs.
For example, if you have changed the public IP of three CVM instances in the Guangzhou region under your account, you cannot change Lighthouse instance public IPs on the same day in the same region under your account.
- If an instance IP is blocked due to DDoS attacks, you need to wait 24 hours until it is unblocked before changing it.
- If an instance is frozen, blocked, or to be repossessed, its public IP cannot be changed.
- The old public IP will be released and cannot be restored after the change.

## Directions

1. Log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index) and select the target instance.
2. On the instance details page, select **More** > **Change public IP** as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/20c188c29bb17cf2e3e23c4fac7306ab.png)
3. In the **Change public IP** pop-up window, click **OK**.
