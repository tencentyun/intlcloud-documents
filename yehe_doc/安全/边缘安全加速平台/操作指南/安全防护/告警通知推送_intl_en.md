## Overview
To be notified of DDoS attacks against the DDoS mitigation Enterprise plan (site access and layer-4 proxy services), you can set an alarm threshold based on the minimum DDoS attack rate in the EdgeOne console and configure the corresponding subscription in the Message Center.
>?
>- EdgeOne identifies DDoS attacks by monitoring external access traffic in real time, and automatically cleanses traffic as soon as malicious attack traffic is detected.
>- Alarm notifications are pushed only for DDoS attacks against the DDoS mitigation Enterprise plan (site access and layer-4 proxy services). Currently, other businesses don't support the DDoS attack traffic alarming feature.


## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone), select **Security** > **Alarm Notification** on the left sidebar, and select the target site.
2. In the **DDoS attack traffic alarm** section, click **Set**.
![](https://qcloudimg.tencent-cloud.cn/raw/3d9ae03f915503fa3bfa95a9cbfb725b.png)
3. On the **DDoS attack traffic alarm** page, you can adjust the default global DDoS attack alarm threshold for the current site, and the Message Center will push attack event notifications only when the attack rate exceeds the configured threshold. Click **Edit** of the default alarm threshold, modify the threshold, and click **Save**.
>? The **DDoS attack traffic alarm** page displays all objects that can be configured and their custom DDoS alarm thresholds if you have set. For those not configured with custom thresholds, you can modify the **Default alarm threshold**.

![](https://qcloudimg.tencent-cloud.cn/raw/e0214d3aa609ca11fcb7e3d14e9a4d41.png)
4. On the **DDoS attack traffic alarm** page, you can configure the alarm threshold for a security acceleration or layer-4 proxy business project.
>?We recommend you adjust the threshold based on the attack frequency and history. It is 100 Mbps by default and can be adjusted to 10 Mbps at the minimum.

 - Set a single alarm threshold
    1. Select the target business and click **Edit** in the alarm threshold column to adjust the minimum attack rate above which the business will push DDoS attack notifications.
   ![](https://qcloudimg.tencent-cloud.cn/raw/99b838db25a710141db2fd3b70131209.png)
	2. Modify the alarm threshold, click **Save**, and the custom threshold will be enabled automatically.
 - Batch set alarm thresholds
    1. Select one or more businesses and click **Batch set**.
     ![](https://qcloudimg.tencent-cloud.cn/raw/77e611f172babf0659807d334cd4e664.png)
    2. Toggle on the custom threshold switch ![](https://qcloudimg.tencent-cloud.cn/raw/027bed3bee658b505f0531e838eb1d80.png), set the alarm threshold, and click **OK**.
	 ![](https://qcloudimg.tencent-cloud.cn/raw/74e96c6cbe56c8da343ef312f7a43444.png)

