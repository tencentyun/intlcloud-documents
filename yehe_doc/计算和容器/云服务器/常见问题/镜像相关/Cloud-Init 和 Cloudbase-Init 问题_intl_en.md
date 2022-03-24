## Cloud-init

### What is cloud-init?
Cloud-init is an open source tool that runs inside a CVM instance as a non-resident service. It is executed at startup and exits immediately after execution. It does not listen to any ports.
All the Linux public images of Tencent Cloud are pre-installed with the cloud-init service. You need to run the service as the root user because the service is mainly used for the initialization of CVM instances such as configuring DNS, hostname, and IP, and the execution of some custom scripts that users specify to be executed during the first boot when creating the CVM instances.

### How do I check whether the cloud-init service inside a Linux instance is working properly?


#### Troubleshooting cloud-init service errors[](id:checkcloud-init)

[Log in to a Linux instance using the standard login method (recommended)](https://intl.cloud.tencent.com/document/product/213/5436). Then, run the following commands in sequence and observe whether an error is reported. If the execution result is displayed, the service is running normally. Otherwise, the cause of the error will be reported. You can troubleshoot the error accordingly.
<dx-alert infotype="explain" title="">
This step only applies to CVM instances created with public Linux images. If you installed cloud-init by yourself, adjust the commands according to the actual situation.
</dx-alert>


1. Delete the cloud-init cache directory.
```
rm -rf /var/lib/cloud
```
2. Perform complete cloud-init initialization.
```
/usr/bin/cloud-init init --local
```
3. Pull data from the configured data source.
```
/usr/bin/cloud-init init
```
4. Cloud-init initialization involves multiple stages. To ensure sufficient dependency between the stages, config stage is specified for the cloud-init modules.
```
/usr/bin/cloud-init modules --mode=config
```
5. Specify final stage for the cloud-init modules.
```
/usr/bin/cloud-init modules --mode=final
```

### What initialization operations does cloud-init perform on instances?

Tencent Cloud implements all instance initialization operations through cloud-init, ensuring the transparency of the operations inside an instance. The following briefly covers some initialization operations. For more details, see [cloud-init documentation](http://cloudinit.readthedocs.io/en/latest/).

<table>
<tr>
    <th style="width: 18%;">Initialization Type</th>
    <th style="width: 25%;">Default Behavior</th>
    <th style="width: 27%;">Disablement Method</th>
    <th style="width: 30%;">Note</th>
  </tr>
  <tr>
	<td>hostname initialization</td>
	<td>During <b>the first boot</b> of an instance, cloud-init will set the hostname of the instance according to the hostname information in <code>vendor_data.json</code>.</td>
	<b>首次启动</b>时，Cloud-Init 会根据 
	<code>vendor_data.json</code> 中的 hostname 信息来设置实例的 hostname。</td>
	<td>
	When you use a custom image to create or reinstall an instance, if you want to keep the custom hostname settings of the image, set <code>preserve_hostname</code> in <code>/etc/cloud/cloud.cfg</code> to <code>true</code> and delete the <code>- scripts-user</code> line before making the image.
	设置，则请在制作自定义镜像之前将 <code>/etc/cloud/cloud.cfg</code> 中的 <code>preserve_hostname</code> 设置为 <code>true</code>，并删除 <code>- scripts-user</code> 这行配置。
	</td>
	<td>If <code>preserve_hostname</code> is <code>true</code> and the <code>- scripts-user</code> configuration is disabled, the instance's internal <code>/var/lib/cloud/instance/scripts/runcmd</code> initialization script will not be executed, which will affect the initialization of other items (mainly related to cloud monitoring and security product installation and repository settings). 
	<code>true</code> 且 <code>- scripts-user</code> 配置被禁用，则实例内部的 
	<code>/var/lib/cloud/instance/scripts/runcmd</code>
	初始化脚本将不会被执行，并会同时影响其他子项的初始化（主要涉及：云监控、云安全的安装、软件源的设置）。
	Meanwhile, custom scripts will not be executed when you create an instance.</td>
  </tr>
  <tr>
	<td>/etc/hosts initialization</td>
	<td>During <b>the first boot</b> of an instance, cloud-init will initialize <code>/etc/hosts</code> as <code>127.0.0.1 $hostname</code> by default.</td>
	<b>首次启动</b>时，Cloud-Init 会默认将 
	<code>/etc/hosts</code> 初始化为 
	<code>127.0.0.1 $hostname</code>。</td>
	<td>When you use a custom image to create or reinstall an instance, if you want to keep the custom `/etc/hosts` settings of the image, you can delete the <code>- scripts-user</code> and <code>- [&#39;update_etc_hosts&#39;, &#39;once-per-instance&#39;]</code> lines in <code>/etc/cloud/cloud.cfg</code> before making the image.</td>
	设置，可以在制作自定义镜像之前在 
	<code>/etc/cloud/cloud.cfg</code> 里面删除 
	<code>- scripts-user</code> 与 
	<code>- [&#39;update_etc_hosts&#39;, &#39;once-per-instance&#39;]</code> 这两行配置。</td>
	<td>
	  <ul style="margin: 0px;">
		<li>If the <code>- scripts-user</code> configuration is disabled, the instance's internal <code>/var/lib/cloud/instance/scripts/runcmd</code> initialization script will not be executed, which will affect the initialization of other items (mainly related to cloud monitoring and security product installation and repository settings). Meanwhile, custom scripts will not be executed when you create an instance.</li> 
		<code>- scripts-user</code> 这行配置，实例内部的 
		<code>/var/lib/cloud/instance/scripts/runcmd</code>
		初始化脚本将不会被执行，并会同时影响其他子项的初始化（主要涉及：云监控、云安全的安装、软件源的设置）。同时，在您创建子机时，自定义脚本也不会被执行。</li>
		<li>During instance restart, the <code>/etc/hosts</code> settings of some existing instances will be overwritten. For solutions, see <a href="https://intl.cloud.tencent.com/document/product/213/32504">Modifying etc/hosts Configuration of Linux Instance</a>.</li> 
		<code>/etc/hosts</code> 的设置都会被覆盖。解决方案请参见 
		<a href="https://intl.cloud.tencent.com/document/product/213/32504">如何有效的修改 Linux 实例的 etc hosts
		配置</a>。</li>
	  </ul>
	</td>
  </tr>
  <tr>
	<td>DNS initialization (non-DHCP scenario)</td>
	<td>During <b>the first boot</b> of an instance, cloud-init will set the DNS of the instance according to the nameservers information in <code>vendor_data.json</code>.</td>
	<b>首次启动</b>时，Cloud-Init 会根据 
	<code>vendor_data.json</code> 中的 nameservers 信息来设置实例的 DNS。</td>
	<td>When you use a custom image to create or reinstall an instance, if you want to keep the custom DNS settings of the image, you can delete the <code>- resolv_conf</code> and <code>unverified_modules: [&#39;resolv_conf&#39;]</code> lines in <code>/etc/cloud/cloud.cfg</code> before making the image.</td>
	设置，可以在制作自定义镜像之前在 
	<code>/etc/cloud/cloud.cfg</code> 里面删除 
	<code>- resolv_conf</code> 与 
	<code>unverified_modules: [&#39;resolv_conf&#39;]</code> 两行配置。</td>
	<td>None.</td>
  </tr>
  <tr>
	<td>Repository initialization</td>
	<td>During <b>the first boot</b> of an instance, cloud-init will set the repository of the instance according to the write_files information in <code>vendor_data.json</code>.</td>
	<b>首次启动</b>时，Cloud-Init 会根据 
	<code>vendor_data.json</code> 中的 write_files 信息来设置实例的软件源。</td>
	<td>
	When you use a custom image to create or reinstall an instance, if you want to keep the custom repository settings of the image, you can delete the <code>- write-files</code> line in <code>/etc/cloud/cloud.cfg</code> before making the image.</td>
	<code>/etc/cloud/cloud.cfg</code> 里面删除 
	<code>- write-files</code> 这行配置。</td>
	<td>None.</td>
  </tr>
  <tr>
	<td>NTP initialization</td>
	<td>During <b>the first boot</b> of an instance, cloud-init will set the NTP server configuration of the instance according to the NTP server information in <code>vendor_data.json</code> and start the NTP service.</td>
	<b>首次启动</b>时，Cloud-Init 会根据 
	<code>vendor_data.json</code> 中的 NTP Server 信息来设置实例的 NTP 服务器配置，并拉起 NTP
	Service。</td>
	<td>When you use a custom image to create or reinstall an instance, if you want to keep the custom NTP settings of the image, you can delete the <code>- ntp</code> line in <code>/etc/cloud/cloud.cfg</code> before making the image.</td>
	设置，可以在制作自定义镜像之前在 
	<code>/etc/cloud/cloud.cfg</code> 里面删除 
	<code>- ntp 这行配置。</code></td>
	<td>None.</td>
  </tr>
  <tr>
	<td>Password initialization</td>
	<td>During <b>the first boot</b> of an instance, cloud-init will set the default account password of the instance according to the chpasswd information in <code>vendor_data.json</code>.</td>
	<b>首次启动</b>时，Cloud-Init 会根据 
	<code>vendor_data.json</code> 中的 chpasswd 信息来设置实例的默认账号密码。</td>
	<td>
	When you use a custom image to create or reinstall an instance, if you want to keep the custom default account password of the image, you can delete the <code>- set-passwords</code> line in <code>/etc/cloud/cloud.cfg</code> before making the image.</td>	
	<code>/etc/cloud/cloud.cfg</code> 里面删除 
	<code>- set-passwords</code> 这行配置。</td>
	<td>None.</td>
  </tr>
  <tr>
	<td>Key binding</td>
	<td>During <b>the first boot</b> of an instance, cloud-init will set the default account key of the instance according to the ssh_authorized_keys information in <code>vendor_data.json</code>.</td>
	<b>首次启动</b>时，Cloud-Init 会根据 
	<code>vendor_data.json</code> 中的 ssh_authorized_keys 信息来设置实例的默认账号密钥。</td>
	<td>
	When you use a custom image to create or reinstall an instance, if you want to keep the custom key of the image, you can delete the <code>- users-groups</code> line in <code>/etc/cloud/cloud.cfg</code> before making the image.</td>	
	<code>/etc/cloud/cloud.cfg</code> 里面删除 
	<code>- users-groups</code> 这行配置。</td>
	<td>
	If you manually bind the instance to a key inside the instance, the previous key will be overwritten when the key binding operation is performed in the console. </td>
  </tr>
  <tr>
	<td>Network initialization (non-DHCP scenario)</td>
	<td>During <b>the first boot</b> of an instance, cloud-init will set the IP, Gateway, and Mask according to the information in <code>network_data.json</code>.</td>
	<b>首次启动</b>时，Cloud-Init 会根据 
	<code>network_data.json</code> 中的信息来设置实例的 IP、GATEWAY、MASK 等。</td>
	<td>
	When you use a custom image to create or reinstall an instance, if you want to keep the custom network information of the image, you can add the <code>network: {config: disabled}</code> line in <code>/etc/cloud/cloud.cfg</code> before making the image.</td>	
	<code>/etc/cloud/cloud.cfg</code> 里面增加 
	<code>network: {config: disabled}</code> 这行配置。</td>
	<td>None.</td>
  </tr>
</table>



### How can I fix issues related to cloud-init? 

#### 1. Error due to the unmounting of the cloud-init dependencies
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
"pkg_resources.DistributionNotFound: xxxxx" indicates that the cloud-init dependencies have been uninstalled.
- Solution:
 1. Reinstall the dependencies.
 2. Follow [Checking the operation of cloud-init](#checkcloud-init) to see if the error is returned again.

#### 2. Error due to the modification of the default Python interpreter
- Problem description:
An error is returned when cloud-init is run on startup.
- Problem analysis:
When cloud-init is installed, Python 2 is used as the default Python interpreter, which means that symbolic links, `/usr/bin/python` and `/bin/python`, are linked to Python 2. Users may change the default Python interpreter to Python 3 inside the instance by directing the symbolic links, `/usr/bin/python` and `/bin/python`, to Python 3. Due to compatibility issues, an error will be returned when cloud-init is run on startup.
- Solution:
 1. Modify the Python interpreter specified in the `/usr/bin/cloud-init` file by changing `#/usr/bin/python` or `#/bin/python` to `#! user/bin/python`.
<dx-alert infotype="notice" title="">
Do not use symbolic links. Point directly to a specific interpreter.
</dx-alert>
 2. Follow [Checking the operation of cloud-init](#checkcloud-init) to see if the error is returned again.

## Cloudbase-Init

### What is Cloudbase-Init?
Like cloud-init, Cloudbase-Init is a bridge by which you can communicate with Windows CVM instances. The Cloudbase-Init service is run when an instance boots up for the first time. The service will read the initialization configuration information of the instance and initialize it. Following operations such as resetting password and modifying IP addresses are also done via Cloudbase-Init.

### How do I check whether the Cloudbase-Init service inside a Windows instance is working properly?


#### Troubleshooting cloudbase-init service errors[](id:checkcloudbase-init)
1. Log in to the instance.
<dx-alert infotype="explain" title="">
If you forget your password or fail to reset your password because of Cloudbase-Init service exceptions, you can reset your password by following [step 2](#step02). 
</dx-alert>
2. [](id:step02)Open **Control panel** > **Administrative tools** > **Services**.
3. Find the cloudbase-init service, right-click it, and go to **Properties**.
 - Check "Startup type" and make sure it is set to "Automatic". See the figure below.
![](https://main.qcloudimg.com/raw/310a278dd2eaf2124d0d52055e0b5b6f.png)
 - View "Logon identity" and ensure that "Local System account" is selected. See the figure below.
![](https://main.qcloudimg.com/raw/5a3f623aaf44d55cfe2eaa6aeadb4c12.png)
 - Manually start the Cloudbase-Init service and see if any error is returned.
If any error is returned, you need to fix the issue first and check whether you have installed any security software which may stop Cloudbase-Init from performing related operations. 
![](https://main.qcloudimg.com/raw/dbbe8f9fc05b07d8011705d9d217b76c.png)
 - Open the registry, find all "LocalScriptsPlugin", and make sure its value is 2. See the figure below.
![](https://main.qcloudimg.com/raw/16106e540d8cf4ef39e5dccb44251350.png)
 - Check whether CD-ROM loading is disabled. If there is an optical disc drive as shown in the figure below, it means that the loading has not been disabled; otherwise, it means that it has been disabled and needs to be enabled.
![](https://main.qcloudimg.com/raw/7707e694b475ba4d70b4d1d52a6c98bb.png)

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

