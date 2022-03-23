You can adjust the specification and number of nodes of the database proxy in the console.

## Prerequisites
You have [enabled the database proxy](https://intl.cloud.tencent.com/document/product/236/42052).

## Notes
When you adjust the configuration, if there is a pending update of the database proxy version, the version will be automatically upgraded during the adjustment.

## Impact Description
Changing different configuration items has different impacts, some of which will not cause a momentary disconnection, while some will. The specific change items and their impacts are as detailed below:
<table>
<thead><tr><th>Proxy Specification</th><th>Node Quantity</th><th>Proxy Kernel Version</th><th>Load Balancing Mode</th><th>Impact</th></tr></thead>
<tbody>
<tr>
<td rowspan="4">Changed</td><td rowspan="4">Increased</td><td rowspan="2">Up to date</td><td>Automatic</td><td rowspan="12">There will be a disconnection lasting seconds. Make sure that your business has a reconnection mechanism.</td></tr>
<tr>
<td>Manual</td></tr>
<tr>
<td rowspan="2">Out of date</td><td>Automatic</td></tr>
<tr>
<td>Manual</td></tr>
<tr>
<td rowspan="4">Changed</td><td rowspan="4">Decreased</td><td rowspan="2">Up to date</td><td>Automatic</td></tr>
<tr>
<td>Manual</td></tr>
<tr>
<td rowspan="2">Out of date</td><td>Automatic</td></tr>
<tr>
<td>Manual</td></tr>
<tr>
<td rowspan="4">Unchanged</td><td rowspan="4">Decreased</td><td rowspan="2">Up to date</td><td>Automatic</td></tr>
<tr>
<td>Manual</td></tr>
<tr>
<td rowspan="2">Out of date</td><td>Automatic</td></tr>
<tr>
<td>Manual</td></tr>
<tr>
<td rowspan="4">Unchanged</td><td rowspan="4">Increased</td><td rowspan="2">Up to date</td><td>Automatic</td><td>There will be a disconnection lasting seconds. Make sure that your business has a reconnection mechanism.</td></tr>
<tr>
<td>Manual</td><td>There will be no momentary disconnections.</td></tr>
<tr>
<td rowspan="2">Out of date</td><td>Automatic</td><td>There will be a disconnection lasting seconds. Make sure that your business has a reconnection mechanism.</td></tr>
<td>Manual</td><td>There will be no momentary disconnections.</td></tr>
</tbody></table>	


## Directions
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), select the region at the top of the page, and click the ID of the target instance to enter the instance management page.
2. On the instance management page, select the **Database Proxy** tab.
3. On the **Overview** tab on the **Database Proxy** tab, click **Adjust Configurations** on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/f558c0dfbaa3f7686f397751749319ed.png)
4. In the pop-up window, select the switch time and click **OK**.
   - **Proxy Specification**: Currently, you can select 2-core 4000 MB, 4-core 8000 MB, or 8-core 16000 MB.
   - **Node Quantity**: To ensure the high availability of proxy, purchase at least two proxy nodes.
   - **Switch Time**:
     - During maintenance time: The switch will be performed during the maintenance time, which can be modified on the instance details page.
     - Upon upgrade completion: The switch will be performed immediately after the upgrade is completed.
![](https://qcloudimg.tencent-cloud.cn/raw/efe6bb6da5af0df4a90cf52a6ed4486e.png)
5. In **Basic Info** on the **Database Proxy** tab, after the task status changes from **Upgrading** to **Running**, the configuration adjustment is completed.
>?
>- If you select **Upon upgrade completion**, after the configuration is adjusted, the system will automatically switch to the new configuration.
>- If you select **During maintenance time**, after the configuration is adjusted, the system will switch the configuration during the specified maintenance time period.
>- If you select **During maintenance time** but need to switch the configuration earlier due to your business requirements, after the configuration is adjusted, you can go to **Database Proxy** > **Overview** > **Basic Info** > **Status/Task** and click **Complete Now** after **Waiting for switch (after upgrade)**.
>
![](https://qcloudimg.tencent-cloud.cn/raw/6f291e1dd9b78893d4b4e4947e5afd1e.png)

