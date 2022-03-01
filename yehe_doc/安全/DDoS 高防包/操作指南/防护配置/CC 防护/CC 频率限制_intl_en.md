
Anti-DDoS supports CC frequency limiting for connected web applications to restrict the access frequency of source IPs. It provides multiple defense levels and is set to "Loose" by default. You can customize a frequency limiting rule to apply CAPTCHA and discard on source IPs if any IP accesses a certain page too frequently in a short time.

You can adjust your frequency limiting rules based on the real-time traffic using the following levels:
<dx-tabs>
::: Strict
This level verifies the identity of visitors using CAPTCHA. Note that this level may lead to false positives due to a stricter verification, and is only applicable to website applications. For API- or app-based applications, please configure the CC frequency limiting policies instead of using the default configurations.
:::
::: Medium
This level verifies the identity of visitors using CAPTCHA. Only requests from verified visitors are forwarded to the origin. Note that this level is only applicable to website applications. For API- or app-based applications, please configure the CC frequency limiting policies instead of using the default configurations.
Urgent: when requests to access the real server surge and cause a high load or abnormal response, you can configure this level.

:::
::: Loose
At this level, there may be a risk that a small number of abnormal requests can bypass the policy. You can change the defense level when attacks come or configure the CC frequency limit for protection.
:::
::: Custom
This level can limit the access frequency of requests that match with configured rules.
:::
</dx-tabs>



## Prerequisites
You have successfully purchased an [Anti-DDoS Pro](https://intl.cloud.tencent.com/document/product/1029/36115) instance and set the protected target.

## Directions
1. Log in to the new [Anti-DDoS console](https://console.cloud.tencent.com/ddos/antiddos-native/config/port) and select **Configurations** on the left sidebar. Open the **CC Protection** tab.
2. Select an Anti-DDoS Pro instance ID in the list on the left, such as "bgp-00xxxxxx".
![](https://qcloudimg.tencent-cloud.cn/raw/96e22f56ce73f2fb7af2e0760d27d986.png)
3. Click **Set** in the **CC Frequency Limit** section to enter the rule list.
![](https://qcloudimg.tencent-cloud.cn/raw/f9eb316ce763443c727a9393fe156bc3.png)
4. Click **Create** and enter the required fields to create a frequency limiting rule. 
>!
>- If no frequency limiting rules are created, the "Custom" level cannot be enabled.
>- After optimization, you can add the default rule optionally before first creating a rule, and configure CC frequency limiting rules for sub-domain names.

![](https://main.qcloudimg.com/raw/f1128c978153cfdf59863a5922931b1b.png)
5. After the rule is created, it is added to the rule list. You can click **Configuration** on the right of the rule to modify it.
![](https://main.qcloudimg.com/raw/8152349ee35d418ccb9b20fbc7f52cdd.png)
