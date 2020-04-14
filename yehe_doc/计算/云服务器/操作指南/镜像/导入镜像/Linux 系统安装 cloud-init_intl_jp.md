## ユースケース

Cloud-initは、インスタンスに最初に初期化されるときにカスタマイズ設定機能を提供します。インポートされたイメージがcloud-initサービスをインストールされていない場合、イメージで起動されたインスタンスは正しく初期化できなくなり、イメージのインポートに失敗する可能性があります。このドキュメントでは、cloud-initサービスをインストールする方法について説明します。
次の2つの方法でcloud-initをインストールすることができます：
- [手動でcloud-initのソースコードパッケージをダウンロードします](#ManualDown) 
- [ソフトウェアソースにあるcloud-initパッケージを使用します](#SoftSources)

## 注意事項
Linuxイメージをインポートする前に、イメージにcloud-initサービスが正しくインストールされていることを確認してください。

## 前提条件
cloud-initサービスをインストールされたサーバは外部ネットワークにアクセスできます。

## 操作手順

<span id="ManualDown"></span>
### 手動でcloud-initのソースコードパッケージをダウンロードする

#### cloud-initのソースコードパッケージをダウンロードする
>? cloud-init-17.1バージョンはTencent Cloudとの互換性が最も高く、そのイメージで作成されたCVMのすべての設定アイテムを正しく初期化することができます。**cloud-init-17.1.tar.gz** バージョンをインストールすることをおすすめです。また [ここをクリック](https://launchpad.net/cloud-init/+download) してそのほかのバージョンのcloud-initのソースコードパッケージをダウンロードすることもできます。 本ドキュメントはcloud-init-17.1バージョンを例として説明します。
>
以下のコマンドを実行して、cloud-initのソースコードパッケージをダウンロードします。
```
wget https://launchpad.net/cloud-init/trunk/17.1/+download/cloud-init-17.1.tar.gz
```

#### cloud-initをインストールする
1. 次のコマンドを実行して、cloud-initインストールパッケージを解凍します。
>? OSがUbuntuの場合は、rootアカウントを使用してください。
>
```
tar -zxvf cloud-init-17.1.tar.gz 
```
2. 以下のコマンドを実行して、解凍したcloud-initのディレクトリ（cloud-init-17.1ディレクトリ）に入ります。
```
cd cloud-init-17.1
```
3. OSバージョンによりPython-pipをインストールします。
 - CentOS 6/7の場合、以下のコマンドを実行します：
```
yum install python-pip -y
```
 - Ubuntuの場合、以下のコマンドを実行します：
```
apt-get install python-pip -y
```
4. 以下のコマンドを実行して、依存関係をインストールします。
>! cloud-initがrequests 2.20.0を使用する場合、Python 2.6はサポートされません。イメージ環境にインストールされているPythonインタープリターがPython 2.6以下の場合、cloud-initの依存関係をインストールする前、`pip install 'requests<2.20.0'` コマンドを実行して、requests 2.20.0以下のバージョンをインストールしてください。
>
```
pip install -r requirements.txt
```
4. OSのバージョンによりcloud-utilsコンポーネントをインストールします。
 - CentOS 6の場合、以下のコマンドを実行します：
```
yum install cloud-utils-growpart dracut-modules-growroot -y
dracut -f
```
 - CentOS 7の場合、以下のコマンドを実行します：
```
yum install cloud-utils-growpart -y
```
 - Ubuntuの場合、以下のコマンドを実行します：
```
apt-get install cloud-guest-utils -y
```
5. 以下のコマンドを実行して、cloud-initをインストールします。
```
python setup.py build
python setup.py install --init-system systemd
```
>! --init-systemのオプションパラメータは：(systemd、sysvinit、sysvinit_deb、sysvinit_FreeBSD、sysvinit_openrc、sysvinit_suse、upstart)[default：None]があります。現在のOSで使用されている自動起動サービス管理方法に従って選択します。間違った方式を選択した場合、Cloud―initサービスは起動時に自動的に起動しません。本ドキュメントは、systemdサービスの自動起動サービス管理を例として説明します。

#### cloud-init構成ファイルの変更

1. OSにより、cloud.cfgをダウンロードします。
 - [ここをクリックして](http://cloudinit-1251783334.cosgz.myqcloud.com/ubuntu-cloud.cfg) Ubuntuのcloud.cfgをダウンロードします。
 - [ここをクリックして](http://cloudinit-1251783334.cosgz.myqcloud.com/centos-cloud.cfg) CentOSのcloud.cfgをダウンロードします。
2. `/etc/cloud/cloud.cfg` の内容をダウンロードしたcloud.cfgファイルの内容に置き換えます。

#### Syslogユーザーの追加
以下のコマンドを実行して、syslogユーザーを追加します。
```
useradd syslog
```

#### cloud-initサービスの自動起動を設定する
- **OSがsystemdを使用して自動起動サービスを管理している場合は、以下のコマンドを実行して設定します。**
 1. **UbuntuまたはDebian OSについて、以下のコマンドを実行します。**
```
 ln -s /usr/local/bin/cloud-init /usr/bin/cloud-init 
```
 2. **すべてのOSは以下のコマンドを実行する必要があります。**
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
 3. **CentOSとRedhat OSについて、以下のコマンドを実行します。**
 /lib/systemd/system/cloud-init-local.service ファイルを以下の内容に置き換えます：
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
/lib/systemd/system/cloud-init.service ファイルを以下の内容に置き換えます：
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
- **OSがsysvinitを使用して自動起動を管理する場合は、以下のコマンドを実行して設定します。**
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
### ソフトウェアソースにあるcloud-initパッケージを使用する

#### cloud-initをインストールする

以下のコマンドを実行して、cloud-initをインストールします。
```
apt-get/yum install cloud-init
```
> デフォルトでは、apt-getまたはyumコマンドを介してインストールされたcloud-initバージョンは、現在のOSに設定されたソフトウェアソースのデフォルトのcloud-initバージョンです。 この方式でインストールされたイメージで作成されたインスタンスは、一部の設定アイテムが予想通りに初期化されていない可能性があるため、 [手動でcloud-initのソースコードパッケージをダウンロードして](#ManualDown) インストールすることをおすすめです。　
>

#### cloud-init構成ファイルを変更する
1. OSにより、cloud.cfgをダウンロードします。
 - [ここをクリックして](http://cloudinit-1251740579.cosgz.myqcloud.com/ubuntu-cloud.cfg) Ubuntu OSのcloud.cfgをダウンロードします。
 - [ここをクリックして](http://cloudinit-1251740579.cosgz.myqcloud.com/centos-cloud.cfg) CentOSのcloud.cfgをダウンロードします。
2. `/etc/cloud/cloud.cfg` の内容をダウンロードしたcloud.cfgファイルの内容に置き換えます。

## 関連操作
>!以下の操作が完了したら、サーバーを再起動しないでください。再起動した場合は、以下の操作を再度実行する必要があります。
>
1. 以下のコマンドを実行して、cloud-initが正常に設定されているかどうかを確認します。
```
cloud-init init --local
rm -rf /var/lib/cloud
```
2. Ubuntu OSまたはDebian OSについて、以下のコマンドを実行します。
```
rm -rf /etc/network/interfaces.d/50-cloud-init.cfg
```
3. Ubuntu OSまたはDebian OSについて、`/etc/network/interfaces` を以下のように変更する必要があります：
```
# This file describes the network interfaces available on your system
# and how to activate them. For more information, see interfaces(5).
source /etc/network/interfaces.d/*
```
