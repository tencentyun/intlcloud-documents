## 작업 시나리오

본 문서는 Windows Server 2012 R2 64비트 운영 체제를 예로, Windows 운영 체제에서 Cloudbase-Init를 설치하는 방법에 대해 안내합니다.

<span id="PreparationSoftware"></span>
## 소프트웨어 준비
Cloudbase-Init 를 설치하기 위해 다음의 소프트웨어가 필요합니다.

| 소프트웨어 명칭 | 획득 경로 | 설명 |
|---------|---------|---------|
| CloudbaseInitSetup_X_X_XX_xXX.msi | 실제 사용하는 운영 체제 비트에 따라 상응하는 Cloudbase-Init 설치 패키지를 다운로드합니다: <ul style="margin: 0;"><li>안정 버전: 해당 버전의 설치 패키지를 사용할 것을 권장합니다<ul style="margin: 0;"><li>Windows 64비트 운영 체제: [다운로드](https://www.cloudbase.it/downloads/CloudbaseInitSetup_Stable_x64.msi)</li><li>Windows 32비트 운영 체제: [다운로드](https://www.cloudbase.it/downloads/CloudbaseInitSetup_Stable_x86.msi)</li></ul></li><li>Beta 버전</li></ul>자세한 정보는 [Cloudbase-Init 공식 홈페이지](http://www.cloudbase.it/cloud-init-for-windows-instances/)를 참조 바랍니다. | Cloudbase-Init 설치에 사용합니다.  |
| TencentCloudRun.ps1 | [ 다운로드](https://cloudinit-1251783334.cosgz.myqcloud.com/TencentCloudRun.ps1) | - |
| localscripts.py | [다운로드](https://cloudinit-1251783334.file.myqcloud.com/localscripts.py) | Cloudbase-Init 의 정상적인 운행을 보장하기 위해 사용합니다. |

## 작업 순서

### Cloudbase-Init 설치

1. 운영 체제 인터페이스에서 Cloudbase-Init 설치 패키지를 더블 클릭하여 엽니다.
2. 아래 이미지와 같이, 보안 경고 팝업 창에서 [실행]을 클릭하여 Cloudbase-Init 설치 인터페이스에 진입합니다.
![](https://main.qcloudimg.com/raw/3249309f71fccaf73feeaa5bb55301c3.png)
3. [Next]를 클릭합니다.
4. [I accept the terms in the License Agreement]를 선택하고 [Next]를 두 번 클릭합니다.
5. 아래 이미지와 같이, 'Configuration options' 인터페이스에서 '**Serial port for logging**'을 '**COM1**'로 설정하고, 'Run Cloudbase-Init service as LocalSystem'을 선택한 뒤 [Next]를 클릭합니다.
![](https://main.qcloudimg.com/raw/a772c35958cdf3be511dab58f730e7be.png)
6. [Install]을 클릭하여 Cloudbase-Init 를 설치합니다.
7. 아래 이미지와 같이, Cloudbase-Init 가 설치되면 [Finish]를 클릭해 Cloudbase-Init 설치 인터페이스를 닫습니다.
>! Cloudbase-Init 설치 인터페이스를 닫을 때, 체크 박스를 선택하거나 Sysprep를 실행하지 마세요.
>
![](https://main.qcloudimg.com/raw/d2d6c30def7812af9d7e484f5e8ccaa9.png)

### cloudbase-init 구성 파일 수정 

1. ‘cloudbase-init.conf’ 구성 파일을 엽니다.
‘cloudbase-init.conf’ 구성 파일의 경로는 ‘C:\Program Files\Cloudbase Solutions\Cloudbase-Init\conf’ 로 기본 설정되어 있습니다. 
2. ‘cloudbase-init.conf’ 구성 파일을 아래 내용과 같이 교체합니다.
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
3. ‘TencentCloudRun.ps1’ 스크립트를 ‘C:\Program Files\Cloudbase Solutions\Cloudbase-Init\LocalScripts’ 경로에 복사합니다.
4.`TencentCloudRun.ps1` 스크립트를 우클릭하고 [속성]을 선택한 후 아래와 같이 팝업 창에서 실행 가능한 사용 권한을 확인하십시오.
![](https://main.qcloudimg.com/raw/3a3a31fc4d0dbd58cacb9211f7a97e79.png)

- [Unblock]을 선택하고 [OK]를 클릭하십시오.
- [Unblock] 옵션이 없는 경우, 이 단계를 건너뛰십시오.
5. ‘C:\Program Files\Cloudbase Solutions\Cloudbase-Init\Python\Lib\site-packages\cloudbaseinit\plugins\common’ 경로에 있는 ‘localscripts.py’ 를 [소프트웨어 준비]의 ‘localscripts.py’ 파일로 교체합니다.
