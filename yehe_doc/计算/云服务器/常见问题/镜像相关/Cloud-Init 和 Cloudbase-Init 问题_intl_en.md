## Cloud-init

### What is cloud-init?
Cloud-init is an open source tool that runs inside a CVM instance as a non-resident service. It is executed at startup and exits immediately after execution. It does not listen to any ports.
All the Linux public images of Tencent Cloud are pre-installed with the cloud-init service. You need to run the service as the root user because the service is mainly used for the initialization of CVM instances such as configuring DNS, hostname, and IP, and the execution of some custom scripts that users specify to be executed during the first boot when creating the CVM instances.

### How do I check whether the cloud-init service inside a Linux instance is working properly?


#### Troubleshooting cloud-init service errors[](id:checkcloud-init)

[Log in to a Linux instance using the standard login method (recommended)](https://www.tencentcloud.com/document/product/213/5436). Then, run the following commands in sequence and observe whether an error is reported. If the execution result is displayed, the service is running normally. Otherwise, the cause of the error will be reported. You can troubleshoot the error accordingly.
<dx-alert infotype="explain" title="">
This step only applies to CVM instances created with public Linux images. If you installed cloud-init by yourself, adjust the commands according to the actual situation.
</dx-alert>


1. Delete the cloud-init cache directory.
```shellsession
rm -rf /var/lib/cloud
```
2. Perform complete cloud-init initialization.
```shellsession
/usr/bin/cloud-init init --local
```
3. Pull data from the configured data source.
```shellsession
/usr/bin/cloud-init init
```
4. Cloud-init initialization involves multiple stages. To ensure sufficient dependencies between the stages, specify the config stage for the cloud-init modules.
```shellsession
/usr/bin/cloud-init modules --mode=config
```
5. Specify the final stage for the cloud-init modules.
```shellsession
/usr/bin/cloud-init modules --mode=final
```

### What initialization operations does cloud-init perform on instances?

Tencent Cloud implements all instance initialization operations through cloud-init, ensuring the transparency of the operations inside an instance. The following briefly covers some initialization operations. For more details, see [cloud-init documentation](http://cloudinit.readthedocs.io/en/latest/).

<table>
<tr>
    <th style="width: 18%;">Initialization Type</th>
    <th style="width: 25%;">Default Behavior</th>
    <th style="width: 27%;">Customization</th>
    <th style="width: 30%;">Notes</th>
  </tr>
  <tr>
	<td>hostname initialization</td>
	<td>During
	<b>the first launch</b> of an instance, cloud-init 
	sets the hostname of the instance according to the hostname information in <code>vendor_data.json</code>.</td>
	<td>
	If you create or reinstall an instance with a custom image and you want to keep the custom `hostname` settings of the image,
	you can set <code>preserve_hostname</code> in <code>/etc/cloud/cloud.cfg</code> to <code>true</code> and delete <code>- scripts-user</code> before creating the custom image.
	</td>
	<td>If <code>preserve_hostname</code> is 
	<code>true</code> and <code>- scripts-user</code> is disabled, 
	the initialization script <code>/var/lib/cloud/instance/scripts/runcmd</code>
	inside the instance will not be executed. Disabling the configuration will also affect the initialization of other sub-items such as the installation of Tencent Cloud Observability Platform and cloud security as well as software source settings.
	Also, the custom script will not be executed when you create the CVM instance.</td>
  </tr>
  <tr>
	<td>/etc/hosts initialization</td>
	<td>During
	<b>the first launch</b> of an instance, cloud-init 
	initializes <code>/etc/hosts</code> 
	to <code>127.0.0.1 $hostname</code> by default.</td>
	<td>If you create or reinstall an instance with a custom image and you want to keep the custom `/etc/hosts` settings of the image,
	of the image, you can delete the following configuration 
	from <code>/etc/cloud/cloud.cfg</code> before creating the custom image: 
	<code>- scripts-user</code> and 
	<code>- [&#39;update_etc_hosts&#39;, &#39;once-per-instance&#39;]</code>.</td>
	<td>
	  <ul style="margin: 0px;">
		<li>After you disable 
		<code>- scripts-user</code>, 
		the initialization script <code>/var/lib/cloud/instance/scripts/runcmd</code>
		inside the instance will not be executed. Disabling the configuration will also affect the initialization of other sub-items such as the installation of Tencent Cloud Observability Platform and cloud security as well as software source settings. Also, the custom script will not be executed when you create the CVM instance.</li>
		<li>During instance restart, 
		the <code>/etc/hosts</code> settings of some existing instances will be overwritten. For information about the solutions, 
		see <a href="https://www.tencentcloud.com/document/product/213/32504">Modifying etc/hosts Configuration of
		Linux Instance</a>.</li>
	  </ul>
	</td>
  </tr>
  <tr>
	<td>DNS initialization (non-DHCP scenario)</td>
	<td>During
	<b>the first launch</b> of an instance, cloud-init 
	sets the DNS of the instance according to the nameservers information in <code>vendor_data.json</code>.</td>
	<td>If you create or reinstall an instance with a custom image and you want to keep the custom DNS settings
	of the image, you can delete the following configuration 
	from <code>/etc/cloud/cloud.cfg</code> before creating the custom image: 
	<code>- resolv_conf</code> and 
	<code>unverified_modules: [&#39;resolv_conf&#39;]</code>.</td>
	<td>None.</td>
  </tr>
  <tr>
	<td>Software source initialization</td>
	<td>During
	<b>the first launch</b> of an instance, cloud-init 
	sets the software source of the instance according to the write_files information in <code>vendor_data.json</code>.</td>
	<td>
	If you create or reinstall an instance with a custom image and you want to keep the custom software source settings of the image, you can delete the following configuration
	from <code>/etc/cloud/cloud.cfg</code> before creating the custom image: 
	<code>- write-files</code>.</td>
	<td>None.</td>
  </tr>
  <tr>
	<td>NTP initialization</td>
	<td>During
	<b>the first launch</b> of an instance, cloud-init 
	sets the INTP server configuration of the instance according to the NTP Server information in <code>vendor_data.json</code> and
	starts the NTP service.</td>
	<td>If you create or reinstall an instance with a custom image and you want to keep the custom NTP settings
	of the image, you can delete the following configuration 
	from <code>/etc/cloud/cloud.cfg</code> before creating the custom image: 
	<code>- ntp</code>.</td>
	<td>None.</td>
  </tr>
  <tr>
	<td>Password initialization</td>
	<td>During
	<b>the first launch</b> of an instance, cloud-init 
	sets the default account password of the instance according to the chpasswd information in <code>vendor_data.json</code>.</td>
	<td>
	If you create or reinstall an instance with a custom image and you want to keep the custom default account password of the image, you can delete the following configuration	
	from <code>/etc/cloud/cloud.cfg</code> before creating the custom image: 
	<code>- set-passwords</code>.</td>
	<td>None.</td>
  </tr>
  <tr>
	<td>Key binding</td>
	<td>During
	<b>the first launch</b> of an instance, cloud-init 
	sets the default account key of the instance according to the `ssh_authorized_keys` information in <code>vendor_data.json</code>.</td>
	<td>
	If you create or reinstall an instance with a custom image and you want to keep the custom key of the image, you can delete the following configuration	
	from <code>/etc/cloud/cloud.cfg</code> before creating the custom image: 
	<code>- users-groups</code>.</td>
	<td>
	If you manually bind the instance to a key inside the instance, the previous key will be overwritten when you perform the key binding operation in the console.</td>
  </tr>
  <tr>
	<td>Network initialization (non-DHCP scenario)</td>
	<td>During
	<b>the first launch</b> of an instance, cloud-init 
	sets the IP, Gateway, and Mask of the instance according to the information in <code>network_data.json</code>.</td>
	<td>
	If you create or reinstall an instance with a custom image and you want to keep the custom network information of the image, you can add the following configuration	
	to <code>/etc/cloud/cloud.cfg</code> before creating the custom image: 
	<code>network: {config: disabled}</code>.</td>
	<td>None.</td>
  </tr>
</table>



### How can I fix common issues related to Cloud-Init? 

#### 1. Error due to the unmounting of Cloud-Init dependencies
- Problem description:
When commands are used to check whether the Cloud-Init service is working properly, the following error is returned:
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
 2. Follow [Troubleshooting cloud-init service errors](#checkcloud-init) to see if the error is returned again.

#### 2. Error due to the modification of the default Python interpreter
- Problem description:
An error is returned when cloud-init is run on startup.
- Problem analysis:
When cloud-init is installed, Python 2 is used as the default Python interpreter, which means that symbolic links, `/usr/bin/python` and `/bin/python`, are linked to Python 2. Users may change the default Python interpreter to Python 3 inside the instance by directing the symbolic links, `/usr/bin/python` and `/bin/python`, to Python 3. Due to compatibility issues, an error will be returned when cloud-init is run on startup.
- Solution:
 1. Taking Python 2.7 for example, modify the Python interpreter specified in the `/usr/bin/cloud-init` file by changing `#!/usr/bin/python` or `#!/bin/python` to `#!/usr/bin/python2.7`.
<dx-alert infotype="notice" title="">
Do not use symbolic links. Point directly to a specific interpreter.
</dx-alert>
 2. Follow [Troubleshooting cloud-init service errors](#checkcloud-init) to see if the error is returned again.

## Cloudbase-Init

### What is Cloudbase-Init?
Like cloud-init, Cloudbase-Init is a bridge by which you can communicate with Windows CVM instances. The Cloudbase-Init service is run when an instance boots up for the first time. The service will read the configuration information of the instance and initialize it. Following operations such as resetting password and modifying IP addresses are also done via Cloudbase-Init.


### How do I check whether the Cloudbase-Init service inside a Windows instance is working properly?


#### Troubleshooting Cloudbase-Init service errors[](id:checkcloudbase-init)
1. Log in to the instance.
<dx-alert infotype="explain" title="">
If you forget your password or fail to reset your password because of Cloudbase-Init service exceptions, you can reset your password by following [Step 2](#step02). 
</dx-alert>
2. [](id:step02)Choose **Control panel** > **Administrative tools** > **Services**.
3. Find the Cloudbase-Init service, right-click it, and go to **Properties**.
 - View **Startup type** and make sure it is set to **Automatic**, as shown in the figure below:
![](https://main.qcloudimg.com/raw/310a278dd2eaf2124d0d52055e0b5b6f.png)
 - View **Log on as** and make sure that **Local System account** is selected, as shown in the figure below:
![](https://main.qcloudimg.com/raw/5a3f623aaf44d55cfe2eaa6aeadb4c12.png)
 - Manually start the Cloudbase-Init service and see if any error is returned.
If any error is returned, you need to fix the issue first and check whether you have installed any security software which may stop Cloudbase-Init from performing related operations. 
![](https://main.qcloudimg.com/raw/dbbe8f9fc05b07d8011705d9d217b76c.png)
 - Open the registry, find each **LocalScriptsPlugin**, and make sure its value is 2, as shown in the figure below:
![](https://main.qcloudimg.com/raw/16106e540d8cf4ef39e5dccb44251350.png)
 - Check whether CD-ROM loading is disabled. If there is an optical disc drive as shown in the figure below, the loading has not been disabled. Otherwise, you need to enable the loading.
![](https://main.qcloudimg.com/raw/7707e694b475ba4d70b4d1d52a6c98bb.png)

### How do I view Cloudbase-Init execution logs?
You can view the log files for different operating systems:
- Linux: `/var/log/cloud-init-output.log`
- Windows: `C:\Program Files\Cloudbase Solutions\Cloudbase-Init\log\cloudbase-init.log`

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


