After you confirm that a CLB instance has no traffic and is no longer needed, you can delete it via CLB Console or API.
Once deleted, the CLB instance will be completely terminated and cannot be recovered. We strongly recommend you unbind all real servers and wait for while before deleting any instance.

## Deleting CLB instance via the console
1. Log into the [CLB Console](https://console.cloud.tencent.com/loadbalance).
2. Find the CLB instance you want to delete and click **Delete** in the "Operation" column on the right.
 ![Delete](https://main.qcloudimg.com/raw/693acd714a4335920aea91b3ec4888f9.png)
3. The confirmation dialog box will pop up. After you read the operation security prompt, click **OK** to confirm the deletion.
The confirmation dialog box is as shown below. We strongly recommend you first confirm that the number of servers is **"0"**, CVM instance is **none**, and the security prompt is **green** before deleting the instance.
 ![Final confirmation dialog box](https://main.qcloudimg.com/raw/e3f3e2f08b4b9c4f61c478762de4b33a.png)
## Deleting CLB instance via API
For more information on detailed steps, please see [Deleting CLB Instances](https://intl.cloud.tencent.com/document/api/214/1257).

