## Prerequisites
Purchase a Web Application Firewall (WAF) plan with [package for bot traffic management](https://www.tencentcloud.com/document/product/627/47799#bot-.E8.A1.8C.E4.B8.BA.E7.AE.A1.E7.90.86.E4.BB.B7.E6.A0.BC.E8.AF.B4.E6.98.8E), and enabled bot analytics features for your domain name.

## Bot allowlist
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-botconfig) and select **Configuration Center** > **Bot and Application Security** on the left sidebar.
2. On the **Bot and Application Security** page, select the target domain name in the top-left corner and choose **Bot management** > **Bot allowlist**.
![](https://qcloudimg.tencent-cloud.cn/raw/83d8c1b878537a6b516703040524b92d.png)
3. On the bot allowlist settings page, click **Add rule**, configure parameters, and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/b777a85876c5906b53f6473bc6f793e1.png)
**Field description**
 - **Rule name:**: The rule name.
 - **Rule description:** The rule description.
 - **On/Off:** Indicates whether the rule is enabled. A rule is enabled by default.
 - **Condition:** Conditions for matching bot policies. Up to 10 match conditions can be set, which are connected by the "AND" relationship. When you hover the cursor over a match condition, you can view its description.
 - **Priority:** Enter an integer between 1 to 100. A smaller integer indicates a higher priority. If the priority values are the same, the latest rule prevails.
 - **Custom tag**: You can set the tag to **Friendly bot** or **Normal traffic**.

4. Now you can view the created rule in the policy list. Click **Edit** or **Delete** to edit or delete it.
![](https://qcloudimg.tencent-cloud.cn/raw/f0a6a41ba840f5b4a6803c9d5e2db702.png)
5. Priority from high to low: Bot allowlist > Scenario 1 (priority 1) > Scenario 2 (priority 2) > ... > Scenario n (priority m).

## Session Management

This feature is similar to session setting in [CC protection](https://www.tencentcloud.com/document/product/627/11709). With different token IDs, you can differentiate between access requests from different requesters through the same IP and record their behavior features.

You can also use token IDs to continuously track the access behaviors of different requesters. This helps identify bot access behaviors through residential or public egress IPs and record session features when proxy IPs are frequently changed.

1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-botconfig) and select **Configuration Center** > **Bot and Application Security** on the left sidebar.
2. On the **Bot and Application Security** page, select the target domain name in the top-left corner and choose **Bot management** > **Bot Protection**.
3. On the **Bot Protection** page, click **Configure now** in the **Session management** area.
![](https://qcloudimg.tencent-cloud.cn/raw/1cfea7e397c73f6a54dec99d2e64bf76.png)
4. On the **Session management** page, click **Add a configuration**, configure parameters, and click **OK**.
>?A token ID should be a continuous tracking ID, such as the value of `set-cookies` after login.

![](https://qcloudimg.tencent-cloud.cn/raw/0adee739bf552682d4b0bb3e611184e1.png)
**Field description**

  - **Token location:** HEADER, COOKIE, GET, or POST. Here, GET and POST are HTTP request parameters rather than HTTP headers.
  - **Token ID**: Token ID.
5. The configuration will take effect immediately upon completion. Then, bot traffic analysis will analyze traffic according to the field of the session feature.


## Setting a custom rule
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-botconfig) and select **Configuration Center** > **Bot and Application Security** on the left sidebar.
2. On the **Bot and Application Security** page, select the target domain name in the top-left corner and choose **Bot management** > **Bot Protection**.
3. In the **Scene management** area, select the target scene, and click **View configuration**.
![](https://qcloudimg.tencent-cloud.cn/raw/f65afdb7aa9f4743ded7268376d1d86f.png)
4. On the scene details page, click **Add rule** in the **Custom Rules** area.
![](https://qcloudimg.tencent-cloud.cn/raw/5a0786b0796837e926b964a52348926b.png)
5. In the **Add custom session feature** pop-up window, configure relevant parameters and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/0c8eee00b5858e81d8b62bbd95f6bf19.png)

**Field description**
 - **Rule name:**: The rule name.
 - **Rule description:** the rule description.
 - **Rule Switch:** enabled by default.
 - **Condition:** Conditions to manage detected bots. You can set up to 10 conditions, which are combined with AND. Mouse over a condition to see the details.
 - **Action**: Action to be executed.

<table>
<thead>
<tr>
<th align="left">Action</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody><tr>
<td align="left">Trust</td>
<td align="left">Allow hit requests without logging.</td>
</tr>
<tr>
<td align="left">Monitor</td>
<td align="left">Allow and log hit requests. You can check details in the **Custom type** of the **Bot details**.</td>
</tr>
<tr>
<td align="left">CAPTCHA</td>
<td align="left">This action is applicable only to the access through browsers. Session requests that match the specified conditions will be verified through CAPTCHA. If they fail, they will be blocked. Otherwise, the access is allowed.</td>
</tr>
<tr>
<td align="left">Redirect</td>
<td align="left">Session requests that match the specified conditions will be redirected to a specific URL of the current domain name.</td>
</tr>
<tr>
<td align="left">Block</td>
<td align="left">Block and log the hit requests. You can check the logs in <a href="https://console.cloud.tencent.com/guanjia/log/attack">Attack Logs</a>. To check the blocked IPs, go to <a href="https://console.cloud.tencent.com/guanjia/ip/record">IP blocking status</a>.</td>
</tr>
</tbody></table>

 - **Priority:** Enter an integer between 1 to 100. A smaller integer indicates a higher priority. If the priority values are the same, the latest rule prevails.
 - **Custom tag**: You can set the tag to **Friendly bot**, **Malicious bot**, **Normal traffic**, or **Suspicious bot**.

6. Now you can see the created rule in the policy list. 
![](https://qcloudimg.tencent-cloud.cn/raw/009b448b6a4f00883fd035a645525e12.png)

## Legitimate Bots
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-botconfig) and select **Configuration Center** > **Bot and Application Security** on the left sidebar.
2. On the **Bot and Application Security** page, select the target domain name in the top-left corner and choose **Bot management** > **Bot Protection**.
3. On the **Bot Protection** page, click **Configure now** in the **Legitimate bots** area.
![](https://qcloudimg.tencent-cloud.cn/raw/ee2f4bc77179387c0fa3397347571618.png)
4. On the **Legitimate bots** page, toggle on the switch to allow bots useful to the website data, such as search engines and external cooperative crawlers.
![](https://qcloudimg.tencent-cloud.cn/raw/1b4e09fb1ca78b1500c6b12f9259a878.png)
