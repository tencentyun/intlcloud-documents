## Connection Process
![Getting Started](https://main.qcloudimg.com/raw/b5199abb5f1d95de1fc10fa69ca66e6d.png)
### Creating Anycast EIP
1. Log in to [EIP Console](https://console.cloud.tencent.com/cvm/eip) and click **Apply**.
![](https://main.qcloudimg.com/raw/76b9964f2ed4457b10c6682296bac9d0.png)
2. Select the region, bandwidth cap, quantity according to your actual needs. For IP address type, select **Accelerated IP**. Click **OK** to create an Anycast EIP.

### Binding Backend Resources
Log in to [EIP Console](https://console.cloud.tencent.com/cvm/eip) and select **More**>**Bind** to bind specified resources. CVM is taken as an example in this document.
![](https://main.qcloudimg.com/raw/7e26cf3d0b27e5acae7d927140e7752d.png)

### Connecting to the Internet Using Accelerated EIP
After logging in to the bound backend resource, you can connect to the internet through the accelerated EIP and use AIA. Since the CVM in this document is bound, you can use AIA after logging in to the CVM.

## Other Common Operations
### Configuring Anycast EIP
#### Adjusting Bandwidth
Log in to the [EIP Console](https://console.cloud.tencent.com/cvm/eip), select the desired EIP from the EIP list, and then click **Adjust Bandwidth**.
![](https://main.qcloudimg.com/raw/624171b8a49f4e4091bac54a7b74ef28.png)
