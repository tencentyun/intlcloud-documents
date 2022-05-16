## Overview

CKafka supports automatic adjustment of the disk utilization. After the disk utilization reaches the threshold, you can set the **dynamic retention policy** to reduce the message retention time or set the **automatic disk capacity expansion policy** to adjust the disk space.
- Dynamic message retention: after you set the message retention time, expired messages will be deleted. In case of message surges, normal production and consumption cannot be performed after the disk is full. If you set a dynamic retention policy, when the disk utilization reaches a certain percentage, a certain proportion of data will be automatically expired to avoid the above issue.
- Automatic disk capacity expansion: when the disk load gets heavy, messages cannot be produced and consumed normally. After the automatic disk capacity expansion policy is set, when the disk load reaches the trigger threshold, the disk capacity will be automatically adjusted according to the policy, thus avoiding this problem.

| Policy     | Supported by CKafka Standard Edition | Supported by CKafka Pro Edition |
| ------------ | --------------------- | --------------------- |
| Dynamic message retention | Yes                    | Yes                    |
| Automatic disk capacity expansion | No                    | Yes                    |



<dx-alert infotype="explain" title="">
You can enable either dynamic message retention or automatic disk capacity expansion at any time.
</dx-alert>



## Directions

<dx-tabs>

::: Set the dynamic message retention policy

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. Click **Instance List** on the left sidebar and click the **ID/Name** of the target instance to enter the basic information page.
3. In the **Disk Utilization Processing** module on the instance's basic information page, enable **Dynamic Message Retention Policy**.
<dx-alert infotype="explain" title="">
The default dynamic policy reduces the message retention time by 10% when the disk load reaches 90%.
</dx-alert>
4. Click **View** to view the message retention time of each topic.
5. Click **Configure** in the **Operation** column of the dynamic retention policy to configure **Policy** and **Minimum Time**.
   - Dynamic Policy: after message retention time adjustment is triggered, the broker will delete the oldest historical data according to the new retention time. This feature has a certain delay.
   - Minimum Time: it can be 1 minute to 30 hours. If the dynamic retention time is lower than this parameter, no dynamic adjustment will be triggered.

:::

::: Set the automatic disk capacity expansion policy

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. Click **Instance List** on the left sidebar and click the **ID/Name** of the target instance to enter the basic information page.
3. In the **Disk Utilization Processing** module on the instance's basic information page, enable **Automatic Disk Capacity Expansion**.
<dx-alert infotype="explain" title="">
When the disk load reaches 90%, the disk capacity will be automatically expanded by 10% by default. The maximum disk capacity is 5,000 GB.
</dx-alert>
4. Click **Configure** in the **Operation** column of the automatic disk capacity expansion policy to configure **Policy** and **Maximum Disk Capacity**.
   - Dynamic Policy: after the disk load reaches the trigger threshold, the disk capacity will be automatically adjusted according to the capacity expansion policy, with a certain delay.
<dx-alert infotype="explain" title="">
The disk capacity will be expanded in increments of 100 GB.
</dx-alert>
   - Maximum Disk Capacity: automatic disk capacity expansion will no longer be triggered after the disk capacity is expanded to this value.

:::
</dx-tabs>
