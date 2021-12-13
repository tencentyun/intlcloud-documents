This document describes how to create a TDSQL for MySQL instance in the console.

## Prerequisite
You have registered a Tencent Cloud account and completed identity verification.
- To register a Tencent Cloud account:
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://intl.cloud.tencent.com/register" target="_blank"  style="color: white; font-size:16px;" hotrep="document.guide.3128.btn1">Click here to sign up for a Tencent Cloud account</a></div>
- To verify your identity:
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/developer" target="_blank"  style="color: white; font-size:16px;"  hotrep="document.guide.3128.btn2">Click here to verify your identity</a></div>

## Directions
1. Log in to the [TDSQL for MySQL purchase page](https://console.cloud.tencent.com/tdsqld/tdmysql-buy), configure the following instance information, and click **Buy Now**.
 - **Billing Mode**: monthly subscription and pay-as-you-go billing are supported.
    - If your business has a stable long-term demand, we recommend you select monthly subscription.
    - If the request volume of your business fluctuates greatly and instantaneously, we recommend you choose pay-as-you-go billing.
 - **Region**: select the region that you want your TDSQL for MySQL instance to be deployed in. We recommend you use the same region as the CVM instance to be connected to. Tencent Cloud services in different regions cannot communicate with each other over the private network. The region cannot be modified after purchase.
 - **Network**: select the network where the TDSQL for MySQL instance resides. We recommend you select the same VPC in the same region as the CVM instance to be connected to; otherwise, the TencentDB for MySQL instance cannot connect to the CVM instance over the private network.
 - **Instance Version**: for more information, see [Instance Architecture](https://intl.cloud.tencent.com/document/product/1042/33319), [Selection of TDSQL Instance and Shard Configuration](https://intl.cloud.tencent.com/document/product/1042/33354), and [Pricing](https://intl.cloud.tencent.com/document/product/1042/35777).
2. After making the payment, return to the instance list, wait for the instance status to become **Uninitialized**, and initialize the instance.


## Subsequent Operations
You need to initialize the TDSQL for MySQL instance. For more information, see [Initializing Instances](https://intl.cloud.tencent.com/document/product/1042/33337).

