## Overview

CKafka supports dynamic partition processing. After you enable **Auto Partition Balancing**, CKafka will automatically check and analyze the partition distribution of topics on your specified time, and then select a time during off-peak hours to initiate partition balancing.

<dx-alert infotype="explain" title="">
This feature is only available for CKafka Pro Edition instances.
</dx-alert>



## Directions

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. Click **Instance List** on the left sidebar and click the **ID/Name** of the target instance to enter the basic information page.
3. Select the **Smart Ops** tab at the top and click **Elastic Scaling**.
4. In the **Dynamic Partition Processing** module, enable **Auto Partition Balancing**.
5. Click **Configure** in the **Operation** column to set the automatic partition balancing policy.
   - Custom time: You can customize the time to initiate partition balancing. We recommend you select a time during off-peak hours to avoid affecting your business.
   - Auto time: CKafka will select the time to initiate partition balancing during off-peak hours calculated by automatic analysis.
6. Click **Adjustment Record** to view the adjustment records of automatic partition balancing.
