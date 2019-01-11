When using the CVM, you may perform various operations, such as logging in, reinstalling operating system, adjusting configuration and resetting password, etc. This document provides an overview of CVM instance and describes how to work with CVM-related products for your reference.
## Instance
[CVM Instance](https://intl.cloud.tencent.com/document/product/213/495) is also known as Cloud Virtual Machine instance. Tencent Cloud CVM instance supports customizing all resources, including CPU, memory, disk, network, security, etc. It also allows easy adjustment of the resources in case of any change in visits, load and other demands. Common features supported by CVM instance are provided as follows:

### Common operations
- [Create Instance](https://cloud.tencent.com/document/product/213/4855)

- Log in to an instance
 - [Log in to Linux Instance](https://cloud.tencent.com/document/product/213/5436)
 - [Logging in to a Windows Instance](https://cloud.tencent.com/document/product/213/5435)

- [Search for Instance](https://cloud.tencent.com/document/product/213/15519)

- [Restart Instance](https://cloud.tencent.com/document/product/213/4928)

- [Shut Down Instance](https://cloud.tencent.com/document/product/213/4929)

- [Terminate Instance](https://cloud.tencent.com/document/product/213/4930)

- [Reclaim Instance](https://cloud.tencent.com/document/product/213/4931)

### Modifying instance attributes
- [Reset Password](https://cloud.tencent.com/document/product/213/16566)

- Adjust configurations
 - [Adjust Instance Configuration](https://cloud.tencent.com/document/product/213/2178)

 - [Adjust Network Configuration](https://cloud.tencent.com/document/product/213/15517)

 - [Adjust Project Configuration](https://cloud.tencent.com/document/product/213/16514)

- [Modify Instance Name](https://cloud.tencent.com/document/product/213/16562)

- Modify IP
 - [Modify Private IP](https://cloud.tencent.com/document/product/213/16561)

 - [Modify Public IP](https://cloud.tencent.com/document/product/213/16642)

- [Change Subnet of Instance](https://cloud.tencent.com/document/product/213/16565)

- [Change Security Group](https://cloud.tencent.com/document/product/213/16564)

- [Reinstall Operating System](https://cloud.tencent.com/document/product/213/4933)

## Image
An [Image](https://intl.cloud.tencent.com/document/product/213/4940) provides all information required to launch a CVM instance. In another word, an image is the installation disk of a CVM. Tencent Cloud provides four types of images: public image, service marketplace image, custom image and shared image. Common operations supported by image are described as follows.
### Common operations
- [Create Custom Image](https://cloud.tencent.com/document/product/213/4942)

- [Delete Custom Image](https://cloud.tencent.com/document/product/213/6036)

- [Import Image](https://cloud.tencent.com/document/product/213/4945)

- [Copy Image](https://cloud.tencent.com/document/product/213/4943)

### Sharing image
- [Share Image](https://cloud.tencent.com/document/product/213/4944)

- [Cancel Image Sharing](https://cloud.tencent.com/document/product/213/7148)

## Security Group
[Security Group](https://intl.cloud.tencent.com/document/product/213/12452) is an important means of network security isolation provided by Tencent Cloud. It is a stateful virtual firewall for filtering packets and is used to set the network access controls for a single or multiple CVMs. The following describes common operations supported by security group and how to set the security group in typical scenarios to meet your business needs. Overview of common ports is provided at the end of this section for your reference.

### Common operations
- [Creating a security group](https://intl.cloud.tencent.com/document/product/213/18197#creating-a-security-group)

- [Deleting a security group](https://intl.cloud.tencent.com/document/product/213/18197#deleting-a-security-group)

- [Cloning a security group](https://intl.cloud.tencent.com/document/product/213/18197#cloning-a-security-group)

- [Adding rules to security group](https://intl.cloud.tencent.com/document/product/213/18197#adding-rules-to-security-group)

- [Configuring a security group to associate with CVM instances](https://intl.cloud.tencent.com/document/product/213/18197#configuring-a-security-group-to-associate-with-cvm-instances)

- [Importing/exporting security group rules](https://intl.cloud.tencent.com/document/product/213/18197#importing.2Fexporting-security-group-rules)

### Configuration in typical scenarios
- [Remotely Log in to Linux Instance via SSH](https://intl.cloud.tencent.com/document/product/213/18197#remotely-logging-in-to-linux-instances-via-ssh)

- [Logging in to a Windows Instance via MSTSC](https://intl.cloud.tencent.com/document/product/213/18197?#logging-in-to-windows-instances-via-mstsc)

- [Ping Public IP of Instance](https://intl.cloud.tencent.com/document/product/213/18197?#pinging-a-cvm-instance-in-public-network)

- [Use Instance as Web Server](https://intl.cloud.tencent.com/document/product/213/18197#using-cvm-instance-as-web-servers)

- [Use Instance as FTP Server](https://intl.cloud.tencent.com/document/product/213/18197#uploading-or-downloading-files-with-ftp)

- [Overview of Common Ports](https://intl.cloud.tencent.com/document/product/213/12451)

## EIP
[Elastic IP Address (EIP)](https://intl.cloud.tencent.com/document/product/213/5733) is also known as elastic IP. It is a static IP designed for dynamic cloud computing, and a fixed public IP in a certain region. With EIPs, you can quickly remap an address to another instance in your account (or NAT gateway instance) to block instance failures. Common operations supported by EIP are provided as follows.
### Common operations
- [Applying for EIPs](https://intl.cloud.tencent.com/document/product/213/5733#applying-for-eips)

- [Releasing EIPs](https://intl.cloud.tencent.com/document/product/213/5733#releasing-eips)

- [Binding instances](https://intl.cloud.tencent.com/document/product/213/5733#binding-eips-to-cloud-products)

- [Unbinding instances](https://intl.cloud.tencent.com/document/product/213/5733#unbinding-eips-from-cloud-products)

- [Adjusting bandwidth](https://intl.cloud.tencent.com/document/product/213/5733#adjusting-bandwidth)

- [Converting public IPs to EIPs](https://intl.cloud.tencent.com/document/product/213/5733#converting-public-ip-to-eip)

## SSH Key
### Common operations
- [Creating SSH keys](https://intl.cloud.tencent.com/document/product/213/16691#creating-an-ssh-key)

- [Deleting SSH keys](https://intl.cloud.tencent.com/document/product/213/16691#deleting-ssh-keys)

- [Binding/unbinding instances](https://intl.cloud.tencent.com/document/product/213/16691#binding.2Funbinding-keys-with-servers)

- [Modifying name/description](https://intl.cloud.tencent.com/document/product/213/16691#modify-ssh-key-name.2Fdescription)

- [Logging in to a Linux instance using a key](https://intl.cloud.tencent.com/document/product/213/16691#log-in-to-the-linux-cvm-using-the-ssh-key)
