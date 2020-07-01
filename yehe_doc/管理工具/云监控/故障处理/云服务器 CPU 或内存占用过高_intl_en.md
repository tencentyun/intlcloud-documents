## Overview
This document describes how to troubleshoot and solve the problem of not being able to log in to Windows and Linux CVM instances due to the instances’ overly high CPU or memory usage.

## Troubleshooting Approaches
1. Log in to the instance and identify the process that is causing high CPU or memory usage.
2. Analyze the process.
 - If the process has an exception, the exception may be caused by a virus or a trojan. In this case, terminate the process or use an antivirus application to scan your system.
 - If the process is a service process, check whether the high CPU or memory usage is caused by an access volume change and whether it can be optimized.
 - If the process is a Tencent Cloud component process, [submit a ticket](https://console.cloud.tencent.com/workorder/category) and we will help you locate and troubleshoot the problem.

## Locating and Troubleshooting the Problem

### Windows CVM instances

#### Logging in to a CVM instance via VNC

> If you cannot establish a remote connection with your CVM instance due to high CPU or memory load, see [Logging in to a Windows Instance via VNC](https://intl.cloud.tencent.com/document/product/213/32496). 

1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index).
2. On the instance management page, locate the target CVM instance and click **Log In**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/d9ccf04da21f4ac86d624742c87d5628.png)
3. On the **Log in to Windows instance** page that appears, click **Log In Now** under **Alternative login methods (VNC)** to log in to the CVM instance.
4. On the login page that appears, select **Send CtrlAltDel** in the upper-left corner and click **Ctrl-Alt-Delete** to access the system login page, as shown in the following figure:
![](https://main.qcloudimg.com/raw/5064251ea86085326e86884a1c13ef6b.png)


#### Viewing the resource usage of processes

1. In the CVM instance, right-click the taskbar and select **Task Manager**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/a795f4948fae3eab8a44ec0a3a4ee352.png)
2. In "Task Manager", you can view the resource usage, as shown in the following figure:
![](https://main.qcloudimg.com/raw/56a4be427be5046a15a05b02abbacf66.png)
> You can sort the processes in ascending or descending order by clicking **CPU** or **Memory**.


#### Analyzing the processes

Analyze the processes on the **Task Manager** page to troubleshoot and solve the problem.

 **The problem is caused by a system process**
If a system process is occupying too many CPU or memory resources, complete the following steps:
1. Verify the name of the process.
 Several viruses use names that are very similar to system processes, such as svch0st.exe, explore.exe, and iexplorer.exe.
2. Locate the executable file that corresponds to the process.
 System processes are usually located in `C:\Windows\System32` and have valid digital signatures and descriptions. To locate the corresponding executable file such as `svchost.exe`, select the process on the **Task Manager** page, right-click the process, and choose **Open file location**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/12780aa6830cc88668df41c6758b9213.png)
 - If the executable file is not in `C:\Windows\System32`, it is likely that your CVM instance has a virus. Kill the virus manually or by using an antivirus application.
 - If the executable file is in `C:\Windows\System32`, restart your CVM instance or end safe but unnecessary processes.

The following describes typical system processes:
 - System Idle Process: a process that displays the percentage of time that the processor is idle for
 - system: a memory management process
 - explorer: the desktop and file management process
 - iexplore: the Microsoft Internet Explorer process
 - csrss: the Microsoft client/server runtime subsystem
 - svchost: a system process that is used to execute DLLs
 - Taskmgr: the task manager process
 - Isass: the local security permission service

**The problem is caused by processes with exceptions**
If you find that high CPU and memory usage is caused by processes with strange names such as xmr64.exe (a cryptocurrency mining malware), your CVM instance may be infected with viruses or trojans. In this case, use a search engine to verify whether the processes are in fact viruses or trojans.
 - Use an antivirus application to remove the virus or trojan. Then, back up the data and reinstall the operating system when necessary.
 - If the process is not a virus or a trojan, restart your CVM instance or end safe but unnecessary processes.

**The problem is caused by a service process**
If you find that the problem is caused by a service process such as IIS, HTTPD, PHP, or Java, further analyze the problem.
For example, check whether your business volume is high.
- If yes, we recommend that you [upgrade your CVM instance](https://intl.cloud.tencent.com/document/product/213/2178). If you do not upgrade your CVM instance, optimize your service processes.
- If no, use service error logs to further analyze the problem. For example, check whether the resources are wasted due to incorrect parameter settings.

**The problem is caused by a Tencent Cloud component process**

If the problem is caused by a Tencent Cloud component process, [submit a ticket](https://console.cloud.tencent.com/workorder/category), and we will help you locate and troubleshoot the problem.


### Linux CVM instances
#### Logging in to the CVM instance

Select a CVM login method based on your actual needs.
- Log in to the Linux CVM remotely via third party software.
> If the Linux CVM has a high CPU load, you may fail to log in to the CVM.

- [Log in to a Linux instance via VNC](https://intl.cloud.tencent.com/document/product/213/32494).
> If the Linux CVM has a high CPU load, you can log in normally via the Console.
>

#### Viewing the resource usage of processes

Run the following command to view the system load. View the **%CPU** and **%MEM** columns and identify which processes consume more resources.
```plaintext
top
```

#### Analyzing processes
Analyze the processes on the **Task Manager** page to troubleshoot and solve the problem.
- If the problem is caused by a service process, analyze whether the service process can be optimized and accordingly optimize the process or [upgrade the CVM configuration](https://intl.cloud.tencent.com/document/product/213/2178).
- If the problem is caused by a process with an exception, the instance may have a virus. In this case, you can terminate the process or use an antivirus application to kill the virus. When necessary, back up the data and reinstall the operating system.
- If the problem is caused by a Tencent Cloud component process, [submit a ticket](https://console.cloud.tencent.com/workorder/category) and we will help you locate and troubleshoot the problem.
Common Tencent Cloud components include:
 - sap00x: a security component
 - Barad_agent: a monitoring component
 - secu-tcs-agent: a security component


#### Terminating processes

1. Compare the resource consumption of different processes and record the PID of the process that needs to be terminated.
2. Enter `k`.
3. Enter the PID of the process that needs to be terminated and press the **Enter** key to terminate it, as shown in the following figure:
Suppose you need to terminate a process whose PID is 23.
![](https://main.qcloudimg.com/raw/38a98b3fc36b09c4e3f99765d3cf5691.png)
> If `kill PID 23 with signal [15]:` appears after you press **Enter**, press **Enter** again to keep the default settings.
>
4. If the operation is successful, the message `Send PID 23 signal [15/sigterm]` will appear. Press **Enter** to confirm the termination.

### Other related problems
#### CPU usage is low but load average is high

**Problem**

The load average is an indicator of CPU load. The higher the load average, the longer the queue of pending processes is.
After the `top` command is executed, information similar to the following is returned, indicating that the CPU usage is low but the load average is very high.
![](https://mc.qcloudimg.com/static/img/4ddf663a68ee602d8cf8075d88edccf6/image.png)

#### Solution

Run the following command to view the process states and check whether any process is in the D state, as shown in the following figure:
```plaintext
ps -axjf
```
![](https://mc.qcloudimg.com/static/img/32420d3fe022b57d85120c941705dbf6/image.png)
 > The D state refers to the uninterrupted sleep state. A process in this state cannot be terminated nor can it be exited by itself.
 >
If there are many processes in the D state, restore the resources on which the processes depend or restart the operating system.

#### CPU usage of the kswapd0 process is high

**Problem**

Linux manages memory by using the pagination mechanism and sets aside a portion of the disk as virtual memory. kswapd0 is the process responsible for page replacement in the virtual memory management of the Linux system. When system memory becomes insufficient, kswapd0 will frequently replace pages, which will result in high CPU usage.

**Solution**

1. Run the following command and find the kswapd0 process.
```plaintext
top
```
2. Check the state of the kswapd0 process.
If the process is not in the D state and has been running for a long time and consuming too many CPU resources, perform [step 3](#kswapd0_step3) to check the memory usage.
3. <span id="kswapd0_step3">Run commands such as `vmstat`, `free`, and `ps` to check how much memory is being consumed by processes in the system.</span>
Based on the memory usage, restart the system or terminate safe but unnecessary processes. If the si and so values are also high, pages are frequently replaced in the system. If the physical memory of the current system can no longer meet your requirements, please consider upgrading your system memory.

