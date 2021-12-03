## Unblocking Procedure
### Auto unblocking
With auto unblocking, you only need to wait until blocked IPs are unblocked automatically. You can check the predicted unblocking time as follows:
1. Log in to the [Anti-DDoS Console](https://console.cloud.tencent.com/ddos/unblock/list), select **Self-Service Unblocking** > **Unblock Blocked IP** on the left sidebar to get to unblocking operation.
2. Check the predicted unblocking time of the IP in **Estimated Unblocking Time** on the unblocking page.

### Chances for self-service unblocking
Only three chances of self-service unblocking are provided for Anti-DDoS Advanced every day. The system resets the chance counter daily at midnight. Unused chances cannot be accumulated for the next day.
>?
>- The unblocking may fail for risk management reasons. A failed attempt does not count as a chance. Please wait for a while and then try again.
>- Before unblocking the IP, please check the predicted unblocking time which may be affected by some factors and will be postponed. If you accept the predicted time, you do not need to operate manually.
>- If the self-recovery chances are used up for the day, you can upgrade the base protection capability or the elastic protection capability to defend against large traffic attack and avoid continuous blocking.

### Manual unblocking
1. Log in to the [Anti-DDoS Advanced Console](https://console.cloud.tencent.com/ddos/antiddos-advanced/config/port) and select **Anti-DDoS Advanced (New)** > **Overview** on the left sidebar.
2. On the **DDoS protection** page, click **Unblock** on the right of the IP that is blocked.
3. Click **OK** on the pop-up dialog box.
>?
>- If the unblocking fails, you will receive a failure message. Please wait for a while and then try again.
>- If you receive a notification indicating successful unblocking, the IP has been successfully unblocked. You can refresh the page to check whether the protected IP is in running status.
