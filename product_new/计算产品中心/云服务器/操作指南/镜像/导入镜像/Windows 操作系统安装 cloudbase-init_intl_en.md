## Downloading the Cloudbase-Init installer

Download the Cloudbase-Init installer corresponding to your operating system architecture. For details, visit [Cloudbase-Init Official Site](http://www.cloudbase.it/cloud-init-for-windows-instances/).

Cloudbase-init has the following versions:
- Stable version (recommended)
Download via the following links:
	- 64-bit Windows: https://www.cloudbase.it/downloads/CloudbaseInitSetup_Stable_x64.msi
	- 32-bit Windows: https://www.cloudbase.it/downloads/CloudbaseInitSetup_Stable_x86.msi
- Beta version

## Installing Cloudbase-Init

When installing Cloudbase-Init, please note:
- **In the “Configuration options” window, set “Serial port for logging” to “COM1” as shown below.**
![Alt text](https://main.qcloudimg.com/raw/beaca64e8484ec7e9880703cad400717.png)
- **At the final step of the installation, do not check any box as shown below: **
![Alt text](https://main.qcloudimg.com/raw/aceec91df6a51db2eca775f3350de88c.png)

## Modifying the Cloudbase-Init configuration file 

1. Open the Cloudbase-Init configuration file at \PATH\TO\Cloudbase Solutions\Cloubase-Init\conf\cloudbase-init.conf.
2. Replace the content in the file with the following:
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
3. Copy the [TencentCloudRun.ps1](http://cloudinit-1251783334.cosgz.myqcloud.com/TencentCloudRun.ps1) script to the C:\Program Files\Cloudbase Solutions\Cloudbase-Init\LocalScripts\ directory.
