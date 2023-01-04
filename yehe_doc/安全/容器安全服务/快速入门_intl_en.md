## Prerequisites
### Installing the Agent 
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Asset Management** on the left sidebar.
2. On the **Asset Management** page, click **Total servers** to view the list of TCSS servers already installed.
>? If the TCSS Agent is not in the list, you need to install it as instructed in [Agent Installation Guide](https://www.tencentcloud.com/document/product/1163/50877#Agent).

<img src="https://qcloudimg.tencent-cloud.cn/raw/9a7f5015d55706a04d40c26328599c0a.png" style="zoom:80%;" />

### Activating the Pro Edition and enabling the value-added feature
After installing the Agent, check whether you want to activate the TCSS Pro Edition and enable the value-added feature.
 - If you have activated the Pro Edition and enabled the value-added feature, you can enjoy the comprehensive security protection provided by TCSS.
 - If you haven't activated the Pro Edition and enabled the value-added feature, you can [do so](https://buy.cloud.tencent.com/tcss) first, and then you can view available features in the console and enjoy the security protection provided by TCSS.

### Supported Linux versions
Currently, the following versions are supported:
- RHEL: Versions 6 and 7 (64-bit)
- CentOS: Versions 6 and 7 (64-bit)
- Ubuntu: Versions 9.10 to 18.04 (64-bit)
- Debian: Versions 6, 7, 8, and 9 (64-bit)

[](id:Agent)
## Agent Installation Guide
### Downloading and installing the Agent
In the Linux system, enter the following command to download and install the Agent:
>? You can select one of the following download addresses based on your network status.

- Classic network (non-VPC servers):
```
wget http://u.yd.qcloud.com/ydeyesinst_linux64.tar.gz && tar -zxvf ydeyesinst_linux64.tar.gz && sh self_cloud_install_linux64.sh
```
- VPC and CPM:
```
wget http://u.yd.tencentyun.com/ydeyesinst_linux64.tar.gz && tar -zxvf ydeyesinst_linux64.tar.gz && sh self_cloud_install_linux64.sh
```


### Checking whether the installation is successful
- After running the installation command, check whether the YDService and YDLive processes are called, and if so, the agent is installed successfully. Run the following command to check:
``` 
ps -ef|grep YD
```
 ![](https://main.qcloudimg.com/raw/f45b92e25896d713de329cbd0733e8b2.png)

- If the processes are not called, run the following command as the root user to start the programs:
```
/usr/local/qcloud/YunJing/YDEyes/YDService
```

### Uninstalling the TCSS Agent
In the Linux system, enter the following command to uninstall the agent:
```
/var/lib/qcloud/YunJing/uninst.sh 
```

## Troubleshooting
If you have questions or experience exceptions during use, see [FAQs](https://www.tencentcloud.com/document/product/1163/50940).
