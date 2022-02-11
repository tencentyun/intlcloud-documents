
You can view and modify certain parameters and query parameter modification logs in [TDSQL-C console](https://console.cloud.tencent.com/cynosdb).

## Notes
- To ensure instance stability, only some parameters can be modified in the console. These parameters are displayed on the **Parameter Settings** page.
- If the modified parameter requires instance restart to take effect, the system will ask you if you wish to restart. We recommend that you do so during off-peak hours and ensure that your application has a reconnection mechanism.
- Currently, you cannot enter a custom formula to set a parameter.
- If you want to return to the default formula, clear the entered parameters and apply.

## Modifying Parameters in Parameter List
### [Modifying parameters in batches](id:plxgcs)
1. Log in to the [TDSQL-C console](https://console.cloud.tencent.com/cynosdb) and click a cluster ID in the cluster list to enter the cluster management page.
2. On the cluster management page, select the **Parameter Settings** tab and click **Modify Parameters**.
![](https://qcloudimg.tencent-cloud.cn/raw/4ba02fd67412019812d35d2b8a8053fb.png)
3. Locate the target parameters and modify their values in the **Current Value** column. After confirming that everything is correct, click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/eee113fe6f3229f26bad7791964da616.png)
4. In the pop-up window, confirm that everything is correct and click **OK**.

### [Modifying one parameter](id:xgdgcs)
1. Log in to the [TDSQL-C console](https://console.cloud.tencent.com/cynosdb) and click a cluster ID in the cluster list to enter the cluster management page.
2. On the **Parameter Settings** tab, locate the target parameter in the parameter list and click <img src="https://main.qcloudimg.com/raw/788902e3f8c335cf17de420f7181c2a8.png"  style="margin:0;"> in the **Current Value** column.
3. Modify the value within the restrictions stated in the **Acceptable Values** column and click <img src="https://main.qcloudimg.com/raw/1f4c7f2e0744bc601efb5d9fb04a7a04.png"  style="margin:0;"> to save the modification. You can click <img src="https://main.qcloudimg.com/raw/2106cb4b9337a1a2fff5908581d2a908.png"  style="margin:0;"> to cancel the operation.
![](https://qcloudimg.tencent-cloud.cn/raw/2a3bd2fa1ca1341f7526f04b1102c7fb.png)
4. In the pop-up window, confirm that everything is correct and click **OK**.

## Modifying Parameters by Importing Parameter Template
1. Log in to the [TDSQL-C console](https://console.cloud.tencent.com/cynosdb) and click a cluster ID in the cluster list to enter the cluster management page.
2. On the cluster management page, select the **Parameter Settings** tab and click **Import from Template**.
![](https://qcloudimg.tencent-cloud.cn/raw/eb5e72ef067744d50e1d744e31572998.png)
3. In the pop-up window, select a parameter template and click **OK**.
4. After confirming that everything is correct, click **OK** in the top-left corner.
5. In the pop-up window, confirm that everything is correct and click **OK**.


## Modifying Parameters by Importing Parameter Configuration File
1. Log in to the [TDSQL-C console](https://console.cloud.tencent.com/cynosdb) and click a cluster ID in the cluster list to enter the cluster management page.
2. On the cluster management page, select the **Parameter Settings** tab and click **Import Parameters**.
![](https://qcloudimg.tencent-cloud.cn/raw/9c4a1bbea12fc43cbe434e5f3388d20c.png)
3. In the pop-up window, select a file to upload and click **Import and Overwrite Original Parameters**.
![](https://qcloudimg.tencent-cloud.cn/raw/877033e022af7ccde30d689c6a0cd5a1.png)
4. After confirming that everything is correct, click **OK** in the top-left corner.
5. In the pop-up window, confirm that everything is correct and click **OK**.

## Exporting Parameter Configuration as File
1. Log in to the [TDSQL-C console](https://console.cloud.tencent.com/cynosdb) and click a cluster ID in the cluster list to enter the cluster management page.
2. On the cluster management page, select the **Parameter Settings** tab and click **Export Parameters** to export the parameter configuration file.

## Exporting Parameter Configuration as Template
1. Log in to the [TDSQL-C console](https://console.cloud.tencent.com/cynosdb) and click a cluster ID in the cluster list to enter the cluster management page.
2. On the cluster management page, select the **Parameter Settings** tab and click **Save as Template** to save the existing parameter configuration as a parameter template.

## Subsequent Operations
- You can use templates to manage database parameters in batches. For more information, see [Managing Parameter Template](https://intl.cloud.tencent.com/document/product/1098/44601).
- For suggestions for configuration of key parameters, see [Suggestions on Parameter Settings](https://intl.cloud.tencent.com/document/product/1098/44600).

