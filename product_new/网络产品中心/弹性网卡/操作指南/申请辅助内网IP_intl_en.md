To deploy multiple IP addresses for a single ENI, you can request secondary private IP addresses for the ENI as follows:
1. Log in to [Virtual Private Cloud Console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Choose **IP and ENI** > **ENI** in the left sidebar to go to the ENI list page.
![](https://main.qcloudimg.com/raw/4075af8d7e9655ab5306e5152e1a79ce.png)
3. Click the instance ID for which secondary private IP addresses need to be requested to go to the details page.
4. Click the **IPv4 Address Management** tab to view bound private IP addresses and EIPs.
![](https://main.qcloudimg.com/raw/c360781a44e6a7f976c5fd3bf0b87bd0.png)
5. Click **Assign Private IP**. In the dialog box that appears, select **Automatic Assignment**, or select **Enter Manually** and manually enter the private IP address to be assigned.
> If you select **Enter Manually**, make sure that the entered private IP address is within the IP range of the subnet and is not a reserved IP address of the system.
> For example, if the IP range of the subnet is `10.0.0.0/24`, the entered private IP address should be within `10.0.0.2 - 10.0.0.254`.
>
![](https://main.qcloudimg.com/raw/ca59f63d94bf1d6694e69373b35fce9f.png)
