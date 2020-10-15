
Tencent Linux (Tlinux) is Tencent’s Linux operating system designed for cloud scenarios. With specialized features and optimized performance, Tencent Linux provides a high-performance, secure, and reliable operating environment for applications in Cloud Virtual Machine (CVM) instances. Tencent Linux is free of charge, and applications developed on CentOS distributions can directly run on Tencent Linux. In addition, Tencent Cloud continuously provides you with updates, maintenance, and technical support.

## Use Cases
Tencent Linux can be used in the following scenarios:
- Tencent Linux is suitable for instances of most CVM types.
- When launching instances, Tencent Linux is used to transfer related operations to cloud-init via user data (the userdata field) to support dynamic configuration.

## Main Features

<table>
	<tr><th>Feature</th><th>Description</th></tr>
	<tr><td><b>Kernel Customization</b></td><td>Kernel customization based on kernel version 4.14.105, which has long been supported by the kernel community, to introduce new features applicable to cloud scenarios and improve the kernel performance to resolve major defects.</td></tr>
	<tr><td><b>Container Support</b></td><td>Tencent Linux optimizes container scenarios by providing enhanced isolation and optimized performance: <ul style="margin: 0;"><li>meminfo, vmstat, cpuinfo, stat, and loadavg isolation.</li><li>Sysctl isolation; for example, tcp_no_delay_ack and tcp_max_orphans.</li><li>Fixes bugs in file systems and networks.</li></ul></td></tr>
	<tr><td><b>Performance Optimization</b></td><td>Tencent Linux optimizes computing, storage, and network subsystems:<ul style="margin: 0;"><li>Optimizes XFS memory allocation to resolve the XFS kmem_alloc failure alarm.</li><li>Optimizes memory allocation for received network packets to resolve excessive memory usage when a large number of UDP packets are received.</li><li>Limits the memory usage of the system page caches to maintain optimal service performance and prevent out-of-memory (OOM) errors.</li></ul></td></tr>
	<tr><td><b>Software Packages</b></td><td><ul style="margin: 0;"><li>Customized based on the CentOS 7 software packages.</li><li>User-mode software packages are compatible with CentOS 7 and can be used directly on Tencent Linux.</li><li>Updated and installed via Yellowdog Updater, Modified (YUM).</li><li>Software packages in the Extra Packages for Enterprise Linux (EPEL) repository can be used after the epel-release package is installed via YUM.</li></ul></td></tr>
	<tr><td><b>Defect Support</b></td><td><ul style="margin: 0;"><li>The Kdump feature is provided in the event of an operating system crash.</li><li>Kernel live patching is supported.</li></ul></td></tr>
	<tr><td><b>Security Updates</b></td><td>Tencent Linux offers regular updates to enhance its security and features.</td></tr>
</table>

## Tencent Linux 2.4 Introduction
### User-mode environment
User-mode software packages are compatible with the latest CentOS 7, which can be used directly on Tencent Linux 2.4.

### System services and optimization configurations
#### System services
- `tlinux-irqaffinity`: the IRQ affinity service on Tencent Linux.
- `tlinux-bootlocal`: the bootlocal service on Tencent Linux. It will be started after the automatic execution of the `/etc/rc.d/boot.local` script at startup.

#### System tools
`tencent-tools`: the tos (t) commands used for the system management. The supported parameters are as follows:
```bash
tos version 2.2
Usage:
	tos TencentOS Server System Management Toolset
	tos -u|-U| update [rpm_name]	Update the system 
	tos -i|-I| install rpm_name	install rpms
	tos -s|-S| show			Show the system version
	tos -c|-C| check [rpm_name]	Check the modified rpms
	tos -f yum | fix yum		Fix yum problems
	tos -f dns | fix dns		Fix DNS problems
	tos -a|-A | analyze		Analyze the system performance 
	tos set dns			Set DNS
	tos set irq			Set irqaffinity, restart irqaffinity service
	tos -cu| check-update		Check available package updates
	tos -b|-B| backup [ reboot ]	Backup the system online, or reboot to backup 
	tos -r|-R| recover|reinstall	Recover or Reinstall the system
	tos -h|-H| help			Show this usage
	tos -v|-V| version		Show the script version
```

#### System configurations
- **pam**: sets a strong password policy.
- **modifying `/etc/bashrc`**: optimizes the bash display.
- **`/etc/hosts`**: adds TENCENT64 and TENCENT64.site.
- **`/root/.bashrc`**: optimizes the configuration.

#### Tencent Linux 2.4 kernel
Tencent Linux 2.4 uses the longterm kernel 4.14 of the kernel community. For more information, see [TencentOS-kernel](https://github.com/Tencent/TencentOS-kernel).


## Obtaining Tlinux
You can obtain and use Tencent Linux by using the following methods:
- When creating a CVM instance, select **Public Image** and the corresponding version of Tencent Linux.
For more information, see [Creating Instances via the CVM Purchase Page](https://intl.cloud.tencent.com/document/product/213/4855).
- For existing CVM instances, you need to reinstall the operating system to Tencent Linux.
For more information, see [Reinstalling the System](https://intl.cloud.tencent.com/document/product/213/4933).

## Release Notes
| Release Time | Image Tag | Description |
|---------|---------|---------|
| September 17, 2019 | Tencent Linux release 2.4 (Final) | Image ID: img-hdt9xxkt<br>Kernel version: 4.14.105<br>Region: all regions |


## Technical Support
Tencent Cloud provides the following technical support for Tencent Linux:
- Tencent Cloud provides security updates in the YUM repository. You can run the `yum update` command to update Tencent Linux to the latest version.
- Tencent Linux is an operating system image designed for cloud scenarios. It is based on kernel version 4.14.105, which has long been supported by the kernel community. Tencent Cloud will provide you with technical assistance in your use of Tencent Linux if needed.
