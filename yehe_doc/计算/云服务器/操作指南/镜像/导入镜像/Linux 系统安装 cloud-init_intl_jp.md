
## ユースケース

Cloud-initはLinuxディストリビューションのインスタンスの自動的な初期化とカスタマイズのためのツールです。インポートされたイメージにcloud-initサービスがインストールされていない場合、イメージを介して起動されたインスタンスは正しく初期化できなくなり、イメージのインポートに失敗する可能性があります。このドキュメントでは、cloud-initサービスをインストールする方法について説明します。
cloud-initをインストールするには、次の3つの方法をお勧めします：
- [cloud-initバイナリパッケージをダウンロードする](#binary)
- [cloud-initパッケージを手動でダウンロードする](#ManualDown) 
- [ソフトウェアソースからcloud-initパッケージを使用する](#SoftSources)

## 注意事項
Linuxシステムイメージをインポートする前に、イメージにcloud-initサービスが正しくインストールされていることを確認してください。

##  前提条件
cloud-initサービスがインストールされているサーバーは、パブリックネットワークに正常にアクセスできます。

## 操作手順
<dx-tabs>
::: cloud-initバイナリーパッケージ[](id:binary)をダウンロードする
<dx-alert infotype="explain" title="">
- cloud-initはqcloud-pythonに依存します。qcloud-pythonは、Tencent Cloudによって再コンパイルおよびパッケージ化されたソフトウェアパッケージです。これは、ディレクトリ`/usr/local/qcloud/python`にインストールされた、cloud-initオペレーティング環境にのみ使用される個別のpython環境です。システムでのデフォルトのpythonと競合しません。
- cloud-initは、Tencent Cloudがコミュニティのバージョン20.1に基づいて開発され、Tencent Cloudの動作環境に適応する専用のcloud-initです。
- cloud-initバイナリーパッケージは、次のOSをサポートします：
</dx-alert>
<table>
<thead>
  <tr>
    <th rowspan="2">タイプ</th>
    <th rowspan="2">OS</th>
    <th rowspan="2">バージョン</th>
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
    <td>NA</td>
    <td>NA</td>
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
    <td>NA</td>
    <td>NA</td>
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
    <td>NA</td>
    <td>NA</td>
  </tr>
  <tr>
    <td>9</td>
    <td><a href="https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/packages/debian9/qcloud-python_3.7.10-1_amd64.deb">qcloud-python_3.7.10-1_amd64.deb</a></td>
    <td><a href="https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/packages/debian9/cloud-init_20.1.0011-1_amd64.deb">cloud-init_20.1.0011-1_amd64.deb</a></td>
    <td>NA</td>
    <td>NA</td>
  </tr>
  <tr>
    <td>8</td>
    <td><a href="https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/packages/debian8/qcloud-python_3.7.10-1_amd64.deb">qcloud-python_3.7.10-1_amd64.deb</a></td>
    <td><a href="https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/packages/debian8/cloud-init_20.1.0011-1_amd64.deb">cloud-init_20.1.0011-1_amd64.deb</a></td>
    <td>NA</td>
    <td>NA</td>
  </tr>
  <tr>
    <td rowspan="4">Ubuntu</td>
    <td>22.04</td>
    <td><a href="https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/packages/ubuntu22.04/qcloud-python_3.7.10-1_amd64.deb">qcloud-python_3.7.10-1_amd64.deb</a></td>
    <td><a href="https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/packages/ubuntu22.04/cloud-init_20.1.0011-1_amd64.deb">cloud-init_20.1.0011-1_amd64.deb</a></td>
    <td>NA</td>
    <td>NA</td>
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
    <td>NA</td>
    <td>NA</td>
  </tr>
</tbody>
</table>

### cloud-initバイナリーパッケージ[](id:binary)のダウンロード
1. 上記のインストールパッケージをダウンロードします。

2. cloud-init がすでに存在する場合は、次のコマンドを実行してクリアします。
```shellsession
rm -rf /var/lib/cloud
rm -rf /etc/cloud
rm -rf /usr/local/bin/cloud*
```
3. OSに応じて、次のコマンドを実行します：
  - debシリーズの場合は、次のコマンドを実行します：
  ```shellsession
  dpkg -i *.deb
  ```
 - rpmシリーズの場合は、次のコマンドを実行します：
 ```shellsession
 rpm -ivh *.rpm
 ```
4. バージョンが正しくインストールされているかどうかを確認します
  ```shellsession
cloud-init qcloud -v
/usr/bin/cloud-init qcloud 0011
  ```
5.  再起動後に有効になります
:::
::: \scloud-init\sパッケージを手動でダウンロードする[](id:ManualDown)

### cloud-initパッケージのダウンロード

<dx-alert infotype="explain" title="">
- cloud-init-20.1.0011 バージョンはTencent Cloud と最も互換性があります。これにより、このイメージで作成されたCVMのすべての設定項目が適切に初期化されることが保証されます。**cloud-init-20.1.0011.tar.gz**バージョンをインストールすることを推奨します。また[ここをクリック](https://launchpad.net/cloud-init/+download)してcloud-initパッケージの他のバージョンをダウンロードすることもできます。 このドキュメントでは、cloud-init-20.1.0011バージョンを例に説明します。
</dx-alert>


次のコマンドを実行して、cloud-initソースパッケージをダウンロードします。
```shellsession
wget https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/src/cloud-init-20.1.0011.tar.gz
```

### cloud-initのインストール
1. 次のコマンドを実行して、cloud-initインストールパッケージを解凍します。
<dx-alert infotype="explain" title="">
OSがUbuntuの場合は、rootアカウントに切り替えてください。
</dx-alert>
```shellsession
tar -zxvf cloud-init-20.1.0011.tar.gz 
```
2. 次のコマンドを実行して、解凍したcloud-initインストールパッケージディレクトリ（cloud-init-20.1.0011ディレクトリ）に移動します。
```shellsession
cd cloud-init
```
3. OSバージョンに応じてPython-pipをインストールします。
  - CentOS 6/7の場合、次のコマンドを実行します：
```shellsession
yum install python3-pip -y
```
  - Ubuntuの場合、次のコマンドを実行します。
```shellsession
apt-get -y install python3-pip
```
インストール中に「インストールに失敗しました」または「インストールパッケージが見つかりません」などのエラーが発生した場合は、 [Python-pipがインストールできない時の解決法](#updateSoftware)を参考して問題のトラブルシューティングを行ってください。
4. 次のコマンドを実行し、pipをアップグレードします。
```
python3 -m pip install --upgrade pip
```
5. 以下のコマンドを実行して、依存関係をインストールします。
<dx-alert infotype="notice" title="">
Cloud-initがrequests 2.20.0コンポーネントを使用する場合、Python 2.6はサポートされません。イメージ環境にインストールされているPythonインタープリターバージョンが2.6以前の場合、cloud-initの依存関係をインストールする前、`pip install 'requests<2.20.0'` コマンドを実行して、requests 2.20.0以前のバージョンをインストールしてください。
</dx-alert>
```shellsession
pip3 install -r requirements.txt
```

6. OSのバージョンによりcloud-utilsコンポーネントをインストールします。
  - CentOS 6の場合、次のコマンドを実行します。
```shellsession
yum install cloud-utils-growpart dracut-modules-growroot -y
dracut -f
```
  - CentOS 7の場合、次のコマンドを実行します。
```shellsession
yum install cloud-utils-growpart -y
```
  - Ubuntuの場合、次のコマンドを実行します。
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
- --init-systemのオプションパラメータには、：(systemd、sysvinit、sysvinit_deb、sysvinit_freebsd、sysvinit_openrc、sysvinit_suse、upstart)[default：None]があります。現在のOSで使用されている自動起動サービス管理方法によってパラメータを選択してください。選択したパラメータが間違った場合、システム起動時にcloud-initサービスを自動的に開始できません。
- CentOS6以前の旧バージョンではsysvinitを選択し、CentOS 7以降のバージョンではsystemdを選択してください。このドキュメントでは、例としてsystemdを使用します。
</dx-alert>


[](id:cloud-init)
### cloud-init設定ファイルの変更

1. OSの違いに応じて、cloud.cfgをダウンロードします。
  - Ubuntu OSのcloud.cfgをダウンロードするには、[ここをクリックしてください](https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/cfg/ubuntu/cloud.cfg)。
  - CentOSのcloud.cfgをダウンロードするには、[ここをクリックしてください](https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/cfg/centos/cloud.cfg)。
2. `/etc/cloud/cloud.cfg` の内容を、ダウンロードしたcloud.cfgファイルの内容に置き換えます。


### syslogユーザーの追加
次のコマンドを実行して、syslogユーザーを追加します。
```shellsession
useradd syslog
```


### システムの起動時にcloud-initサービスを自動実行させる方法
- **OSがsystemdを使用する場合、次のコマンドを実行します。**
<dx-alert infotype="explain" title="">
OSがsystemdを使用しているかどうかを確認するには、`strings /sbin/init | grep "/lib/system"`コマンドを実行できます。メッセージが返された場合は、OSがsystemdを使用していることを意味します。
</dx-alert>
- OSが**UbuntuまたはDebianの場合は、次のコマンドを実行する必要があります。**
```shellsession
 ln -s /usr/local/bin/cloud-init /usr/bin/cloud-init 
```
- **すべてのOSは、次のコマンドを実行する必要があります。**
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
- OSが**CentOSまたはRedhatの場合は、次のコマンドを実行する必要があります。**
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
- **OSがsystemdを使用する場合、次のコマンドを実行します。**
<dx-alert infotype="explain" title="">
OSがsystemdを使用しているかどうかを確認するには、`strings /sbin/init | grep "sysvinit"`コマンドを実行できます。メッセージが返された場合は、OSがsysvinitを使用していることを意味します。
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
::: ソフトウェアソースから\scloud-init\sパッケージを使用する[](id:SoftSources)
### cloud-initのインストール

次のコマンドを実行して、cloud-initをインストールします。
```shellsession
apt-get/yum install cloud-init
```
<dx-alert infotype="explain" title="">
デフォルトでは、apt-getまたはyumコマンドでインストールされるcloud-initは、現在のOSで設定されたソフトウェアソース中のデフォルトcloud-initバージョンを使用します。 この方法でインストールされたイメージを使用して作成したインスタンスは、一部の設定項目が予想通りに初期化されない可能性があるため、 [手動でcloud-initソースコードパッケージをダウンロード](#ManualDown)してサービスをインストールすることをお勧めします。
</dx-alert>



### cloud-init設定ファイル[](id:cloud-init)の変更
1. OSの違いに応じて、cloud.cfgをダウンロードします。
 - Ubuntu OSのcloud.cfgをダウンロードするには、[ここをクリックしてください](https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/cfg/ubuntu/cloud.cfg)。
 - CentOSのcloud.cfgをダウンロードするには、[ここをクリックしてください](https://gerryguan-1306210569.cos.ap-chongqing.myqcloud.com/cloud-init/cfg/centos/cloud.cfg)。
2. `/etc/cloud/cloud.cfg` の内容を、ダウンロードしたcloud.cfgファイルの内容に置き換えます。
:::
</dx-tabs>



## 関連する操作


<dx-alert infotype="notice" title="">
以下の操作が完了した後、サーバーを再起動しないでください。再起動した場合は、以下の操作を再実行する必要があります。
</dx-alert>


1. 次のコマンドを実行して、cloud-initが正しく設定されているかどうかを確認します。
```shellsession
cloud-init init --local
```
次のようなメッセージが返却された場合、cloud-initの設定が完了したことがわかります。
```shellsession
Cloud-init v. 20.1.0011 running 'init-local' at Fri, 01 Apr 2022 01:26:11 +0000. Up 38.70 seconds.
```
2. 次のコマンドを実行し、cloudinitのキャッシュをクリアします。
```shellsession
rm -rf /var/lib/cloud
```
3. Ubuntu OSまたはDebian OSについて、以下のコマンドを実行します。
``` shellsession
rm -rf /etc/network/interfaces.d/50-cloud-init.cfg
```
4. Ubuntu OSまたはDebian OSの場合、`/etc/network/interfaces`の内容を次のように変更します：
```shellsession
# This file describes the network interfaces available on your system
# and how to activate them. For more information, see interfaces(5).
source /etc/network/interfaces.d/*
```

## 付録
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
