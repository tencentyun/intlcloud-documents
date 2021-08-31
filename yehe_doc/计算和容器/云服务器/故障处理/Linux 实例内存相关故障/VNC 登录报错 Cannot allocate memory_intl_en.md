## Error Description
I cannot log in to the CVM via VNC, and the error message “Cannot allocate memory” appears.
![](https://main.qcloudimg.com/raw/0a31fdd909701c27c9923b2fff24668a.png)

## Possible Reasons[](id:PossibleCauses)
This issue may be caused by too many huge pages. The default huge page size is 2048 KB. The number of huge pages is stated in `/etc/sysctl.conf`. If there are 1280 huge pages (as shown below), 2.5 GB of memory are taken. In case of low instance specification, there may not be enough memory for proper system running, and you cannot enter the system after restarting it.
![](https://main.qcloudimg.com/raw/1978a0b2a85fc828674f720c108c48a3.png)


## Solutions
1. Perform the [troubleshooting procedure](#ProcessingSteps) to check whether the total number of threads exceeds the limit. 
2. Modify the configurations of huge pages as needed.


## Troubleshooting Procedure[](id:ProcessingSteps)
1. Check whether the total number of threads exceeds the limit as instructed in [Log Error “fork: Cannot allocate memory”](https://intl.cloud.tencent.com/document/product/213/40502). If not, proceed to the next step.
2. Enter the single user mode and log in to the CVM. For detailed directions, see [Booting into Linux Single User Mode](https://intl.cloud.tencent.com/document/product/213/34819).
3. Run the following command to check the configurations of huge pages.
```
cat /etc/sysctl.conf | grep hugepages
```
If there are many huge pages, perform the following steps to modify the configurations.
4. Run the following command to open the `/etc/sysctl.conf` configuration file with VIM editor.
```
vim /etc/sysctl.conf
```
5. Press **i** to enter the edit mode and reduce the value of the `vm.nr_hugepages`  as needed.
6. Press **Esc**, enter **:wq**, and press **Enter** to save the configurations and exit the VIM editor.
7. Run the following command for the configuration to take effect immediately.
```
sysctl -p
```
8. Then restart the CVM, and you can log in normally.
