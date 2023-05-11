## 概要

このドキュメントでは、Windows Server 2012 R2 64ビットOSを例に、Windows OSでのCloudbase-Initをインストールする方法について説明します。

<span id="PreparationSoftware"></span>
## 必要なソフトウェア
Cloudbase-Initをインストールには、以下のソフトウェアが必要です。

| ソフトウェア名 | 入手方法 | 説明 |
|---------|---------|---------|
| CloudbaseInitSetup_X_X_XX_xXX.msi | 実際にご利用のOSのビット数に応じて、対応するCloudbase-Initインストールパッケージをダウンロードしてください。<ul style="margin: 0;"><li>安定版：このバージョンのインストールパッケージをお勧めします<ul style="margin: 0;"><li>Windows 64ビット OS：インストールパッケージを入手するには、[ここをクリックしてください](https://www.cloudbase.it/downloads/CloudbaseInitSetup_Stable_x64.msi)</li><li>Windows 32ビット OS：インストールパッケージを入手するには、[ここをクリックしてください](https://www.cloudbase.it/downloads/CloudbaseInitSetup_Stable_x86.msi)</li></ul></li><li>ベータ版</li></ul>詳しくは[Cloudbase-Init 公式サイト](http://www.cloudbase.it/cloud-init-for-windows-instances/)をご覧ください。 |  Cloudbase-Initのインストールに使用されます。  |
| TencentCloudRun.ps1 | インストールパッケージを入手するには、[ここをクリックしてください](https://cloudinit-1251783334.cosgz.myqcloud.com/TencentCloudRun.ps1) | - |
| localscripts.py | インストールパッケージを入手するには、[ここをクリックしてください](https://cloudinit-1251783334.file.myqcloud.com/localscripts.py) | Cloudbase-Initが正常に起動するために使用されます。|

## 操作手順

### Cloudbase-Initのインストール

1. OS画面で、Cloudbase-Initインストールパッケージをダブルクリックして開きます。
2. セキュリティの警告メッセージが出たら**Run**を押して続行してください。次の図に示すように、Cloudbase-Initインストール画面へ進みます。
![](https://main.qcloudimg.com/raw/3249309f71fccaf73feeaa5bb55301c3.png)
3. **Next**をクリックします。
4. “I accept the terms in the License Agreement”にチェックを入れて、**Next**を2回クリックします。
5. 「Configuration options」画面で、「**Serial port for logging**」を「**COM1**」に設定し、「**Run Cloudbase-Init service as LocalSystem**」を選択して、**Next**をクリックします。次図に示すように：
![](https://main.qcloudimg.com/raw/a772c35958cdf3be511dab58f730e7be.png)
6. **Install**をクリックして、Cloudbase-Initをインストールします。
7. Cloudbase-Init のインストールが完了した後、次の図に示すように、**Finish**をクリックしてCloudbase-Initインストール画面を閉じます。
>! Cloudbase-Initインストール画面を閉じる時、チェックボックスを選択したり、Sysprepを実行したりしないでください。
>
![](https://main.qcloudimg.com/raw/d2d6c30def7812af9d7e484f5e8ccaa9.png)

### cloudbase-init 構成ファイルの変更 

1. `cloudbase-init.conf`構成ファイルを開きます。
`cloudbase-init.conf` 構成ファイルは、デフォルトで `C:\Program Files\Cloudbase Solutions\Cloudbase-Init\conf` に保存されます。 
2. `cloudbase-init.conf` 構成ファイルの内容を次のように置き換えます。
```
[DEFAULT]
username=Administrator
groups=Administrators
inject_user_password=true
config_drive_raw_hhd=true
config_drive_cdrom=true
config_drive_vfat=true
bsdtar_path=C:\Program Files\Cloudbase Solutions\Cloudbase-Init\bin\bsdtar.exe
mtools_path=C:\Program Files\Cloudbase Solutions\Cloudbase-Init\bin\
san_policy=OnlineAll
metadata_services=cloudbaseinit.metadata.services.configdrive.ConfigDriveService,cloudbaseinit.metadata.services.ec2service.EC2Service
#,cloudbaseinit.metadata.services.httpservice.HttpService
#,cloudbaseinit.metadata.services.maasservice.MaaSHttpService
metadata_base_url=http://169.254.0.23/
ec2_metadata_base_url=http://169.254.0.23/
retry_count=2
retry_count_interval=5
plugins=cloudbaseinit.plugins.windows.extendvolumes.ExtendVolumesPlugin,cloudbaseinit.plugins.common.networkconfig.NetworkConfigPlugin,cloudbaseinit.plugins.common.sethostname.SetHostNamePlugin,cloudbaseinit.plugins.common.setuserpassword.SetUserPasswordPlugin,cloudbaseinit.plugins.common.localscripts.LocalScriptsPlugin,cloudbaseinit.plugins.common.userdata.UserDataPlugin
verbose=true
debug=true
logdir=C:\Program Files\Cloudbase Solutions\Cloudbase-Init\log\
logfile=cloudbase-init.log
default_log_levels=comtypes=INFO,suds=INFO,iso8601=WARN,requests=WARN
#logging_serial_port_settings=COM1,115200,N,8
mtu_use_dhcp_config=true
ntp_use_dhcp_config=true
first_logon_behaviour=no
netbios_host_name_compatibility=false
allow_reboot=true
activate_windows=true
kms_host="kms.tencentyun.com"
local_scripts_path=C:\Program Files\Cloudbase Solutions\Cloudbase-Init\LocalScripts\
C:\powershell
PS C:\Set-ExecutionPolicy Unrestricted
volumes_to_extend=1,2
```
3. `TencentCloudRun.ps1`スクリプトを`C:\Program Files\Cloudbase Solutions\Cloudbase-Init\LocalScripts`のパスにコピーします。
4. `TencentCloudRun.ps1`スクリプトを右クリックし、**プロパティ**を選択して、ポップアップウィンドウでスクリプトに実行権限があるかどうかを確認します。 次図に示すように：
![](https://main.qcloudimg.com/raw/3a3a31fc4d0dbd58cacb9211f7a97e79.png)
 - [Unblock] オプションがある場合、 [Unblock] にチェックを入れて、[OK]をクリックして終了する必要があります。 
 - [Unblock ] オプションが存在しない場合は、この手順をスキップしてください。
5. `C:\Program Files\Cloudbase Solutions\Cloudbase-Init\Python\Lib\site-packages\cloudbaseinit\plugins\common`パスにある`localscripts.py`を[必要なソフトウェア](#PreparationSoftware) 中の`localscripts.py`ファイルに置き換えます。
