TencentOS Server (aka Tlinux or TS) is a Linux distribution developed by Tencent Cloud for cloud scenarios. It offers specific features and performance optimizations to deliver a higher performance and a more secure and reliable runtime environment for applications in CVM instances. Independently developed and designed based on the Linux kernel on top of Tencent's technical experience accumulated in the field of operating systems over the last decade, TencentOS Server has been verified and improved by Tencent's many internal businesses for many years. It is used as the OS of more than 99% of internal servers in all Tencent businesses. Meanwhile, as Tencent has the widest variety of business ecosystems in China ranging from social networking, gaming, and payment to AI and security, TencentOS Server's core capabilities such as stability, security, compatibility, and performance have been fully proven for a long time. Compared with community OS distributions, TencentOS Server is comprehensively enhanced and optimized in terms of stability, performance, and container infrastructure. It can provide enterprises with stable and highly available services to meet their demanding workload requirements, making it a better enterprise-grade OS solution than CentOS. Tencent Cloud strives to make TencentOS Server the best OS in the cloud.

TencentOS Server is publicly available currently, and its user-mode environment is compatible with CentOS, so applications developed on CentOS can run directly on TencentOS Server.


## Use Cases
TencentOS Server is suitable for most models, including Standard, Compute, MEM Optimized, and High IO models. It also supports CPM 2.0 and high-performance computing clusters.

<dx-alert infotype="notice" title="">
If you need to use TencentOS Server to run a GPU instance, install the corresponding GPU driver.
</dx-alert>


## TencentOS Server Strengths
- **Extreme stability verified by tens of millions of nodes**
TencentOS Server has undergone long-term practical testing by massive businesses deployed on tens of millions of nodes, delivering an overall availability of 99.999%.
- **Comprehensive optimization for a higher performance**
The deeply optimized high-performance TencentOS Server has been improved for various software programs in the system. It increases the typical business performance by over 50%.
- **Open-source compatibility for a better OS in the cloud**
TencentOS Server is a 100% open-source Linux distribution. Its user mode remains compatible with CentOS and has a higher stability and performance, making it a better alternative to CentOS in the cloud.
- **Deep customization designed for the cloud**
TencentOS Server is dedicatedly developed for the cloud and suitable for a wide variety of workloads. It comes with the latest open standards-based virtualization and cloud-native tools.
- **Security compliance with zero-downtime fix**
The security lab safeguards the system, enhances system-level security, fixes various vulnerabilities promptly, and supports hot patches to avoid unnecessary downtime.



## TencentOS Server Image Version
Currently, three TencentOS Server images are available for your choice:

<table>
<tr>
<th width="35%">Image Version</th>
<th>Description</th>
</tr>
<tr>
<td>TencentOS Server 3.1</td>
<td>It is compatible with the CentOS 8 user mode and uses the tkernel4 version deeply optimized based on the community 5.4 LTS kernel.</td>
</tr>
<tr>
<td>TencentOS Server 2.4</td>
<td>It is compatible with the CentOS 7 user mode and uses the tkernel3 version deeply optimized based on the community 4.14 LTS kernel.</td>
</tr>
<tr>
<td>TencentOS Server 2.4 (TK4)</td>
<td>It is compatible with the CentOS 7 user mode and uses the tkernel3 version deeply optimized based on the community 5.4 LTS kernel.</td>
</tr>
</table>



## TencentOS Server Kernel
The TencentOS Server kernel (tkernel) is decoupled from the distribution. The current main kernel is divided into two versions.
- tkernel4 deeply optimized based on community 5.4 LTS (tk4).
- tkernel3 deeply optimized based on community 4.14 LTS (tk3).
For more information, see [TencentOS Kernel's GitHub repository](https://github.com/Tencent/TencentOS-kernel).

## Using TencentOS Server 

### Use in the cloud
When you create an instance or reinstall the operating system of an existing instance, you can select a public image and choose to use the corresponding version of OpenCloudOS. For detailed directions, see [Creating Instances via CVM Purchase Page](https://intl.cloud.tencent.com/document/product/213/4855) and [Reinstalling System](https://intl.cloud.tencent.com/document/product/213/4933).





## Services and Updates
Tencent Cloud provides more than five years of maintenance and updates for each major version of TencentOS Server, including regular image updates, introduction of new features and optimizations, timely security vulnerability fixes, and bug fixes. Existing servers can be upgraded through `yum` for bug fixes in time.
For more information on TencentOS Server, follow Tencent Cloud Assistant on WeChat Mini Program.

