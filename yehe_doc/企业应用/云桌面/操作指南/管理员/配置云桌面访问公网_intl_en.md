## Directions
### Step 1. Create a NAT gateway
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/nat?rid=1), go to the **NAT Gateway** page, and click **New**. (Be sure to select the same region as the CVD instance.)
![](https://qcloudimg.tencent-cloud.cn/raw/5ef1bfb7c0034c3f6e9d3d35ceaf663b.png)
2. Enter the gateway name, select the VPC of the CVD instance for **Network**, select the **Gateway type** and **Outbound bandwidth cap** as needed (they can be modified after creation), select **Create EIP** for **Elastic IP**, and click **Activate now**.
<img style="width:600px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/2aae202d4671740d15140db0f98d7057.png" />
3. After confirming that everything is correct, click **Confirm order**.
<img style="width:600px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/405ff9204a834e868ec96d6ddf3be410.png" />
4. The NAT gateway is created.
![](https://qcloudimg.tencent-cloud.cn/raw/6cea97c518e881c09c57574a7b1eb96c.png)

### Step 2. Configure the route table
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/route?rid=1), go to the **Route tables** page, and click the target route table to edit it.
![](https://qcloudimg.tencent-cloud.cn/raw/7b728d1743adb0392997b998ff5b124b.png)
2. Click **+ Add routing policies**.
![](https://qcloudimg.tencent-cloud.cn/raw/46e41b38235995cd1585f9bdad7dea0f.png)
3. Enter `0.0.0.0/0` for **Destination**, select **NAT gateway** for **Next hop type**, and select the just created NAT gateway for **Next hop**.
![](https://qcloudimg.tencent-cloud.cn/raw/6861503fb9af71966c6040e781baf0a9.png)
>! Entering `0.0.0.0/0` for **Destination** indicates to route all outbound traffic to the NAT gateway.
4. **Enable** the created routing policy for your CVD instance to access the internet.
![](https://qcloudimg.tencent-cloud.cn/raw/eac1bd3744c1790e14dc32da5230d546.png)
