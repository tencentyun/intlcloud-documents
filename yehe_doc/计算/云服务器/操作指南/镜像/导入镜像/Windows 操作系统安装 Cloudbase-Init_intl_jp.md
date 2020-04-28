## cloudbase-initツールインストールパッケージをダウンロードする

実際に使用しているOSのビット数に基づいて、対応するバージョンのcloudbase-initツールインストールパッケージをダウンロードし、インストールを行います。詳細については [Cloudbase-Init 公式サイト](http://www.cloudbase.it/cloud-init-for-windows-instances/)をご参照ください。

Cloudbase-init は以下のバージョンに分かれています。
- 安定版：このバージョンのインストールパッケージでインストールすることをお勧めします。
パスは以下の通り：
	- Windows 64ビット OS：https://www.cloudbase.it/downloads/CloudbaseInitSetup_Stable_x64.msi
	- Windwos 32ビット OS：https://www.cloudbase.it/downloads/CloudbaseInitSetup_Stable_x86.msi
- ベータ版

## cloudbase-initのインストール

cloudbase-initをインストールする際、以下の点にご注意ください：
- **「Configuration options」ウィンドウでは、下図の通りに構成を行ってください。すなわち「Serial port for logging」を「COM1」に設定します。**
![Alt text](https://main.qcloudimg.com/raw/beaca64e8484ec7e9880703cad400717.png)
- **インストールの最後のステップでは、チェックボックスにチェックを入れず、 Sysprepを実行しないでください。下図の示す通りです：**
![Alt text](https://main.qcloudimg.com/raw/aceec91df6a51db2eca775f3350de88c.png)

## cloudbase-init 構成ファイルを変更する 

1.  cloudbase-init 構成ファイル（構成ファイルのパスは：\PATH\TO\Cloudbase Solutions\Cloubase-Init\conf\cloudbase-init.conf）を開きます。
2. cloudbase-init の構成ファイルを以下の内容に置き換えます：
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
C:\powershell
PS C:\Set-ExecutionPolicy Unrestricted
```
3.  [TencentCloudRun.ps1](http://cloudinit-1251783334.cosgz.myqcloud.com/TencentCloudRun.ps1) スクリプトを C:\Program Files\Cloudbase Solutions\Cloudbase-Init\LocalScripts\ というパスの配下にコピーします。
