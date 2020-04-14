## cloudbase-init 툴 설치 패키지 다운로드

실제 사용하고 있는 운영 체제 비트수에 따라 대응하는 버전의 cloudbase-init 툴 설치 패키지를 다운로드하여 설치하십시오. 자세한 내용은 [Cloudbase-Init 공식 홈페이지](http://www.cloudbase.it/cloud-init-for-windows-instances/)를 참조하십시오.

Cloudbase-init은 아래의 버전으로 나뉩니다.
- 안정적인 버전: 해당 버전 설치 패키지로 설치할 것을 권장합니다.
획득 경로는 다음과 같습니다.
	- Windows 64비트 운영 체제: https://www.cloudbase.it/downloads/CloudbaseInitSetup_Stable_x64.msi
	- Windwos 32비트 운영 체제: https://www.cloudbase.it/downloads/CloudbaseInitSetup_Stable_x86.msi
- Beta 버전

## cloudbase-init 설치

cloudbase-init 설치 과정에서 아래의 두 가지에 유의하십시오.
- **"Configuration options" 창에서 아래 그림의 콘텐츠에 따라 설정하십시오. 즉 "Serial port for logging"을 "COM1"로 설정합니다.**
![Alt text](https://main.qcloudimg.com/raw/beaca64e8484ec7e9880703cad400717.png)
- **설치 완료의 마지막 단계에서 어떠한 체크 박스에도 체크 표시하지 말고 Sysprep를 실행하지 마십시오. 아래 그림 참조**
![Alt text](https://main.qcloudimg.com/raw/aceec91df6a51db2eca775f3350de88c.png)

## cloudbase-init 설정 파일 수정 

1. cloudbase-init 설정 파일(설정 파일의 경로는 \PATH\TO\Cloudbase Solutions\Cloubase-Init\conf\cloudbase-init.conf 입니다)을 엽니다.
2. cloudbase-init 설정 파일을 아래의 콘텐츠로 대체합니다.
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
3. [TencentCloudRun.ps1](http://cloudinit-1251783334.cosgz.myqcloud.com/TencentCloudRun.ps1) 스크립트를 C:\Program Files\Cloudbase Solutions\Cloudbase-Init\LocalScripts\ 경로 아래로 카피합니다.
