## Overview

Cloud-init allows you to customize configurations during the first initialization of an instance. If the imported image does not have the cloud-init service installed, instances booted through the image cannot be initialized properly. As a result, the image will fail to be imported. This document describes how to install the cloud-init service.
You can use either of the following methods to install cloud-init:

- [Manually downloading the cloud-init source package](#ManualDown) 
- [Using the cloud-init package from the software source](#SoftSources)

## Notes
Before importing a Linux image, ensure that you have properly installed the cloud-init service in the image.

## Prerequisites
The server with the cloud-init service installed can access the public network.

## Directions


<span id="ManualDown"></span>
### Manually downloading the cloud-init source package 

#### Downloading the cloud-init source package
>?  
> - The cloud-init-17.1 version is most compatible with Tencent Cloud. It ensures that all configuration items of CVMs created through the image can be initialized properly. We recommend that you install **cloud-init-17.1.tar.gz**. You can also [click here](https://launchpad.net/cloud-init/+download) to download other versions. This document uses cloud-init-17.1 as an example.
> - If the installation fails, [manually download the green cloud-init package](#greeninitCloudInit) to install the service.
>
Run the following command to download the cloud-init source package:
```
wget https://launchpad.net/cloud-init/trunk/17.1/+download/cloud-init-17.1.tar.gz
```

#### Installing cloud-init
1. Run the following command to decompress the cloud-init installation package:
>? If you are using the Ubuntu operating system, run this command with the “root” account.
>
```
tar -zxvf cloud-init-17.1.tar.gz 
```
2. Run the following command to enter the decompressed cloud-init installation package directory; that is, the cloud-init-17.1 directory:
```
cd cloud-init-17.1
```
3. Install Python-pip according to the operating system version.
 - For CentOS 6/7, run the following command:
```
yum install python-pip -y
```
 - For Ubuntu, run the following command:
```
apt-get install python-pip -y
```
During installation, if an error such as “failed to install” or “installation package not found” occurs, see [resolving Python-pip installation failure](#updateSoftware) to troubleshoot it.
4. Run the following command to install dependencies:
>!  Python 2.6 is not supported when cloud-init uses requests 2.20.0 or later. If the Python interpreter installed in the image environment is Python version 2.6 or earlier, run the `pip install 'requests<2.20.0'` command to install requests 2.20.0 or later before installing the cloud-init dependencies.
>
```
pip install -r requirements.txt
```
5. Install the cloud-utils component according to the operating system version.
 - For CentOS 6, run the following command:
```
yum install cloud-utils-growpart dracut-modules-growroot -y
dracut -f
```
 - For CentOS 7, run the following command:
```
yum install cloud-utils-growpart -y
```
 - For Ubuntu, run the following command:
```
apt-get install cloud-guest-utils -y
```
6. Run the following commands to install cloud-init:
```
python setup.py build
python setup.py install --init-system systemd
```
>! The `--init-system` can be followed by any of systemd, sysvinit, sysvinit_deb, sysvinit_freebsd, sysvinit_openrc, sysvinit_suse or upstart [default: None]. Please configure parameters based on the auto-start service management method of the operating system. If incorrect parameters are configured, the cloud-init service cannot automatically start upon system startup. This document uses the systemd auto-start service management method as an example.

#### Modifying the cloud-init configuration file

1. Download cloud.cfg for your operating system.
 - [Click here](https://cloudinit-1251783334.cos.ap-guangzhou.myqcloud.com/ubuntu/cloud.cfg) to download cloud.cfg for Ubuntu.
 - [Click here](https://cloudinit-1251783334.cos.ap-guangzhou.myqcloud.com/centos/cloud.cfg) to download cloud.cfg for CentOS.
2. Replace the content of `/etc/cloud/cloud.cfg` with that of the downloaded cloud.cfg file.

#### Adding a syslog user
Run the following command to add a syslog user:
```
useradd syslog
```

#### Setting the cloud-init service to autostart
- **If your operating system uses the systemd auto-start service management method, run the following commands.**
>? To check whether the operating system uses systemd, run the `strings /sbin/init | grep "/lib/system"` command, and you will receive a return message.
>
 1. **Run the following command in Ubuntu or Debian:**
```
 ln -s /usr/local/bin/cloud-init /usr/bin/cloud-init 
```
 2. **Run the following commands in all operating systems:**
```
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
 3. **Run the following command in CentOS or Redhat.**
 Replace the content of `/lib/systemd/system/cloud-init-local.service` with the following:
```
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
```
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
>? To check whether the operating system uses sysvinit, run the `strings /sbin/init | grep "sysvinit"` command, and you will receive a return message.
>
```
chkconfig --add cloud-init-local
chkconfig --add cloud-init
chkconfig --add cloud-config
chkconfig --add cloud-final
chkconfig cloud-init-local on 
chkconfig cloud-init on 
chkconfig cloud-config on 
chkconfig cloud-final on 
```


<span id="SoftSources"></span>
### Using the cloud-init package from the software source

#### Installing cloud-init

Run the following command to install cloud-init:
```
apt-get/yum install cloud-init
```
>? By default, the cloud-init version installed by running `apt-get` or `yum` is the default cloud-init version in the software source configured for the operating system. Some configuration items of instances created by using the image whose cloud-init is installed this way may not be initialized as expected. Therefore, we recommend that you install the service by [manually downloading the cloud-init source package](#ManualDown).
>

#### Modifying the cloud-init configuration file
1. Download cloud.cfg for your operating system.
 - [Click here](https://cloudinit-1251783334.cos.ap-guangzhou.myqcloud.com/ubuntu/cloud.cfg) to download cloud.cfg for Ubuntu.
 - [Click here](https://cloudinit-1251783334.cos.ap-guangzhou.myqcloud.com/centos/cloud.cfg) to download cloud.cfg for CentOS.
2. Replace the content of `/etc/cloud/cloud.cfg` with that of the downloaded cloud.cfg file.

## Relevant Operations
>! Do not restart the server after performing the above operations. Otherwise, you will need to perform them again.
>
1. Run the following commands to check whether the cloud-init configuration is successful.
```
cloud-init init --local
rm -rf /var/lib/cloud
```
2. Run the following command in Ubuntu or Debian:
```
rm -rf /etc/network/interfaces.d/50-cloud-init.cfg
```
3. For Ubuntu or Debian, replace the content of `/etc/network/interfaces` with the following:
```
# This file describes the network interfaces available on your system
# and how to activate them. For more information, see interfaces(5).
source /etc/network/interfaces.d/*
```

## Notes

<span id="greeninitCloudInit"></span>
### Downloading the portable edition of cloud-init package
If you fail to install cloud-init as instructed in [Manually downloading the cloud-init source package](#ManualDown), try the following steps:
1. [Click here](https://image-tools-1251783334.cos.ap-guangzhou.myqcloud.com/greeninit-x64-beta.tgz) to obtain the portable edition of cloud-init package.
2. Run the following command to decompress the portable package:
```
tar xvf greeninit-x64-beta.tgz 
```
3. Run the following command to enter the decompressed the package directory; that is, the `greeninit` directory:
```
cd greeninit
```
4. Run the following command to install cloud-init:
```
sh install.sh 
```

<span id="updateSoftware"></span>

### Resolving Python-pip installation failure

During installation, if an error such as “failed to install” or “installation package not found” occurs, troubleshoot it based on the operating system as follows:
- For CentOS 6/7:
  1. Run the following command to configure the EPEL storage repository.
```
yum install epel-release -y
```
  2. Run the following command to install Python-pip.
```
yum install python-pip -y
```
- For Ubuntu:
  1. Run the following command to update the software package list.
```
apt-get update -y
```
  2. Run the following command to install Python-pip.
```
apt-get install python-pip -y
```


