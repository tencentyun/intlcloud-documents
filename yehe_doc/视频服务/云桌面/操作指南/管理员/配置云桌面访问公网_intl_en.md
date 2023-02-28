## Directions
### Step 1. Create a NAT gateway
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/nat?rid=1), go to the **NAT Gateway** page, and click **New**. (Be sure to select the same region as the CVD instance.)
![](https://qcloudimg.tencent-cloud.cn/raw/0456c7b59e97c030d5b66d09395beee7.png)
2. Enter the gateway name, select the VPC of the CVD instance for **Network**, select the **Gateway type** and **Outbound bandwidth cap** as needed (they can be modified after creation), select **Create EIP** for **Elastic IP**, and click **Activate now**.
<img style="width:700px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/5d31698fc1e8c434793e433e1580bd65.png" />
3. After confirming that everything is correct, click **Confirm order**.
<img style="width:700px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/8bf2b471cf1d82997244c998abcd0a05.png" />
4. The NAT gateway is created.
![](https://qcloudimg.tencent-cloud.cn/raw/64b300d8f0e3785fa9ffec80f828e569.png)

### Step 2. Configure the route table
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/route?rid=1), go to the **Route tables** page, and click the target route table to edit it.
![](https://qcloudimg.tencent-cloud.cn/raw/04eab214cf8d02d4aad0001028445c34.png)
2. Click **+ Add routing policies**.
![](https://qcloudimg.tencent-cloud.cn/raw/04b975c22996f51349ff7739db168f04.png)
3. Enter `0.0.0.0/0` for **Destination**, select **NAT gateway** for **Next hop type**, and select the just created NAT gateway for **Next hop**.
![](https://qcloudimg.tencent-cloud.cn/raw/35001bab62e50f401631c7d4c1bfedb0.png)
>!  Entering `0.0.0.0/0` for **Destination** indicates to route all outbound traffic to the NAT gateway.

4. **Enable** the created routing policy for your CVD instance to access the internet.
![](https://qcloudimg.tencent-cloud.cn/raw/614be31065f8f1cda5633f39d2339244.png)
