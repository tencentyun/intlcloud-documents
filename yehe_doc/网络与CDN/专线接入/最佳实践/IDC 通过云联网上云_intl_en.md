## Step 1: Create a CCN-based Direct Connect Gateway
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1) and click **Direct Connect Gateway** on the left sidebar.
2. Click **+New**.
3. In the pop-up window, enter a gateway name, select **CCN** for **Associate Network**, leave **CCN instance** empty, and click **OK**.

## Step 2: Add an IP Range to Publish to the Direct Connect Gateway
1. Locate the direct connect gateway just created and click the **ID/Name** to access its details page.
2. Select the <b>Publish IP Range</b> tab.
3. Click <b>Create</b> and enter a published IP range.

## Step 3: Create a CCN Instance
For more information , see [Creating a CCN Instance](https://intl.cloud.tencent.com/document/product/1003/30062).


## Step 4: Create a Dedicated Tunnel to Connect the CCN-based Direct Connect Gateway
1. Log in to the [Direct Connect console](https://console.cloud.tencent.com/dc/dc) and click **Dedicated Tunnels** on the left sidebar.
2. Click **+New**.
3. In the pop-up window, enter relevant information as prompted. Select **CCN** for **Access Network** and then select the CCN-based direct connect gateway just created.

## Step 5: Associate a Network Instance
Associate the network instances (including VPC and direct connect gateway) with the CCN instance for interconnection. For detailed directions, see [Associating Network Instances](https://intl.cloud.tencent.com/document/product/1003/30064).

