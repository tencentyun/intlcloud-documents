This document describes how to schedule traffic from CTCC, CUCC, and CMCC through smart scheduling.
## Overview
With a [CTCC/CUCC/CMCC Anti-DDoS Advanced instance](https://buy.cloud.tencent.com/antiddos#/advanced), business traffic can be forwarded according to the source ISP of DNS requests, which is a common traffic scheduling method. You can configure smart scheduling to schedule the traffic from CTCC, CUCC, CMCC, or other ISPs to the Anti-DDoS Advanced instances of CTCC, CUCC, CMCC, and other ISPs respectively.

## Prerequisites
- Before enabling smart scheduling, please connect your business to your Anti-DDoS instance.
>?
>- If you need to add the IP of your protected Tencent Cloud product to an Anti-DDoS Pro instance, please see [Getting Started](https://intl.cloud.tencent.com/document/product/1029/36116).
>- If you need to connect your layer-4 or layer-7 business to an Anti-DDoS Advanced instance, please see Anti-DDoS Advanced documents [Port Connection](https://intl.cloud.tencent.com/document/product/297/37221) or [Domain Name Connection](https://intl.cloud.tencent.com/document/product/297/37222).


- To modify the DNS resolution, you need to purchase a domain name resolution product.


## Operation Directions
1. Log in to the [Anti-DDoS console](https://console.cloud.tencent.com/ddos/antiddos-advanced/overview), select **Anti-DDoS Advanced (New)** -> **Smart Scheduling** on the left sidebar to view the policy list, and click **New Scheduling Policy** to automatically generate a CNAME record.
2. Click **Add Anti-DDoS instance** of the CNAME record to enter the smart scheduling editing page.
3. The TTL value defaults to **60 seconds** and ranges from 1 to 3,600 seconds. The default scheduling mode is **Priority**.
4. Click **Add Anti-DDoS IP**, tick the target Anti-DDoS instance and IP, and click **OK**.
5. After the instance is selected, DNS will be enabled for its protective line by default. At this point, you can set the line priority.
>?
>- The priority of the three ISPs must be the same to guarantee that DNS requests can receive responses according to source ISPs.
>- For smart scheduling configurations, please see [Configuring Smart Scheduling](https://intl.cloud.tencent.com/document/product/297/37229).
>

