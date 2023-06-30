## Overview
Compute Unified Device Architecture (CUDA™) is a computing platform developed by NVIDIA. With a generic parallel computing architecture, CUDA allows GPUs to solve complex computing problems. It includes the CUDA instruction set architecture (ISA) and the parallel computing engine within the GPU. The CUDA platform is designed to work with programming languages such as C, C++, and Fortran. The compiled programs can be run on CUDA-enabled processors.

Because GPU instances use NVIDIA graphic cards, you must install the CUDA Toolkit. This document uses the most common CUDA Toolkit 10.1 as an example to describe how to install CUDA Toolkit on a GPU instance.


## Directions
### Installing CUDA Toolkit on a Linux instance
1. Go to the [CUDA Toolkit](https://developer.nvidia.com/cuda-toolkit-archive) download page or visit `https://developer.nvidia.com/cuda-toolkit-archive`.
2. Select the CUDA Toolkit version, as shown in the following figure. Below uses CUDA Toolkit 10.1 as an example.
![](https://main.qcloudimg.com/raw/1bff72aeaceb4ad6a930861c5a5d74f0.png)
3. Configure the platform information as instructed, as shown in the following figure.
>!**Installer Type**: We recommend selecting **runfile (local)**.
> - **network**: the network installer. It is a small executable and an internet connection is required during the installation.
> - **local**: the local installer. It is very large and has all of the components embedded into it.
> 
![](https://main.qcloudimg.com/raw/acadac8128996daf65731875ae8aec3e.png)
4. <span id="Step4"></span>When the following information appears, right-click **Download** and select **Copy link address**, as shown in the following figure.
![](https://main.qcloudimg.com/raw/a494df725c2e7bcd924a0331ccaf9a11.png)
5. To log in to GPU instances, see [Log into Linux Instance Using Standard Login Method](https://intl.cloud.tencent.com/document/product/213/5436). You can also use other login methods:
	- [Logging into Linux instances via remote login tools](https://intl.cloud.tencent.com/document/product/213/32502)
	- [Logging into Linux instance via SSH key](https://intl.cloud.tencent.com/document/product/213/32501)
6. Run the `wget` command to download the installer using the URL copied in [Step 4](#Step4), as shown in the following figure.
![](https://main.qcloudimg.com/raw/0301e9615259750e5ce9f6fbe6874238.png)
You can also download the installer to your local computer and upload it to the GPU instance.
7. Add execution permissions to the installer. For example, to add execution permissions to the `cuda_10.1.105_418.39_linux.run` file, run the following commands in sequence:
```
 sudo chmod +x cuda_10.1.105_418.39_linux.run
```
```
./cuda_10.1.105_418.39_linux.run --toolkit --samples --silent
```
8. Restart the operating system.
9. Run the following commands in sequence to configure environment variables:
```
echo 'export PATH=/usr/local/cuda/bin:$PATH' | sudo tee /etc/profile.d/cuda.sh
```
```
source /etc/profile
```
10. <span id="Step10"></span>Run the following commands in sequence to check whether CUDA Toolkit has been installed:
```
cd /usr/local/cuda-10.1/samples/1_Utilities/deviceQuery
```
```
make
```
```
./deviceQuery
```
If Result=PASS is returned, the installation is successful.
After you run the `make` command, the following error is shown.
![](https://main.qcloudimg.com/raw/416e1e50a4226925af6debb6cb26f0c8.png)
In this case, run the following command to install gcc:
```
yum install -y gcc-c++
```
After the installation is completed, repeat [Step 10](#Step10) to verify.


### Installing CUDA Toolkit on a Windows instance
1. To log in to GPU instances, see [Logging in to a Windows Instance Using the RDP File (Recommended)](https://intl.cloud.tencent.com/document/product/213/5435).
2. Visit the [CUDA Toolkit](https://developer.nvidia.com/cuda-toolkit-archive) download page.
3. Select the CUDA Toolkit version, as shown in the following figure. Below uses CUDA Toolkit 10.1 as an example.
![](https://main.qcloudimg.com/raw/1bff72aeaceb4ad6a930861c5a5d74f0.png)
4. Configure the platform information as instructed, as shown in the following figure.
![](https://main.qcloudimg.com/raw/9c25375680dcad463e8d758d3bbb0977.png)
5. Go to the directory where the downloaded installer is located, double-click on it to install CUDA Toolkit as instructed, and restart the GPU instance as required.
If the dialog box shown in the following figure appears, CUDA Toolkit has been installed.
![](https://main.qcloudimg.com/raw/ae1ac03436a89fcb0ecb09842e9d0a68.png)



