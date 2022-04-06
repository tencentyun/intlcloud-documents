## Error Description
Log contains the error message “fork: Cannot allocate memory”.
![](https://main.qcloudimg.com/raw/db85a43e7495f1655a2b59063ffc33e3.png)

## Possible Reasons
This issue may be caused by excessive threads. If a new thread is created after the `pid_max` value is reached, the error message “fork: Cannot allocate memory” appears.

## Solutions
1. Perform the [troubleshooting procedure](#ProcessingSteps) to check the memory utilization.
2. Check the number of threads and modify the `pid_max` configuration. 



## Troubleshooting Procedure[](id:ProcessingSteps)
1. Check the memory utilization as instructed in [High Memory Utilization](https://intl.cloud.tencent.com/document/product/213/40501). If the memory utilization is normal, proceed to the next step.
2. Run the following command to obtain the value of `pid_max`.
```
sysctl -a | grep pid_max
```
The default value of `pid_max` is `32768`, as shown below:
![](https://main.qcloudimg.com/raw/816a0bd183244aadf14e04c6ed200d68.png)
3. Run the following command to view the total number of threads.
```
pstree -p | wc -l
```
When the total number of threads has reached `pid_max`, a new thread will cause the “fork: Cannot allocate memory” error.
>?You can use the `ps -efL` command to locate the programs for which many threads are running.
>
4. Change the `kernel.pid_max` value in the `/etc/sysctl.conf` configuration file to `65535` to increase the number of threads. The result should be as follows:
![](https://main.qcloudimg.com/raw/a4bbf49b3236b9f50988e914298adb31.png)
5. Run the following command for the configuration to take effect immediately.
```
sysctl -p
```
