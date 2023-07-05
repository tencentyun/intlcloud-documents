## Overview
The GPU instance must be installed with the necessary infrastructure software in advance. For an NVIDIA GPU instance, the following software packages are required:
- Hardware driver for the GPU
- Libraries required by upper-level applications

To use NVIDIA GPU instances for general computing tasks, you must install Tesla driver and Compute Unified Device Architecture (CUDA) driver. This document only describes how to install a Tesla driver. For more information on CUDA driver, please see [Installing CUDA Driver](https://intl.cloud.tencent.com/document/product/560/8064).

## Directions
### Installing an NVIDIA Tesla driver on a Linux instance
You can use the Shell script to install a driver on the Linux instance. This method is applicable to all Linux distributions, including CentOS and Ubuntu.

When installing an NVIDIA Tesla driver for Linux, the driver needs to compile the kernel module. You must install gcc and packages required to compile the Linux kernel module in advance, such as `kernel-devel-$(uname -r)`.

1. Run the following command to check whether dkms has been installed in the operating system:
```
rpm -qa | grep -i dkms
```
If the returned result is as shown in the following figure, dkms has been installed.
![](https://main.qcloudimg.com/raw/ada786e81334e5a88f8c95e54ff42f18.png)
If dkms is not installed, run the following command to install dkms:
```
sudo yum install -y dkms
```
2. Go to [NVIDIA Driver Downloads](http://www.nvidia.com/Download/Find.aspx) or visit `http://www.nvidia.com/Download/Find.aspx`.
3. Configure the GPU type and operating system, and click **SEARCH** to search for the driver you need to download, as shown in the following figure. Below uses Tesla V100 as an example.
>!You can configure **Operating System** as **Linux 64-bit** to download shell setup files. If you configure **Operating System** to a specific Linux distribution, the corresponding installation files will be downloaded.
>
![](https://main.qcloudimg.com/raw/296039c584039388c7988c22fb0227a4.png)
4. Select the required version to go to the driver download page, and click **DOWNLOAD**, as shown in the following figure.
![](https://main.qcloudimg.com/raw/2d933595a3a21e89f64a6463b14f3bd3.png)
5. <span id="Step5"></span>You can skip the page for entering personal information. If the following page appears, right-click **AGREE & DOWNLOAD** and select **Copy link address**.
![](https://main.qcloudimg.com/raw/1b1831cd9e2a3530a99195e9005b5da7.png)
6. To log in to GPU instances, see [Log into Linux Instance Using Standard Login Method](https://intl.cloud.tencent.com/document/product/213/5436). You can also use other login methods:
	- [Logging into Linux instances via remote login tools](https://intl.cloud.tencent.com/document/product/213/32502)
	- [Logging into Linux instance via SSH key](https://intl.cloud.tencent.com/document/product/213/32501)
7. Run the `wget` command to download the installation package using the URL copied in [Step 5](#Step5), as shown in the following figure.
![](https://main.qcloudimg.com/raw/cbbb80409d43052061ba638d7ae622e5.png)
You can also download the installation package to your local computer and upload it to the GPU instance.
8. Add execution permissions to the installation package. For example, run the following command to add execution permissions to the `NVIDIA-Linux-x86_64-418.126.02.run` file:
```
chmod +x NVIDIA-Linux-x86_64-418.126.02.run
```
9. Run the following commands in sequence to check whether kernel-devel and gcc have been installed in the operating system:
```
rpm -qa | grep kernel-devel
```
```
rpm -qa | grep gcc
```
If the returned result is as shown in the following figure, kernel-devel and gcc have been installed.
![](https://main.qcloudimg.com/raw/0a9d385944669528d49544eb0bd6b8eb.png)
If kernel-devel and gcc are not installed, run the following command to install them:
```
sudo yum install -y gcc kernel-devel
```
>!If the kernel version has been upgraded, you must upgrade kernel-devel to the same version.
>
10. Run the following command to install the driver as instructed:
```
sudo sh NVIDIA-Linux-x86_64-418.126.02.run
```
11. After the installation is completed, run the following command to verify.
```
nvidia-smi
```
If GPU information similar to that shown in the following figure is returned, the installation is successful.
![](https://main.qcloudimg.com/raw/94cbceaa09720cd7edba76961f2763d8.png)



### Installing an NVIDIA Tesla driver on a Windows instance
1. To log in to GPU instances, see [Logging in to a Windows Instance Using the RDP File (Recommended)](https://intl.cloud.tencent.com/document/product/213/5435).
2. Go to [NVIDIA Driver Downloads](http://www.nvidia.com/Download/Find.aspx).
3. Configure the GPU type and operating system, and click **SEARCH** to search for the driver you need to download, as shown in the following figure. Below uses Tesla V100 as an example.
![](https://main.qcloudimg.com/raw/222b7f9fa96b269a9c6c0b6b5781d048.png)
4. Go to the directory where the downloaded installation package is located, double-click on it to install the driver as instructed, and restart the GPU instance as required.
After the installation is completed, go to **Device Manager** to check whether the GPU works properly.


## Reasons for installation failures
If nvidia-smi does not run properly, the driver has not been installed correctly. Common reasons include:
1. The operating system does not have the required packages installed for compiling the kernel module, such as gcc and kernel-devel.
2. The operating system has kernels in multiple versions. Due to incorrect DKMS configuration, the driver compiles a kernel module that is not in the version of the current kernel, causing kernel module installation to fail.
3. After the driver is installed, kernel version upgrade causes the original installation to fail.
