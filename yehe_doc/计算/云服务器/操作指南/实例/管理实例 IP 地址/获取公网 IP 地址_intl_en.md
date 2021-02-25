## Scenario
This document describes how to obtain the public IP address through console, API, or Instance metadata.


## Directions

### Obtaining the public IP address on the console
1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/).
2. On the instance management page, move the mouse to the primary IP column, and <img src = "https://main.qcloudimg.com/raw/6603ab4f907562addb1c01596c6296cd.png" style = "margin: 0;"> </ img> appears, as shown below:
![](https://main.qcloudimg.com/raw/952664b0a70077ba49a031b98a57c782.png)
3. Click <img src="https://main.qcloudimg.com/raw/6603ab4f907562addb1c01596c6296cd.png" style="margin: 0;"> to copy the IP address.	
>! The public IP address is mapped to the private IP address through NAT. If you view the network interface attributes from within the instance (for example by using commands such as `ifconfig (Linux)` or `ipconfig (Windows)`), the public IP address is not displayed. To obtain the public IP from within the instance, please see [Obtaining a Public IP Address of the Instance Using Instance Metadata](#jump).
>

### Obtaining the public IP address using API
Please see [DescribeInstances](https://intl.cloud.tencent.com/document/product/213/33258).

<span id = "jump">  </span>
### Obtaining the public IP address using instance metadata
1. Log in to the CVM instance.
For more information, please see [Log in to Linux Instance](https://intl.cloud.tencent.com/document/product/213/5436) and [Log in to Windows Instance](https://intl.cloud.tencent.com/document/product/213/5435).
2. To obtain the public IP address, you can access the metadata by using the cURL tool or an HTTP GET request.
```
curl http://metadata.tencentyun.com/meta-data/public-ipv4
```
If the returned value is in the following structure, you can view the public IP address:
![](https://main.qcloudimg.com/raw/03f603e433b7a5da09e33a8b09d731b4.png)
For more information, see [Instance Metadata](http://intl.cloud.tencent.com/document/product/213/4934).
