## Overview

This document describes how to use [EventBridge](https://intl.cloud.tencent.com/document/product/1108/42267) to set a CVM instance event alarm in the CVM console. You can set an alarm for a CVM instance maintenance task, so that you will be notified immediately that you need to take countermeasures through channels such as WeChat, email, SMS, and phone when an exception occurs.



## Directions
1. Log in to the [EventBridge console](https://console.cloud.tencent.com/eb) and activate the service as instructed in [Activating EventBridge](https://intl.cloud.tencent.com/document/product/1108/42272).
2. Select **[Event Rule](https://console.cloud.tencent.com/eb/rule)** on the left sidebar, select the target region and event bus at the top of the **Event Rule** page, and click **Create Event Rule**.
3. On the **Create Event Rule** page:
 1. In **Event Pattern**, set **Event Matching** parameters as needed as shown below:
    ![](https://qcloudimg.tencent-cloud.cn/raw/25c14455b34298bd11db850fd4c0d2a4.png)
    - **Tencent Cloud service**: select **CVM** in the drop-down list.
    - **Event Type**: select **CVM storage problem**, **CVM connection problem**, and **CVM running exception** as needed in the drop-down list.
  2. Click **Next**.
  3. In **Delivery Target**, configure the push target. You can configure a delivery target for an event alarm as needed: CLS or notification message.

    - Select **CLS** for **Trigger method**.
    - Select **Notification message** for **Trigger method**.
4. Click **Complete**.
