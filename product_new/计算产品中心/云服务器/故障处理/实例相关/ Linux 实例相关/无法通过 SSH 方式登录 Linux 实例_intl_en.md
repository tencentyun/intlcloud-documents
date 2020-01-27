This document uses the CVM with CentOS 7.5 operating system as an example to show you how to troubleshoot the problem where a Linux instance cannot be logged in to via SSH.

## Problems

When using SSH to log in to a Linux instance, you receive an error message that connection is unavailable or failed.

## Locating and troubleshooting the problem

1. Log in to the [Cloud Virtual Machine Console](https://console.cloud.tencent.com/cvm).
2. On the instance management page, select the instance to be troubleshot and choose **More* > **Security Group** > **Configure Security Group**, as shown below:
![](https://main.qcloudimg.com/raw/deff7af1803cc95cfd45036b850a9cb6.png)
3. In the “Configure Security Group” pop-up window, click the configured (selected) security group ID.
Enter the page where security group bound to this instance appears.
![](https://main.qcloudimg.com/raw/8beddaae54897226d160c7d54c488990.png)
4. On the inbound rule tab page of the security group rule, click **Open All**.
5. In the pop-up window, click **OK**.
6. Log in to the Linux instance via SSH again to check whether the login is successful.
 - Yes. The problem has been solved.
 - No. Go to [Step 7](#step07).
7. <span id="step07">Log in to the Linux instance via virtual network computing (VNC).</span>
8. On the operating system UI, run the following command to check whether a port is listened on by the SSH daemon (SSHD) service:
```
netstat -tnlp | grep sshd
```
 - If the following result is returned, the SSHD process is listening on port 22. Go to [Step 9](#step09).
```
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      1015/sshd  
```
 - If no result is returned, the SSHD service may haven’t started yet. Go to [Step 3](#step03).
9. <span id="step09">Run the following command to check whether the SSHD service has started.</span>
```
systemctl status sshd.service
```
 - If the SSHD service has started, send feedback by [Submit Ticket](https://console.cloud.tencent.com/workorder/category).
 - If the SSHD service has not started, run the following command to start the SSDH service and log in to the Linux instance again via SSH.
```
systemctl start sshd
```

If you still cannot connect to your instance after performing these steps, we recommend you send feedback by [Submit Ticket](https://console.cloud.tencent.com/workorder/category).





