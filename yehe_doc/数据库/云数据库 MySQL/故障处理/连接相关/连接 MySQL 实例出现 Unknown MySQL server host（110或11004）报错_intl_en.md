## Issue
When you try to connect to a TencentDB for MySQL instance at its public network address, the system prompts `Unknown MySQL server host`.
![](https://main.qcloudimg.com/raw/b75b23dd5f306336145dab1719eeb1c7.png)

## Possible Causes
The public network address is incorrect.

## Solutions
Check whether the public network address of the instance is enabled and correctly entered.

## Troubleshooting
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb) and click the ID of the target instance in the instance list to enter the instance details page.
2. In the **Public Network Address** configuration item on the instance details page, check whether the public network address is enabled.
 - If so, proceed to [step 3](#step3).
 - If not, click **Enable** after **Public Network Address** and then proceed to [step 3](#step3).
>?
>- If the **Basic Info** section displays the public network address and port, the public network address has been enabled.
>- For more information on the restrictions on enabling the public network address, see [Connecting to MySQL Instance](https://intl.cloud.tencent.com/document/product/236/37788).
>
![](https://qcloudimg.tencent-cloud.cn/raw/40c8d7d175e9209992609daa3357cbf5.png)
3. [](id:step3)Check whether the public network address entered on the client is the same as that of the instance.
 - If so, proceed to [step 4](#step4).
 - If not, copy the **Public Network Address** as shown in the red box in the screenshot below, paste it on the client, and then proceed to [step 4](#step4).
![](https://qcloudimg.tencent-cloud.cn/raw/b6ebdab6bc0be840f1c79f983e3db9d6.png)
4. [](id:step4)Ping the public network address and check whether the DNS resolution is normal.
 - If so, the specific network latency will be returned, and the troubleshooting ends.
 - If not, the `Unknown host` error will be returned. In this case, [submit a ticket](https://cloud.tencent.com/act/event/connect-service) for assistance.

