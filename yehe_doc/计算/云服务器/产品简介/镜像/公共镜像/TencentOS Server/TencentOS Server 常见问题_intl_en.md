### What is TencentOS Server?
TencentOS Server (also known as Tencent Linux, TS, or Tlinux) is Tencent's Linux operating system designed for cloud scenarios. With specific features and optimized performance, it provides a high-performance, secure, and reliable operating environment for applications in CVM instances.
TencentOS Server contains the TencentOS kernel developed by the TencentOS team and is deeply customized based on the cloud environment to introduce the latest Linux innovations to the market and offer high performance, scalability, and reliability for various software programs of enterprises. It is free of charge, and you can get updates and technical support from the TencentOS team continuously.

### What are the characteristics of TencentOS Server?
TencentOS Server has the following characteristics:
- Deeply customized out-of-the-box service with no complex configuration required.
- High security and compliance with support for hotfixes and zero-downtime repair.
- Long-Term support by a powerful operations support team and full open-sourceness.
- Comprehensively optimized high-performance operating system specifically design for cloud scenarios.

### What are the strengths of TencentOS Server compared with other Linux distributions?
Compared with Linux distributions such as CentOS and Ubuntu, TencentOS Server has the following strengths:
- It has been proven by and optimized through a large number of Tencent businesses for over a decade.
- It is supported by an authoritative kernel expert team.
- It is out-of-the-box with key performance optimizations and features customized for cloud and container scenarios.
- It has a powerful operations support team, from which you can get strong business support simply by paying small fees.

### In what editions is TencentOS Server available?
Currently, TencentOS Server is available in the following two editions:
- TencentOS Server 2 (TS2): latest user mode package based on CentOS 7.
- TencentOS Server 3 (TS3): latest user mode package based on RHEL 8.

The user mode software package of TencentOS Server maintains 100% binary compatibility with RHEL.

### In what editions is the TencentOS Server kernel available?
The TencentOS Server kernel (TK) is available in the following two editions:
- TK3: kernel version based on longterm Community Edition 4.14.
- TK4: kernel version based on longterm Community Edition 5.4.

You can get the TK code from GitHub. For more information, see [TencentOS-kernel](https://github.com/Tencent/TencentOS-kernel).

### How long is the lifecycle of TencentOS Server?
Below is the lifecycle of each TencentOS Server edition. Before the lifecycle ends, bugfixes and security patch updates will be provided continuously.
- TencentOS Server 2 distribution: maintenance will continue until December 31, 2024.
- TencentOS Server 3 distribution: maintenance will continue until December 31, 2029.

### How do I use TencentOS Server in Tencent Cloud?
Tencent Cloud provides public images in two TencentOS Server editions. You can choose to use a TencentOS Server image edition when creating a Linux CVM instance.

### Which CVM instance types does TencentOS Server support?
TencentOS Server supports most CVM instance types. You can select an image on the [CVM instance purchase page](https://buy.intl.cloud.tencent.com/cvm?tab=custom&regionId=1&projectId=-1) to use it.

### Will fees be charged for using TencentOS Server in CVM?
No. TencentOS Server is free of charge, and you only need to pay for CVM instances.

### How do I install and upgrade software programs after using TencentOS Server?
On TencentOS Server distribution, you can run the `yum` command as well as the `t` command that comes with TencentOS Server to manage software packages. In addition, TencentOS Server 3 supports running the `dnf` command to manage software packages.

### Can I install and use TencentOS Server on my local server?
Yes. You can download the TencentOS Server distribution .iso file. Click [here](http://mirrors.tencent.com/tlinux/2.4/iso/) for TencentOS Server 2 or [here](http://mirrors.tencent.com/tlinux/3.1/iso/x86_64/) for TencentOS Server 3.
You can install and use TencentOS Server on your local server or a VM such as VirtualBox.

### Can I view the TencentOS Server source code?
TencentOS Server is fully open-source. You can get the source code package [here](http://mirrors.tencent.com/) or by running the `yum downloader --source glibc` command in the system.

### Does TencentOS Server support 32-bit applications and libraries?
No. You can install certain 32-bit software packages through `yum` on TencentOS Server 2.

### How does TencentOS Server guarantee the system security?
TencentOS Server is binary compatible with RHEL 7 and 8 and complies with RHEL security specifications. Tencent Cloud guarantees the security of TencentOS Server in the following ways:
- Tencent's proprietary vulnerability scanning tool and other standard vulnerability scanning and security check tools in the industry are used for regular security scanning.
- TencentOS Server cooperates with the Tencent Security team to implement system security scanning and hardening.
- RHEL and community CVE patches are assessed and user mode software packages are updated regularly to fix the security vulnerabilities.
- CWP is used to regularly check the system security, trigger user security alarms, and provided solutions.



