Anti-DDoS Advanced (Global Enterprise Edition) supports CC frequency limiting for connected web applications to restrict the access frequency of source IPs. It provides multiple defense levels and is set to "Loose" by default. You can customize a frequency limiting rule to apply CAPTCHA and discard on source IPs if any IP accesses a certain page too frequently in a short time.

You can adjust your frequency limiting rules based on the real-time traffic using the following levels:
<dx-tabs>
::: Loose
At this level, there may be a risk that a small number of abnormal requests can bypass the policy. You can change the defense level when attacks come or configure the CC frequency limit for protection.
:::
::: Medium
This level verifies the identity of visitors using CAPTCHA. Only requests from verified visitors are forwarded to the origin. Note that this level is only applicable to website applications. For API- or app-based applications, please configure the CC frequency limiting policies instead of using the default configurations.
Urgent: when requests to access the real server surge and cause a high load or abnormal response, you can configure this level.
:::
::: Strict
This level verifies the identity of visitors using CAPTCHA. Note that this level may lead to false positives due to a stricter verification, and is only applicable to website applications. For API- or app-based applications, please configure the CC frequency limiting policies instead of using the default configurations.
:::
::: Urgent
When requests to access the real server surge and cause a high load or abnormal response, you can configure this level.
:::
::: Custom
This level can limit the access frequency of requests that match with configured rules.
:::
</dx-tabs>



## Prerequisite
You have purchased an [Anti-DDoS Advanced (Global Enterprise Edition) instance](https://intl.cloud.tencent.com/document/product/297/37241) and set the object to protect.


## Directions
1. Log in to the [Anti-DDoS Advanced (Global Enterprise Edition) console](https://console.cloud.tencent.com/ddos/ddos-basic) and select **Anti-DDoS Advanced** > **Configurations** > **CC Protection**.
2. Select an Anti-DDoS Advanced instance ID in the list on the left, such as "bgp-00xxxxxx".
![](https://main.qcloudimg.com/raw/6a4d39de7a74962647c56b0608bb1bf1.png)
3. Click **Set** in the **CC Frequency Limit** section.
4. Click **Create**. Select or add a domain name, turn on the "Defense" switch, and then select an appropriate defense level.
5. To configure custom rules, click **Add Rule**. On the pop-up page, enter the required fields and click **OK**.
![](https://main.qcloudimg.com/raw/98ed17178231f248c2747e147860bb0e.png)
**Parameter description:**
 - For "Domain name", select a domain name.
 - For "Action", set to "Discard" or "CAPTCH".
        - If "Discard" is selected, requests that matched the specified conditions will be discarded.
        - If "CAPTCH" is selected, requests that matched the specified conditions will be verified via CAPTCH.
 - For "Condition", set the number of requests that are allowed to access a source IP within a specified period.
 - For "Punishment time", set a time period.
6. After the rule is created, it is added to the rule list. You can click **Configuration** on the right of the rule to modify it.
![](https://main.qcloudimg.com/raw/65c453e0d0d8ec07a795e777f1410fce.png)
