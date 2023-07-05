
## Overview

This document describes how to install the cloud-init service. Cloud-init allows you to customize configurations during the first initialization of an instance.
Options to install cloud-init:
- [Download the cloud-init binary package](#binary)
- [Download the cloud-init source package](#ManualDown) 
- [Use the cloud-init package from the software source](#SoftSources)


## Prerequisites
Connect the server that you want to install cloud-init to the public network.

## How It Works
<dx-tabs>
::: Download the cloud-init binary package[](id:binary)
<dx-alert infotype="explain" title="">
- cloud-init depends on qcloud-python, which is a software package recompiled by Tencent Cloud. qcloud-python is a separate python environment and is only used for cloud-init. It is installed under the directory of `/usr/local/qcloud/python`, and it does not conflict with the default python in the system.
- cloud-init is developed by Tencent Cloud based on the community v20.1. It is adapted to Tencent Cloud operation environment.
- The cloud-init binary package supports the following operating systems:
</dx-alert>
<table>
<thead>
  <tr>
    <th rowspan="2">Type</th>
    <th rowspan="2">OS</th>
    <th rowspan="2">Version</th>
    <th colspan="2" style="text-align:center">x86_64</th>
    <th colspan="2" style="text-align:center">arm64</th>
  </tr>
  <tr>
    <th>qcloud-python</th>
    <th>cloud-init</th>
    <th>qcloud-python</th>
    <th>cloud-init</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td rowspan="5">rpm</td>
    <td rowspan="2">CentOS</td>
    <td>7</td>
    <td><a href="https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/packages/centos7.6/qcloud-python-3.7.10-1.el7.x86_64.rpm">qcloud-python-3.7.10-1.el7.x86_64.rpm</a></td>
    <td><a href="https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/packages/centos7.6/cloud-init-20.1.0011-1.el7.x86_64.rpm">cloud-init-20.1.0011-1.el7.x86_64.rpm</a></td>
    <td><a href="https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/packages/centos7.4/aarch64/qcloud-python-3.7.10-1.el7.centos.aarch64.rpm">qcloud-python-3.7.10-1.el7.centos.aarch64.rpm</a></td>
    <td><a href="https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/packages/centos7.4/aarch64/cloud-init-20.1.0011-3.el7.centos.aarch64.rpm">cloud-init-20.1.0011-3.el7.centos.aarch64.rpm</a></td>
  </tr>
  <tr>
    <td>8</td>
    <td><a href="https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/packages/centos8.2/x86_64/qcloud-python-3.7.10-1.el8.x86_64.rpm">qcloud-python-3.7.10-1.el8.x86_64.rpm</a></td>
    <td><a href="https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/packages/centos8.2/x86_64/cloud-init-20.1.0011-1.el8.x86_64.rpm">cloud-init-20.1.0011-1.el8.x86_64.rpm</a></td>
    <td><a href="https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/packages/centos8.2/aarch64/qcloud-python-3.7.10-1.el8.aarch64.rpm">qcloud-python-3.7.10-1.el8.aarch64.rpm</a></td>
    <td><a href="https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/packages/centos8.2/aarch64/cloud-init-20.1.0011-3.el8.aarch64.rpm">cloud-init-20.1.0011-3.el8.aarch64.rpm</a></td>
  </tr>
  <tr>
    <td>Fedora</td>
    <td>36</td>
    <td><a href="https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/packages/fedora36/qcloud-python-3.7.10-2.fc36.x86_64.rpm">qcloud-python-3.7.10-2.fc36.x86_64.rpm</a></td>
    <td><a href="https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/packages/ubuntu20.04/cloud-init_20.1.0011-1_arm64.deb">cloud-init_20.1.0011-1_arm64.deb</a></td>
    <td>N/A</td>
    <td>N/A</td>
  </tr>
  <tr>
    <td>Kylin</td>
    <td>20sp1</td>
    <td><a href="https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/packages/kylin10sp1/x86_64/qcloud-python-3.7.10-1.ky10.x86_64.rpm">qcloud-python-3.7.10-1.ky10.x86_64.rpm</a></td>
    <td><a href="https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/packages/kylin10sp1/x86_64/cloud-init-20.1.0011-2.ky10.x86_64.rpm">cloud-init-20.1.0011-2.ky10.x86_64.rpm</a></td>
    <td><a href="https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/packages/kylin10sp1/aarch64/qcloud-python-3.7.10-1.ky10.aarch64.rpm">qcloud-python-3.7.10-1.ky10.aarch64.rpm</a></td>
    <td><a href="https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/packages/kylin10sp1/aarch64/cloud-init-20.1.0011-1.ky10.aarch64.rpm">cloud-init-20.1.0011-1.ky10.aarch64.rpm</a></td>
  </tr>
  <tr>
    <td>openSUSE</td>
    <td>15.4</td>
    <td><a href="https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/packages/opensuse15.4/qcloud-python-3.7.10-2.x86_64.rpm">qcloud-python-3.7.10-2.x86_64.rpm</a></td>
    <td><a href="https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/packages/opensuse15.4/cloud-init-20.1.0011-2.x86_64.rpm">cloud-init-20.1.0011-2.x86_64.rpm</a></td>
    <td>N/A</td>
    <td>N/A</td>
  </tr>
  <tr>
    <td rowspan="8">deb</td>
    <td rowspan="4">Debian</td>
    <td>11</td>
    <td><a href="https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/packages/debian11/qcloud-python_3.7.10-1_amd64.deb">qcloud-python_3.7.10-1_amd64.deb</a></td>
    <td><a href="https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/packages/debian11/cloud-init_20.1.0011-1_amd64.deb">cloud-init_20.1.0011-1_amd64.deb</a></td>
    <td><a href="https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/packages/debian11/aarch64/qcloud-python_3.7.10-1_arm64.deb">qcloud-python_3.7.10-1_arm64.deb</a></td>
    <td><a href="https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/packages/debian11/aarch64/cloud-init_20.1.0011-1_arm64.deb">cloud-init_20.1.0011-1_arm64.deb</a></td>
  </tr>
  <tr>
    <td>10</td>
    <td><a href="https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/packages/debian10/qcloud-python_3.7.10-1_amd64.deb">qcloud-python_3.7.10-1_amd64.deb</a></td>
    <td><a href="https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/packages/debian10/cloud-init_20.1.0011-1_amd64.deb">cloud-init_20.1.0011-1_amd64.deb</a></td>
    <td>N/A</td>
    <td>N/A</td>
  </tr>
  <tr>
    <td>9</td>
    <td><a href="https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/packages/debian9/qcloud-python_3.7.10-1_amd64.deb">qcloud-python_3.7.10-1_amd64.deb</a></td>
    <td><a href="https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/packages/debian9/cloud-init_20.1.0011-1_amd64.deb">cloud-init_20.1.0011-1_amd64.deb</a></td>
    <td>N/A</td>
    <td>N/A</td>
  </tr>
  <tr>
    <td>8</td>
    <td><a href="https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/packages/debian8/qcloud-python_3.7.10-1_amd64.deb">qcloud-python_3.7.10-1_amd64.deb</a></td>
    <td><a href="https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/packages/debian8/cloud-init_20.1.0011-1_amd64.deb">cloud-init_20.1.0011-1_amd64.deb</a></td>
    <td>N/A</td>
    <td>N/A</td>
  </tr>
  <tr>
    <td rowspan="4">Ubuntu</td>
    <td>22.04</td>
    <td><a href="https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/packages/ubuntu22.04/qcloud-python_3.7.10-1_amd64.deb">qcloud-python_3.7.10-1_amd64.deb</a></td>
    <td><a href="https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/packages/ubuntu22.04/cloud-init_20.1.0011-1_amd64.deb">cloud-init_20.1.0011-1_amd64.deb</a></td>
    <td>N/A</td>
    <td>N/A</td>
  </tr>
  <tr>
    <td>20.04</td>
    <td><a href="https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/packages/ubuntu20.04/x86_64/qcloud-python_3.7.10-1_amd64.deb">qcloud-python_3.7.10-1_amd64.deb</a></td>
    <td><a href="https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/packages/ubuntu20.04/x86_64/cloud-init_20.1.0011-1_amd64.deb">cloud-init_20.1.0011-1_amd64.deb</a></td>
    <td><a href="https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/packages/ubuntu20.04/qcloud-python_3.7.10-1_arm64.deb">qcloud-python_3.7.10-1_arm64.deb</a></td>
    <td><a href="https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/packages/ubuntu20.04/cloud-init_20.1.0011-1_arm64.deb">cloud-init_20.1.0011-1_arm64.deb</a></td>
  </tr>
  <tr>
    <td>18.04</td>
    <td><a href="https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/packages/ubuntu18.04/x86_64/qcloud-python_3.7.10-1%2Bubuntu18.04_amd64.deb">qcloud-python_3.7.10-1%2Bubuntu18.04_amd64.deb</a></td>
    <td><a href="https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/packages/ubuntu18.04/x86_64/cloud-init_20.1.0011-1%2Bubuntu18.04_amd64.deb">cloud-init_20.1.0011-1%2Bubuntu18.04_amd64.deb</a></td>
    <td><a href="https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/packages/ubuntu18.04/aarch64/qcloud-python_3.7.10-1_arm64.deb">qcloud-python_3.7.10-1_arm64.deb</a></td>
    <td><a href="https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/packages/ubuntu18.04/aarch64/cloud-init_20.1.0011-1_arm64.deb">cloud-init_20.1.0011-1_arm64.deb</a></td>
  </tr>
  <tr>
    <td>16.04</td>
    <td><a href="https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/packages/ubuntu16.04/qcloud-python_3.7.10-1_amd64.deb">qcloud-python_3.7.10-1_amd64.deb</a></td>
    <td><a href="https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/packages/ubuntu16.04/cloud-init_20.1.0011-1_amd64.deb">cloud-init_20.1.0011-1_amd64.deb</a></td>
    <td>N/A</td>
    <td>N/A</td>
  </tr>
</tbody>
</table>

### Downloading cloud-init binary package[](id:binary)
1. Download the installation package.

2. If cloud-init already exists, run the following command to clear it.
```shellsession
rm -rf /var/lib/cloud
rm -rf /etc/cloud
rm -rf /usr/local/bin/cloud*
```
3. Run the following commands based on the OS.
  - For deb type, run the following command.
  ```shellsession
  dpkg -i *.deb
  ```
 - For rpm type, run the following command.
 ```shellsession
 rpm -ivh *.rpm
 ```
4. Check whether the version is installed properly.
  ```shellsession
cloud-init qcloud -v
/usr/bin/cloud-init qcloud 0011
  ```
5. Restart.
:::
::: Manual download[](id:ManualDown)

### Downloading the cloud-init source package

<dx-alert infotype="explain" title="">
- The cloud-init-20.1.0011 version is most compatible with Tencent Cloud. It ensures that all configuration items of CVMs created through the image can be initialized properly. We recommend that you install **cloud-init-20.1.0011.tar.gz**. You can also [click here](https://launchpad.net/cloud-init/+download) to download other versions. This document uses cloud-init-20.1.0011 as an example.
</dx-alert>


Run the following command to download the cloud-init source package:
```shellsession
wget https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/src/cloud-init-20.1.0011.tar.gz
```

### Installing cloud-init
1. Run the following command to decompress the cloud-init installation package.
<dx-alert infotype="explain" title="">
If you are using the Ubuntu operating system, run this command with the “root” account.
</dx-alert>
```shellsession
tar -zxvf cloud-init-20.1.0011.tar.gz 
```
2. Run the following command to enter the decompressed cloud-init installation package directory, that is, the cloud-init-20.1.0011 directory:
```shellsession
cd cloud-init
```
3. Install Python-pip according to the operating system version.
  - For CentOS 6/7, run the following command:
```shellsession
yum install python3-pip -y
```
  - For Ubuntu, run the following command:
```shellsession
apt-get -y install python3-pip
```
During installation, if an error such as “failed to install” or “installation package not found” occurs, see [resolving Python-pip installation failure](#updateSoftware) to troubleshoot it.
4. Run the following command to upgrade pip.
```
python3 -m pip install --upgrade pip
```
5. Run the following command to install dependencies.
<dx-alert infotype="notice" title="">
Python 2.6 is not supported when cloud-init uses requests 2.20.0 or later. If the Python interpreter installed in the image environment is Python version 2.6 or earlier, run the `pip install 'requests&lt;2.20.0'` command to install requests 2.20.0 or later before installing the cloud-init dependencies.
</dx-alert>
```shellsession
pip3 install -r requirements.txt
```

6. Install the cloud-utils components corresponding to your OS version.
  - For CentOS 6, run the following command:
```shellsession
yum install cloud-utils-growpart dracut-modules-growroot -y
dracut -f
```
  - For CentOS 7, run the following command:
```shellsession
yum install cloud-utils-growpart -y
```
  - For Ubuntu, run the following command:
```shellsession
apt-get install cloud-guest-utils -y
```

7. Run the following command to install cloud-init:
```shellsession
python3 setup.py build
```
```shellsession
python3 setup.py install --init-system systemd
```
<dx-alert infotype="notice" title="">
- The `--init-system` can be followed by any of `systemd`, `sysvinit`, `sysvinit_deb`, `sysvinit_freebsd`, `sysvinit_openrc`, `sysvinit_suse`, `upstart`, or `None` (default). Choose one according to the auto-start service management method of the operating system. Otherwise the cloud-init service cannot automatically start upon system startup.
- Select `sysvinit` for the CentOS 6 and earlier versions, and select `systemd` for CentOS 7 and later versions. This document uses systemd as an example.
</dx-alert>


[](id:cloud-init)
### Modifying the cloud-init configuration file

1. Download cloud.cfg for your operating system.
  - [Download cloud.cfg for Ubuntu](https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/cfg/ubuntu/cloud.cfg).
  - [Download cloud.cfg for CentOS](https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/cfg/centos/cloud.cfg).
2. Replace the content of `/etc/cloud/cloud.cfg` with that of the downloaded cloud.cfg file.


### Adding syslog user
Run the following command to add a syslog user:
```shellsession
useradd syslog
```


### Configuring the auto-start of the cloud-init service on boot
- **If your operating system uses the systemd auto-start service management method, run the following command.**
<dx-alert infotype="explain" title="">
To check whether the operating system uses systemd, run the `strings /sbin/init | grep "/lib/system"` command, and you will receive a return message.
</dx-alert>
- **Run the following command in Ubuntu or Debian.**
```shellsession
 ln -s /usr/local/bin/cloud-init /usr/bin/cloud-init 
```
- **Run the following commands in all operating systems.**
```shellsession
systemctl enable cloud-init-local.service 
systemctl start cloud-init-local.service
systemctl enable cloud-init.service
systemctl start cloud-init.service
systemctl enable cloud-config.service
systemctl start cloud-config.service
systemctl enable cloud-final.service
systemctl start cloud-final.service
systemctl status cloud-init-local.service
systemctl status cloud-init.service
systemctl status cloud-config.service
systemctl status cloud-final.service
```
- **Run the following commands in CentOS or Redhat.**
 Replace the content of `/lib/systemd/system/cloud-init-local.service` with the following:
```shellsession
[Unit]
Description=Initial cloud-init job (pre-networking)
Wants=network-pre.target
After=systemd-remount-fs.service
Before=NetworkManager.service
Before=network-pre.target
Before=shutdown.target
Conflicts=shutdown.target
RequiresMountsFor=/var/lib/cloud
[Service]
Type=oneshot
ExecStart=/usr/bin/cloud-init init --local
ExecStart=/bin/touch /run/cloud-init/network-config-ready
RemainAfterExit=yes
TimeoutSec=0
# Output needs to appear in instance console output
StandardOutput=journal+console
[Install]
WantedBy=cloud-init.target
```
Replace the content of `/lib/systemd/system/cloud-init.service` with the following:
```shellsession
[Unit]
Description=Initial cloud-init job (metadata service crawler)
Wants=cloud-init-local.service
Wants=sshd-keygen.service
Wants=sshd.service
After=cloud-init-local.service
After=systemd-networkd-wait-online.service
After=networking.service
After=systemd-hostnamed.service
Before=network-online.target
Before=sshd-keygen.service
Before=sshd.service
Before=systemd-user-sessions.service
Conflicts=shutdown.target
[Service]
Type=oneshot
ExecStart=/usr/bin/cloud-init init
RemainAfterExit=yes
TimeoutSec=0
# Output needs to appear in instance console output
StandardOutput=journal+console
[Install]
WantedBy=cloud-init.target
```
- **If your operating system uses the sysvinit auto-start service management method, run the following commands:**
<dx-alert infotype="explain" title="">
To check whether the operating system uses sysvinit, run the `strings /sbin/init | grep "sysvinit"` command, and you will receive a return message.
</dx-alert>
```shellsession
chkconfig --add cloud-init-local
chkconfig --add cloud-init
chkconfig --add cloud-config
chkconfig --add cloud-final
chkconfig cloud-init-local on 
chkconfig cloud-init on 
chkconfig cloud-config on 
chkconfig cloud-final on 
```
:::
::: Using software source[](id:SoftSources)
### Installing cloud-init

Run the following command to install cloud-init:
```shellsession
apt-get/yum install cloud-init
```
<dx-alert infotype="explain" title="">
By default, the cloud-init version installed by running `apt-get` or `yum` is the default cloud-init version in the software source configured for the operating system. Some configuration items of instances created by using the image whose cloud-init is installed this way may not be initialized as expected. Therefore, we recommend that you install the service by [manually downloading the cloud-init source package](#ManualDown).
</dx-alert>



### Modifying the cloud-init configuration file[](id:cloud-init)
1. Download cloud.cfg for your operating system.
 - [Download cloud.cfg for Ubuntu](https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/cfg/ubuntu/cloud.cfg).
  - [Download cloud.cfg for CentOS](https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/cfg/centos/cloud.cfg).
2. Replace the content of `/etc/cloud/cloud.cfg` with that of the downloaded cloud.cfg file.
:::
</dx-tabs>



## More


<dx-alert infotype="notice" title="">
Do not restart the server after performing the following operations. Otherwise, you will need to perform them again.
</dx-alert>


1. Run the following command to check whether the cloud-init configuration is successful.
```shellsession
cloud-init init --local
```
If the following information is returned, it indicates that the cloud-init has been successfully configured.
```shellsession
Cloud-init v. 20.1.0011 running 'init-local' at Fri, 01 Apr 2022 01:26:11 +0000. Up 38.70 seconds.
```
2. Run the following command to delete the cache records of cloud-init.
```shellsession
rm -rf /var/lib/cloud
```
3. Run the following command in Ubuntu or Debian.
```shellsession
rm -rf /etc/network/interfaces.d/50-cloud-init.cfg
```
4. For Ubuntu or Debian, modify the content of `/etc/network/interfaces` to the following:
```shellsession
# This file describes the network interfaces available on your system
# and how to activate them. For more information, see interfaces(5).
source /etc/network/interfaces.d/*
```

## Appendix
[](id:updateSoftware)
### Resolving Python-pip installation failure
During installation, if an error such as “failed to install” or “installation package not found” occurs, troubleshoot it based on the operating system as follows:
<dx-tabs>
::: CentOS 6/7:
  1. Run the following command to configure the EPEL storage repository.
```shellsession
yum install epel-release -y
```
  2. Run the following command to install Python-pip.
```shellsession
yum install python3-pip -y
```
:::
::: Ubuntu:
  1. Run the following command to clear the cache.
```shellsession
apt-get clean all
```
  2. Run the following command to update the software package list.
```shellsession
apt-get update -y
```
  3. Run the following command to install Python-pip.
```shellsession
apt-get -y install python3-pip
```
:::
</dx-tabs>
