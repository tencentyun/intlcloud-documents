This article guides you to use the Cloud Connect Network to interconnect the VPC with IDC of the same account.

## Prerequisites
- Your account is eligible for the beta testing of the Cloud Connect Network.
- Created the VPCs for interconnecting.
- Eliminating conflicts between the VPC subnet IP range and IDC IP range.

## Step 1: Creating a CCN Instance
1. Log in to [Tencent Cloud Console](https://console.cloud.tencent.com/) and select **Products** -> **Networking** -> **Virtual Private Cloud** to enter the VPC console.
2. Click **Cloud Connect Network** in the left pane to enter the CCN management page.
3. Click **Create**. 
 ![](https://main.qcloudimg.com/raw/8cb211dc827289135c6ab7dd0162a837.png)
4. Enter the name and description of the CCN instance in the pop-up window, select the ID of the VPC to be associated, then click **Create**.
![](https://main.qcloudimg.com/raw/a1ed83d1e415155a9ff8f255e578d5f8.png)
5. Associate a network instance (or do it after the CCN is created).
6. Click **OK** to create a CCN instance.

## Step 2: Associating a Network Instance
1. In the CCN list, click the CCN ID to be associated with a network instance to enter the details page.
2. On the new instance page, click **Associate Instance**. 
 ![](https://main.qcloudimg.com/raw/ed20b910cff3b387a92adf11ba7e8b5e.png)
3. In the pop-up window, select the network instance type and region, as well as a specific instance for making an association.  
![](https://main.qcloudimg.com/raw/48dbf2f66725c3ee2b7ec249d594cb1a.png)
> If you need to associate another network instance, click **+ Add**.
4. Click **OK** to add the selected network instance to CCN.

## Step 3: Checking the Route Table
If the IP ranges of the associated network instances conflict, there will be an invalid route. You can check it as follows:
1. In the CCN list, click the CCN ID of the route for the check.
2. In the details page, click **Route Tables** to view the route table.
3. Check if there is any invalid routing policy.
 ![](https://main.qcloudimg.com/raw/e802fd5a736644e0a6dc2757400adbf1.png)
4. For details of routing conflicts, see [Use Limits](https://intl.cloud.tencent.com/document/product/1003/30052#.E8.B7.AF.E7.94.B1.E9.99.90.E5.88.B6). To enable a conflicted route, see [Enabling a Route](https://intl.cloud.tencent.com/document/product/1003/30069).

## Step 4: Setting Cross-region Bandwidth Cap (Optional)

1. In the CCN list, click the CCN ID for which to set the bandwidth.
2. In the details page, click the **Monitoring** tab to view the metrics of the CCN.
3. Select the region for which to set the outbound bandwidth cap.
4. Set the outbound bandwidth cap for each region (1 Gbps by default).
 ![](https://main.qcloudimg.com/raw/1f08b6b4bd07f4f5d03b0ac478598944.png)

>Communications between CCN instances incur fees. For pricing details, see [Pricing](https://intl.cloud.tencent.com/document/product/1003/30053).

