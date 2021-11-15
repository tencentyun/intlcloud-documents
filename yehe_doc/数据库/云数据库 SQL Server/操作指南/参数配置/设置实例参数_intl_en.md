
You can view and modify certain parameters and query parameter modification logs in the TencentDB for SQL Server console.

## Notes
- To ensure instance stability, only some parameters can be modified in the console. These parameters are displayed on the **Parameter Settings** page.
- If the modified parameter requires instance restart to take effect, the system will ask you if you wish to restart. We recommend you do so during off-peak hours and ensure that your application has a reconnection mechanism.

## Batch Modifying Parameters
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver). In the instance list, click an instance ID or **Manage** in the **Operation** column to access the instance management page.
2. On the instance management page, select the **Parameter Configuration** > **Parameter Settings** tab and click **Batch Modify Parameters**.
![](https://main.qcloudimg.com/raw/eb99fc02ef937bcf284cde55c65defc7.png)
3. Select the target parameters and modify their values in the **Current Value** column. After confirming that everything is correct, click **OK**.
![](https://main.qcloudimg.com/raw/56e48d579e473235848479d9c0bfd809.png)
4. In the pop-up window, select the **Execution Mode** and click **OK**.
>?
>- If you select **Immediate execution**, the parameter modification task will be executed and take effect immediately.
>- If you select **During maintenance time**, the parameter modification task will be executed and take effect during the [instance maintenance time](https://intl.cloud.tencent.com/document/product/238/35785).
> 
![](https://main.qcloudimg.com/raw/09cd7df6181f175a265a3c0c29a71b25.png)

## Modifying One Parameter
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver). In the instance list, click an instance ID to access the instance management page.
2. On the instance management page, select the **Parameter Configuration** > **Parameter Settings** tab, select the row of the target parameter, and click ![img](https://main.qcloudimg.com/raw/788902e3f8c335cf17de420f7181c2a8.png) in the **Current Value** column to modify its value.
![](https://main.qcloudimg.com/raw/840cd20adf065b0fa30adefed997a640.png)
3. Enter the target parameter value as prompted in the **Current Value** column and click ![img](https://main.qcloudimg.com/raw/1f4c7f2e0744bc601efb5d9fb04a7a04.png) to save the change. You can click ![img](https://main.qcloudimg.com/raw/2106cb4b9337a1a2fff5908581d2a908.png) to cancel the operation.
![](https://main.qcloudimg.com/raw/896f3db37107b9e3c69d7b3cd1164f55.png)
4. In the pop-up window, select the **Execution Mode** and click **OK**.
>?
>- If you select **Immediate execution**, the parameter modification task will be executed and take effect immediately.
>- If you select **During maintenance time**, the parameter modification task will be executed and take effect during the [instance maintenance time](https://intl.cloud.tencent.com/document/product/238/35785).
>
![](https://main.qcloudimg.com/raw/f31ea4d1b771972dbde10e5fab9eb763.png)
