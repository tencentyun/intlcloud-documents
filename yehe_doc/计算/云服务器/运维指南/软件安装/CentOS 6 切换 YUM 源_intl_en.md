## Overview
The CentOS 6 is an end-of-life (EOL) operating system since November 30, 2020, and no longer maintained by the Linux community. Therefore, the CentOS 6 source is unavailable in `http://mirror.centos.org/centos-6/`, a third-party image site, or Tencent Cloud at `http://mirrors.tencent.com/` and `http://mirrors.tencentyun.com/`. If you continue to use the default CentOS 6 source configured in Tencent Cloud, an error may occur.

<dx-alert infotype="explain" title="">
Upgrading your operating system to CentOS 7 or a later version is recommended. If you still need to use the CentOS 6 dependencies during the transition period, switch the CentOS 6 source as instructed below.
</dx-alert>


## Directions
1. Log in to the Linux instance. [Logging in via Web Shell is recommended.](https://intl.cloud.tencent.com/document/product/213/5436). You can also use other login methods as required.
	- [Logging In to Linux Instances (Remote Login)](https://intl.cloud.tencent.com/document/product/213/32502)
	- [Logging In to Linux Instance (SSH Key)](https://intl.cloud.tencent.com/document/product/213/32501)
2. Run the following command to check the CentOS version of the current operating system.
```shellsession
cat /etc/centos-release
```
If the result as shown in the following figure is returned, the operating system version is CentOS 6.9.
![](https://main.qcloudimg.com/raw/de65529a43dc5bfee695c08d5f7bff80.png)
3. Run the following command to edit the `CentOS-Base.repo` file.
```shellsession
vim /etc/yum.repos.d/CentOS-Base.repo 
```
4. Press **i** to enter edit mode and modify `baseurl` according to the CentOS version and network environment.
<dx-alert infotype="explain" title="">
See [Private Network Access](https://intl.cloud.tencent.com/document/product/213/5225) and [Internet Access](https://intl.cloud.tencent.com/document/product/213/5224) to determine the required source:
- Source for private network access: `http://mirrors.tencentyun.com/centos-vault/6.x/`
- Source for public network access: `http://mirrors.tencent.com/centos-vault/6.x/`
</dx-alert>
This document uses CentOS 6.9 that requires a private network access as an example. The modified <code>CentOS-Base.repo</code> file is as follows:
<img src="https://main.qcloudimg.com/raw/1d2485a9be0df6d5f7c46151fc50d73b.png"/>
You can configure as follows:
```plaintext
[extras]
gpgcheck=1
gpgkey=http://mirrors.tencentyun.com/centos/RPM-GPG-KEY-CentOS-6
enabled=1
baseurl=http://mirrors.tencentyun.com/centos-vault/6.9/extras/$basearch/
name=Qcloud centos extras - $basearch
[os]
gpgcheck=1
gpgkey=http://mirrors.tencentyun.com/centos/RPM-GPG-KEY-CentOS-6
enabled=1
baseurl=http://mirrors.tencentyun.com/centos-vault/6.9/os/$basearch/
name=Qcloud centos os - $basearch
[updates]
gpgcheck=1
gpgkey=http://mirrors.tencentyun.com/centos/RPM-GPG-KEY-CentOS-6
enabled=1
baseurl=http://mirrors.tencentyun.com/centos-vault/6.9/updates/$basearch/
name=Qcloud centos updates - $basearch
```
5. Press **ESC**, enter **:wq**, and press **Enter** to save the modification.
6. Run the following command to modify the `CentOS-Epel.repo` file.
```shellsession
vim /etc/yum.repos.d/CentOS-Epel.repo 
```
7. Press **i** to enter edit mode and modify `baseurl` based on the network environment.
In this example, change `baseurl=http://mirrors.tencentyun.com/epel/$releasever/$basearch/` to `baseurl=http://mirrors.tencentyun.com/epel-archive/6/$basearch/`. The result is as follows:
![](https://main.qcloudimg.com/raw/9c4b3eaf65d005b3d6819f013037443d.png)
You can configure as follows:
```plaintext
[epel]
name=epel for redhat/centos $releasever - $basearch
failovermethod=priority
gpgcheck=1
gpgkey=http://mirrors.tencentyun.com/epel/RPM-GPG-KEY-EPEL-6
enabled=1
baseurl=http://mirrors.tencentyun.com/epel-archive/6/$basearch/
```
8. Press **ESC**, enter **:wq**, and press **Enter** to save the modification.
9. Now you can use the `yum install` command to install the required software.


