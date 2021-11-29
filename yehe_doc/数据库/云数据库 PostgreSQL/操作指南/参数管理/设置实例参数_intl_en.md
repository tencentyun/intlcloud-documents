You can view and modify certain parameters and query parameter modification logs in [TencentDB for PostgreSQL console](https://console.cloud.tencent.com/postgres).

## Notes
- To ensure instance stability, only some parameters can be modified in the console. These parameters are displayed on the **Parameter Settings** page.
- If the modified parameter requires instance restart to take effect, the system will ask you if you wish to restart. We recommend that you do so during off-peak hours and ensure that your application has a reconnection mechanism.
>!Some are key parameters, modifying which may affect your use or the normal running of the instance. Therefore, exercise caution when modifying key parameters.

## Modifying Parameters in the Parameter List
### [Modifying parameters in batches](id:plxgcs)
1. Log in to the [TencentDB for PostgreSQL console](https://console.cloud.tencent.com/postgres). In the instance list, click an instance ID or **Manage** in the **Operation** column to access the instance management page.
2. On the **Parameter Settings** tab, click **Batch Modify Parameters**.
![](https://qcloudimg.tencent-cloud.cn/raw/0f16ab118a91292812af5209cc43e9c1.png)
3. Locate the desired parameters, and modify their values in the **Current Value** column. After confirming that everything is correct, click **Confirm Modification**.
![](https://qcloudimg.tencent-cloud.cn/raw/55e3eee69bbb800513284721eae8a066.png)
4. In the pop-up dialog box, confirm that all parameter values are correctly modified, and click **OK**.
>?If there are modified parameters requiring instance restart to take effect, click **Restart Now** and then the instance will be restarted. The modified parameters take effect only after the restart is completed.
>
<img src="https://qcloudimg.tencent-cloud.cn/raw/3a210d6dccf0384fd474b99644c5a3b0.png"  style="zoom:80%;">

### [Modifying one parameter](id:xgdgcs)
1. Log in to the [TencentDB for PostgreSQL console](https://console.cloud.tencent.com/postgres). In the instance list, click an instance ID or **Manage** in the **Operation** column to access the instance management page.
2. On the **Parameter Settings** tab, locate the desired parameter in the parameter list and click <img src="https://main.qcloudimg.com/raw/788902e3f8c335cf17de420f7181c2a8.png"  style="margin:0;"> in the **Current Value** column.
![](https://qcloudimg.tencent-cloud.cn/raw/93d71d1aab3594921e94397d22cd45f8.png)
3. Modify the value within the restrictions stated in the **Acceptable Values** column and click <img src="https://main.qcloudimg.com/raw/1f4c7f2e0744bc601efb5d9fb04a7a04.png"  style="margin:0;"> to save the modification. You can click <img src="https://main.qcloudimg.com/raw/2106cb4b9337a1a2fff5908581d2a908.png"  style="margin:0;"> to cancel the operation.
4. In the pop-up dialog box, confirm that the parameter value is correctly modified, and click **OK**.
>?If the modified parameter requires instance restart to take effect, click **Restart Now** and then the instance will be restarted. The modified parameter takes effect only after the restart is completed.

## Viewing Parameter Modification Logs
1. Log in to the [TencentDB for PostgreSQL console](https://console.cloud.tencent.com/postgres). In the instance list, click an instance ID or **Manage** in the **Operation** column to access the instance management page.
2. On the **Parameter Settings** tab, click **Recent Modifications** on the right.
3. You can view the recent parameter modification records here.
![](https://qcloudimg.tencent-cloud.cn/raw/e4f08b170b7cd1ff76bbc437330d6471.png)
