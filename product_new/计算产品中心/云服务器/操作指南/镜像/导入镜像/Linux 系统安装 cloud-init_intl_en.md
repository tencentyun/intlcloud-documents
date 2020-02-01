## Scenario

Cloud-init enables you to customize configuration during the first initialization of an instance. If the imported image is not installed with the cloud-init service, instances booted with the image will not be initialized properly, which will result in an image import failure.
You can install cloud-init in two ways:
- [Manually downloading cloud-init source package](#ManualDown) 
- [Using the cloud-init package from the software source](#SoftSources)

## Notes
> Before importing a Linux image, please make sure you have properly installed the cloud-init service in your image.

## Prerequisites

Servers installed with the cloud-init service can visit external IPs.


## Directions

<span id="ManualDown"></span>
### Manually downloading cloud-init source package

#### Downloading the cloud-init source package
> Cloud-init source package: [download here](https://launchpad.net/cloud-init/+download). It is recommended to download **cloud-init-17.1.tar.gz** version.
>
Execute the following command to download the cloud-init source package.
```
wget https://launchpad.net/cloud-init/trunk/17.1/+download/cloud-init-17.1.tar.gz
```

#### Installing cloud-init
1. Execute the following command to decompress the cloud-init install package.
> If your operating system is Ubuntu, please switch to root account.
>
```
tar -zxvf cloud-init-17.1.tar.gz 
```
2. Execute the following command to enter the directory of the decompressed package, i.e., the cloud-init-17.1 directory.
```
cd cloud-init-17.1
```
3. Execute the following command to install Python-pip.
 - CentOS 6/7
```
yum install python-pip -y
```
 - Ubuntu
 ```
apt-get install python-pip -y
```
4. Execute the following command to install dependencies.
>  Python 2.6 is not supported when cloud-init uses requests 2.20.0. If the Python interpreter installed in the image environment is Python 2.6 or below, please execute the following command to install requests version below 2.20.0 before installing the cloud-init dependencies.
>
```
pip install -r requirements.txt
```
4. Install the cloud-utils components corresponding to your OS version.
 - CentOS 6:
```
yum install cloud-utils-growpart dracut-modules-growroot -y
dracut -f
```
 - CentOS 7:
```
yum install cloud-utils-growpart -y
```
 - Ubuntu:
```
apt-get install cloud-guest-utils -y
```
5. Execute the following command to install cloud-init.
```
python setup.py build
python setup.py install --init-system systemd
```
> Optional parameters for `--init-system` include: (ssystemd, sysvinit, sysvinit_deb, sysvinit_freebsd, sysvinit_openrc, sysvinit_suse, upstart)  [default: None]. Make a selection based on the current method of managing auto-start services of your OS. If you select a wrong one, the cloud-init service will not auto-start on boot. This document uses the systemd auto-start service manager as an example.

### Modifying the cloud-init configuration file

1. Download cloud.cfg for your operating system.
 - [cloud.cfg for Ubuntu](http://cloudinit-1251783334.cosgz.myqcloud.com/ubuntu-cloud.cfg)
 - [cloud.cfg for Centos](http://cloudinit-1251783334.cosgz.myqcloud.com/centos-cloud.cfg)
2. Replace the content in `/etc/cloud/cloud.cfg` with the content of the downloaded cloud.cfg file.

### Adding syslog user
Execute the following command to add a syslog user.
```
useradd syslog
```

### Configuring the auto-start of the cloud-init service on boot
- **If your operating system uses systemd to manage auto-start services, execute the following commands to make the configuration.**
 1. **Execute the following command in Ubuntu or Debian.**
```
 ln -s /usr/local/bin/cloud-init /usr/bin/cloud-init 
```
 2. **Execute the following commands in all operating systems.**
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
 3. **Execute the following command in Centos or Red Hat.**
 Replace the content in /lib/systemd/system/cloud-init-local.service with the following:
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
Replace the content in /lib/systemd/system/cloud-init.service with the following:
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
- **If your operating system uses sysvinit to manage auto-start services, execute the following commands to make the configuration.**
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

Execute the following command to install cloud-init.
```
apt-get/yum install cloud-init
```
> By default, the cloud-init version installed via `apt-get` or `yum` is the default cloud-init version in the software source configured for the current operating system. In the instances created with images whose cloud-init is installed this way, some configuration items may not be initialized as expected. It is recommended to install the service by [manually downloading cloud-init source package](#ManualDown).

#### Modifying the cloud-init configuration file
1. Download cloud.cfg needed for your operating system.
 - [cloud.cfg for Ubuntu](http://cloudinit-1251740579.cosgz.myqcloud.com/ubuntu-cloud.cfg)
 - [cloud.cfg for Centos](http://cloudinit-1251740579.cosgz.myqcloud.com/centos-cloud.cfg)
2. Replace the content in `/etc/cloud/cloud.cfg` with the content of the downloaded cloud.cfg file.

## Relevant operations after you finish the installation of cloud-init
> Please do not restart the server after you finish the following operations. Otherwise, you will need to perform the following operations again.
>
1. Execute the following command to see if cloud-init has been configured successful.
```
cloud-init init --local
rm -rf /var/lib/cloud
```
2. Execute the following command in Ubuntu or Debian.
```
rm -rf /etc/network/interfaces.d/50-cloud-init.cfg
```
3. For Ubuntu or Debian, you need to modify the content of `/etc/network/interfaces` to the following:
```
# This file describes the network interfaces available on your system
# and how to activate them. For more information, see interfaces(5).
source /etc/network/interfaces.d/*
```
