You can use HTTP headers to define fields that carry information about HTTP transactions. Header fields work on the domain level. This means the header fields you configure will take effect for all responses under your domain.


## Prerequisites
- You have logged in to the [CSS console](https://console.cloud.tencent.com/live).
- You have added a [playback domain name](https://intl.cloud.tencent.com/document/product/267/35970).

[](id:limit)
## Use Limits
- You can configure at most 10 header fields.
- You cannot add two fields with the same name. To specify multiple values for a field, use this format: `value 1, value 2, value 3`.
- If a field you configure is the same as a field used by the CSS backend, you will be asked to modify it.
- A custom field can be 1-100 characters long and can contain letters, numbers, and hyphens (-).
- The value of a field cannot be empty. It can be 1-1,000 characters long and cannot contain Chinese characters.


## Configuring HTTP Response Header
1. Go to [Domain Management](https://console.cloud.tencent.com/live/domainmanage). Click the name of your playback domain or click **Manage** on the right.
2. Select the **Advanced Configuration** tab.
![](https://qcloudimg.tencent-cloud.cn/raw/57a34fdc0b51c2f9384a677163c302ff.png)
3. In the **HTTP response headers** area, click **Edit** to add new header fields or modify/delete existing header fields.
![](https://qcloudimg.tencent-cloud.cn/raw/2fcc14051e1ed41d2896bbcea41c5293.png)
To add a header field, click **New**.
  - Select **Preset** to add a preset field: `Access-Control-Allow-Methods`, `Access-Control-Max-Age`, or `Access-Control-Expose-Headers`.
![](https://qcloudimg.tencent-cloud.cn/raw/416416d2cba4a0cff15a016ce987658c.png)

<table>
<thead><tr><th style="width:30%">Field</th><th>Description</th></tr></thead>
<tbody>
<tr>
<td>Access-Control-Allow-Methods</td>
<td>Indicates which HTTP methods are allowed for cross-origin requests. You can specify multiple methods at a time: <br><code>Access-Control-Allow-Methods: POST, GET, OPTIONS</code>.</td>
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

  - Select **Custom** to add a custom field.

>! The name of a custom field can be 1-100 characters long and can contain letters, numbers, and hyphens. The value of a custom field can be 1-1,000 characters long and cannot contain Chinese characters.

![](https://qcloudimg.tencent-cloud.cn/raw/31ee91ac9ef344cd26ea5c89ed73740e.png)
5. When you are finished, Click **OK**. Your configuration may be in one of three statuses: yet to take effect, failed, or effective.
![](https://qcloudimg.tencent-cloud.cn/raw/d8982f6db31f73de86eae641ab82b6ba.png)

