## What is Tencent Cloud Lighthouse?

Tencent Cloud Lighthouse (Lighthouse) is a new-gen cloud server service for small- and medium-sized enterprises (SMEs) and developers. It features out-of-the-box service for cloud-based lightweight business scenarios, such as websites, mini games, ecommerce, cloud storage, image hosting, and various development, testing as well as learning environments. It is easier to use than traditional cloud server services and integrates common basic cloud services into bundles with different data transfer quota. Such bundles contain popular open-source software programs, enabling you to build applications swiftly and enjoy the best way to get started with Tencent Cloud.


## Why Tencent Cloud Lighthouse?

Tencent Cloud Lighthouse features the following advantages:
- One-Click App Deployment: A rich set of out-of-the-box app images and preconfigured software stacks for websites, blogs, and other application systems allow you to deploy apps in seconds.
- Easy to Use: One-stop integration of basic cloud services, including computing, storage, and network, makes creating and managing cloud servers and applications simple and intuitive.
- Cost Effective Bundles: Bundles for computing, storage, and network resources make your deployments highly cost-effective.
- Stable, reliable, and secure.

To learn more about Tencent Cloud Lighthouse, see [Strengths](https://intl.cloud.tencent.com/document/product/1103/41262) and [Use Cases](https://intl.cloud.tencent.com/document/product/1103/41263).

## Differences from CVM
For more information on the differences between Lighthouse and CVM, see [Comparison with CVM](https://intl.cloud.tencent.com/document/product/1103/41521).

## Instances

A Lighthouse instance is a virtual computing resource in the cloud, containing the most basic components such as CPU, OS, network, and disk. Lighthouse instances are generally suitable for lightweight application scenarios with a moderate number of access requests, including small websites, web applications, blogs, forums, and cloud-based development, testing, and learning environments. For more information on how to select an instance specification, see [Lighthouse Bundles](https://intl.cloud.tencent.com/document/product/1103/41264).
For scenarios like high-concurrency websites, video encoding/decoding, large-scale games, and complex distributed cluster applications, it's recommended to use CVM. CVM provides rich instance models, such as Memory Optimized, High I/O, Big Data, Bare Metal, and GPU/FPGA Heterogeneous Computing. For more information, see [CVM Instance Types](https://intl.cloud.tencent.com/document/product/213/11518).

## [Image](id:OS)
An image is a preconfigured template used for the launch and running of Lighthouse instances. It contains the preinstalled operating system and software applications. Simply put, you can consider an image as an "installation disk" for Lighthouse instance. You can use an image to create one or multiple instances.
Lighthouse provides five types of images:
<dx-tabs>
::: Application image[](id:appOS)
- **Description**
An application image provides everything you need to launch a Lighthouse instance, including the OS (CentOS and Windows Server), applications (such as LAMP, WordPress, ASP.NET, and Node.js), their runtime environments, and relevant initialization configuration files.
- **Use cases**
It is suitable for quick out-of-the-box application deployment. After a Lighthouse instance is created from an application image, the application system can be initialized automatically, and you can build the application in just a few steps of simple configuration, with no need to perform operations such as manually installing applications and uploading software packages.
- **Available images**
<ul class="params">
<li>WordPress</li>
<li>WooCommerce</li>
<li>SRS audio/video server</li>
<li>Interactive live streaming room service</li>
<li>Typecho</li>
<li>Cloudreve</li>
<li>Matomo</li>
<li>LAMP</li>
<li>Node.js</li>
<li>Theia IDE</li>
<li>Docker CE</li>
<li>K3s</li>
<li>ASP.NET</li>
</ul>

For more information on the images, please go to the <a href="https://buy.intl.cloud.tencent.com/lighthouse">Lighthouse purchase page</a>.
:::
::: System image
- **Description**
A system image contains only the initial operating system (CentOS, Ubuntu, and Windows Server). It does not have preinstalled applications, their runtime environments, and relevant initialization configuration files. 
- **Use cases**
It is suitable for users familiar with the installation and environment configuration of server operating systems and software programs. Lighthouse instances created from a system image have only the initial operating system environment installed, where you can install software programs or application systems as needed.
- **Available images**
<ul class="params">
<li>Windows Server 2022</li>
<li>Windows Server 2019</li>
<li>Windows Server 2016</li>
<li>Windows Server 2012 R2</li>
<li>TencentOS Server 3.1 (TK4)</li>
<li>TencentOS Server 2.4 (TK4)</li>
<li>CentOS 7.6</li>
<li>CentOS 8.0</li>
<li>CentOS 8.2</li>
<li>CentOS Stream 8</li>
<li>Ubuntu 18.04.1 LTS</li>
<li>Ubuntu 20.04 LTS</li>
<li>Debian 10.2</li>
<li>Debian 11.1</li>
</ul>

:::
::: Docker image[](id:DokcerOS)
- **Description**
A Docker image not only contains the operating systems (such as CentOS, Ubuntu, etc.), but also encapsulates the Docker software, operating environment and relevant configuration files by default.
- **Use cases**
It is applicable for rapid deployment of containerized applications. You can quickly create and manage Docker containers based on the Lighthouse instances using Docker basic images in the console.
- **Available images**
  - CentOS 8.2 - Docker 20
  - CentOS 7.6 - Docker 20
  - Ubuntu 20.04 - Docker 20
  

 :::
 ::: Custom Image[](id:customOS)

- **Description**
A custom image is an image created using the image creation feature and can only be used by the creator.
- **Use cases**
You can select a Lighthouse instance on which applications have already been deployed to create a custom image and use it as a template to quickly create more instances.
- **Available images**
You can create a custom image as instructed in [Working with Custom Images](https://intl.cloud.tencent.com/document/product/1103/41395).

:::
::: Shared image[](id:shareOS)

- **Description**
A shared image is an image shared from CVM to Lighthouse under the same account and in the same region.
- **Use cases**
It is applicable for fast offline migration of services between CVMs and Lighthouse instances. You can use this image to quickly create an instance, get the required components and add custom content.
- **Available images**
You can create a shared image as instructed in [Managing Shared Image](https://intl.cloud.tencent.com/document/product/1103/46403).
:::
</dx-tabs>

<dx-alert infotype="explain" title="">
You can use an image to build personal websites, forums, or other platforms as instructed in [Best Practice](https://intl.cloud.tencent.com/zh/document/product/1103/41255).
</dx-alert>

## Network

The network of Lighthouse is based on Tencent Cloud VPC, which is stable and secure.
<dx-alert infotype="explain" title="">
For more information about the networking of Lighthouse instances, [Region and Network Connectivity](https://intl.cloud.tencent.com/document/product/1103/41266).
</dx-alert>

<dx-accordion>
::: Public IP
An independent public IP is assigned to each created Lighthouse instance, and a dedicated public network bandwidth value is configured by default for access over the internet. You cannot add more public IPs or change the public IP.
:::
::: Public network bandwidth
It is the upper limit of the public network outbound bandwidth for a Lighthouse instance outside the Chinese mainland.
<dx-alert infotype="explain" title="">

- It is called "Bandwidth" in [Lighthouse Bundles](https://intl.cloud.tencent.com/document/product/1103/41264).
- For information on inbound/outbound bandwidth cap, see [Bandwidth Cap Description](https://intl.cloud.tencent.com/document/product/1103/41264#BandwidthUpperLimit).
- During peak periods, due to cross-border network congestion, the actual public network bandwidth connected from the Chinese mainland may not reach the "Bandwidth" indicated in the Lighthouse bundles.
</dx-alert>
:::
::: Private IP
- Each Lighthouse instance is assigned with one private IP for communication with other Lighthouse instances.
- Under the same account, Lighthouse instances are grouped by the region and deployed on different VPCs.
- Private network bandwidth is the bandwidth of a shared network, and there is no guarantee for its continuous stability.
- Network isolation between Lighthouse instances can be implemented by a firewall.

:::
::: Data transfer
Data transfer of a Lighthouse instance is included in the bundle. The quota of data transfer refers to the monthly upper limit on the public network outbound traffic. When the quota is used up, the excessive part is billed on the pay-as-you-go basis. For more information, see [Billing Overview](https://intl.cloud.tencent.com/document/product/1103/41403).
:::
</dx-accordion>

## Storage
Cloud Block Storage (CBS) is a cost-effective and customizable block storage device service, featuring high availability and reliability. It provides efficient and reliable storage device for Lighthouse instances. CBS provides long-term storage at the data block level. It is typically used as the primary storage device for data that requires frequent and fine-grained updates (such as file system and database). CBS uses a three-copy distributed mechanism to back up your data on different physical machines to avoid data loss caused by a single point of failure.

See below for the lifecycles of system disks and data disks.

<dx-accordion>
::: System disk
- The lifecycle of a system disk is follows the lifecycle of the bound Lighthouse instance. It is purchased with the Lighthouse, and cannot be attached or detached.
- All system disks included in Lighthouse bundles are SSDs, which are based on full NVMe SSD storage media and use a three-copy distributed storage mechanism. It features low-latency and high-throughput I/O capabilities with a high random IOPS and 99.9999999% data security.

:::
::: Data disk
- The lifecycle of a data disk is independent of a Lighthouse instance. You can purchase data disks independently and then manually attach them to or detach them from any Lighthouse instance in the same availability zone. You can attach multiple data disks to one Lighthouse instance.
- The Lighthouse data disk supports **Premium cloud disks** and **SSD cloud disks**. See [Cloud Disk Types](https://intl.cloud.tencent.com/ document/product/362/31636).
:::
</dx-accordion>





## Secure service
Anti-DDoS Basic and [Cloud Workload Protection Platform (CWPP) Basic](https://intl.cloud.tencent.com/document/product/296/2222) are activated by default for Lighthouse instances.
<dx-alert infotype="explain" title="">

- Anti-DDoS: To check the DDoS protection status, go to the [Anti-DDoS Basic](https://console.cloud.tencent.com/ddos/ddos-basic) console, and select **Lighthouse** at the top.
- CWPP Basic: To check the details , go to the CWPP console, open the [Server List](https://console.cloud.tencent.com/cwpp/asset/machine) page, and select **Lighthouse**.
</dx-alert>


## Relevant Tencent Cloud Services
- If you want to create a website and release information on the internet, you need to register a domain name.
- Bind the domain name and resolve it for accessing your website directly with the domain name.
- [SSL Certificates Service](https://intl.cloud.tencent.com/zh/document/product/1007): Install a Secure Sockets Layer (SSL) certificate to provide security features for your website such as HTTPS, identity verification, and encrypted data transfer. 
- [Cloud Monitor](https://intl.cloud.tencent.com/document/product/248/32799): Monitor performance of the Lighthouse instance, and [creating alarm policies](https://intl.cloud.tencent.com/document/product/248/38916) to receive notifications when exceptions happen by email, SMS, or phone call.
