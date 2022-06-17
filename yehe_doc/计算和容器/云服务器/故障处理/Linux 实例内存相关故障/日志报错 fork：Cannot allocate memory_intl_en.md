## Error Description
Log contains the error message "fork: Cannot allocate memory".
![](https://main.qcloudimg.com/raw/db85a43e7495f1655a2b59063ffc33e3.png)

## Common Causes
There are too many processes. If a new process is created after the `pid_max` value is reached, the error message "fork: Cannot allocate memory" will appear.

## Solution
1. Check the memory utilization as instructed in [Steps](#ProcessingSteps).
2. Check the number of processes and modify the `pid_max` configuration. 



## Steps[](id:ProcessingSteps)
1. Check the memory utilization as instructed in [High Memory Utilization](https://intl.cloud.tencent.com/document/product/213/40501). If the memory utilization is normal, proceed to the next step.
2. Run the following command to obtain the value of `pid_max`.
```
sysctl -a | grep pid_max
```
Perform corresponding operations according to the returned result:
 - If the returned result is as shown below, where the default value of `pid_max` is 32768, go to the next step.
![](https://main.qcloudimg.com/raw/816a0bd183244aadf14e04c6ed200d68.png)
 - If the error message "fork: Cannot allocate memory" is returned, run the following command to temporarily increase `pid_max`.
```
echo 42768 > /proc/sys/kernel/pid_max
```
Run the following command again to get the value of `pid_max`.
3. Run the following command to view the total number of processes.
```
pstree -p | wc -l
```
When the total number of processes has reached `pid_max`, a new process will cause the "fork: Cannot allocate memory" error.
<dx-alert infotype="explain" title="">
You can use the `ps -efL` command to locate the programs for which many processes are running.
</dx-alert>
4. Change the `kernel.pid_max` value in the `/etc/sysctl.conf` configuration file to `65535` to increase the number of processes. The result should be as follows:
![](https://main.qcloudimg.com/raw/a4bbf49b3236b9f50988e914298adb31.png)
5. Run the following command for the configuration to take effect immediately.
```
sysctl -p
```
