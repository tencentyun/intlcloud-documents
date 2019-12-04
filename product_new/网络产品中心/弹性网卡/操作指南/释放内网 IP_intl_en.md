This document describes how to release secondary private IP addresses.
1. Log in to [Virtual Private Cloud Console](https://console.cloud.tencent.com/vpc).
2. Choose **IP and ENI** > **ENI** in the left sidebar to go to the ENI list page.
![](https://main.qcloudimg.com/raw/6eb5d412b00efe583a87dab70e2fc55a.png)
3. Click the target instance ID to go to the details page.
4. Click the **IPv4 Address Management** tab to view private IP addresses and EIPs that have been bound.
![](https://main.qcloudimg.com/raw/9e893f9aa79c69a6b83703477292a7ab.png)
5. Find the target private IP address, and click **Release** in the **Operation** column.
6. In the dialog box that appears, click **OK**.
![](https://main.qcloudimg.com/raw/51f72b65c4b535c752800ccf5d96a28b.png)
>
>- Only a secondary IP address can be released from an ENI. The primary IP address cannot be released.
>- After a private IP address is unbound, the associated EIP will be unbound automatically.
