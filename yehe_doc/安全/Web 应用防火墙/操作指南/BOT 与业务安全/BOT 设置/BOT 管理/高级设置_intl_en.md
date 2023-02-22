## Prerequisites
You have purchased a WAF instance and [bot traffic management extra pack](https://cloud.tencent.com/document/product/627/11730#bot-.E8.A1.8C.E4.B8.BA.E7.AE.A1.E7.90.86.E4.BB.B7.E6.A0.BC.E8.AF.B4.E6.98.8E) and enabled bot analysis for WAF-connected domain names.

## Bot allowlist
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-botconfig) and select **Configuration center** > **Bot and application security** on the left sidebar.
2. On the **Bot and application security** page, select the target domain name in the top-left corner and click **Bot management** > **Bot allowlist**.
![](https://qcloudimg.tencent-cloud.cn/raw/83d8c1b878537a6b516703040524b92d.png)
3. On the bot allowlist settings page, click **Add rule**, configure parameters, and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/b777a85876c5906b53f6473bc6f793e1.png)

**Field description**
 - **Policy name**: 	Policy name.
 - **Rule description**: The rule description.
 - **Rule Switch**: Enabled by default.
 - **Condition**: Conditions for matching bot policies. Up to 10 match conditions can be set, which are connected by the "AND" relationship. When you hover the cursor over a match condition, you can view its description.
 - **Action**: Action to be executed, as described below:
 <table>
<thead>
<tr>
<th align="left">Action Type</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody><tr>
<td align="left">Allow</td>
<td align="left">Session requests that match the set conditions will be allowed and will not be logged.</td>
</tr>
<tr>
</tbody></table>

 - **Priority**: Enter an integer between 1 and 100. A smaller value indicates a higher execution priority. When the priority is the same, rules more recently added are executed before the less recently added.
 - **Custom tag**: You can set a tag of **Friendly bots**, **Malicious bots**, **Normal traffic**, or **Suspicious bots**.
5. Now you can view the created rule in the policy list. Click **Edit** or **Delete** to edit or delete it.
![](https://qcloudimg.tencent-cloud.cn/raw/cd5a8064c9547ef872feafebda03c350.png)
6.	 Priority from high to low: Bot allowlist > Scenario 1 (priority 1) > Scenario 2 (priority 2) > ... > Scenario n (priority m).


## Session management

This feature is similar to session setting in [CC protection](https://intl.cloud.tencent.com/document/product/627/11709). With different token IDs, you can differentiate between access requests from different requesters through the same IP and record their behavior features.

You can also use token IDs to continuously track the access behaviors of different requesters. This helps identify bot access behaviors through residential or public egress IPs and record session features when proxy IPs are frequently changed.

1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-botconfig) and select **Configuration center** > **Bot and application security** on the left sidebar.
2. On the **Bot and application security** page, select the target domain name in the top-left corner and click **Bot management**.
![](https://qcloudimg.tencent-cloud.cn/raw/f755b07c980b5a8d12de1c72e80ef885.png)
3. In **Global settings**, click **Configure now** in the **Session management module** section.
4. On the **Session management** page, click **Add a configuration**, configure parameters, and click **OK**.
>? A token ID should be a continuous tracking ID, such as the value of `set-cookies` after login.

<img src="https://qcloudimg.tencent-cloud.cn/raw/5e77d5be086b56b9f7ccd8f46456e072.png" style="zoom:67%;" />

**Field description**

  - **Token location**:	 It can be **HEADER**, **COOKIE**, **GET**, or **POST**. Here, **GET** and **POST** are HTTP request content parameters rather than HTTP header information.
  - **Token ID**: Token ID.
4. The configuration will take effect immediately upon completion. Then, bot traffic analysis will analyze traffic according to the field of the session feature.


## Setting a custom rule

1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-botconfig) and select **Configuration center** > **Bot and application security** on the left sidebar.
2. On the **Bot and application security** page, select the target domain name in the top-left corner and click **Bot management**.
![](https://qcloudimg.tencent-cloud.cn/raw/f755b07c980b5a8d12de1c72e80ef885.png)
3. Click the configuration page of a certain scenario and click **Custom rules**.
![](https://qcloudimg.tencent-cloud.cn/raw/224ab0225b42e198d1d9cf39010e4017.png)
4. On the **Bot custom setting** page, click **Add rule**, configure parameters, and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/b777a85876c5906b53f6473bc6f793e1.png)

**Field description**
 - **Policy name**: 	Policy name.
 - **Rule description**: The rule description.
 - **Rule Switch**: Enabled by default.
 - **Condition**: Conditions for matching bot policies. Up to 10 match conditions can be set, which are connected by the "AND" relationship. When you hover the cursor over a match condition, you can view its description.
 - **Action**: Action to be executed, as described below:
 <table>
<thead>
<tr>
<th align="left">Action Type</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody><tr>
<td align="left">Allow</td>
<td align="left">Session requests that match the set conditions will be allowed and will not be logged.</td>
</tr>
<tr>
<td align="left">Monitor</td>
<td align="left">Session requests that match the set conditions will be monitored and logged. You can view more information of the monitored sessions in the <b> Custom type</b> of the <b>Bot details</b>.</td>
</tr>
<tr>
<td align="left">CAPTCHA</td>
<td align="left">It is applicable only to access through browsers. Session requests that match the set conditions will be verified with a CAPTCHA. If they fail, they will be blocked; otherwise, they will be allowed within the penalty duration.</td>
</tr>
<tr>
<td align="left">Redirect</td>
<td align="left">Session requests that match the set conditions will be redirected to a specified URL of the current domain name within the specified penalty duration.</td>
</tr>
<tr>
<td align="left">Block</td>
<td align="left">Session requests that match the set conditions will be blocked. You can set the penalty duration to 5 to 10,080 minutes (7 days). You can view the blocking results in <a href="https://console.cloud.tencent.com/guanjia/log/attack">Attack logs</a> and view the blocked IPs in real time in the <a href="https://console.cloud.tencent.com/guanjia/ip/record">IP blocking status</a>.</td>
</tr>
</tbody></table>

 - **Priority**: Enter an integer between 1 and 100. A smaller value indicates a higher execution priority. When the priority is the same, rules more recently added are executed before the less recently added.
 - **Custom tag**: 	You can set a tag of **Friendly bots**, **Malicious bots**, **Normal traffic**, or **Suspicious bots**.
5. Now you can view the created rule in the policy list. Click **Edit** or **Delete** to edit or delete it.
![](https://qcloudimg.tencent-cloud.cn/raw/cd5a8064c9547ef872feafebda03c350.png)


## Legitimate bot
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-botconfig) and select **Configuration center** > **Bot and application security** on the left sidebar.
2. On the **Bot and application security** page, select the target domain name in the top-left corner and click **Bot management**.
![](https://qcloudimg.tencent-cloud.cn/raw/f755b07c980b5a8d12de1c72e80ef885.png)
3. In **Global settings**, click **Configure now** in the **Legitimate bots** module section.
4. On the **Legitimate bots** page, toggle on the switch to allow bots useful to the website data, such as search engines and external cooperative crawlers.
![](https://qcloudimg.tencent-cloud.cn/raw/6727c08a0431ee35503babe00470e502.png)
