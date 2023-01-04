The **Container** page displays the baseline compliance details of containers, including statistics, check information, and the list of check results.

## Viewing the Container Overview
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Baseline Management** > **Container** on the left sidebar.
2. On the **Container** page, the **Statistics** window displays the percentage of compliant containers and the numbers of check items at the critical, high, medium, and low severity levels.
>? The percentage of compliant containers is calculated as the number of compliant containers/the total number of containers (including those that failed the check).

![](https://qcloudimg.tencent-cloud.cn/raw/3a2434deb613e9bf5c29f4ab81b3438c.png)
3. On the **Container** page, click **View** next to the proportion to pop up the container drawer, which displays the list of check results.
![](https://qcloudimg.tencent-cloud.cn/raw/f49a2fa88fb61cefaa49880dd0ca4945.png)
4. In the container drawer, click the search box and search for container check results by check item or ID.
![](https://qcloudimg.tencent-cloud.cn/raw/054fdebd6e44a854f63615034b3402a0.png)
5. In the container drawer, click ![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png) to select the target container check item and click **Check again** > **OK** to check it again.
![](https://qcloudimg.tencent-cloud.cn/raw/7581a3db59fa5ca44f6d3487a17a744b.png)
6. In the container drawer, click a check item to view the check results of a specified container.
![](https://qcloudimg.tencent-cloud.cn/raw/77df6c07922a2da0bd8bbfe89cd1d892.png)

## Viewing the Check Information
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Baseline Management** > **Container** on the left sidebar.
2. On the **Container** page, the **Check information** window displays the last baseline check time, check duration, and configured automatic check schedule.
![](https://qcloudimg.tencent-cloud.cn/raw/8c92ffe8e087c229d0f68ab022c4f550.png)
3. On the **Container** page, click **Check again** to perform a baseline check on the container.
![](https://qcloudimg.tencent-cloud.cn/raw/7b82a3a6979d23c615156d6bb7102186.png)
4. On the **Container** page, click **Baseline settings** to set the baseline policy and baseline ignored list.
![](https://qcloudimg.tencent-cloud.cn/raw/d929438f40c2b787fb14e649860d47dd.png)

### Setting the baseline policy
The **Baseline policies** tab displays the baseline for the current asset check and the number of check items.
1. On the **Baseline policies** tab, toggle on or off ![](https://main.qcloudimg.com/raw/9053f4e9bc709aa720fccd5045eb8cd0.png) to enable or disable the periodic check against the current baseline.
![](https://qcloudimg.tencent-cloud.cn/raw/50f39ad938444c89f3ff54a7d70fdf04.png)
2. On the **Baseline policies** tab, click **Check cycle settings**.
![](https://qcloudimg.tencent-cloud.cn/raw/1e0edd49fe6d07246b0faa760a8c0ccb.png)
3. In the pop-up window, set the check cycle to every day, every 3 days, every 7 days, or a specified time range.
<img src="https://qcloudimg.tencent-cloud.cn/raw/dc5e798e4d088b594f5ec20752431e82.png" style="zoom:67%;" />
4. Click **OK**.

### Baseline ignored list
The **Baseline ignored list** tab displays the ignored check items of the container.
1. On the **Baseline ignored list** tab, click the search box and search for container check items by check item.
<img src="https://qcloudimg.tencent-cloud.cn/raw/a57c2df4ec45ad236b8f3603a2cdd911.png" style="zoom:67%;" />
2. On the **Baseline ignored list** tab, click ![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png) to select the target check item and click **Unignore** to unignore it.
>? After a check item is unignored, it will be considered as normal.

## Viewing the List of Check Results
### Filtering and refreshing check items
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Baseline Management** > **Container** on the left sidebar.
2. On the **Container** page, click the search box and search for check items by container check item or ID.
<img src="https://qcloudimg.tencent-cloud.cn/raw/9b176d794d544082cf5b3946c484e1ef.png" style="zoom:67%;" />
3. On the **Container** page, click the type drop-down list in the top-left corner and filter container check items by type.
<img src="https://qcloudimg.tencent-cloud.cn/raw/377965051b57173419d9d49d13f0efaf.png" style="zoom:67%;" />
4. On the **Container** page, click the severity drop-down list in the top-left corner and filter container check items by severity.
<img src="https://qcloudimg.tencent-cloud.cn/raw/9e1faad620683c83078bf40c5f1df7c6.png" style="zoom:67%;" />
3. On the **Container** page, click ![](https://main.qcloudimg.com/raw/84b6cc4d2eabf9ed7fc0bea43503bb1d.png) on the right of the **Operation** column to refresh the container check items.

### Checking a check item again
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Baseline Management** > **Container** on the left sidebar.
2. On the **Container** page, click ![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png) to select the target container check item and click **Check again** > **OK** to check it again.
>? You can batch check container check items again by selecting them and clicking **Check again** next to ②.

![](https://qcloudimg.tencent-cloud.cn/raw/97bbdf4d8983d16faa5f33df94880be9.png)

### Ignoring a check item
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Baseline Management** > **Container** on the left sidebar.
2. On the **Container** page, click ![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png) to select the target check item and click **Ignore** > **OK** to ignore it.
>? You can batch ignore check items by selecting them and clicking **Ignore** next to ②.

![](https://qcloudimg.tencent-cloud.cn/raw/19eaa1b115dcc167415fec3220224e2d.png)

### Custom list management
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Baseline Management** > **Container** on the left sidebar.
2. On the **Container** page, click ![](https://main.qcloudimg.com/raw/d42b27540eef9bf90a9e30f96b500bf3.png) to pop up the **Custom List Management** window.
3. In the pop-up window, select the target type and click **OK**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/1654a9c6e0e0e43a6f11b1e95d12c97c.png" style="zoom:67%;" />

#### Key fields in the list
1. Check item: Click a check item	 to view the details.
1. Failed check items: Number of failed check items.
2. Result: **Failed** if there are failed check items or **Passed** if all items are passed.
3. Last checked: The time of the last check.
