## Cloud-init

### What is cloud-init?
Cloud-init is an open source tool that runs inside a CVM instance as a non-resident service. It is executed at startup and exits immediately after execution. It does not listen to any ports.
All the Linux public images of Tencent Cloud are pre-installed with the cloud-init service. You need to run the service as the root user because the service is mainly used for the initialization of CVM instances such as configuring DNS, hostname, and IP, and the execution of some custom scripts that users specify to be executed during the first boot when creating the CVM instances.

### How do I check whether the cloud-init service inside a Linux instance is working properly?

<span id="checkcloud-init"></span>
#### Checking the operation of cloud-init
First, log in to the instance and execute the following commands to see if any error is returned. If the execution result is returned, it means that the service is running normally. Otherwise, an error will be returned. Please troubleshoot according to the error message.
1. Delete the cloud-init cache directory.
```
rm -rf /var/lib/cloud
```
2. Perform complete cloud-init initialization.
```
cloud-init init --local
```
3. Pull data from the configured data source.
```
cloud-init init
```
4. Cloud-init initialization involves multiple stages. To ensure sufficient dependency between the stages, config stage is specified for the cloud-init modules.
```
cloud-init modules --mode=config
```
5. Specify final stage for the cloud-init modules.
```
cloud-init modules --mode=final
```

###  What initialization operations does cloud-init perform on instances?

Tencent Cloud implements all instance initialization operations through cloud-init, ensuring the transparency of the operations inside an instance. The following briefly covers some initialization operations. For more details, see [cloud-init documentation](http://cloudinit.readthedocs.io/en/latest/).

<table>
<tr><th style="width: 25%;">Initialization operation</th><th style="width: 25%;">Default behavior</th><th style="width: 25%;">Customization</th><th style="width: 25%;">Notes</th></tr>
<tr>
	<td>hostname initialization</td>
	<td>During <b>the first boot</b> of an instance, cloud-init will set the hostname of the instance according to the hostname information in <code>vendor_data.json</code>.</td>
	<td>If you create or reinstall an instance with a custom image and you want to keep the custom hostname of the image, you can delete the configuration, <code>- scripts-user</code>, from <code>/etc/cloud/cloud.cfg</code> before creating the custom image.</td>
	<td>After you disable <code>- scripts-user</code>, the initialization script, <code>/var/lib/cloud/instance/scripts/runcmd</code>, inside the instance will not be run. Disabling the configuration will also affect the initialization of other sub-items such as the installation of cloud monitor and cloud security and software source settings. Also, the custom script will not be run when you create the CVM.</td>
</tr>

<tr>
	<td>/etc/hosts initialization</td>
	<td>During <b>the first boot</b> of an instance, cloud-init will initialize <code>/etc/hosts</code> to <code>127.0.0.1 $hostname</code> by default.</td>
	<td>If you create or reinstall an instance with a custom image and you want to keep the custom /etc/hosts setting of the image, you can delete the configuration, <code>- scripts-user</code>, from <code>/etc/cloud/cloud.cfg</code> before creating the custom image.</td>
	<td>
		<ul style="margin: 0px;">
			<li>After you disable <code>- scripts-user</code>, the initialization script, <code>/var/lib/cloud/instance/scripts/runcmd</code>, inside the instance will not be run. Disabling the configuration will also affect the initialization of other sub-items such as the installation of cloud monitor and cloud security and software source settings. Also, the custom script will not be run when you create the CVM.</li>
			<li>Every time the CVM restarts，the <code>/etc/hosts</code> settings of some existing CVMs will be overwritten. To solve the issue, see <a href="https://intl.cloud.tencent.com/document/product/213/32504">Modifying etc/hosts Configuration of Linux Instance</a></li>。
		</ul>
	</td>
</tr>

<tr>
	<td>DNS initialization (non-DHCP scenario)</td>
	<td>During <b>the first boot</b> of an instance, cloud-init will set the DNS of the instance according to the nameservers information in <code>vendor_data.json</code>.</td>
	<td>If you create or reinstall an instance with a custom image and you want to keep the custom DNS setting of the image, you can delete the configuration, <code>- resolv_conf</code> and <code>unverified_modules: ['resolv_conf']</code>, from <code>/etc/cloud/cloud.cfg</code> before creating the custom image.</td>
	<td>None.</td>
</tr>

<tr>
	<td>Software source initialization</td>
	<td>During <b>the first boot</b> of an instance, cloud-init will set the software source of the instance according to the write_files information in <code>vendor_data.json</code>.</td><td>If you create or reinstall an instance with a custom image and you want to keep the custom software source setting of the image, you can delete the configuration, <code>- write-files</code>, from <code>/etc/cloud/cloud.cfg</code> before creating the custom image.</td>
	<td>None.</td>
</tr>

<tr>
	<td>NTP initialization</td>
	<td>During <b>the first boot</b> of an instance, cloud-init will set the NTP server configuration of the instance according to the NTP server information in <code>vendor_data.json</code> and start the NTP service.</td>
	<td>If you create or reinstall an instance with a custom image and you want to keep the custom NTP configuration of the image, you can delete the configuration, <code>- ntp<code/>, from <code>/etc/cloud/cloud.cfg</code> before creating the custom image.</td>
	<td>None.</td>
</tr>

<tr>
	<td>Password initialization</td>
	<td>During <b>the first boot</b> of an instance, cloud-init will set the default account password of the instance according to the chpasswd information in <code>vendor_data.json</code>.</td>
	<td>If you create or reinstall an instance with a custom image and you want to keep the custom default password of the image, you can delete the configuration, <code>- set-passwords</code>, from <code>/etc/cloud/cloud.cfg</code> before creating the custom image.</td>
	<td>None.</td>
</tr>

<tr>
	<td>Key binding</td>
	<td>During <b>the first boot</b> of an instance, cloud-init will set the default account key of the instance according to the ssh_authorized_keys information in <code>vendor_data.json</code>.</td>
	<td>If you create or reinstall an instance with a custom image and you want to keep the custom default key of the image, you can delete the configuration, <code>- users-groups</code>, from <code>/etc/cloud/cloud.cfg</code> before creating the custom image.</td>
	<td> If you manually bind the instance to a key inside the instance, the previous key will be overwritten when the key binding operation is performed via the console. </td>
</tr>

<tr>
	<td>Network initialization (non-DHCP scenario)</td>
	<td>During <b>the first boot</b> of an instance, cloud-init will set the IP, Gateway, Mask, etc., according to the information in <code>network_data.json</code>.</td>
	<td>If you create or reinstall an instance with a custom image and you want to keep the custom network information of the image, you can add <code>network: {config: disabled}</code> to <code>/etc/cloud/cloud.cfg</code> before creating the custom image.</td>
	<td>None.</td>
</tr>
</table>

### How do I fix issues related to cloud-init? 

#### 1. Error due to the uninstallation of the cloud-init dependencies
- Problem description:
When commands are used to check whether the cloud-init service is working properly, the following error is returned:
```
Traceback (most recent call last):
  File "/usr/bin/cloud-init", line 5, in 
    ********
    raise DistributionNotFound(req)
pkg_resources.DistributionNotFound: pyyaml
```
- Problem analysis:
“pkg_resources.DistributionNotFound: xxxxx” indicates that the cloud-init dependencies have been uninstalled.
- Solution:
 1. Reinstall the dependencies.
 2. Follow [Checking the operation of cloud-init](#checkcloud-init) to see if the error is returned again.

#### 2. Error due to the modification of the default Python interpreter
- Problem description:
An error is returned when cloud-init is run on startup.
- Problem analysis:
When cloud-init is installed, Python 2 is used as the default Python interpreter, which means that symbolic links, `/usr/bin/python` and `/bin/python`, are linked to Python 2. Users may change the default Python interpreter to Python 3 inside the instance by directing the symbolic links, `/usr/bin/python` and `/bin/python`, to Python 3. Due to compatibility issues, an error will be returned when cloud-init is run on startup.
- Solution:
 1. Modify the Python interpreter specified in the  `/usr/bin/cloud-init` file by changing `#/usr/bin/python` or `#/bin/python` to `#! user/bin/python`.
> Do not use symbolic links. Point directly to a specific interpreter.
>
 2. Follow [Checking the operation of cloud-init](#checkcloud-init) to see if the error is returned again.

## Cloudbase-Init

### What is Cloudbase-Init?
Like cloud-init, Cloudbase-Init is a bridge by which you can communicate with Windows CVM instances. The Cloudbase-Init service is run when an instance boots up for the first time. The service will read the  initialization configuration information of the instance and initialize it. Following operations such as resetting password and modifying IP addresses are also done via Cloudbase-Init.

### How do I check whether the Cloudbase-Init service inside a Windows instance is working properly?

<span id="checkcloudbase-init"></span>
#### Checking the operation of the Cloudbase-Init service:
1. Log in to the instance.
> If you forget your password or fail to reset your password because of Cloudbase-Init service exceptions, you can reset your password by following [step 2](#step02). 
>
2. <span id="step02">Open **Control panel** > **Administrative tools** > **Services**.
3. Find the Cloudbase-Init service, right-click it, and go to **Properties**. </span>
 - Check “Startup type” and make sure it is set to “Automatic”.
 - View “Logon identity” and ensure that “Local System account” is selected.
 - Manually start the Cloudbase-Init service and see if any error is returned.
If any error is returned, you need to fix the issue first and check whether you have installed any security software which may stop Cloudbase-Init from performing related operations. 
 - Open the registry, locate all “LocalScriptsPlugin”, and make sure its value is 2.
 - Check whether CD-ROM loading is disabled. If there is an optical disc drive as shown in the figure below, it means that the loading has not been disabled; otherwise, it means that it has been disabled and needs to be enabled.

### How do I fix common issues related to Cloudbase-Init?
#### Failed to reset password during initialization
- Possible reasons:
 - The Cloudbase-Init account password is manually changed, which results in the failure to start the Cloudbase-Init service, which further led to the failure of operations such as resetting password during initialization.
 - The Cloudbase-Init service is disabled, which led to the failure of operations such as resetting password during initialization.
 - The security software installed stops the Cloudbase-Init service from resetting password so that the operation returns a successful result but actually failed.
- Solution:
Follow the corresponding solution to each possible reason to fix the issue.
 1. Change the Cloudbase-Init service to LocalSystem service. For details, see [step 2](#step02) in [Checking the operation of the Cloudbase-Init service](#checkcloudbase-init). 
 2. Change the startup type of the Cloudbase-Init service to automatic. For details, see [step 2](#step02) in [Checking the operation of the Cloudbase-Init service](#checkcloudbase-init).
 3. Uninstall the security software involved or add the relevant operations of the Cloudbase-Init service to the white list of the security software.
