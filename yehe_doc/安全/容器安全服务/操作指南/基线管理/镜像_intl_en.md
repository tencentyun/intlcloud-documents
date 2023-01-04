The **Image** page displays the baseline compliance details of images, including statistics, check information, and the list of check results.

## Viewing the Image Overview
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Baseline Management** > **Image** on the left sidebar.
2. On the **Image** page, the **Statistics** window displays the percentage of compliant images and the numbers of check items at the critical, high, medium, and low severity levels.
>? The percentage of compliant images is calculated as the number of compliant images/the total number of images (including those that failed the check).

![](https://qcloudimg.tencent-cloud.cn/raw/759dc59943c0a45900d4e812698484d3.png)
3. On the **Image** page, click **View** next to the proportion to pop up the image drawer, which displays the list of check results.
![](https://qcloudimg.tencent-cloud.cn/raw/cd041e25c522077703f70001003dba8b.png)
4. In the image drawer, click the search box and search for image check results by check item or ID.
![](https://qcloudimg.tencent-cloud.cn/raw/c05441614aff065b44319fe241f9813f.png)
5. In the image drawer, click ![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png) to select the target check item and click **Check again** > **OK** to check it again.
>? You can batch check image check items again by selecting them and clicking **Check again** next to ②.

![](https://qcloudimg.tencent-cloud.cn/raw/6dffc7eddd051ab71ad40a5834c10f89.png)
6. In the image drawer, click a check item to view the check results of a specified image.
![](https://qcloudimg.tencent-cloud.cn/raw/6d9348c28ba8fe70a2c73618e3bc575e.png)

## Viewing the Check Information
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Baseline Management** > **Image** on the left sidebar.
2. On the **Image** page, the **Check information** window displays the last baseline check time, check duration, and configured automatic check schedule.
![](https://qcloudimg.tencent-cloud.cn/raw/02e929735eff5f8078c61c2519884996.png)
3. On the **Image** page, click **Check again** to perform a baseline check on the image.
![](https://qcloudimg.tencent-cloud.cn/raw/a88ceafd92404f555f5b7fa32a082ece.png)
4. On the **Image** page, click **Baseline settings** to set the baseline policy and baseline ignored list.
![](https://qcloudimg.tencent-cloud.cn/raw/70561a356f1a32f22dac505266685275.png)

### Setting the baseline policy
The **Baseline policies** tab displays the baseline for the current asset check and the number of check items.
1. On the **Baseline policies** tab, toggle on or off ![](https://main.qcloudimg.com/raw/9053f4e9bc709aa720fccd5045eb8cd0.png) to enable or disable the periodic check against the current baseline.
![](https://qcloudimg.tencent-cloud.cn/raw/e5acfbc650bdc2be940725e053970776.png)
2. On the **Baseline policies** tab, click **Check cycle settings**.
![](https://qcloudimg.tencent-cloud.cn/raw/41ef230c8b1667ec5cfc40b1991d2496.png)
3. In the pop-up window, set the check cycle to every day, every 3 days, every 7 days, or a specified time range.
<img src="https://qcloudimg.tencent-cloud.cn/raw/468515d3c90e2f9aae562da9b1a7c851.png" style="zoom:67%;" />
4. Click **OK**.

### Baseline ignored list
The **Baseline ignored list** tab displays the ignored check items of the image.
1. On the **Baseline ignored list** tab, click the search box and search for image check items by check item.
![](https://qcloudimg.tencent-cloud.cn/raw/92e94da9a70bb837d105f9fc1ff8a9f0.png)
2. On the **Baseline ignored list** tab, click ![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png) to select the target check item and click **Unignore** to unignore it.
>? After a check item is unignored, it will be considered as normal.

## Viewing the List of Check Results
### Filtering and refreshing check items
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Baseline Management** > **Image** on the left sidebar.
2. On the **Image** page, click the search box and search for image check items by check item or ID.
![](https://qcloudimg.tencent-cloud.cn/raw/177ab63d51ca2e31f2fcb35f3aeff4ac.png)
3. On the **Image** page, click the type drop-down list in the top-left corner and filter image check items by type.
<img src="https://qcloudimg.tencent-cloud.cn/raw/51f80edd6ac2355e750db6bedb4d9edf.png" style="zoom:67%;" />
4. On the **Image** page, click the severity drop-down list in the top-left corner and filter image check items by severity.
<img src="https://qcloudimg.tencent-cloud.cn/raw/96ec298c3f633e98928d511d4b519fb7.png" style="zoom:67%;" />
5. On the **Image** page, click ![](https://main.qcloudimg.com/raw/84b6cc4d2eabf9ed7fc0bea43503bb1d.png) on the right of the **Operation** column to refresh the baseline check results.

### Checking a check item again
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Baseline Management** > **Image** on the left sidebar.
2. On the **Image** page, click ![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png) to select the target image check item and click **Check again** > **OK** to check it again.
>? You can batch check image check items again by selecting them and clicking **Check again** next to ②.

![](https://qcloudimg.tencent-cloud.cn/raw/b86f4e962892756f921db9d65184a9cb.png)

### Ignoring a check item
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Baseline Management** > **Image** on the left sidebar.
2. On the **Image** page, click ![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png) to select the target check item and click **Ignore** > **OK** to ignore it.
>? You can batch ignore check items by selecting them and clicking **Ignore** next to ②.

![](https://qcloudimg.tencent-cloud.cn/raw/e995bf121e6d4d935f057326859088b4.png)

### Custom list management
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Baseline Management** > **Image** on the left sidebar.
2. On the **Image** page, click ![](https://main.qcloudimg.com/raw/d42b27540eef9bf90a9e30f96b500bf3.png) to pop up the **Custom List Management** window.
3. In the pop-up window, select the target type and click **OK**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/f592340c35167f49335a737578916e32.png" style="zoom:67%;" />

#### Key fields in the list
1. ID: ID of the check item, which is globally unique.
2. Check item: Check content. You can click a check item to view the details.
3. Type: Type of the check item.
4. Baseline standard: Baseline standard of the check item.
5. Severity: Severity of the check item, which can be **Critical**, **High**, **Medium**, **Low**, or **Prompt**.
6. Result: Numbers of passed and failed assets for the current check item.
7. Operation: **Check again** or **Ignore**.