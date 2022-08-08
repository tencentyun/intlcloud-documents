## Feature overview
The HBase RIT fixing feature is suitable for fixing regions in the `FAILED_OPEN`, `FAILED_CLOSED`, or `CLOSING` status when an HBase 2.2.0 or later cluster encounters prolonged Region-In-Transition (RIT) issues.

## Directions
1. Log in to the [EMR console](https://console.cloud.tencent.com/emr) and click a **cluster ID/name** in the **Cluster list** to enter the cluster details page.
2. On the cluster details page, click **Cluster Service** and select **Operation** > **RIT fixing** in the top-right corner of the HBase component panel to view and fix regions in the RIT status.
![](https://qcloudimg.tencent-cloud.cn/raw/5487f3cb623241d878e791c1bb57810b.png)
3. In the list, click **Fix** in the **Operation** column, or select the target regions and click **Batch fix**, and confirm the information in the **RIT fixing** pop-up window.
4. After confirming that everything is incorrect, click **Confirm**.
5. You can view the progress and result of RIT fixing in the **Task Center**.

