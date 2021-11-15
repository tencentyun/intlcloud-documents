 This guide describes protection levels that DDoS Edge Defender provides in different scenarios and how to set them in the console.
>? DDoS Edge Defender is currently available to beta users. To use it, please [contact us](https://intl.cloud.tencent.com/contact-us).

## Use Cases
DDoS Edge Defender provides three available protection levels for you to adjust protection policies against different DDoS attacks. The details are as follows:
<dx-tabs>
::: Loose
| Protection Level | Protection Action                                                     | Description                                                         |
| -------- | :----------------------------------------------------------- | ------------------------------------------------------------ |
| Loose     | <li>Filters SYN and ACK data packets with explicit attack attributes.</li><li>Filters TCP, UDP, and ICMP data packets that are not compliant with the protocol specifications.</li><li>Filters UDP data packets with explicit attack attributes.</li> | <li>This cleansing policy is loose and only defends against explicit attack packets.</li><li>We recommend choosing this protection level when normal requests are blocked. Complex attack packets may pass through the security system.</li> |
:::
::: Medium
| Protection Level | Protection Action                                                     | Description                                                         |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Medium     | <li>Filters SYN and ACK data packets with explicit attack attributes.</li><li>Filters TCP, UDP, and ICMP data packets that are not compliant with the protocol specifications.</li><li>Filters UDP data packets with explicit attack attributes.</li><li>Filters common UDP-based attack packets.</li><li>Actively verifies the source IPs of some access attempts.</li> | <li>This cleansing policy is suitable for most businesses and capable of defending against common attacks.</li><li>The level Medium is chosen by default.</li> |
:::
::: Strict
| Protection Level | Protection Action                                                     | Description                                                 |
| -------- | ------------------------------------------------------------ | ---------------------------------------------------- |
| Strict     | <li>Filters SYN and ACK data packets with explicit attack attributes.</li><li>Filters TCP, UDP, and ICMP data packets that are not compliant with the protocol specifications.</li><li>Strictly checks UDP data packets with explicit attack attributes and UDP-based attack packets.</li><li>Actively verifies the source IPs of some access attempts.</li><li>Filters ICMP attack packets.</li> | This cleansing policy is strict. We recommend choosing this level when attack packets pass through the security system on Normal mode. |
:::
</dx-tabs>

>?
>- If you need to use UDP in your business, please contact [Tencent Cloud Technical Support](https://intl.cloud.tencent.com/contact-us) to customize an ideal policy for not letting the level Strict affect normal business process.
>- The level Medium is chosen by default for your DDoS Edge Defender instance. You can set the DDoS protection level for your business needs and also the cleansing threshold. Attack traffic will be cleansed when it is detected higher than the threshold you set.

## Prerequisites
You have successfully purchased a [DDoS Edge Defender](https://intl.cloud.tencent.com/document/product/297/42172) instance and set the object to protect.


## Directions
1. Log in to the [DDoS Edge Defender Console](https://console.cloud.tencent.com/ddos/antiddos-edge/policy/ddos), click **Protection Policy** on the left sidebar, and then select the tab **DDoS Protection**.
2. Select an Edge Defender instance ID, such as "edge-xxxxxxx".
![](https://main.qcloudimg.com/raw/ceb4f1ebedc2efb78e428f5ffe071473.png)
3. Set the protection level and cleansing threshold in the **DDoS Protection** section on the right.
>?If you have a clear concept about the threshold, set it as required. Otherwise leave it to the default value. The DDoS protection system will automatically learn through AI algorithms and calculate the default threshold for you.

![](https://main.qcloudimg.com/raw/9d9ed77e18ed9864dd1cc2ea5bf5182b.png)

**Parameter Description:**
- **Level**
	If the protection is enabled, the level Medium is chosen by default for your DDoS Edge Defender instance. You can adjust the DDoS protection level for your business needs.
- **Cleansing Threshold**
	- This indicates a value to trigger cleansing. Cleansing will not be triggered by the traffic below the threshold you set even though it is found malicious.
	- If the protection is enabled, your DDoS Edge Defender instance will use the default cleansing threshold after your business is connected, and the system will generate a baseline based on historical patterns of your business traffic. You can also set the cleansing threshold for your business needs.
