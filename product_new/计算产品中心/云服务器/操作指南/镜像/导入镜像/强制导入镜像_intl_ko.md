## 작업 시나리오
사용자의 Linux 미러 이미지가 어떤 이유로 [cloudinit 설치](https://intl.cloud.tencent.com/document/product/213/12587)를 할 수 없을 경우 **미러 이미지 강제로 가져오기** 기능을 사용하여 완료할 수 있습니다. 사용자가 강제로 미러 이미지를 가져오는 경우 Tencent Cloud가 사용자의 CVM에 초기화 구성을 실행할 수 없으므로 사용자가 스크립트를 설치하여 Tencent Cloud에서 제공한 구성 파일에 따라 직접 CVM에 구성해야 합니다. 본 문서는 사용자가 미러 이미지를 강제로 가져오는 전제 하에 CVM를 구성하는 방법을 안내합니다.

## 제한 조건
- 미러 이미지는 [미러 이미지 가져오기](https://intl.cloud.tencent.com/document/product/213/4945)에서 Linux 미러 이미지 가져오기에 대한 미러링 제한(cloudinit 제외)을 충족해야 합니다.
- 가져온 미러 이미지의 시스템 파티션이 충족하지 않습니다.
- 가져온 미러 이미지는 원격으로 이용할 수 있는 취약점이 존재하면 안됩니다.
- 사용자가 미러 이미지를 강제로 가져오기를 실행하여 인스턴스가 성공적으로 생성된 후 즉시 비밀번호를 수정할 것을 권장합니다.

## 작업 순서

사용자가 강제로 가져온 미러 이미지는 cloudinit를 사용하지 않기 때문에 자동으로 구성되지 않습니다. Tencent Cloud는 구성 정보가 포함된 cdrom 장치를 제공하므로 사용자가 직접 구성할 수 있습니다. cdrom을 마운트할 경우 `mount_point/qcloud_action/os.conf` 의 정보를 읽고 구성해야 합니다. 만약 사용자가 다른 구성 데이터인 UserData 를 사용해야 한다면 `mount_point/`에서 파일을 직접 읽을 수 있습니다.

### os.conf 구성 파일 내용
os.conf 의 기본 내용은 다음과 같습니다.
<pre>
hostname=VM_10_20_xxxx
password=GRSgae1fw9frsG.rfrF
eth0&#95;ip&#95;addr=10.104.62.201
eth0&#95;mac&#95;addr=52:54:00:E1:96:EB
eth0&#95;netmask=255.255.192.0
eth0&#95;gateway=10.104.0.1
dns&#95;nameserver="10.138.224.65 10.182.20.26 10.182.24.12"
</pre>
> 위 정보는 파라미터 이름만 참고하면 되고 파라미터값은 예시로만 사용됩니다.
>
os.conf 에서 각 파라미터의 의미는 다음과 같습니다.

|파라미터 이름|파라미터 의미|
|----------|----------|
|hostname|호스트 이름|
|password|암호화된 비밀번호|
|eth0_ip_addr|eth0 ENI의 랜 IP|
|eth0_mac_addr|eth0 ENI의 MAC 주소|
|eth0_netmask|eth0 ENI의 서브넷 마스트|
|eth0_gateway|eth0 ENI의 게이트웨이|
|dns_nameserver|DNS 서버 확인|


### 스크립트 구성 확인

#### 주의사항
- 스크립트가 시작할 때 자동으로 실행되므로 운영 체제에 따라 해당 요구 사항을 실행하십시오.
- 스크립트는 `/dev/cdrom`을 마운트 포인트하고 아래 `os_action/os.conf` 파일을 읽은 후 구성 정보를 가져옵니다.
- Tencent Cloud가 cdrom에 설치한 비밀번호는 암호화된 비밀번호이므로 사용자는 `chpasswd -e` 방식을 사용하여 설정할 수 있습니다.
**암호화된 비밀번호는 특수 문자가 포함될 수 있으므로 먼저 파일에 배치한 후 `chpasswd -e < passwd_file` 방식으로 설정하는 것을 권장합니다.**
- 강제로 가져온 미러 이미지를 사용하여 미러 이미지를 다시 작성할 경우 스크립트의 지속적인 실행으로 인스턴스의 정확한 구성을 보장해야 합니다. 또한 해당 인스턴스에 cloudinit를 설치할 수 있습니다.

#### 예시
Tencent Cloud는 CentOS를 기반한 스크립트 예시를 제공하여 사용자는 스크립트 예시에 따라 미러 이미지 구성을 생성합니다. 생성 과정에서 다음과 같은 사항에 주의해야 합니다.
- **해당 스크립트는 미러 이미지 가져오기 전에 시스템에 정확하게 배치해야 합니다**.
- 해당 스크립트는 모든 운영 체제에 적합하지 않으므로 사용자가 본인의 운영 체제에 따라 수정해야 semantics를 충족할 수 있습니다.



1. 다음 스크립트 예시에 따라 `os_config` 스크립트를 생성합니다.
사용자는 실제 상황에 따라 `os_config` 스크립트를 수정할 수 있습니다.
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
2. `os_config` 스크립트를 `/etc/init.d/` 디렉터리에 배치하고 다음 명령어를 실행합니다.
```
chmod +x /etc/init.d/os_config
chkconfig --add os_config
```
3. 다음 명령어를 실행하여 `os_config`가 시작 서비스에 추가되었는지 확인합니다.
```
chkconfig --list
```
> 사용자는 스크립트의 정확한 실행을 보장해야 합니다. 미러 이미지를 가져온 후 SSH을 통해 인스턴스 및 네트워크에 연결할 수 없을 경우 콘솔에서 인스턴스를 연결하여 스크립트를 다시 시작합니다. 여전히 문제가 처리되지 않으면 고객서비스에 문의하십시오.


