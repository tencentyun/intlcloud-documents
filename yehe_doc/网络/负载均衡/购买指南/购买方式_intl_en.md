Tencent Cloud allows you to purchase CLB instances either from the console or via API. This document describes these two purchaseing methods in detail.

## Purchasing from Tencent Cloud Console
You can purchase CLB instances on the [Tencent Cloud Console](https://buy.cloud.tencent.com/lb).
### Bill-by-CVM accounts
Private network CLB is free of charge. Public network CLB charges instance fees on an hourly basis, and the billing mode is pay-as-you-go. You can purchase public network on [CVM](https://intl.cloud.tencent.com/document/product/213/495). For more information on the network billing modes, see [Public Network Billing](https://intl.cloud.tencent.com/document/product/213/10578).
To purchase a CLB instance from the console, perform the following:

1. Log in to the Tencent Cloud Console and go to the [CLB purchase page](https://buy.cloud.tencent.com/lb).
2. In the **Instance type**, select "Cloud Load Balancer".
3. Select attributes as needed, including network and project. Go to [CLB Attributes selection](https://intl.cloud.tencent.com/document/product/214/13629) to view attributes details.
4. Confirm and pay for the selected CLB instance.
5. CLB service is activated once the payment completes. You can now configure and use the CLB instance.
![](https://main.qcloudimg.com/raw/33dfce7ca7a0bbde210346a313a42d8e.png)

### Bill-by-IP accounts
Private network CLB is free of charge. Public network CLB charges instance fees and public network fees on a pay-as-you-go basis. The pay-as-you-go public network supports three billing options: bill-by-bandwidth, bill-by-traffic, and bandwidth package.
To purchase a CLB instance from the console, perform the following:
1. Log in to the Tencent Cloud Console and go to the [CLB purchase page](https://buy.cloud.tencent.com/lb).
2. In the **Instance type**, select "Cloud Load Balancer".
3. Select attributes as needed, including network, network billing mode, and project. Go to [Product Attribute selection](https://intl.cloud.tencent.com/document/product/214/13629) to view attributes details.
4. Confirm and pay for the selected CLB instance.
5. CLB service is activated once the payment completes. You can now configure and use the CLB instance.
![](https://main.qcloudimg.com/raw/315549c93a7552d2b97f83e9b47602d4.png)

## Purchasing via API
To purchase CLB via API, you can create a CLB instance referring [CreateLoadBalancer](https://intl.cloud.tencent.com/document/product/214/33841).

## Subsequent Steps
- To configure a TCP listener on the CLB instance, see [Configuring a TCP Listener](https://intl.cloud.tencent.com/document/product/214/32517).
- To configure a UDP listener on the CLB instance, see [Configuring a UDP Listener](https://intl.cloud.tencent.com/document/product/214/32518).
- To configure a TCP SSL listener on the CLB instance, see [Configuring a TCP SSL Listener](https://intl.cloud.tencent.com/document/product/214/32519).
- To configure an HTTP listener on the CLB instance, see [Configuring an HTTP Listener](https://intl.cloud.tencent.com/document/product/214/32515).
- To configure an HTTPS listener on the CLB instance, see [Configuring an HTTPS Listener](https://intl.cloud.tencent.com/document/product/214/32516).
