Anti-DDoS Advanced (Global Enterprise Edition) supports precise protection for connected web businesses. With the precise protection, you can configure protection policies combining multiple conditions of common HTTP fields, such as URI, UA, Cookie, Referer, and Accept to screen access requests. For the requests matched the conditions, you can configure CAPTCHA to verify the requesters or a policy to automatically drop or allow the requests. Precise protection is available for policy customization in various use cases to precisely defend against CC attacks.



## Prerequisite
You have purchased an [Anti-DDoS Advanced (Global Enterprise Edition) instance](https://intl.cloud.tencent.com/document/product/297/37241) and set the object to protect.


## Directions
1. Log in to the [Anti-DDoS Advanced (Global Enterprise Edition) console](https://console.cloud.tencent.com/ddos/ddos-basic) and select **Anti-DDoS Advanced** > **Configurations** > **CC Protection**.
2. Select an Anti-DDoS Advanced instance ID in the list on the left, such as "bgp-00xxxxxx".
![](https://qcloudimg.tencent-cloud.cn/raw/273bc2d0fa1e5a38c0771792d2f85e07.png)
3. Click **Set** in the **Precise Protection** section.
4. Click **Create**. On the pop-up page, enter the required fields and click **OK**.
![](https://main.qcloudimg.com/raw/0b4604f0d97e6059c6d35c3181beee60.png)
**Parameter description:**
 - For "Domain Name", select a domain name.
 - For "Match Condition", set a match condition to identify requests that use HTTP fields. The following HTTP fields are supported:
 <table>
<thead>
<tr>
<th>Match Field</th>
<th>Field Description</th>
<th>Logic</th>
</tr>
</thead>
<tbody><tr>
<td>URI</td>
<td>The URI of an access request.</td>
<td>Equals to, includes, or does not include.</td>
</tr>
<tr>
<td>UA</td>
<td>The identifier and other information of the client browser that initiates an access request.</td>
<td>Equals to, includes, or does not include.</td>
</tr>
<tr>
<td>Cookie</td>
<td>The cookie information in an access request.</td>
<td>Equals to, includes, or does not include.</td>
</tr>
<tr>
<td>Referer</td>
<td>The source website of an access request, from which the access request is redirected.</td>
<td>Equals to, includes, or does not include.</td>
</tr>
<tr>
<td>Accept</td>
<td>The data type to be received by the client that initiates the access request.</td>
<td>Equals to, includes, or does not include.</td>
</tr>
</tbody></table>
 - For "Match Action", set to "CAPTCHA", "Block" or "Allow".
    - If "CAPTCHA" is selected, requests that matched the specified conditions will be verified via CAPTCHA.
    - If "Block" is selected, requests that matched the specified conditions will be blocked.
    - If "Allow" is selected, requests that matched the specified conditions will be allowed.
5. After the rule is created, it is added to the rule list. You can click **Configuration** on the right of the rule to modify it.
![](https://main.qcloudimg.com/raw/13ed1705034538fc6fc1b1090a65bc8e.png)
