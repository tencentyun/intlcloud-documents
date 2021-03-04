## Background
CentOS 6 reached end-of-life (EOL) on November 30, 2020, and is no longer maintained by the Linux community. Therefore, the CentOS 6 source is unavailable in `http://mirror.centos.org/centos-6/` and third-party image sites. Tencent Cloud sites, `http://mirrors.cloud.tencent.com/` and `http://mirrors.tencentyun.com/`, cannot obtain CentOS 6 source. If you continue to use the default CentOS 6 source configured in Tencent Cloud, an error may occur.



>? Upgrading your operating system to CentOS 7 or a later version is recommended. If you still need to use the CentOS 6 dependencies, switch the CentOS 6 source as instructed below.



## Directions
1. Log in to a Linux instance using Web Shell (See [documentation](https://intl.cloud.tencent.com/document/product/213/5436). You can also use other login methods that you are more comfortable with:
	- [Log in to Linux Instances via Remote Login Tools](https://intl.cloud.tencent.com/document/product/213/32502)
	- [Log in to Linux Instance via SSH Key](https://intl.cloud.tencent.com/document/product/213/32501)
2. Run the following command to check the CentOS version of the current operating system.
```
cat /etc/centos-release
```
As shown in the following figure, the operating system version is CentOS 6.9.
![](https://main.qcloudimg.com/raw/de65529a43dc5bfee695c08d5f7bff80.png)
3. Run the following command to edit the `CentOS-Base.repo` file.
```
vim /etc/yum.repos.d/CentOS-Base.repo 
```
4. Press **i** to enter edit mode and modify `baseurl` according to the CentOS version and network environment.
>?
>Determine the source required for your instance as instructed in [Private Network Access](https://intl.cloud.tencent.com/document/product/213/5225) and [Internet Access](https://intl.cloud.tencent.com/document/product/213/5224) 
>
>- Source for private network access: `http://mirrors.tencentyun.com/centos-vault/6.x/`
>- Source for public network access: `https://mirrors.cloud.tencent.com/centos-vault/6.x/`

This document uses a CentOS 6.9-based instance that requires private network access as an example. The modified <code>CentOS-Base.repo</code> file is as follows:
<img src="https://main.qcloudimg.com/raw/1d2485a9be0df6d5f7c46151fc50d73b.png"/>
5. Press **ESC**, enter **:wq**, and press **Enter** to save the modification.
6. Run the following command to modify the `CentOS-Epel.repo` file.
```
vim /etc/yum.repos.d/CentOS-Epel.repo 
```
7. Press **i** to enter edit mode and modify `baseurl` based on the network environment.
In this example, change `baseurl=http://mirrors.tencentyun.com/epel/$releasever/$basearch/` to `baseurl=http://mirrors.tencentyun.com/epel-archive/6/$basearch/`. The result should be as follows:
![](https://main.qcloudimg.com/raw/9c4b3eaf65d005b3d6819f013037443d.png)
8. Press **ESC**, enter **:wq**, and press **Enter** to save the modification.
9. Now you can use the `yum install` command to install the required software.
