## Background
Currently, connection to a VPC over DC is only supported in Southeast Asia (Singapore) region. The public cloud can communicate with the customer's data center network over a VPC, and the agent can be directly installed.

If connection to a VPC over DC is not supported in a region, you need to use [CCN](https://intl.cloud.tencent.com/document/product/1003/30049) to connect the Direct Connect gateway (VPN) and the VPC. You need to [purchase](https://intl.cloud.tencent.com/document/product/1003/30053) the Direct Connect gateway and set up the connection to the VPC over DC.

## Directions
### Step 1. Check whether CCN is required for connection[](id:steps1)
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Asset Management** on the left sidebar.
2. On the **Asset Management** page, click **Servers** > **Install a TCSS agent** to pop up the **Installation guide** window on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/a8966391675dbad4dba489b1e080e50d.png)
2. In the pop-up window, select **Non-Tencent Cloud** for **Server vendor** and **Direct Connect** for **Network**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/67ee48c55bca284198185415f2f616a1.png" style="zoom:67%;" />
3. If you are in Southeast Asia (Singapore) region:
 - If you have a VPC connected to the non-Tencent Cloud data center network, select the VPC connected to Direct Connect and run the installation command.
 - If you find no VPC for connection to your non-Tencent Cloud data center network, see [step 2](#steps2).

### Step 2. Confirm the VPC for connection to Direct Connect[](id:steps2)
1. If you have no VPC in Southeast Asia (Singapore) region, log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1) and click **VPC**.
2. On the **VPC** page, click the drop-down list to select the target region and click **+ New**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/6ec8c48b834707b56627d275ed3f2fa9.png" style="zoom:67%;" />
3. In the **Create VPC** pop-up window, enter the required parameters and click **OK**.

### Step 3. Use CCN to connect the VPC to the non-Tencent Cloud data center network connected to Direct Connect
1. If you have the CCN instance connected to the non-Tencent Cloud data center network, add the VPC instance selected in [step 2](#steps2) to the CCN instance.
   a. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1) and select **CCN** on the left sidebar.  
   b. On the **CCN** page, click **Manage instances** > **Associated to** on the right.
   c. On the **Associated to** page, click **Add instance**, add the VPC instance selected in [step 2](#steps2) to the CCN instance, and click **OK**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/e87062c6be2c42a64397995fa57aaa58.png" style="zoom:67%;" />      
2. If you haven't configured a CCN instance, create one.
   a. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1) and select **CCN** on the left sidebar.  
   b. On the **CCN** page, click **+ New**.
   c. In the **Create CCN instance** pop-up window, enter the required parameters and click **OK**.
>?
>- Direct connect gateway: Select the Direct Connect gateway connected to your non-Tencent Cloud data center network.
>- VPC: Select the VPC instance selected in [step 2](#steps2).
>- If an IP range conflict occurs, go back to [step 2](#steps2) and select another VPC instance or create one.   

<img src="https://qcloudimg.tencent-cloud.cn/raw/6335d335ff39ead6c4a955ceeb918ac2.png" style="zoom:67%;" />

3. Go back to the [TCSS console](https://console.cloud.tencent.com/tcss) and get the installation command as instructed in [step 1](#steps1). You need to open ports 5574, 8080, 80, and 9080 of the IP described in [step 1](#steps1) for your non-Tencent Cloud data center network.