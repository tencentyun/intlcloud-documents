You can purchase CLB instances on Tencent Cloud official purchase page or via API. 

## Purchasing on the official purchase page
You can purchase a CLB instance on the [Tencent Cloud official website](https://buy.cloud.tencent.com/lb). There are two types of Tencent Cloud accounts, namely the bill-by-IP accounts and bill-by-CVM accounts. All accounts created after June 17, 2020 00:00:00 (Beijing time) are bill-by-IP accounts. If your account is created before that time, you can check your account type in the console as instructed in [Checking Account Type](https://intl.cloud.tencent.com/document/product/684/15246).
### Bill-by-CVM accounts
Private network CLB instances are free of charge. Public network CLB instances are billed on an hourly pay-as-you-go basis. You can purchase public network on [CVM](https://intl.cloud.tencent.com/document/product/213/495). For more information on the network billing modes, please see [Public Network Billing](https://intl.cloud.tencent.com/document/product/213/10578).
To purchase a CLB instance on the official website:
1. Log in to the Tencent Cloud console and go to the [CLB purchase page](https://buy.cloud.tencent.com/lb).
2. For the instance type, **Cloud Load Balancer** is recommended.
3. Select attributes as needed, including the network type and project. For attribute details, please see [Product Attribute Selection](https://intl.cloud.tencent.com/document/product/214/13629).
![](https://main.qcloudimg.com/raw/33dfce7ca7sa0bbde210346a313a42d8e.png)
4. Confirm and pay for the selected CLB instance.
5. CLB service will be activated once the payment completes. You can now configure and use the CLB instance.

### Bill-by-IP accounts
Private network CLB instances are free of charge. Public network CLB instances charge instance fees and public network fees on a monthly subscription or pay-as-you-go basis. The monthly-subscribed public network can only be billed by bandwidth, while the pay-as-you-go public network can be billed by bandwidth, traffic, and bandwidth package.
To purchase a CLB instance on the official website, perform the following:
1. Log in to the Tencent Cloud console and go to the [CLB purchase page](https://buy.cloud.tencent.com/lb).
2. For the instance type, **Cloud Load Balancer** is recommended.
3. Select attributes as needed, including the network type, network billing mode, and project. For attribute details, please see [Product Attribute Selection](https://intl.cloud.tencent.com/document/product/214/13629).
>?Currently, the static single-line IP is supported only in Guangzhou, Shanghai, Nanjing, Jinan, Hangzhou, Fuzhou, Beijing, Shijiazhuang, Wuhan, Changsha, Chengdu, and Chongqing. For its support in other districts, please see the console. The feature is currently in beta, if you want to try it out, please submit an application. Once you are accepted, you can select an ISP (China Mobile, China Unicom, or China Telecom) on the purchase page.
>
![](https://main.qcloudimg.com/raw/f09271383a733a0c0281ebe324b6ff56.png)
4. Confirm and pay for the selected CLB instance.
5. CLB service will be activated once the payment completes. You can now configure and use the CLB instance.

## Purchasing a CLB instance via API
To purchase a CLB instance via API, please see [CreateLoadBalancer](https://intl.cloud.tencent.com/document/product/214/33841).

## Subsequent operations
- To configure a TCP listener on the CLB instance, please see [Configuring a TCP Listener](https://intl.cloud.tencent.com/document/product/214/32517).
- To configure a UDP listener on the CLB instance, please see [Configuring a UDP Listener](https://intl.cloud.tencent.com/document/product/214/32518).
- To configure a TCP SSL listener on the CLB instance, please see [Configuring a TCP SSL Listener](https://intl.cloud.tencent.com/document/product/214/32519).
- To configure an HTTP listener on the CLB instance, please see [Configuring an HTTP Listener](https://intl.cloud.tencent.com/document/product/214/32515).
- To configure an HTTPS listener on the CLB instance, please see [Configuring an HTTPS Listener](https://intl.cloud.tencent.com/document/product/214/32516).
