This document uses the CVM with CentOS 7.5 as an example to show how to troubleshoot the problem where a Linux instance cannot be logged in to by using SSH.

## Problems

During [login to a Linux instance by using SSH](https://intl.cloud.tencent.com/document/product/213/32501), a message indicating that the connection is unavailable or failed appears.

## Locating and Troubleshooting the Issues
### Step 1: Checking the security group rule configuration

Use the [port verification tool for security groups](https://console.cloud.tencent.com/vpc/helper) to check whether security group rules are correct.
- If the problem is caused by the security group port configuration, you can use the **Open All Ports** feature to open all ports. You can also customize security group rules based on your actual needs. For more information, see [Adding Security Group Rules](https://intl.cloud.tencent.com/document/product/213/34272).
- If the security group port configuration is correct, proceed to [the next step](#step07).
 
### Step 2: Querying the SSHD service port
1. <span id="step07">[Log in to a Linux instance by using VNC](https://intl.cloud.tencent.com/document/product/213/32494).</span>
>?When the remote login and other login methods fail, you can use VNC to connect the instance, monitor instance status, and troubleshoot issues.
>
2. On the operating system interface, run the following command to check whether a port is listened on by the SSH daemon (SSHD) service:
```
netstat -tnlp | grep sshd
```
 - If the following result is returned, the SSHD process is listening on port 22. In this case, [submit a ticket](https://console.cloud.tencent.com/workorder/category).
```
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      1015/sshd  
```
 - If no result is returned, the SSHD service be not launched yet. In this case, proceed to [the next step](#step09).
 
### Step 3: Checking whether the SSHD service has been launched
<span id="step09">Run the following command to check whether the SSHD service has been launched.</span>
```
systemctl status sshd.service
```
 - If yes, [submit a ticket](https://console.cloud.tencent.com/workorder/category).
 - If no, run the following command to launch the SSDH service and try to log in to the Linux instance again by using SSH.
```
systemctl start sshd
```

If you still cannot log in to your instance after performing these steps, we recommend that you report this problem by [submitting a ticket](https://console.cloud.tencent.com/workorder/category).

