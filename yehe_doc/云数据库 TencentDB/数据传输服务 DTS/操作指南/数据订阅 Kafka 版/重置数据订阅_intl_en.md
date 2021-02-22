Data subscription Kafka edition supports resetting the subscription task to remove the information and data of the current subscription instance, and reconfiguring the data subscription task. This document describes how to reset the data subscription in the console.

## Prerequisites
- You have created the [Data Subscription Kafka Edition](https://intl.cloud.tencent.com/document/product/571/39531).
- The state of the data subscription is “running” or “abnormal”.

## Directions 
1. Log in to the [DTS console](https://console.cloud.tencent.com/dts/dss), select **Data Subscription** on the left sidebar to go to the **Data Subscription** page.
2. In the data subscription list, select a data subscription and select **More** > **Reset subscription** in the **Operation** column.
3. In the pop-up dialog box, confirm that everything is correct and click **Confirm**.
>!
>- After the subscription is reset, the binding relationship between the subscription instance and the source instance will be unassociated, and the state of the instance will become “not started”. You can perform the initialization configuration again.
>- The subscription to the incremental data of the source database will be stopped once the subscription is reset, and the incremental data stored in the subscription will be deleted.
4. In the data subscription list, click **Configure Subscription** in the **Operation** column to reconfigure the subscription task.
