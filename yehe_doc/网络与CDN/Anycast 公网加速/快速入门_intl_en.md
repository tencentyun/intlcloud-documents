## Connection Process
![Getting Started](https://main.qcloudimg.com/raw/b9848b8db42e252992cb4931c2e67999.png)
### Creating Anycast EIP
1. Log in to the [EIP Console](https://console.cloud.tencent.com/cvm/eip) and click **Apply**.
2. Select the region, bandwidth cap, and quantity according to your actual needs, select **Acceleration IP** as the IP address type, and click **OK** to create an Anycast EIP.

### Binding backend resource
Log in to the [EIP Console](https://console.cloud.tencent.com/cvm/eip) and select **More** > **Bind** to bind specified resources. This document uses CVM as an example.


### Connecting to the internet by using acceleration EIP
After logging in to the bound backend resource, you can connect to the internet through the acceleration EIP to use AIA. As a CVM instance is bound as an example in this document, you can use AIA after logging in to the instance.

## Other Common Operations
### Changing Anycast EIP configuration
#### Adjusting bandwidth
>?Only bill-by-EIP/CLB accounts can adjust the bandwidth in the EIP console. For bill-by-CVM accounts, please adjust the bandwidth in the corresponding [CVM instance](https://console.cloud.tencent.com/cvm/instance/index?rid=1) or [NAT gateway](https://console.cloud.tencent.com/vpc/nat?rid=1). If you are not sure of your account type, please see [Account Type](https://intl.cloud.tencent.com/document/product/214/36999).

1. Log in to the [EIP Console](https://console.cloud.tencent.com/cvm/eip).
2. In the EIP list, select the EIP you want to use, and click **Adjust Network**.
