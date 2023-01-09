
## ユースケース

Cloud-initは、主にインスタンスが最初に初期化されるときにカスタマイズ設定機能を提供します。インポートされたイメージにcloud-initサービスがインストールされていない場合、イメージを介して起動されたインスタンスは正しく初期化できなくなり、イメージのインポートに失敗する可能性があります。このドキュメントでは、cloud-initサービスをインストールする方法について説明します。
cloud-initをインストールするには、次の2つの方法をお勧めします：
- [手動でcloud-initソースパッケージをダウンロードする](#ManualDown) 
- [ソフトウェアソースにあるcloud-initパッケージを使用する](#SoftSources)

## 注意事項
Linuxシステムイメージをインポートする前に、イメージにcloud-initサービスが正しくインストールされていることを確認してください。

##  前提条件
cloud-initサービスがインストールされているサーバーは、外部ネットワークに正しくアクセスできます。

## 操作手順
<dx-tabs>
::: \scloud-init\sソースコードパッケージを手動でダウンロードする方法[](id:ManualDown)

### cloud-initソースパッケージのダウンロード

<dx-alert infotype="explain" title="">
- 正常にインストールされた状態では、cloud-init-17.1バージョンがTencent Cloudとの互換性が最も高く、そのイメージで作成されたCVMのすべての設定項目は正常に初期化されます。**cloud-init-17.1.tar.gz** バージョンをインストールすることを推奨します。また [ここをクリック](https://launchpad.net/cloud-init/+download)して、その他のバージョンのcloud-initソースパッケージをダウンロードすることもできます。 このドキュメントでは、cloud-init-17.1バージョンを例に説明します。
- cloud-init-17.1または他のバージョンのcloud-initソースパッケージによるインストールに失敗した場合は、[手動で簡易バージョンのcloud-initソースパッケージをダウンロード](#greeninitCloudInit) してインストールできます。
</dx-alert>


次のコマンドを実行して、cloud-initソースパッケージをダウンロードします。
```shellsession
wget https://launchpad.net/cloud-init/trunk/17.1/+download/cloud-init-17.1.tar.gz
```

### cloud-initのインストール
1. 次のコマンドを実行して、cloud-initインストールパッケージを解凍します。
<dx-alert infotype="explain" title="">
OSがUbuntuの場合は、rootアカウントに切り替えてください。
</dx-alert>
```shellsession
tar -zxvf cloud-init-17.1.tar.gz 
```
2. 次のコマンドを実行して、解凍されたcloud-initのインストールパッケージディレクトリ（cloud-init-17.1ディレクトリ）に入ります。
```shellsession
cd cloud-init-17.1
```
3. OSバージョンに応じてPython-pipをインストールします。
    - CentOS 6/7の場合、次のコマンドを実行します：
    ```shellsession
    yum install python3-pip -y
    ```
    - Ubuntuの場合、次のコマンドを実行します：
    ```shellsession
    apt-get -y install python3-pip
    ```
インストール中に「インストールに失敗しました」または「インストールパッケージが見つかりません」などのエラーが発生した場合は、 [Python-pipがインストールできない時の解決法](#updateSoftware)を参考して問題のトラブルシューティングを行ってください。
4. 次のコマンドを実行し、pipをアップグレードします。
```
python3 -m pip install --upgrade pip
```
5. 次のコマンドを実行して、依存関係をインストールします。
<dx-alert infotype="notice" title="">
Cloud-initがrequests 2.20.0コンポーネントを使用する場合、Python 2.6はサポートされません。イメージ環境にインストールされているPythonインタープリターバージョンが2.6以前の場合、cloud-initの依存関係をインストールする前、`pip install ';2.20.0'` コマンドを実行して、requests 2.20.0以前のバージョンをインストールしてください。
</dx-alert>
```shellsession
pip3 install -r requirements.txt
```

6.  OSのバージョンに応じて、cloud-utilsコンポーネントをインストールします。
    - CentOS 6の場合、次のコマンドを実行します：
    ```shellsession
    yum install cloud-utils-growpart dracut-modules-growroot -y
    dracut -f
    ```
    - CentOS 7の場合、次のコマンドを実行します：
    ```shellsession
    yum install cloud-utils-growpart -y
    ```
    - Ubuntuの場合、次のコマンドを実行します：
    ```shellsession
    apt-get install cloud-guest-utils -y
    ```
7. 次のコマンドを実行して、cloud-initをインストールします。
```shellsession
python3 setup.py build
```
```shellsession
python3 setup.py install --init-system systemd
```

<dx-alert infotype="notice" title="">
--init-systemのオプションパラメータには、：(systemd、sysvinit、sysvinit_deb、sysvinit_FreeBSD、sysvinit_openrc、sysvinit_suse、upstart)[default：None]があります。現在のOSで使用されている自動起動サービス管理方法によってパラメータを選択してください。選択したパラメータが間違った場合、Cloud―initサービスはシステムの起動時に自動的に起動できません。このドキュメントでは、systemdの自動起動サービス管理を例として説明します。
</dx-alert>


[](id:cloud-init)
### cloud-init設定ファイルの変更

1. OSの違いに応じて、cloud.cfgをダウンロードします。
    - Ubuntu用のcloud.cfgをダウンロードするには、[ここをクリック](https://cloudinit-1251783334.cos.ap-guangzhou.myqcloud.com/ubuntu/cloud.cfg)してください。
    - CentOS用のcloud.cfgをダウンロードするには、[ここをクリック](https://cloudinit-1251783334.cos.ap-guangzhou.myqcloud.com/centos/cloud.cfg)してください。
2. `/etc/cloud/cloud.cfg` の内容を、ダウンロードしたcloud.cfgファイルの内容に置き換えます。


### syslogユーザーの追加
次のコマンドを実行して、syslogユーザーを追加します。
```shellsession
useradd syslog
```

### cloud-initサービスの自動起動の設定
- **OSが systemd自動起動管理サービスの場合は、以下のコマンドを実行して設定します。**
<dx-alert infotype="explain" title="">
`strings /sbin/init | grep "/lib/system"`  コマンドを実行します。メッセージが返却された場合は、OSは systemd自動起動管理サービスです。
</dx-alert>

- **UbuntuまたはDebianの場合、次のコマンドを実行します。**
```shellsession
 ln -s /usr/local/bin/cloud-init /usr/bin/cloud-init 
```

- **すべてのOSで次のコマンドを実行する必要があります。**
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

- **CentOSまたはRedhatで次のコマンドを実行します。**
 /lib/systemd/system/cloud-init-local.service ファイルを以下の内容に置き換えます：
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
/lib/systemd/system/cloud-init.service ファイルを以下の内容に置き換えます：
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
- **OSがsysvinit自動起動管理サービスの場合は、以下のコマンドを実行して設定します。**
<dx-alert infotype="explain" title="">
`strings /sbin/init | grep "sysvinit"`コマンドを実行します。メッセージが返却された場合は、OSはsysvinit自動起動管理サービスです。
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
::: ソフトウェアソースの\scloud-init\sパッケージを使用する方法[](id:SoftSources)
### cloud-initのインストール

次のコマンドを実行して、cloud-initをインストールします。
```shellsession
apt-get/yum install cloud-init
```
<dx-alert infotype="explain" title="">
デフォルトでは、apt-getまたはyumコマンドでインストールされるcloud-initは、現在のOSで設定されたソフトウェアソース中のデフォルトcloud-initバージョンを使用します。 この方法でインストールされたイメージを使用して作成したインスタンスは、一部の設定項目が予想通りに初期化されない可能性があるため、 [手動でcloud-initソースコードパッケージをダウンロード](#ManualDown)してサービスをインストールすることをお勧めします。
</dx-alert>



### cloud-init設定ファイルの変更
1. OSの違いに応じて、cloud.cfgをダウンロードします。
   - Ubuntu用のcloud.cfgをダウンロードするには、[ここをクリック](https://cloudinit-1251783334.cos.ap-guangzhou.myqcloud.com/ubuntu/cloud.cfg)してください。
   - CentOS用のcloud.cfgをダウンロードするには、[ここをクリック](https://cloudinit-1251783334.cos.ap-guangzhou.myqcloud.com/centos/cloud.cfg)してください。
2. `/etc/cloud/cloud.cfg` の内容を、ダウンロードしたcloud.cfgファイルの内容に置き換えます。
:::
</dx-tabs>



## 関連する操作


<dx-alert infotype="notice" title="">
以下の操作が完了した後、サーバーを再起動しないでください。再起動した場合は、以下の操作を再度実施する必要があります。
</dx-alert>


1. 次のコマンドを実行して、cloud-initが正しく設定されているかどうかを確認します。
```shellsession
cloud-init init --local
```
次のようなメッセージが戻ってきた場合、cloud-initの設定が完了したことがわかります。
```shellsession
Cloud-init v. 17.1 running 'init-local' at Fri, 01 Apr 2022 01:26:11 +0000. Up 38.70 seconds.
```
2. 次のコマンドを実行し、cloudinitのキャッシュをクリアします。
```shellsession
rm -rf /var/lib/cloud
```
3. UbuntuまたはDebianの場合、次のコマンドを実行します。
``` shellsession
rm -rf /etc/network/interfaces.d/50-cloud-init.cfg
```
4. UbuntuまたはDebianの場合、`/etc/network/interfaces` の内容を次のように置き換えます：
```shellsession
# This file describes the network interfaces available on your system
# and how to activate them. For more information, see interfaces(5).
source /etc/network/interfaces.d/*
```

## 付録
[](id:greeninitCloudInit)
### 手動で簡易バージョンのcloud-initパッケージをダウンロードする
[手動で簡易バージョンのcloud-initソースパッケージをダウンロード](#ManualDown) してcloud-initサービスをインストールできない場合は、次の手順を実行してcloud-initをインストールします：
1. 次のコマンドを実行して、`/usr/local`ディレクトリに切り替えます。
```shellsession
cd /usr/local
```
1. [ここをクリック](https://image-tools-1251783334.cos.ap-guangzhou.myqcloud.com/greeninit-x64-beta.tgz)して簡易バージョンのcloud-initパッケージを取得します。ダウンロードしたインストールパッケージは`/usr/lcoal`ディレクトリにアップロードされます。
>!注意：インストールディレクトリはシステムディスクディレクトリである必要があります。ファイルシステムをまたがることはできません。`/usr/local`ディレクトリにインストールすることをお勧めします
3. 次のコマンドを実行して、簡易バージョンのcloud-initパッケージを解凍します。
```shellsession
tar xvf greeninit-x64-beta.tgz 
```
4. 次のコマンドを実行して、解凍された簡易バージョンのcloud-initパッケージディレクトリ（つまり、greeninitディレクトリ）に入ります。
```shellsession
cd greeninit
```
5. 次のコマンドを実行して、cloud-initをインストールします。
```shellsession
sh install.sh 
```
[](id:updateSoftware)
### Python-pipがインストールできない時の解決法
インストール中に「インストールに失敗しました」や「インストールパッケージが見つかりません」などのエラーが発生した場合は、ご使用のOSに基づいて次のようにトラブルシューティングを行います。
<dx-tabs>
::: CentOS\s6/7の場合
  1. .次のコマンドを実行して、EPELストレージリポジトリを設定します。
```shellsession
yum install epel-release -y
```
  2. 次のコマンドを実行して、Python-pipをインストールします。
```shellsession
yum install python3-pip -y
```
:::
::: Ubuntu\sの場合
  1. 次のコマンドを実行して、キャッシュを消去します。
```shellsession
apt-get clean all
```
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
