You can use HTTP headers to define fields that carry information about HTTP transactions. Header fields work on the domain level. This means the header fields you configure will take effect for all responses under your domain.


## Prerequisites
- You have logged in to the [CSS console](https://console.cloud.tencent.com/live).
- You have added a [playback domain name](https://intl.cloud.tencent.com/document/product/267/35970).



## Configuring HTTP Response Headers
1. Go to [Domain Management](https://console.cloud.tencent.com/live/domainmanage). Click the name of your playback domain or **Manage** on the right.
2. Select the **Advanced Configuration** tab.
![](https://qcloudimg.tencent-cloud.cn/raw/3dc3dc0a5a71fe671560ec32162d6381.png)
3. In the **HTTP response headers** area, click **Edit** to add new header fields or modify/delete existing header fields.
![](https://qcloudimg.tencent-cloud.cn/raw/7bc7b1573336ce7b97221dfeb835a780.png)
4. When adding a field, you can choose from preset fields (Access-Control-Allow-Methods, Access-Control-Max-Age, Access-Control-Expose-Headers) or customize a field. A custom field can be 1-100 characters long and can contain letters, numbers, and hyphens (-). The value of a header field can be 1-1,000 characters long and cannot contain Chinese characters.
![](https://qcloudimg.tencent-cloud.cn/raw/2d88d3599a30008822743d37038cf5eb.png)
![](https://qcloudimg.tencent-cloud.cn/raw/b065487fa03a250edaf82961f4d2c5cf.png)
5. When you are finished, Click **OK**. Your configuration may be in one of three statuses: yet to take effect, failed, or effective.
![](https://qcloudimg.tencent-cloud.cn/raw/de983bb2682da2521b33395096d6f77c.png)

## Preset Fields

<table>
<thead>
<tr>
<th style="width:230px">Header Field</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
</tr>
<tr>
<td>Access-Control-Allow-Methods</td>
<td>Indicates which HTTP methods are allowed for cross-origin requests. You can specify multiple methods at a time: <br>Access-Control-Allow-Methods: <code>POST, GET, OPTIONS</code>.</td>
</tr>
<tr>
<td>Access-Control-Max-Age</td>
<td>Indicates how long (seconds) the results of a preflight request can be cached
</tr>
<tr>
<td>Access-Control-Expose-Headers</td>
<td>Indicates which headers can be exposed to clients as part of the response
</tr>
</tbody></table>


## Limits
1. You can configure at most 10 header fields.
2. You cannot add two fields with the same name. To specify multiple values for a field, use this format: value 1, value 2, value 3.
3. If a field you configure is the same as a field used by the CSS backend, you will be asked to modify it.
4. A custom field can be 1-100 characters long and can contain letters, numbers, and hyphens (-).
5. The value of a field cannot be empty. It can be 1-1,000 characters long and cannot contain Chinese characters.
