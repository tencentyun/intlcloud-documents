## 操作シナリオ

Cloud-initは主にインスタンスを初めて初期化する際のカスタム設定機能を提供するものです。インポートされたイメージにcloud-initサービスがインストールされていない場合、イメージで起動されたインスタンスは正しく初期化できなくなり、イメージのインポートに失敗する可能性があります。このドキュメントではcloud-initサービスのインストールについてご説明します。
cloud-initのインストールについては次の2つの方法が推奨されます。
- [手動でcloud-initのソースコードパッケージをダウンロードする方法](#ManualDown) 
- [ソフトウェアソースにあるcloud-initパッケージを使用する方法](#SoftSources)

## 注意事項
Linuxシステムイメージをインポートする前に、イメージにcloud-initサービスが正しくインストールされていることを確認してください。

## 前提条件
cloud-initサービスをインストールされたサーバは外部ネットワークにアクセスできます。

## 操作手順
<dx-tabs>
::: 手動で\scloud-init\sソースコードパッケージをダウンロードする方法[](id:ManualDown)

### cloud-initのソースコードパッケージをダウンロードする



<dx-alert infotype="explain" title="">
- 正常にインストールされた状態では、cloud-init-17.1バージョンはTencent Cloudとの互換性が最も高く、そのイメージで作成されたCVMのすべての設定項目を正しく初期化することができます。**cloud-init-17.1.tar.gz**インストールバージョンの選択をお勧めします。また、[ここをクリック](https://launchpad.net/cloud-init/+download)して他のバージョンのcloud-initソースコードパッケージを入手することもできます。このドキュメントではcloud-init-17.1バージョンを例に説明します。
- cloud-init-17.1または他のバージョンのcloud-initソースコードパッケージによるインストールが失敗した場合は、[手動で簡易バージョンのcloud-initパッケージをダウンロードする方法](#greeninitCloudInit)方法でもインストールできます。
</dx-alert>


以下のコマンドを実行して、cloud-initのソースコードパッケージをダウンロードします。
```shellsession
wget https://launchpad.net/cloud-init/trunk/17.1/+download/cloud-init-17.1.tar.gz
```

### cloud-initをインストールする
1. 次のコマンドを実行して、cloud-initインストールパッケージを解凍します。
<dx-alert infotype="explain" title="">
ご使用の OSがUbuntuの場合は、rootアカウントに切り替えてください。
</dx-alert>
```shellsession
tar -zxvf cloud-init-17.1.tar.gz 
```
2. 次のコマンドを実行して、解凍したcloud-initのインストールパッケージディレクトリ（cloud-init-17.1ディレクトリ）に進みます。
```shellsession
cd cloud-init-17.1
```
3. OSバージョンに応じてPython-pipをインストールします。
  - CentOS 6/7シリーズの場合は、次のコマンドを実行します。
```shellsession
yum install python3-pip -y
```
  - Ubuntuシリーズの場合は、次のコマンドを実行します。
```shellsession
apt-get -y install python3-pip
```
インストールの際に、インストールできない、またはインストールパッケージが見つからないエラーが発生した場合は、[Python-pipがインストールできない問題の対処方法](#updateSoftware)を参照して処理を行うことができます。
4. 次のコマンドを実行し、pipをアップグレードします。
```
python3 -m pip install --upgrade pip 
```
4. 次のコマンドを実行し、依存パッケージをインストールします。
<dx-alert infotype="notice" title="">
Cloud-initがrequests 2.20.0バージョンのコンポーネントに依存する場合、Python 2.6はサポートされません。イメージ環境のPythonインタープリターがPython 2.6以下の場合、cloud-initの依存パッケージをインストールする前に、`pip install 'requests&lt;2.20.0'`コマンドを実行して、requests 2.20.0以下のバージョンをインストールしてください。
</dx-alert>
```shellsession
pip3 install -r requirements.txt
```
5. OSバージョンに応じてcloud-utilsコンポーネントをインストールします。
  - CentOS 6シリーズの場合は、次のコマンドを実行します。
```shellsession
yum install cloud-utils-growpart dracut-modules-growroot -y
dracut -f
```
  - CentOS 7シリーズの場合は、次のコマンドを実行します。
```shellsession
yum install cloud-utils-growpart -y
```
  - Ubuntuシリーズの場合は、次のコマンドを実行します。
```shellsession
apt-get install cloud-guest-utils -y
```
6. 次のコマンドを実行して、cloud-initをインストールします。
```shellsession
python3 setup.py build 
```
```shellsession
python3 setup.py install --init-system systemd
``` <dx-alert infotype="notice" title="">
--init-systemのオプションパラメータには：(systemd, sysvinit,  sysvinit_deb, sysvinit_freebsd, sysvinit_openrc, sysvinit_suse, upstart)  [default: None]があります。現在のOSで使用されている自動起動サービス管理方法に従って選択してください。間違った方式を選択した場合、cloud-initサービスはスタートアップで自動的に起動しません。このドキュメントでは、systemd自動起動サービス管理を例に説明します。
</dx-alert>


### cloud-init設定ファイルの変更

1. OSの違いに応じて、cloud.cfgをダウンロードします。
  - Ubuntu OSのcloud.cfgは、[ここをクリックしてダウンロード](https://cloudinit-1251783334.cos.ap-guangzhou.myqcloud.com/ubuntu/cloud.cfg)します。
  - CentOS OSのcloud.cfgは、[ここをクリックしてダウンロード](https://cloudinit-1251783334.cos.ap-guangzhou.myqcloud.com/centos/cloud.cfg)します。
2. `/etc/cloud/cloud.cfg` の内容を、ダウンロードしたcloud.cfgファイルの内容に置き換えます。


### syslogユーザーの追加
以下のコマンドを実行して、syslogユーザーを追加します。
```shellsession
useradd syslog
```


### cloud-initサービスの自動起動を設定する
- **OSがsystemdを使用してサービスの自動起動を管理している場合は、次のコマンドを実行して設定します。**
<dx-alert infotype="explain" title="">
`strings /sbin/init | grep "/lib/system"`コマンドを実行し、メッセージが返された場合、OSはsystemdを使用してサービスの自動起動を管理しています。
</dx-alert>
 1. **Ubuntu OSまたはDebian OSに対しては、次のコマンドを実行する必要があります。**
```shellsession
 ln -s /usr/local/bin/cloud-init /usr/bin/cloud-init 
```
 2. **すべてのOSで次のコマンドを実行する必要があります。**
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
 3. **CentOSとRedhat OSに対しては、次のコマンドを実行する必要があります。**
 /lib/systemd/system/cloud-init-local.serviceファイルを次の内容に置き換えます。
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
/lib/systemd/system/cloud-init.serviceファイルを次の内容に置き換えます。
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
- **OSがsysvinitを使用してサービスの自動起動を管理している場合は、次のコマンドを実行して設定します。**
<dx-alert infotype="explain" title="">
`strings /sbin/init | grep "sysvinit"`コマンドを実行し、メッセージが返された場合、OSはsysvinitを使用してサービスの自動起動を管理しています。
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
::: ソフトウェアソースにある\scloud-init\sパッケージを使用する方法[](id:SoftSources)
### cloud-initをインストールする

以下のコマンドを実行して、cloud-initをインストールします。
```shellsession
apt-get/yum install cloud-init
```
<dx-alert infotype="explain" title="">
apt-getまたはyumコマンドによってインストールされたcloud-initバージョンは、デフォルトが現在のOSに設定されたソフトウェアソースのデフォルトのcloud-initバージョンです。 この方式でインストールされたイメージで作成したインスタンスは、一部の設定項目が予想どおりに初期化されていない可能性があるため、 [手動でcloud-initのソースコードパッケージをダウンロードする方法](#ManualDown) を利用してインストールすることをお勧めします。
</dx-alert>



### cloud-init設定ファイルの変更
1. OSの違いに応じて、cloud.cfgをダウンロードします。
 - Ubuntu OSのcloud.cfgは、[ここをクリックしてダウンロード](https://cloudinit-1251783334.cos.ap-guangzhou.myqcloud.com/ubuntu/cloud.cfg)します。
 - CentOS OSのcloud.cfgは、[ここをクリックしてダウンロード](https://cloudinit-1251783334.cos.ap-guangzhou.myqcloud.com/centos/cloud.cfg)します。
2. `/etc/cloud/cloud.cfg` の内容を、ダウンロードしたcloud.cfgファイルの内容に置き換えます。
:::
</dx-tabs>



## 関連操作


<dx-alert infotype="notice" title="">
以下の操作が完了したら、サーバーを再起動しないでください。再起動した場合は、以下の操作を再度実行する必要があります。
</dx-alert>


1. 以下のコマンドを実行して、cloud-init関連の設定が正常に完了したかどうかを確認します。
```shellsession
cloud-init init --local
```
次のようなメッセージが返された場合、cloud-initの構成は正常に完了しています。
```shellsession
Cloud-init v. 20.1 running 'init-local' at Fri, 01 Apr 2022 01:26:11 +0000. Up 38.70 seconds.
```
2. 次のコマンドを実行して、cloudinitのキャッシュ記録を削除します。
```shellsession
rm -rf /var/lib/cloud
```
3. Ubuntu OSまたはDebian OSに対しては、次のコマンドを実行する必要があります。
``` shellsession
rm -rf /etc/network/interfaces.d/50-cloud-init.cfg
```
4. Ubuntu OSまたはDebian OSに対して、`/etc/network/interfaces`を以下のように変更する必要があります。
```shellsession
# This file describes the network interfaces available on your system
# and how to activate them. For more information, see interfaces(5).
source /etc/network/interfaces.d/*
```

## 付録

#### 手動で簡易バージョンのcloud-initパッケージをダウンロードする方法[](id:greeninitCloudInit)
[手動でcloud-initのソースコードパッケージをダウンロードする方法](#ManualDown)でインストールに失敗した場合は、以下の操作でインストールできます。
1. [ここをクリック](https://image-tools-1251783334.cos.ap-guangzhou.myqcloud.com/greeninit-x64-beta.tgz)して簡易版のcloud-initパッケージを入手します。
2. 次のコマンドを実行して、簡易版のcloud-initパッケージを解凍します。
```shellsession
tar xvf greeninit-x64-beta.tgz 
```
3. 次のコマンドを実行して、解凍した簡易版cloud-initのパッケージディレクトリ（greeninitディレクトリ）に進みます。
```shellsession
cd greeninit
```
4. 次のコマンドを実行して、cloud-initをインストールします。
```shellsession
sh install.sh 
```

### Python-pipがインストールできない問題の対処方法[](id:updateSoftware)
Python-pipのインストールの際に、このインストールパッケージがない、またはインストールできないエラーが発生した場合は、実際に使用しているOSに応じて、次の手順を参照して対処することができます。
<dx-tabs>
::: CentOS\s6/7シリーズ
  1. 次のコマンドを実行して、EPELリポジトリを設定します。
```shellsession
yum install epel-release -y
```
  2. 次のコマンドを実行して、Python-pipをインストールします。
```shellsession
yum install python3-pip -y
```
:::
::: Ubuntu\sシリーズ
  1. 次のコマンドを実行して、ソフトウェアパッケージリストを更新します。
```shellsession
apt-get update -y
```
  2. 次のコマンドを実行して、Python-pipをインストールします。
```shellsession
apt-get -y install python3-pip
```
:::
</dx-tabs>
