This guide describes protection levels the Anti-DDoS Pro provides in different scenarios and how to set them in the console.
## Use Cases
Anti-DDoS Pro provides three available protection levels for you to adjust protection policies against different DDoS attacks. The details are as follows:

<dx-tabs>
::: Loose
| Protection Level | Protection Action                                                     | Description                                                         |
| -------- | :----------------------------------------------------------- | ------------------------------------------------------------ |
| Loose     | <li>Filters SYN and ACK data packets with explicit attack attributes.</li><li>Filters TCP, UDP, and ICMP data packets that are not compliant with the protocol specifications.</li><li>Filters UDP data packets with explicit attack attributes.</li> | <li>This cleansing policy is loose and only defends against explicit attack packets.</li><li>We recommend choosing this protection level when normal requests are blocked. Complex attack packets may pass through the security system.</li> |
:::
::: Medium
| Protection Level | Protection Action                                                     | Description                                                         |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Medium     | <li>Filters SYN and ACK data packets with explicit attack attributes.</li><li>Filters TCP, UDP, and ICMP data packets that are not compliant with the protocol specifications.</li><li>Filters UDP data packets with explicit attack attributes.</li><li>Filters common UDP-based attack packets.</li><li>Actively verifies the source IPs of some access attempts.</li> | <li>Medium is the default level.</li><li>This cleansing policy is suitable for most businesses and capable of defending against common attacks.</li> |
:::
::: Strict
| Protection Level | Protection Action                                                     | Description                                                 |
| -------- | ------------------------------------------------------------ | ---------------------------------------------------- |
| Strict     | <li>Filters SYN and ACK data packets with explicit attack attributes.</li><li>Filters TCP, UDP, and ICMP data packets that are not compliant with the protocol specifications.</li><li>Strictly checks and filters UDP data packets with explicit attack attributes and UDP-based attack packets.</li><li>Actively verifies the source IPs of some access attempts.</li><li>Filters ICMP attack packets.</li> | This cleansing policy is strict. We recommend choosing this level when attack packets pass through the security system on Normal mode. |
:::
</dx-tabs>

>?
>- If you need to use UDP in your business, please contact [Tencent Cloud Technical Support](https://intl.cloud.tencent.com/contact-us) to customize an ideal policy for not letting the level Strict affect normal business process.
>- The level Medium is chosen by default in each Anti-DDoS Pro instance.
>- The real server may suffer seconds of attacks in the following situations:
>  - It happens when you are changing the protection level.
>  - It happens when you are connecting to Anti-DDoS Pro.
> 
## Prerequisites
You have successfully purchased an [Anti-DDoS Pro](https://intl.cloud.tencent.com/document/product/1029/36115) instance and set the protected target.

## Directions
1. Log in to the new [Anti-DDoS console](https://console.cloud.tencent.com/ddos/antiddos-native/package) and select **Anti-DDoS Pro (New)** > **Configurations** on the left sidebar. Open the **DDoS Protection** tab.
2. Select an Anti-DDoS Pro instance ID in the list on the left, such as "bgp-00xxxxxx".
![](https://main.qcloudimg.com/raw/ceb4f1ebedc2efb78e428f5ffe071473.png)
3. Choose a protection level in the **DDoS Protection Level** section.
![](https://main.qcloudimg.com/raw/9d9ed77e18ed9864dd1cc2ea5bf5182b.png)


