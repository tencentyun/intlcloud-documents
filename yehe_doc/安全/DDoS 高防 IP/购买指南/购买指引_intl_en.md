## Prerequisite
You need to [sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) before using Anti-DDoS Advanced.

>! 
>- Anti-DDoS Advanced is a pay-as-you-go service that is billed monthly. The minimum subscription term is 1 month. Upon expiry, your subscription will be auto-renewed unless canceled by [contacting us](https://intl.cloud.tencent.com/contact-us). Your instances cannot be terminated during a subscription term.
>- Make sure that you have one-month credit to be frozen when activating this service.
>- Payments for this service are not refundable.

## Directions
### Purchase an Anti-DDoS Advanced instance (Chinese mainland)
1. Go to the [buy page](https://buy.cloud.tencent.com/antiddos#/advanced), and select **Anti-DDoS Advanced (Chinese Mainland)**.
![](https://qcloudimg.tencent-cloud.cn/raw/478f73e3a802b32572145bc9c3529600.png)
2. Configure the following parameters as needed.
  - Line: provides BGP lines and non-BGP lines (CTCC, CUCC, CMCC).
   - Specifications:
        - Access mode: proxy
        - Resources: 1 dedicated IP
        - Bandwidth type: multi-line BGP
        - Protection capability: base protection bandwidth + elastic protection bandwidth
 - Base protection bandwidth: supports monthly subscription. We recommend that you select a base protection bandwidth slightly higher than the average value of the historical attack traffic, which will allow you to handle normal attacks.
 - Elastic protection bandwidth: Fees based on the actual protection bandwidth by day. We recommend that you select an elastic protection bandwidth slightly higher than the largest attack traffic in history to defend against sudden increases in attack traffic, and avoid IP blocking caused by traffic exceeding the protection bandwidth limit.
 - Application bandwidth: the maximum application bandwidth, which must be greater than the total amount of inbound and outbound application bandwidth.
>! You can enable elastic protection bandwidth when you need to increase application bandwidth and QPS. After it’s enabled, the amount of bandwidth exceeding the specified amount will be billed at 1 USD/Mbps/day. Please select as needed.
 - Forwarding rules: the total number of TCP/UDP ports (for non-website connections) and HTTP/HTTPS domain names (for website connections) that you configure for an Anti-DDoS Advanced instance.
 - Validity: Select how long the service plan you want to purchase. The fees are prepaid and calculated based on the number of instances, the base protection bandwidth and the purchased usage period.
3. Click **Pay Now** to complete your purchase.

### Purchase an Anti-DDoS Advanced instance (outside the Chinese mainland)
1. Go to the [buy page](https://buy.cloud.tencent.com/antiddos#/advanced-intl), and select **Anti-DDoS Advanced (Outside Chinese Mainland)**.
![](https://qcloudimg.tencent-cloud.cn/raw/6a947508d368898ecf42b564f3d2fc0e.png)
2. Specify the following configurations according to your needs.
 - Specifications:
    - Access mode: proxy
    - Resources: 1 dedicated IP
    - Protection capability: Base protection bandwidth + elastic protection bandwidth
  - Region: Anti-DDoS Advanced uses the forwarding proxy method. Please choose a location near the real server to reduce connection latency.
  - Base protection bandwidth: It supports monthly subscription. We recommend that you select a base protection bandwidth slightly higher than the average value of the historical attack traffic, which will allow you to handle normal attacks.
  - Elastic protection bandwidth: Fees based on the actual protection bandwidth by day. We recommend that you select an elastic protection bandwidth slightly higher than the largest attack traffic in history to defend against sudden increases in attack traffic, and avoid IP blocking caused by traffic exceeding the protection bandwidth limit.
  - Application bandwidth: The maximum application bandwidth, which must be greater than the total amount of inbound and outbound application bandwidth.
>! You can enable elastic protection bandwidth when you need to increase application bandwidth and QPS. After it’s enabled, the amount of bandwidth exceeding the specified amount will be billed at 1 USD/Mbps/day. Please select as needed.
  - Forwarding rules: The total number of TCP/UDP ports (for non-website connections) and HTTP/HTTPS domain names (for website connections) that you configure for an Anti-DDoS Advanced instance.
  - Validity: Select how long the service plan you want to purchase. The fees are prepaid and calculated based on the number of instances, the base protection bandwidth and the purchased usage period.
3. Click **Pay Now** to complete your purchase.
