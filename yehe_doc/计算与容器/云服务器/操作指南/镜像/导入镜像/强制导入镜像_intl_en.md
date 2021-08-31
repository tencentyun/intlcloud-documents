## Scenario
If you cannot [install cloudinit](https://intl.cloud.tencent.com/document/product/213/12587) in your Linux image, use **Forced Image Import** to import the image. If you use this image for import, which does not have cloudinit installed, Tencent Cloud cannot initialize your CVM. In this case, you need to set up the script on your own to configure the CVM based on the configuration file provided by Tencent Cloud. This document describes how to configure the CVM if the image is forcibly imported.

Tencent Cloud provides the user with CDROM device containing the configuration information. The user needs to mount CDROM and read the information of `mount_point/qcloud_action/os.conf` for configuration. If other configuration data or UserData needs to be used, the user can directly read files under `mount_point/`.

## os.conf Configuration File
The content of os.conf is as follows.
<pre>
hostname=VM_10_20_xxxx
password=GRSgae1fw9frsG.rfrF
eth0&#95;ip&#95;addr=10.104.62.201
eth0&#95;mac&#95;addr=52:54:00:E1:96:EB
eth0&#95;netmask=255.255.192.0
eth0&#95;gateway=10.104.0.1
dns&#95;nameserver="10.138.224.65 10.182.20.26 10.182.24.12"
</pre>
>? The parameter names above are for reference, and the values are used as examples only.
>
The description of each parameter in the os.conf configuration file is as follows:

| Parameter Name | Description |
|----------|----------|
| hostname | CVM name |
| password | Encrypted password |
| eth0_ip_addr | LAN IP of eth0 |
| eth0_mac_addr | MAC address of eth0 |
| eth0_netmask | Subnet mask of eth0 |
| eth0_gateway | Gateway of eth0 |
| dns_nameserver | DNS resolution server |


## Limits
- The image must meet the limits on Linux images as outlined in [Import Images](https://intl.cloud.tencent.com/document/product/213/4945), except for cloudinit.
- The system partition for importing the image is not full.
- The imported image contains no vulnerability that can be exploited remotely.
- We recommend you change the password immediately after the instance is created successfully with the forcibly imported image.

## Notes
Note the following when configuring script parsing:
- The script is executed automatically at startup. Please implement this requirement based on your operating system.
- Mount `/dev/cdrom` and read `os_action/os.conf` file under the mount point to obtain the configuration information.
- The password placed in CDROM by Tencent Cloud is encrypted. You can set new password with `chpasswd -e`.
**Note that the encrypted password may contain special characters. We recommend you place it in a file and then set the password with `chpasswd -e < passwd_file`.**
- When you use the forcibly imported image to create an instance and then create an image, you need to ensure that the script will still be executed to ensure that the instance is configured correctly. You can also install cloudinit in this instance.


## Directions

>! Tencent Cloud provides a script sample based on CentOS. You can refer to it to create script for your images. During the creation, note that:
> - **The script must be properly placed in the system before image import**.
> - The script is not applicable to all operating systems. You need to modify it according to your own operating systems.
> 


1. Create an `os_config` script based on the following script sample.
You can modify the script as needed.

```
#!/bin/bash
### BEGIN INIT INFO
# Provides:          os-config
# Required-Start:    $local_fs $network $named $remote_fs
# Required-Stop:
# Should-Stop:
# Default-Start:     2 3 4 5
# Default-Stop:      0 1 6
# Short-Description: config of os-init job
# Description: run the config phase without cloud-init
### END INIT INFO
###################user settings#####################
cdrom_path=`blkid -L config-2`
load_os_config() {
	mount_path=$(mktemp -d /mnt/tmp.XXXX)
	mount /dev/cdrom $mount_path
	if [[ -f $mount_path/qcloud_action/os.conf ]]; then
		. $mount_path/qcloud_action/os.conf
		if [[ -n $password ]]; then
			passwd_file=$(mktemp /mnt/pass.XXXX)
			passwd_line=$(grep password $mount_path/qcloud_action/os.conf)
			echo root:${passwd_line#*=} > $passwd_file
		fi
		return 0
	else 
		return 1
	fi
}
cleanup() {
	umount /dev/cdrom
	if [[ -f $passwd_file ]]; then
		echo $passwd_file
		rm -f $passwd_file
	fi
	if [[ -d $mount_path ]]; then
		echo $mount_path
		rm -rf $mount_path
	fi
}
config_password() {
	if [[ -f $passwd_file ]]; then
		chpasswd -e < $passwd_file
	fi
}
config_hostname(){
	if [[ -n $hostname ]]; then
		sed -i "/^HOSTNAME=.*/d" /etc/sysconfig/network
		echo "HOSTNAME=$hostname" >> /etc/sysconfig/network
	fi
}
config_dns() {
    if [[ -n $dns_nameserver ]]; then
        dns_conf=/etc/resolv.conf
        sed -i '/^nameserver.*/d' $dns_conf
        for i in $dns_nameserver; do
            echo "nameserver $i" >> $dns_conf
        done
    fi
}
config_network() {
    /etc/init.d/network stop
    cat << EOF > /etc/sysconfig/network-scripts/ifcfg-eth0
DEVICE=eth0
IPADDR=$eth0_ip_addr
NETMASK=$eth0_netmask
HWADDR=$eth0_mac_addr
ONBOOT=yes
GATEWAY=$eth0_gateway
BOOTPROTO=static
EOF
    if [[ -n $hostname ]]; then
    	sed -i "/^${eth0_ip_addr}.*/d" /etc/hosts
		echo "${eth0_ip_addr} $hostname" >> /etc/hosts
	fi
    /etc/init.d/network start
}
config_gateway() {
	sed -i "s/^GATEWAY=.*/GATEWAY=$eth0_gateway" /etc/sysconfig/network
}
###################init#####################
start() {
	if load_os_config ; then
		config_password
		config_hostname
		config_dns
		config_network
		cleanup
		exit 0
	else 
		echo "mount ${cdrom_path} failed"
		exit 1
	fi
}
RETVAL=0
case "$1" in
	start)
		start
		RETVAL=$?
	;;
	*)
		echo "Usage: $0 {start}"
		RETVAL=3
	;;
esac
exit $RETVAL
```
2. Place the `os_config` script in the `/etc/init.d/` directory and execute the following command.
```
chmod +x /etc/init.d/os_config
chkconfig --add os_config
```
3. Execute the following command to check whether `os_config` has been added to the startup service.
```
chkconfig --list
```
>? You must ensure that the script is correctly executed. If you fail to connect to the instance via SSH or network exception occurs after the image import, try to connect to the instance via the console to execute the script again. If such problems remain, contact the customer service.


