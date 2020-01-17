## 操作シナリオ
ユーザーのLinuxイメージはある原因で[cloudinitのインストール](https://intl.cloud.tencent.com/document/product/213/12587)できなくなった場合は、**強制的にイメージをインポートする**機能を使用してインポートを完成させます。ユーザーが強制的にイメージをインポートする場合、Tencent CloudはユーザーのCVMに対して初期化を設定できなくなります。ユーザーはTencent Cloudが提供している設定ファイルに基づいてスクリプトを設定してCVMを設定する必要があります。このドキュメントは強制的にイメージをインポートしてCVMを設定する方法について説明します。

## 制限条件
- [イメージのインポート](https://intl.cloud.tencent.com/document/product/213/4945) 時、Linux イメージをインポートする制限（cloudinit 以外）を満たす必要があります。
- インポートしたイメージのOSパーティションが残っています。
- インポートしたイメージはリモート利用可能な脆弱性が存在できません。
- イメージを強制的にインポートして、インスタンスが成功に作成した後にユーザーがパスワードを変更することをお勧めします。

## 操作手順

ユーザーが強制的にイメージをインポートする時に、cloudinitを使用していないため、自動的に設定することができません。Tencent Cloudは設定情報を含むcdromデバイスを提供して、ユーザーが自分で設定できます。ユーザーはcdromをマウントする必要があり、`mount_point/qcloud_action/os.conf` 情報を読み取って設定します。ユーザーはほかの設定データとUserDataを利用するニーズがある場合、 直接`mount_point/` 配下のファイルを読み取ることができます。

### 設定ファイルos.confの内容
os.conf の基本内容は以下のようなります：
<pre>
hostname=VM_10_20_xxxx
password=GRSgae1fw9frsG.rfrF
eth0_ip_addr=10.104.62.201
eth0_mac_addr=52:54:00:E1:96:EB
eth0_netmask=255.255.192.0
eth0_gateway=10.104.0.1
dns_nameserver="10.138.224.65 10.182.20.26 10.182.24.12"
</pre>
> 以上の情報はパラメータ名のみ参考する意味があり、パラメータ值は単なる事例になります。
>
os.conf に各パラメータの意味は以下の通り：

|パラメータ名|パラメータ意味|
|----------|----------|
|hostname|ホスト名|
|password|暗号化したパスワード|
|eth0_ip_addr|eth0 ENIのLAN IP|
|eth0_mac_addr|eth0 ENIの MAC アドレス|
|eth0_netmask|eth0 ENIのサブネットマスク|
|eth0_gateway|eth0 ENIのゲートウェイ|
|dns_nameserver|DNS 解析サーバー|


### 設定スクリプトの解析

#### 注意事项
- スクリプトはスタートアップする時、自動的に実行されます、OSのタイプに基づいてこの要件を実現してください。
- スクリプトは `/dev/cdrom`をマウントする必要があり、マウントポイントの`os_action/os.conf` ファイルを読み取って、設定情報を取得します。
- Tencent Cloudが cdrom に入力したパスワードは暗号化されたパスワードであり、ユーザーは `chpasswd -e` 方式を使用して設定します。
**暗号化されたパスワードには特別な文字が含まれる可能性があり、まずファイルの中に入力してから、 `chpasswd -e < passwd_file`方式で設定することを推薦します。**
- 強制的にイメージをインポートして作成したインスタンスを使用して再びイメージを作成する時に、インスタンスを正確に設定することを保証するために、スクリプトが実行されることを確認する必要があります。インスタンスの中でcloudinitをインストールすることもできます。

#### 事例
Tencent CloudはCentOSに基づいてサンプルスクリプトを提供します。ユーザーはサンプルスクリプトに基づいて、独自のイメージ設定スクリプトを作成できます。作成中、以下の点を注意してください：
- **イメージをインポートする前にこのスクリプトをOSに正しく設置する必要があります**。
- このスクリプトは全てのOSに適しいることではなく、ユーザーは自分のOSに応じて修正する必要があります。



1. 以下スクリプトを例として、 `os_config` スクリプトを作成する。
ユーザーは実際状況に応じて `os_config` スクリプトを修正します。
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
2. `/etc/init.d/` ディレクトリに`os_config`スクリプトを設置して、以下のコマンドを実行します。
```
chmod +x /etc/init.d/os_config
chkconfig --add os_config
```
3. 以下のコマンドを実行し、 `os_config` は起動サービスに追加されたかどうかを確認します。
```
chkconfig --list
```
> ユーザーはスクリプトが正しく実行されたことを確認する必要があります。イメージをインポートした後、SSHを利用してインスタンスへの接続ができなかったり、ネットワークに接続できなかった場合、コンソールを利用してインスタンスに接続し、スクリプトを再実行して、問題をトラブルシューティングしてください。それでも処理できない場合は、カスターサービスにお問い合わせください。


