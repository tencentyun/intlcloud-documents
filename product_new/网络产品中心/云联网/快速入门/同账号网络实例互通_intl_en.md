This article guides you to use the cloud connect network to interconnect the VPC with IDC of the same account.

## Prerequisites
- Your account is eligible for the [beta testing](https://cloud.tencent.com/apply/p/tp2478t9skn) of the cloud connect network.
- The VPCs to be interconnected has been created.
- There are no conflicts between the VPC subnet IP range and IDC IP range.

## Step 1: Creating a CCN Instance
1. Log in to [Tencent Cloud Console](https://console.cloud.tencent.com/) and select **Products** -> **Networking** -> **Virtual Private Cloud** to enter the VPC console.
2. Click **Cloud Connect Network** in the left pane to enter the CCN management page.
3. Click **Create**. 
 ![](https://main.qcloudimg.com/raw/eb943bbeed18cfb7ebdcb1fb557cc6d5.png)
4. Enter the name and description of the CCN instance in the pop-up window, select the ID of the VPC to be associated, then click **Create**.
![](https://main.qcloudimg.com/raw/b4f5777d0e79324c8570babd91165fa0.png)
5. Associate a network instance (or do it after the CCN is created).
6. Click **OK** to create a CCN instance.

## Step 2: Associating a Network Instance
1. In the CCN list, click the ID of the CCN to be associated with a network instance to enter the details page.
2. On the new instance page, click **Associate Instance**. 
 ![](https://main.qcloudimg.com/raw/ed20b910cff3b387a92adf11ba7e8b5e.png)
3. In the pop-up window, select the network instance type, region and a instance.
![](https://main.qcloudimg.com/raw/48dbf2f66725c3ee2b7ec249d594cb1a.png)
>? If you need to associate another network instance, click **+ Add**.
4. Click **OK** to add the selected network instance to CCN.

## Step 3: Checking the Route Table
If the IP ranges of the associated network instances conflict, there will be an invalid route. You can check it as follows:
1. In the CCN list, click the CCN ID for which to check the route.
2. In the details page, click **Route Tables** to view the route table.
3. Check if there is any invalid routing policy.
 ![](https://main.qcloudimg.com/raw/ae2fb3be44f2f56ab64a257f505b2b4e.png)
4. For details of routing conflicts, see [Use Limits](https://intl.cloud.tencent.com/document/product/1003/30052#.E8.B7.AF.E7.94.B1.E9.99.90.E5.88.B6). To enable a conflicting route, see [Enabling a Route](https://intl.cloud.tencent.com/document/product/1003/30069).

## Step 4: Setting Cross-region Bandwidth Cap (Optional)

1. In the CCN list, click the CCN ID for which to set the bandwidth.
2. In the details page, click the **Monitoring** tab to view the metrics of the CCN.
3. Select the region for which to set the outbound bandwidth cap.
4. Set the outbound bandwidth cap for each region (1 Gbps by default).
 ![](https://main.qcloudimg.com/raw/e92d2cef0bdf5366054f7fd71415f24a.png)

>Communications between CCN instances incur fees, for pricing details, see [Pricing](https://intl.cloud.tencent.com/document/product/1003/30053).

