You can set referer blocklist/allowlist and rules to block/allow playback requests so as to protect live streaming content. You can also choose whether to allow empty referer.

## How to Configure

Referer URL supports HTTP protocol. CSS uses the referer field in an HTTP request to identify the source and verify the request, and then determine whether to accept or reject the request.

## Note
- Referer information is included in HTTP requests. Therefore, referer configuration is ineffective for non-HTTP (such as RTMP, WebRTC, QUIC) requests. If you want to restrict the access of RTMP requests, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
- Enabling, disabling, or modifying the referer takes effects in 15-20 minutes after the configuration. You don't need to push again.
- The referer hotlink protection feature verifies the referer information in the header of an HTTP request so as to check whether the request is valid and allow or reject live streaming accordingly. However, there may be cases where a forged referer bypasses the verification to hotlink the service. Therefore, we recommend you not strongly rely on referer for content protection.

## Prerequisites

- You have activated CSS service and logged in to the [CSS console](https://console.cloud.tencent.com/live/livestat).
- You have [added a playback domain name](https://intl.cloud.tencent.com/document/product/267/35970).

[](id:open)

## Enabling Referer

1. Select **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**, click the target **playback domain** or click **Manage** on the right to enter the domain management page.
2. In **Access Control** > **Referer Configuration**, click **Edit** to enter the referer configuration page.
 ![](https://main.qcloudimg.com/raw/32461edf0353c2c95925b74d80dc25b3.png)
3. Click ![](https://main.qcloudimg.com/raw/c032c517e25867ff592f128424154688.png) to enable the referer and configure as follows:
 ![](https://main.qcloudimg.com/raw/551044de4acd79683ae69cf106a87c0b.png)
<table id="setmess">
<tr><th width="14%">Configuration Item</th><th>Description</th>
</tr><tr>
<td>Referer Type</td>
<td>Select <b>Blocklist</b> or <b>Allowlist</b> as the referer type.
<ul style="margin:0">
<li>You cannot select both of them.</li>
<li>When the referer allowlist is configured, request sources on the list will be allowed to access the live streaming content while those not on the list will be blocked.</li>
<li>When the referer blocklist is configured, request sources on the list will be blocked to access the live streaming content while those not on the list will be allowed.</li>
</ul></td>
</tr><tr>
<td>Allow Empty Referer</td>
<td><ul style="margin:0">
<li>When this feature is enabled, access will be allowed for HTTP requests with empty or no referer field. Users can access the live stream URL directly via browsers.</li>
<li>When this feature is disabled, requests with empty referer will be rejected.</li>
</ul></td>
</tr><tr>
<td>Referer Patterns</td>
<td><ul style="margin:0">
<li>You can enter up to <b>100</b> patterns. Please separate them with line breaks.</li>
<li>You can enter <b>IPs</b> or <b>domain names</b>. The field supports path prefixes (domain names and IPs) and wildcards (domain names) for match. For example:<ul>
<li/>If you enter <code>101.1.0.1</code> and <code>www.test.com</code>, the configuration will take effect for both <code>101.1.0.1/157</code> and <code>www.test.com/tencent</code>.
<li/>If you enter <code>*.test.com</code>, the configuration will take effect for both <code>www.test.com</code> and <code>a.test.com</code>.</ul></li>
<li>If you enter no referer pattern, the blocklist/allowlist is not configured.</li>
</ul></td>
</tr></table>
4. Click **Save** to save the configuration.


[](id:change)
## Modifying Referer
1. Select **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**, click the target **playback domain** or click **Manage** on the right to enter the domain management page.
2. In **Access Control** > **Referer Configuration**, click **Edit** to enter the referer configuration page.
3. Modify the [configuration items](#setmess) and click **Save**.

![](https://main.qcloudimg.com/raw/a8c79376ed22b4e47f35e69411c6df10.png)

[](id:close)
## Disabling Referer
After [enabling the referer](#open), you can disable it by performing the following steps:

1. Select **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**, click the target **playback domain** or click **Manage** on the right to enter the domain management page.
2. In **Access Control** > **Referer Configuration**, click **Edit** to enter the referer configuration page.
3. Click ![](https://main.qcloudimg.com/raw/e72f89a0deb6858428dc3e93ce7e7088.png) to disable the referer.
4. Click **Save**.

![](https://main.qcloudimg.com/raw/eb36bc40cca9f19e198fc742256fed21.png)






