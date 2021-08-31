Data subscription Kafka Edition supports the management of consumer groups, including password modification and consumer group deletion. This document describes how to modify the consumer group password and delete the consumer group in the console.

## Prerequisites
- You have created a [consumer group](https://intl.cloud.tencent.com/document/product/571/39534).

## Modifying the Password of Consumer Group
1. Log in to the [DTS console](https://console.cloud.tencent.com/dts/dss), select **Data Subscription** on the left sidebar to go to the **Data Subscription** page.
2. In the data subscription list, select a data subscription and click its name or **View Subscription Details** in the **Operation** column to go to the subscription management page.
3. Select the **Consumption Management** tab and click **Change Password** in the **Operation** column.
4. In the pop-up window, modify the password and click **Modify**.

## Deleting the Consumer Group
1. Log in to the [DTS console](https://console.cloud.tencent.com/dts/dss), select **Data Subscription** on the left sidebar to go to the **Data Subscription** page.
2. In the data subscription list, select a data subscription and click its name or **View Subscription Details** in the **Operation** column to go to the subscription management page.
3. Select the **Consumption Management** tab and click **Delete** in the **Operation** column.
4. In the pop-up dialog box, confirm that everything is correct and click **Confirm**.
>!After the consumer group is deleted, the consumption offset in the consumer group will be deleted, but the data in the data subscription will not be deleted.
