## Preparations

CWP agent can be installed upon launch of CVM or CPM instance or later.
Log in to the [CWP Console](https://console.cloud.tencent.com/yunjing) and select **Asset Management** > **Server List** on the left sidebar to see whether CWP agent has been installed on the instance, as shown below:
![](https://main.qcloudimg.com/raw/76641a48eb933d23657fa3aeed902481.png)
- The server in the red box has enabled CWP Pro.
- The server in the blue box has enabled CWP Basic. You can click **Activate CWP Pro** to upgrade it.
- The server in the yellow box has not been installed with CWP. You can install CWP by following the instructions below:
  - [Windows-based CVM](#windows-based-cvm) 
  - [Linux-based CVM](#linux-based-cvm) 


## Intrusion Detection

After installing CWP, you can use the features such as trojan detection and killing, login audit, and password cracking detection, which are automatically started after CWP is installed. At this time, you can view server intrusion detection details in two ways as shown below:
- Log in to the [CWP Console](https://console.cloud.tencent.com/yunjing), select **Asset Management** > **Server List** on the left sidebar, and find the server you want to query. Click the IP address of the server and click **Intrusion Detection** to view its intrusion detection details.
- Log in to the [CWP Console](https://console.cloud.tencent.com/yunjing), click **Intrusion Detection** on the left sidebar, and click the feature you want to view. Then, you can view the intrusion detection details of all servers with CWP enabled.
- For more information on feature-related operations, please see:
	- [Trojan operation and handling](https://intl.cloud.tencent.com/document/product/296/13008)
	- [Login audit operation](https://intl.cloud.tencent.com/document/product/296/34229)

## Vulnerability Detection

After installing CWP and upgrade to the Pro edition, you can use the system component vulnerability detection, web component vulnerability detection, and security baseline detection features.
Log in to the [CWP Console](https://console.cloud.tencent.com/yunjing), click **Vulnerability Management** on the left sidebar, and click the feature you want to view. Then, you can view the vulnerability detection details of all servers with CWP enabled and repair the vulnerabilities as prompted.

## CWP Agent Installation
### Windows-based CVM  
#### Compatible versions
Currently, the following versions are supported:
- Windows Server 2012
- Windows Server 2008 R2
- Windows Server 2003 (limited support)
- Windows Server 2016

#### Download addresses
- Internet:
```
https://imgcache.qq.com/qcloud/csec/yunjing/static/ydeyes_win32.exe
```
- Basic network (non-VPC servers):
```
http://u.yd.qcloud.com/ydeyes_win32.exe
```
- VPC and CPM:
```
http://u.yd.tencentyun.com/ydeyes_win32.exe
```

#### Installation instructions
Verification of installation result on Windows: open Task Manager and check whether the YDService and YDLive processes are called, and if yes, the installation is successful.
![Windows processes](https://main.qcloudimg.com/raw/fe5aefe39b682cc05358e07b954bb44c.png)
#### FAQs
- Firewall interception
   We recommend allowing access addresses of the CWP backend server in the firewall policies:
   Domain names: `s.yd.qcloud.com; l.yd.qcloud.com; u.yd.qcloud.com`
   Ports: `5574`, `8080`, `80`, and `9080`
- DNS description
   If you do not want to use the default DNS, you need to forward all resolution requests of the root domains of `tencentyun.com` and `yd.qcloud.com` to the default DNS.

### Linux-based CVM
#### Compatible versions
Currently, the following versions are supported:
- RHEL: Versions 5, 6 and 7 (32/64-bit)
- CentOS: Versions 5, 6 and 7 (32/64-bit)
- Ubuntu: 9.10–14.4 (64-bit)

#### Download addresses
- Internet:
```
wget --no-check-certificate https://imgcache.qq.com/qcloud/csec/yunjing/static/yunjinginstall.sh && sh ./yunjinginstall.sh
```
- Basic network (non-VPC servers):
```
wget http://u.yd.qcloud.com/ydeyesinst_linux64.tar.gz && tar -zxvf ydeyesinst_linux64.tar.gz && sh self_cloud_install_linux64.sh
```
- VPC and CPM:
```
wget http://u.yd.tencentyun.com/ydeyesinst_linux64.tar.gz && tar -zxvf ydeyesinst_linux64.tar.gz && sh self_cloud_install_linux64.sh
```

#### Installation instructions

After executing installation commands, check whether the YDService and YDLive processes are called, and if yes, CWP agent is successfully installed. Run the following command to check:
```
ps -ef|grep YD
```
![](https://mc.qcloudimg.com/static/img/25c18ce3ed1673ca7d47425c28c3b8ef/image.png)
If the processes are not called, you can manually run the following command as the root user to start the program:
```
/usr/local/qcloud/YunJing/YDEyes/YDService
```

#### Uninstallation instructions
You can uninstall CWP agent in the console or OS, as shown below:
- **Uninstallation in the console**
	1. Log in to the [CWP Console](https://console.cloud.tencent.com/yunjing).
	2. In the server list, select the server from which you want to uninstall CWP agent.
		![](https://main.qcloudimg.com/raw/be64dbdb9e4ac97804fb7d2eb169269b.png)

- **Uninstallation in the OS**
	1. Windows
   Find and double-click the uninst.exe file in the following path to uninstall CWP agent:
   `C:\Program Files\QCloud\YunJing\uninst.exe`.
	2. Linux
   Run the following command to uninstall CWP: `/usr/local/qcloud/YunJing/uninst.sh`.

#### FAQs

- Firewall interception
   You are recommended to allow access addresses of the CWP backend server in the firewall policies:
   Domain names: `s.yd.qcloud.com; l.yd.qcloud.com; u.yd.qcloud.com`
   Ports: `5574`, `8080`, `80`, and `9080`
- DNS description
   If you do not want to use the default DNS, you need to forward all resolution requests of the root domains of `tencentyun.com` and `yd.qcloud.com` to the default DNS.

## Activating CWP Pro
You can activate the CWP Pro in the following two ways:
- On the Tencent Cloud website, enter the [CWP product page](https://intl.cloud.tencent.com/product/hs) and click **Purchase Now**. You will be redirected to the Tencent Cloud Console login page. After login, you can activate CWP Pro.
- Log in to the [Tencent Cloud Console](https://console.cloud.tencent.com/), click **Cloud Product** > **Endpoint Security** > **Cloud Workload Protection** to enter the CWP configuration page. Click **Security Overview** on the left sidebar and click **Upgrade to CWP Pro** in the bulletin board zone above to activate the Pro edition.
