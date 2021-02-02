Anti-DDoS Pro provides CC attack protection, the protection policy features protection level, cleansing threshold, precise protection, and CC frequency limit, etc. After connecting your business, you can configure CC attack protection policy as instructed in this document to use Anti-DDoS Pro to safeguard your business.
## Configuration Directions
1. Log in to the [Anti-DDoS console](https://console.cloud.tencent.com/ddos/antiddos-native/config/web) and click **Anti-DDoS Pro (New)** -> **Configurations** on the left sidebar.
2. Select an instance ID from the left list, e.g., `bgp-000000co`, and then open the **Domain name protection** tab.
3. **Set the CC protection cleansing threshold**: You can set a threshold value in the **CC Protection Policy** section.
>?
>- The Anti-DDoS Pro CC protection will be enabled once you set a cleansing threshold. A value that 1.5 times your normal business peak is recommended.
>- The Anti-DDoS Pro cleansing feature will remain disabled if no threshold value is set, and the protection level, precise protection, and CC frequency limit you configured in the console will not be in effect even when your business is under CC attacks. For more information, please see [Protection Level and Cleansing Threshold](https://intl.cloud.tencent.com/document/product/1029/36135).
>
4. **Set the CC protection level**:
	① Click **Set** in the **CC Protection Policy** section to enter the configuration page.
	② You can now create a new protection level or modify an old one.
>?If the Anti-DDoS Pro CC attack protection is enabled, the cleansing will be triggered when there is attack traffic, of which the detection strictness is the protection level. There are three available levels for you to select based on actual attacks: **Loose**, **Medium**, and **Strict**. For more information, please see [Protection Level and Cleansing Threshold](https://intl.cloud.tencent.com/document/product/1029/36135).
>
5. **Configure the precise protection policy**:
When your business is under attack, we recommend deriving the attack characteristics from the specific attack request information obtained through packet capture, middleware access log, and other protection devices to configure your precise protection policy based on your business.
You can enable the precise protection to configure protection policies combining multiple conditions of common HTTP fields, such as URI, UA, Cookie, Referer, and Accept to screen access requests. For the requests that match the conditions, you can configure CAPTCHA to verify requesters or a policy to automatically discard the packets.
	① On the [**Configurations**](https://console.cloud.tencent.com/ddos/antiddos-native/config/web) page, click **Set** in the **Precise Protection** section to view the precise protection rule list.
	② Click **Create**, fill in the rule fields, and click **OK** to create a new precise protection rule. For more information, please see [Precise Protection](https://intl.cloud.tencent.com/document/product/1029/36136).
>!
>- If a policy involves multiple HTTP fields, the policy can be matched if all conditions are met.
>- Anti-DDoS Pro supports configuring precise protection for HTTPS businesses.
>

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
<td>User-Agent</td>
<td>The identifier and other information of the client browser that initiates an access request.</td>
</tr>
<tr>
<td>Cookie</td>
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
<td>Match Condition</td>
<td>CAPTCHA and discard<ul><li>Discard: discards packets without verifying the requester.</li><li>CAPTCHA: verifies the requester through algorithms.</li></ul></td>
</tr>
</tbody></table>

6. **Set the CC frequency limit**:
Anti-DDoS Pro supports configuring CC frequency policy for connected web businesses to restrict the access frequency of source IPs. You can customize a frequency policy to apply CAPTCHA and discard on source IPs if any IP accesses a certain page too frequently in a short time.
	① On the [**Configurations**](https://console.cloud.tencent.com/ddos/antiddos-native/config/web) page, click **Set** in the **CC Frequency Limit** section to view the frequency limit rule list.
	② Click **Create**, fill in the rule fields, and click **OK** to create a new rule.
>!
>- When configuring a CC frequency limit policy targeting the URI field, you need to configure a frequency limit on the directory `/` first and the match mode must be "equals to". Then you can configure the URI access frequency limit on other directories.
>- If a source IP accesses the `/` directory of the domain name for more than the set number of times in the set period, the set action (**CAPTCHA** or **Discard**) will be triggered.
>- If a frequency limit policy is configured for the `/` directory of a domain name, then the frequency of the domain name's other directories must be the same.
>- If the request URI contains any unfixed string, you can set the match mode to "include", so that URIs with the set prefix will be matched.
 >

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
<td>CAPTCHA and discard<ul><li>Discard: discards packets without verifying the requester.</li><li>CAPTCHA: verifies the requester through algorithms.</li></ul></td>
</tr>
<tr>
<td>Check Condition</td>
<td>Set the access frequency based on your business, for which a value 2 to 3 times the normal number of access requests is recommended. For example, if your website is accessed averagely 20 times per minute, you can configure the value to 40 to 60 times per minute or adjust it according to the attack severity.</td>
</tr>
<tr>
<td>Punishment Time</td>
<td>The longest period is a whole day.</td>
</tbody></table>
