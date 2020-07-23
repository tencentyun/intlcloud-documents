## 操作シナリオ

Cloud-initは、主にインスタンスが最初に初期化されるときにカスタマイズ設定機能を提供します。インポートされたイメージにcloud-initサービスがインストールされていない場合、イメージを介して起動されたインスタンスは正しく初期化できなくなり、イメージのインポートに失敗する可能性があります。このドキュメントでは、cloud-initサービスをインストールする方法について説明します。
cloud-initをインストールするには、次の2つの方法をお勧めします。
- [手動でcloud-initソースパッケージをダウンロードする](#ManualDown) 
- [ソフトウェアソースにあるcloud-initパッケージを使用する](#SoftSources)

## 注意事項
Linuxシステムイメージをインポートする前に、イメージにcloud-initサービスが正しくインストールされていることを確認してください。

## 前提条件
cloud-initサービスがインストールされているサーバーは、外部ネットワークに正しくアクセスできます。

## 操作手順

<span id="ManualDown"></span>
### 手動でcloud-initソースパッケージをダウンロードする

#### cloud-initソースパッケージのダウンロード
>  
>- 正常にインストールされた状態では、cloud-init-17.1バージョンはTencent Cloudとの互換性が最も高く、そのイメージで作成されたCVMのすべての設定アイテムを正しく初期化することができます。**cloud-init-17.1.tar.gz** バージョンをインストールすることをお薦めします。また [ここをクリック](https://launchpad.net/cloud-init/+download) してそのほかのバージョンのcloud-initソースパッケージをダウンロードすることもできます。 このドキュメントでは、cloud-init-17.1バージョンを例に説明します。
>- cloud-init-17.1または他のバージョンのcloud-initソースパッケージによるインストールが失敗した場合は、[手動で簡易バージョンのcloud-initソースパッケージをダウンロード](#greeninitCloudInit) してインストールできます。
>
次のコマンドを実行して、cloud-initソースパッケージをダウンロードします。
```
wget https://launchpad.net/cloud-init/trunk/17.1/+download/cloud-init-17.1.tar.gz
```

#### cloud-initのインストール
1. 次のコマンドを実行して、cloud-initインストールパッケージを解凍します。
> Ubuntu OSを使用している場合は、rootアカウントに切り替えてください。
>
```
tar -zxvf cloud-init-17.1.tar.gz 
```
2. 次のコマンドを実行して、解凍されたcloud-initのインストールパッケージディレクトリ（cloud-init-17.1ディレクトリ）に入ります。
```
cd cloud-init-17.1
```
3. OSバージョンに応じてPython-pipをインストールします。
 - CentOS 6/7の場合、次のコマンドを実行します：
```
yum install python-pip -y
```
 - Ubuntuの場合、次のコマンドを実行します：
```
apt-get install python-pip -y
```
4. 次のコマンドを実行して、依存関係をインストールします。
> cloud-initがrequests 2.20.0バージョンを使用する場合、Python 2.6はサポートされません。イメージ環境にインストールされているPythonインタープリターがPython 2.6以前の場合、cloud-init依存関係をインストールする前に、`pip install 'requests<2.20.0'` コマンドを実行して、requests 2.20.0以降のバージョンをインストールしてください。
>
```
pip install -r requirements.txt
```
4. OSのバージョンに応じて、cloud-utilsコンポーネントをインストールします。
 - CentOS 6の場合、次のコマンドを実行します。
```
yum install cloud-utils-growpart dracut-modules-growroot -y
dracut -f
```
 - CentOS 7の場合、次のコマンドを実行します。
```
yum install cloud-utils-growpart -y
```
 - Ubuntuの場合、次のコマンドを実行します。
```
apt-get install cloud-guest-utils -y
```
5. 次のコマンドを実行して、cloud-initをインストールします。
```
python setup.py build
python setup.py install --init-system systemd
```
> --init-systemのオプションパラメータには：(systemd、sysvinit、sysvinit_deb、sysvinit_freebsd、sysvinit_openrc、sysvinit_suse、upstart)[default：None]が含まれます。現在のOSで使用されている自動起動サービス管理方法に従って選択してください。間違った方式を選択した場合、cloud―initサービスは起動時に自動的に起動しません。このドキュメントでは、systemd自動起動サービス管理を例に説明します。

#### cloud-init構成ファイルの変更

1. OSの違いに応じて、cloud.cfgをダウンロードします。
 - Ubuntu OSのcloud.cfgをダウンロードするには、[ここをクリック](https://cloudinit-1251783334.cos.ap-guangzhou.myqcloud.com/ubuntu/cloud.cfg)してください。
 - CentOSのcloud.cfgをダウンロードするには、[ここをクリック](https://cloudinit-1251783334.cos.ap-guangzhou.myqcloud.com/centos/cloud.cfg)してください。
2. `/etc/cloud/cloud.cfg` の内容を、ダウンロードしたcloud.cfgファイルの内容に置き換えます。

#### syslogユーザーの追加
次のコマンドを実行して、syslogユーザーを追加します。
```
useradd syslog
```

#### cloud-initサービスの自動起動の設定
- **OSがsystemdを使用して自動起動サービスを管理している場合は、次のコマンドを実行して設定します。**
 1. **UbuntuまたはDebian OSに対して、次のコマンドを実行します。**
```
 ln -s /usr/local/bin/cloud-init /usr/bin/cloud-init 
```
 2. **すべてのOSで以下のコマンドを実行する必要があります。**
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
 3. **CentOSとRedhat OSで次のコマンドを実行します。**
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
- **OSがsysvinitを使用して自動起動サービスを管理している場合は、次のコマンドを実行して設定します。**
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
### ソフトウェアソースにあるcloud-initパッケージを使用する方法

#### cloud-initをインストールする

以下のコマンドを実行して、cloud-initをインストールします。
```
apt-get/yum install cloud-init
```
> apt-getまたはyumコマンドを介してインストールされたcloud-initバージョンは、デフォルトが現在のOSに設定されたソフトウェアソースのデフォルトのcloud-initバージョンです。 この方式でインストールされたイメージで作成したインスタンスは、一部の設定アイテムが予想通りに初期化されていない可能性があるため、 [手動でcloud-initのソースコードパッケージをダウンロードする](#ManualDown) を利用してインストールすることをお勧めします。　
>

#### cloud-init構成ファイルの変更
1. OSの違いに応じて、cloud.cfgをダウンロードします。
 - [ここをクリックしてダウンロード](https://cloudinit-1251783334.cos.ap-guangzhou.myqcloud.com/ubuntu/cloud.cfg) してUbuntu OSのcloud.cfgをダウンロードします。
 - [ここをクリックしてダウンロード](https://cloudinit-1251783334.cos.ap-guangzhou.myqcloud.com/centos/cloud.cfg) してCentOSのcloud.cfgをダウンロードします。
2. `/etc/cloud/cloud.cfg` の内容を、ダウンロードしたcloud.cfgファイルの内容に置き換えます。

## 関連する操作
> 以下の操作が完了したら、サーバーを再起動しないでください。再起動した場合は、以下の操作を再度実行する必要があります。
>
1. 次のコマンドを実行して、cloud-init関連の設定が正常に完了したかどうかを確認します。
```
cloud-init init --local
rm -rf /var/lib/cloud
```
2. Ubuntu OSまたはDebian OSの場合、次のコマンドを実行します。
```
rm -rf /etc/network/interfaces.d/50-cloud-init.cfg
```
3. Ubuntu OSまたはDebian OSの場合、`/etc/network/interfaces` の内容を次のように置き換えます。
```
# This file describes the network interfaces available on your system
# and how to activate them. For more information, see interfaces(5).
source /etc/network/interfaces.d/*
```

## 付録

<span id="greeninitCloudInit"></span>
### 手動で簡易バージョンのcloud-initパッケージをダウンロードする
[手動で簡易バージョンのcloud-initソースパッケージをダウンロードする](#ManualDown) でインストールに失敗した場合は、次の手順を実行してcloud-initをインストールします。
1. [ここをクリック](https://image-tools-1251783334.cos.ap-guangzhou.myqcloud.com/greeninit-x64-beta.tgz)して簡易バージョンのcloud-initパッケージを取得します。
2. 次のコマンドを実行して、簡易バージョンのcloud-initパッケージを解凍します。
```
tar xvf greeninit-x64-beta.tgz 
```
3. 次のコマンドを実行して、解凍された簡易バージョンのcloud-initパッケージディレクトリ（つまり、greeninitディレクトリ）に入ります。
```
cd greeninit
```
4.  次のコマンドを実行して、cloud-initをインストールします。
```
sh install.sh 
```






