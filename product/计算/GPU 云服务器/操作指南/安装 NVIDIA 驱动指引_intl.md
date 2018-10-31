The proper infrastructure software needs to be installed for GPU instance to work properly. For NVIDIA series GPU, there are two software packages to be installed:
1. Hardware driver that drives GPU to work.
2. Libraries required by upper-level applications.

If NVIDIA GPU is used for general computing, Tesla Driver and CUDA need to be installed. This document only describes how to install Tesla Driver.

For the convenience of users, users can select to pre-install a specific version of the driver and the image of CUDA in the image marketplace when creating the GPU instance.

## Installing the Driver in Linux System
There are two ways to install the driver in Linux system:
1. Install the driver using Shell script. It works with all Linux distributions, including CentOS and Ubuntu.
2. Install the driver using packages. It works with various Linux distributions, such as the installation using DEB and RPM.

Regardless of the installation method, the Linux driver of NVIDIA Telsa GPU needs to compile the kernel module during the installation process, so the system is required to install gcc and the package which the compiling of Linux kernel module depends on, such as kernel-devel-$(uname -r).

### Installing the driver using Shell script
1. Log in to [Download NVIDIA Driver](http://www.nvidia.com/Download/Find.aspx) or open the link http://www.nvidia.com/Download/Find.aspx .

2. Select an operating system and an installer package. Take P40 as an example, search for the driver and select the version of the driver to download.
![](https://main.qcloudimg.com/raw/42f815083c1ee87a98a13595c69bd496.png)
> **Note:**
If "Linux 64-bit" is selected for the "Operating System", the shell installation file will be downloaded. If a specific distribution is selected, the corresponding package installation file will be downloaded.

3. After jumping to the page of selected version, click **DOWNLOAD**.
![](https://main.qcloudimg.com/raw/95ada99ab6bcc84decfef4caf1905f62.png)

4. After jumping again, if there is a page that requires personal information, you can skip it directly. When the following page appears, right click on **AGREE&DOWNLOAD** and copy the link address in the context menu.
![](https://main.qcloudimg.com/raw/e343c0276071797f3bc1051e430758f5.png)

5. Log in to the GPU instance, and paste the link address copied in the previous step to download the installer package by executing `wget` command. Or, you can download the NVIDIA installer package to a local system, and upload it to the GPU instance server.
![](https://main.qcloudimg.com/raw/e8648c2802a0c31bf557b056ce084911.png)

6. Add the execution permission to the installer package. For example, add the execution permission to the file named `NVIDIA-Linux-x86_64-396.44.run`:
```
chmod +x NVIDIA-Linux-x86_64-396.44.run
```

7. Install the corresponding gcc and kernel-devel packages for the current system.
```
sudo yum install -y gcc kernel-devel-xxx
```
`xxx` is the kernel version number, which can be viewed by using `uname -r`.

8. Follow the prompts after running the driver installer.
```
sudo /bin/bash ./NVIDIA-Linux-x86_64-396.44.run
```

9. Once the installation is finished, run `nvidia-smi`. The driver installation is successful if you see GPU information displayed (similar to what is shown below).
![](https://main.qcloudimg.com/raw/b5877169c7012d20e7de02754d43cedc.png)

### Installing the driver using DEB/RPM
#### Installing the driver using DEB
1. Log in to [Download NVIDIA Driver](http://www.nvidia.com/Download/Find.aspx) or open the link http://www.nvidia.com/Download/Find.aspx.
2. Select the corresponding operating system that supports DEB, such as Ubuntu 16.04, and get the download link: `wget http://us.download.nvidia.com/tesla/396.44/nvidia-diag-driver-local-repo-ubuntu1604-396.44_1.0-1_amd64.deb`.
3. Run the command to install the package. 
```
dpkg -i nvidia-diag-driver-local-repo-ubuntu1604-396.44_1.0-1_amd64.deb
```
4. Update the software package with the `apt-get` command. 
```
apt-get update
```
5. Run the `apt-get` command to install the driver. 
```
apt-get install cuda-drivers
```
6. Run the `reboot` command to restart. 
7. If the correct information can be output when running `nvidia-smi`, the driver is installed successfully. 
 
#### Installing the driver using RPM
1. Log in to [Download NVIDIA Driver](http://www.nvidia.com/Download/Find.aspx) or open the link http://www.nvidia.com/Download/Find.aspx.
2. Select the corresponding operating system that supports RPM package, such as rhel 7.x. Get the download link: `wget http://us.download.nvidia.com/tesla/396.44/nvidia-diag-driver-local-repo-rhel7-396.44-1.0-1.x86_64.rpm`
3. Install the RPM package using the `rpm` command. 
```
rpm -i nvidia-diag-driver-local-repo-rhel7-396.44-1.0-1.x86_64.rpm
```
4. Clear the cache using the `yum` command. 
 ```
 yum clean all
 ```
5. Install the driver using the `yum` command. 
```
yum install cuda-drivers
```
6. Run the `reboot` command to restart.
7. If the correct information can be output when running `nvidia-smi`, the driver is installed successfully.

## Installing the Driver in Windows System
1. Log in to the [Official Website for NVIDIA Driver Downloads](http://www.nvidia.com/Download/Find.aspx).
2. Select an operating system and an installer package. Suppose we use M40, we select the following driver:
![](//mc.qcloudimg.com/static/img/ba82ef3631369d12b995b6cb2a94b14c/image.png)
3. Open the folder where the downloaded driver is located and double click the installation file to launch the installation program. Install the driver according to instructions and restart your instance when required. Check the Device Manager to verify whether the GPU is functioning normally.

## Reason for installation failure
The failure of Linux system driver installation is reflected in the fact that nvidia-smi does not work. There are several common reasons for failure:
1. The system lacks the packages needed to compile the kernel module, such as gcc, kernel-devel-xxx, etc., resulting in failure to compile and install.
2. There are multiple versions of the kernel in the system. Due to the incorrect configuration of DKMS, the driver is compiled into a kernel module that is not the current version of the kernel, resulting in the failure of kernel module installation.
3. After the driver is installed, the original installation becomes invalid due to the upgrade of the kernel version.
