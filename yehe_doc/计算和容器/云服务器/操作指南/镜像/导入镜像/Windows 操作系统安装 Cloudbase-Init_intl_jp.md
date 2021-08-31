## ユースケース

このドキュメントでは、Windows Server 2012 R2 64ビットOSを例に、Windows OSでのCloudbase-Initをインストールする方法について説明します。

<span id="PreparationSoftware"></span>
## 必要なソフトウェア
Cloudbase-Initをインストールには、以下のソフトウェアが必要です。

| ソフトウェア名 | 入手方法 | 説明 |
|---------|---------|---------|
| CloudbaseInitSetup_X_X_XX_xXX.msi | 実際にご利用のOSのビット数に応じて、対応するCloudbase-Initインストールパッケージをダウンロードしてください。<ul style="margin: 0;"><li>安定版：このバージョンのインストールパッケージをお勧めします<ul style="margin: 0;"><li>Windows 64ビット OS：：インストールパッケージを入手するには、[ここをクリックしてください](https://www.cloudbase.it/downloads/CloudbaseInitSetup_Stable_x64.msi)</li><li>Windows 32ビット OS：インストールパッケージを入手するには、[ここをクリックしてください](https://www.cloudbase.it/downloads/CloudbaseInitSetup_Stable_x86.msi)</li></ul></li><li>ベータ版</li></ul>詳細について、 [Cloudbase-Init公式サイト](http://www.cloudbase.it/cloud-init-for-windows-instances/)をご参照ください。 |  Cloudbase-Initのインストールに使用されます。  |
| TencentCloudRun.ps1 | インストールパッケージを入手するには、[ここをクリックしてください](https://cloudinit-1251783334.cosgz.myqcloud.com/TencentCloudRun.ps1) | - |
| localscripts.py | インストールパッケージを入手するには、[ここをクリックしてください](https://cloudinit-1251783334.file.myqcloud.com/localscripts.py) | Cloudbase-Initが正常に起動できるために使用されます。|

## 操作手順

### Cloudbase-Initのインストール

1. OS画面で、Cloudbase-Initインストールパッケージをダブルクリックして開きます。
2. ポップアップされたセキュリティ警告メッセージボックスで、次の図に示すように、【Run 】をクリックしてCloudbase-Initインストール画面に入ります。
![](https://main.qcloudimg.com/raw/3249309f71fccaf73feeaa5bb55301c3.png)
3. 【Next】をクリックします。
4. 【I accept the terms in the License Agreement】にチェックを入れて、【Next】を2回クリックします。
5. 「Configuration options」画面で、「**Serial port for logging**」を「**COM1**」に設定し、「**Run Cloudbase-Init service as LocalSystem**」を選択して、【Next】をクリックします。次図に示すように：
![](https://main.qcloudimg.com/raw/a772c35958cdf3be511dab58f730e7be.png)
6. 【Install】をクリックして、Cloudbase-Initをインストールします。
7. Cloudbase-Init のインストールが完了した後、次の図に示すように、【Finish】をクリックしてCloudbase-Initインストール画面を閉じます。
>! Cloudbase-Initインストール画面を閉じる時、チェックボックスを選択したり、Sysprepを実行したりしないでください。
>
![](https://main.qcloudimg.com/raw/d2d6c30def7812af9d7e484f5e8ccaa9.png)

### cloudbase-init 構成ファイルの変更 

1. 構成ファイル`cloudbase-init.conf`を開きます。
構成ファイル`cloudbase-init.conf`のデフォルトパスは`C:\Program Files\Cloudbase Solutions\Cloudbase-Init\conf`となります 
2. 構成ファイル`cloudbase-init.conf`の内容を以下の内容に置き換えます。
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
metadata_services=cloudbaseinit.metadata.services.configdrive.ConfigDriveService
plugins=cloudbaseinit.plugins.windows.extendvolumes.ExtendVolumesPlugin,cloudbaseinit.plugins.common.networkconfig.NetworkConfigPlugin,cloudbaseinit.plugins.common.sethostname.SetHostNamePlugin,cloudbaseinit.plugins.common.setuserpassword.SetUserPasswordPlugin,cloudbaseinit.plugins.common.localscripts.LocalScriptsPlugin,cloudbaseinit.plugins.common.userdata.UserDataPlugin
verbose=true
debug=true
logdir=C:\Program Files\Cloudbase Solutions\Cloudbase-Init\log\
logfile=cloudbase-init.log
default_log_levels=comtypes=INFO,suds=INFO,iso8601=WARN,requests=WARN
logging_serial_port_settings=COM1,115200,N,8
mtu_use_dhcp_config=true
ntp_use_dhcp_config=true
first_logon_behaviour=no
netbios_host_name_compatibility=false
allow_reboot=false
activate_windows=true
kms_host="kms.tencentyun.com"
local_scripts_path=C:\Program Files\Cloudbase Solutions\Cloudbase-Init\LocalScripts\
```
3. `TencentCloudRun.ps1`スクリプトを`C:\Program Files\Cloudbase Solutions\Cloudbase-Init\LocalScripts`のパスにコピーします。
4. `TencentCloudRun.ps1`スクリプトを右クリックし、【プロパティ】を選択して、ポップアップウィンドウでスクリプトに実行権限があるかどうかを確認します。 次図に示すように：
![](https://main.qcloudimg.com/raw/3a3a31fc4d0dbd58cacb9211f7a97e79.png)
 - [Unblock] オプションがある場合、 [Unblock] にチェックを入れて、[OK]をクリックして終了する必要があります。 
 - [Unblock ] オプションが存在しない場合は、この手順をスキップしてください。
5. `C:\Program Files\Cloudbase Solutions\Cloudbase-Init\Python\Lib\site-packages\cloudbaseinit\plugins\common`パスにある`localscripts.py`を[必要なソフトウェア](#PreparationSoftware) 中の`localscripts.py`ファイルに置き換えます。
