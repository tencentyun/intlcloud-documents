## Error Description
The application suffered high-traffic attacks, causing the IP to be blocked and the application to be inaccessible.

## Possible Causes
- The protection traffic threshold is exceeded, leading to blocking.
- The attack is still ongoing, so the IP cannot be automatically unblocked.

## Solutions
- Anti-DDoS Basic user: An attacked IP blocked for 2 hours will be automatically unblocked by default. You can apply for Anti-DDoS Emergency Protection in case of emergency.
- Anti-DDoS Pro or Advanced user: Only **three** chances of manual unblocking are provided each day. The system resets the chance counter daily at midnight. Unused chances cannot be accumulated for the next day.

If the manual unblocking chances are used up:
- If you haven't purchased Anti-DDoS Pro, we recommend you purchase Anti-DDoS Pro. Then, you can perform unblocking when binding devices for the first time.
- If you have already purchased Anti-DDoS Pro, we recommend you upgrade the protection package so as to perform unblocking earlier.

## Troubleshooting Procedure
1. Log in to the [Anti-DDoS Console](https://console.cloud.tencent.com/ddos/unblock/list), select **Manual Unblocking** on the left sidebar, and view the remaining number of manual unblocking times.
  - If the remaining number of manual unblocking times is 0, proceed to [step 5](#step5) or wait for auto unblocking.
  - Otherwise, proceed to [step 2](#step2).
>?For more information on the auto unblocking time, please see the **Estimated Unblocking Time** value on the **Manual Unblocking** > **Unblocking Operation** page in the Anti-DDoS console.

2. [](id:step2)Check whether the attack has stopped by selecting **Anti-DDoS Pro** > **[Protection Overview](https://console.cloud.tencent.com/ddos/antiddos-native/overview/ddos)**.
 - If yes, proceed to [step 3](#step3).
 - If no, continue the unblocking operation and perform [step 3](#step3) after the attack is over.
>?If the attack persists, you cannot perform unblocking, and you need to wait for the attack to end before manual unblocking or auto unblocking.
3. [](id:step3)On the left sidebar, select **Manual Unblocking** > **Unblocking Operation** to enter the **Unblocking Operation** page.
4. On the **Unblocking Operation** page, find the protected IP in **Pending Auto Unblocking** and click **Unblock** in the **Operation** column on the right.
5. [](id:step5)The suggestions for users of different Anti-DDoS services are as follows:
 - If you use Anti-DDoS Basic, we recommend you purchase [Anti-DDoS Pro](https://buy.cloud.tencent.com/antiddos#/native) (available in Guangzhou, Shanghai, and Beijing regions). Then, you can perform unblocking when [binding devices for the first time](https://intl.cloud.tencent.com/document/product/1029/36116). 
 - If you use Anti-DDoS Pro or Advanced, we recommend you upgrade the protection package so as to increase the number of protected times or protected IPs and perform unblocking earlier.
