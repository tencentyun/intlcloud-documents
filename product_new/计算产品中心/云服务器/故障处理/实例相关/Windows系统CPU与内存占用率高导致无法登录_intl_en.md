## Scenario

This document describes how to investigate and solve the problem of failing to log in to a Windows CVM due to high CPU and memory usage.
> The following steps take Windows server 2012 R2 as an example. Operation details may vary slightly depending on the operating system version.

## Directions

### Logging in to the CVM using mstsc

1. On your local computer, use the **Windows+R** shortcut to open the Run box.
2. Enter **mstsc** and press **Enter** to open the “Remote Desktop Connection” interface.
3. In the “Remote Desktop Connection” window, enter the public IP address of the CVM and the login password to log in to the CVM.
> If the CVM has a high load average, you will not be able to establish a remote connection. You will have to log in to the CVM using **VNC**. You can do so by logging in to the [CVM console](https://console.cloud.tencent.com/cvm), clicking **Log in** in the right operation column, and selecting alternative login methods (VNC).

### Viewing the resource usage of processes

1. In CVM, right click the taskbar, and select **Task Manager** as shown below:
![](https://main.qcloudimg.com/raw/a795f4948fae3eab8a44ec0a3a4ee352.png)
2. In the “Task Manager”, you can view the resource usage as shown below:
> You can sort the processes in ascending/descending order by clicking CPU or memory.
>
![](https://main.qcloudimg.com/raw/56a4be427be5046a15a05b02abbacf66.png)

### Analyzing the processes

Analyze the resource usage of the processes in Task Manager and adopt solutions according to your situation.
 - Some business processes such as IIS, httpd, PHP, and Java are consuming a lot of resources.
 	- If there is indeed heavy traffic currently, it is normal to have a high load. You may need to consider expansion.
 	- If the current business load is not high, you may need to refer to the service error log for further analysis. The root cause may be improper parameter configuration which can cause a waste of resources.
 - System processes such as `svchost.exe` are consuming a lot of resources.
 	- You can verify if a process is a system process on the Internet.
 	- A system process is usually located in the `C:\windows\system32` directory and has a signature and a complete description.
 	- Restart the system or shut down secure but unnecessary system processes.
 - Neither business processes nor system processes are consuming a lot of resources.
	 - If there are some processes which have strange names, do not have a signature or a description, are not in the `C:\windows\system32` directory, and are consuming abnormally high amount of resources, the CVM may have been infected with viruses.
	 - Check the security of the server. Back up the data and reinstall the system if necessary.
