## Failed Startup of CWPP Agent Processes
1. Check whether the CWPP process exists.
Open Windows Task Manager and check whether the `YDService.exe` process exists.
 ![](https://qcloudimg.tencent-cloud.cn/raw/ac7115446eb5743870b62c6cdac2a4b8.png)
2. If the process does not exist, possible reasons include the following:
 - The CWPP agent is not installed on the server or has been uninstalled from the server. Please install it by following the steps described in [Getting Started](https://intl.cloud.tencent.com/document/product/296/12236)
 - The agent has a conflict or crash, which leads to the failed startup of processes.
3. Troubleshooting methods:
 - View the agent log stored in `C:\Program Files\QCloud\YunJing\log`.
 - Run the command `sc start ydservice` to manually start the agent.


## Network Failures
If the process exists, but CWPP is offline, the issue is caused by network disconnection in most cases. Troubleshoot the issue by following the steps below:
1. Check whether the DNS has been modified by running the following commands. If a normal result is returned, the DNS is correct:
 - Download address for the basic network (non-VPC servers): `telnet s.yd.qcloud.com 5574`.
 - Download address for VPC and CPM: `telnet s.yd.tencentyun.com 5574`.
2. Make sure the ports 5574, 8080, 80, and 9080 are open in the firewall rules.
3. If the CWPP process exists and the offline state of the CWPP agent is not caused by network issues, package the agent logs (log path: `C:\Program Files\QCloud\YunJing\log`) and [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for feedback.