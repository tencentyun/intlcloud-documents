Data subscription Kafka edition supports dynamic increase or decrease of the subscribed objects during data consumption. This document describes how to modify the subscribed object of the data subscription Kafka edition in the console.

## Prerequisites
- You have created the [Data Subscription Kafka Edition](https://intl.cloud.tencent.com/document/product/571/39531).

## Directions
1. Log in to the [DTS console](https://console.cloud.tencent.com/dts/dss), select **Data Subscription** on the left sidebar to go to the **Data Subscription** page.
2. In the data subscription list, select a data subscription and select **More** > **Modify subscribed object** in the **Operation** column to go to the **Configure data subscription** page.
3. In the **Configure data subscription** page, select the subscription type, edit the subscribed object, and click **Save**.
4. Return to the subscription list, the subscription instance enters the “enabling” state, and the task is pre-checked and initialized. After being enabled, the subscription instance enters the running state, and the Kafka client can be used to consume the subscription data.
