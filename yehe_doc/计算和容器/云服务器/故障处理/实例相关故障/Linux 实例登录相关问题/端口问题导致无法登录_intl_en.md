This document describes how to diagnose and troubleshoot remote login failures caused by port problems.
>?The following operations use a CVM instance with the CentOS 7.8 operating system as an example.
>

## Tools
You can use the following tools to check whether the login issues are related to port or security group configuration:
- [Self-diagnose](https://console.cloud.tencent.com/workorder/check)
- [Port Verification](https://console.cloud.tencent.com/vpc/helper)

If the problem is indeed caused by security group configurations, click **Open all ports** in [Port Verification](https://console.cloud.tencent.com/vpc/helper) and try to log in again. If you still cannot log in after opening the ports, refer to the following for troubleshooting.

## Troubleshooting
### Checking network connectivity
You can use the `Ping` command to test network connectivity from your PC. You should run the test from computers in different network environments (such as different IP ranges or ISPs) to check whether it is a local network problem or a server problem.
1. Open the command line tool on your local computer.
	- **Windows**: click **Start** > **Run** and enter `cmd`. A Command Prompt window appears.
	- **MacOS**: open a Terminal window.
2. Run the following command to test network connection.
```
ping [CVM instance’s public IP address]
```
You should first [obtain the public IP address](https://intl.cloud.tencent.com/document/product/213/17940) of the CVM instance. For example, `ping 81.71.XXX.XXX`.
 - If the result similar to the following is returned, your network connection to the CVM instance is normal.
![](https://main.qcloudimg.com/raw/796dd285720755d7b5dc9e0bee492c83.png)
 - If **Request Timeout** appears, your network connection to the CVM instance is not working properly. In this case, refer to [Instance IP Address Ping Failure](https://intl.cloud.tencent.com/document/product/213/14639) for troubleshooting instructions.

### Checking port connectivity
1. [Log in to a Linux instance via VNC](https://intl.cloud.tencent.com/document/product/213/32494).
2. Run the following command and press **Enter** to check whether the remote port is open and accessible.
```
telnet [CVM instance’s public IP address] [Port number]
```
For example, run the `telnet 119.XX.XXX.67 22` command to check whether the port 22 is open.
 - If information similar to what is shown below is returned, the port 22 is accessible.
![](https://main.qcloudimg.com/raw/246134de6829323457dc1d51f85589b8.png)
 - If information similar to what is shown below is returned, the port 22 is unaccessible. Check the corresponding network configuration. For example, check whether the port 22 is open in the firewall or security group of the instance.
 ![](https://main.qcloudimg.com/raw/d6eadfe7638046f0b0c1f15261ea74ab.png)


### Checking the SSHD service
If you are unable to [log in to a Linux instance via SSH key](https://intl.cloud.tencent.com/document/product/213/32501) due to connection failures, it may be because the SSHD port is not being listened on or the SSHD service is not started. In this case, refer to [Unable to Log into a Linux Instance via SSH](https://intl.cloud.tencent.com/document/product/213/32486) for troubleshooting instructions.
