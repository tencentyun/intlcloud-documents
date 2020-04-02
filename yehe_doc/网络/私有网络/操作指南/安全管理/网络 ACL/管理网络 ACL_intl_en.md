## Creating Network ACLs
1. Log in to [VPC Console](https://console.cloud.tencent.com/vpc).
2. Click **Security** > **Network ACL** in the left sidebar to go to the management page.
3. Select the target region and VPC at the top of the list and click **+Create**.
4. In the pop-up box, enter a name for the ACL, select the belonging VPC, and click **OK**.
![](https://main.qcloudimg.com/raw/3e5444cc57b2da457c2cd9db221dd1d3.png)
5. On the list page, click the ID of the ACL to go to the details page, where you can add ACL rules and associated subnets.

## Adding Network ACL Rules
1. Log in to [VPC Console](https://console.cloud.tencent.com/vpc).
2. Click **Security** > **Network ACL** in the left sidebar to go to the management page.
3. In the list, find the network ACL to be modified, and click its ID to go to the details page.
4. To add an outbound or inbound rule, click **Outbound Rules** or **Inbound Rules** and choose **Edit** > **New Line**. Then, select the protocol type, enter the port and source IP address, and select the policy.
 - Protocol type: select the protocol types to be allowed or rejected by the ACL rule, such as TCP and UDP.
 - Port: indicates the source port of the traffic. It can be a single port or port range, for example port 80 or ports 90–100.
 - Source IP: indicates the source IP address or source IP address range of the traffic. It can be an IP address or CIDR block, for example, `10.20.3.0` or `10.0.0.2/24`.
 - Policy: allow or reject.
![](https://main.qcloudimg.com/raw/d6d87cc117b15f5125d7f7fbb327f845.png)
5. Click **Save**.

## Deleting Network ACL Rules
1. Log in to [VPC Console](https://console.cloud.tencent.com/vpc).
2. Click **Security** > **Network ACL** in the left sidebar to go to the management page.
3. In the list, find the network ACL in which an ACL rule will be deleted, and click its ID to go to the **Basic Information** page.
4. Click the **Inbound Rules** tab or the **Outbound Rules** tab to go to the **Rule List** page.
5. Click **Edit**. The steps for deleting inbound rules are the same as those for deleting outbound rules. Here, the deletion of outbound rules is used as an example.
![](https://main.qcloudimg.com/raw/2d3a16b59a2566a2bfd6226086b3528b.png)
6. In the list, locate the row of the rule to be deleted. Then, click **Delete** in the operation column.
> This ACL rule is now grayed out. If the deletion is a misoperation, you can click **Recover the deleted rule** in the operation column to restore the rule.
>
![](https://main.qcloudimg.com/raw/57389cf8420513b893c5f55747826247.png)
7. Click **Save** to save the change.
> The deletion or restoration of the ACL rule takes effect only after you save it.

## Associating a Network ACL with a Subnet
1. Log in to [VPC Console](https://console.cloud.tencent.com/vpc).
2. Click **Security** > **Network ACL** in the left sidebar to go to the management page.
3. In the list, find the network ACL to be associated, and click its ID to go to the details page.
4. On the **Basic Information** page, click **Add Association** in the **Associated Subnets** section.
![](https://main.qcloudimg.com/raw/60374f034ac84bc088b42f1b2811af93.png)
5. Choose the subnet to be associated from the pop-up box, and then click **OK** to associate it.
![2](https://main.qcloudimg.com/raw/dd1c974c4938aa5bfd13ebbba2fa3274.png)

## Disassociating a Network ACL from a Subnet
1. Log in to [VPC Console](https://console.cloud.tencent.com/vpc).
2. Click **Security** > **Network ACL** in the left sidebar to go to the management page.
3. In the list, find the network ACL to be disassociated, and click its ID to go to the details page.
4. Disassociate the ACL from subnets in one of the following ways:
 - Method 1: locate the subnet to be disassociated in the **Associated Subnets** section of the **Basic Information** page, and then click **Unbind**.
![1](https://main.qcloudimg.com/raw/f5049453bb9838e03e093461232e5c82.png)
 - Method 2: In the **Associated Subnets** section of the **Basic Information** page, select the check boxes of the subnets to be disassociated and click **Batch Unbind**.
![2](https://main.qcloudimg.com/raw/e2953af15a89f4476e033e08e67009e5.png)
4. Click **OK** in the pop-up window.
![3](https://main.qcloudimg.com/raw/e44731b65300f164200946b10b2d8be6.png)

## Deleting Network ACLs
1. Log in to [VPC Console](https://console.cloud.tencent.com/vpc).
2. Click **Security** > **Network ACL** in the left sidebar to go to the management page.
3. Select the target region and VPC.
4. In the list, find the network ACL that you want to delete, and click its ID to go to the details page.
5. Click **Delete** and confirm the operation. Then, this network ACL and all its rules are deleted.
> If **Delete** is grayed out, such as for the network ACL named `testEg` in the following figure, it indicates that the network ACL is associated with a subnet. In this case, you must disassociate it from the subnet before you can complete the deletion.
>
![](https://main.qcloudimg.com/raw/3d6113a44321ce73e35f99efc246bfb4.png)

