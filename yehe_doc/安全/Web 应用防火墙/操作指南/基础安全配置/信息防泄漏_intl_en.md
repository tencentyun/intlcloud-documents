
This document describes the information leakage protection feature of WAF. It can filter and then replace, mask, and block sensitive information (e.g., identity card/mobile/bank card numbers), keywords, and response codes returned by websites. This helps meet the requirements of data security protection and cybersecurity classified protection by setting leakage protection rules as needed.

## Overview
With the leakage protection feature, you can add protection rules to filter the content returned by websites as needed, such as identity card/mobile/bank card numbers. You can also customize keywords (regex is supported) to filter order numbers and addresses and completely or partially replace them. Moreover, you can block or trigger alarms for status codes other than 200 returned by websites to meet compliance requirements.
>? CLB WAF doesn't support the data leakage protection feature. For more information on detailed specifications, see [Billing Overview](https://intl.cloud.tencent.com/document/product/627/47409).

## Prerequisites
You have [added a protected domain name](https://intl.cloud.tencent.com/document/product/627/35651) to SaaS WAF, and ensured the domain name is in normal protection.

## Adding a Rule
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-overview) and select **Configuration Center** > **Basic Security** on the left sidebar.
2. On the basic security page, select the target domain name in the top-left corner and click **Data leakage prevention**.
3. On the page displayed, click **Add rule**, and the rule adding window will pop up.
![](https://qcloudimg.tencent-cloud.cn/raw/4ae3fa9d2d0821de691aa771cdf71533.png)
4. In the pop-up window, configure relevant fields and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/67ecc95ee325f42991d09d7b1e60340d.png)

**Field description:**

- **Rule name**: Leakage protection rule name of up to 50 characters. You can search for rules by name in attack logs.
- **Condition**: Match condition for leakage protection. You can select sensitive information, keyword, or response code, and the match content and action type vary by the condition as follows:

<table>
<thead>
<tr>
<th>Condition</th>
<th>Content</th>
<th>Action</th>
</tr>
</thead>
<tbody><tr>
<td>Sensitive information</td>
<td>Identity card/mobile/bank card numbers</td>
<td>Alert, Replace all, Show the last 4 digits, Show the first 4 digits, and Block</td>
</tr>
<tr>
<td>Keyword</td>
<td>Keyword and regex</td>
<td>Alert, Replace all, and Blcok</td>
</tr>
<tr>
<td>Response code</td>
<td>400, 403, 404, other 4XX codes, 500, 501, 502, 504, and other 5XX codes</td>
<td>Alert and Block</td>
</tr>
</tbody></table>

- **Content**: The match content varies by match condition.
- **Protected path**: Specific path where the information needs to be protected from leakage. You can enter a directory or specific path as needed.
- **Action**: Action to be executed after the match condition is hit. You can view the relevant hit information in attack logs.

5. Once the rule takes effect, it will begin protecting the sensitive information returned in your web pages as shown in the following example that performs the Replace action (demo content):
 - **Before protection is enabled:**
![Before protection](https://mc.qcloudimg.com/static/img/a1f9740fafcf3f8913cc5d5c3370e7f7/image.png)
 - **After protection is enabled:**
![After protection](https://mc.qcloudimg.com/static/img/6a738492711125c684fa0f132ba74250/image.png)

## Search rules
1. On the [basic security page](https://console.cloud.tencent.com/guanjia/tea-baseconfig), select the target domain name in the top-left corner and click **Data leakage prevention**.
2. On the page displayed, click the search box to filter rules by keywords in a rule ID, rule name, and protected path.
![](https://qcloudimg.tencent-cloud.cn/raw/0e237366cf88c57820bce7c31cc5c6fe.png)

## Editing a Rule
1. On the [basic security page](https://console.cloud.tencent.com/guanjia/tea-baseconfig), select the target domain name in the top-left corner and click **Data leakage prevention**.
2. On the page displayed, select the target rule, click **Edit** in the **Operation** column, and the rule editing window will pop up.
![](https://qcloudimg.tencent-cloud.cn/raw/936ec721b7f2deac7bea5419f15193cc.png)
3. In the pop-up window, modify relevant parameters and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/d2b28cd20e28853e280d504dad5941f6.png)

## Deleting a Rule
1. On the [basic security page](https://console.cloud.tencent.com/guanjia/tea-baseconfig), select the target domain name in the top-left corner and click **Data leakage prevention**.
2. On the page displayed, select the target rule, click **Delete** in the **Operation** column, and the deletion confirmation window will pop up.
![](https://qcloudimg.tencent-cloud.cn/raw/af5c057466277c8bd350551e2e93bc59.png)
3. In the pop-up window, click **OK**.

