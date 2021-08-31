Data subscription Kafka Edition allows users to create multiple consumer groups for multi-point consumption. By creating multiple consumption groups, you can consume for multiple times and increase consumption channels to reduce usage costs and improve the data consumption speed.

## Prerequisites
- You have created the [Data Subscription Kafka Edition](https://intl.cloud.tencent.com/document/product/571/39531).
>?In the data subscription list, the subscription with the "Kafka Edition" tag is the data subscription in Kafka edition.

## Notes
- The data subscription task must be in the running status.
- A data subscription task can contain up to 10 consumer groups.
- A consumer group can only have one consumer for consumption.

## Directions
1. Log in to the [DTS console](https://console.cloud.tencent.com/dts/dss), select **Data Subscription** on the left sidebar to go to the **Data Subscription** page.
2. In the data subscription list, select a data subscription and click its name or **View Subscription Details** in the **Operation** column to go to the subscription management page.
3. In the subscription management page, select the **Consumption Management** tab and click **Create Consumer Group**.
4. In the pop-up window, set the consumer group information and click **Create**.
 - Consumer Group Name: set the consumer group name as needed.
 - Account: set the consumer group account.
 - Password: set the password of the consumer group account.
 - Confirm Password: enter the same password again.
 - Remarks: set the remarks to record the information.

