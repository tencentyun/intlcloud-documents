## Error Description
VPCs or subnets cannot be deleted.

## Common Causes
+ VPC: A VPC can only be deleted when there is no resource associated other than empty subnets (IPs in the subnet are not used), routing tables, and network ACLs.
+ Subnet: A subnet can only be deleted when it’s not associated with any resource.
>? Resources that can be associated with the subnet include CVM, private network CLB, ENI, HAVIP, SCF, TKE, and TencentDB (for MySQL, Redis, TDSQL, etc.).

According to the rules above, VPCs and subnets cannot be deleted in the following cases:
+ There are cloud resources that have not been completely deleted. For example, after a database is terminated, it is in **isolated** status, and the database resources in this status actually are not completely released and continue to use the IP resources of the VPC. Therefore, the VPC or subnet cannot be deleted immediately.
+ Some resources can not be deleted in the VPC console.


## Troubleshooting Procedure
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **Delete** on the right of the VPC to be deleted, and check the associated resources.
>? Note that public network CLB instances don’t use VPC resources.
>
<img  src="" width="70%">   
3. Click the **VPC ID** to enter the details page, click the corresponding cloud resource to enter its details page, and release it.
    + If the direction to a resource fails, search for the corresponding product in the Tencent Cloud console, go to the resource's console, search for the resource under the VPC ID, and release it.
    +  A TencentDB instance is put into the **Isolated** status for a certain period after being terminated, during which the resources are not actually released. You need to click **Eliminate Now** or wait until the instance is automatically eliminated before you can delete the VPC or subnet.
   <dx-alert infotype="explain" title="">
+ The **Eliminate Now** operation in TencentDB is async. There may be a delay in the repossession of some resources, so the VPC cannot be deleted immediately. In this case, wait a while.
+ For more information, see [Terminating Instances](https://intl.cloud.tencent.com/document/product/213/4930) (for CVM), [Deleting CLB Instances](https://intl.cloud.tencent.com/document/product/214/15369), [Deleting an ENI](https://intl.cloud.tencent.com/document/product/576/18536), [Deleting a Peering Connection](https://intl.cloud.tencent.com/document/product/553/18848), [Deleting NAT Gateway](https://intl.cloud.tencent.com/document/product/1015/30243), [Deleting a VPN Gateway](https://intl.cloud.tencent.com/document/product/1037/41582), [Deleting Direct Connect Gateway](https://intl.cloud.tencent.com/document/product/216/19258), [Delete Flow Logs](https://intl.cloud.tencent.com/document/product/682/18968), [Network Probe](https://intl.cloud.tencent.com/document/product/215/35522), [Releasing HAVIPs](https://intl.cloud.tencent.com/document/product/215/40082), [Terminating Instance](https://intl.cloud.tencent.com/document/product/239/31937) (for TencentDB for Redis), and [Terminating Instance](https://intl.cloud.tencent.com/document/product/236/31895) (for TencentDB for MySQL).
</dx-alert>
4. After the resources are completely released, [delete the VPC](https://intl.cloud.tencent.com/document/product/215/40073) and [subnet](https://intl.cloud.tencent.com/document/product/215/40077) again.

   + If the problem persists, [contact us](https://intl.cloud.tencent.com/contact-sales) for assistance.
