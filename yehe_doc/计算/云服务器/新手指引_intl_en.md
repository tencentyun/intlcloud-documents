## 1. Basic CVM Knowledge
- [CVM Overview](https://intl.cloud.tencent.com/document/product/213/495)
- [Our Advantages](https://intl.cloud.tencent.com/document/product/213/3036)
- [Use Limits Overview](https://intl.cloud.tencent.com/document/product/213/15379)
- [Concepts](https://intl.cloud.tencent.com/document/product/213/38678).


## 2. CVM Billing Modes
Tencent Cloud CVM supports the **pay-as-you-go** and **spot instance** billing modes. You need to understand the two billing modes so that you can choose the right billing solution. For more information, see [Instance Billing Modes](https://intl.cloud.tencent.com/document/product/213/2180).

## 3. Getting Started
#### 3.1 Registration and authentication
Before using Tencent Cloud CVM, you need to sign up for a [Tencent Cloud account](https://intl.cloud.tencent.com/register) and complete the [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).

#### 3.2 Purchasing CVM instances
After completing the registration and identity verification, you can flexibly select the region, model, image, public network bandwidth, purchase quantity and purchase period on the [Custom Configuration](http://manage.qcloud.com/shoppingcart/shop.php?tab=cvm&_ga=1.91351132.770173325.1571651505) page to purchase CVM instances to meet your business needs. For more information, please see: 

- [Customizing Linux CVM Configurations](https://intl.cloud.tencent.com/document/product/213/10517)

- [Customizing Windows CVM Configurations](https://intl.cloud.tencent.com/document/product/213/10516)

#### 3.3 Logging in to and using CVM instances
After you purchase CVM instances, you can log in to them to store your local files, use them as your virtual machines or build websites.
- For more information about how to log in to a CVM instance, see:
 - [Logging in to Linux Instances Using the Standard Login Method](https://intl.cloud.tencent.com/document/product/213/5436)
 - [Logging in to Windows Instances Using the RDP File (Recommended)](https://intl.cloud.tencent.com/document/product/213/5435)
- For more information about how to store local files onto a CVM instance, see [Copying Local Files to CVMs](https://intl.cloud.tencent.com/document/product/213/34821).
- For more information about how to build websites, see [Setting up a Website](https://intl.cloud.tencent.com/document/product/213/34815).


## 4. Console
The following is the overview page of the CVM console:
![](https://main.qcloudimg.com/raw/98a624ab6b2e13beb8d69b966d1e12d4.png)

## 5. Overview of Console Features

| Feature | Reference |
|---------|---------|
| Create CVM instances. | [Guidelines for Creating Instances](https://intl.cloud.tencent.com/document/product/213/36302) |
| Name instances or CVMs according to a rule. | [Batch Sequential Naming or Pattern String-Based Naming](https://intl.cloud.tencent.com/document/product/213/32020) |
| Upgrade or downgrade the CVM configurations. | [Changing Instance Configurations](https://intl.cloud.tencent.com/document/product/213/2178) |
| Select SSH key pair as the encrypted CVM login method and manage SSH keys. | [Managing SSH Keys](https://intl.cloud.tencent.com/document/product/213/16691) |
| Change or reset your instance password. | [Resetting Instance Passwords](https://intl.cloud.tencent.com/document/product/213/16566) |
| Terminate, release or return a CVM instance. | [Terminating Instances](https://intl.cloud.tencent.com/document/product/213/4930) |
| Obtain the CVM instance list of a region. | [Export Instances](https://intl.cloud.tencent.com/document/product/213/16563) |
| Search for CVM instances and other resources. | [Cross-region Search](https://intl.cloud.tencent.com/document/product/213/8668) |
| Create a custom image and use this image to start more new instances that have the same custom configurations as the original one. | [Creating Custom Images](https://intl.cloud.tencent.com/document/product/213/4942) |
| Obtain shared images from other users to get the necessary components and add custom contents. | [Sharing Custom Images](https://intl.cloud.tencent.com/document/product/213/4944) |
| Import the system disk image on local computers or other platforms to the custom image on the CVM. | [Overview](https://intl.cloud.tencent.com/document/product/213/4945) |
| Create and export a Linux image. | [Creating Linux Images](https://intl.cloud.tencent.com/document/product/213/17814) |
| Create and export a Windows image. | [Creating Windows Images](https://intl.cloud.tencent.com/document/product/213/17815) |
| Migrate systems and applications on the source servers from your IDCs or other cloud platforms to Tencent Cloud. | [Overview](https://intl.cloud.tencent.com/document/product/213/35639) |
| Expand cloud disks to increase the storage capacity. | [Expanding Cloud Disks](https://intl.cloud.tencent.com/document/product/213/32377) |
| Convert a public IP to an EIP to mask an instance failure. | [Elastic IP](https://intl.cloud.tencent.com/document/product/213/16586) |
| Create a CVM with IPv6 CIDR block and enable IPv6 for ENI, implementing the IPv6 communication over the private and public networks. | [Configuring IPv6](https://intl.cloud.tencent.com/document/product/213/34836) |
| Configure security groups based on use cases. | [Security Group Use Cases](https://intl.cloud.tencent.com/document/product/213/32369) |
| Use tags to categorize and manage your CVM resources. | [User Guide on Tags](https://intl.cloud.tencent.com/document/product/213/19548) |
| View the monitoring data of CVM instances such as the CPU, memory, network bandwidth, and disks. | [Getting Monitoring Statistics](https://intl.cloud.tencent.com/document/product/213/5178) |

## 6. FAQs

#### Regions and availability zones
- [Can I change the region of a purchased CVM?](https://intl.cloud.tencent.com/document/product/213/17276)
- [Can I change between Linux and Windows operating systems for a CVM instance purchased in a region outside the Chinese mainland?](https://intl.cloud.tencent.com/document/product/213/17276)

#### Billing
- [What are the limits for purchasing a pay-as-you-go CVM?](https://intl.cloud.tencent.com/document/product/213/17283)
- [How do I select a CVM instance that is suitable for my business?](https://intl.cloud.tencent.com/document/product/213/36781)
- [I paid for a CVM instance but the instance was not created. Why did this happen?](https://intl.cloud.tencent.com/document/product/213/36781)

#### Login and remote access
- [How can I log in to an instance running on Ubuntu as root?](https://intl.cloud.tencent.com/document/product/213/17278)
- [What do I do when I connect to my CVM instance remotely and the connection times out?](https://intl.cloud.tencent.com/document/product/213/17278)
- [What do I do if I cannot connect to my Linux instance?](https://intl.cloud.tencent.com/document/product/213/17278)
- [What do I do if I cannot connect to my Windows instance?](https://intl.cloud.tencent.com/document/product/213/17278)

#### Using cloud disks
- [How do I read and write the original NTFS data disk after the Windows operating system is reinstalled to Linux?](https://intl.cloud.tencent.com/document/product/213/37890)
- [How do I read the data disk in EXT format after the Linux operating system is reinstalled to Windows?](https://intl.cloud.tencent.com/document/product/213/37890)

#### Passwords
- [How can I obtain the initial CVM password?](https://intl.cloud.tencent.com/document/product/213/36779)
- [What are the default CVM login username and password?](https://intl.cloud.tencent.com/document/product/213/36779)
- [What should I do if I fail to reset the password?](https://intl.cloud.tencent.com/document/product/213/36779)

#### Ports
- [Which ports should be opened to the Internet before I log in to an instance?](https://intl.cloud.tencent.com/document/product/213/2502)
- [Which ports are often used in CVM?](https://intl.cloud.tencent.com/document/product/213/12451)
- [How do I unblock port 25?](https://intl.cloud.tencent.com/document/product/213/34833)

## 7. Feedback and Suggestions
If you have any doubts or suggestions when using Tencent Cloud CVM products and services, you can submit your feedback through the following channels. Dedicated personnel will contact you to solve your problems.
- To report product documentation issues such as link, content, or API errors, you can click **Send Feedback** at the bottom of the document.
- If you encounter product-related problems, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).


