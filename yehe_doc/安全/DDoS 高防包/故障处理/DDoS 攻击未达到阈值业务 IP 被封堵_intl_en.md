
## Error Description
The attack traffic did not reach the purchased blocking threshold, but the IP was blocked.

## Possible Causes
You have purchased Anti-DDoS Pro, and the total attack traffic at all network egresses has not reached the purchased threshold, so the IP was blocked. The calculation method is to compare the attack traffic at all network egresses with the purchase threshold.
1. There are two types of blocking based on the location of the blocked node.
 - TIX blocking: Tencent's egress gateway is blocked. The blocking threshold is adjustable.
 - ISP blocking: the ISP is blocked. The blocking threshold is basically fixed.

2. In case of ISP blocking, there are two ways of blocking.
 - Single-IP blocking: when an IP's traffic reaches the single-IP blocking threshold of a certain egress (set according to the egress bandwidth), it will be blocked.
 - Multi-IP blocking: when the total IDC traffic (attack traffic + business traffic) in a certain detection range exceeds the multi-IP blocking threshold, multi-IP blocking will be triggered.
![](https://main.qcloudimg.com/raw/98964f295039560f01b0f3a2d196f579.png)

## Solutions
After the attack is over, you can perform manual unblocking or wait for auto unblocking.

## Troubleshooting Procedure
1. Log in to the [Anti-DDoS console](https://console.cloud.tencent.com/ddos/unblock/list), select **Manual Unblocking** on the left sidebar, and view the remaining number of manual unblocking times.
  - If the remaining number of manual unblocking times is 0, proceed to [step 5](#step5) or wait for auto unblocking.
  - Otherwise, proceed to [step 2](#step2).
  >?For more information on the auto unblocking time, please see the **Estimated Unblocking Time** value on the [Unblocking Operation](https://console.cloud.tencent.com/ddos/unblock/list) page in the console.
  >
2. [](id:step2)Check whether the attack has stopped by clicking [Protection Overview](https://console.cloud.tencent.com/ddos/antiddos-native/overview/ddos).
 - If yes, proceed to [step 3](#step3).
 - If no, continue the unblocking operation and perform [step 3](#step3) after the attack is over.
>? If the attack persists, you cannot perform unblocking, and you need to wait for the attack to end before manual unblocking or auto unblocking.
3. [](id:step3)On the left sidebar, select **Manual Unblocking** > **Unblocking Operation** to enter the **Unblocking Operation** page.
4. On the **Unblocking Operation** page, find the protected IP in **Pending Auto Unblocking** and click **Unblock** in the **Operation** column on the right.
   
5. [](id:step5)The suggestions for users of different Anti-DDoS services are as follows:
 - If you use Anti-DDoS Basic, we recommend you purchase [Anti-DDoS Pro](https://buy.cloud.tencent.com/antiddos#/native) (available in Guangzhou, Shanghai, and Beijing regions). Then, you can perform unblocking when [binding devices for the first time](https://intl.cloud.tencent.com/document/product/1029/36116). 
 - If you use Anti-DDoS Pro or Advanced, we recommend you [upgrade the protection package] so as to increase the number of protected times or protected IPs and perform unblocking earlier.
