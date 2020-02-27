## Agent Process Not Started
1. Check whether the CWP process exist.
Open Windows Task Manager and check whether the `YDService.exe` process exists.
 ![](https://main.qcloudimg.com/raw/27dbe87687c917e2cd2426cbc71a45c4.png)
2. If the agent process do not exist, possible reasons include the following:
 - The CWP agent is not installed on or has been uninstalled from the server. Please see [Getting Started](https://cloud.tencent.com/document/product/296/12236) and follow the instructions to install the agent.
 - The agent has a conflict or crash and thus cannot be started.
3. Troubleshooting methods:
 - View the agent log stored in `C:\Program Files\QCloud\YunJing\log`.
 - Run the following command to manually start the agent: `sc start ydservice`.

## Network Failures
If the process exists, but CWP is offline, the issue is caused by network disconnection in most cases. Please check the following:
1. Check whether the DNS has been modified. If any of the following commands returns a normal result, the DNS is correct:
 - Download address for the basic network (non-VPC servers): `telnet s.yd.qcloud.com 5574`.
 - Download address for VPC and CPM: `telnet s.yd.tencentyun.com 5574`.
2. Make sure the following ports are open: 5574, 8080, 80, and 9080.
