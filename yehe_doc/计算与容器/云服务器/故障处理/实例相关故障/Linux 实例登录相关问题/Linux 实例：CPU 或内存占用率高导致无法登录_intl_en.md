## Scenario

This document describes how to investigate and solve issues such as failure to log in to a Linux CVM due to high CPU and memory usage.

## Directions

### Logging in and viewing the system load

1. Log in to the CVM in different ways depending on your actual needs.
	- Log in to the Linux CVM via third party software remotely.
	>  When the Linux CVM has a high CPU load, you may fail to log in.
	>
	- Log in to CVM via **VNC**.
	Log in to the [CVM console](https://console.cloud.tencent.com/cvm) > click **Log in** in the right operation column > log in with alternative login methods (VNC).
	> When the Linux CVM has a high CPU load, you may be able to log in via the console normally.
	>
2. Execute the following command to view the system load. View the `%CPU` column and the `%MEM` column and identify which processes consume more resources.
```
top
```

### Terminating processes

1. Compare the resource consumption of different processes and record the PIDs of processes which need to be terminated.
2. Enter ` k `.
3. Enter the PID of the process which needs to be terminated, and press **Enter** to terminate it as shown below:
For example, you need to terminate a process whose PID is 23.
![](//mc.qcloudimg.com/static/img/61cd74354cf2b4d2a80a83528a500f5c/image.png)
> If `kill PID 23 with signal [15]:` appears after you press **Enter**, press **Enter** again to keep the default settings.
>
4. If the operation is successful, the following message, ` Send PID 23 signal [15/sigterm] ` will show up. Press **Enter** to confirm the termination.

### Low CPU usage but high load average

### Problem Description

The load average is an indicator of CPU load. A high load average indicates a long queue of processes waiting to run.
Running `top` returns very low CPU usage but very high load average as shown below.
![](//mc.qcloudimg.com/static/img/4ddf663a68ee602d8cf8075d88edccf6/image.png)
 
#### Solution
 
Execute the following command to view process states and check whether there is are processes in D state as shown below below:
```
ps -axjf
```
![](//mc.qcloudimg.com/static/img/32420d3fe022b57d85120c941705dbf6/image.png)
 > Processes in D state are in uninterrupted sleep. Processes in the state cannot be terminated nor exit by itself. If there are many processes in D state, you can solve the problem by restoring resources on which the processes depend or restarting the system.
 >


### kswapd0 process uses much CPU

### Problem Description

Linux manages memory with the paging mechanism, and it also sets aside a portion of the disk for virtual memory. kswapd0 is the process responsible for page replacement in the  virtual memory management of Linux system. When there is not enough system memory, kswapd0 will frequently replace pages, which is very CPU consuming. That is why the process uses a lot of CPU.
 
#### Solution

1. Execute the following command and find the kswapd0 process.
```
top
```
2. Observe the state of the kswapd0 process.
If the process is not sleeping, has run for a long time, and has been using a lot of CPU, please take [Step3](#kswapd0_step3) to check the memory usage rate.
3. <span id="kswapd0_step3">Execute commands, such as `free`，`ps` to check how much memory is being used by processes in the system.</span>
Restart the system or terminate the processes that are safe but unnecessary based on the memory usage rate.

If the problem is not solved, please refer to [High CPU usage rate (Linux system)](https://intl.cloud.tencent.com/document/product/213/14634) for more details.
