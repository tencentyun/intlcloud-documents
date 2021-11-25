## What Is Lighthouse?

TencentCloud Lighthouse (Lighthouse) is a new-gen, out-of-the-box cloud server service developed for lightweight business scenarios to help small and medium-sized enterprises (SMEs) and developers conveniently and efficiently build small websites, blogs, forums, storage services, and various development, testing, and learning environments in the cloud. It is easier to use than traditional cloud server services and delivers applications at one stop by integrating and packaging basic cloud resources and popular open-source software, offering you the best way to get started with Tencent Cloud.


## Why Lighthouse?

Lighthouse offers the following benefits:
- It is easy to get started with and use and allows you to quickly build cloud environments or applications with just a few clicks.
- It is ready to use out of the box, eliminating the need to purchase servers and manage hardware infrastructure.
- It can be used on demand, reducing the costs and offering cost-effective and excellent products and services.
- It is stable, reliable, and secure.

For more information on why this service, please see [Strengths](https://intl.cloud.tencent.com/document/product/1103/41262) and [Use Cases](https://intl.cloud.tencent.com/document/product/1103/41263).

## Differences from CVM
For more information on the differences between Lighthouse and CVM, please see [Product Comparison](https://intl.cloud.tencent.com/document/product/1103/41521).

## Instance

An instance is a virtual computing resource in the cloud, containing the most basic components such as CPU, OS, network, and disk. Lighthouse instances are generally suitable for supporting low-load lightweight application scenarios with a moderate number of access requests, including small websites, web applications, blogs, forums, and cloud-based development, testing, and learning environments. For more information on how to select an instance specification, please see [Instance Package](https://intl.cloud.tencent.com/document/product/1103/41264).
If you want to use more instance types, such as Memory Optimized, High I/O, Big Data, Bare Metal, and GPU/FPGA Heterogeneous Computing, to support your business scenarios such as high-concurrency websites, video encoding/decoding, large games, and complex distributed cluster applications, please use CVM. For more information, please see [Instance Types](https://intl.cloud.tencent.com/document/product/213/11518).

## [Image](id:OS)
An image is a preconfigured template started and executed by Lighthouse, which contains preinstalled operating systems and software applications. Simply put, you can consider an image as an "installation disk" for Lighthouse. You can use an image to create one or multiple instances.
Lighthouse supports the following three image types:
<dx-tabs>
::: System image
- **Image description**
A system image contains only the initial operating system (i.e., different distributions of operating systems such as CentOS, Ubuntu, and Windows Server) without applications, their runtime environments, and relevant initialization configuration files. 
- **Use cases**
It is suitable for users familiar with the installation and environment configuration of server operating systems and software programs. Lighthouse instances created from a system image have only the initial operating system environment installed, where you can install software programs or application systems as needed.
- **Included images**
<ul class="params">
<li>CentOS 7.6</li>
<li>CentOS 8.0</li>
<li>Ubuntu 18.04.1 LTS</li>
<li>Ubuntu 20.04 LTS</li>
<li>Debian 10.2</li>
<li>Windows Server 2012 R2</li>
<li>Windows Server 2016</li>
<li>Windows Server 2019</li>
</ul>
:::
::: Application image
- **Image description**
In addition to the underlying operating system (i.e., different distributions of operating systems such as CentOS and Windows Server), an application image also encapsulates applications (such as LAMP, WordPress, ASP.NET, Node.js, and Baota Panel), their runtime environments, and relevant initialization configuration files, delivering an out-of-the-box user experience.
- **Use cases**
It is suitable for quick out-of-the-box application deployment. After a Lighthouse instance is created from an application image, the application system can be initialized automatically, and you can build the application in just a few steps of simple configuration, with no need to perform operations such as manually installing applications and uploading software packages.
- **Included images**
<ul class="params">
<li>Baota Linux Panel for Tencent Cloud</li>
<li>Discuz! Q </li>
<li>WordPress Community Edition</li>
<li>Typecho</li>
<li>Cloudreve</li>
<li>LAMP</li>
<li>Node.js</li>
<li>ASP.NET</li>
<li>Theia IDE</li>
<li>Docker CE</li>
<li>WordPress Tencent Cloud Plugin</li>
<li>Nextcloud Tencent Cloud Plugin</li>
<li>Discuz! X Tencent Cloud Plugin</li>
</ul>
:::
::: Custom image

- **Image description**
A custom image is an image created by using the image creation feature and can only be used by the creator.
- **Use cases**
You can select a Lighthouse instance on which applications have already been deployed to create a custom image and use it as a template to quickly create more instances.
:::
</dx-tabs>

<dx-alert infotype="explain" title="">
You can use an image to build personal websites, forums, or other platforms as instructed in Best Practice.
</dx-alert>

## Network

The network of Lighthouse is based on VPC, which can build a stable and secure cloud-based network for you.
>? For more information on the private network connectivity between different Lighthouse instances and between Lighthouse instances and other Tencent Cloud services, please see [Region and Network Connectivity](https://intl.cloud.tencent.com/document/product/1103/41266).
>

<dx-accordion>
::: Public \sIP
An independent public IP is assigned to each created Lighthouse instance, and a dedicated public network bandwidth (or peak bandwidth) value is configured by default for access over the internet. You cannot add more public IPs or change the public IP.
:::
::: Public network bandwidth
It is the public network outbound bandwidth provided by Lighthouse in different regions in the Chinese mainland, which guarantees stable and low-latency network quality.
>?
>- It is called "bandwidth" in [instance packages](https://intl.cloud.tencent.com/document/product/1103/41264).
>- For more information on the inbound and outbound bandwidth caps, please see [Bandwidth Cap Description](https://intl.cloud.tencent.com/document/product/1103/41264).
>
:::
::: Public network peak bandwidth
It is the upper limit of the public network outbound bandwidth provided by Lighthouse instances outside the Chinese mainland.
>?
>- It is called "peak bandwidth" in [instance packages](https://intl.cloud.tencent.com/document/product/1103/41264).
>- For more information on the inbound and outbound bandwidth caps, please see [Bandwidth Cap Description](https://intl.cloud.tencent.com/document/product/1103/41264).
>- For Lighthouse instances outside the Chinese mainland, as access from the Chinese mainland may experience a significant delay and packet loss due to the ISP network lines (non-cross-border access typically suffers no impact), Tencent Cloud only guarantees that the public network bandwidth provided in instance packages is the "peak bandwidth".
:::
::: Private \sIP
- One private IP is assigned to each created Lighthouse instance by default for communication between different Lighthouse instances.
- Under the same account, multiple Lighthouse instances in the same region are in the same VPC, while Lighthouse instances in different regions are in different VPCs by default.
- Private network bandwidth is the bandwidth of a shared network, and there is no guarantee for its continuous stability.
- Network isolation between Lighthouse instances can be implemented by a firewall.

:::
::: Traffic package
Lighthouse is offered in the form of traffic package, which is the monthly limit on the public network outbound traffic. If the traffic used by an instance in a month exceeds the traffic package limit, the excessive traffic will be billed by usage. For more information, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/1103/41403).
:::
</dx-accordion>

## Storage
The instance system disks of all Lighthouse packages are Tencent Cloud SSD cloud disks, which are based on full NVMe SSD storage media and use a three-copy distributed storage mechanism to provide low-latency and high-throughput I/O capabilities with a high random IOPS and 99.9999999% data security. For more information on the SSD cloud disk performance, please see [Storage Performance Description](https://intl.cloud.tencent.com/document/product/1103/41264).

## Security
Anti-DDoS Basic and [CWP Basic](https://intl.cloud.tencent.com/document/product/296/2222) are activated by default to help you build a server security protection system.
>?
>- You can log in to the Anti-DDoS console and select **Lighthouse** at the top of the [Anti-DDoS Basic](https://console.cloud.tencent.com/ddos/ddos-basic) page to view the DDoS protection status.
>- You can log in to the CWP console and select **Lighthouse** at the top of the [Server List](https://console.cloud.tencent.com/cwp/asset/machine) page to view the security protection status of Lighthouse instances.
>


## Other Relevant Tencent Cloud Services
- If you want to access your website directly at a domain name, you need to bind and resolve it first.
- If you want to provide security features for your website such as HTTPS, identity verification, and encrypted data transfer, you need to install a Secure Sockets Layer (SSL) certificate. For more information, please see [SSL Certificates Service](https://intl.cloud.tencent.com/zh/document/product/1007).
- If you want to set threshold alarms for the performance metrics of Lighthouse resources supported by [Cloud Monitor](https://intl.cloud.tencent.com/document/product/248/32799), so that when an exception occurs, you can promptly receive a notification by WeChat, email, SMS, or phone call and take corresponding actions, you need to create an alarm policy. For more information, please see [Creating Alarm Policy](https://intl.cloud.tencent.com/document/product/248/38916).
