This document describes how to modify parameters and view parameter modifications in the console.

## Notes
- To ensure instance stability, only some parameters can be modified in the console. These parameters are displayed on the **Parameter Settings** tab.
- If the modified parameter requires instance restart to take effect, the system will ask you if you wish to restart. We recommend you do so during off-peak hours and ensure that your application has a reconnection mechanism.
- Parameter task: You can query the details of parameter modification tasks in the task list.
 - 	Parameter modification tasks that haven't been executed yet can be canceled.
 - 	If a cluster already has an ongoing parameter modification task, modifying parameters again will fail.
- Global parameters can be modified only on a read-write instance. Once modified, they will be applied to all instances in the cluster. Local parameters can be set in individual instances in the cluster.

## Modifying one parameter
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb), find the target cluster in the cluster list, and click the cluster ID to enter the cluster management page.
2. On the cluster management page, click the **Parameter Settings** tab, select the target instance ID (global parameters can be modified only on a read-write instance and will take effect for the entire cluster once configured, while local parameters can be set in individual instances).
![](https://qcloudimg.tencent-cloud.cn/raw/23a197a8ce021f2c4543d7c1c77af8b0.png)
>!TDSQL-C for MySQL provides the **Global Parameters** field to help you quickly distinguish between parameters that take effect for the entire cluster and that can be set separately for different instances. Once configured, values of global parameters will take effect for all instances in the cluster, while values of local parameters will take effect only for the target instance and can be synced to other instances.
3. Find the target parameter in the parameter list and click <img src="https://main.qcloudimg.com/raw/788902e3f8c335cf17de420f7181c2a8.png"  style="margin:0;"> in the **Current Value** column.
>?You can quickly find the target parameter in the search box on the right of the **Parameter Settings** tab.
>![](https://qcloudimg.tencent-cloud.cn/raw/23a197a8ce021f2c4543d7c1c77af8b0.png)
4. Enter the target parameter value as prompted in the **Acceptable Values** column and click ![](https://qcloudimg.tencent-cloud.cn/raw/e8e0e48e149000b81beb9aa8401b144f.png) to save the change. You can also click ![](https://qcloudimg.tencent-cloud.cn/raw/63fbddc988994f6de30f39c9f3916295.png) to discard the change.
>?If the ![](https://qcloudimg.tencent-cloud.cn/raw/69a6a4c89f58c07672271750d8e8766e.png) icon is displayed before a parameter value, the parameter supports two value types: integer and formula. After the parameter is set based on a formula, the value will change automatically along with specifications such as CPU and memory (you can only modify numeric variables in a formula; for more information, see [Parameter Formula](https://www.tencentcloud.com/document/product/1098/53398)).
>![](https://qcloudimg.tencent-cloud.cn/raw/2a3bd2fa1ca1341f7526f04b1102c7fb.png)
>![](https://qcloudimg.tencent-cloud.cn/raw/60e15ba99673a26d898f703fc98fafb1.png)
>
>5. Click <img src="https://main.qcloudimg.com/raw/1f4c7f2e0744bc601efb5d9fb04a7a04.png"  style="margin:0;">. In the pop-up window, confirm that everything is correct, set **Execution Time**, and click **OK**.
>Execution Time:
 - If **Execute now** is selected, modification will be triggered immediately upon confirmation.
 - If **During maintenance time** is selected, the parameter will be modified within the maintenance time of the instance. For more information, see [Modifying Instance Maintenance Time](https://www.tencentcloud.com/document/product/1098/53399).
>!When you confirm the parameter modification, the system will ask you whether to restart the database instance. You can select **Execute now** or **During maintenance time**.
The page displayed when you modify a parameter that doesn't involve restart is as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/e0cf7cac1816b23e8042407e8698b89b.png)
The page displayed when you modify a parameter that involves restart is as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/19b0e8faa36b535f51b8f50011fb031f.png)
If the modified parameter is local, the system will ask you whether to sync its value to other instances.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/dhfB353_67.png)
You can also select the target instance ID in the drop-down list to sync the value to it.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/zsJU490_68.png)

## Batch modifying parameters
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb), find the target cluster in the cluster list, and click the cluster ID to enter the cluster management page.
2. On the cluster management page, click the **Parameter Settings** tab, select the target instance ID (global parameters can be modified only on a read-write instance and will take effect for the entire cluster once configured, while local parameters can be set in individual instances).
![](https://qcloudimg.tencent-cloud.cn/raw/23a197a8ce021f2c4543d7c1c77af8b0.png)
3. Click **Modify Parameters**.
4. Find the target parameters and modify their values in the **Current Value** column. After confirming that everything is correct, click **OK**.
5. In the pop-up window, the system will ask you whether to restart the database instance. If there are local parameters involved, you can choose whether to sync them to other instances. After confirming that everything is correct, select **Execute now** or **During maintenance time** and click **OK**.

## Modifying parameters by importing a parameter template
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb), find the target cluster in the cluster list, and click the cluster ID to enter the cluster management page.
2. On the cluster management page, click the **Parameter Settings** tab, select the target instance ID, and click **Import from Template**.
![](https://qcloudimg.tencent-cloud.cn/raw/9c4a1bbea12fc43cbe434e5f3388d20c.png)
3. In the pop-up window, select a parameter template and click **OK**.
4. After confirming that everything is correct, click **OK** in the top-left corner.
5. In the pop-up window, the system will ask you whether to restart the database instance. If there are local parameters involved, you can choose whether to sync them to other instances. After confirming that everything is correct, select **Execute now** or **During maintenance time** and click **OK**.

## Modifying parameters by importing a parameter configuration file
>!You cannot import formulas from a parameter configuration file.
>
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb), find the target cluster in the cluster list, and click the cluster ID to enter the cluster management page.
2. On the cluster management page, click the **Parameter Settings** tab, select the target instance ID, and click **Import Parameters**.
![](https://qcloudimg.tencent-cloud.cn/raw/9c4a1bbea12fc43cbe434e5f3388d20c.png)
3. In the pop-up window, select the file to be uploaded and click **Import and Overwrite Original Parameters**.
![](https://qcloudimg.tencent-cloud.cn/raw/877033e022af7ccde30d689c6a0cd5a1.png)
4. After confirming that everything is correct, click **OK** in the top-left corner.
5. In the pop-up window, the system will ask you whether to restart the database instance. If there are local parameters involved, you can choose whether to sync them to other instances. After confirming that everything is correct, select **Execute now** or **During maintenance time** and click **OK**.

## Exporting the parameter configuration as a file
>!Currently, when you export a parameter configuration file, formula-based parameter values will be automatically converted into integer values for export.
>
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb), find the target cluster in the cluster list, and click the cluster ID to enter the cluster management page.
2. On the cluster management page, click the **Parameter Settings** tab, select the target instance ID, click **Export Parameters**, and the exported file will be directly saved to the local file system.
![](https://qcloudimg.tencent-cloud.cn/raw/9c4a1bbea12fc43cbe434e5f3388d20c.png)

## Querying parameter modifications
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb), find the target cluster in the cluster list, and click the cluster ID to enter the cluster management page.
2. On the cluster management page, select the **Parameter Settings** tab and click **Recent Modifications** on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/9c4a1bbea12fc43cbe434e5f3388d20c.png)
3. On the page redirected to, you can select the target instance ID on the right to view the following fields of parameter modifications: **Parameter Name**, **Original Value**, **New Value**, **Modification Status**, and **Modification Time**.
![](https://qcloudimg.tencent-cloud.cn/raw/0a11e1f1e927f2e8332cdc318657ef0b.png)
