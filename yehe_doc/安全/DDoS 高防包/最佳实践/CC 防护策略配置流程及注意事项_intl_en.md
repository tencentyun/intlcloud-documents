Anti-DDoS Pro provides CC attack protection, the protection policy features protection level, cleansing threshold, precise protection, and CC frequency limit, etc. After connecting your business, you can configure CC attack protection policy as instructed in this document to use Anti-DDoS Pro to safeguard your business.

## Step 1: Set Cleansing Threshold
1. Log in to the [Anti-DDoS Pro console](https://console.cloud.tencent.com/ddos/antiddos-native/config/web) and select **Anti-DDoS Pro (New)** > **Configurations** > **CC Protection**.
2. Select an Anti-DDoS Pro instance ID in the list on the left, such as "bgp-00xxxxxx".
![](https://qcloudimg.tencent-cloud.cn/raw/06a338bad6a895ce3f1ab990e62606db.png)
3. To enable CC protection in the "CC Protection and Cleansing Threshold" section, click ![](https://qcloudimg.tencent-cloud.cn/raw/b56da8e70914bb5f6fce1900bcf81ef5.png) and set a cleansing threshold.
>?
>- The Anti-DDoS Advanced CC protection will be enabled once you set a cleansing threshold. A value that 1.5 times your common business peak is recommended.
>- The Anti-DDoS Pro cleansing feature will remain disabled if no threshold value is set, and the protection level, precise protection, and CC frequency limit you configured in the console will not be in effect even when your business is under CC attacks. For more information, please see [Protection Level and Cleansing Threshold](https://cloud.tencent.com/document/product/1021/43921).

![](https://qcloudimg.tencent-cloud.cn/raw/b215992a9e43113484ce147295688b42.png)

## Step 2: Set CC Protection Level
1. Click **Set** in the **CC Protection and Cleansing Threshold** section to enter the rule list.
![](https://qcloudimg.tencent-cloud.cn/raw/a2b51859c3f67e8bcac47da1346eb659.png)
2. Click **Create**. Select an associated IP and a domain name, and set the defense status and cleaning threshold.
>?
>- Wildcard domain names are not supported.
>- When you create CC frequency limiting rules, CC protection is enabled by default.
>- Connected Anti-DDoS Pro instances will use the default cleansing threshold, and the system will generate a baseline based on historical patterns of your application traffic. You can set a cleansing threshold for a single domain name.

![](https://qcloudimg.tencent-cloud.cn/raw/04e36e5ae1dee1a46a1391505f04d2f0.png)
3. Click **Save**.

## Step 3: Set Precise Protection Policy
When your business is under attack, we recommend deriving the attack characteristics from the specific attack request information obtained through packet capture, middleware access logs, and other protection devices to configure your precise protection policy based on your business.

You can enable precise protection to configure protection policies combining multiple conditions of common HTTP fields, such as URI, UA, Cookie, Referer, and Accept to screen access requests. For the requests that match the conditions, you can configure CAPTCHA to verify requesters or a policy to automatically discard the packets.

1. Click **Set** in the **Precise Protection** section to enter the rule list.
![](https://qcloudimg.tencent-cloud.cn/raw/aec10deea0cc7e54f8f8f51c062d5b94.png)
2. Click **Create**. On the pop-up page, enter the required fields, and click **OK**. For more information, please see [Precise Protection](https://intl.cloud.tencent.com/document/product/1029/36136).
>!
>- If a policy involves multiple HTTP fields, the policy can be matched if all conditions are met.
>- [Precise protection](https://intl.cloud.tencent.com/document/product/297/37218) for HTTPS businesses is currently supported for Anti-DDoS Advanced but not for Anti-DDoS Pro.

![](https://qcloudimg.tencent-cloud.cn/raw/059021bd2afd350d2589d503e571aac8.png)

**Field description:**
<table>
<thead>
<tr>
<th>Field</th>
<th>Field Description</th>
</tr>
</thead>
<tbody><tr>
<td>URI</td>
<td>The URI of an access request.</td>
</tr>
<tr>
<td>UA</td>
<td>The identifier and other information of the client browser that initiates an access request.</td>
</tr>
<tr>
<td>cookie</td>
<td>The cookie information in an access request.</td>
</tr>
<tr>
<td>Referer</td>
<td>The source website of an access request, from which the access request is redirected.</td>
</tr>
<tr>
<td>Accept</td>
<td>The data type to be received by the client that initiates the access request.</td>
</tr>
<tr>
<td>Match condition</td>
<td>CAPTCHA and discard<ul><li>Discard: discards packets without verifying the requester. </li><li> CAPTCHA: verifies the requester through algorithms.</li></li><li> Allow: allows the requests that match the specified conditions.</li></ul> </td>
</tr>
</tbody></table>


## Step 4: Set CC Frequency Limit
Anti-DDoS Advanced supports configuring CC frequency policy for connected web businesses to restrict the access frequency of source IPs. You can customize a frequency policy to apply CAPTCHA and discard on source IPs if any IP accesses a certain page too frequently in a short time.
1. Click **Set** in the **CC Frequency Limit** section to enter the rule list.
![](https://qcloudimg.tencent-cloud.cn/raw/adea1149fcee272461492b67a7f296c2.png)
2. You can create new rules, or edit existing rules by changing the defense level.
>?If the Anti-DDoS Advanced CC attack protection is enabled, the cleansing will be triggered when there is attack traffic, of which the detection strictness is the protection level. There are three available levels for you to select based on actual attacks: **Loose**, **Urgent** **Medium**, **Strict** and **Custom**. For more information, please see [Protection Level and Cleansing Threshold](https://cloud.tencent.com/document/product/1021/43921).
3. Click **Create**. On the pop-up page, enter the required fields, and click **OK**. For detailed configurations, please see [CC Frequency Limiting](https://intl.cloud.tencent.com/document/product/1029/36137).
>!
>- Newly created rules only take effect in the "Custom" mode.
>- When configuring a CC frequency limit policy targeting the URI field, you need to configure a frequency limit on the directory `/` first and the match mode must be "equals to". Then you can configure the URI access frequency limit on other directories.
>- If a source IP accesses the `/` directory of the domain name for more than the set number of times in the set period, the set action (**CAPTCHA** or **Discard**) will be triggered.
>- If a frequency limit policy is configured for the `/` directory of a domain name, then the frequency of the domain name's other directories must be the same.
>- If the request URI contains any unfixed string, you can set the match mode to "include", so that URIs with the set prefix will be matched.

![](https://qcloudimg.tencent-cloud.cn/raw/32b082e671748d092186e6d5f7421849.png)

**Field description:**
<table>
<thead>
<tr>
<th>Field</th>
<th>Field Description</th>
</tr>
</thead>
<tbody><tr>
</tr>
<tr>
<td>Cookie</td>
<td>The cookie information in an access request.</td>
</tr>
<tr>
<td>User-Agent</td>
<td>The identifier and other information of the client browser that initiates an access request.</td>
</tr>
<tr>
<td>URI</td>
<td>The URI of an access request.</td>
</tr>
<tr>
<td>Frequency limit policy</td>
<td>CAPTCHA and discard<ul><li>Discard: discards packets without verifying the requester. </li><li> CAPTCHA: verifies the requester through algorithms.</li><li> Allow: allows the requests that match the specified conditions.</li></ul> </td>
</tr>
<tr>
<td>Check condition</td>
<td>Set the access frequency based on your business, for which a value 2 to 3 times the common number of access requests is recommended. For example, if your website is accessed averagely 20 times per minute, you can configure the value to 40 to 60 times per minute or adjust it according to the attack severity.</td>
</tr>
<tr>
<td>Blocking time</td>
<td>The longest period is a whole day.</td>
</tbody></table>
