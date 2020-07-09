CUDA (Compute Unified Device Architecture) is a computing platform published by the graphic card vendor NVIDIA. As a generic parallel computing architecture, CUDA™ allows GPUs to solve complex computing problems. It contains CUDA instruction set architecture (ISA) and parallel computing engine within the GPU. Now, developers can write programs for CUDA ™ architecture using C, C++. These programs can be run with great performance on processors that support CUDA™.
GPU instances use NVIDIA graphic cards and you need to install CUDA development operating environment for them. As the most frequently used one, CUDA 7.5 can be installed by following the steps below.

## Installing on Linux
1. Click to [download CUDA driver](https://developer.nvidia.com/cuda-75-downloads-archive) or copy the link `https://developer.nvidia.com/cuda-75-downloads-archive`.
2. Select the operating system and installation package. We choose  CentOS 7.2 (64 bit) in this example.
![](https://mc.qcloudimg.com/static/img/a69a79a2d6cbd1f442b58bfb423d8cca/image.jpg)
>
>- **Installer Type**: it is recommended to choose **rpm (network)**.
>- **network**: network installer package. The package is small, and you need to download the actual installer package in the server via private network.
>- **local**: local installation package. The package is large because it contains the installation packages for all downloaded installation components.
>
3. Right click **Download** -> **Copy Link Address**.
![](https://mc.qcloudimg.com/static/img/3a2552b7e1637055bae0a1391520713b/image.png)
4. [Log in to a Linux instance using WebShell (recommended)](https://intl.cloud.tencent.com/document/product/213/5436). You can also use other login methods that you are comfortable with:
 - [Log in to a Linux instance using remote login software](https://intl.cloud.tencent.com/document/product/213/32502).
 - [Log in to a Linux instance using SSH](https://intl.cloud.tencent.com/document/product/213/32501)
5. Use `wget` command and paste the link address copied in the previous step to download the installer package. Or, you can download the CUDA installer package to a local system, and upload it to the GPU instance.
![](https://mc.qcloudimg.com/static/img/e40ed1109aaed75d51b3781fe0045eb6/image.png)
5. Run the following commands in the directory where the CUDA installer package is located:
```
sudo rpm -i cuda-repo-rhel7-7.5-18.x86_64.rpm
```
```
sudo yum clean all
```
```
sudo yum install cuda
```
6. Go to the` /usr/local/cuda-7.5/samples/1_Utilities/deviceQuery ` directory and execute `make` command to compile the `deviceQuery` program.
7. Execute `deviceQuery`. The CUDA installation is successful if the following device information is displayed.
![](https://mc.qcloudimg.com/static/img/d545951dc869591d83bf23e27831287a/image.jpg)

## Installing on Windows
To install CUDA on Windows instance, use the remote desktop to log in to your Windows instance as admin.
1. Download the CUDA installer package from [CUDA Driver Official Website](https://developer.nvidia.com/cuda-75-downloads-archive).
2. Select the OS and installer. In this example, we choose Win Server 2012 R2 (64 bit).
![](https://mc.qcloudimg.com/static/img/ecf81426ceb95fd4ed549cf0bc627895/image.jpg)
![](https://mc.qcloudimg.com/static/img/525b743130bda690a7223cbd5533ec75/image.jpg)
3. Launch the installation program and proceed according to the instructions. Installation is successful when you see the final dialog indicating the end of the process.
![](https://mc.qcloudimg.com/static/img/52aef97b2d048f884c467d8446fed003/image.jpg)
