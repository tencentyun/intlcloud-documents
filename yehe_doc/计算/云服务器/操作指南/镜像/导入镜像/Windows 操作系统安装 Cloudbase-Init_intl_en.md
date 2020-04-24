## Scenario

This document uses the Windows Server 2012 R2 64-bit operating system as an example to describe how to install cloudbase-init on Windows.

<span id="PreparationSoftware"></span>
## Software
The following table describes the software programs required for installing cloudbase-init.

| Software | How to Obtain It | Description |
|---------|---------|---------|
| CloudbaseInitSetup_X_X_XX_xXX.msi | Download the cloudbase-init installation package based on the used operating system.<ul style="margin: 0;"><li>Stable version (recommended)<ul style="margin: 0;"><li>Windows 64-bit operating system: [Click here](https://www.cloudbase.it/downloads/CloudbaseInitSetup_Stable_x64.msi) to obtain the installation package.</li><li>Windows 32-bit operating system: [Click here](https://www.cloudbase.it/downloads/CloudbaseInitSetup_Stable_x86.msi) to obtain the installation package.</li></ul></li><li>Beta version</li></ul>For details, visit the [cloudbase-init official website](http://www.cloudbase.it/cloud-init-for-windows-instances/). | It is used to install cloudbase-init. |
| TencentCloudRun.ps1 | [Click here](http://cloudinit-1251783334.cosgz.myqcloud.com/TencentCloudRun.ps1) to obtain the installation package. | - |
| localscripts.py | [Click here](http://cloudinit-1251783334.file.myqcloud.com/localscripts.py) to obtain the installation package. | It is used to ensure that cloudbase-init starts properly. |

## Directions

### Installing cloudbase-init

1. On the desktop, double-click the cloudbase-init installation package.
2. In the warning dialog box that appears, click **Run** to start the cloudbase-init setup wizard, as shown in the following figure.
![](https://main.qcloudimg.com/raw/bdeb8ff4370dc6da38da6749154e449f.png)
3. Click **Next**.
4. Select **I accept the terms in the License Agreement** and click **Next** for the following two operations.
5. On the **Configuration options** page, set **Serial port for logging** to **COM1** and click **Next**, as shown in the following figure.
![](https://main.qcloudimg.com/raw/a41580e9b21e4550245b661b44682937.png)
6. Click **Install**.
7. After cloudbase-init is installed, click **Finish** to exit the cloudbase-init setup wizard, as shown in the following figure.
> When exiting the cloudbase-init setup wizard, do not select any checkboxes nor run Sysprep.
>
![](https://main.qcloudimg.com/raw/d2d6c30def7812af9d7e484f5e8ccaa9.png)

### Modifying the cloudbase-init configuration file 

1. Open the `cloudbase-init.conf` configuration file.
The `cloudbase-init.conf` configuration file is saved under `C:\Program Files\Cloudbase Solutions\Cloudbase-Init\conf` by default. 
2. Replace the content of the `cloudbase-init.conf` configuration file with the following:
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
3. Copy the `TencentCloudRun.ps1` script to `C:\Program Files\Cloudbase Solutions\Cloudbase-Init\LocalScripts`.
4. Replace `localscripts.py` in `C:\Program Files\Cloudbase Solutions\Cloudbase-Init\Python\Lib\site-packages\cloudbaseinit\plugins\common` with the `localscripts.py` file mentioned in [Software](#PreparationSoftware).
