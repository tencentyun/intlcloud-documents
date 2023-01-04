The **Docker server** page displays the baseline compliance details of servers, including statistics, check information, and the list of check results.

## Viewing the Docker Server Overview
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Baseline Management** > **Docker server** on the left sidebar.
2. On the **Docker server** page, the **Statistics** window displays the percentage of compliant servers and the numbers of check items at the critical, high, medium, and low severity levels.
>? The percentage of compliant Docker servers is calculated as the number of compliant Docker servers/the total number of Docker servers (including those that failed the check).

![](https://qcloudimg.tencent-cloud.cn/raw/20f6a4f66da98b0c446ecd839addf232.png)
3. On the **Docker server** page, click **View** next to the proportion to pop up the server drawer, which displays the list of check results.
4. In the Docker server drawer, click the search box and search for server check results by check item or ID.
![](https://qcloudimg.tencent-cloud.cn/raw/f42b3c4a6ccfd620cd738091c512c8b7.png)
5. In the Docker server drawer, click ![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png) to select the target check item and click **Check again** > **OK** to check it again.
>? You can batch check server check items again by selecting them and clicking **Check again** next to ②.

![](https://qcloudimg.tencent-cloud.cn/raw/a3360909cb6076aaa584a883c2c220c8.png)
6. In the Docker server drawer, click a check item to view the baseline check results of a specified Docker server.
![](https://qcloudimg.tencent-cloud.cn/raw/702b7e8c1070f5c0350e2e0d8067dddd.png)

## Viewing the Check Information
1. On the **Docker server** page, the **Check information** window displays the last baseline check time, check duration, and configured automatic check schedule.
![](https://qcloudimg.tencent-cloud.cn/raw/28b81698276618f55f4d6f9287874deb.png)
2. On the **Docker server** page, click **Check again** to perform a baseline check on the server.
![](https://qcloudimg.tencent-cloud.cn/raw/2b963706ac58cea9050402553d84e3ec.png)
3. On the **Docker server** page, click **Baseline settings** to set the baseline policy and baseline ignored list.
![](https://qcloudimg.tencent-cloud.cn/raw/fdd13194c19a1bd0b2e21e03a539741d.png)

### Setting the baseline policy
The **Baseline policies** tab displays the baseline for the current asset check and the number of check items.
1. On the **Baseline policies** tab, toggle on or off ![](https://qcloudimg.tencent-cloud.cn/raw/5e6cbf6d522b288cdd3c901e63ffc416.png) to enable or disable the periodic check against the current baseline.
2. On the **Baseline policies** tab, click **Edit** next to the check cycle to pop up the **Check cycle setting** window.
![](https://qcloudimg.tencent-cloud.cn/raw/695a6f1da2751aad52d65e8ff53d1c38.png)
3. In the pop-up window, set the check cycle to every day, every 3 days, every 7 days, or a specified time range.
<img src="https://qcloudimg.tencent-cloud.cn/raw/8e422b986b9e40605e3a29a9bedf6997.png" style="zoom:67%;" />
4. Click **OK**.

### Baseline ignored list
The **Baseline ignored list** tab displays the ignored check items of the server.
1. On the **Baseline ignored list** tab, click the search box and search for check items by check item or server name/IP.
![](https://qcloudimg.tencent-cloud.cn/raw/2c370630a0f1489a9259a73d57ff884d.png)
2. On the **Baseline ignored list** tab, click ![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png) to select the target server check item and click **Unignore** to unignore it.
>? After a check item is unignored, it will be considered as normal.

## Viewing the List of Check Results
### Filtering and refreshing check items
1. On the **Docker server** page, click the search box and search for Docker server check items by check item or ID.
![](https://qcloudimg.tencent-cloud.cn/raw/cc235c93d7649fd18a2125504d9097cf.png)
2. On the **Docker server** page, click the type drop-down list in the top-left corner and filter check items by type.
<img src="https://qcloudimg.tencent-cloud.cn/raw/4091bfe54b69562d999899439d7d12ed.png" style="zoom:67%;" />
3. On the **Docker server** page, click the severity drop-down list in the top-left corner and filter check items by severity.
<img src="https://qcloudimg.tencent-cloud.cn/raw/11430b1a4d9a33c8cc344c7525f473f7.png" style="zoom:67%;" />
4. On the **Docker server** page, click ![](https://main.qcloudimg.com/raw/84b6cc4d2eabf9ed7fc0bea43503bb1d.png) on the right of the **Operation** column to refresh the baseline check results.

### Checking a check item again
On the **Docker server** page, click ![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png) to select the target Docker server check item and click **Check again** > **OK** to check it again.
>? You can batch check server check items again by selecting them and clicking **Check again** next to ②.

![](https://qcloudimg.tencent-cloud.cn/raw/e829e61548f0058173bb5324eb1e65ad.png)

### Ignoring a check item
On the **Docker server** page, click ![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png) to select the target check item and click **Ignore** > **OK** to ignore it.
>? You can batch ignore check items by selecting them and clicking **Ignore** next to ②.

![](https://qcloudimg.tencent-cloud.cn/raw/598413d2e82af3dc0f0ff97ee7917981.png)

### Custom list management
1. On the **Docker server** page, click ![](https://main.qcloudimg.com/raw/d42b27540eef9bf90a9e30f96b500bf3.png) to pop up the **Custom List Management** window.
3. In the pop-up window, select the target type and click **OK**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/33d2472985cb38fe32c8a5ed8e88b048.png" style="zoom:67%;" />

#### Key fields in the list
1. ID: ID of the check item, which is globally unique.
2. Check item: Check content. You can click a check item to view the details.
3. Type: Type of the check item.
4. Baseline standard: Baseline standard of the check item.
5. Severity: Severity of the check item, which can be **Critical**, **High**, **Medium**, **Low**, or **Prompt**.
6. Result: Numbers of passed and failed assets for the current check item.
7. Operation: **Check again** or **Ignore**.