## Connection Process
![Getting Started](https://mc.qcloudimg.com/static/img/8fbd4b6fe3c5694b4d664b31d590fc4a/image.png)
### Creating Anycast EIP
1. Log in to [EIP Console](https://console.cloud.tencent.com/cvm/eip) and click **Apply**.
![](https://main.qcloudimg.com/raw/54feee4003bbc2eb4df94c8bf24f3c52.png)
2. Select the region, bandwidth cap, quantity according to your actual needs; select **Accelerated IP** according to the IP address type. Click **OK** to create an Anycast EIP.

### Binding Backend Resources
Log in to [EIP Console](https://console.cloud.tencent.com/cvm/eip) and select **More**>**Bind** to bind specified resources – we take CVM as an example in this document.
![](https://main.qcloudimg.com/raw/3bd6a79550f47da5de715eba6f620e06.png)

### Connecting to the Internet Using Accelerated EIP
After logging in to the bound backend resource, you can connect to the internet through the accelerated EIP and use AIA. Since the CVM in this document is bound, you can use AIA after logging in to the CVM.

## Other Common Operations
### Configuring Anycast EIP
#### Adjusting Bandwidth
Log in to the [EIP Console](https://console.cloud.tencent.com/cvm/eip), select the desired EIP from the EIP list, and then click **Adjust Bandwidth**.
![](https://main.qcloudimg.com/raw/2d0cc12a2086c5a3d31be0a09a29fe2e.png)