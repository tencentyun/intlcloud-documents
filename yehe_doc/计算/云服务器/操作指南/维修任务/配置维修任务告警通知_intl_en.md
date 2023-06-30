## Overview

This document describes how to use [EventBridge](https://www.tencentcloud.com/document/product/1108/42267) to set alarm notification for a CVM instance in the EventBridge console. You can set alarm notification for the maintenance tasks of a CVM instance, so that you will be notified immediately that you need to take countermeasures through channels such as email, SMS, and phone call when an exception occurs.

## Directions
1. Log in to the [EventBridge console](https://console.cloud.tencent.com/eb) and activate the service as instructed in [Activating EventBridge](https://www.tencentcloud.com/document/product/1108/42272).
2. Select **[Event Rule](https://console.cloud.tencent.com/eb/rule)** on the left sidebar, select the target region and event bus at the top of the **Event Rule** page, and click **Create Event Rule**.
3. On the **Create Event Rule** page, perform the following operations:
    i. In **Basic Information**, set the **Rule Name** parameter as shown below:
 ![](https://staticintl.cloudcachetci.com/yehe/backend-news/zHwA899_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230421102346.png)
    ii. In **Event Pattern**, set **Event Matching** parameters as needed as shown below:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/bQp2060_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230421102608.png)
       - **Tencent Cloud service**: Select **CVM** from the drop-down list.
       - **Event Type**: Select an option as needed from the drop-down list.
   iii. Click **Next**.
   iv. In **Delivery target**, select an option as needed from the **Trigger method** drop-down list.
      - Select **CLS** for **Trigger method**. For more information, see [CLS Log Target](https://intl.cloud.tencent.com/document/product/1108/46992).
      - Select **Notification message** for **Trigger method**. For more information, see [Message Push Target](https://intl.cloud.tencent.com/document/product/1108/46779).
4. Click **Complete**.
