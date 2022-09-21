## Overview

Data Subscription Kafka Edition supports consumer group management, including password change, consumer group deletion, and consumption offset modification.

In addition, you can view information such as client ID (the ID of the client consuming the data), partition ID, consumption offset, and consumption delay in **Consumption Management**.

## Prerequisites

- You have created a consumer group as instructed in [Adding Consumer Group](https://intl.cloud.tencent.com/document/product/571/39534).

## Notes

If other Kafka clients are consuming the data in the same consumer group, the consumption offset cannot be modified.

## Modifying the password of a consumer group
1. Log in to the [DTS console](https://console.cloud.tencent.com/dts/dss) and select **Data Subscription** on the left sidebar to enter the data subscription page.
2. In the data subscription list, select the target data subscription, click the subscription name or **View Subscription Details** in the **Operation** column.
3. On the subscription management page, select the **Consumption Management** tab and click **Change Password** in the **Operation** column.
4. In the pop-up window, click **Modify** and change the password.

## Deleting a consumer group
1. Log in to the [DTS console](https://console.cloud.tencent.com/dts/dss) and select **Data Subscription** on the left sidebar to enter the data subscription page.
2. In the data subscription list, select the target data subscription, click the subscription name or **View Subscription Details** in the **Operation** column.
3. On the subscription management page, select the **Consumption Management** tab and click **Delete** in the **Operation** column.
4. In the pop-up window, confirm that everything is correct and click **OK**.
>!After the consumer group is deleted, the consumption offset in the consumer group will be deleted, but the data in the data subscription will not. Proceed with caution.

## Modifying the consumption offset

1. Log in to the [DTS console](https://console.cloud.tencent.com/dts/dss) and select **Data Subscription** on the left sidebar to enter the data subscription page.
2. In the data subscription list, select the target data subscription, click the subscription name or **View Subscription Details** in the **Operation** column.
3. On the subscription management page, select the **Consumption Management** tab, select the target consumer group, and click **Modify Offset**.
4. In the pop-up window, select the offset object and click **Next**.	
5. Set the reset method of data consumption and click **Done**.
 - From latest offset: Reset the consumption offset to the latest offset of Kafka messages.
 - From start offset: Reset the consumption offset to the earliest offset from where Kafka messages start to be stored.
 - From specified time point: You can enter a time, and DTS will find the consumption offset corresponding to the entered time to start consumption.
   If the configured time point is after the Kafka message time, the consumption offset will be the maximum offset of Kafka messages; otherwise, the consumption offset will be the minimum offset of Kafka messages.	
   

