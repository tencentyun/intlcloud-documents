
Tencent Linux (Tlinux) is a Linux operating system developed by Tencent for cloud scenarios. With specialized features and optimized performance, Tlinux provides a high-performance, securer, and more reliable operating environment for applications in Cloud Virtual Machine (CVM) instances. Tlinux is free, and applications developed on CentOS and Linux distributions can directly run on Tlinux. Tencent Cloud provides users with continuous updates, maintenance, and technical support.

## Use Cases
Tlinux can be used in the following scenarios:
- Tlinux is applicable to the instance type families of most CVMs, including Cloud Physical Machine (CPM) 2.0.
- During instance launching, Tlinux is used to transfer related operations to cloud-init through user data (the userdata field), allowing it to support dynamic configuration.

## Main Features

<table>
	<tr><th>Feature</th><th>Description</th></tr>
	<tr><td><b>Kernel customization</b></td><td>Customized the kernel based on the kernel version 4.14.105 that has long been supported by the kernel community; introduced new features applicable to cloud scenarios; improved the kernel performance improved, and resolved major defects.</td></tr>
	<tr><td><b>Support for containers</b></td><td>Tlinux is optimized for container scenarios for enhanced isolation and optimized performance: <ul style="margin: 0;"><li>Isolated meminfo, vmstat, cpuinfo, stat, and loadavg.</li><li>Isolated Sysctl, for example, tcp_no_delay_ack and tcp_max_orphans.</li><li>Fixed bugs in the file system and network.</li></ul></td></tr>
	<tr><td><b>Performance optimization</b></td><td>Optimized the computing, storage, and network subsystems:<ul style="margin: 0;"><li>Optimized XFS memory allocation to resolve the XFS kmem_alloc failure alarm.</li><li>Optimized the memory allocation for received network packets to resolve the issue of excessive memory usage when many UDP packets are received.</li><li>Limited the percentage of memory occupied by system page caches to ensure that service performance is not affected and no out-of-memory (OOM) errors occur due to insufficient memory.</li></ul></td></tr>
	<tr><td><b>Software packages</b></td><td><ul style="margin: 0;"><li>Customized based on the CentOS 7 software packages.</li><li>User state software packages are compatible with CentOS 7 and can be directly used in Tlinux.</li><li>Updated and installed via Yellowdog Updater, Modified (YUM).</li><li>Supports the use of software packages in the Extra Packages for Enterprise Linux (EPEL) repository after the epel-release package is installed via YUM.</li></ul></td></tr>
	<tr><td><b>Support for defects</b></td><td><ul style="margin: 0;"><li>Provides kdump feature in the event of a operating system crash.</li><li>Supports kernel live patching </li></ul></td></tr>
	<tr><td><b>Security updates</b></td><td>Regularly updates security patches to enhance security and features.</td></tr>
</table>

## Release Notes

| Release Time | Image Tag | Description |
|---------|---------|---------|
| September 17, 2019 | Tencent Linux release 2.4 (Final) | Image ID: img-hdt9xxkt<br>Kernel version: 4.14.105<br>Region: All regions |

## Obtaining Tlinux
Tlinux public images are provided in the [CVM Console](https://console.cloud.tencent.com/cvm). You can obtain and use Tlinux by using the following methods.
- When creating a CVM instance, select **Public Image** and the corresponding version of Tlinux.
For more information, see [Creating an Instance](http://intl.cloud.tencent.com/document/product/213/4855).
- For existing CVM instances, you need to reinstall the operating system to Tlinux.
For more information, see [Reinstalling the Operating System](http://intl.cloud.tencent.com/document/product/213/4933).

## Technical Support
Tencent Cloud provides the following technical support for Tlinux:
We provide security updates in the YUM repository. You can update Tlinux to the latest version by running `yum update`.
