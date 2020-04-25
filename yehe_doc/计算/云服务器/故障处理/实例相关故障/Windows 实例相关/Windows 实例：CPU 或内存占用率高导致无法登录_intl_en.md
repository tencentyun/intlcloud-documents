This document describes how to troubleshoot the issue of Windows CVM login failure due to high CPU or memory usage.
> The following procedure uses Windows Server 2012 R2 as an example. The specific procedure may vary depending on your operating system.

## Possible Causes

High CPU or memory usage may cause service slowdown or login failure. The causes can range from hardware, system processes, service processes, or even trojans or viruses. You can use [Cloud Monitor](https://intl.cloud.tencent.com/document/product/248/32799) to create alerts to track CPU or memory usage. You will be alerted when CPU or memory usage exceeds the set threshold values.

## Troubleshooting

1. Identify the process causing high CPU or memory usage.
2. Analyze the process.
 - If it is an abnormal process, it may be caused by a virus or trojan. Terminate the process and use an antivirus application to scan your system.
 - If it is a normal process, see if a change to parameters caused the high usage and if it can be optimized.
 - If it is a Tencent Cloud component process, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for further assistance.

## Tools

**Task Manager**: this is a tool to manage programs and processes included with Microsoft Windows systems. It provides information about computer performance and running software, including the names of running processes, CPU load, I/O details, logged-in users, and Windows services.
- **Processes**: a list of all running processes.
- **Performance**: system performance statistics such as overall CPU usage and memory usage.
- **Users**: all current user sessions.
- **Details**: a detailed list of running processes, including information such as PID, status, CPU usage, and memory usage.
- **Services**: a list of services, including those that are not running.


## Troubleshooting

### Logging in to CVM instances using VNC
> If you cannot log in to your CVM instance due to high CPU or memory load, we recommend [Logging in to Windows Instances via VNC](https://intl.cloud.tencent.com/document/product/213/32496). 
>
1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index).
2. On the instance management page, find the desired CVM instance and click **Log In**.
3. In the **Log in to Windows instance** window that appears, select **Alternative login methods (VNC)** and click **Log In Now** to log in to the CVM.
4. In the login window that appears, select **Send Remote Command** in the top-left corner. Click **Ctrl-Alt-Delete** to enter the system login interface.

### Viewing process resource usage

1. In CVM, right-click the taskbar and select **Task Manager** as shown below:
![](https://main.qcloudimg.com/raw/a795f4948fae3eab8a44ec0a3a4ee352.png)
2. In “Task Manager”, you can view the resource usage as shown below:
> You can sort the processes in ascending/descending order by clicking CPU or memory.
>
![](https://main.qcloudimg.com/raw/56a4be427be5046a15a05b02abbacf66.png)

### Analyzing the processes

Identify the process causing the issue. Analyze it to find the root cause and implement a fix.
#### A system process is causing the issue
If a system process is causing the issue, follow these steps:
1. Verify the name of the process.
 Several viruses use names that are very similar to system processes, such as svch0st.exe, explore.exe, or iexplorer.exe.
2. Locate the executable file that corresponds to the process.
 System processes are usually located in `C:\Windows\System32`. They should all have valid digital signatures and descriptions. To locate the corresponding executable file, select a process in Task Manager, right-click the process, and select `Open file location`.
 - If the executable file is not in `C:\Windows\System32`, it is likely that your CVM instance is infected. Use an antivirus application or manually fix the issue.
 - If the executable file is in `C:\Windows\System32`, reboot your instance or close non-essential processes.

The following is a list of typical system processes:
 - System Idle Process: the System Idle Process indicates the percentage of time that the processor is idle. 
 - system: the system process is responsible for the system memory and compressed memory in the NT kernel.
 - explorer: the explorer process is responsible for desktop and file management.
 - iexplore: the iexplore process is the process for Microsoft Internet Explorer.
 - csrss: the csrss process is responsible for console windows, creating and/or deleting threads, and implementing some portions of the 16-bit virtual MS-DOS environment.
 - svchost: the svchost process is a system process that can host one or more Windows services in the Windows NT family of operating systems.
 - Taskmgr: the Taskmgr process is the process for Task Manager.
 - Isass: the Isass process is a process in Microsoft Windows operating systems that is responsible for enforcing the security policy on the system.

#### Strange processes are causing the issue
If you find that the high CPU and memory usage issue is caused by processes with strange names, such as xmr64.exe (a cryptocurrency mining malware), your CVM instance may be infected with viruses or trojans. Use a search engine to verify if the processes are in fact viruses or trojans.
 - Use an antivirus application to remove the virus or trojan. Back up data and reinstall the operating system if necessary. 
 - If the process is not a virus or trojan, reboot your CVM instance and close non-essential processes.

#### A service process is causing the issue
If you find that a service process, such as IIS, HTTPD, PHP, or Java, is causing the issue, further investigate the situation. 
Is your business volume high?
- If so, we recommend that you [upgrade your CVM instance](https://intl.cloud.tencent.com/document/product/213/2178). Otherwise, consider optimizing your service deployment.
- If not, use logs to troubleshoot and see if a misconfigured parameter is causing the issue.

#### A Tencent Cloud process is causing the issue.

- If the process causing the issue is a Tencent Cloud component process, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for further assistance.

