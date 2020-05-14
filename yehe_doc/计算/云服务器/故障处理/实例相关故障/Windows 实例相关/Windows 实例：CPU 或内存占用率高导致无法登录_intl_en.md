This document describes how to troubleshoot Windows CVM login failures due to high CPU or memory utilization.
> The following uses Windows Server 2012 R2 as an example. The steps may vary slightly depending on the operating system (OS) version.

## Possible Causes

High CPU or memory utilization can result in slow service responsiveness or CVM login failure. Hardware, system processes, service processes, trojans, and viruses may cause high CPU or memory utilization. You can use [CloudMonitor](https://intl.cloud.tencent.com/document/product/248/32799) to create a CPU or memory usage alarm threshold. In this way, you will be alerted when the CPU or memory utilization exceeds the set threshold.

## Troubleshooting

1. Identify the process that causes high CPU or memory utilization.
2. Analyze the process.
 - If it is an unexpected process, it may be the result of a virus or trojan. In this case, terminate the process or scan your system by using an antivirus application.
 - If it is a service process, check whether the high CPU or memory utilization is caused by an access volume change and whether it can be optimized.
 - If it is a Tencent Cloud component process, [submit a ticket](https://console.cloud.tencent.com/workorder/category) and contact Tencent engineers for assistance.

## Tools

**Task Manager**: this is a tool for managing applications and processes in the Microsoft Windows OS. It provides information on computer performance and running software, including the names of running processes, CPU load, memory usage, I/O details, logged-in users, and Windows services.
- **Processes**: shows a list of all running processes.
- **Performance**: provides system performance statistics such as overall CPU usage and memory usage.
- **Users**: lists all users with sessions.
- **Details**: offers a detailed list of running processes, including information such as the PID, status, CPU usage, and memory usage.
- **Services**: provides a list of all services, including those that are not running.


## Troubleshooting

### Logging in to the CVM instance by using VNC
> If you cannot log in to your CVM instance due to high CPU or memory utilization, [use VNC to log in to the Windows instance](https://intl.cloud.tencent.com/document/product/213/32496). 
>
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index).
2. On the instance management page, locate the target CVM instance and click **Log In**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/d9ccf04da21f4ac86d624742c87d5628.png)
3. In the "Log into Windows instance" window that appears, select **Alternative login methods (VNC)** and click **Log In Now** to log in to the CVM instance.
4. In the login window that appears, select "Send CtrlAltDel" in the upper-left corner and click **Ctrl-Alt-Delete** to go to the OS login page, as shown in the following figure:
![](https://main.qcloudimg.com/raw/5064251ea86085326e86884a1c13ef6b.png)

### Viewing the resource usage of processes

1. In the CVM, right-click the "taskbar" and choose **Task Manager**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/a795f4948fae3eab8a44ec0a3a4ee352.png)
2. In the "Task Manager" window, view resource usage, as shown in the following figure:
> You can click the CPU or memory column to sort the processes in ascending or descending order.
>
![](https://main.qcloudimg.com/raw/56a4be427be5046a15a05b02abbacf66.png)

### Analyzing processes

Analyze processes in Task Manager to identify the causes and take appropriate measures.
#### A system process causes the issue
If a system process causes the issue, complete these steps:
1. Check process names.
 Some malicious programs use names that are similar to system processes, such as svch0st.exe, explore.exe, and iexplorer.exe.
2. Check the locations of the executable files of processes.
 The executable files of system processes are usually located in `C:\Windows\System32` with valid signatures and descriptions. To locate the executable file of a process, such as `svchost.exe`, right-click the process in Task Manager and choose **Open file location**.
 - If the executable file is not in `C:\Windows\System32`, your CVM instance may be infected with viruses. In this case, scan for viruses with an antivirus application or manually fix the issue.
 - If the executable file is in `C:\Windows\System32`, restart your CVM instance or terminate secure but unnecessary system processes.

The following lists common system processes:
 - System Idle Process: displays the percentage of time that the processor is idle.
 - system: indicates the memory management process.
 - explorer: indicates the desktop and file management process.
 - iexplore: indicates the process for Microsoft Internet Explorer.
 - csrss: indicates the runtime subsystem on the Microsoft client or server
 - svchost: indicates the system process for running DLLs.
 - Taskmgr: indicates the task manager.
 - Isass: indicates the local security permission service.

#### An unexpected process causes the issue
If you find that a process with a strange name, such as xmr64.exe (a cryptocurrency mining malware) causes high CPU or memory utilization, your CVM instance may be infected with viruses or trojans. In this case, use a search engine to verify whether the process is a virus or trojan.
 - If the process is a virus or trojan, use an antivirus application to remove the virus or trojan. Back up your data and reinstall the OS if necessary.
 - If the process is not a virus or trojan, restart your CVM instance or terminate secure but unnecessary processes.

#### A service process causes the issue
If you find that a service process such as IIS, HTTPD, PHP, or Java causes the issue, further analyze the issue.
For example, check whether your business volume is high.
- If yes, we recommend that you [upgrade your CVM instance](https://intl.cloud.tencent.com/document/product/213/2178). If you do not upgrade your CVM instance, optimize your service processes.
- If no, use service error logs to further analyze the issue. For example, check whether resources are wasted due to incorrect parameter settings.

#### A Tencent Cloud process causes the issue

- If a Tencent Cloud component process causes the issue, [submit a ticket](https://console.cloud.tencent.com/workorder/category) to contact Tencent engineers for assistance.

