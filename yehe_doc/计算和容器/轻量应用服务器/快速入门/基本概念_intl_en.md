### Instance
A Lighthouse instance is a virtual computing resource in the cloud, containing the most basic components such as CPU, OS, network, and disk. Lighthouse instances are generally suitable for supporting low-load lightweight application scenarios with a mild amount of access requests, including small websites, web applications, blogs, forums, and cloud-based development, testing, and learning environments.

### Instance Package
When you create a Lighthouse instance, the instance package you specify determines its server hardware configuration. Lighthouse provides multiple instance packages consisting of CPU, memory, SSD cloud disk, and network traffic package. The computing, memory, and storage features vary by instance package. You can select an appropriate instance package based on the scale of your application to be deployed. For more information, please see [Instance Package](https://intl.cloud.tencent.com/document/product/1103/41264).

### Image
An image is a preconfigured template that used to launch and run Lighthouse instances, which contains preinstalled OS and software applications. Lighthouse provides system and application images. You can use an image to create one or multiple instances.

### Storage
The system disks in all Lighthouse packages are Tencent Cloud SSD cloud disks, which are based on full NVMe SSD storage media and use a three-copy distributed storage mechanism to provide low-latency and high-throughput I/O capabilities with a high random IOPS and 99.9999999% data security. For more information on the SSD cloud disk performance, please see [Storage Performance Description](https://intl.cloud.tencent.com/document/product/1103/41264).

### IP Address
Tencent Cloud provides [private IPs](https://intl.cloud.tencent.com/document/product/213/5225) and [public IPs](https://intl.cloud.tencent.com/document/product/213/5224). Simply put, a private IP provides a LAN service for access between Lighthouse instances, while a public IP is used for you to access an internet service on a Lighthouse instance.

For more information on the private network connectivity between different Lighthouse instances and between Lighthouse instances and other Tencent Cloud services, please see [Private Network Connectivity Description](https://intl.cloud.tencent.com/document/product/1103/41266).

### Firewall
A firewall is an important method to protect the Lighthouse network security. It works similarly to security groups of CVM instances. You can configure firewall rules to open only certain ports on an instance so as to control the instance inbound traffic.

### Login Method
Tencent Cloud provides the following two encrypted login methods:
- **SSH key pair**: you can remotely log in to an instance after completing simple configurations in the console and local client and don't need to enter the password repeatedly in subsequent logins. This login method is more secure and reliable and can eliminate the threats of brute force attacks.
- **Login password**: any user with the instance login password can remotely log in to the corresponding Lighthouse instance at a public network address allowed by a security group.



