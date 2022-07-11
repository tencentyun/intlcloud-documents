## Overview
This document describes how to obtain the private IP address of the instance and configure the private DNS.

## Directions
### Obtaining the private IP address of an instance
<dx-tabs>
::: Obtain in console
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/).
2. On the instance management page, proceed according to the actually used view mode:
   - **List view**: select the target instance, move the cursor to the primary IP column, and click <img src="https://main.qcloudimg.com/raw/6603ab4f907562addb1c01596c6296cd.png" style="margin: -3px 0px;"> to copy the private IP as shown below:
   ![](https://qcloudimg.tencent-cloud.cn/raw/14720408f77509b0dced407f75adbd21.png)
 - **Tab view**: on the instance page, click <img src="https://main.qcloudimg.com/raw/6603ab4f907562addb1c01596c6296cd.png" style="margin: -3px 0px;"> after the private network address in "IP Address" to copy the private IP as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/3a251c153caddfb6cf62bb6e6e6ff2cd.png)

:::
::: Obtain via API
See [DescribeInstances](https://intl.cloud.tencent.com/zh/document/product/213/33258).
:::
::: Obtain via instance metadata
1. Log in to your CVM.
2. Access the instance metadata by using the cURL tool or an HTTP GET request.
<dx-alert infotype="explain" title="">
The following operations use the cURL tool as an example.
</dx-alert>
Execute the following command to obtain the private IP.
```
curl http://metadata.tencentyun.com/meta-data/local-ipv4
``` The returned information is the private IP address, as shown below:
![](//mc.qcloudimg.com/static/img/14a13eccebc7eee6f83bc026adb30902/image.png)
For more information about instance metadata, see [Querying Instance Metadata](https://intl.cloud.tencent.com/zh/document/product/213/4934).
:::
</dx-tabs>

### Configuring private network DNS 
When a network resolution error occurs, you can manually configure the private network DNS based on your CVM operating system.
<dx-tabs>
::: Linux
1. Log into the Linux CVM.
2. Execute the following command to open the `/etc/grub.conf` file.
```
vi /etc/resolv.conf
```
3. Press **i** to switch to the edit mode, and modify the DNS IP according to the corresponding region in the [Private Network DNS](https://intl.cloud.tencent.com/zh/document/product/213/5225?from_cn_redirect=1#.E5.86.85.E7.BD.91-dns) list.
For example, change the private network DNS IP to an private network DNS server in the Beijing region.
```
nameserver 10.53.216.182
nameserver 10.53.216.198
options timeout:1 rotate
```
4. Press **Esc**, enter **:wq**, save the file and return.
:::
::: Windows
1. Log in to the Windows CVM.
2. On the operating system UI, open **Control Panel** > **Network and Sharing Center** > **Change adapter settings**.
3. Right-click **Ethernet** and select **Properties** to open the "Ethernet Properties" window.
4. In the "Ethernet Properties" window, double-click **Internet Protocol Version 4 (TCP/IPv4)** as shown below:
![](https://main.qcloudimg.com/raw/1eef10b5919ba4db272fa0fc21fb1702.png)
5. Select **Use the following DNS server addresses** and modify the DNS IP according to the corresponding region in the [Private Network DNS](https://intl.cloud.tencent.com/zh/document/product/213/5225?from_cn_redirect=1#.E5.86.85.E7.BD.91-dns) list.
![](https://main.qcloudimg.com/raw/1eef10b5919ba4db272fa0fc21fb1702.png)
6. Click **OK**.
:::
</dx-tabs>
