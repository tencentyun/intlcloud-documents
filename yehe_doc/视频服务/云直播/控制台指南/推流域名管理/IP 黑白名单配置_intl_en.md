This document shows you how to configure an IP allowlist/blocklist to filter requests and control access to streaming content.

## How It Works
- IP **allowlist**: Only IP addresses on the list can access your streaming content.
- IP **blocklist**: IP addresses on the list cannot access your streaming content.

## Reminders
- An IP allowlist/blocklist takes effect about five minutes after configuration.
- For an IP allowlist/blocklist configuration to apply to ongoing streams, you need to restart the streams.

## Prerequisites
- You have activated CSS and logged in to the [CSS console](https://console.cloud.tencent.com/live/livestat).
- You have added a [push domain](https://intl.cloud.tencent.com/document/product/267/35970).

[](id:set)
## Configuring an IP Allowlist/Blocklist
1. Select [Domain Management](https://console.cloud.tencent.com/live/domainmanage) on the left sidebar. Click the name of the target playback domain or click **Manage** on the right to enter the domain management page.
2. Select the **Access Control** tab and find **IP allowlist/blocklist**.
![](https://qcloudimg.tencent-cloud.cn/raw/0fb58ebd1e7bcbddfc50c687aa486281.png)
3. Click ![](https://qcloudimg.tencent-cloud.cn/raw/b64d8a4343b3a1e340db3adb9002db60.png) to enable IP allowlist/blocklist and complete the following settings:
![](https://qcloudimg.tencent-cloud.cn/raw/0c7ad338e825a85dce922fd9b9f5d0d4.png)

<table>
<thead><tr><th>Configuration Item</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Authenticate By</td>
<td>Allowlist or blocklist:<ul style="margin:0">
<li>You cannot select both.</li>
<li>If you configure an allowlist, only IP addresses on the list will be able to access your streaming content.</li>
<li>If you configure a blocklist, IP addresses on the list cannot access your streaming content.</li></ul></td>
</tr><tr>
<td>IP List</td>
<td>You can add up to 200 entries. Separate them with line breaks.<ul style="margin:0">
<li>You can enter IP addresses or IP ranges (/8/16/24). The “IP address: port number” format is not supported.</li>
<li>IPv6 is not supported currently.</li></ul></td>
</tr>
</tbody></table>

4. Click **Save** to save the configuration (it takes a while for the configuration to take effect).
![](https://qcloudimg.tencent-cloud.cn/raw/b69fefdda388b25f5adf09781094dcb9.png)

[](id:change)
## Modifying an IP Allowlist/Blocklist
1. Select [Domain Management](https://console.cloud.tencent.com/live/domainmanage) on the left sidebar. Click the name of the target playback domain or click **Manage** on the right to enter the domain management page.
2. Select the **Access Control** tab. In the **IP allowlist/blocklist** area, click **Edit**.
3. Modify the configuration and click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/61ded2bf69e3e38163b1b85716ff9477.png)

[](id:close)
## Disabling IP Allowlist/Blocklist
Follow the steps below to disable IP allowlist/blocklist:
1. Select [Domain Management](https://console.cloud.tencent.com/live/domainmanage) on the left sidebar. Click the name of the target playback domain or click **Manage** on the right to enter the domain management page.
2. Select the **Access Control** tab. In the **IP allowlist/blocklist** area, click ![img](https://main.qcloudimg.com/raw/e72f89a0deb6858428dc3e93ce7e7088.png) to disable IP allowlist/blocklist.
![](https://qcloudimg.tencent-cloud.cn/raw/a3f6197b29df76c3e4cc0deebb17890b.png)