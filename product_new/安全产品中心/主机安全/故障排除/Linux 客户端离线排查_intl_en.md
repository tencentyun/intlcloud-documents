## Agent Processes Are not Started
1. Run the following command to check whether the CWP processes exist: `ps -ef|grep YD`.
2. In normal state, CWP has two processes as shown below:
  ![1](https://main.qcloudimg.com/raw/f999a58033d7ddca296e4eb74f2758a9.png)
3. If the processes do not exist, possible reasons include the following:
 - The CWP agent is not installed on or has been uninstalled from the server. Please see [Getting Started](https://cloud.tencent.com/document/product/296/12236) and follow the instructions to install the agent.
 - The agent has a conflict or crash and thus cannot be started.
4. Troubleshooting methods:
 - View the agent log stored in `/usr/local/qcloud/YunJing/log`.
 - Run the following command to manually start the agent: `/usr/local/qcloud/YunJing/YDEyes/YDService`.

## Network Failures
If the processes exist, but CWP is offline, the issue is caused by network disconnection in most cases. Troubleshoot the network issue as shown below:
1. Run the following command to check whether the DNS has been modified: 
	- Basic network environment (non-VPC servers): telnet s.yd.qcloud.com 5574.
	- VPC or CPM environment: telnet s.yd.tencentyun.com 5574.
 
 In normal state, the returned result is as shown below:
	![](https://main.qcloudimg.com/raw/50e39ceadcb275a72738b235e9637b4c.png)

2. Make sure your firewall policies allows the following TCP ports: 5574, 8080, 80, and 9080.
