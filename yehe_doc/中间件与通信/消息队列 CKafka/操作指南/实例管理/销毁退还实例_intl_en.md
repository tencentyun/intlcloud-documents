## Overview

If you no longer need a CKafka instance, you can terminate and release it.

The lifecycle of a CKafka instance refers to all statuses from the start of the instance to its release. Properly managing an instance in different statuses can ensure that applications running on it can provide services economically and efficiently. The statuses of an instance are as follows:

| Status | Status Attribute | Description |
| -------- | -------- | ------------------------------------------------------------ |
| Creating | Intermediate status | The instance has been created but is not running yet. |
| <nobr>Running</nobr> | <nobr>Steady status</nobr> | The instance is running normally, and the disk space, traffic, and the number of connections are all within the normal range. |
| Deleting | Intermediate status | The instance is being deleted through the console or API. |
| Isolated | Intermediate status | The instance is isolated through the console or API, or your overdue instance is in a seven-day isolation status. |
| Failed to create | Intermediate status | You have purchased an instance through the console or API but are not assigned the instance. In this case, please [submit a ticket](https://console.cloud.tencent.com/workorder/category). |
| Failed to delete | Steady status | CKafka fails to release resources after the instance is manually deleted or is not renewed 14 days after expiration (including the 14th day). |

## Directions

### Manual termination

You can manually terminate a monthly-subscribed instance before it expires by following the steps below:

1. Log in to the [CKafka Console](https://console.cloud.tencent.com/ckafka).
2. On the instance list page, select **More** > **Terminate** in the **Operation** column.
3. In the pop-up window, click **Submit** to terminate the instance.
   ![](https://main.qcloudimg.com/raw/05cef4bc7b69d2f68c1f2367ecdfd7fa.png)
> !
> - After a monthly-subscribed instance is terminated, it will be in “Isolated” status for seven days in the CKafka console. It will be completely released after 14 days (including the 14th day).
> - Isolated instances cannot produce or consume data. Data and configurations saved in CKafka will not be terminated, but **expired messages will still be automatically deleted according to the open-source Kafka mechanism**.
> - For instances in the seven-day isolation status, you can go to the CKafka console to renew them by clicking **Renew** in the **Operation** column on the instance list page. Successfully renewed instances can go back to the running status and be normally used.

### Automatic termination upon expiration/overdue payment

Monthly-subscribed instances can be retained in the CKafka console for up to seven natural days after they expire or have overdue payments. You can continue to use them if you renew them within 7-14 days after expiration. For details, see [Payment Overdue](https://intl.cloud.tencent.com/document/product/597/34248). 

- If the CKafka instance is not renewed within 14 days (including the 14th day) after expiration, its resources will be released at 00:00:00 on the 15th day after expiration, and data in it will be cleared and cannot be recovered.

### Deleting instances

A monthly-subscribed instance will be retained for seven days in the CKafka console after manual termination or automatic termination upon expiration/overdue payment, during which it will be in “Isolated” status. After 14 days (including the 14th day), it will be completely released, and you can delete it completely.

>!Once the instance is deleted, all data in it will be cleared and cannot be recovered. Please back up the data in advance.

1. Log in to the [CKafka Console](https://console.cloud.tencent.com/ckafka).
2. On the instance list page, select **More** > **Terminate** in the **Operation** column.
3. In the pop-up window, click **Submit** to delete the instance.
   ![](https://main.qcloudimg.com/raw/166e8127c0f30f409415519999f47a8b.png)
