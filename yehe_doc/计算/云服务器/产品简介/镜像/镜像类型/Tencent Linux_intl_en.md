
Tencent Linux (Tlinux) is a Linux operating system of Tencent designed for cloud scenarios. With specialized features and optimized performance, Tlinux provides a high-performance, secure, and reliable operating environment for applications in Cloud Virtual Machine (CVM) instances. Tlinux is free of charge, and applications developed on CentOS distributions can directly run on Tlinux. What’s more, Tencent Cloud provides you with continuous updates, maintenance, and technical support.

## Use Cases
Tlinux can be used in the following scenarios:
- Tlinux is suitable for instances of most CVM types.
- When launching instances, Tlinux is used to transfer related operations to cloud-init via user data (the userdata field) to support dynamic configuration.

## Main Features

<table>
	<tr><th>Feature</th><th>Description</th></tr>
	<tr><td><b>Kernel Customization</b></td><td>Kernel customization based on kernel version 4.14.105 that has long been supported by the kernel community, while introducing new features applicable to cloud scenarios and improving the kernel performance to resolve major defects.</td></tr>
	<tr><td><b>Container Support</b></td><td>Tlinux is optimized for container scenarios with enhanced isolation and optimized performance: <ul style="margin: 0;"><li>meminfo, vmstat, cpuinfo, stat, and loadavg isolation.</li><li>Sysctl isolation, for example, tcp_no_delay_ack and tcp_max_orphans.</li><li>Bug fix in file systems and networks.</li></ul></td></tr>
	<tr><td><b>Performance Optimization</b></td><td>Tlinux has optimized computing, storage, and network subsystems:<ul style="margin: 0;"><li>Optimized XFS memory allocation to resolve the XFS kmem_alloc failure alarm.</li><li>Optimized memory allocation for received network packets to resolve excessive memory usage when a large number of UDP packets are received.</li><li>Limited memory usage of the system page caches to maintain service performance and avoid out-of-memory (OOM) error.</li></ul></td></tr>
	<tr><td><b>Software Packages</b></td><td><ul style="margin: 0;"><li>Customized based on the CentOS 7 software packages.</li><li>User state software packages are compatible with CentOS 7 and can be used directly on Tlinux.</li><li>Updated and installed via Yellowdog Updater, Modified (YUM).</li><li>Software packages in Extra Packages for Enterprise Linux (EPEL) repository can be used after epel-release package is installed via YUM.</li></ul></td></tr>
	<tr><td><b>Defect Support</b></td><td><ul style="margin: 0;"><li>Kdump feature is provided in the event of an operating system crash.</li><li>Kernel live patching is supported.</li></ul></td></tr>
	<tr><td><b>Security Updates</b></td><td>Tencent Linux offers regular updates to enhance security and features.</td></tr>
</table>

## Release Notes

| Release Time | Image Tag | Description |
|---------|---------|---------|
| September 17, 2019 | Tencent Linux release 2.4 (Final) | Image ID: img-hdt9xxkt<br>Kernel version: 4.14.105<br>Region: all regions |

## Obtaining Tlinux
You can obtain and use Tlinux by the following methods:
- When creating a CVM instance, select **Public Image** and the corresponding version of Tlinux.
For more information, see [Creating Instances](https://intl.cloud.tencent.com/document/product/213/4855).
- For existing CVM instances, you need to reinstall the operating system to Tlinux.
For more information, see [Reinstalling System](https://intl.cloud.tencent.com/document/product/213/4933).

## Technical Support
Tencent Cloud provides the following technical support for Tlinux:
We provide security updates in the YUM repository. You can run `yum update` to update Tlinux to the latest version.
