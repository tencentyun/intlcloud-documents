Now, you need to configure the SSL VPN client certificate on the mobile client.

## Directions
1. [](id:step1)Download the SSL VPN client verification file assigned by Tencent Cloud. See [Downloading SSL VPN ‍Client Configuration](https://intl.cloud.tencent.com/document/product/1037/43914).
>? The download SSL VPN client certificate can only be used for one local client. 
>
2. ‍Download OpenVPN ‍and install it on the mobile device.
<dx-tabs>
‍::: Windows client
1. Download OpenVPN Connect from the official website and install it.
![](https://qcloudimg.tencent-cloud.cn/raw/c1fa844ae99696903f7b71cd054c5722.png)
2. Go to **Import Profile** > **FILE** to upload the SSL VPN client configuration file (.ovpn file) downloaded in [Step 1](#step1).
![](https://qcloudimg.tencent-cloud.cn/raw/9521a7f3dc592eeef9dc0081d85a7bd0.png)
:::
::: MAC client
1. Download OpenVPN Connect from the official website and install it.
![](https://qcloudimg.tencent-cloud.cn/raw/e0b037d45c2f34e181fe3219c7194f18.png)
2. Go to **Import Profile** > **FILE** to upload the SSL VPN client configuration file (.ovpn file) downloaded in [Step 1](#step1).
![](https://qcloudimg.tencent-cloud.cn/raw/4f9258654a0010aec4c48ba8f3af75fc.png)
:::
::: Linux client
1. Open the command line window.
2. Run the following command to install OpenVPN Connect.
 - CentOS distribution
```
yum install -y openvpn
```
 - Ubuntu distribution
```
sudo apt-get install openvpn
```
3. Unzip the SSL VPN client certificate from the package downloaded in [Step 1](#step1) and copy it to the `/etc/openvpn/conf/` directory.
Enter the `/etc/openvpn/conf/` directory and run the following command to establish a VPN connection.
```
openvpn --config /etc/openvpn/conf/SSLVpnClientConfiguration.ovpn --daemon

```
:::
</dx-tabs>
