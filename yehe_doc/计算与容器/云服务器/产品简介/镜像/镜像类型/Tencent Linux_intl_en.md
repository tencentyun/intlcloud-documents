TencentOS Server (also known as Tencent Linux, TS or Tlinux) is Tencent’s Linux operating system designed for cloud scenarios. With specialized features and optimized performance, TencentOS Server provides a high-performance, secure, and reliable operating environment for applications in CVM instances. TencentOS Server is free of charge, and applications developed on CentOS and other distributions can directly run on TencentOS Server. In addition, Tencent Cloud continuously provides you with updates, maintenance, and technical support.

## Scenarios

TencentOS Server is applicable to the following scenarios:

- It’s applicable to all CVM models.
- During instance start-up, it’s required to transfer related operations to cloud-init via user data (the userdata field) to support dynamic configuration.

## TencentOS Server 2.4 Environment

### User-mode environment

User-mode software packages are compatible with the latest CentOS 7, which can be used directly on TencentOS Server 2.4.

### System services and optimization configurations

#### System services

- `tlinux-irqaffinity`: the IRQ affinity service on TencentOS Server.
- `tlinux-bootlocal`: the bootlocal service on TencentOS Server. It will be started after the automatic execution of the `/etc/rc.d/boot.local` script at startup.

#### System tools

`tencent-tools`: the tos (t) commands used for system management. The supported parameters are as follows:

```bash
tos version 2.2
Usage:
	tos TencentOS Server System Management Toolset
	tos -u|-U| update [rpm_name]Update the system 
	tos -i|-I| install rpm_name	install rpms
	tos -s|-S| showShow the system version
	tos -c|-C| check [rpm_name]Check the modified rpms
	tos -f yum | fix yumFix yum problems
	tos -f dns | fix dnsFix DNS problems
	tos -a|-A | analyzeAnalyze the system performance 
	tos set dns			Set DNS
	tos set irqSet irqaffinity, restart irqaffinity service
	tos -cu| check-updateCheck available package updates
	tos -b|-B| backup [ reboot ]Backup the system online, or reboot to backup 
	tos -r|-R| recover|reinstallRecover or Reinstall the system
	tos -h|-H| helpShow this usage
	tos -v|-V| versionShow the script version
```

#### System configurations

- **pam**: sets a strong password policy.
- **modifying `/etc/bashrc`**: optimizes the bash display.
- **`/etc/hosts`**: adds TENCENT64 and TENCENT64.site.
- **`/root/.bashrc`**: optimizes the configuration.

#### TencentOS Server 2.4 kernel

TencentOS Server 2.4 uses the longterm kernel 4.14 of the kernel community. For more information, see [TencentOS-kernel](https://github.com/Tencent/TencentOS-kernel).


## Obtaining TencentOS Server

You can use TencentOS Server by using the following methods:

- When creating a CVM instance, select **Public Image** and the corresponding version of TencentOS Server.
  For more information, see [Creating Instances via CVM Purchase Page](https://intl.cloud.tencent.com/document/product/213/4855).
- For existing CVM instances, you need to reinstall the operating system to TencentOS Server.
  For more information, see [Reinstalling System](https://intl.cloud.tencent.com/document/product/213/4933).

## Release Notes

| Release Time      | Image Tag                                                    | Description                                                  |
| ------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| September 17, 2019 | TencentOS Server 2.4, formerly known as Tencent linux release 2.4 (Final) | Image ID: img-hdt9xxkt<br>Kernel version: 4.14.105<br>Region: all regions |


## Technical Support

Tencent Cloud provides the following technical support for TencentOS Server:

- Tencent Cloud provides security updates in the YUM repository. You can run the `yum update` command to update TencentOS Server to the latest version.
- TencentOS Server is an operating system image designed for cloud scenarios. It is based on kernel version 4.14.105, which has long been supported by the kernel community. If needed, Tencent Cloud will provide technical assistance to help you solve any problems you encounter while using TencentOS Server.
