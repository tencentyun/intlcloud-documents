## Prerequisites
Before you purchase an Anti-DDoS Pro instance, you need to register for a Tencent Cloud account and complete the identity verification.

## Directions
1. Log in to the [Anti-DDoS Pro Console](https://console.cloud.tencent.com/dayu/bgp_v2), go to **Anti-DDoS Pro** > **Resource List**, and click **Purchase** on the top right.
2. Make the following configurations according to your needs:
 ![](https://main.qcloudimg.com/raw/3219dad97fc2deaa07d5377a15a86d81.png)
 - Type: choose **Single IP Instance** or **Multi-IP Instance**.
    - A single IP instance can be bound to only one Tencent Cloud public IP which will enjoy dedicated protection.
    - A multi-IP instance can can be bound to multiple Tencent Cloud public IPs which will share the protection capability.
 - (Optional) Number of IPs: this is available only when you choose **Multi-IP Instance**. It represents the maximum number of Tencent Cloud public IPs that can be bound to the Anti-DDoS Pro instance.
 - Region: please select the region of Tencent Cloud real server. Currently, an Anti-DDoS Pro instance can only provide DDoS protection for Tencent Cloud public IPs in the same region.
 >Currently Anti-DDoS Pro instances in regions outside Mainland China are only available to whitelisted users. If you need such instances, please [contact us](https://intl.cloud.tencent.com/support) for more information.
 - Base Protection Bandwidth: the basic protection capability of the instance. It’s recommended to set the base protection bandwidth slightly higher than the average of historical attack traffic so that the instance can handle most attacks.
 - Quantity: number of instances you want to purchase. You can purchase up to 100 Anti-DDoS Pro instances at a time.
 - Validity Period: how long the instance is going to be valid. The price will be calculated based on the number of IPs, the base protection bandwidth, and the validity period.
 - Elastic Protection Bandwidth: the maximum protection bandwidth of the instance. It is recommended to set the elastic protection bandwidth slightly higher than the highest historical attack traffic to defend against large traffic attacks. Elastic protection can help you keep your IPs from being blocked when the attack traffic goes over the base protection bandwidth to ensure the continuity of your business. The fees for elastic protection are calculated based on the actual bandwidth of the attack traffic and are billed daily.
3. Click **Purchase Now** to complete the purchase.

>You can also find the Purchase button on the Protection Configuration page and the Statistics page.

## References
- [Billing Overview](https://intl.cloud.tencent.com/document/product/1029/31747)
- [About Billing](https://intl.cloud.tencent.com/document/product/1029/31774)

