This document describes how to troubleshoot Windows CVM login failures due to high CPU or memory utilization.
> The following uses Windows Server 2012 R2 as an example. The steps may vary by operating system (OS) versions.

## Possible Causes

Hardware, system processes, service processes, trojans, and viruses may cause high CPU or memory utilization, resulting in slow service response speed or CVM login failure. You can use [Cloud Monitor](https://intl.cloud.tencent.com/document/product/248/32799) to create an alarm threshold for CPU or memory usage. You will be notified promptly when the configured threshold is exceeded.

## Troubleshooting

1. Identify the process that causes high CPU or memory utilization.
2. Analyze the process.
 - If it is an unhealthy process, it may be caused by a virus or trojan. Terminate the process or use an antivirus application to scan the system.
 - If it is a service process, check whether the high CPU or memory utilization is caused by access traffic and whether it can be optimized.
 - If it is a Tencent Cloud component process, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

## Tools

**Task Manager**: an application and process manager included with the Microsoft Windows OS. It provides information on computer performance and running software, such as the names of running processes, CPU load, memory usage, I/O, logged-in users, and Windows services.
- **Processes**: a list of all running processes.
- **Performance**: system performance statistics such as the overall CPU usage and current memory usage.
- **Users**: all users with sessions.
- **Details**: an enhanced version of the processes tab, including detailed information on PID, status, CPU usage, and memory usage.
- **Services**: a list of all services, including those that are not running.


## Troubleshooting Method

### Logging in to the CVM instance using VNC
> If you cannot log in to your CVM instance due to high CPU or memory utilization, we recommend [logging into Windows instance via VNC](https://intl.cloud.tencent.com/document/product/213/32496). 
>
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index).
2. On the instance management page, locate the CVM instance and click **Log In**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/d9ccf04da21f4ac86d624742c87d5628.png)
3. In the pop-up "Log into Windows instance" window, select **Alternative login methods (VNC)** and click **Log In Now** to log in to the CVM instance.
4. In the pop-up login window, select "Send CtrlAltDel" in the upper-left corner and click **Ctrl-Alt-Delete** to go to the OS login page, as shown in the following figure:
![](https://main.qcloudimg.com/raw/5064251ea86085326e86884a1c13ef6b.png)

### Viewing the resource usage of processes

1. In the CVM, right-click the "taskbar" and choose **Task Manager**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/a795f4948fae3eab8a44ec0a3a4ee352.png)
2. View resource usage in the "Task Manager" window, as shown in the following figure:
> You can click the CPU or memory column to sort the processes in ascending or descending order.
>
![](https://main.qcloudimg.com/raw/56a4be427be5046a15a05b02abbacf66.png)

### Analyzing processes

Analyze processes in Task Manager to identify the causes and troubleshoot accordingly.
#### A system process causes the issue
If a system process causes high CPU and memory utilization, troubleshoot as follows:
1. Check the name of the process.
 Some viruses use names similar to system processes, such as svch0st.exe, explore.exe, iexplorer.exe, etc.
2. Check the location of the executable file of a process.
 The executable file of a system process is usually located in `C:\Windows\System32` with valid signatures and descriptions. To locate the executable file of a process, such as `svchost.exe`, right-click the process in Task Manager and choose **Open file location**.
 - If the executable file is not in `C:\Windows\System32`, your CVM instance may have a virus. Scan for viruses with an antivirus application or manually fix the issue.
 - If the executable file is in `C:\Windows\System32`, restart your CVM instance or terminate unnecessary but secure system processes.

The following lists common system processes:
 - System Idle Process: a process that displays the percentage of time that the processor is idle
 - system: indicates the memory management process
 - explorer: indicates the desktop and file management process
 - iexplore: indicates the Microsoft Internet Explorer process
 - csrss: indicates the runtime subsystem on the Microsoft client or server
 - svchost: indicates the system process for running DLL
 - Taskmgr: indicates the task manager
 - Isass: indicates the local security authority service

#### An unhealthy process causes the issue
If high CPU or memory utilization is caused by a process that has a strange name, such as xmr64.exe (a cryptomining malware), your CVM instance may have a virus or trojan. We recommend using a search engine to verify.
 - If the process is a virus or trojan, use an antivirus application to delete the virus or trojan. If necessary, back up your data and reinstall the operating system.
 - If the process is not a virus or trojan, restart your CVM instance or terminate unnecessary but secure processes.

#### A service process causes the issue
If a service process such as IIS, HTTPD, PHP, or Java causes the issue, we recommend analyzing it further.
For example, check whether your business volume is high.
- If yes, we recommend [upgrading configuration](https://intl.cloud.tencent.com/document/product/213/2178) for your CVM instance. Alternatively, you can optimize service processes.
- If no, use service error logs to further analyze the issue. For example, check whether incorrect parameter configurations lead to resource waste.

#### A Tencent Cloud process causes the issue

- If a Tencent Cloud component process causes the issue, [submit a ticket](https://console.cloud.tencent.com/workorder/category) to contact us for assistance.

