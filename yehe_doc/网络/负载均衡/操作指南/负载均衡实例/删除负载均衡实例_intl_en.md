>?The monthly-subscribed instances cannot be deleted, but you can stop renewing them upon expiration.

After you confirm that a CLB instance has no traffic and is no longer needed, you can delete it via the CLB console or API.
Once deleted, the CLB instance will be completely terminated and cannot be recovered. We strongly recommend unbinding all real servers and observing for a while before deleting any instance.

## Deleting a CLB instance via the console
1. Log in to the [CLB console](https://console.cloud.tencent.com/loadbalance).
2. Find the CLB instance you want to delete and click **More** -> **Delete** in the **Operation** column on the right.
 ![](https://main.qcloudimg.com/raw/693acd714a4335920aea91b3ec4888f9.png)
3. The confirmation dialog box will pop up. After you read the operation security prompt, click **Submit** to confirm the deletion.
The dialog box is as shown below. We recommend confirming the deletion when there are **0** bound rules, **none** bound CVM instances, and a green tick under the **Notes About Operation Security** column.                              ![](https://main.qcloudimg.com/raw/e3f3e2f08b4b9c4f61c478762de4b33a.png)

## Deleting a CLB instance via API
For more information, please see [DeleteLoadBalancers](https://intl.cloud.tencent.com/document/api/214/1257).
