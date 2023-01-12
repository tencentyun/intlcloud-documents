This document describes how to adjust the database proxy configuration in the console, including the proxy specification, AZ, and node quantity.

## Prerequisites
You have enabled the database proxy. For more information, see [Enabling Database Proxy](https://intl.cloud.tencent.com/document/product/236/42052).

## Notes
- The database proxy will be automatically upgraded to the latest version during configuration adjustment if its version is old.
- If the selected proxy and the source instance are not in the same AZ and you access the instance through the proxy, the write performance will be reduced.
- If the recommended number of proxy nodes you calculated exceeds the maximum purchasable quantity, choose a higher proxy node specification.
- If resources are sufficient in the region, you can select up to three AZs and need to retain at least one AZ (the one in the first row).

## Impact description
Changing different configuration items has different impacts, some of which will not cause a momentary disconnection, while some will. The specific change items and their impacts are as detailed below:
**Scenario 1: Changing the proxy specification but not AZ or node quantity**

<table>
<thead><tr><th>Proxy Specification</th><th>AZ</th><th>Node Quantity</th><th>Load Balancing Mode</th><th>Switch Time</th><th>Impact</th></tr></thead>
<tbody>
<tr>
<td rowspan="4">Upgrade or downgrade</td><td rowspan="4">Unchanged</td><td rowspan="4">Unchanged</td><td rowspan="2">Automatic</td><td>During maintenance time</td><td rowspan="4">There will be a momentary disconnection lasting seconds. Make sure that your business has a reconnection mechanism.</td></tr>
<td>Upon upgrade completion</td></tr>
<td rowspan="2">Manual</td><td>During maintenance time</td></tr>
<td>Upon upgrade completion</td></tr>
</tbody></table>	

**Scenario 2: Changing the node quantity but not proxy specification or AZ**
<table>
<thead><tr><th>Proxy Specification</th><th>AZ</th><th>Node Quantity</th><th>Load Balancing Mode</th><th>Switch Time</th><th>Impact</th></tr></thead>
<tbody>
<tr>
<td rowspan="7">Unchanged</td><td rowspan="7">Unchanged</td><td rowspan="3">Increased</td><td rowspan="2">Automatic</td><td>During maintenance time</td><td rowspan="2">There will be a momentary disconnection lasting seconds. Make sure that your business has a reconnection mechanism.</td></tr>
<td>Upon upgrade completion</td></tr>
<td>Manual</td><td>-</td><td>There will be no momentary disconnections.</td></tr>
<td rowspan="4">Decreased</td><td rowspan="2">Automatic</td><td>During maintenance time</td><td rowspan="4">There will be a momentary disconnection lasting seconds. Make sure that your business has a reconnection mechanism.</td></tr>
<td>Upon upgrade completion</td></tr>
<td rowspan="2">Manual</td><td>During maintenance time</td></tr>
<td>Upon upgrade completion</td></tr>
</tbody></table>

**Scenario 3: Changing the AZ and node quantity but not proxy specification**
<table>
<thead><tr><th>Proxy Specification</th><th>AZ</th><th>Node Quantity</th><th>Load Balancing Mode</th><th>Switch Time</th><th>Impact</th></tr></thead>
<tbody>
<tr>
<td rowspan="23">Unchanged</td><td rowspan="7">Increased</td><td rowspan="3">Increased</td><td rowspan="2">Automatic</td><td>During maintenance time</td><td rowspan="2">There will be a momentary disconnection lasting seconds. Make sure that your business has a reconnection mechanism.</td></tr>
<td>Upon upgrade completion</td></tr>
<td>Manual</td><td>-</td><td>There will be no momentary disconnections.</td></tr>
<td rowspan="4">Decreased</td><td rowspan="2">Automatic</td><td>During maintenance time</td><td rowspan="20">There will be a momentary disconnection lasting seconds. Make sure that your business has a reconnection mechanism.</td></tr>
<td>Upon upgrade completion</td></tr>
<td rowspan="2">Manual</td><td>During maintenance time</td></tr>
<td>Upon upgrade completion</td></tr>
<td rowspan="8">Decreased</td><td rowspan="4">Increased</td><td rowspan="2">Automatic</td><td>During maintenance time</td></tr>
<td>Upon upgrade completion</td></tr>
<td rowspan="2">Manual</td><td>During maintenance time</td></tr>
<td>Upon upgrade completion</td></tr>
<td rowspan="4">Decreased</td><td rowspan="2">Automatic</td><td>During maintenance time</td></tr>
<td>Upon upgrade completion</td></tr>
<td rowspan="2">Manual</td><td>During maintenance time</td></tr>
<td>Upon upgrade completion</td></tr>
<td rowspan="8">Changed</td><td rowspan="4">Increased</td><td rowspan="2">Automatic</td><td>During maintenance time</td></tr>
<td>Upon upgrade completion</td></tr>
<td rowspan="2">Manual</td><td>During maintenance time</td></tr>
<td>Upon upgrade completion</td></tr>
<td rowspan="4">Decreased</td><td rowspan="2">Automatic</td><td>During maintenance time</td></tr>
<td>Upon upgrade completion</td></tr>
<td rowspan="2">Manual</td><td>During maintenance time</td></tr>
<td>Upon upgrade completion</td></tr>
</tbody></table>

## Directions
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), select the region at the top of the page, and click the ID of the target instance to enter the instance management page.
2. On the instance management page, select the **Database Proxy** tab.
3. On the **Overview** tab on the **Database Proxy** tab, select **Basic Info** > **Node Quantity** and click **Adjust Configurations**.
![](https://qcloudimg.tencent-cloud.cn/raw/f558c0dfbaa3f7686f397751749319ed.png)
4. In the pop-up window, modify the proxy specification, AZ, and node quantity of the database proxy as needed and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/efe6bb6da5af0df4a90cf52a6ed4486e.png)
5. In **Basic Info** on the **Database Proxy** tab, after the task status changes from **Upgrading** to **Running**, the configuration adjustment is completed.
>?
>- If you select **Upon upgrade completion**, after the configuration is adjusted, the system will automatically switch to the new configuration.
>- If you select **During maintenance time**, after the configuration is adjusted, the system will switch the configuration during the specified maintenance time period.
>- If you select **During maintenance time** but need to switch the configuration earlier due to your business requirements, after the configuration is adjusted, you can go to **Database Proxy** > **Overview** > **Basic Info** > **Status/Task** and click **Complete Now** after **Waiting for switch (after upgrade)**.
>- If you select manual rebalance after the configuration adjustment, perform the operation in **Overview** > **Connection Address** on the **Database Proxy** tab after the configuration is adjusted.

