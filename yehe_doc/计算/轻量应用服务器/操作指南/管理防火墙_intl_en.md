## Overview
A firewall is an important method to protect the Lighthouse instance's network security. Its security protection features are equivalent to security groups in CVM. You can configure firewall rules to allow or reject access to Lighthouse instances over the private or public network.

<dx-alert infotype="explain" title="">
The firewall can control only the traffic flowing to the instance. All traffic going out from the instance is allowed by default.
</dx-alert>

## Concepts
- Outbound traffic: Traffic generated when data is transmitted from within the instance to outside the instance through the public or private network.
- Inbound traffic: Traffic generated when data is transmitted from outside the instance to within the instance through the public or private network.



## Firewall Rule
### Quota limits
Up to **100** firewall rules can be created for each Lighthouse instance.

### Parameters[](id:CompositionDescription)
A Lighthouse instance firewall can have multiple firewall rules, each of which contains the following parameters:
<table>
<tr>
<th width="10%">Parameter</th><th>Description</th>
</tr>
<tr>
<td><b>Type</b></td>
<td>
<ul class="params">
<li>Custom: Specify the protocol and port as needed.</li>
<li>**Common templates**, such as Windows login (3389) and Linux login (22), are provided. If you choose a template, the corresponding protocol and port are entered automatically and cannot be modified.</li>
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
<td>Port number. You can specify one or multiple ports.</td>
</tr>
<tr>
<td><b>Policy</b></td>
<td>
<ul class="params">
<li>Allow: Allow traffic to this port</li>
<li>Reject: Discard all data packets going to this port without any response.</li>
</ul>
</td>
</tr>
<tr>
<td><b>Notes</b></td>
<td>A short description of the rule</td>
</tr>
</table>

### Rule priorities
- Firewall rules have priorities.
The rule at the top of the list has the highest priority and will take effect first, while the rule at the bottom has the lowest priority and will take effect last.
- If there is a rule conflict, the rule with the higher priority will prevail by default.
- When traffic goes into an instance associated with the firewall, the firewall rules are calculated from top to bottom. If a rule is hit and takes effect, the subsequent rules do not take effect.
- You can adjust the priority of existing firewall rules as instructed in [Modifying firewall rule priority](#AdjustPriority).

## Directions

<dx-alert infotype="explain" title="">
You can add or delete firewall rules as follows, and the modification will take effect immediately.
</dx-alert>



### Adding a firewall rule

1. Log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index), select the target instance and enter the details page.
2. On the instance details page, select the **Firewall** tab, and click **Add a rule**.
![](https://qcloudimg.tencent-cloud.cn/raw/aa28f25617e5af8e6106ac19e0f973e7.png)
<dx-alert infotype="explain" title="">
- After a Lighthouse instance is created, the ICMP protocol will be allowed and ports 80 (HTTP service), 443 (HTTPS service), 22 (Linux SSH service), and 3389 (Windows RDP service) will be opened by default.
- You can modify the policies of these ports to **Reject**, or delete the firewall rules as needed on the instance details page. If the firewall rules are deleted, the port will be disabled by default.
</dx-alert>
3. In the **Create a rule** pop-up window, add a rule by referring to the following:
This document takes adding a rule of allowing traffic whose source IP is `192.168.1.1`, protocol type is `TCP`, and ports are `3306–20000` as an example. Add rules based on your actual conditions. For more information on rule parameters, see [Parameters](#CompositionDescription).
![](https://qcloudimg.tencent-cloud.cn/raw/241f5d89a005eac0171e3fb8c47c1b2a.png)
 - **Type**: To set the protocol type and port, select **Custom**. [](id:illustrate)
 - **Specified source**: To restrict the source IPs, select **Enable**.
 If **Enable** is not selected, the rule takes effect for all IPv4 source addresses. 
 - **Source IP**: The firewall rule only takes effect on the specified source IPs. You can enter IP addresses in the following formats:
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
    - **Allow**: Traffic to this port is allowed.
    - **Reject**: Data packets will be discarded without any response.
 - **Notes**: A short description of the rule for easier management.
5. Click **OK**.


### Deleting a firewall rule
1. Log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index), select the target instance and enter the details page.
2. On the instance details page, select the **Firewall** tab.
3. On the **Firewall** tab, select **Delete** on the right of the target firewall rule.
![](https://qcloudimg.tencent-cloud.cn/raw/70869b4342e0503a760b28d322845381.png)
4. In the pop-up prompt box, click **OK**.


### Modifying a firewall rule
1. Log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index), select the target instance and enter the details page.
2. On the instance details page, select the **Firewall** tab.
3. On the **Firewall** tab, select **Edit** on the right of target firewall rule.
![](https://qcloudimg.tencent-cloud.cn/raw/b5650ba57784fc1fdc397ca691e9efed.png)
4. In the pop-up window, modify the configurations with reference to [Parameters](#illustrate). Click **OK**.
<dx-alert infotype="explain" title="">
- If the **Type** is not **Custom**, the protocols and ports cannot be modified. If you want to modify them, please change the application type to **Custom**.
- You do not need to restart the Lighthouse instance after the modification.
</dx-alert>




## Related Operations
### Modifying firewall rule priority[](id:AdjustPriority)
1. Log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index), select the target instance and enter the details page.
2. On the instance details page, select the **Firewall** tab, and click **Sort**.
3. Select <img src="https://main.qcloudimg.com/raw/1b4e7395b052e5ce8f60d973c7db72b8.png" style="margin:-4px 0px"> before the target rule, drag the rule to the desired position, and drop it as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/2183698ee6a2d9be5e2e823bc9d3d841.png)
4. Click **Save** below the list.

<style>
.params{margin-bottom:0px !important}
</style>
