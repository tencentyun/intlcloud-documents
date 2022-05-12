## Overview
A firewall is an important method to protect the Lighthouse instance's network security. Its security protection features are equivalent to security groups in CVM. You can configure firewall rules to allow or reject access to Lighthouse instances over the private or public network.
>? A firewall can control only inbound traffic to the instance and allows all outbound requests by default.
>

## Firewall Rules
### Quota limits
Up to **100** firewall rules can be created for each Lighthouse instance.

### Parameters[](id:CompositionDescription)
A Lighthouse instance firewall can have multiple firewall rules, each of which contains the following parameters:
<table>
<tr>
<th width="10%">Parameter</th><th>Description</th>
</tr>
<tr>
<td><b>Application type</b></td>
<td>
<ul class="params">
<li>Custom: You can customize the protocol and port as needed.</li>
<li>Pre-installed application: Common firewall rule templates such as Windows login (3389) and Linux login (22) are provided. If you select this option, the corresponding protocol and port will be entered automatically and cannot be modified.</li>
</ul>
</td>
</tr>
<tr>
<td><b>Source</b></td>
<td>Specified IPv4 address or range.</td>
</tr>
<tr>
<td><b>Protocol</b></td>
<td>Protocol type. You can select TCP, UDP, or ICMP.</td>
</tr>
<tr>
<td><b>Port</b></td>
<td>Protocol port. You can specify one or multiple ports.</td>
</tr>
<tr>
<td><b>Policy</b></td>
<td>
<ul class="params">
<li>Allow: Access requests of this port are allowed.</li>
<li>Reject: Data packets will be discarded without any response.</li>
</ul>
</td>
</tr>
<tr>
<td><b>Remarks</b></td>
<td>A short description of the rule for easier management.</td>
</tr>
</table>

### Rule priorities
- Firewall rules have priorities.
The rules are prioritized from top to bottom. The rule at the top of the list has the highest priority and will take effect first, while the rule at the bottom has the lowest priority and will take effect last.
- If there is a rule conflict, the rule with the higher priority will prevail by default.
- When traffic goes in an instance in the firewall, the firewall rules will be matched sequentially from top to bottom. If a rule is matched successfully and takes effect, the subsequent rules will not be matched.
- You can adjust the priority of existing firewall rules as instructed in [Modifying firewall rule priority](#AdjustPriority).

## Directions
>?You can add or delete firewall rules as follows, and the modification will take effect immediately.

### Adding firewall rule

1. Log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index) and select the target instance to enter its details page.
2. On the instance details page, select the **Firewall** tab and click **Add rule** as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/aa28f25617e5af8e6106ac19e0f973e7.png)
>? After a Lighthouse instance is created, the ICMP protocol will be allowed and ports 80 (HTTP service), 443 (HTTPS service), 22 (Linux SSH service), and 3389 (Windows RDP service) will be opened by default.
>
3. In the **Create a rule** pop-up window, add a rule by referring to the following:
This document takes adding a rule of allowing traffic whose source IP is `192.168.1.1`, protocol type is `TCP`, and ports are `3306–20000` as an example. Add rules based on your actual conditions. For more information on rule parameters, see [Parameters](#CompositionDescription).
![](https://qcloudimg.tencent-cloud.cn/raw/241f5d89a005eac0171e3fb8c47c1b2a.png)
 - **Type**: To set the protocol type and port on your own, select **Custom**.
 - **Specified source**: To restrict the source IPs, select **Enable**.
 If you don't select **Enable**, the rule will take effect for all IPv4 source addresses. 
 - **Source IP**: The firewall rule will take effect for only entered source IP addresses. You can enter IP addresses in the following formats:
    - **Single IP**: Such as `192.168.1.1`.
    - **CIDR block**: Such as `192.168.1.0/24`.
    - **All IPv4 addresses**: `0.0.0.0/0`.
 - **Protocol**: You can select TCP, UDP, or ICMP. This document takes **TCP** as an example.
 - **Port**: You can select one or multiple ports ranging from 1 to 65535 and use commas to separate them. You can enter ports in the following formats:
    - **Single port**: Such as `80`.
    - **Multiple discrete ports**: Such as `80,443`.
    - **Continuous ports**: Such as `3306-20000`.
    - **All ports**: `ALL`.
 - **Policy**: **Allow** or **Refuse**. **Allow** is selected by default.
    - **Allow**: Access requests of this port are allowed.
    - **Reject**: Data packets will be discarded without any response.
 - **Notes**: A short description of the rule for easier management.
5. Click **OK**.


### Deleting firewall rule
1. Log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index) and select the target instance to enter its details page.
2. On the instance details page, select the **Firewall** tab.
3. On the **Firewall** tab, select **Delete** on the right of the target firewall rule as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/70869b4342e0503a760b28d322845381.png)
4. In the pop-up window, click **OK**.


## Related Operations
### Modifying firewall rule priority[](id:AdjustPriority)
1. Log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index) and select the target instance to enter its details page.
2. On the instance details page, select the **Firewall** tab and click **Sort**.
3. Select <img src="https://main.qcloudimg.com/raw/1b4e7395b052e5ce8f60d973c7db72b8.png" style="margin:-4px 0px"> before the target rule, drag the rule to the desired position, and drop it as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/2183698ee6a2d9be5e2e823bc9d3d841.png)
4. Click **Save** below the list.

<style>
.params{margin-bottom:0px !important}
</style>
