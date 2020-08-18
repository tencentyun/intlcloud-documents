
Tencent Linux (Tlinux) is Tencent’s Linux operating system designed for cloud scenarios. With specialized features and optimized performance, Tlinux provides a high-performance, secure, and reliable operating environment for applications in Cloud Virtual Machine (CVM) instances. Tlinux is free of charge, and applications developed on CentOS distributions can directly run on Tlinux. In addition, Tencent Cloud continuously provides you with updates, maintenance, and technical support.

## Use Cases
Tlinux can be used in the following scenarios:
- Tlinux is suitable for instances of most CVM types.
- When launching instances, Tlinux is used to transfer related operations to cloud-init via user data (the userdata field) to support dynamic configuration.

## Main Features

<table>
	<tr><th>Feature</th><th>Description</th></tr>
	<tr><td><b>Kernel Customization</b></td><td>Kernel customization based on kernel version 4.14.105, which has long been supported by the kernel community, to introduce new features applicable to cloud scenarios and improve the kernel performance to resolve major defects.</td></tr>
	<tr><td><b>Container Support</b></td><td>Tlinux optimizes container scenarios by providing enhanced isolation and optimized performance: <ul style="margin: 0;"><li>meminfo, vmstat, cpuinfo, stat, and loadavg isolation.</li><li>Sysctl isolation; for example, tcp_no_delay_ack and tcp_max_orphans.</li><li>Fixes bugs in file systems and networks.</li></ul></td></tr>
	<tr><td><b>Performance Optimization</b></td><td>Tlinux optimizes computing, storage, and network subsystems:<ul style="margin: 0;"><li>Optimizes XFS memory allocation to resolve the XFS kmem_alloc failure alarm.</li><li>Optimizes memory allocation for received network packets to resolve excessive memory usage when a large number of UDP packets are received.</li><li>Limits the memory usage of the system page caches to maintain optimal service performance and prevent out-of-memory (OOM) errors.</li></ul></td></tr>
	<tr><td><b>Software Packages</b></td><td><ul style="margin: 0;"><li>Customized based on the CentOS 7 software packages.</li><li>User state software packages are compatible with CentOS 7 and can be used directly on Tlinux.</li><li>Updated and installed via Yellowdog Updater, Modified (YUM).</li><li>Software packages in the Extra Packages for Enterprise Linux (EPEL) repository can be used after the epel-release package is installed via YUM.</li></ul></td></tr>
	<tr><td><b>Defect Support</b></td><td><ul style="margin: 0;"><li>The Kdump feature is provided in the event of an operating system crash.</li><li>Kernel live patching is supported.</li></ul></td></tr>
	<tr><td><b>Security Updates</b></td><td>Tencent Linux offers regular updates to enhance its security and features.</td></tr>
</table>

## Release Notes

| Release Time | Image Tag | Description |
|---------|---------|---------|
| September 17, 2019 | Tencent Linux release 2.4 (Final) | Image ID: img-hdt9xxkt<br>Kernel version: 4.14.105<br>Region: all regions |

## Obtaining Tlinux
You can obtain and use Tlinux by using the following methods:
- When creating a CVM instance, select **Public Image** and the corresponding version of Tlinux.
For more information, see [Creating Instances via the CVM Purchase Page](https://intl.cloud.tencent.com/document/product/213/4855).
- For existing CVM instances, you need to reinstall the operating system to Tlinux.
For more information, see [Reinstalling the System](https://intl.cloud.tencent.com/document/product/213/4933).

## Technical Support
- Tencent Cloud provides security updates in the YUM repository. You can run the `yum update` command to upgrade Tlinux.
- Tlinux is an operating system image tailored to the cloud environment. It is based on kernel version 4.14.105, which has long been supported by the kernel community. Tencent Cloud will provide technical support for the problems you encounter while using Tlinux.
