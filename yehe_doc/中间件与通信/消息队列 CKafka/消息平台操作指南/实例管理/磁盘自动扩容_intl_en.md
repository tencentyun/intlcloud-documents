## Overview

CKafka supports automatic adjustment of the disk utilization. After the disk utilization reaches the threshold, you can set the **Dynamic Message Retention Policy** to reduce the message retention time or set the **Automatic Disk Capacity Expansion** to adjust the disk space.

- Dynamic Message Retention Policy: After you set the message retention time, expired messages will be deleted. In case of message surges, normal production and consumption cannot be performed after the disk is full. If you set a dynamic retention policy, when the disk utilization reaches a certain percentage, a certain proportion of data will be automatically expired to avoid the above issue.
- Automatic Disk Capacity Expansion: When the disk load gets heavy, messages cannot be produced and consumed normally. After the automatic disk capacity expansion policy is set, when the disk load reaches the trigger threshold, the disk capacity will be automatically adjusted according to the policy, thus avoiding this problem.

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

1. Log in to the [CKafka console](https://console.intl.cloud.tencent.com/ckafka).
2. Click **Instance List** on the left sidebar and click the **ID/Name** of the target instance to enter the basic information page.
<<<<<<< HEAD
3. In the **Disk Utilization Policy** module on the instance's basic information page, enable **Dynamic Retention Policy**.
   <dx-alert infotype="explain" title="">
   The default dynamic policy reduces the message retention time by 10% when the disk load reaches 90%.
   </dx-alert>
   ![](https://qcloudimg.tencent-cloud.cn/raw/77e078fc3c63a467c8de2e32e39e999e.png)
4. Click **View** to view the message retention time of each topic.
   ![](https://main.qcloudimg.com/raw/9debb1aedbdb65461f17788276ef0202.png)
5. Click **Configure** in the **Operation** column of the dynamic retention policy to configure **Dynamic Policy** and **Minimum Retention Period**.
   ![](https://main.qcloudimg.com/raw/381d81ec44b0fccc326076fea03c9084.png)
   - Dynamic Policy: After message retention time adjustment is triggered, the broker will delete the oldest historical data according to the new retention time. This feature has a certain delay.
   - Minimum Retention Period: It can be 1 minute to 30 hours. If the dynamic retention period is lower than this parameter, no dynamic adjustment will be triggered.

6. Click **Adjustment Record** to view the dynamic adjustment records of the message retention period.
=======
3. In the **Disk Utilization Processing** module on the instance's basic information page, enable **Dynamic Message Retention Policy**.
<dx-alert infotype="explain" title="">
The default dynamic policy reduces the message retention time by 10% when the disk load reaches 90%.
</dx-alert>
4. Click **View** to view the message retention time of each topic.
5. Click **Configure** in the **Operation** column of the dynamic retention policy to configure **Policy** and **Minimum Time**.
   - Dynamic Policy: after message retention time adjustment is triggered, the broker will delete the oldest historical data according to the new retention time. This feature has a certain delay.
   - Minimum Retention Period: it can be 1 minute to 30 hours. If the dynamic retention time is lower than this parameter, no dynamic adjustment will be triggered.
>>>>>>> 4c0ee768bf0276e04d7ad55207e181473466eaf0

:::

::: Set the automatic disk capacity expansion policy

1. Log in to the [CKafka console](https://console.intl.cloud.tencent.com/ckafka).
2. Click **Instance List** on the left sidebar and click the **ID/Name** of the target instance to enter the basic information page.
<<<<<<< HEAD
3. In the **Disk Utilization Policy** module on the instance's basic information page, enable **Automatic Disk Capacity Expansion**.
   <dx-alert infotype="explain" title="">
   When the disk load reaches 90%, the disk capacity will be automatically expanded by 10% by default. The maximum disk capacity is 5,000 GB.
   </dx-alert>
    ![](https://qcloudimg.tencent-cloud.cn/raw/14e630c4b14e0d33b8658745d2cbed57.png)
4. Click **Configure** in the **Operation** column of the automatic disk capacity expansion policy to configure **Dynamic Policy** and **Max Disk Capacity**.
    ![](https://qcloudimg.tencent-cloud.cn/raw/ee2b8b36740b0286491a3e751faa9cc9.png)
   - Dynamic Policy: After the disk load reaches the trigger threshold, the disk capacity will be automatically adjusted according to the capacity expansion policy, with a certain delay.
     <dx-alert infotype="explain" title="">
     The disk capacity will be expanded in increments of 100 GB.
     </dx-alert>
   - Maximum Disk Capacity: Automatic disk capacity expansion will no longer be triggered after the disk capacity is expanded to this value.

5. Click **Adjustment Record** to view the adjustment records of automatic disk expansion.
=======
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
>>>>>>> 4c0ee768bf0276e04d7ad55207e181473466eaf0

:::
</dx-tabs>

