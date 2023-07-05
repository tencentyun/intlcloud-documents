## Error Description
The Linux CVM does not run out of memory and triggers OOM (Out of Memory) as shown below:
![](https://main.qcloudimg.com/raw/72cbd63ac445a1caa8d82fa1e55ba5a5.png)

## Possible Reasons
This issue may be caused by the `min_free_kbytes` configuration. It specifies the minimum idle memory of the Linux system (in kilobytes). When the system’s available memory goes below the set value of `min_free_kbytes`, the system will invoke oom-killer or forcibly restart depending on the `vm.panic_on_oom` kernel parameter:
 - If `vm.panic_on_oom=0` is set, the system prompts OOM and invokes oom-killer to kill the process using the most memory.
 - If `vm.panic_on_oom =1` is set, the system will restart automatically.

## Solutions
1. Perform the [troubleshooting procedure] to check the memory utilization and total number of threads.
2. Correct the `min_free_kbytes` configuration.


## Troubleshooting Procedure[](id:ProcessingSteps)
1. Check the memory utilization as instructed in [High Memory Utilization](https://intl.cloud.tencent.com/document/product/213/40501). If the memory utilization is normal, proceed to the next step.
2. Check whether the number of threads exceeds the limit as instructed in [Log Error “fork: Cannot allocate memory”](https://intl.cloud.tencent.com/document/product/213/40502). If the number of threads is within the limit, proceed to the next step.
3. Log in to the CVM and run the following command to view the `min_free_kbytes` configuration.
```
sysctl -a | grep min_free
```
The `min_free_kbytes` value is in kbytes. For example, the `min_free_kbytes = 1024000` shown below is 1 GB.
![](https://main.qcloudimg.com/raw/18ac6c04962abfbf67132eab1a604167.png)
4. Run the following command to open the `/etc/sysctl.conf` configuration file with VIM editor.
```
vim /etc/sysctl.conf
```
5. Press **i** to enter the edit mode and modify the `vm.min_free_kbytes` configuration item.
>? We recommend changing the `vm.min_free_kbytes` value to no more than 1% of the total memory.
>
6. Press **Esc**, enter **:wq**, and press **Enter** to save the configurations and exit the VIM editor.
7. Run the following command for the configuration to take effect.
```
sysctl -p
```
