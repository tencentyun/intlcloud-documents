## Overview

This document describes how to install Cloudbase-Init on the Windows Server 2012 R2 64-bit operating system.

<span id="PreparationSoftware"></span>
## Required Software
The following table describes the software required for installing Cloudbase-Init.

| Software | Download Link | Description |
|---------|---------|---------|
| CloudbaseInitSetup_X_X_XX_xXX.msi | Download the Cloudbase-Init installation package based on the operating system used.<ul style="margin: 0;"><li>Stable version (recommended)<ul style="margin: 0;"><li>Windows 64-bit operating system: [Click here](https://www.cloudbase.it/downloads/CloudbaseInitSetup_Stable_x64.msi) to download the installation package.</li><li>Windows 32-bit operating system: [Click here](https://www.cloudbase.it/downloads/CloudbaseInitSetup_Stable_x86.msi) to download the installation package.</li></ul></li><li>Beta version</li></ul>For details, see the [Cloudbase-Init official website](http://www.cloudbase.it/cloud-init-for-windows-instances/). | Used to install Cloudbase-Init |
| TencentCloudRun.ps1 | [Click here](https://cloudinit-1251783334.cosgz.myqcloud.com/TencentCloudRun.ps1) to download the installation package. | - |
| localscripts.py | [Click here](https://cloudinit-1251783334.file.myqcloud.com/localscripts.py) to download the installation package. | Used to ensure that Cloudbase-Init starts properly |

## Directions

### Installing Cloudbase-Init

1. On the desktop, double-click the Cloudbase-Init installation package.
2. In the dialog box, click **Run** to enter the Cloudbase-Init setup wizard, as shown below:
![](https://main.qcloudimg.com/raw/3249309f71fccaf73feeaa5bb55301c3.png)
3. Click **Next**.
4. Check **I accept the terms in the License Agreement** and click **Next** for the following two operations.
5. On the **Configuration options** page, set **Serial port for logging** to **COM1**, select **Run Cloudbase-Init service as LocalSystem** and click **Next**, as shown below:
![](https://main.qcloudimg.com/raw/a772c35958cdf3be511dab58f730e7be.png)
6. Click **Install**.
7. When the installation is completed, click **Finish** to close the Cloudbase-Init setup wizard, as shown below:
>! When closing the Cloudbase-Init setup wizard, do not check any checkbox or run Sysprep.
>
![](https://main.qcloudimg.com/raw/d2d6c30def7812af9d7e484f5e8ccaa9.png)

### Modifying the Cloudbase-Init configuration file 

1. Open the `cloudbase-init.conf` configuration file.
The `cloudbase-init.conf` configuration file is saved in `C:\Program Files\Cloudbase Solutions\Cloudbase-Init\conf` by default. 
2. Replace content in the `cloudbase-init.conf` configuration file with the following:
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
3. Copy the `TencentCloudRun.ps1` script to `C:\Program Files\Cloudbase Solutions\Cloudbase-Init\LocalScripts`.
4. Right-click the `TencentCloudRun.ps1` script, select **Properties**, and check for its executable permission in the pop-up window, as shown below:
![](https://main.qcloudimg.com/raw/3a3a31fc4d0dbd58cacb9211f7a97e79.png)
- Check **Unblock** and click **OK**.
- Skip this step if the **Unblock** option does not exist.
5. Replace `localscripts.py` in `C:\Program Files\Cloudbase Solutions\Cloudbase-Init\Python\Lib\site-packages\cloudbaseinit\plugins\common` with the `localscripts.py` file in [Required Software](#PreparationSoftware).
