## Problem Description
When using a GPU instance, if you use `nvidia-smi` to view the GPU status in the system, the GPU usage may be displayed as 100% while no processes are using GPU, as shown below:
![](https://mc.qcloudimg.com/static/img/5a58bc996b38c28b94131105a3fbd000/image.png)
## Possible Causes
This may be caused by the ECC Memory Scrubbing mechanism used when the instance loads the NVIDIA driver.
## Solution
Run the `nvidia-smi -pm 1` command in the instance system to get the GPU Driver into the Persistence mode.
## Instructions
1. Log in to the GPU instance and run the following command:
```
nvidia-smi -pm 1
```
![](https://mc.qcloudimg.com/static/img/456d59df82aa68c243b6073bfe63f490/image.png)
2. Run the following command to check GPU usage:
```
nvidia-smi
```
You will see the GPU usage is normal, as shown below:
![](https://mc.qcloudimg.com/static/img/460c515a0a7ac32b4c525b759e13c732/image.png)

