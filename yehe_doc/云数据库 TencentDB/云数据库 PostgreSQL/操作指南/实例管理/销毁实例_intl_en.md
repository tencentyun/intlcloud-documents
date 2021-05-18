This document describes how to terminate a TencentDB for PostgreSQL instance in the console.

## Overview
You can manually terminate instances at any time as needed. Terminated instances will be moved to the recycle bin. Monthly-subscribed instances will be refunded after termination.

## Notes
- If a pay-as-you-go instance is terminated, it will be moved to the recycle bin and retained there for up to three days. The instance in the recycle bin is in the "Isolated" status and cannot be accessed.
  - To use the instance again, you can restore it from the recycle bin.
  - If the instance in the recycle bin is no longer needed, you can eliminate it.
- After the instance is eliminated, its data and backup files will also be deleted and cannot be restored in the cloud. Please store your backup files safely elsewhere in advance.
- If a primary instance has one or more read-only instances, terminating the primary instance won't affect the read-only instances, but eliminating the primary instance will eliminate the read-only instances at the same time. To prevent instances from being eliminated due to overdue payment, please pay attention to the instance expiration information.
- If a pay-as-you-go instance is terminated, its billing stops.
 - For monthly-subscribed instances that met the 5-day no-questions-asked refund policy, the payment will be returned to the original payment account after the termination.
 - For normal monthly-subscribed instances, the payment will be returned to your Tencent Cloud account by the proportion of the cash and gift cards paid for the purchase after the termination.
 - For an order placed from promotion rewarding channels, 25% of the actual cash payment amount will be deducted from the refund amount as a refund handling fee. Currently, self-service refund is unavailable for such kind of orders, and the refund application should be initiated by [submitting a ticket](https://console.cloud.tencent.com/workorder/category).

## Directions
1. Log in to the [TencentDB for PostgreSQL console](https://console.cloud.tencent.com/postgres), locate the instance to be terminated in the instance list, and click **More** > **Terminate Instance** in the **Operation** column.
2. In the pop-up dialog box, indicate your consent and click **Terminate Now**.
   ![](https://main.qcloudimg.com/raw/eee2085b2ede55bf5369e56a68524f71.png)
