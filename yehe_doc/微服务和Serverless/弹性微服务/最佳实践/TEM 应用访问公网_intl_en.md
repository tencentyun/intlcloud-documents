## Overview

Applications running on TEM usually need public network access, and also require allowlist access in scenarios such as mini programs. In these cases, the application should have a fixed public IP.

This document describes how to enable public network access of the applications deployed on TEM.

#### Solution
The applications are deployed in a TEM environment, which associates with your VPC. In other words, they are essentially deployed in your VPC. You can configure a NAT Gateway instance and associate it with an EIP for your VPC, allowing the applications in your VPC to access the public network.


#### Steps
<dx-steps>
- [Deploy the applications in TEM.](#step1)
- [Create a NAT Gateway.](#step2)
- [Configure the NAT Gateway in the VPC console.](#step3)
- [Verify whether the TEM applications can access the public network.](#step4)
- [(Optional) Query public network access IP addresses.](#step5)
</dx-steps>



## Directions

### Step 1: deploy the applications in TEM[](id:step1)

Configure the applications in the TEM console as instructed in [Creating Environment](https://intl.cloud.tencent.com/document/product/1094/40358) and [Creating and Deploying Application](https://intl.cloud.tencent.com/document/product/1094/40362).



### Step 2: create a NAT Gateway[](id:step2)

Log in to the [NAT Gateway](https://console.cloud.tencent.com/vpc/nat?rid=4) console, select the region where the TEM applications are deployed, and click **+New** to create a NAT Gateway instance.

<img src="https://main.qcloudimg.com/raw/c5d87bc70ca058f67bf93e99d68d47f5.png" width="600px">

- **Network**: select the VPC with which the environment of the TEM applications associates.
- **Elastic IP**: if there is no available elastic IP (EIP), click **Create Now** to purchase an EIP, and then return to the **Create NAT Gateway** page to select it.



### Step 3: configure the NAT Gateway in the VPC console[](id:step3)

1. Log in to the TEM console and access the [**Environment**](https://console.cloud.tencent.com/tem/env) page. Select the environment in which the TEM applications are deployed to enter its details page.
2. Click the VPC next to **Cluster Network** to enter the VPC details page.
<img src="https://main.qcloudimg.com/raw/6a240ee7d99c77aafba1a3b8340746d3.png" width="450px">
3. Select the **Route Table** module.
4. Click **Create** on the **Route Table** page to configure a route table.
      ![](https://main.qcloudimg.com/raw/8a61dab5ac424d7b3654c0f63dd6118e.png)
   - **Destination**: select the public IP address to be accessed. You can configure a CIDR block for this parameter. For example, if you enter `0.0.0.0/0`, all traffic will be forwarded to the NAT Gateway.
   - **Next hop type**: select **NAT Gateway**.
   - **Next hop**: select the NAT Gateway created in the **step 2**.

   For detailed directions, see [Creating Custom Route Tables](https://intl.cloud.tencent.com/document/product/215/35236).
5. On the **Route Table** page, locate the route table just created, and click **More** > **Associated Subnets** under the **Operation** column. In the pop-up window, select the subnet associated with the environment in which the TEM applications are deployed.
![](https://main.qcloudimg.com/raw/ad7581c40397a2880716995f87838c03.png)


### Step 4: verify whether the TEM applications can access the public network[](id:step4)

1. Log in to the TEM console and access the [**Application Management**](https://console.cloud.tencent.com/tem/application?rid=4) page. Click the **ID/Name** of the TEM applications to enter the instance list page.
2. Click **Webshell** under the **Operation**column of the target application.
      ![](https://main.qcloudimg.com/raw/1a82ce68a9638c84cf67589d20a92cc3.png)
3. Verify whether the application can access the public network.
	![](https://main.qcloudimg.com/raw/74eaf5884506d3880dcf0529df16ea15.png)



### Step 5: (optional) query public network access IP addresses[](id:step5)

1. Log in to the TEM console and access the [**Environment**](https://console.cloud.tencent.com/tem/env) page. Select the environment in which the TEM applications are deployed to enter its details page.
2. Click the VPC next to **Cluster Network** to enter the VPC details page.
<img src="https://main.qcloudimg.com/raw/e0505caec5440515b1fc7c65f4493a2e.png" width="450px">
3. Select the **NAT Gateway** model to go to the **NAT Gateway** page.
4. Click the **ID/Name** of the target NAT Gateway to access its details page. Select the **Bind Elastic IP** tab to view the IP addresses that can access the public network.


## Additional Fees

The [NAT Gateway](https://intl.cloud.tencent.com/product/nat) and EIP will be charged separately. For pricing details, see:

- [NAT Gateway Billing Overview](https://intl.cloud.tencent.com/document/product/1015/30248)
- [Elastic IP Billing](https://intl.cloud.tencent.com/document/product/213/17156)
