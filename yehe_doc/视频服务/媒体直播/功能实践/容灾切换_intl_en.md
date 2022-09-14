StreamLive provides redundancy and supports failover to help you ensure the reliability of live stream sources. Follow the steps below to configure failover:

1. On the **Channel Management** page, Click **Create Channel**. To configure input failover for an existing channel, click **Edit**.
![](https://qcloudimg.tencent-cloud.cn/raw/2299ba64984e13565781af9235aeb430.png)

2. Add inputs in the **Input Setting** step. The backup input used for failover must be of the same type as the primary input.
![](https://qcloudimg.tencent-cloud.cn/raw/d05b8b563e4a124e0fbd09514c9ae290.png)

3. Find the input for which you want to configure failover and click **Setting**.
![](https://qcloudimg.tencent-cloud.cn/raw/9bec3699f616ac1ee76472728a46b557.png)

4. Toggle on **Input Failover** and complete the following settings.
![](https://qcloudimg.tencent-cloud.cn/raw/2b28b7c0495c2718358b2f7823603b9a.png)
Select a **backup input** from the inputs bound to the current channel. Specify the downtime threshold, which indicates the time (ms) to wait when there is no data from the primary input before the system switches to the backup input. We recommend you set this to 3000. The lower the downtime threshold, the faster the failover. However, a low downtime threshold also means there may be a frequent switch of inputs caused by temporary packet loss. At last, specify what you want the system to do after the primary input is recovered. If you select **CURRENT_PREFERRED**, the system will continue to use the current input. If you select **PRIMARY_PREFERRED**, the system will switch back to the primary input if the backup is currently used.

5. Click **Confirm** to return to the **Input Setting** page. You will see that the bind status of the two inputs is now **Primary** and **Backup** respectively.
![](https://qcloudimg.tencent-cloud.cn/raw/a9b76c8ce82c4cea993e8edf858aa646.png)
You have now configured input failover and can continue to configure outputs for the channel. For detailed directions, see “Channel Management - Step 4. Configure Output Groups”.

