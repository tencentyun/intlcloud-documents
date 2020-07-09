To ensure the proper working of GPU instances, we need to install required infrastructure software. For NVIDIA series GPU, there are two software packages to be installed:
- Hardware driver for the GPU
- Libraries required by upper-level applications

If the NVIDIA GPU instance is used for general purpose, we need to install Tesla Driver and CUDA. In this document, we only introduce how to install Tesla Driver. To learn about how to install CUDA, please refer to [Installing CUDA Driver](https://intl.cloud.tencent.com/document/product/560/8064).

## Installing the Driver in Linux System
You can install the driver in two ways: 
- Install the driver using Shell script. It works with all Linux distributions, including CentOS and Ubuntu.
- Install the driver using packages. It works with various Linux distributions, such as the installation using DEB and RPM.

Regardless of the installation method, the Linux driver of NVIDIA Telsa GPU needs to compile the kernel module during the installation process, so the system is required to install GCC and the package which the compiling of Linux kernel module depends on, such as `kernel-devel-$(uname -r)`.

### Installing the driver using Shell script
1. Click to [download NVIDIA driver](http://www.nvidia.com/Download/Find.aspx) or open the link `http://www.nvidia.com/Download/Find.aspx`.
2. Choose the OS and installing package. In this example, we will choose P40.
![](https://main.qcloudimg.com/raw/42f815083c1ee87a98a13595c69bd496.png)
>If **Linux 64-bit** is selected for the **Operating System**, the shell installation file will be downloaded. If a specific distribution is selected, the corresponding package installation file will be downloaded.
3. You will be directed to the page of selected version. Click **DOWNLOAD**.
![](https://main.qcloudimg.com/raw/95ada99ab6bcc84decfef4caf1905f62.png)
4. After re-direction, skip the page that requires personal information if appears. When the following page appears, right click on **AGREE&DOWNLOAD** and copy the link address in the context menu.
![](https://main.qcloudimg.com/raw/e343c0276071797f3bc1051e430758f5.png)
4. [Log in to a Linux instance using WebShell (recommended)](https://intl.cloud.tencent.com/document/product/213/5436). You can also use other login methods that you are comfortable with:
 - [Log in to a Linux instance using remote login software](https://intl.cloud.tencent.com/document/product/213/32502).
 - [Log in to a Linux instance using SSH](https://intl.cloud.tencent.com/document/product/213/32501)
5. Log in to the GPU instance, execute `wget` command and paste the link address copied in the previous step to download the installer. Or, you can download the NVIDIA installer package to a local system, and upload it to the GPU instance server.
![](https://main.qcloudimg.com/raw/e8648c2802a0c31bf557b056ce084911.png)
Then you can run `ls` to check the name of the downloaded installation package. 
6. For example, add the execution permission to the file named `NVIDIA-Linux-x86_64-396.44.run`:
```
chmod +x NVIDIA-Linux-x86_64-396.44.run
```
7. Install the corresponding gcc and kernel-devel packages for the current system.
```
sudo yum install -y gcc kernel-devel-xxx
```
`xxx` is the kernel version number, which can be checked by using `uname -r`.
8. Follow the prompts after running the driver installer.
```
sudo /bin/bash ./NVIDIA-Linux-x86_64-396.44.run
```
9. After the installation, run `nvidia-smi`. The driver installation is successful if you see GPU information displayed (similar to what is shown below).
![](https://main.qcloudimg.com/raw/b5877169c7012d20e7de02754d43cedc.png)

### Installing the driver using DEB/RPM
#### Installing the driver using DEB
1. Click to [download NVIDIA driver](http://www.nvidia.com/Download/Find.aspx) or open the link `http://www.nvidia.com/Download/Find.aspx`.
2. Select the corresponding operating system that supports DEB, such as Ubuntu 16.04, and get the download link: `wget http://us.download.nvidia.com/tesla/396.44/nvidia-diag-driver-local-repo-ubuntu1604-396.44_1.0-1_amd64.deb`.
3. Run the command to install the package.
```
dpkg -i nvidia-diag-driver-local-repo-ubuntu1604-396.44_1.0-1_amd64.deb
```
4. Run `apt-get update` to update the software package.
```
apt-get update
```
5. Run the following command to install the driver.
```
apt-get install cuda-drivers
```
6. Run `reboot` to restart.
7. Run `nvidia-smi`. If the correct information is output, the driver is installed successfully.

#### Installing the driver using RPM
1. Click to [download NVIDIA driver](http://www.nvidia.com/Download/Find.aspx) or open the link `http://www.nvidia.com/Download/Find.aspx`.
2. Select an OS that supports RPM package and obtain the download link of the RPM package. In this example, we choose `CentOS 7.x`.
`wget http://us.download.nvidia.com/tesla/396.44/nvidia-diag-driver-local-repo-rhel7-396.44-1.0-1.x86_64.rpm`
3. Run `rpm` command to install the RPM package.
```
rpm -i nvidia-diag-driver-local-repo-rhel7-396.44-1.0-1.x86_64.rpm
```
4. Run `yum` to clear the cache.
```
yum clean all
```
5. Run `yum` to install the driver.
```
yum install cuda-drivers
```
6. Run `reboot` to restart.
7. Run `nvidia-smi`. If the correct information is output, the driver is installed successfully.

## Installing the Driver in Windows System
1. Log in to the [Official Website for NVIDIA Driver Downloads](http://www.nvidia.com/Download/Find.aspx).
2. Select the OS and installation package. In this example, we will use **M40**.
![](https://mc.qcloudimg.com/static/img/ba82ef3631369d12b995b6cb2a94b14c/image.png)
3. Open the folder where the driver is stored and double click to start it. Follow the instructions to install the driver and restart the instance as required. You can check whether the GPU is working properly in the Device Management.

## Common Installation Failures
nvidia-smi does not work if the driver is not installed correctly. Common reasons include: 
1. The required packages for the kernel module compiling are missing, such as gcc, kernel-devel-xxx, etc.
2. There are multiple versions of the kernel in the system, and the DKMS cannot be configured correctly. The driver is compiled into a kernel module that is not the current version of the kernel, resulting in the failure of kernel module installation.
3. After the driver is installed, the original installation becomes invalid due to the upgrade of the kernel version.
