## Overview
The anti-replay plugin is provided by API Gateway to protect APIs from replay attacks. You can create an anti-replay plugin and bind it to an API to protect your backend services.

## Directions
### Step 1. Create a plugin
1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway).
2. On the left sidebar, click **Plugin** to enter the plugin list page.
3. Click **Create** in the top-left corner of the page and select **Anti-Replay** as the **Plugin Type** to create an anti-replay plugin.
<table>
<tr>
<th>Parameter</th>
<th>Required</th>
<th>Description</th>
</tr>
<tr>
<td>Forced anti-replay</td>
<td>No</td>
<td>Whether to enable forced anti-replay. It is disabled by default. If you need to enable it, you must add the `x-apigw-nonce` field to the request header.</td>
</tr>
<tr>
<td>Anti-replay period</td>
<td>No</td>
<td>Valid anti-replay period, which is 900 seconds by default. Value range: 1–1800.</td>
</tr>
</table>

### Step 2. Bind an API and make the plugin effective
1. Select the just created plugin in the list and click **Bind API** in the **Operation** column.
2. In the **Bind API** pop-up window, select the service, environment, and the target API.


## PluginData
<dx-codeblock>
:::  JSON
{
    "force_nonce":true, // Whether to enable forced anti-replay. It is disabled by default. If you need to enable it, you must add the `x-apigw-nonce` field to the request header.
    "nonce_ttl":1       //  Valid period of `nonce`, which is 900 seconds by default. Value range: 1–1800.
}
:::
</dx-codeblock>

