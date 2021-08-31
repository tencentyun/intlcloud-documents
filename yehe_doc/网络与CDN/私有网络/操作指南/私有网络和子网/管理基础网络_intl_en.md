The classic network is a public network resource pool for all users on Tencent Cloud (as shown on the right side of the figure below). The private IP addresses of all CVMs are uniformly assigned by Tencent Cloud, and IP range division and IP addresses cannot be customized.
VPC refers to a logically isolated network space built by the user on Tencent Cloud (as shown on the left side of the figure below). In a VPC, you can customize IP ranges, IP addresses, and routing policies. Compared with the classic network, VPC is more suitable for scenarios in which network configurations need to be customized.
![](https://main.qcloudimg.com/raw/5fe7730ac2f302d960cf20443f976b6f.png)

## Precautions
1. Classic network resources are becoming increasingly sparse and cannot be expanded, so the classic network is no longer supported for newly registered accounts since June 13, 2017. This means that instances (such as cloud virtual machines and cloud load balancers) can no longer be created in the classic network, and only VPCs can be created.
2. You can query your account’s network attributes using the API DescribeAccountVpcAttributes.
3. If your service requires the use of a classic network, please [submit an application](https://intl.cloud.tencent.com/apply/p/qnm7krv9glo).
4. Classiclink only supports VPCs in the IP range of `10.0.0.0/16 - 10.47.0.0/16` (including subsets). (This limit does not apply to CVMs in classic networks.) If the IP range of your VPC is not within this range, then you cannot associate or interconnect with CVMs in a classic network.
5. One classic network CVM can be associated with only one VPC.
6. After the classic network is associated with a VPC, it only supports resource communication with the primary CIDR block of the VPC, not the secondary CIDR block.


## Switching a Classic Network CVM to a VPC
In order to facilitate your use of VPCs, Tencent Cloud allows you to switch one CVM or batch of CVMs from a classic network to a VPC. For more information, refer to [Switching to VPC](https://intl.cloud.tencent.com/document/product/213/20278).

## Associating Classic Network CVM with VPC
CVM “TomCVM” can communicate with VPC “TomVPC” using Classiclink. The step-by-step directions are as follows:
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Select the region and click the ID of the `TomVPC` to be interconnected with the classic network to go to the details page.
3. Click the **Classiclink** tab and then click **+Associate CVM**. 
4. In the pop-up window, select the CVM in the classic network to be associated with the VPC `TomCVM` and click **OK**.

## Viewing VPCs Interconnected with Classic Network CVMs
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Select the region and click the ID of the VPC to be interconnected with the classic network to go to the details page.
3. Click the **Classiclink** tab to view the list of classic network CVMs associated with the VPC.



## <span id="release" ></span>

## Unassociating a VPC and Classic Network CVM

1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Click the ID of the VPC to be interconnected with the classic network to go to the details page.
3. Click the **Classiclink** tab, select the CVM to be disassociated from the list of classic network CVMs, click **Disassociate** in the operation column, and confirm the operation.


