The **Kubernetes** page displays the baseline compliance details of Kubernetes assets against CIS Benchmarks, including statistics, check information, and the list of check results.
## Viewing the Kubernetes Overview
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Baseline Management** > **Kubernetes** on the left sidebar.
2. On the **Kubernetes** page, the **Statistics** window displays the check pass rate and the numbers of check items at the critical, high, medium, and low severity levels.
>? The check pass rate is calculated as the number of passed check items/the total number of check items.

![](https://qcloudimg.tencent-cloud.cn/raw/7fbfed49bd18af21c1a1b9943343bd8c.png)
3. On the **Kubernetes** page, click **View** next to the proportion to pop up the drawer, which displays the list of check results.
![](https://qcloudimg.tencent-cloud.cn/raw/1912eee952d4ff7e8fd3f07f0459bd8a.png)
4. On the **Kubernetes** page, click the search box and search for check results by check item or ID.
![](https://qcloudimg.tencent-cloud.cn/raw/1b60c8cac29456cd66333d003b3d35f7.png)
5. On the **Kubernetes** page, click ![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png) to select the target check item and click **Check again** > **OK** to check it again.
>? You can batch check Kubernetes check items again by selecting them and clicking **Check again** next to ②.

![](https://qcloudimg.tencent-cloud.cn/raw/ad8dae6e7ce9303a4cb619cbc9cda5da.png)

## Viewing the Check Information
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Baseline Management** > **Kubernetes** on the left sidebar.
2. On the **Kubernetes** page, the **Check information** window displays the last baseline check time, check duration, and configured automatic check schedule.
![](https://qcloudimg.tencent-cloud.cn/raw/901ced62853bf4d431d8b26a0b3e2e68.png)
3. On the **Kubernetes** page, click **Check again** to perform a baseline check on the Kubernetes asset.
![](https://qcloudimg.tencent-cloud.cn/raw/f5dc41b6075c1a8802c97ab2470ed989.png)
4. On the **Kubernetes** page, click **Baseline settings** to set the baseline policy and baseline ignored list.
![](https://qcloudimg.tencent-cloud.cn/raw/05fefe13302a647b824bba6626823934.png)

### Setting the baseline policy
The **Baseline policies** tab displays the baseline for the current asset check and the number of check items.
1. On the **Baseline policies** tab, toggle on or off ![](https://qcloudimg.tencent-cloud.cn/raw/1d06b60e53ef5b971de76fb26f686b85.png) to enable or disable the periodic check against the current baseline.
2. On the **Baseline policies** tab, click **Edit** next to the check cycle to pop up the **Check cycle setting** window.
![](https://qcloudimg.tencent-cloud.cn/raw/0b65b3b7f8acaeedda48ca5117cc28fb.png)
3. In the pop-up window, set the check cycle to every day, every 3 days, every 7 days, or a specified time range.
<img src="https://qcloudimg.tencent-cloud.cn/raw/c5e9236da94792617ba555dd5cea74be.png" style="zoom:67%;" />
4. Click **OK**.

### Baseline ignored list
The **Baseline ignored list** tab displays the ignored check items of the container.
1. On the **Baseline ignored list** tab, click the search box and search for Kubernetes check items by check item, server name, or server IP.
![](https://qcloudimg.tencent-cloud.cn/raw/223d321254fa4cef054d0d3675f46a99.png)
2. On the **Baseline ignored list** tab, click ![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png) to select the target Kubernetes check item and click **Unignore** to unignore it.
>? After a check item is unignored, it will be considered as normal.

## Viewing the List of Check Results
### Filtering and refreshing check items
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Baseline Management** > **Kubernetes** on the left sidebar.
2. On the **Kubernetes** page, click the search box and search for Kubernetes check items by check item.
![](https://qcloudimg.tencent-cloud.cn/raw/a96a15b44619d42b71103a5723c7886f.png)
3. On the **Kubernetes** page, click the type drop-down list in the top-left corner and filter Kubernetes check items by type.
<img src="https://qcloudimg.tencent-cloud.cn/raw/964b5c4e57fe5455964989c04a484413.png" style="zoom:67%;" />
4. On the **Kubernetes** page, click the severity drop-down list in the top-left corner and filter Kubernetes check items by severity.
<img src="https://qcloudimg.tencent-cloud.cn/raw/f89492734e22d6add50ec8347ab378d3.png" style="zoom:80%;" />
5. On the **Kubernetes** page, click ![](https://main.qcloudimg.com/raw/84b6cc4d2eabf9ed7fc0bea43503bb1d.png) on the right of the **Operation** column to refresh the Kubernetes check items.

### Checking a check item again
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Baseline Management** > **Kubernetes** on the left sidebar.
2. On the **Kubernetes** page, click ![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png) to select the target check item and click **Check again** > **OK** to check it again.
>? You can batch check Kubernetes check items again by selecting them and clicking **Check again** next to ②.

![](https://qcloudimg.tencent-cloud.cn/raw/be3e7416cf887fe231a4dec4ff43a8bd.png)

### Ignoring a check item
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Baseline Management** > **Kubernetes** on the left sidebar.
2. On the **Kubernetes** page, click ![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png) to select the target Kubernetes check item and click **Ignore** > **OK** to ignore it.
>? You can batch ignore Kubernetes check items by selecting them and clicking **Ignore** next to ②.

![](https://qcloudimg.tencent-cloud.cn/raw/8187c6fcff974e316a2728eef042dad6.png)

### Custom list management
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Baseline Management** > **Kubernetes** on the left sidebar.
2. On the **Kubernetes** page, click ![](https://main.qcloudimg.com/raw/d42b27540eef9bf90a9e30f96b500bf3.png) to pop up the **Custom List Management** window.
3. In the pop-up window, select the target type and click **OK**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/0e7ca1ea701c7f6172548aa75efff6d8.png" style="zoom:67%;" />

#### Key fields in the list
1. ID: ID of the check item, which is globally unique.
2. Check item: Check content. You can click a check item to view the details.
3. Type: Type of the check item.
4. Baseline standard: Baseline standard of the check item.
5. Severity: Severity of the check item, which can be **Critical**, **High**, **Medium**, **Low**, or **Prompt**.
6. Result: Numbers of passed and failed assets for the current check item.
7. Operation: **Check again** or **Ignore**.