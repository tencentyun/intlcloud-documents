This document describes how to create a TencentDB for Tendis instance in the console.

## Prerequisites
You have registered a Tencent Cloud account and completed identity verification.
- To register a Tencent Cloud account:
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://intl.cloud.tencent.com/register" target="_blank"  style="color: white; font-size:16px;" hotrep="document.guide.3128.btn1">Click here to sign up for a Tencent Cloud account</a></div>
- To verify your identity (to purchase TencentDB for Tendis instances in the Chinese mainland, please verify your identity first):
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/developer" target="_blank"  style="color: white; font-size:16px;"  hotrep="document.guide.3128.btn2">Click here to verify your identity</a></div>

## Directions
1. Log in and go to the [Tendis purchase page](https://buy.cloud.tencent.com/tendis), select configuration items based on your actual needs, confirm that everything is correct, and click **Buy Now**.
 - **Billing Mode**: pay-as-you-go billing is supported.
    - If the request volume of your business fluctuates greatly and instantaneously, we recommend you choose pay-as-you-go billing.
 - **Region** and **Availability Zone**: select the region and availability zone which you want your TencentDB for Tendis instance to be deployed in. We recommend that you use the same region as the CVM instance to be connected to. Tencent Cloud products in different regions cannot communicate with each other over the private network. The region cannot be modified after purchase.
 - **Instance Edition**: Storage Edition and Hybrid Storage Edition are supported.
 - **Compatible Version**: Hybrid Storage Edition is compatible with Redis v4.0.
 - **Architecture Version**: Hybrid Storage Edition supports cluster architecture; Storage Edition supports standard architecture.
 - **Network**: select the network where the TencentDB for Tendis instance resides, which is "Default-VPC (default)" by default. We recommend that you select the same VPC in the same region as the CVM instance to be connected to. Otherwise, the Tendis instance cannot connect to the CVM instance over the private network.
 - **Security Group**: for more information on security group creation and management, please see [Configuring Security Groups](https://intl.cloud.tencent.com/document/product/1083/39345).
 - **Specify Project**: select a project to which the TencentDB instance belongs. The default project is used.
 - **Quantity**: you can purchase up to 10 pay-as-you-go instances in each AZ.
2. You will be returned to the instance list after you purchase the instance. The instance will be in the **Delivering** status. You can use the instance after around 3-5 minutes when its status changes to **Running**.


## Subsequent Operations
- Use a CVM instance to directly access the private IP of the TencentDB instance. For more information, please see [Connecting to Tendis Instances](https://intl.cloud.tencent.com/document/product/1083/39268).
- Use a CVM instance with a public IP for port forwarding to connect to the TencentDB instance over the public network. For more information, please see [iptables Forwarding](https://intl.cloud.tencent.com/document/product/1083/39269).
