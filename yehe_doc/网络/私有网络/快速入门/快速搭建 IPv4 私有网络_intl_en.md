## Operation Scenarios
Taking the networks required in the deployment of a CVM with Internet access as an example, this document explains each step in detail, from creating a VPC and subnet, to purchasing a CVM, assigning a public IP address, and lastly using a security group to control the inbound and outbound traffic of the CVM.
![](https://main.qcloudimg.com/raw/82eefc24e8eeded09773ef7a5b6ab077.png)

## Prerequisites
1. Before using Tencent Cloud products, you need to [register a Tencent Cloud account](https://intl.cloud.tencent.com/register).
2. Confirm the [region and availability zone](https://intl.cloud.tencent.com/document/product/215/31786) in which the VPC is to be deployed based on your business requirements.
3. Understand the basic configurations of the two types of Tencent Cloud CVMs: [Getting Started with Linux CVMs](https://intl.cloud.tencent.com/document/product/213/2936) and [Getting Started with Windows CVMs](https://intl.cloud.tencent.com/document/product/213/2764).

## Steps
### Step 1: (Optional) Create a VPC and subnet.
You can create a custom VPC and subnet, or you can skip this step by choosing to have the system automatically create a default VPC and subnet when purchasing the CVM.
A VPC includes at least one subnet. When a VPC is created, the system will create an initial subnet, and cloud service resources can only be added in the subnet.
The features of the default VPC are the same as those of the custom VPC that you create.

1. Log in to [VPC Console](https://console.cloud.tencent.com/vpc).
2. After selecting the region of the VPC on the top bar, click **+Create**.
3. Enter the VPC information and initial subnet information, and click **Create**. If you need multiple subnets, see [Creating a Subnet](https://intl.cloud.tencent.com/document/product/215/31806#.E5.88.9B.E5.BB.BA.E5.AD.90.E7.BD.91).

>The CIDR blocks (IP ranges) of VPC instances and subnets cannot be modified once they are created. Therefore, complete [network planning](https://intl.cloud.tencent.com/document/product/215/31795) in advance.

### Step 2: purchase a CVM.
1. Log in to [CVM Console](https://console.cloud.tencent.com/cvm).
2. Click **Create** in the upper-left corner of the list page to go to the CVM purchase page.
3. For information on the configurations of CVMs, see [Custom Configuration for Linux CVMs](https://intl.cloud.tencent.com/document/product/213/10517) and [Custom Configuration for Windows CVMs](https://intl.cloud.tencent.com/document/product/213/10516).
4. Select a VPC and subnet. There are two selection methods:
- **Using custom VPC and subnet**
In **1. Select the region and model** in **Custom Configuration**, you can select the VPC and subnet created in Step 1 in the **Network** option, and the CVM will be created in the custom VPC and subnet.

- **Using default VPC and subnet**
In **1. Select the region and model** in **Custom Configuration**, you can select the default VPC (Default-VPC) and subnet (Default-subnet) in the **Network** option, and the CVM will be created in the default VPC and subnet.


>We recommend that you assign a free public IP address when purchasing a CVM. If no public IP address is assigned during the purchase, you can bind the CVM to an elastic public IP address in CVM Console.

### Step 3: configure a security group.
When purchasing a CVM, you can select the default security group (Default) of the system. This security group permits all traffic by default. You can set security group rules based on your needs.
1. Log in to [CVM Console](https://console.cloud.tencent.com/cvm).
2. Click **Security Group** in the left sidebar to go to the management page.
3. Find the default security group in the list and click **Modify Rules**.
4. Modify the inbound and outbound rules of the security group on this page.

For more information on configuring security group rules, see [Creating a Security Group](https://intl.cloud.tencent.com/document/product/215/35506) and [Security Group Use Cases](https://intl.cloud.tencent.com/document/product/215/35519).

### Step 4: configure a route table.
After finishing configuring the CVM and security group, you need to configure the route table associated with the subnet.
1. Log in to [VPC Console](https://console.cloud.tencent.com/vpc).
2. Click **Route Tables** in the left sidebar to go to the management page.
3. Find the default route table of the default VPC in the list and click its ID to go to the details page.
4. Click **+Add Routing Policy** in **Routing Policy**.
5. Enter your destination IP address range for accessing the Internet and select **CVM's Public IP** for the next-hop type. This indicates that when CVMs in the subnet that is bound with this route table access this IP address range, they will always use the CVM’s public IP address.

>You can purchase a NAT gateway to provide Internet access to CVMs without public IP addresses. For more information, see [NAT Gateways](https://intl.cloud.tencent.com/document/product/1015).
