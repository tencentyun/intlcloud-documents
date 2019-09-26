## Prerequisites
Before you purchase an Anti-DDoS Pro instance, you need to register a Tencent Cloud account and complete the identity verification.

## Steps
1. Log in to the [Tencent Cloud Anti-DDoS Pro Console](https://console.cloud.tencent.com/dayu/bgp_v2), select **Anti-DDoS Pro** -> **Resource List** page, and click **Purchase** on the top right.
2. Configure the following parameters according to the actual protection needs:
 ![](https://main.qcloudimg.com/raw/3219dad97fc2deaa07d5377a15a86d81.png)
 - Type: Select **Single IP Instance** or **Multi-IP Instance**.
    - A Single IP instance can bind to one public network IP of Tencent Cloud. The IP enjoys dedicated protection capability.
    - A Multi-IP instance can bind to multiple public network IP of Tencent Cloud. These IPs share the protection capability.
 - (Optional) Number of IPs: This parameter is visible only when **Type** is set to **Multi-IP Instance**. It indicates the number of public network IPs of Tencent Cloud that Anti-DDoS Pro instance can bind to.
 - Region: Please select the region of the origin server of Tencent Cloud. Currently, Anti-DDoS Pro only provides anti-DDoS service for public network IPs of Tencent Cloud within the same region.
 >Anti-DDoS Pro in regions outside China is only available to whiltelisted users. If you want to purchase the service, please [contact us](https://intl.cloud.tencent.com/support) for more information.
 - Base Protection Bandwidth: The basic protection capability of this instance. It’s recommended to set the base protection bandwidth slightly higher than the historical average attack traffic value, which will allow you to handle normal attacks.
 - Purchase Number: Set the number of instances you need to purchase. You are allowed to purchase up to 100 Anti-DDoS Pro instances at one time.
 - Purchase Duration: Set how long the service plan you want to purchase. The fees are prepaid and calculated based on the IP number, the base protection bandwidth, and the purchased usage period.
 - Elastic Protection Bandwidth: The highest possible protection capability of this instance. You are advised to refer to the largest value of the historical attack traffic, and select an elastic protection bandwidth slightly higher than the largest value to defend against sudden increases in attack traffic, avoiding IP block caused by traffic exceeding the protection bandwidth limit to ensure a non-stop business protection. The cost of the elastic part is billed according to the actual protection volume and is settled by day.
3. Click **Pay Now** to complete the payment process.

>In addition to the Resource List, you can also the protection configuration page and the statistics report page also provide you with purchase entry.

## More Information
- [Detailed Billing Description of Anti-DDoS Pro](https://intl.cloud.tencent.com/document/product/1029/31747)
- [Billing FAQs](https://intl.cloud.tencent.com/document/product/1029/31774)

