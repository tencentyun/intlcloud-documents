This document describes how to obtain the private IP address of the instance and configure the private DNS.

## Obtaining the private IP address of an instance
### Obtaining the private IP address on the console
1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/).
2. On the instance management page, select the instance and move the mouse to the **Primary IP** column to view its private IP, and click <img src = "https://main.qcloudimg.com/raw/6603ab4f907562addb1c01596c6296cd.png" style = "margin: 0;"> to copy the private IP, as shown below:
![](https://main.qcloudimg.com/raw/f4849355a4890861e2d07b35de1099a4.png)

### Obtaining the private IP address using API
Please see [DescribeInstances API](https://intl.cloud.tencent.com/document/product/213/33258).

### Obtaining the private IP address using instance metadata

1. Log in to the CVM.
2. Access the instance metadata by using the cURL tool or an HTTP GET request.
> The following operations use the cURL tool as an example.
>
Execute the following command to obtain the private IP.
```
curl http://metadata.tencentyun.com/meta-data/local-ipv4
```
The returned information is the private IP address, as shown below:
![](https://mc.qcloudimg.com/static/img/14a13eccebc7eee6f83bc026adb30902/image.png)

For more information about instance metadata, see [Instance Metadata](http://intl.cloud.tencent.com/document/product/213/4934).

## Configuring private network DNS 
When a network resolution error occurs, you can manually configure the private network DNS based on your CVM operating system.

### For Linux operating system

1. Log into the Linux CVM.
2. Execute the following command to open the `/etc/resolv.conf` file.
```
vi /etc/resolv.conf
```
3. Press **i** to switch to the edit mode, and modify the DNS IP according to the corresponding region in the [Private Network DNS](https://intl.cloud.tencent.com/document/product/213/5225) list.
For example, to change the private network DNS IP to an private network DNS server in the Beijing region.
```
nameserver 10.53.216.182
nameserver 10.53.216.198
options timeout:1 rotate
```
4. Press **Esc**, enter **:wq**, save the file and return.

### For Windows operating system

1. Log in to the Windows CVM.
2. On the operating system interface, open **Control Panel** > **Network and Sharing Center** > **Change adapter settings**.
3. Right-click the **Ethernet** and select **Properties** to open the “Ethernet Properties” window.
4. In the “Ethernet Properties” window, double-click **IP version 4 (TCP/IPv4)**, as shown below:
![](https://main.qcloudimg.com/raw/1eef10b5919ba4db272fa0fc21fb1702.png)
5. Select [Use the following DNS server address] and modify the DNS IP according to the corresponding region in the [Private Network DNS](https://intl.cloud.tencent.com/document/product/213/5225) list.

6. Click **OK**.
