This topic describes how to troubleshoot the CWPP agent running on Linux, including how to troubleshoot the failed startup of CWPP agent processes and network failures.
## Failed Startup of CWPP Agent Processes
1. Enter the command `ps -ef|grep YD` to check whether the CWPP processes exist.
	- Normally, CWPP has two processes as shown below:
![](https://main.qcloudimg.com/raw/80b75da06e95eaa1704035a0c1c5370e.png)
	- If the processes do not exist, possible reasons include the following:
	 - The CWPP agent is not installed on the server or has been uninstalled from the server. Please install it by following the steps described in [Getting Started](https://intl.cloud.tencent.com/document/product/296/12236)
	 - The agent has a conflict or crash, which leads to the failed startup of processes.
2. If CWPP agent has been installed on the server, troubleshoot the problem using the following method:
 - View the agent log stored in `/usr/local/qcloud/YunJing/log`.
 - Run the command `sh /usr/local/qcloud/YunJing/startYD.sh` to start CWPP.

## Network Failures
If the processes exist, but CWPP is offline, the issue is caused by network disconnection in most cases. Troubleshoot the issue by following the steps below:    
1. If you are unable to access the CWPP security domain, try changing the DNS. Run the following command line to check whether the CWPP security domain is accessible: 
	- VPC or CPM environment: telnet s.yd.tencentyun.com 5574.
	**Normally**, the returned result is as shown below:
![](https://main.qcloudimg.com/raw/50e39ceadcb275a72738b235e9637b4c.png)
**If it is inaccessible**：
		a. Change the field `dns nameserver`: `vim /etc/resolv.conf`
		`nameserver 183.60.83.19`
		`nameserver 183.60.82.98`
		b. Then run `telnet s.yd.tencentyun.com 5574` again to check whether you can connect to it.
		![](https://main.qcloudimg.com/raw/1ca906db209a6ddacaad46146a7355b8.png)
		c. If it can be connected, wait for a few minutes (the time length depends on the network conditions), and then you will see that the server is online again.
	- Basic network environment (non-VPC servers): `telnet s.yd.qcloud.com 5574`.
	**Normally**, the returned result is as shown below:
	![](https://main.qcloudimg.com/raw/93a2f6f05867b88aa41e753e4c4e83c0.png)
		**If it is inaccessible**：
		a. Change the field `dns nameserver`: `vim /etc/resolv.conf`. Comment the original field `nameserver` first, and then add a new `nameserver` field.
		b. Then run `telnet s.yd.qcloud.com 5574` again to check whether you can connect to it.
		c. If it can be connected, wait for a few minutes (the time length depends on the network conditions), and then you will see that the server is online again.
2. Make sure your firewall policies allow the TCP ports 5574, 8080, 80, and 9080.
3. If the CWPP processes exist and the offline state of the CWPP agent is not caused by network issues, package the agent logs (log path: `/usr/local/qcloud/YunJing/log`) and [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for feedback.