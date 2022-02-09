## I Description
When you try to connect to a TencentDB for MySQL instance via its public network address, the system prompts `Unknown MySQL server host`.
![](https://main.qcloudimg.com/raw/b75b23dd5f306336145dab1719eeb1c7.png)

## Possible Causes
The public network address is incorrect.

## Solutions
Check whether the public network address of the instance is enabled and correctly entered.

## Troubleshooting Procedure
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb) and click the ID of the target instance in the instance list to enter the instance details page.
2. In the **Public Network Address** configuration item on the instance details page, check whether the public network address is enabled.
 - If so, please proceed to [step 3](#step3).
 - If not, please click **Enable** after **Public Network Address** and then proceed to [step 3](#step3).
 >?
 >- If the **Basic Info** section displays the public network address and port, the public network address has been enabled.
 >- For more information on the restrictions on enabling the public network address, please see [Connecting to MySQL Instance](https://intl.cloud.tencent.com/document/product/236/37788).
 >
![](https://main.qcloudimg.com/raw/eb085d53fb6f569d763412bba5afcf11.png)
3. [](id:step3)Check whether the public network address entered on the client is the same as that of the instance.
 - If so, please proceed to [step 4](#step4).
 - If not, please copy the "public network address" as shown in the red box in the screenshot below, paste it on the client, and then proceed to [step 4](#step4).
 ![](https://main.qcloudimg.com/raw/27246f1777099c9e34b8dd26a89693eb.png)
4. [](id:step4)Ping the public network address and check whether the DNS resolution is normal.
 - If so, the specific network latency will be returned, and the troubleshooting ends.
 - If not, the `Unknown host` error will be returned. In this case, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

